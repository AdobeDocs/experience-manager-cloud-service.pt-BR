---
title: Pesquisa e indexação de conteúdo
description: Pesquisa e indexação de conteúdo
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 38%

---

# Pesquisa e indexação de conteúdo {#indexing}

## Alterações no AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Com o AEM as a Cloud Service, a Adobe está passando de um modelo centrado em instâncias do AEM para uma visualização baseada em serviços com containers n-x do AEM, impulsionada por pipelines de CI/CD no Cloud Manager. Em vez de configurar e manter índices em instâncias únicas do AEM, a configuração de índice deve ser especificada antes de uma implantação. As mudanças de configuração na produção estão claramente quebrando as políticas de CI/CD. O mesmo vale para as alterações de índice, pois podem afetar a estabilidade e o desempenho do sistema se não forem especificadas, testadas e reindexadas antes de serem trazidas para a produção.

Abaixo está uma lista das principais alterações em comparação ao AEM 6.5 e versões anteriores:

1. Os usuários não têm mais acesso ao Gerenciador de índice de uma instância única do AEM para depurar, configurar ou manter a indexação. Ele só será usado para desenvolvimento e implantações locais.
1. Os usuários não podem mais alterar índices em uma instância única do AEM, nem precisam se preocupar com verificações de consistência ou reindexação.
1. Em geral, as alterações de índice são iniciadas antes de entrar na produção para não contornar gateways de qualidade nos pipelines CI/CD do Cloud Manager e não afetar os KPIs de negócios em produção.
1. Todas as métricas relacionadas, incluindo o desempenho da pesquisa na produção, estão disponíveis para clientes no tempo de execução para fornecer uma visualização integral sobre os tópicos de Pesquisa e indexação.
1. Os clientes podem configurar alertas de acordo com suas necessidades.
1. Os SREs estão monitorando a integridade do sistema 24 horas por dia, 7 dias por semana, e são tomadas medidas o mais rápido possível.
1. A configuração do índice é alterada por meio de implantações. As alterações na definição do índice são configuradas como outras alterações de conteúdo.
1. A um nível elevado de AEM as a Cloud Service, com a introdução da [modelo de implantação contínua](#index-management-using-rolling-deployments), existem dois conjuntos de índices: um para a versão antiga e um para a nova versão.
1. Os clientes podem ver se o trabalho de indexação foi concluído na página de criação do Cloud Manager e recebem uma notificação quando a nova versão está pronta para receber tráfego.

Limitações:

* Atualmente, o gerenciamento de índice no AEM as a Cloud Service é compatível somente com índices do tipo `lucene`.
* Somente os analisadores padrão são compatíveis (ou seja, os analisadores enviados com o produto). Não há compatibilidade com analisadores personalizados.
* Internamente, outros índices podem ser configurados e usados para consultas. Por exemplo, consultas gravadas em relação ao índice `damAssetLucene` podem, no Skyline, ser executadas em uma versão Elasticsearch desse índice. Normalmente, essa diferença não é visível para o aplicativo e para o usuário. No entanto, certas ferramentas, como o `explain` relatório de recursos um índice diferente. Para ver as diferenças entre os índices Lucene e os índices Elastic, consulte [a documentação do Elastic no Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Os clientes não precisam e não podem configurar os índices de Elasticsearch diretamente.

## Como usar {#how-to-use}

A definição de índices pode incluir estes três casos de uso:

1. Adição de uma definição de índice de cliente.
1. Atualização de uma definição de índice existente. Essa atualização significa que uma nova versão de uma definição de índice existente é adicionada.
1. Remoção de um índice existente redundante ou obsoleto.

Para ambos os itens 1 e 2 acima, você deve criar uma definição de índice como parte da base de código personalizada no cronograma de lançamento respectivo do Cloud Manager. Para obter mais informações, consulte [Implantação da documentação as a Cloud Service do AEM](/help/implementing/deploying/overview.md).

## Nomes de índice {#index-names}

Uma definição de índice pode ser:

1. Um índice pronto para uso. Um exemplo é o `/oak:index/cqPageLucene-2`.
1. Uma personalização de um índice pronto para uso. Essas personalizações são definidas pelo cliente. Um exemplo é o `/oak:index/cqPageLucene-2-custom-1`.
1. Um índice totalmente personalizado. Um exemplo é o `/oak:index/acme.product-1-custom-2`. Para evitar colisões de nomes, o Adobe exige que os índices totalmente personalizados tenham um prefixo, por exemplo, `acme.`

Observe que tanto a personalização de um índice pronto para uso como de índices totalmente personalizados devem conter `-custom-`. Somente índices totalmente personalizados devem começar com um prefixo.

## Preparação da nova definição de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se estiver personalizando um índice pronto para uso (por exemplo, `damAssetLucene-6`, copie a definição mais recente do índice pronto para uso de uma *ambiente do Cloud Service* utilizando o gerenciador de pacotes CRX DE (`/crx/packmgr/`). Em seguida, renomeie a configuração (por exemplo, como `damAssetLucene-6-custom-1`) e adicione suas personalizações. Esse processo garante que as configurações necessárias não sejam removidas inadvertidamente. Por exemplo, o nó `tika` sob `/oak:index/damAssetLucene-6/tika` é necessário no índice personalizado do Cloud Service. Ele não existe no SDK da nuvem.

Prepare um pacote de definição de índice que contenha a definição de índice real, seguindo esse padrão de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

Que deverá ficar em `ui.apps/src/main/content/jcr_root`. Todas as definições de índice personalizadas devem ser armazenadas em `/oak:index`.

O filtro do pacote deve ser definido de modo que os índices existentes (prontos para uso) sejam retidos. No arquivo `ui.apps/src/main/content/META-INF/vault/filter.xml`, cada índice personalizado deve ser listado, por exemplo, como `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Se a versão do índice for alterada posteriormente, o filtro deverá ser ajustado.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualquer pacote de conteúdo que contenha definições de índice deve ter a seguinte propriedade definida no arquivo de propriedades do pacote de conteúdo, em `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Implantação de definições de índice {#deploying-index-definitions}

As definições de índice são marcadas como personalizadas e com controle de versão:

* A própria definição do índice (por exemplo, `/oak:index/ntBaseLucene-custom-1`)

Para implantar um índice personalizado, a definição do índice (`/oak:index/definitionname`) devem ser entregues através de `ui.apps` por meio do Git e do processo de implantação do Cloud Manager. No filtro FileVault, por exemplo, `ui.apps/src/main/content/META-INF/vault/filter.xml`, listar cada índice personalizado individualmente, por exemplo `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. A própria definição de índice personalizado é armazenada no arquivo `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`, como se segue:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

O exemplo acima contém uma configuração para o Apache Tika. O arquivo de configuração do Tika seria armazenado em `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml`.

### Configuração do projeto

Dependendo de qual versão do plug-in do pacote Jackrabbit Filevault Maven for usada, configurações adicionais no projeto serão necessárias. Ao usar a versão do plug-in do pacote Jackrabbit Filevault Maven **1.1.6** ou mais recente, então o arquivo `pom.xml` deve conter a seguinte seção na configuração do plug-in para o `filevault-package-maven-plugin`, em `configuration/validatorsSettings` (pouco antes `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

Além disso, neste caso, a `vault-validation` A versão deve ser atualizada para uma versão mais recente:

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

Em seguida, em `ui.apps.structure/pom.xml` e `ui.apps/pom.xml`, a configuração do `filevault-package-maven-plugin` deve ter `allowIndexDefinitions` e `noIntermediateSaves` ativado. A opção `noIntermediateSaves` garante que as configurações de índice sejam adicionadas com precisão.

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

Entrada `ui.apps.structure/pom.xml`, o `filters` A seção para este plug-in deve conter uma raiz de filtro, como a seguir:

```xml
<filter><root>/oak:index</root></filter>
```

Depois que a nova definição de índice é adicionada, o novo aplicativo é implantado por meio do Cloud Manager. Na implantação, dois trabalhos são iniciados e responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para criação e publicação, respectivamente. Os repositórios subjacentes são reindexados com as novas definições de índice, antes que a mudança ocorra.

### OBSERVAÇÃO

Caso observe o seguinte erro na validação do cofre de arquivos <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
Em seguida, uma das etapas a seguir pode ser seguida para corrigir o problema: <br>

1. Faça downgrade do cofre de arquivos para a versão 1.0.4 e adicione o seguinte ao pom de nível superior:

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

Veja abaixo um exemplo de onde colocar a configuração acima no pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. Desative a validação do tipo de nó. Defina a seguinte propriedade na seção jackrabbit-nodetypes da configuração do plug-in filevault:

```xml
<isDisabled>true</isDisabled>
```

Veja abaixo um exemplo de onde colocar a configuração acima no pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

>[!TIP]
>
>Para obter mais detalhes sobre a estrutura do pacote necessária para o AEM as a Cloud Service, consulte o documento [Estrutura de projeto do AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Gerenciamento de Índice usando Implantações Móveis {#index-management-using-rolling-deployments}

### O que é o gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata da adição, remoção e alteração de índices. Alterar a *definição* de um índice é uma tarefa rápida, mas aplicar essa alteração (o que geralmente é chamado de “criação de um índice” ou, para índices existentes, “reindexação”) requer tempo. Não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

### O que são implantações graduais {#what-are-rolling-deployments}

Uma implantação contínua pode reduzir o tempo de inatividade. Ela também permite atualizações sem tempo de inatividade e reversões rápidas. A versão antiga do aplicativo é executada ao mesmo tempo que a nova versão do aplicativo.

### Áreas Somente de leitura e de Leitura e gravação {#read-only-and-read-write-areas}

Determinadas áreas do repositório (partes somente de leitura) podem ser diferentes na versão antiga e na nova do aplicativo. As áreas somente de leitura do repositório normalmente são `/app` e `/libs`. No exemplo a seguir, o itálico é usado para marcar áreas somente de leitura, enquanto o negrito é usado para áreas de leitura e gravação.

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

### Gerenciamento de índice sem implantações graduais {#index-management-without-rolling-deployments}

Durante o desenvolvimento ou ao usar instalações locais, os índices podem ser adicionados, removidos ou alterados em tempo de execução. Os índices são usados quando estão disponíveis. Se um índice ainda não for usado na versão antiga do aplicativo, ele normalmente será criado durante um tempo de inatividade programado. O mesmo ocorre ao remover um índice ou ao alterar um índice existente. Ao remover um índice, ele fica indisponível quando é removido.

### Gerenciamento de índice com implantações graduais {#index-management-with-rolling-deployments}

Com implantações contínuas, não há tempo de inatividade. Por algum tempo durante uma atualização, a versão antiga (por exemplo, a versão 1) do aplicativo e a nova versão (versão 2) são executadas simultaneamente no mesmo repositório. Se a versão 1 exigir que um determinado índice esteja disponível, esse índice não deverá ser removido na versão 2. O índice deve ser removido posteriormente, por exemplo, na versão 3, quando é garantido que a versão 1 do aplicativo não estará mais em execução. Além disso, os aplicativos devem ser programados de modo que a versão 1 funcione bem, mesmo se a versão 2 estiver em execução e se os índices da versão 2 estiverem disponíveis.

Após a conclusão da atualização para a nova versão, os índices antigos podem ser coletados pela lixeira do sistema. Os índices antigos ainda podem permanecer por algum tempo, para acelerar as reversões (caso elas sejam necessárias).

A tabela a seguir mostra cinco definições de índice: o índice `cqPageLucene` é usado em ambas as versões, enquanto o índice `damAssetLucene-custom-1` é usado somente na versão 2.

>[!NOTE]
>
>A variável `<indexName>-custom-<customerVersionNumber>` é necessário para o AEM as a Cloud Service marcá-lo como uma substituição de um índice existente.

| Índice | Índice pronto para uso | Uso na versão 1 | Uso na versão 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sim | Sim | Não |
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Não | Sim |
| /oak:index/acme.product-custom-1 | Não | Sim | Não |
| /oak:index/acme.product-custom-2 | Não | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Sim |

O número da versão é incrementado sempre que o índice é alterado. Para evitar que os nomes de índice personalizados colidam com os nomes de índice do produto em si, os índices personalizados e as alterações nos índices prontos para uso devem terminar com `-custom-<number>`.

### Alterações nos índices prontos para uso {#changes-to-out-of-the-box-indexes}

Depois que o Adobe altera um índice pronto para uso, como &quot;damAssetLucene&quot; ou &quot;cqPageLucene&quot;, um novo índice chamado `damAssetLucene-2` ou `cqPageLucene-2` é criado. Ou, se o índice já tiver sido personalizado, a definição dele será mesclada com as alterações no índice pronto para uso, conforme mostrado abaixo. A mesclagem de alterações ocorre automaticamente. Isso significa que você não precisa fazer nada se um índice pronto para uso for alterado. No entanto, é possível personalizar o índice novamente mais tarde.

| Índice | Índice pronto para uso | Uso na versão 2 | Uso na versão 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Sim | Não |
| /oak:index/damAssetLucene-2-custom-1 | Sim (mesclado automaticamente de “damAssetLucene-custom-1” e “damAssetLucene-2”) | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Não |
| /oak:index/cqPageLucene-2 | Sim | Não | Sim |

### Limitações atuais {#current-limitations}

O gerenciamento de índice é compatível somente com índices do tipo `lucene`, com `compatVersion` definir como `2`. Internamente, outros índices podem ser configurados e usados para consultas, por exemplo, índices Elasticsearch. Consultas gravadas em relação ao `damAssetLucene` O índice pode, no AEM as a Cloud Service, ser executado de fato em uma versão Elasticsearch desse índice. Essa diferença é invisível para o usuário final do aplicativo, no entanto, certas ferramentas, como `explain` O recurso relata um índice diferente. Para ver as diferenças entre os índices Lucene e Elasticsearch, consulte [a documentação do Elasticsearch no Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Os clientes não podem e não precisam configurar os índices de Elasticsearch diretamente.

Somente os analisadores incorporados são compatíveis (ou seja, os analisadores enviados com o produto). Não há compatibilidade com analisadores personalizados.

Para obter o melhor desempenho operacional, os índices não devem ser excessivamente grandes. O tamanho total de todos os índices pode ser usado como guia. Se esse tamanho aumentar em mais de 100% após a adição de índices personalizados e os índices padrão forem ajustados em um ambiente de desenvolvimento, as definições de índice personalizado deverão ser ajustadas. O AEM as a Cloud Service pode impedir a implantação de índices que afetariam negativamente a estabilidade e o desempenho do sistema.

### Adicionar um índice {#adding-an-index}

Para adicionar um índice totalmente personalizado chamado `/oak:index/acme.product-custom-1`, para ser usado em uma nova versão do aplicativo e posteriores, o índice deve ser configurado da seguinte maneira:

`acme.product-1-custom-1`

Essa configuração funciona anexando um identificador personalizado ao nome do índice, seguido por um ponto (**`.`**). O identificador deve ter de 2 a 5 caracteres de comprimento.

Como descrito acima, essa configuração garante que o índice seja usado somente pela nova versão do aplicativo.

### Alterar um índice {#changing-an-index}

Quando um índice existente é alterado, um novo índice deve ser adicionado com a definição de índice alterada. Por exemplo, considere que o índice existente `/oak:index/acme.product-custom-1` seja alterado. O índice antigo é armazenado em `/oak:index/acme.product-custom-1` e o novo índice é armazenado em `/oak:index/acme.product-custom-2`.

A versão antiga do aplicativo usa a seguinte configuração:

`/oak:index/acme.product-custom-1`

A nova versão do aplicativo usa a seguinte configuração (alterada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>As definições de índice no AEM as a Cloud Service podem não corresponder totalmente às definições de índice em uma instância de desenvolvimento local. A instância de desenvolvimento não tem uma configuração Tika, enquanto instâncias do AEM as a Cloud Service têm uma. Se você personalizar um índice com uma configuração Tika, mantenha essa configuração.

### Desfazer uma alteração {#undoing-a-change}

Às vezes, uma alteração em uma definição de índice deve ser revertida. Isso pode ocorrer porque uma alteração foi feita por engano ou porque ela talvez não seja mais necessária. Por exemplo, a definição do índice `damAssetLucene-8-custom-3` foi criada por engano e já foi implantada. Por esse motivo, talvez você queira reverter para a definição de índice anterior, `damAssetLucene-8-custom-2`. Para fazer isso, adicione um índice chamado `damAssetLucene-8-custom-4` que contém a definição do índice anterior, `damAssetLucene-8-custom-2`.

### Remover um índice {#removing-an-index}

O seguinte se aplica somente a índices personalizados. Os índices de produto não podem ser removidos, pois são usados pelo AEM.

Se um índice for removido em uma versão posterior do aplicativo, você poderá definir um índice vazio (um índice vazio que nunca é usado e que não contém dados) com um novo nome. Neste exemplo, você pode nomeá-lo como `/oak:index/acme.product-custom-3`. Esse nome substitui o índice `/oak:index/acme.product-custom-2`. Depois `/oak:index/acme.product-custom-2` for removido pelo sistema, o índice vazio `/oak:index/acme.product-custom-3` pode ser removido. Um exemplo de índice vazio é:

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

Se não precisar mais de uma personalização de um índice pronto para uso, você deverá copiar a definição desse índice. Por exemplo, se você já implantou o índice `damAssetLucene-8-custom-3`, mas não precisa mais das personalizações e deseja voltar para o índice padrão (`damAssetLucene-8`), você deve adicionar um índice `damAssetLucene-8-custom-4` que contém a definição de índice de `damAssetLucene-8`.

## Otimizações de índice e consulta {#index-query-optimizations}

O Apache Jackrabbit Oak permite configurações de índice flexíveis para lidar com consultas de pesquisa com eficiência. Os índices são especialmente importantes para repositórios maiores. Certifique-se de que todas as consultas sejam apoiadas por um índice apropriado. Consultas sem um índice adequado podem ler milhares de nós, que são então registrados como um aviso.

Consulte [este documento](query-and-indexing-best-practices.md) para obter informações sobre como consultas e índices podem ser otimizados.
