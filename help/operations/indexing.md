---
title: Pesquisa e indexação de conteúdo
description: Pesquisa e indexação de conteúdo
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: e03e15c18e3013a309ee59678ec4024df072e839
workflow-type: tm+mt
source-wordcount: '2366'
ht-degree: 1%

---

# Pesquisa e indexação de conteúdo {#indexing}

## Mudanças AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Com AEM as a Cloud Service, o Adobe está mudando de um modelo centrado em instâncias AEM para uma exibição baseada em serviços com n-x AEM Containers, impulsionado por pipelines de CI/CD no Cloud Manager. Em vez de configurar e manter Índices em instâncias de AEM único, a configuração de Índice deve ser especificada antes de uma implantação. As mudanças de configuração na produção estão claramente quebrando as políticas de CI/CD. O mesmo vale para as alterações de índice, pois pode afetar a estabilidade e o desempenho do sistema se não especificado for testado e reindexado antes de trazê-los para produção.

Abaixo está uma lista das principais alterações em comparação ao AEM 6.5 e versões anteriores:

1. Os usuários não terão acesso ao Gerenciador de índice de uma única Instância de AEM para depurar, configurar ou manter a indexação. Ele só é usado para desenvolvimento local e implantações no local.

1. Os usuários não alterarão Índices em uma única Instância de AEM nem precisarão se preocupar mais com verificações de consistência ou reindexação.

1. Em geral, as alterações de índice são iniciadas antes de entrar na produção para não contornar gateways de qualidade nos pipelines CI/CD do Cloud Manager e não afetar os KPIs de negócios na produção.

1. Todas as métricas relacionadas, incluindo o desempenho da pesquisa na produção, estarão disponíveis para os clientes em tempo de execução para fornecer a visualização holística sobre os tópicos de Pesquisa e indexação.

1. Os clientes poderão configurar alertas de acordo com suas necessidades.

1. Os SREs estão monitorando a integridade do sistema 24 horas por dia, 7 dias por semana, e tomarão as medidas necessárias e o mais cedo possível.

1. A configuração do índice é alterada por meio de implantações. As alterações na definição do índice são configuradas como outras alterações de conteúdo.

1. A um alto nível em AEM as a Cloud Service, com a introdução da [Modelo de implantação azul-verde](#index-management-using-blue-green-deployments) dois conjuntos de índices existirão: um conjunto para a versão antiga (azul) e um conjunto para a nova versão (verde).

1. Os clientes podem ver se o trabalho de indexação está concluído na página de build do Cloud Manager e receberão uma notificação quando a nova versão estiver pronta para receber tráfego.

1. Limitações:
* Atualmente, o gerenciamento de índice em AEM as a Cloud Service é compatível somente com índices do tipo `lucene`.
* Somente os analisadores padrão são suportados (ou seja, aqueles enviados com o produto). Não há suporte para analisadores personalizados.
* Internamente, outros índices podem ser configurados e usados para consultas. Por exemplo, consultas gravadas em relação à variável `damAssetLucene` O índice pode, no Skyline, de fato, ser executado em uma versão Elasticsearch desse índice. Normalmente, essa diferença não é visível para o aplicativo e para o usuário, no entanto, certas ferramentas, como a variável `explain` reportará um índice diferente. Para obter diferenças entre os índices Lucene e os índices elásticos, consulte [a documentação elástica no Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Os clientes não precisam e não podem configurar os índices de Elasticsearch diretamente.

## Como usar {#how-to-use}

A definição de índices pode incluir estes três casos de uso:

1. Adicionando uma nova definição de índice de cliente.
1. Atualização de uma definição de índice existente. Isso significa efetivamente adicionar uma nova versão de uma definição de índice existente.
1. Remoção de um índice existente redundante ou obsoleto.

Para ambos os pontos 1 e 2 acima, é necessário criar uma nova definição de índice como parte da base de código personalizada no agendamento de lançamento do Cloud Manager respectivo. Para obter mais informações, consulte o [Implantação em AEM documentação as a Cloud Service](/help/implementing/deploying/overview.md).

## Nomes de Índice {#index-names}

Uma definição de índice pode ser:

1. Um índice pronto para uso. Um exemplo é `/oak:index/cqPageLucene-2`.
1. Uma personalização de um índice pronto para uso. Essas personalizações são definidas pelo cliente. Um exemplo é `/oak:index/cqPageLucene-2-custom-1`.
1. Um índice totalmente personalizado. Um exemplo é `/oak:index/acme.product-1-custom-2`. Para evitar nomear colisões, é necessário que os índices totalmente personalizados tenham um prefixo, por exemplo `acme.`

Observe que a personalização de um índice pronto para uso, bem como os índices totalmente personalizados, precisam conter `-custom-`. Somente índices totalmente personalizados devem começar com um prefixo .

### Preparando a Nova Definição de Índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se estiver personalizando um índice pronto para uso, por exemplo `damAssetLucene-6`, copie a definição de índice mais recente pronta para uso de uma *Ambiente Cloud Service* Além disso, adicione suas personalizações no topo, isso garante que as configurações necessárias não sejam removidas inadvertidamente. Por exemplo, a variável `tika` nó abaixo `/oak:index/damAssetLucene-6/tika` O é um nó obrigatório e também deve fazer parte do índice personalizado, e não existe no SDK do Cloud.

Você precisa preparar um novo pacote de definição de índice que contenha a definição de índice real, seguindo esse padrão de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

, que deverá ser `ui.apps/src/main/content/jcr_root`. As pastas de sub-raiz não são compatíveis a partir de agora.

O pacote da amostra acima é criado como `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

>[!NOTE]
>
>Qualquer pacote de conteúdo que contenha definições de índice deve ter a seguinte propriedade definida no arquivo de propriedades do pacote de conteúdo, localizado em `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

### Implantação de definições de índice {#deploying-index-definitions}

>[!NOTE]
>
>Há um problema conhecido com a versão do plug-in do pacote Jackrabbit Filevault Maven **1.1.0** que não permite adicionar `oak:index` aos módulos de `<packageType>application</packageType>`. Você deve atualizar para uma versão mais recente desse plug-in.

As definições de índice agora são marcadas como personalizadas e com versão:

* A própria definição do índice (por exemplo, `/oak:index/ntBaseLucene-custom-1`)

Portanto, para implantar um índice, a definição do índice (`/oak:index/definitionname`) precisa ser entregue via `ui.apps` por meio do Git e do processo de implantação do Cloud Manager.

Depois que a nova definição de índice é adicionada, o novo aplicativo precisa ser implantado por meio do Cloud Manager. Após a implantação, dois trabalhos são iniciados, responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para autor e publicação, respectivamente. Os repositórios subjacentes estão sendo reindexados com as novas definições de índice, antes da mudança Blue-Green ocorrer.

>[!TIP]
>
>Para obter mais detalhes sobre a estrutura do pacote necessária para AEM as a Cloud Service, consulte o documento [AEM Estrutura do projeto.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gerenciamento de índice usando implantações em verde-azul {#index-management-using-blue-green-deployments}

### O que é Gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata da adição, remoção e alteração de índices. Alteração do *definição* de um índice é rápido, mas a aplicação da alteração (muitas vezes chamada de &quot;criação de um índice&quot; ou, para índices existentes, &quot;reindexação&quot;) requer tempo. Não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

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

As áreas de leitura e gravação do repositório são compartilhadas entre todas as versões do aplicativo, enquanto para cada versão do aplicativo há um conjunto específico de `/apps` e `/libs`.

### Gerenciamento de índice sem implantação em verde-azul {#index-management-without-blue-green-deployment}

Durante o desenvolvimento ou ao usar instalações locais, os índices podem ser adicionados, removidos ou alterados no tempo de execução. Os índices são usados assim que estão disponíveis. Se um índice ainda não tiver que ser usado na versão antiga do aplicativo, ele normalmente será criado durante um tempo de inatividade programado. O mesmo ocorre ao remover um índice ou alterar um índice existente. Ao remover um índice, ele fica indisponível assim que é removido.

### Gerenciamento de índice com implantação em verde-azul {#index-management-with-blue-green-deployment}

Com implantações azul-esverdeadas, não há tempo de inatividade. Durante uma atualização, por algum tempo, a versão antiga (por exemplo, a versão 1) do aplicativo, bem como a nova versão (versão 2), estão sendo executadas simultaneamente, no mesmo repositório. Se a versão 1 exigir que um determinado índice esteja disponível, esse índice não deverá ser removido na versão 2: o índice deve ser removido posteriormente, por exemplo, na versão 3, em que é garantido que a versão 1 do aplicativo não está mais em execução. Além disso, os aplicativos devem ser escritos de modo que a versão 1 funcione bem, mesmo se a versão 2 estiver em execução e se os índices da versão 2 estiverem disponíveis.

Após a conclusão da atualização para a nova versão, os índices antigos podem ser coletados pela lixeira do sistema. Os índices antigos ainda podem permanecer por algum tempo, para acelerar as reversões (caso uma reversão deva ser necessária).

A tabela a seguir mostra cinco definições de índice: index `cqPageLucene` é usada em ambas as versões enquanto o índice `damAssetLucene-custom-1` é usada somente na versão 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` é necessário para AEM as a Cloud Service marcar isso como uma substituição de um índice existente.

| Índice | Índice pronto para uso | Uso na versão 1 | Uso na versão 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sim | Sim | Não |
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Não | Sim |
| /oak:index/acme.product-custom-1 | Não | Sim | Não |
| /oak:index/acme.product-custom-2 | Não | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Sim |

O número da versão é incrementado sempre que o índice é alterado. Para evitar que os nomes de índice personalizados colidam com os nomes de índice do próprio produto, os índices personalizados, bem como as alterações nos índices prontos para uso, devem terminar com `-custom-<number>`.

### Alterações nos índices prontos para uso {#changes-to-out-of-the-box-indexes}

Uma vez o Adobe altera um índice pronto para uso como &quot;damAssetLucene&quot; ou &quot;cqPageLucene&quot;, um novo índice chamado `damAssetLucene-2` ou `cqPageLucene-2` for criado ou, se o índice já tiver sido personalizado, a definição do índice personalizado será mesclada com as alterações no índice pronto para uso, conforme mostrado abaixo. A mesclagem de alterações ocorre automaticamente. Isso significa que você não precisa fazer nada se um índice pronto para uso for alterado. No entanto, é possível personalizar o índice novamente mais tarde.

| Índice | Índice pronto para uso | Uso na versão 2 | Uso na versão 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Sim | Não |
| /oak:index/damAssetLucene-2-custom-1 | Sim (mesclado automaticamente de damAssetLucene-custom-1 e damAssetLucene-2) | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Não |
| /oak:index/cqPageLucene-2 | Sim | Não | Sim |

### Limitações atuais {#current-limitations}

Atualmente, o gerenciamento de índice é compatível apenas com índices do tipo `lucene`. Internamente, outros índices podem ser configurados e usados para consultas, por exemplo, índices elásticos.

### Adicionar um índice {#adding-an-index}

Para adicionar um índice totalmente personalizado chamado `/oak:index/acme.product-custom-1` para ser usado em uma nova versão do aplicativo e posterior, o índice deve ser configurado da seguinte maneira:

`acme.product-1-custom-1`

Funciona ao anexar um identificador personalizado ao nome do índice, seguido por um ponto (**`.`**). O identificador deve ter entre 2 e 5 caracteres de comprimento.

Como acima, isso garante que o índice seja usado somente pela nova versão do aplicativo.

### Alterar um índice {#changing-an-index}

Quando um índice existente é alterado, um novo índice precisa ser adicionado com a definição de índice alterada. Por exemplo, considere o índice existente `/oak:index/acme.product-custom-1` é alterada. O índice antigo é armazenado em `/oak:index/acme.product-custom-1`e o novo índice é armazenado em `/oak:index/acme.product-custom-2`.

A versão antiga do aplicativo usa a seguinte configuração:

`/oak:index/acme.product-custom-1`

A nova versão do aplicativo usa a seguinte configuração (alterada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>As definições de índice em AEM as a Cloud Service podem não corresponder totalmente às definições de índice em uma instância de desenvolvimento local. A instância de desenvolvimento não tem uma configuração Tika, enquanto AEM instâncias as a Cloud Service têm uma. Se você personalizar um índice com uma configuração Tika, mantenha a configuração Tika.

### Desfazer uma alteração {#undoing-a-change}

Às vezes, uma alteração em uma definição de índice precisa ser revertida. As razões podem ser que uma mudança foi feita por engano, ou uma mudança já não é necessária. Por exemplo, a definição do índice `damAssetLucene-8-custom-3` foi criada por engano e já está implantada. Por esse motivo, talvez você queira reverter para a definição de índice anterior `damAssetLucene-8-custom-2`. Para fazer isso, você precisa adicionar um novo índice chamado `damAssetLucene-8-custom-4` que contém a definição do índice anterior, `damAssetLucene-8-custom-2`.

### Remover um índice {#removing-an-index}

O seguinte se aplica somente a índices personalizados. Os índices de produto não podem ser removidos, pois são usados pelo AEM.

Se um índice deve ser removido em uma versão posterior do aplicativo, você pode definir um índice vazio (um índice vazio que nunca é usado e não contém dados), com um novo nome. Para o propósito deste exemplo, você pode nomeá-lo `/oak:index/acme.product-custom-3`. Isso substitui o índice `/oak:index/acme.product-custom-2`. Uma vez `/oak:index/acme.product-custom-2` for removido pelo sistema, o índice vazio `/oak:index/acme.product-custom-3` também pode ser removido. Um exemplo desse índice vazio é:

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

Se não for mais necessário ter uma personalização de um índice pronto para uso, você deverá copiar a definição de índice pronta para uso. Por exemplo, se você já implantou o `damAssetLucene-8-custom-3`, mas não precisa mais das personalizações e deseja voltar para o padrão `damAssetLucene-8` , em seguida, você deve adicionar um índice `damAssetLucene-8-custom-4` que contém a definição de índice de `damAssetLucene-8`.

## Otimizações de índice {#index-optimizations}

O Apache Jackrabbit Oak permite configurações de índice flexíveis para lidar com consultas de pesquisa com eficiência. Os índices são especialmente importantes para repositórios maiores. Certifique-se de que todas as consultas sejam apoiadas por um índice adequado. Consultas sem um índice adequado podem ler milhares de nós, que são registrados como um aviso. Essas consultas devem ser identificadas ao analisar os arquivos de log, para que as definições de índice possam ser otimizadas. Consulte [esta página](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes) para obter mais informações.

### Índice de texto completo do Lucene em AEM as a Cloud Service {#index-lucene}

O índice de texto completo `/oak:index/lucene-2` pode se tornar muito grande porque indexa todos os nós no repositório de AEM por padrão.  Após os planos da Adobe para desativar esse índice, ele não será mais usado no lado do produto AEM as a Cloud Service e não deverá ser necessário executar o código do cliente. Para AEM ambientes as a Cloud Service com índices comuns do Lucene, o Adobe está trabalhando com os clientes individualmente para obter uma abordagem coordenada para compensar esse índice e usar índices melhores e otimizados. Os clientes não necessitam de qualquer ação sem aviso prévio da Adobe. AEM clientes as a Cloud Service serão informados pelo Adobe quando houver necessidade de ação em relação a essa otimização. Se esse índice for necessário para consultas personalizadas, como uma solução temporária, uma cópia desse índice deverá ser criada usando um nome diferente, por exemplo, `/oak:index/acme.lucene-1-custom-1`, conforme descrito [here](/help/operations/indexing.md).
Essa otimização não se aplica por padrão a outros ambientes de AEM hospedados no local ou gerenciados pelo Adobe Managed Services.

## Otimizações de consulta {#index-query}

O **Desempenho da consulta** A ferramenta permite observar queries JCR populares e lentas. Além disso, é possível analisar consultas e exibir várias informações sobre o , principalmente se um índice estiver sendo usado ou não para essa consulta.

Ao contrário do AEM no local, AEM as a Cloud Service não exibe a variável **Desempenho da consulta** na interface do usuário. Em vez disso, agora está disponível por meio do Console do desenvolvedor (no Cloud Manager) na [Queries](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) guia .
