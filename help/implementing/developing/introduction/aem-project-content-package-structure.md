---
title: Estrutura de projetos do AEM
description: Saiba mais sobre como definir estruturas de pacote para implantação no Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 798cd0f459b668dc372a88773ed6221927e7d02e
workflow-type: tm+mt
source-wordcount: '2880'
ht-degree: 13%

---

# Estrutura de projetos do AEM

>[!TIP]
>
>Familiarize-se com o [AEM básico do Arquétipo de projeto use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) e o [Plug-in FileVault Content Maven](/help/implementing/developing/tools/maven-plugin.md), pois este artigo se baseia nesses aprendizados e conceitos.

Este artigo descreve as alterações necessárias para que os projetos Adobe Experience Manager Maven sejam AEM como Cloud Service compatíveis, garantindo que eles respeitem a divisão de conteúdo mutável e imutável, que as dependências sejam estabelecidas para criar implantações determinísticas e não conflitantes e que sejam compactadas em uma estrutura implantável.

AEM implantações de aplicativos devem ser compostas por um único pacote AEM. Este pacote deve, por sua vez, conter subpacotes que contêm tudo o que o aplicativo requer para funcionar, incluindo código, configuração e qualquer conteúdo de linha de base de suporte.

O AEM requer uma separação de **conteúdo** e **código**, ou seja, um único pacote de conteúdo **não pode** ser implantado em **ambos** `/apps` as áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer outra que não `/apps`) do repositório. Em vez disso, o aplicativo deve separar código e conteúdo em pacotes separados para implantação no AEM.

A estrutura do pacote descrita neste documento é compatível com **ambas** as implantações de desenvolvimento locais e implantações do serviço da AEM Cloud.

>[!TIP]
>
>As configurações descritas neste documento são fornecidas por [AEM Project Maven Archetype 24 ou posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutáveis versus imutáveis do repositório {#mutable-vs-immutable}

`/apps` e `/libs`**são consideradas áreas imutáveis do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução).** Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

Todo o restante no repositório, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. são todas áreas **mutável**, o que significa que podem ser alteradas no tempo de execução.

>[!WARNING]
>
>Como nas versões anteriores do AEM, `/libs` não deve ser modificado. Somente AEM código de produto pode implantar em `/libs`.

### Índices Oak {#oak-indexes}

Os índices do Oak (`/oak:index`) são gerenciados especificamente pelo AEM como um processo de implantação do Cloud Service. Isso ocorre porque o Cloud Manager deve aguardar até que qualquer novo índice seja implantado e totalmente reindexado antes de passar para a nova imagem de código.

Por isso, embora os índices Oak sejam mutáveis em tempo de execução, eles devem ser implantados como código para que possam ser instalados antes que qualquer pacote mutável seja instalado. Portanto, as configurações `/oak:index` fazem parte do Pacote de código e não fazem parte do Pacote de conteúdo [conforme descrito abaixo](#recommended-package-structure).

>[!TIP]
>
>Para obter mais detalhes sobre a indexação no AEM como um Cloud Service, consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

## Estrutura de pacote recomendada {#recommended-package-structure}

![Estrutura do pacote de projetos do Experience Manager](assets/content-package-organization.png)

Este diagrama fornece uma visão geral da estrutura de projeto recomendada e dos artefatos de implantação de pacote.

A estrutura de implantação do aplicativo recomendada é a seguinte:

### Pacotes de código / Pacotes OSGi

+ O arquivo Jar do pacote OSGi é gerado e diretamente incorporado no projeto inteiro.

+ O pacote `ui.apps` contém todo o código a ser implantado e só é implantado em `/apps`. Os elementos comuns do pacote `ui.apps` incluem, mas não estão limitados a:
   + [Definições de componentes e ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=pt-BR) scripts HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (por meio de [Bibliotecas do cliente](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) Sobreposição de  `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurações com reconhecimento de contexto de fallback
      + `/apps/settings`
   + ACLs (permissões)
      + Qualquer `rep:policy` para qualquer caminho em `/apps`
   + [Scripts agrupados pré-compilados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/using/developing/archetype/precompiled-bundled-scripts.html)

+ O pacote `ui.config` contém todas as [configurações OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Pasta organizacional contendo definições de configuração OSGi específicas do modo de execução
      + `/apps/my-app/osgiconfig`
   + Pasta de configuração OSGi comum contendo configurações OSGi padrão que se aplicam a todos os AEM de destino como alvos de implantação do Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Execute pastas de configuração OSGi específicas ao modo que contêm configurações OSGi padrão que se aplicam a todos os AEM de destino como destinos de implantação do Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init Scripts de configuração do OSGi
      + [O Repo ](#repo-init) é a maneira recomendada de implantar conteúdo (mutável) que é logicamente parte do aplicativo AEM. As configurações de OSGi da Inicialização do Repo devem ser colocadas na pasta `config.<runmode>` apropriada, conforme descrito acima, e ser usadas para definir:
         + Estruturas de conteúdo da linha de base
         + Usuários
         + Usuários do Serviço
         + Grupos
         + ACLs (permissões)

>[!NOTE]
>
>O mesmo código deve ser implantado em todos os ambientes. Isso é necessário para garantir que um nível de validação de confiança no ambiente de preparo também esteja em produção. Para obter mais informações, consulte a seção em [Runmodes](/help/implementing/deploying/overview.md#runmodes).


### Pacotes de conteúdo

+ O pacote `ui.content` contém todo o conteúdo e configuração. O Pacote de conteúdo contém todas as definições de nó que não estão nos pacotes `ui.apps` ou `ui.config`, ou em outras palavras, nada que não esteja em `/apps` ou `/oak:index`. Os elementos comuns do pacote `ui.content` incluem, mas não estão limitados a:
   + Configurações sensíveis ao contexto
      + `/conf`
   + Estruturas de conteúdo necessárias e complexas (ou seja, Compilação de conteúdo que é criada e estende por cima das estruturas de conteúdo da Linha de base definidas no Repo Init.)
      + `/content`,  `/content/dam`, etc.
   + taxonomias de marcação controladas
      + `/content/cq:tags`
   + Nós etc herdados (idealmente, migre-os para locais que não sejam/etc)
      + `/etc`

### Pacotes do contêiner

+ O pacote `all` é um pacote de contêiner que APENAS inclui artefatos implantáveis, o arquivo Jar do pacote OSGI, os pacotes `ui.apps`, `ui.config` e `ui.content` como incorporados. O pacote `all` não deve ter **nenhum conteúdo ou código** próprio, mas deve delegar toda a implantação no repositório em seus pacotes secundários ou em arquivos Jar do pacote OSGi.

   Os pacotes agora são incluídos usando a configuração incorporada do plug-in Maven [FileVault Package Maven](#embeddeds), em vez da configuração `<subPackages>`.

   Para implantações complexas de Experience Manager, pode ser desejável criar vários `ui.apps`, `ui.config` e `ui.content` projetos/pacotes que representem sites ou locatários específicos no AEM. Se isso for feito, verifique se a divisão entre conteúdo mutável e imutável é respeitada, e os pacotes de conteúdo necessários e os arquivos Jar do pacote OSGi são incorporados como subpacotes no pacote de conteúdo do contêiner `all`.

   Por exemplo, uma estrutura complexa de pacote de conteúdo de implantação do pode ser semelhante a:

   + `all` o pacote de conteúdo incorpora os seguintes pacotes para criar um artefato de implantação singular
      + `common.ui.apps` implanta o código exigido pelo  **** site A e pelo site B
      + `site-a.core` Jar do pacote OSGi exigido pelo site A
      + `site-a.ui.apps` implanta o código exigido pelo site A
      + `site-a.ui.config` implanta configurações OSGi necessárias para o Site A
      + `site-a.ui.content` implanta conteúdo e configuração exigidos pelo site A
      + `site-b.core` Jar do pacote OSGi exigido pelo site B
      + `site-b.ui.apps` implanta o código exigido pelo site B
      + `site-b.ui.config` implanta configurações OSGi necessárias para o site B
      + `site-b.ui.content` implanta conteúdo e configuração exigidos pelo site B

### Pacotes de aplicativos extras{#extra-application-packages}

Se outros projetos de AEM, que são compostos por seus próprios pacotes de código e conteúdo, forem usados pela implantação de AEM, seus pacotes de contêiner deverão ser incorporados ao pacote `all` do projeto.

Por exemplo, um projeto de AEM que inclui dois aplicativos de AEM de fornecedor pode ter a seguinte aparência:

+ `all` o pacote de conteúdo incorpora os seguintes pacotes para criar um artefato de implantação singular
   + `core` Jar do pacote OSGi exigido pelo aplicativo AEM
   + `ui.apps` implanta o código exigido pelo aplicativo AEM
   + `ui.config` implanta configurações OSGi necessárias para o aplicativo AEM
   + `ui.content` implanta conteúdo e configuração exigidos pelo aplicativo AEM
   + `vendor-x.all` implanta tudo (código e conteúdo) exigido pelo aplicativo X do fornecedor
   + `vendor-y.all` implanta tudo (código e conteúdo) exigido pelo aplicativo Y do fornecedor

## Tipos de pacotes {#package-types}

As embalagens devem ser marcadas com o tipo de pacote declarado.

+ Os pacotes de contêiner devem definir seu `packageType` para `container`. Os pacotes de contêineres não devem conter diretamente pacotes OSGi, configurações OSGi e não têm permissão para usar [instalar ganchos](http://jackrabbit.apache.org/filevault/installhooks.html).
+ Os pacotes de código (imutáveis) devem definir `packageType` para `application`.
+ Os pacotes de conteúdo (mutável) devem definir `packageType` como `content`.


Para obter mais informações, consulte [Apache Jackrabbit FileVault - Documentação de plug-in do pacote Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) e o [trecho de configuração do FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) abaixo.

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-package-types) abaixo para obter um trecho completo.

## Pacotes de marcação para implantação pelo Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Por padrão, o Adobe Cloud Manager coleta todos os pacotes produzidos pela compilação Maven. No entanto, como o pacote do contêiner (`all`) é o artefato de implantação singular que contém todos os pacotes de código e conteúdo, devemos garantir que **somente** o pacote do contêiner (`all`) seja implantado. Para garantir isso, outros pacotes gerados pela compilação Maven devem ser marcados com a configuração do Plug-in FileVault Content Package Maven do `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#pom-xml-snippets) abaixo para obter um trecho completo.

## Repo Init{#repo-init}

A Init do Repo fornece instruções, ou scripts, que definem estruturas JCR, que vão de estruturas de nós comuns, como árvores de pastas, a usuários, usuários de serviços, grupos e definições de ACL.

Os principais benefícios do Repo Init são ter permissões implícitas para executar todas as ações definidas por seus scripts e serem chamadas no início do ciclo de vida da implantação, garantindo que todas as estruturas JCR necessárias existam pelo código de tempo em que é executado.

Embora a Init do Repo se scripts live no projeto `ui.config` como scripts, eles podem e devem ser usados para definir as seguintes estruturas mutáveis:

+ Estruturas de conteúdo da linha de base
+ Usuários do Serviço
+ Usuários
+ Grupos
+ ACLs

Os scripts de Init do Repo são armazenados como entradas `scripts` de `RepositoryInitializer` configurações de fábrica OSGi e, portanto, podem ser implicitamente direcionados pelo modo de execução, permitindo diferenças entre o Autor do AEM e os scripts de Init do Repo dos Serviços de Publicação do AEM, ou mesmo entre ambientes (Dev, Stage e Prod).

As configurações de OSGi da Inicialização do Repo são melhor escritas no [`.config` formato de configuração OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1), pois oferecem suporte a várias linhas, o que é uma exceção às práticas recomendadas de uso de [`.cfg.json` para definir configurações de OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Observe que, ao definir Usuários e Grupos, somente grupos são considerados parte do aplicativo, e parte integrante de sua função deve ser definida aqui. Usuários e grupos da organização ainda devem ser definidos no tempo de execução em AEM; por exemplo, se um fluxo de trabalho personalizado atribuir trabalho a um Grupo nomeado, esse Grupo deverá ser definido em por meio da Inicialização do Repo no aplicativo AEM, no entanto, se o Agrupamento for meramente organizacional, como &quot;Equipe da Wendy&quot; e &quot;Equipe do Sean&quot;, eles serão melhor definidos e gerenciados no tempo de execução em AEM.

>[!TIP]
>
>Os scripts Repo Init *devem* ser definidos no campo incorporado `scripts` e a configuração `references` não funcionará.

O vocabulário completo para scripts de Init do Repo está disponível na [documentação do Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte a seção [Snippets de inicialização de repo](#snippet-repo-init) abaixo para obter um trecho completo.

## Pacote de estrutura do repositório {#repository-structure-package}

Os pacotes de código exigem a configuração do plug-in FileVault Maven para fazer referência a um `<repositoryStructurePackage>` que aplica corretamente as dependências estruturais (para garantir que um pacote de código não seja instalado sobre outro). Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

Isso **só é necessário** em Pacotes de código, ou seja, qualquer pacote marcado com `<packageType>application</packageType>`.

Para saber como criar um pacote de estrutura de repositório para seu aplicativo, consulte [Desenvolver um pacote de estrutura de repositório](repository-structure-package.md).

Observe que os pacotes de conteúdo (`<packageType>content</packageType>`) **não** exigem este Pacote de estrutura de repositório.

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-repository-structure-package) abaixo para obter um trecho completo.

## Incorporação de subpacotes no pacote de contêiner{#embeddeds}

Os pacotes de conteúdo ou código são colocados em uma pasta &quot;side-car&quot; especial e podem ser direcionados para instalação AEM autor, AEM publicação ou ambos, usando a configuração `<embeddeds>` do plug-in FileVault Maven. Observe que a configuração `<subPackages>` não deve ser usada.

Os casos de uso comuns incluem:

+ ACLs/permissões que diferem entre AEM usuários do autor e AEM usuários de publicação
+ Configurações usadas para suportar atividades somente em AEM autor
+ Código como integrações com sistemas de back-office, necessário apenas para ser executado AEM autor

![Como incorporar pacotes](assets/embeddeds.png)

Para direcionar AEM autor, AEM publicação ou ambos, o pacote é incorporado no pacote do contêiner `all` em um local de pasta especial, no seguinte formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Analisando esta estrutura de pastas:

+ A pasta de primeiro nível **deve ser** `/apps`.
+ A pasta de segundo nível representa o aplicativo com `-packages` pós-fixado no nome da pasta. Geralmente, há apenas uma única pasta de segundo nível em que todos os sub-pacotes são incorporados, no entanto, qualquer número de pastas de segundo nível pode ser criado para melhor representar a estrutura lógica do aplicativo:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Por convenção, as pastas incorporadas do pacote secundário são nomeadas com o sufixo `-packages`. Isso garante que o código de implantação e os pacotes de conteúdo **não** sejam implantados nas pastas de destino de qualquer pacote secundário `/apps/<app-name>/...` que resulte em comportamento de instalação destrutivo e cíclico.

+ A pasta de terceiro nível deve ser
   `application`, `content` ou `container`
   + A pasta `application` contém pacotes de código
   + A pasta `content` contém pacotes de conteúdo
   + A pasta `container` armazena qualquer [pacote de aplicativo extra](#extra-application-packages) que possa ser incluído pelo aplicativo AEM.
Esse nome de pasta corresponde aos [tipos de pacote](#package-types) dos pacotes que ele contém.
+ A pasta de 4º nível contém os pacotes secundários e deve ser uma das seguintes:
   + `install` para instalar no autor do AEM **e** na publicação do AEM
   + `install.author` para instalar **somente** no autor do AEM
   + `install.publish` para instalar  **** somente em AEM publicar Observe que somente  `install.author` e  `install.publish` são alvos compatíveis. Outros modos de execução **não são** compatíveis.

Por exemplo, uma implantação que contém AEM criar e publicar pacotes específicos pode ser semelhante ao seguinte:

+ `all` O pacote de contêiner incorpora os seguintes pacotes para criar um artefato de implantação singular
   + `ui.apps` incorporado em  `/apps/my-app-packages/application/install` implantações de código para autor AEM e publicação AEM
   + `ui.apps.author` incorporado no código de  `/apps/my-app-packages/application/install.author` implantações somente AEM autor
   + `ui.content` incorporado no  `/apps/my-app-packages/content/install` implanta conteúdo e configuração no autor AEM e na publicação AEM
   + `ui.content.publish` incorporado em  `/apps/my-app-packages/content/install.publish` implantações de conteúdo e configuração para AEM apenas publicar

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-embeddeds) abaixo para obter um trecho completo.

### Definição de Filtro do Pacote do Contêiner {#container-package-filter-definition}

Devido à incorporação dos subpacotes de código e conteúdo no pacote de contêiner, os caminhos de destino incorporados devem ser adicionados ao `filter.xml` do projeto de contêiner para garantir que os pacotes incorporados sejam incluídos no pacote de contêiner quando criados.

Basta adicionar as entradas `<filter root="/apps/<my-app>-packages"/>` para qualquer pasta de segundo nível que contenha pacotes secundários a serem implantados.

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-container-package-filters) abaixo para obter um trecho completo.

## Como incorporar pacotes de terceiros {#embedding-3rd-party-packages}

Todos os pacotes devem estar disponíveis por meio do repositório público do Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) ou de um repositório de artefatos Maven acessível público e referenciável de terceiros.[

Se os pacotes de terceiros estiverem no **repositório público de artefatos Maven da Adobe**, nenhuma configuração adicional será necessária para o Adobe Cloud Manager resolver os artefatos.

Se os pacotes de terceiros estiverem em um **repositório de artefatos Maven de terceiros público**, esse repositório deverá ser registrado no `pom.xml` do projeto e incorporado de acordo com o método [descrito acima](#embeddeds).

Aplicativos/conectores de terceiros devem ser incorporados usando seu pacote `all` como um contêiner no pacote do contêiner do seu projeto (`all`).

A adição de dependências de Maven segue as práticas padrão de Maven e a incorporação de artefatos de terceiros (pacotes de código e conteúdo) são [descritas acima](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-3rd-party-maven-repositories) abaixo para obter um trecho completo.

## Dependências do pacote entre `ui.apps` dos pacotes `ui.content` {#package-dependencies}

Para garantir a instalação correta das embalagens, recomenda-se estabelecer as dependências entre pacotes.

A regra geral é que os pacotes que contêm conteúdo mutável (`ui.content`) devem depender do código imutável (`ui.apps`) que suporta a renderização e o uso do conteúdo mutável.

Uma exceção notável para essa regra geral é se o pacote de código imutável (`ui.apps` ou qualquer outro), __only__ contém pacotes OSGi. Em caso afirmativo, nenhum pacote AEM deve declarar uma dependência em relação a ele. Isso ocorre porque pacotes de código imutáveis __somente__ contendo pacotes OSGi não são registrados no Gerenciador de Pacotes AEM e, portanto, qualquer pacote AEM dependendo dele terá uma dependência insatisfeita e não será instalado.

>[!TIP]
>
>Consulte a seção [POM XML Snippets](#xml-package-dependencies) abaixo para obter um trecho completo.

Os padrões comuns para dependências de pacotes de conteúdo são:

### Dependências do pacote de implantação simples {#simple-deployment-package-dependencies}

O caso simples define o pacote de conteúdo mutável `ui.content` para depender do `ui.apps` pacote de código imutável.

+ `all` não tem dependências
   + `ui.apps` não tem dependências
   + `ui.content` depende de  `ui.apps`

### Dependências complexas do pacote de implantação {#complex-deploxment-package-dependencies}

Implantações complexas se expandem no caso simples e definem dependências entre o conteúdo mutável correspondente e os pacotes de código imutáveis. Conforme necessário, as dependências também podem ser estabelecidas entre pacotes de código imutáveis.

+ `all` não tem dependências
   + `common.ui.apps.common` não tem dependências
   + `site-a.ui.apps` depende de  `common.ui.apps`
   + `site-a.ui.content` depende de  `site-a.ui.apps`
   + `site-b.ui.apps` depende de  `common.ui.apps`
   + `site-b.ui.content` depende de  `site-b.ui.apps`

## Desenvolvimento e implantação locais {#local-development-and-deployment}

As estruturas e a organização do projeto descritas neste artigo são **instâncias de desenvolvimento local totalmente compatíveis** AEM.

## Trechos de POM XML {#pom-xml-snippets}

A seguir estão trechos de configuração Maven `pom.xml` que podem ser adicionados a projetos Maven para alinhar-se às recomendações acima.

### Tipos de pacotes {#xml-package-types}

Os pacotes de código e conteúdo, que são implantados como pacotes secundários, devem declarar um tipo de pacote de **aplicativo** ou **conteúdo**, dependendo do que eles contêm.

#### Tipos de pacote do contêiner {#container-package-types}

O contêiner `all/pom.xml` projeto **não** declara um `<packageType>`.

#### Tipos de pacote de código (imutável) {#immutable-package-types}

Os pacotes de código devem definir `packageType` para `application`.

No `ui.apps/pom.xml`, as `<packageType>application</packageType>` diretivas de configuração de build da declaração de plug-in `filevault-package-maven-plugin` declaram o tipo de pacote.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.apps</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### Tipos de pacote de conteúdo (variável) {#mutable-package-types}

Os pacotes de conteúdo devem definir `packageType` para `content`.

No `ui.content/pom.xml`, a diretiva `<packageType>content</packageType>` de configuração de build da declaração de plug-in `filevault-package-maven-plugin` declara o tipo de pacote.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Pacotes de marcação para a implantação do Adobe Cloud Manager {#cloud-manager-target}

Em todos os projetos que geram um pacote, **exceto** do projeto do contêiner (`all`), adicione `<cloudManagerTarget>none</cloudManagerTarget>` à configuração `<properties>` da declaração do plug-in `filevault-package-maven-plugin` para garantir que eles **não sejam** implantados pelo Adobe Cloud Manager. O pacote do contêiner (`all`) deve ser o único pacote implantado pelo Cloud Manager, que, por sua vez, incorpora todos os pacotes de código e conteúdo necessários.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Repo Init{#snippet-repo-init}

Os scripts Repo Init que contêm os scripts Repo Init são definidos na configuração de fábrica `RepositoryInitializer` OSGi por meio da propriedade `scripts`. Observe que, como esses scripts são definidos nas configurações OSGi, eles podem ser facilmente escopo por modo de execução usando a semântica de pasta `../config.<runmode>` normal.

Observe que, como os scripts geralmente são declarações de várias linhas, é mais fácil defini-los no arquivo `.config`, do que no formato `.cfg.json` baseado em JSON.

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

A propriedade `scripts` OSGi contém diretivas, conforme definido pelo [idioma de inicialização do Repo do Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacote de estrutura do repositório {#xml-repository-structure-package}

No `ui.apps/pom.xml` e em qualquer outro `pom.xml` que declare um pacote de código (`<packageType>application</packageType>`), adicione a seguinte configuração de pacote de estrutura de repositório ao plug-in FileVault Maven . Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### Incorporação de subpacotes no pacote de contêiner {#xml-embeddeds}

Na `all/pom.xml`, adicione as seguintes diretivas `<embeddeds>` à declaração de plug-in `filevault-package-maven-plugin`. Lembre-se de que **não** usa a configuração `<subPackages>`, pois isso incluirá os subpacotes em `/etc/packages` em vez de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### Definição de Filtro do Pacote do Contêiner {#xml-container-package-filters}

No `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) do projeto `all`, **inclua** as pastas `-packages` que contêm pacotes secundários a serem implantados:

```xml
<filter root="/apps/my-app-packages"/>
```

Se vários `/apps/*-packages` forem usados nos destinos incorporados, todos deverão ser enumerados aqui.

### Repositórios Maven de terceiros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>A adição de mais repositórios Maven pode estender os tempos de build maven, pois repositórios Maven adicionais serão verificados quanto às dependências.

No `pom.xml` do projeto do reator, adicione quaisquer diretivas de repositório Maven públicas de terceiros necessárias. A configuração completa `<repository>` deve estar disponível no provedor de repositório de terceiros.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### Dependências do pacote entre `ui.apps` dos pacotes `ui.content` {#xml-package-dependencies}

Na `ui.content/pom.xml`, adicione as seguintes diretivas `<dependencies>` à declaração de plug-in `filevault-package-maven-plugin`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### Limpando a pasta de destino do projeto do contêiner {#xml-clean-container-package}

No `all/pom.xml`, adicione o plug-in `maven-clean-plugin` que limpará o diretório de destino antes de uma compilação Maven.

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## Recursos adicionais {#additional-resources}

+ [Gerenciamento de pacotes usando o Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Plug-in FileVault Content Package Maven](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
