---
title: Pesquisa e indexação de conteúdo
description: Pesquisa e indexação de conteúdo
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 8e978616bd1409c12e8a40eeeeb828c853faa408
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 2%

---

# Pesquisa e indexação de conteúdo {#indexing}

## Alterações no AEM como Cloud Service {#changes-in-aem-as-a-cloud-service}

Com o AEM como Cloud Service, o Adobe está saindo de um modelo centrado em instâncias AEM para uma exibição baseada em serviços com n-x AEM Containers, conduzido por pipelines de CI/CD no Cloud Manager. Em vez de configurar e manter Índices em instâncias de AEM único, a configuração de Índice deve ser especificada antes de uma implantação. As mudanças de configuração na produção estão claramente quebrando as políticas de CI/CD. O mesmo vale para as alterações de índice, pois pode afetar a estabilidade e o desempenho do sistema se não especificado for testado e reindexado antes de trazê-los para produção.

Abaixo está uma lista das principais alterações em comparação ao AEM 6.5 e versões anteriores:

1. Os usuários não terão acesso ao Gerenciador de índice de uma única Instância de AEM para depurar, configurar ou manter a indexação. Ele só é usado para desenvolvimento local e implantações no local.

1. Os usuários não alterarão Índices em uma única Instância de AEM nem precisarão se preocupar mais com verificações de consistência ou reindexação.

1. Em geral, as alterações de índice são iniciadas antes de entrar na produção para não contornar gateways de qualidade nos pipelines CI/CD do Cloud Manager e não afetar os KPIs de negócios na produção.

1. Todas as métricas relacionadas, incluindo o desempenho da pesquisa na produção, estarão disponíveis para os clientes em tempo de execução para fornecer a visualização holística sobre os tópicos de Pesquisa e indexação.

1. Os clientes poderão configurar alertas de acordo com suas necessidades.

1. Os SREs estão monitorando a integridade do sistema 24 horas por dia, 7 dias por semana, e tomarão as medidas necessárias e o mais cedo possível.

1. A configuração do índice é alterada por meio de implantações. As alterações na definição do índice são configuradas como outras alterações de conteúdo.

1. Em um alto nível no AEM como um Cloud Service, com a introdução do [Modelo de implantação Blue-Green](#index-management-using-blue-green-deployments), dois conjuntos de índices existirão: um conjunto para a versão antiga (azul) e um conjunto para a nova versão (verde).

1. Os clientes podem ver se o trabalho de indexação está concluído na página de build do Cloud Manager e receberão uma notificação quando a nova versão estiver pronta para receber tráfego.

1. Limitações: atualmente, o gerenciamento de índice no AEM como Cloud Service só é compatível com índices do tipo lucene.

## Como usar {#how-to-use}

A definição de índices pode incluir esses três casos de uso:

1. Adicionando uma nova definição de índice de cliente
1. Atualização de uma definição de índice existente. Isso significa efetivamente adicionar uma nova versão de uma definição de índice existente
1. Remoção de um índice existente redundante ou obsoleto.

Para ambos os pontos 1 e 2 acima, é necessário criar uma nova definição de índice como parte da base de código personalizada no agendamento de lançamento do Cloud Manager respectivo. Para obter mais informações, consulte a [Implantação para AEM como uma documentação do Cloud Service](/help/implementing/deploying/overview.md).

### Preparando a Nova Definição de Índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se estiver personalizando um índice pronto para uso, por exemplo `damAssetLucene-6`, copie a definição de índice pronta para uso mais recente de um *ambiente Cloud Service* e adicione suas personalizações no topo, isso garante que as configurações necessárias não sejam removidas inadvertidamente. Por exemplo, o nó `tika` em `/oak:index/damAssetLucene-6/tika` é um nó obrigatório e também deve fazer parte do índice personalizado, e não existe no SDK do Cloud.

Você precisa preparar um novo pacote de definição de índice que contenha a definição de índice real, seguindo esse padrão de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

que precisa então ficar em `ui.apps/src/main/content/jcr_root`. As pastas de sub-raiz não são compatíveis a partir de agora.

O pacote da amostra acima é criado como `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

>[!NOTE]
>
>Qualquer pacote de conteúdo que contenha definições de índice deve ter a seguinte propriedade definida no arquivo de propriedades do pacote de conteúdo, localizado em `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

### Implantação de definições de índice {#deploying-index-definitions}

>[!NOTE]
>
>Há um problema conhecido com o Jackrabbit Filevault Maven Package Plugin versão **1.1.0** que não permite adicionar `oak:index` a módulos de `<packageType>application</packageType>`. Para contornar isso, use a versão **1.0.4**.

As definições de índice agora são marcadas como personalizadas e com versão:

* A própria definição do índice (por exemplo `/oak:index/ntBaseLucene-custom-1`)

Portanto, para implantar um índice, a definição de índice (`/oak:index/definitionname`) precisa ser entregue via `ui.apps` via Git e o processo de implantação do Cloud Manager.

Depois que a nova definição de índice é adicionada, o novo aplicativo precisa ser implantado por meio do Cloud Manager. Após a implantação, dois trabalhos são iniciados, responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para autor e publicação, respectivamente. Os repositórios subjacentes estão sendo reindexados com as novas definições de índice, antes da mudança Blue-Green ocorrer.

>[!TIP]
>
>Para obter mais detalhes sobre a estrutura do pacote necessária para AEM como Cloud Service, consulte o documento [AEM Estrutura do Projeto.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gerenciamento de índice usando implantações em verde-azul {#index-management-using-blue-green-deployments}

### O que é Gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata da adição, remoção e alteração de índices. Alterar a *definição* de um índice é rápido, mas a aplicação da alteração (muitas vezes chamada de &quot;criação de índice&quot; ou, para índices existentes, &quot;reindexação&quot;) requer tempo. Não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

### O que é implantação azul-verde {#what-is-blue-green-deployment}

A implantação do Blue-Green pode reduzir o tempo de inatividade. Também permite atualizações de tempo de inatividade zero e reversões rápidas. A versão antiga do aplicativo (azul) é executada ao mesmo tempo que a nova versão do aplicativo (verde).

### Áreas somente leitura e leitura-gravação {#read-only-and-read-write-areas}

Determinadas áreas do repositório (partes somente leitura do repositório) podem ser diferentes na versão antiga (azul) e na nova (verde) do aplicativo. As áreas somente leitura do repositório normalmente são &quot;`/app`&quot; e &quot;`/libs`&quot;. No exemplo a seguir, itálico é usado para marcar áreas somente leitura, enquanto negrito é usado para áreas de leitura e gravação.

* **/**
* */apps (somente leitura)*
* **/content**
* */libs (somente leitura)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

As áreas de leitura e gravação do repositório são compartilhadas entre todas as versões do aplicativo, enquanto para cada versão do aplicativo, há um conjunto específico de `/apps` e `/libs`.

### Gerenciamento de índice sem implantação em verde-azul {#index-management-without-blue-green-deployment}

Durante o desenvolvimento ou ao usar instalações locais, os índices podem ser adicionados, removidos ou alterados no tempo de execução. Os índices são usados assim que estão disponíveis. Se um índice ainda não tiver que ser usado na versão antiga do aplicativo, ele normalmente será criado durante um tempo de inatividade programado. O mesmo ocorre ao remover um índice ou alterar um índice existente. Ao remover um índice, ele fica indisponível assim que é removido.

### Gerenciamento de índice com implantação em verde-azul {#index-management-with-blue-green-deployment}

Com implantações azul-esverdeadas, não há tempo de inatividade. No entanto, para o gerenciamento de índice, isso requer que os índices sejam usados apenas por determinadas versões do aplicativo. Por exemplo, ao adicionar um índice na versão 2 do aplicativo, você não gostaria que ele fosse usado pela versão 1 do aplicativo ainda. O inverso é o caso quando um índice é removido: um índice removido na versão 2 ainda é necessário na versão 1. Ao alterar uma definição de índice, queremos que a versão antiga do índice seja usada apenas para a versão 1 e que a nova versão do índice seja usada apenas para a versão 2.

A tabela a seguir mostra cinco definições de índice: o índice `cqPageLucene` é usado em ambas as versões, enquanto o índice `damAssetLucene-custom-1` é usado somente na versão 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` é necessário para o AEM como um Cloud Service para marcar isso como uma substituição de um índice existente.

| Índice | Índice pronto para uso | Uso na versão 1 | Uso na versão 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sim | Sim | Não |
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Não | Sim |
| /oak:index/acme.product-custom-1 | Não | Sim | Não |
| /oak:index/acme.product-custom-2 | Não | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Sim |

O número da versão é incrementado sempre que o índice é alterado. Para evitar que os nomes de índice personalizados colidam com os nomes de índice do próprio produto, os índices personalizados, bem como as alterações nos índices prontos devem terminar com `-custom-<number>`.

### Alterações nos índices prontos para uso {#changes-to-out-of-the-box-indexes}

Quando o Adobe altera um índice pronto para uso como &quot;damAssetLucene&quot; ou &quot;cqPageLucene&quot;, um novo índice chamado `damAssetLucene-2` ou `cqPageLucene-2` é criado ou, se o índice já foi personalizado, a definição de índice personalizada é mesclada com as alterações no índice pronto para uso, conforme mostrado abaixo. A mesclagem de alterações ocorre automaticamente. Isso significa que você não precisa fazer nada se um índice pronto para uso for alterado. No entanto, é possível personalizar o índice novamente mais tarde.

| Índice | Índice pronto para uso | Uso na versão 2 | Uso na versão 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Sim | Não |
| /oak:index/damAssetLucene-2-custom-1 | Sim (mesclado automaticamente de damAssetLucene-custom-1 e damAssetLucene-2) | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Não |
| /oak:index/cqPageLucene-2 | Sim | Não | Sim |

### Limitações atuais {#current-limitations}

Atualmente, o gerenciamento de índice é compatível apenas com índices do tipo `lucene`.

### Adicionar um índice {#adding-an-index}

Para adicionar um índice chamado `/oak:index/acme.product-custom-1` a ser usado em uma nova versão do aplicativo e posterior, o índice deve ser configurado da seguinte maneira:

`acme.product-1-custom-1`

Isso funciona ao anexar um identificador personalizado ao nome do índice, seguido por um ponto (**`.`**). O identificador deve ter entre 2 e 5 caracteres de comprimento.

Como acima, isso garante que o índice seja usado somente pela nova versão do aplicativo.

### Alterar um índice {#changing-an-index}

Quando um índice existente é alterado, um novo índice precisa ser adicionado com a definição de índice alterada. Por exemplo, considere que o índice existente `/oak:index/acme.product-custom-1` é alterado. O índice antigo é armazenado em `/oak:index/acme.product-custom-1` e o novo índice é armazenado em `/oak:index/acme.product-custom-2`.

A versão antiga do aplicativo usa a seguinte configuração:

`/oak:index/acme.product-custom-1`

A nova versão do aplicativo usa a seguinte configuração (alterada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>As definições de índice no AEM como Cloud Service podem não corresponder totalmente às definições de índice em uma instância de desenvolvimento local. A instância de desenvolvimento não tem uma configuração Tika, enquanto as instâncias AEM como Cloud Service têm uma. Se você personalizar um índice com uma configuração Tika, mantenha a configuração Tika.

### Desfazer uma alteração {#undoing-a-change}

Às vezes, uma alteração em uma definição de índice precisa ser revertida. As razões podem ser que uma mudança foi feita por engano, ou uma mudança já não é necessária. Por exemplo, a definição de índice `damAssetLucene-8-custom-3` foi criada por engano e já está implantada. Por causa disso, você pode querer reverter para a definição de índice anterior `damAssetLucene-8-custom-2`. Para fazer isso, você precisa adicionar um novo índice chamado `damAssetLucene-8-custom-4` que contenha a definição do índice anterior, `damAssetLucene-8-custom-2`.

### Remover um índice {#removing-an-index}

O seguinte se aplica somente a índices personalizados. Os índices de produto não podem ser removidos, pois são usados pelo AEM.

Se um índice deve ser removido em uma versão posterior do aplicativo, você pode definir um índice vazio (um índice vazio que nunca é usado e não contém dados), com um novo nome. Para o propósito deste exemplo, você pode nomeá-lo `/oak:index/acme.product-custom-3`. Isso substitui o índice `/oak:index/acme.product-custom-2`. Depois que `/oak:index/acme.product-custom-2` for removido pelo sistema, o índice vazio `/oak:index/acme.product-custom-3` também poderá ser removido. Um exemplo desse índice vazio é:

```xml
<acme.product-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
    </acme.product-custom-3>
```

Se não for mais necessário ter uma personalização de um índice pronto para uso, você deverá copiar a definição de índice pronta para uso. Por exemplo, se você já implantou `damAssetLucene-8-custom-3`, mas não precisa mais das personalizações e deseja voltar ao índice `damAssetLucene-8` padrão, é necessário adicionar um índice `damAssetLucene-8-custom-4` que contenha a definição de índice `damAssetLucene-8`.

## Otimizações de índice

O Apache Jackrabbit Oak permite configurações de índice flexíveis para lidar com consultas de pesquisa com eficiência. Embora as otimizações de índice possam não desempenhar um papel importante para projetos de pequeno a médio porte, é imperativo que os projetos com repositórios de conteúdo de grande porte e maior velocidade de conteúdo realizem melhorias de eficiência direcionadas para indexação. Os índices não otimizados e os índices de fallback devem ser evitados o máximo possível. É recomendável tomar etapas proativas para garantir que índices adequados e otimizados estejam disponíveis para todas as suas consultas no AEM. Na ausência de um índice adequado, as consultas atravessam todo o repositório - essas consultas devem ser identificadas ao analisar os arquivos de log para otimizar as definições de índice adequadamente, pois uma consulta de travessia do repositório é o método de consulta menos eficiente na AEM. Consulte [esta página](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes) para obter mais informações.

### Índice de texto completo do Lucene no AEM como Cloud Service

O índice de texto completo lucene2, indexa todo o conteúdo no repositório de AEM por padrão e, portanto, é extremamente ineficiente devido ao tamanho dependente do repositório. O índice de texto completo do Lucene foi preterido internamente e não será mais implantado em AEM como Cloud Service a partir de setembro de 2021. Dessa forma, ele não é mais usado no lado do produto no AEM como um Cloud Service e não deve ser necessário executar o código do cliente. Para AEM como um ambiente de Cloud Service com índices comuns do Lucene, o Adobe está trabalhando com os clientes individualmente para obter uma abordagem coordenada para compensar esse índice e usar índices melhores e otimizados. Se, ao contrário de todas as expectativas, um índice de texto completo for realmente necessário para executar consultas no código personalizado, a definição de índice analógica para o índice Lucene deve ser criada com um nome diferente para evitar conflitos na manutenção.
Essa otimização não se aplica a outros ambientes AEM, que são hospedados no local ou gerenciados pelo Adobe Managed Services, a menos que o Adobe o aconselhasse de outra forma.
