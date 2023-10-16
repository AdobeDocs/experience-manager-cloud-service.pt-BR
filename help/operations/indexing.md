---
title: Pesquisa e indexação de conteúdo
description: Saiba mais sobre Pesquisa e indexação de conteúdo no AEM as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: d567115445c0a068380e991452d9b976535e3a1d
workflow-type: tm+mt
source-wordcount: '2433'
ht-degree: 32%

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
* Pesquisar por vetores de recursos semelhantes (`useInSimilarity = true`) não é compatível.

>[!TIP]
>
>Para obter mais detalhes sobre a indexação e consultas do Oak, incluindo uma descrição detalhada de recursos avançados de pesquisa e indexação, consulte [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/query/query.html).


## Como usar {#how-to-use}

As definições de índice podem ser categorizadas em três casos de uso principais, da seguinte maneira:

1. **Adicionar** uma nova definição de índice personalizado.
2. **Atualizar** uma definição de índice existente adicionando uma nova versão.
3. **Remover** uma definição de índice que não é mais necessária.

Para ambos os itens 1 e 2 acima, é necessário criar uma nova definição de índice como parte da base de código personalizada no cronograma de lançamento respectivo do Cloud Manager. Para obter mais informações, consulte [Implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md) documentação.

## Nomes de índice {#index-names}

Uma definição de índice pode se enquadrar em uma das seguintes categorias:

1. Índice pronto para uso (OOTB). Por exemplo: `/oak:index/cqPageLucene-2` ou `/oak:index/damAssetLucene-8`.

2. Personalização de um índice OOTB. Elas são indicadas anexando `-custom-` seguido por um identificador numérico do nome do índice original. Por exemplo: `/oak:index/damAssetLucene-8-custom-1`.

3. Índice totalmente personalizado: é possível criar um índice totalmente novo do zero. O nome deve ter um prefixo para evitar conflitos de nomenclatura. Por exemplo: `/oak:index/acme.product-1-custom-2`, onde o prefixo é `acme.`

>[!NOTE]
>
>Introdução de novos índices no `dam:Asset` O nodetype (especialmente índices de texto completo) é altamente desencorajado, pois pode entrar em conflito com recursos de produtos OOTB, resultando em problemas funcionais e de desempenho. Em geral, adicionar outras propriedades ao atual `damAssetLucene-*` a versão do índice é a maneira mais apropriada para indexar consultas no `dam:Asset` nodetype (essas alterações serão mescladas automaticamente em uma nova versão do produto do índice se ele for lançado posteriormente). Em caso de dúvida, entre em contato com o Suporte da Adobe para obter assistência.

## Preparação da nova definição de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se estiver personalizando um índice pronto para uso (por exemplo, `damAssetLucene-8`), copie a definição mais recente do índice pronto para uso de um *ambiente do Cloud Service* usando o gerenciador de pacotes CRX DE (`/crx/packmgr/`). Renomear para `damAssetLucene-8-custom-1` (ou superior) e adicione suas personalizações dentro do arquivo XML. Isso garante que as configurações necessárias não sejam removidas inadvertidamente. Por exemplo, a variável `tika` nó em `/oak:index/damAssetLucene-8/tika` é obrigatório no índice personalizado implantado em um ambiente AEM Cloud Service, mas não existe no SDK AEM local.

Para personalizações de um índice OOTB, prepare um novo pacote que contenha a definição de índice real que siga esse padrão de nomenclatura:

`<indexName>-<productVersion>-custom-<customVersion>`

Para um índice totalmente personalizado, prepare um novo pacote de definição de índice que contenha a definição de índice que siga esse padrão de nomenclatura:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualquer pacote de conteúdo que contenha definições de índice deve ter as seguintes propriedades definidas no arquivo de propriedades do pacote de conteúdo, localizado em `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Implantação de definições de índice personalizadas {#deploying-custom-index-definitions}

Para ilustrar a implantação de uma versão personalizada do índice pronto para uso `damAssetLucene-8`, forneceremos um guia passo a passo. Neste exemplo, vamos renomeá-lo para `damAssetLucene-8-custom-1`. Então, o processo é o seguinte:

1. Crie uma nova pasta com o nome de índice atualizado no `ui.apps` diretório:
   * Exemplo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Adicionar um arquivo de configuração `.content.xml` com as configurações personalizadas dentro da pasta recém-criada. Veja abaixo um exemplo de personalização: Nome do arquivo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. Adicionar uma entrada ao filtro FileVault em `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Adicione um arquivo de configuração para o Apache Tika em: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. Verifique se a sua configuração está em conformidade com as diretrizes fornecidas no [Configuração do projeto](#project-configuration) seção. Faça as adaptações necessárias de acordo.

## Configuração do projeto

É altamente recomendável usar a versão >= `1.3.2` do Jackrabbit `filevault-package-maven-plugin`. As etapas para incorporá-lo ao seu projeto são as seguintes:

1. Atualizar a versão no nível superior `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. Adicione o seguinte ao nível superior `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   Esta é uma amostra do nível superior do projeto `pom.xml` arquivo com as configurações acima incluídas:

   Nome de arquivo: `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. Entrada `ui.apps/pom.xml` e `ui.apps.structure/pom.xml` é necessário permitir que os `allowIndexDefinitions` e `noIntermediateSaves` opções no `filevault-package-maven-plugin`. Ativando `allowIndexDefinitions` permite definições de índice personalizadas, enquanto `noIntermediateSaves` garante que as configurações sejam adicionadas com precisão.

   Nomes de arquivos: `ui.apps/pom.xml` e `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. Adicionar um filtro para `/oak:index` in `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

Depois de adicionar a nova definição de índice, implante o novo aplicativo usando o Cloud Manager. Essa implantação inicia dois trabalhos, responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para criação e publicação, respectivamente. Antes da mudança, os repositórios subjacentes passam por reindexação com as definições de índice atualizadas.

>[!TIP]
>
>Para obter mais detalhes sobre a estrutura do pacote necessária para o AEM as a Cloud Service, consulte o documento [Estrutura de projeto do AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Gerenciamento de Índice usando Implantações Móveis {#index-management-using-rolling-deployments}

### O que é o gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata da adição, remoção e alteração de índices. Alterar a *definição* de um índice é uma tarefa rápida, mas aplicar essa alteração (o que geralmente é chamado de “criação de um índice” ou, para índices existentes, “reindexação”) requer tempo. Não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

### O que são Implantações Móveis {#what-are-rolling-deployments}

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

Às vezes, é necessário desfazer uma modificação em uma definição de índice. Isso pode ocorrer devido a um erro inadvertido ou que a modificação não é mais necessária. Tome, por exemplo, a definição do índice `damAssetLucene-8-custom-3,` que foi criado por engano e já foi implantado. Consequentemente, você deseja reverter para a definição de índice anterior, `damAssetLucene-8-custom-2.` Para fazer isso, é necessário introduzir um novo índice chamado `damAssetLucene-8-custom-4` que incorpora a definição do índice anterior, `damAssetLucene-8-custom-2.`

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
