---
title: Pesquisa e indexação de conteúdo
description: Pesquisa e indexação de conteúdo
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 6fd5f8e7a9699f60457e232bb3cfa011f34880e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 88%

---

# Pesquisa e indexação de conteúdo {#indexing}

## Alterações no AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Com o AEM as a Cloud Service, a Adobe está passando de um modelo centrado em instâncias do AEM para uma visualização baseada em serviços com containers n-x do AEM, impulsionada por pipelines de CI/CD no Cloud Manager. Em vez de configurar e manter índices em instâncias únicas do AEM, a configuração de índice deve ser especificada antes de uma implantação. As mudanças de configuração na produção estão claramente quebrando as políticas de CI/CD. O mesmo vale para as alterações de índice, pois podem afetar a estabilidade e o desempenho do sistema se não forem especificadas, testadas e reindexadas antes de serem trazidas para a produção.

Abaixo está uma lista das principais alterações em comparação ao AEM 6.5 e versões anteriores:

1. Os usuários não terão mais acesso ao Gerenciador de índice de uma instância única do AEM para depurar, configurar ou manter a indexação. Ele só será usado para desenvolvimento e implantações locais.
1. Os usuários não poderão mais alterar índices em uma instância única do AEM, nem precisarão se preocupar com verificações de consistência ou reindexação.
1. Em geral, as alterações de índice são iniciadas antes de entrar na produção, para não contornar gateways de qualidade nos pipelines CI/CD do Cloud Manager e não afetar os KPIs de negócios em produção.
1. Todas as métricas relacionadas, incluindo o desempenho da pesquisa na produção, estarão disponíveis para os clientes durante o tempo de execução para fornecer uma visualização integral sobre os tópicos de pesquisa e indexação.
1. Os clientes poderão configurar alertas de acordo com suas necessidades.
1. Os SREs estão monitorando a integridade do sistema 24 horas por dia, 7 dias por semana, e tomarão as medidas necessárias assim que possível.
1. A configuração do índice é alterada por meio de implantações. As alterações na definição do índice são configuradas como outras alterações de conteúdo.
1. Em alto nível no AEM as a Cloud Service, com a introdução do [Modelo de implantação azul-verde](#index-management-using-blue-green-deployments), dois conjuntos de índices existirão: um conjunto para a versão antiga (azul) e um conjunto para a nova versão (verde).
1. Os clientes poderão ver se o trabalho de indexação foi concluído na página de criação do Cloud Manager e serão notificados quando a nova versão estiver pronta para receber tráfego.

Limitações:

* Atualmente, o gerenciamento de índice no AEM as a Cloud Service é compatível somente com índices do tipo `lucene`.
* Somente os analisadores padrão são compatíveis (ou seja, aqueles enviados com o produto). Não há compatibilidade com analisadores personalizados.
* Internamente, outros índices podem ser configurados e usados para consultas. Por exemplo, consultas gravadas em relação ao índice `damAssetLucene` podem, no Skyline, ser executadas em uma versão Elasticsearch desse índice. Normalmente, essa diferença não é visível para o aplicativo e para o usuário. No entanto, certas ferramentas, como o recurso `explain`, relatarão um índice diferente. Para ver as diferenças entre os índices Lucene e os índices Elastic, consulte [a documentação do Elastic no Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Os clientes não precisam e não podem configurar os índices de Elasticsearch diretamente.

## Como usar {#how-to-use}

A definição de índices pode incluir estes três casos de uso:

1. Adição de uma nova definição de índice de cliente.
1. Atualização de uma definição de índice existente. Isso significa adicionar uma nova versão de uma definição de índice existente.
1. Remoção de um índice existente redundante ou obsoleto.

Para ambos os itens 1 e 2 acima, é necessário criar uma nova definição de índice como parte da base de código personalizada no cronograma de lançamento respectivo do Cloud Manager. Para obter mais informações, consulte a [Documentação de implantação do AEM as a Cloud Service](/help/implementing/deploying/overview.md).

## Nomes de índice {#index-names}

Uma definição de índice pode ser:

1. Um índice pronto para uso. Um exemplo é o `/oak:index/cqPageLucene-2`.
1. Uma personalização de um índice pronto para uso. Essas personalizações são definidas pelo cliente. Um exemplo é o `/oak:index/cqPageLucene-2-custom-1`.
1. Um índice totalmente personalizado. Um exemplo é o `/oak:index/acme.product-1-custom-2`. Para evitar colisões de nomes, é necessário que os índices totalmente personalizados tenham um prefixo, por exemplo, `acme.`

Observe que tanto a personalização de um índice pronto para uso como de índices totalmente personalizados precisam conter `-custom-`. Somente índices totalmente personalizados devem começar com um prefixo.

## Preparação da nova definição de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se estiver personalizando um índice pronto para uso (por exemplo, `damAssetLucene-6`), copie a definição mais recente do índice pronto para uso de um *ambiente do Cloud Service* usando o gerenciador de pacotes CRX DE (`/crx/packmgr/`). Em seguida, renomeie a configuração (por exemplo, como `damAssetLucene-6-custom-1`) e adicione suas personalizações. Isso garante que as configurações necessárias não sejam removidas inadvertidamente. Por exemplo, o nó `tika` sob `/oak:index/damAssetLucene-6/tika` é necessário no índice personalizado do Cloud Service. Ele não existe no SDK da nuvem.

Você precisa preparar um novo pacote de definição de índice que contenha a definição de índice real, seguindo esse padrão de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

que deverá ficar em `ui.apps/src/main/content/jcr_root`. Todas as definições de índice personalizadas precisam ser armazenadas em `/oak:index`.

O filtro do pacote precisa ser definido de maneira que os índices existentes (prontos para uso) sejam retidos. No arquivo `ui.apps/src/main/content/META-INF/vault/filter.xml`, cada índice personalizado precisa ser listado. Por exemplo, como `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Se a versão do índice for alterada posteriormente, o filtro precisará ser ajustado.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualquer pacote de conteúdo que contenha definições de índice deve ter a seguinte propriedade definida no arquivo de propriedades do pacote de conteúdo, localizado em `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Implantação de definições de índice {#deploying-index-definitions}

As definições de índice são marcadas como personalizadas e com controle de versão:

* A própria definição do índice (por exemplo, `/oak:index/ntBaseLucene-custom-1`)

Para implantar um índice personalizado, a definição do índice (`/oak:index/definitionname`) precisa ser entregue via `ui.apps` por meio do Git e do processo de implantação do Cloud Manager. No filtro FileVault, por exemplo, `ui.apps/src/main/content/META-INF/vault/filter.xml`, listar cada índice personalizado individualmente, por exemplo `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. A própria definição de índice personalizado será armazenada no arquivo `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`, como demonstrado a seguir:

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

Dependendo de qual versão do plug-in do pacote Jackrabbit Filevault Maven for usada, configurações adicionais no projeto serão necessárias. Ao usar a versão **1.1.6** ou mais recente do plug-in do pacote Jackrabbit Filevault Maven, o arquivo `pom.xml` precisa conter a seguinte seção na configuração do plug-in para o `filevault-package-maven-plugin`, em `configuration/validatorsSettings` (antes de `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

Além disso, nesse caso, a versão de `vault-validation` precisa ser atualizada para uma versão mais recente:

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

Em seguida, em `ui.apps.structure/pom.xml` e `ui.apps/pom.xml`, a configuração do `filevault-package-maven-plugin` precisa ter as opções `allowIndexDefinitions` e `noIntermediateSaves` ativadas. A opção `noIntermediateSaves` garante que as configurações de índice sejam adicionadas com precisão.

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

Em `ui.apps.structure/pom.xml`, a seção `filters` desse plug-in precisa conter uma raiz de filtro, como demonstrado a seguir:

```xml
<filter><root>/oak:index</root></filter>
```

Depois que a nova definição de índice é adicionada, o novo aplicativo precisa ser implantado por meio do Cloud Manager. Após a implantação, dois trabalhos são iniciados, responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para criação e publicação, respectivamente. Os repositórios subjacentes estão sendo reindexados com as novas definições de índice, antes da mudança azul-verde ocorrer.

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
>Para obter mais detalhes sobre a estrutura do pacote necessária para o AEM as a Cloud Service, consulte o documento [Estrutura de projeto do AEM.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gerenciamento de índice usando implantações azul-verde {#index-management-using-blue-green-deployments}

### O que é o gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata da adição, remoção e alteração de índices. Alterar a *definição* de um índice é uma tarefa rápida, mas aplicar essa alteração (o que geralmente é chamado de “criação de um índice” ou, para índices existentes, “reindexação”) requer tempo. Esse processo não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

### O que é a implantação azul-verde {#what-is-blue-green-deployment}

A implantação azul-verde pode reduzir o tempo de inatividade. Ela também permite atualizações sem tempo de inatividade e reversões rápidas. A versão antiga do aplicativo (azul) é executada ao mesmo tempo que a nova versão (verde).

### Áreas Somente de leitura e de Leitura e gravação {#read-only-and-read-write-areas}

Determinadas áreas do repositório (partes somente de leitura) podem ser diferentes na versão antiga (azul) e na versão nova (verde) do aplicativo. As áreas somente de leitura do repositório normalmente são “`/app`” e “`/libs`”. No exemplo a seguir, o itálico é usado para marcar áreas somente de leitura, enquanto o negrito é usado para áreas de leitura e gravação.

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

### Gerenciamento de índice sem a implantação azul-verde {#index-management-without-blue-green-deployment}

Durante o desenvolvimento, ou ao usar instalações locais, os índices podem ser adicionados, removidos ou alterados em tempo de execução. Os índices são usados assim que ficam disponíveis. Se um índice ainda não deve ser usado na versão antiga do aplicativo, ele normalmente é criado durante um tempo de inatividade agendado. O mesmo ocorre ao remover um índice ou ao alterar um índice existente. Ao remover um índice, ele fica indisponível assim que é removido.

### Gerenciamento de índice com a implantação azul-verde {#index-management-with-blue-green-deployment}

Com implantações azul-verde, não há tempo de inatividade. Durante uma atualização, por algum tempo, a versão antiga (por exemplo, a versão 1) do aplicativo e a nova versão (versão 2) são executadas simultaneamente, no mesmo repositório. Se a versão 1 exigir que um determinado índice esteja disponível, esse índice não deverá ser removido na versão 2: o índice deve ser removido posteriormente, por exemplo, na versão 3, pois nesse momento é garantido que a versão 1 do aplicativo não estará mais em execução. Além disso, os aplicativos devem ser programados de modo que a versão 1 funcione bem, mesmo se a versão 2 estiver em execução e se os índices da versão 2 estiverem disponíveis.

Após a conclusão da atualização para a nova versão, os índices antigos podem ser coletados pela lixeira do sistema. Os índices antigos ainda podem permanecer por algum tempo, para acelerar as reversões (caso elas sejam necessárias).

A tabela a seguir mostra cinco definições de índice: o índice `cqPageLucene` é usado em ambas as versões, enquanto o índice `damAssetLucene-custom-1` é usado somente na versão 2.

>[!NOTE]
>
>É necessário usar `<indexName>-custom-<customerVersionNumber>` para que o AEM as a Cloud Service possa marcar isso como uma substituição de um índice existente.

| Índice | Índice pronto para uso | Uso na versão 1 | Uso na versão 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sim | Sim | Não |
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Não | Sim |
| /oak:index/acme.product-custom-1 | Não | Sim | Não |
| /oak:index/acme.product-custom-2 | Não | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Sim |

O número da versão é incrementado sempre que o índice é alterado. Para evitar que os nomes de índice personalizados colidam com os nomes de índice do produto em si, os índices personalizados, bem como as alterações nos índices prontos para uso, devem terminar com `-custom-<number>`.

### Alterações nos índices prontos para uso {#changes-to-out-of-the-box-indexes}

Quando a Adobe altera um índice pronto para uso, como “damAssetLucene” ou “cqPageLucene”, um novo índice chamado `damAssetLucene-2` ou `cqPageLucene-2` é criado ou, se o índice já tiver sido personalizado, a definição desse índice é mesclada com as alterações no índice pronto para uso, conforme mostrado abaixo. A mesclagem de alterações ocorre automaticamente. Isso significa que você não precisa fazer nada se um índice pronto para uso for alterado. No entanto, é possível personalizar o índice novamente mais tarde.

| Índice | Índice pronto para uso | Uso na versão 2 | Uso na versão 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Sim | Não |
| /oak:index/damAssetLucene-2-custom-1 | Sim (mesclado automaticamente de “damAssetLucene-custom-1” e “damAssetLucene-2”) | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Não |
| /oak:index/cqPageLucene-2 | Sim | Não | Sim |

### Limitações atuais {#current-limitations}

No momento, o gerenciamento de índice é compatível apenas com índices do tipo `lucene`, com `compatVersion` definir como `2`. Internamente, outros índices podem ser configurados e usados para consultas, por exemplo, índices Elasticsearch. Consultas gravadas em relação ao `damAssetLucene` O índice pode, no AEM as a Cloud Service, ser executado de fato em uma versão Elasticsearch desse índice. Essa diferença é invisível para o usuário final do aplicativo, no entanto, certas ferramentas, como `explain` O recurso informará um índice diferente. Para ver as diferenças entre os índices Lucene e Elasticsearch, consulte [a documentação do Elasticsearch no Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Os clientes não podem e não precisam configurar os índices de Elasticsearch diretamente.

Somente os analisadores incorporados são compatíveis (ou seja, aqueles enviados com o produto). Não há compatibilidade com analisadores personalizados.

Para obter o melhor desempenho operacional, os índices não devem ser excessivamente grandes. O tamanho total de todos os índices pode ser usado como guia: se isso aumentar em mais de 100% depois que os índices personalizados forem adicionados e os índices padrão forem ajustados em um ambiente de desenvolvimento, as definições de índice personalizado deverão ser ajustadas. O AEM as a Cloud Service pode impedir a implantação de índices que afetariam negativamente a estabilidade e o desempenho do sistema.

### Adicionar um índice {#adding-an-index}

Para adicionar um índice totalmente personalizado chamado `/oak:index/acme.product-custom-1`, para ser usado em uma nova versão do aplicativo e posteriores, o índice deve ser configurado da seguinte maneira:

`acme.product-1-custom-1`

Isso funciona anexando um identificador personalizado ao nome do índice, seguido por um ponto (**`.`**). O identificador deve ter entre 2 e 5 caracteres de comprimento.

Como descrito acima, isso garante que o índice seja usado somente pela nova versão do aplicativo.

### Alterar um índice {#changing-an-index}

Quando um índice existente é alterado, um novo índice precisa ser adicionado com a definição de índice alterada. Por exemplo, considere que o índice existente `/oak:index/acme.product-custom-1` seja alterado. O índice antigo é armazenado em `/oak:index/acme.product-custom-1` e o novo índice é armazenado em `/oak:index/acme.product-custom-2`.

A versão antiga do aplicativo usa a seguinte configuração:

`/oak:index/acme.product-custom-1`

A nova versão do aplicativo usa a seguinte configuração (alterada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>As definições de índice no AEM as a Cloud Service podem não corresponder totalmente às definições de índice em uma instância de desenvolvimento local. A instância de desenvolvimento não tem uma configuração Tika, enquanto as instâncias do AEM as a Cloud Service têm uma. Se você personalizar um índice com uma configuração Tika, mantenha essa configuração.

### Desfazer uma alteração {#undoing-a-change}

Às vezes, uma alteração em uma definição de índice precisa ser revertida. Isso pode ocorrer porque uma alteração foi feita por engano ou porque ela talvez não seja mais necessária. Por exemplo, a definição do índice `damAssetLucene-8-custom-3` foi criada por engano e já foi implantada. Por esse motivo, talvez você queira reverter para a definição de índice anterior, `damAssetLucene-8-custom-2`. Para fazer isso, é necessário adicionar um novo índice chamado `damAssetLucene-8-custom-4`, que contém a definição do índice anterior, `damAssetLucene-8-custom-2`.

### Remover um índice {#removing-an-index}

O seguinte se aplica somente a índices personalizados. Os índices de produto não podem ser removidos, pois são usados pelo AEM.

Se um índice precisar ser removido em uma versão posterior do aplicativo, você pode definir um índice vazio (um que nunca é usado e que não contém dados) com um novo nome. Para o propósito deste exemplo, você pode nomeá-lo como `/oak:index/acme.product-custom-3`. Isso substitui o índice `/oak:index/acme.product-custom-2`. Uma vez que o índice `/oak:index/acme.product-custom-2` for removido pelo sistema, o índice vazio `/oak:index/acme.product-custom-3` também poderá ser removido. Um exemplo de índice vazio é:

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

O Apache Jackrabbit Oak permite configurações de índice flexíveis para lidar com consultas de pesquisa com eficiência. Os índices são especialmente importantes para repositórios maiores. Certifique-se de que todas as consultas sejam apoiadas por um índice adequado. Consultas sem um índice adequado podem ler milhares de nós, o que será então registrado como um aviso.

Consulte [este documento](query-and-indexing-best-practices.md) para obter informações sobre como consultas e índices podem ser otimizados.
