---
title: Estrutura de projetos do AEM
description: Saiba mais sobre como definir estruturas de pacote para implantação no Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: 5594792b84bdb5a0c72bfb6d034ca162529e4ab2
workflow-type: tm+mt
source-wordcount: '2522'
ht-degree: 17%

---


# Estrutura de projetos do AEM

>[!TIP]
>
>Familiarize-se com o uso [básico do](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)AEM Project Archetype e com o plug-in [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Maven, pois este artigo se baseia nesses aprendizados e conceitos.

Este artigo descreve as alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service, garantindo que eles respeitem a divisão de conteúdo mutável e imutável. que sejam estabelecidas as dependências necessárias para criar implantações determinísticas e não conflitantes; E que eles são empacotados numa estrutura implantável.

As implantações de aplicativos AEM devem ser compostas por um único pacote AEM. Este pacote deve, por sua vez, conter subpacotes que contêm tudo o que o aplicativo exige para funcionar, incluindo código, configuração e qualquer conteúdo básico de suporte.

O AEM requer uma separação de **conteúdo** e **código**, ou seja, um único pacote de conteúdo **não pode** ser implantado em **ambos** `/apps` as áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer outra que não `/apps`) do repositório. Em vez disso, o aplicativo deve separar código e conteúdo em pacotes separados para implantação no AEM.

A estrutura do pacote descrita neste documento é compatível com **ambas** as implantações de desenvolvimento locais e implantações do serviço da AEM Cloud.

>[!TIP]
>
>As configurações descritas neste documento são fornecidas pelo [AEM Project Maven Archetype 21 ou posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutáveis vs. imutáveis do repositório {#mutable-vs-immutable}

`/apps` e `/libs` são consideradas áreas **imutáveis** do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução). Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

Tudo o resto no repositório, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. são todas áreas **mutáveis** , o que significa que podem ser alteradas em tempo de execução.

>[!WARNING]
>
> Como nas versões anteriores do AEM, não `/libs` deve ser modificado. Somente o código de produto AEM pode ser implantado em `/libs`.

### Índices de Oak {#oak-indexes}

Os índices de Oak (`/oak:index`) são gerenciados especificamente pelo processo de implantação do AEM Cloud Service. Isso ocorre porque o Gerenciador de nuvem deve aguardar até que qualquer novo índice seja implantado e totalmente indexado novamente antes de alternar para a nova imagem de código.

Por isso, embora os índices Oak sejam mutáveis em tempo de execução, eles devem ser implantados como código para que possam ser instalados antes que qualquer pacote mutável seja instalado. Portanto, `/oak:index` as configurações fazem parte do Pacote de código e não fazem parte do Pacote de conteúdo, [conforme descrito abaixo.](#recommended-package-structure)

>[!TIP]
>
>Para obter mais detalhes sobre a indexação no AEM como um serviço em nuvem, consulte a Pesquisa e indexação de [conteúdo do documento.](/help/operations/indexing.md)

## Estrutura do pacote recomendada {#recommended-package-structure}

![Estrutura do pacote de projetos do Experience Manager](assets/content-package-organization.png)

Este diagrama fornece uma visão geral da estrutura do projeto e dos artefatos de implantação do pacote recomendados.

A estrutura de implantação do aplicativo recomendada é a seguinte:

+ O `ui.apps` pacote, ou Pacote de código, contém todo o código a ser implantado e só é implantado `/apps`. Os elementos comuns do `ui.apps` pacote incluem, mas não se limitam a:
   + Pacotes OSGi
      + `/apps/my-app/install`
   + Configurações do OSGi
      + `/apps/my-app/config`
   + Scripts HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (por meio das bibliotecas do cliente)
      + `/apps/my-app/clientlibs`
   + Sobreposições de /libs
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurações com reconhecimento de contexto de fallback
      + `/apps/settings`
   + ACLs (permissões)
      + Qualquer caminho `rep:policy` sob qualquer `/apps`
   + Diretrizes de configuração do Repo Init OSGi (e scripts correspondentes)
      + [Inicialização](#repo-init) de repo é a maneira recomendada de implantar conteúdo (mutável) que logicamente faz parte do aplicativo AEM. Deve utilizar - se a opção de recompra para definir:
         + Estruturas de conteúdo da linha de base
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + Usuários
         + Usuários do serviço
         + Grupos
         + ACLs (permissões)
            + Qualquer `rep:policy` caminho (mutável ou imutável)
+ O `ui.content` pacote, ou Pacote de conteúdo, contém todo o conteúdo e a configuração. O Pacote de conteúdo, contém tudo que não está no `ui.apps` pacote, ou em outras palavras, nada que não esteja no `/apps` ou `/oak:index`. Os elementos comuns do `ui.content` pacote incluem, mas não se limitam a:
   + Configurações sensíveis ao contexto
      + `/conf`
   + Estruturas de conteúdo necessárias e complexas (ou seja, Compilação de conteúdo que é criada e estende além das estruturas de conteúdo da Linha de base definidas no Repo Init.
      + `/content`, `/content/dam`, etc.
   + Taxonomias de marcação controladas
      + `/content/cq:tags`
   + Etc. nós herdados
      + `/etc`
+ O pacote `all` é um pacote de contêiner que APENAS inclui os pacotes `ui.apps` e `ui.content` como incorporados. O pacote `all` não deve ter **nenhum conteúdo** próprio, mas deve delegar toda a implantação no repositório em seus pacotes secundários.

   Os pacotes agora são incluídos usando a configuração [incorporada do plug-in Maven](#embeddeds)FileVault Package Maven, em vez da `<subPackages>` configuração.

   Para implantações complexas do Experience Manager, pode ser desejável criar vários projetos `ui.apps` e `ui.content` pacotes que representem sites ou locatários específicos no AEM. Se isso for feito, verifique se a divisão entre conteúdo mutável e imutável é respeitada e se os pacotes de conteúdo necessários são adicionados como subpacotes no pacote de conteúdo do `all` container.

   Por exemplo, uma estrutura complexa de pacote de conteúdo de implantação pode ter a seguinte aparência:

   + `all` o pacote de conteúdo incorpora os seguintes pacotes para criar um artefato de implantação singular
      + `ui.apps.common` implanta o código necessário para **ambos** os locais A e B
      + `ui.apps.site-a` implanta o código exigido pelo site A
      + `ui.content.site-a` implanta o conteúdo e a configuração necessários para o site A
      + `ui.apps.site-b` implanta o código exigido pelo site B
      + `ui.content.site-b` implanta o conteúdo e a configuração necessários para o site B

## Tipos de encapsulamento {#package-types}

As embalagens devem ser marcadas com o tipo de embalagem declarado.

+ Os pacotes de Container não devem ter um `packageType` conjunto.
+ Os pacotes de código (imutáveis) devem definir seus `packageType` como `application`.
+ Os pacotes de conteúdo (mutável) devem definir `packageType` como `content`.

Para obter mais informações, consulte [Apache Jackrabbit FileVault - documentação](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) do plug-in Package Maven e o trecho [de configuração](#marking-packages-for-deployment-by-adoube-cloud-manager) FileVault Maven abaixo.

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-package-types) POM abaixo para obter um trecho completo.

## Pacotes de marcação para implantação pelo Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Por padrão, o Adobe Cloud Manager coleta todos os pacotes produzidos pela compilação Maven. No entanto, como o pacote do contêiner (`all`) é o artefato de implantação singular que contém todos os pacotes de código e conteúdo, devemos garantir que **somente** o pacote do contêiner (`all`) seja implantado. Para garantir isso, outros pacotes gerados pela compilação Maven devem ser marcados com a configuração do Plug-in FileVault Content Package Maven do `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte a seção Trechos [XML](#pom-xml-snippets) POM abaixo para obter um trecho completo.

## Inicialização do Repo{#repo-init}

A Inicialização do Repo fornece instruções, ou scripts, que definem estruturas JCR, desde estruturas de nós comuns, como árvores de pastas, até usuários, usuários de serviços, grupos e definição de ACL.

Os principais benefícios do Repo Init são ter permissões implícitas para executar todas as ações definidas pelos scripts e serem chamadas no início do ciclo de vida da implantação, garantindo que todas as estruturas JCR necessárias existam até que o código seja executado.

Embora o Repo Init faça scripts em tempo real no `ui.apps` projeto como scripts, eles podem e devem ser usados para definir as seguintes estruturas mutáveis:

+ Estruturas de conteúdo da linha de base
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ Usuários do serviço
+ Usuários
+ Grupos
+ ACLs

Os scripts de Inicialização de Repo são armazenados como entradas de configurações de fábrica do `scripts` `RepositoryInitializer` OSGi e, portanto, podem ser implicitamente direcionados pelo modo de execução, permitindo diferenças entre os scripts de Inicialização de Repo do autor do AEM e dos Serviços de publicação do AEM, ou mesmo entre Envs (Dev, Stage e Prod).

Observe que, ao definir Usuários e Grupos, somente grupos são considerados parte do aplicativo e integrantes de sua função devem ser definidos aqui. Os usuários e grupos da organização ainda devem ser definidos em tempo de execução no AEM; por exemplo, se um fluxo de trabalho personalizado atribuir trabalho a um Grupo nomeado, esse Grupo deverá ser definido por meio da Inicialização de acordo com o AEM no aplicativo AEM, no entanto, se o Agrupamento for meramente organizacional, como &quot;Equipe do Wendy&quot; e &quot;Equipe do Sean&quot;, eles serão melhor definidos e gerenciados em tempo de execução no AEM.

>[!TIP]
>
>Os scripts de inicialização de acordo com o repo *devem* ser definidos no campo em linha `scripts` e a `references` configuração não funcionará.

O vocabulário completo para scripts do Repo Init está disponível na documentação [do](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Apache Sling Repo Init.

>[!TIP]
>
>Consulte a seção [Repo Init Snippets](#snippet-repo-init) abaixo para obter um trecho completo.

## Pacote de estrutura do repositório {#repository-structure-package}

Os Pacotes de código exigem a configuração do plug-in FileVault Maven para fazer referência a uma configuração `<repositoryStructurePackage>` que imponha a correção das dependências estruturais (para garantir que um pacote de código não seja instalado sobre outro). Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

Isso **só é necessário** em Pacotes de código, ou seja, qualquer pacote marcado com `<packageType>application</packageType>`.

Para saber como criar um pacote de estrutura de repositório para seu aplicativo, consulte [Desenvolver um pacote](repository-structure-package.md)de estrutura de repositório.

Observe que os pacotes de conteúdo (`<packageType>content</packageType>`) **não** exigem este Pacote de estrutura de repositório.

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-repository-structure-package) POM abaixo para obter um trecho completo.

## Incorporação de subpacotes no pacote de Container{#embeddeds}

Os pacotes de conteúdo ou código são colocados em uma pasta especial &quot;carro lateral&quot; e podem ser direcionados para instalação no autor do AEM, na publicação do AEM ou em ambos, usando a `<embeddeds>` configuração do plug-in FileVault Maven. Observe que a `<subPackages>` configuração não deve ser usada.

Os casos de uso frequentes incluem:

+ ACLs/permissões diferentes entre usuários do autor de AEM e usuários de publicação de AEM
+ Configurações usadas para suportar atividade somente no autor do AEM
+ Códigos como integrações com sistemas de back-office, necessários apenas para execução no autor de AEM

![Incorporação de pacotes](assets/embeddeds.png)

Para público alvo do autor do AEM, da publicação do AEM ou de ambos, o pacote é incorporado no pacote do `all` container em um local de pasta especial, no seguinte formato:

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

Detalhando a estrutura desta pasta:

+ A pasta de primeiro nível **deve ser** `/apps`.
+ A pasta de segundo nível representa o aplicativo com `-packages` post-fixed no nome da pasta. Muitas vezes, há apenas uma única pasta de segundo nível na qual todos os subpacotes são incorporados, no entanto, qualquer número de pastas de segundo nível pode ser criado para melhor representar a estrutura lógica do aplicativo:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Por convenção, as pastas incorporadas do pacote secundário são nomeadas com o sufixo `-packages`. Isso garante que o código de implantação e os pacotes de conteúdo **não** sejam implantados nas pastas de destino de qualquer pacote secundário `/apps/<app-name>/...` que resulte em comportamento de instalação destrutivo e cíclico.

+ A pasta de terceiro nível deve ser
   `application` ou `content`
   + A `application` pasta contém pacotes de códigos
   + A `content` pasta contém pacotes de conteúdo. Esse nome de pasta deve corresponder aos tipos [de](#package-types) pacote dos pacotes que contém.
+ A pasta de 4º nível contém os pacotes secundários e deve ser uma das seguintes:
   + `install` para instalar no autor do AEM **e** na publicação do AEM
   + `install.author` para instalar **somente** no autor do AEM
   + `install.publish` para instalar **somente** no AEM publishObserve que somente `install.author` e `install.publish` são públicos alvos suportados. Outros modos de execução **não são** compatíveis.

Por exemplo, uma implantação que contenha o autor do AEM e publique pacotes específicos pode ser semelhante ao seguinte:

+ `all` O pacote de Container incorpora os seguintes pacotes para criar um artefato de implantação singular
   + `ui.apps` incorporado em `/apps/my-app-packages/application/install` implanta o código para o autor do AEM e para a publicação do AEM
   + `ui.apps.author` incorporado em `/apps/my-app-packages/application/install.author` implanta código somente para autor de AEM
   + `ui.content` incorporado na implantação `/apps/my-app-packages/content/install` do conteúdo e da configuração para o autor do AEM e para a publicação do AEM
   + `ui.content.publish` incorporado em `/apps/my-app-packages/content/install.publish` implanta conteúdo e configuração somente para publicação do AEM

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-embeddeds) POM abaixo para obter um trecho completo.

### Definição de Filtro do Pacote de Container {#container-package-filter-definition}

Devido à incorporação dos subpacotes de código e conteúdo no pacote de container, os caminhos de públicos alvos incorporados devem ser adicionados ao projeto do container `filter.xml` para garantir que os pacotes incorporados sejam incluídos no pacote do container quando criados.

Basta adicionar as `<filter root="/apps/<my-app>-packages"/>` entradas para qualquer pasta de segundo nível que contenha subpacotes a serem implantados.

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-container-package-filters) POM abaixo para obter um trecho completo.

## Como incorporar pacotes de terceiros {#embedding-3rd-party-packages}

Todos os pacotes devem estar disponíveis no repositório [público de artefatos Maven da](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) Adobe ou em um repositório de artefatos Maven de terceiros acessível e referenciável.

Se os pacotes de terceiros estiverem no **repositório público de artefatos Maven da Adobe**, nenhuma configuração adicional será necessária para o Adobe Cloud Manager resolver os artefatos.

Se os pacotes de terceiros estiverem em um **repositório de artefatos Maven de terceiros público**, esse repositório deverá ser registrado no `pom.xml` do projeto e incorporado de acordo com o método [descrito acima](#embeddeds). Se o aplicativo/conector de terceiros exigir pacotes de código e conteúdo, cada um deles deve ser incorporado aos locais corretos no pacote do contêiner (`all`).

A adição de dependências Maven segue as práticas padrão de Maven e a incorporação de artefatos de terceiros (pacotes de código e conteúdo) são [descritas acima](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-3rd-party-maven-repositories) POM abaixo para obter um trecho completo.

## Dependências do pacote entre os pacotes `ui.apps` dos `ui.content` pacotes {#package-dependencies}

A fim de garantir a instalação correta das embalagens, recomenda-se estabelecer as dependências entre embalagens.

A regra geral é que os pacotes que contêm conteúdo mutável (`ui.content`) devem depender do código imutável (`ui.apps`) que suporta a renderização e o uso do conteúdo mutável.

Uma exceção notável a essa regra geral é se o pacote de código imutável (`ui.apps` ou qualquer outro) __contiver apenas__ pacotes OSGi. Em caso afirmativo, nenhum pacote do AEM deve declarar uma dependência dele. Isso ocorre porque os pacotes de código imutáveis ____ que contêm pacotes OSGi não estão registrados no AEM Package Manager e, portanto, qualquer pacote AEM que dependa dele terá uma dependência insatisfatória e não será instalado.

>[!TIP]
>
>Consulte a seção Trechos [XML](#xml-package-dependencies) POM abaixo para obter um trecho completo.

Os padrões comuns para dependências de pacotes de conteúdo são:

### Dependências do pacote de implantação simples {#simple-deployment-package-dependencies}

O caso simples define o pacote de conteúdo `ui.content` mutável para depender do pacote de código `ui.apps` imutável.

+ `all` não possui dependências
   + `ui.apps` não possui dependências
   + `ui.content` depende de `ui.apps`

### Dependências complexas do pacote de implantação {#complex-deploxment-package-dependencies}

Implantações complexas se expandem no caso simples e definem dependências entre o conteúdo mutável correspondente e os pacotes de código imutáveis. Conforme necessário, as dependências também podem ser estabelecidas entre pacotes de código imutáveis.

+ `all` não possui dependências
   + `ui.apps.common` não possui dependências
   + `ui.apps.site-a` depende de `ui.apps.common`
   + `ui.content.site-a` depende de `ui.apps.site-a`
   + `ui.apps.site-b` depende de `ui.apps.common`
   + `ui.content.site-b` depende de `ui.apps.site-b`

## Desenvolvimento local e implantação {#local-development-and-deployment}

As estruturas e a organização do projeto descritas neste artigo são instâncias do AEM de desenvolvimento local **totalmente compatíveis** .

## Trechos XML POM {#pom-xml-snippets}

A seguir estão trechos `pom.xml` de configuração Maven que podem ser adicionados aos projetos Maven para alinhar às recomendações acima.

### Tipos de encapsulamento {#xml-package-types}

Os pacotes de código e conteúdo, que são implantados como pacotes secundários, devem declarar um tipo de pacote de **aplicativo** ou **conteúdo**, dependendo do que eles contêm.

#### Tipos de encapsulamento de Container {#container-package-types}

O projeto container `all/pom.xml` não **declara um** `<packageType>`.

#### Tipos de encapsulamento de código (imutável) {#immutable-package-types}

Os pacotes de código devem definir `packageType` como `application`.

Na `ui.apps/pom.xml`, as diretivas de configuração de `<packageType>application</packageType>` compilação da declaração de `filevault-package-maven-plugin` plug-in declaram seu tipo de pacote.

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
        <name>${my-app.ui.apps}</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### Tipos de encapsulamento de conteúdo (variável) {#mutable-package-types}

Os pacotes de conteúdo devem definir `packageType` como `content`.

Na `ui.content/pom.xml`, a diretiva de configuração de `<packageType>content</packageType>` compilação da declaração de `filevault-package-maven-plugin` plug-in declara seu tipo de pacote.

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
        <name>${my-app.ui.content}</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Implantação de pacotes de marcação para o Adobe Cloud Manager {#cloud-manager-target}

Em todos os projetos que geram um pacote, **exceto** do projeto do contêiner (`all`), adicione `<cloudManagerTarget>none</cloudManagerTarget>` à configuração `<properties>` da declaração do plug-in `filevault-package-maven-plugin` para garantir que eles **não sejam** implantados pelo Adobe Cloud Manager. The container (`all`) package should be the singular package deployed via Cloud Manager, which in turn embeds all required code and content packages.

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

### Inicialização do Repo{#snippet-repo-init}

Os scripts de Inicialização do Repo que contêm os scripts de Inicialização do Repo são definidos na configuração de fábrica `RepositoryInitializer` OSGi por meio da `scripts` propriedade. Observe que, como esses scripts são definidos em configurações OSGi, eles podem ser facilmente escopo por modo de execução usando a semântica de `../config.<runmode>` pasta comum.

Observe que, como os scripts normalmente são declarações de várias linhas, é mais fácil defini-los no `.config` arquivo do que no formato de bases XML `sling:OsgiConfig` .

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

A propriedade `scripts` OSGi contém diretivas, conforme definido pela linguagem [de Inicialização do](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Apache Sling.

### Pacote de estrutura do repositório {#xml-repository-structure-package}

No `ui.apps/pom.xml` e em qualquer outra `pom.xml` que declare um pacote de códigos (`<packageType>application</packageType>`), adicione a seguinte configuração de pacote de estrutura de repositório ao plug-in FileVault Maven. Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

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

### Incorporação de subpacotes no pacote de Container {#xml-embeddeds}

Na `all/pom.xml`, adicione as seguintes `<embeddeds>` diretivas à declaração de `filevault-package-maven-plugin` plug-in. Lembre-se de **não** usar a `<subPackages>` configuração, pois isso incluirá os subpacotes em `/etc/packages` vez de `/apps/my-app-packages/<application|content>/install(.author|.publish)?`.

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

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
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

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### Definição de Filtro do Pacote de Container {#xml-container-package-filters}

No `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) do projeto `all`, **inclua** as pastas `-packages` que contêm pacotes secundários a serem implantados:

```xml
<filter root="/apps/my-app-packages"/>
```

Se vários `/apps/*-packages` forem usados nos públicos alvos incorporados, todos devem ser enumerados aqui.

### Repositórios Maven de terceiros {#xml-3rd-party-maven-repositories}

>[!WARNING]
> A adição de mais repositórios Maven pode estender os tempos de criação de maven, já que repositórios Maven adicionais serão verificados quanto às dependências.

No projeto do reator `pom.xml`, adicione quaisquer diretivas de repositório Maven público de terceiros. A `<repository>` configuração completa deve estar disponível no provedor de repositório de terceiros.

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

### Dependências do pacote entre os pacotes `ui.apps` dos `ui.content` pacotes {#xml-package-dependencies}

Na `ui.content/pom.xml`, adicione as seguintes `<dependencies>` diretivas à declaração de `filevault-package-maven-plugin` plug-in.

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

### Limpando a pasta de Públicos alvos do projeto do Container {#xml-clean-container-package}

Na página `all/pom.xml` , adicione o plug- `maven-clean-plugin` in que limpará o diretório do público alvo antes das compilações do Maven.

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

+ [Gerenciamento De Pacotes Usando O Maven](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [Plug-in FileVault Content Package Maven](http://jackrabbit.apache.org/filevault-package-maven-plugin/)