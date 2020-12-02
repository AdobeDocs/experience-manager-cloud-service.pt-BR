---
title: Estrutura de projetos do AEM
description: Saiba mais sobre como definir estruturas de pacote para implantação no Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: 1a282bdaca02f47d7936222da8522e74831a4572
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 13%

---


# Estrutura de projetos do AEM

>[!TIP]
>
>Familiarize-se com o [AEM Project Archetype básico use](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html) e o [Plug-in FileVault Content Maven](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html), uma vez que este artigo se baseia nesses aprendizados e conceitos.

Este artigo descreve as mudanças necessárias para que os projetos do Adobe Experience Manager Maven sejam AEM como Cloud Service compatíveis, garantindo que eles respeitem a divisão de conteúdo mutável e imutável, as dependências são estabelecidas para criar implantações determinísticas e não conflitantes e que sejam compactadas em uma estrutura implantável.

AEM implantações de aplicativos devem ser compostas por um único pacote AEM. Este pacote deve, por sua vez, conter subpacotes que contêm tudo o que o aplicativo exige para funcionar, incluindo código, configuração e qualquer conteúdo básico de suporte.

O AEM requer uma separação de **conteúdo** e **código**, ou seja, um único pacote de conteúdo **não pode** ser implantado em **ambos** `/apps` as áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer outra que não `/apps`) do repositório. Em vez disso, o aplicativo deve separar código e conteúdo em pacotes separados para implantação no AEM.

A estrutura do pacote descrita neste documento é compatível com **ambas** as implantações de desenvolvimento locais e implantações do serviço da AEM Cloud.

>[!TIP]
>
>As configurações descritas neste documento são fornecidas por [AEM Project Maven Archetype 24 ou posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutáveis vs. imutáveis do repositório {#mutable-vs-immutable}

`/apps` e `/libs`**são consideradas áreas imutáveis do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução).** Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

Tudo o resto no repositório, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. são todas áreas **mutável**, o que significa que podem ser alteradas no tempo de execução.

>[!WARNING]
>
>Como nas versões anteriores do AEM, `/libs` não deve ser modificado. Somente AEM código de produto pode ser implantado em `/libs`.

### Índices de Oak {#oak-indexes}

Os índices de Oak (`/oak:index`) são gerenciados especificamente pelo AEM como um processo de implantação de Cloud Service. Isso ocorre porque o Gerenciador de nuvem deve aguardar até que qualquer novo índice seja implantado e completamente indexado novamente antes de alternar para a nova imagem de código.

Por isso, embora os índices Oak sejam mutáveis em tempo de execução, eles devem ser implantados como código para que possam ser instalados antes que qualquer pacote mutável seja instalado. Portanto, as configurações `/oak:index` fazem parte do Pacote de código e não fazem parte do Pacote de conteúdo [conforme descrito abaixo](#recommended-package-structure).

>[!TIP]
>
>Para obter mais detalhes sobre a indexação em AEM como um Cloud Service, consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

## Estrutura do pacote recomendada {#recommended-package-structure}

![Estrutura do Pacote do Projeto Experience Manager](assets/content-package-organization.png)

Este diagrama fornece uma visão geral da estrutura do projeto e dos artefatos de implantação do pacote recomendados.

A estrutura de implantação do aplicativo recomendada é a seguinte:

### Pacotes de código / Pacotes OSGi

+ O arquivo Jar do pacote OSGi é gerado e incorporado diretamente no projeto inteiro.

+ O pacote `ui.apps` contém todo o código a ser implantado e só é implantado em `/apps`. Elementos comuns do pacote `ui.apps` incluem, mas não estão limitados a:
   + [Definições de componentes e ](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) scripts HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (via [Bibliotecas do cliente](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) Sobreposição de  `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurações com reconhecimento de contexto de fallback
      + `/apps/settings`
   + ACLs (permissões)
      + Qualquer `rep:policy` para qualquer caminho em `/apps`

+ O pacote `ui.config` contém todas as [configurações OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Pasta organizacional contendo definições de configuração OSGi específicas para modo de execução
      + `/apps/my-app/osgiconfig`
   + Pasta de configuração OSGi comum contendo configurações OSGi padrão que se aplicam a todos os AEM de público alvo
      + `/apps/my-app/osgiconfig/config`
   + Executar pastas de configuração OSGi específicas do modo que contêm configurações OSGi padrão que se aplicam a todos os AEM de público alvo
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init Scripts de configuração OSGi
      + [O ](#repo-init) Repo é a maneira recomendada de implantar conteúdo (mutável) que é logicamente parte do aplicativo AEM. As configurações do Repo Init OSGi devem estar localizadas na pasta `config.<runmode>` apropriada, conforme descrito acima, e devem ser usadas para definir:
         + Estruturas de conteúdo da linha de base
         + Usuários
         + Usuários do serviço
         + Grupos
         + ACLs (permissões)

### Pacotes de conteúdo

+ O pacote `ui.content` contém todo o conteúdo e a configuração. O Pacote de conteúdo contém todas as definições de nó que não estão nos pacotes `ui.apps` ou `ui.config`, ou em outras palavras, nada que não esteja em `/apps` ou `/oak:index`. Elementos comuns do pacote `ui.content` incluem, mas não estão limitados a:
   + Configurações sensíveis ao contexto
      + `/conf`
   + Estruturas de conteúdo necessárias e complexas (ou seja, Compilação de conteúdo que é criada e estende além das estruturas de conteúdo da Linha de base definidas no Repo Init.)
      + `/content`,  `/content/dam`etc.
   + Taxonomias de marcação controladas
      + `/content/cq:tags`
   + Nós herdados etc (idealmente, migre-os para locais diferentes/etc)
      + `/etc`

### Pacotes de container

+ O pacote `all` é um pacote de container que APENAS inclui artefatos implantáveis, os pacotes de Jar de pacote OSGI, `ui.apps`, `ui.config` e `ui.content` como incorporados. O pacote `all` não deve ter **nenhum conteúdo ou código** próprio, mas antes delegar toda a implantação ao repositório em seus subpacotes ou arquivos Jar de pacote OSGi.

   Os pacotes agora são incluídos usando a configuração incorporada do plug-in Maven [FileVault Package Maven](#embeddeds), em vez da configuração `<subPackages>`.

   Para implantações complexas de Experience Manager, pode ser desejável criar vários `ui.apps`, `ui.config` e `ui.content` projetos/pacotes que representem sites ou locatários específicos no AEM. Se isso for feito, verifique se a divisão entre conteúdo mutável e imutável é respeitada e se os pacotes de conteúdo e arquivos Jar de pacote OSGi são incorporados como subpacotes no pacote de conteúdo do container `all`.

   Por exemplo, uma estrutura complexa de pacote de conteúdo de implantação pode ter a seguinte aparência:

   + `all` o pacote de conteúdo incorpora os seguintes pacotes para criar um artefato de implantação singular
      + `common.ui.apps` implanta o código exigido pelo  **** site A e pelo site B
      + `site-a.core` Jar de pacote OSGi exigido pelo site A
      + `site-a.ui.apps` implanta o código exigido pelo site A
      + `site-a.ui.config` implanta configurações OSGi exigidas pelo Site A
      + `site-a.ui.content` implanta o conteúdo e a configuração necessários para o site A
      + `site-b.core` Jar de pacote OSGi exigido pelo site B
      + `site-b.ui.apps` implanta o código exigido pelo site B
      + `site-b.ui.config` implanta configurações OSGi exigidas pelo site B
      + `site-b.ui.content` implanta o conteúdo e a configuração necessários para o site B

### Pacotes de aplicativo extra{#extra-application-packages}

Se outros projetos AEM, que são eles mesmos compostos de seus próprios pacotes de código e conteúdo, forem usados pela implantação AEM, seus pacotes de container deverão ser incorporados ao pacote `all` do projeto.

Por exemplo, um projeto AEM que inclui dois aplicativos AEM de fornecedor pode ter a seguinte aparência:

+ `all` o pacote de conteúdo incorpora os seguintes pacotes para criar um artefato de implantação singular
   + `core` Jar de pacote OSGi exigido pelo aplicativo AEM
   + `ui.apps` implanta o código exigido pelo aplicativo AEM
   + `ui.config` implanta configurações OSGi exigidas pelo aplicativo AEM
   + `ui.content` implanta o conteúdo e a configuração necessários para o aplicativo AEM
   + `vendor-x.all` implanta tudo (código e conteúdo) exigido pelo aplicativo X do fornecedor
   + `vendor-y.all` implanta tudo (código e conteúdo) exigido pelo aplicativo Y do fornecedor

## Tipos de encapsulamento {#package-types}

As embalagens devem ser marcadas com o tipo de embalagem declarado.

+ Os pacotes de container devem definir `packageType` como `container`.
+ Os pacotes de código (imutável) devem definir `packageType` como `application`.
+ Os pacotes de conteúdo (mutável) devem definir `packageType` como `content`.

Para obter mais informações, consulte [Apache Jackrabbit FileVault - documentação do plug-in Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) e o [trecho de configuração FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) abaixo.

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-package-types) abaixo para obter um trecho completo.

## Marking Packages for Deployment pelo Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Por padrão, o Adobe Cloud Manager coleta todos os pacotes produzidos pela compilação Maven. No entanto, como o pacote do contêiner (`all`) é o artefato de implantação singular que contém todos os pacotes de código e conteúdo, devemos garantir que **somente** o pacote do contêiner (`all`) seja implantado. Para garantir isso, outros pacotes gerados pela compilação Maven devem ser marcados com a configuração do Plug-in FileVault Content Package Maven do `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#pom-xml-snippets) abaixo para obter um trecho completo.

## Inicialização do acordo{#repo-init}

A Inicialização do Repo fornece instruções, ou scripts, que definem estruturas JCR, desde estruturas de nós comuns, como árvores de pastas, até usuários, usuários de serviços, grupos e definição de ACL.

Os principais benefícios do Repo Init são ter permissões implícitas para executar todas as ações definidas pelos scripts e serem chamadas no início do ciclo de vida da implantação, garantindo que todas as estruturas JCR necessárias existam até que o código seja executado.

Enquanto os próprios scripts de Inicialização de acordo com o Repo funcionam no projeto `ui.config` como scripts, eles podem e devem ser usados para definir as seguintes estruturas mutáveis:

+ Estruturas de conteúdo da linha de base
+ Usuários do serviço
+ Usuários
+ Grupos
+ ACLs

Os scripts de Inicialização do Repo são armazenados como entradas `scripts` de `RepositoryInitializer` configurações de fábrica OSGi e, portanto, podem ser implicitamente direcionados pelo modo de execução, permitindo diferenças entre os scripts de Inicialização do AEM Author e do AEM Publish Services, ou mesmo entre ambientes (Dev, Stage e Prod).

As configurações OSGi de inicialização de acordo com o repo são escritas melhor no [`.config` formato de configuração OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1), pois oferecem suporte a várias linhas, o que é uma exceção às práticas recomendadas de usar [`.cfg.json` para definir configurações OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Observe que, ao definir Usuários e Grupos, somente grupos são considerados parte do aplicativo e integrantes de sua função devem ser definidos aqui. Os utilizadores e grupos da organização devem ainda ser definidos em tempo de execução no AEM; por exemplo, se um fluxo de trabalho personalizado atribuir trabalho a um Grupo nomeado, esse Grupo deverá ser definido por meio da Inicialização de Repo no aplicativo AEM, no entanto, se o Agrupamento for meramente organizacional, como &quot;Equipe de Wendy&quot; e &quot;Equipe de Sean&quot;, eles serão melhor definidos e gerenciados no tempo de execução em AEM.

>[!TIP]
>
>Os scripts de Inicialização do Repo *devem* ser definidos no campo em linha `scripts` e a configuração `references` não funcionará.

O vocabulário completo para scripts de inicialização do Repo está disponível na [documentação de inicialização do Apache Sling Repo](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte a seção [Trechos de inicialização do Repo](#snippet-repo-init) abaixo para obter um trecho completo.

## Pacote de estrutura do repositório {#repository-structure-package}

Pacotes de código exigem a configuração do plug-in FileVault Maven para fazer referência a `<repositoryStructurePackage>` que aplica a correção das dependências estruturais (para garantir que um pacote de código não seja instalado sobre outro). Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

Isso **só é necessário** em Pacotes de código, ou seja, qualquer pacote marcado com `<packageType>application</packageType>`.

Para saber como criar um pacote de estrutura de repositório para seu aplicativo, consulte [Desenvolver um pacote de estrutura de repositório](repository-structure-package.md).

Observe que os pacotes de conteúdo (`<packageType>content</packageType>`) **não** exigem este Pacote de estrutura de repositório.

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-repository-structure-package) abaixo para obter um trecho completo.

## Incorporação de subpacotes no Pacote de Container{#embeddeds}

Os pacotes de conteúdo ou código são colocados em uma pasta especial &quot;carro lateral&quot; e podem ser direcionados para instalação AEM autor, AEM publicação ou ambos, usando a configuração `<embeddeds>` do plug-in FileVault Maven. Observe que a configuração `<subPackages>` não deve ser usada.

Os casos de uso frequentes incluem:

+ ACLs/permissões que diferem entre AEM usuários do autor e AEM usuários de publicação
+ Configurações usadas para suportar atividades somente AEM autor
+ Código como integrações com sistemas de back-office, necessário apenas para execução AEM autor

![Incorporação de pacotes](assets/embeddeds.png)

Para AEM autor, AEM publicar ou ambos, o pacote é incorporado no pacote de container `all` em uma pasta-local especial, no seguinte formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Detalhando a estrutura desta pasta:

+ A pasta de primeiro nível **tem de ser** `/apps`.
+ A pasta de segundo nível representa o aplicativo com `-packages` corrigido no nome da pasta. Muitas vezes, há apenas uma única pasta de segundo nível na qual todos os subpacotes são incorporados, no entanto, qualquer número de pastas de segundo nível pode ser criado para melhor representar a estrutura lógica do aplicativo:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Por convenção, as pastas incorporadas do pacote secundário são nomeadas com o sufixo `-packages`. Isso garante que o código de implantação e os pacotes de conteúdo **não** sejam implantados nas pastas de destino de qualquer pacote secundário `/apps/<app-name>/...` que resulte em comportamento de instalação destrutivo e cíclico.

+ A pasta de terceiro nível deve ser
   `application`,  `content` ou  `container`
   + A pasta `application` contém pacotes de códigos
   + A pasta `content` contém pacotes de conteúdo
   + A pasta `container` contém [pacotes de aplicativo extra](#extra-application-packages) que podem ser incluídos pelo aplicativo AEM.
O nome desta pasta corresponde aos [tipos de pacote](#package-types) dos pacotes que contém.
+ A pasta de 4º nível contém os pacotes secundários e deve ser uma das seguintes:
   + `install` para instalar no autor do AEM **e** na publicação do AEM
   + `install.author` para instalar **somente** no autor do AEM
   + `install.publish` para instalar  **** somente AEM publicar Observe que somente  `install.author` e  `install.publish` são públicos alvos suportados. Outros modos de execução **não são** compatíveis.

Por exemplo, uma implantação que contém AEM pacotes específicos de autor e publicação pode ser semelhante ao seguinte:

+ `all` O pacote de container incorpora os seguintes pacotes para criar um artefato de implantação singular
   + `ui.apps` incorporado na  `/apps/my-app-packages/application/install` implanta código para AEM autor e publicação AEM
   + `ui.apps.author` incorporado na  `/apps/my-app-packages/application/install.author` implanta código somente AEM autor
   + `ui.content` incorporado na  `/apps/my-app-packages/content/install` implanta conteúdo e configuração para AEM autor e publicação AEM
   + `ui.content.publish` incorporado na  `/apps/my-app-packages/content/install.publish` implanta conteúdo e configuração somente para AEM publicação

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-embeddeds) abaixo para obter um trecho completo.

### Definição de Filtro do Pacote de container {#container-package-filter-definition}

Devido à incorporação dos subpacotes de código e conteúdo no pacote de container, os caminhos de públicos alvos incorporados devem ser adicionados ao `filter.xml` do projeto de container para garantir que os pacotes incorporados sejam incluídos no pacote de container quando criados.

Basta adicionar as entradas `<filter root="/apps/<my-app>-packages"/>` para qualquer pasta de segundo nível que contenha subpacotes a serem implantados.

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-container-package-filters) abaixo para obter um trecho completo.

## Incorporando pacotes de terceiros {#embedding-3rd-party-packages}

Todos os pacotes devem estar disponíveis através do repositório de artefatos Maven público[ ou de um repositório de artefatos Maven de terceiros acessível e referenciável.](https://repo.adobe.com/nexus/content/groups/public/com/adobe/)

Se os pacotes de terceiros estiverem no **repositório público de artefatos Maven da Adobe**, nenhuma configuração adicional será necessária para o Adobe Cloud Manager resolver os artefatos.

Se os pacotes de terceiros estiverem em um **repositório de artefatos Maven de terceiros público**, esse repositório deverá ser registrado no `pom.xml` do projeto e incorporado de acordo com o método [descrito acima](#embeddeds).

Os conectores/aplicativos de terceiros devem ser incorporados usando seu pacote `all` como um container no pacote container (`all`) do seu projeto.

A adição de dependências Maven segue as práticas padrão de Maven e a incorporação de artefatos de terceiros (pacotes de código e conteúdo) são [descritas acima](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-3rd-party-maven-repositories) abaixo para obter um trecho completo.

## Dependências do pacote entre `ui.apps` de `ui.content` pacotes {#package-dependencies}

A fim de garantir a instalação correta das embalagens, recomenda-se estabelecer as dependências entre embalagens.

A regra geral é que os pacotes que contêm conteúdo mutável (`ui.content`) devem depender do código imutável (`ui.apps`) que suporta a renderização e o uso do conteúdo mutável.

Uma exceção notável a essa regra geral é se o pacote de código imutável (`ui.apps` ou qualquer outro), __only__ contém pacotes OSGi. Em caso afirmativo, nenhum pacote AEM deve declarar uma dependência do mesmo. Isso ocorre porque os pacotes de código imutáveis __only__ que contêm pacotes OSGi não estão registrados AEM Gerenciador de Pacotes e, portanto, qualquer pacote AEM que dependa dele terá uma dependência insatisfeita e não será instalado.

>[!TIP]
>
>Consulte a seção [Trechos XML do POM](#xml-package-dependencies) abaixo para obter um trecho completo.

Os padrões comuns para dependências de pacotes de conteúdo são:

### Dependências do Pacote de Implantação Simples {#simple-deployment-package-dependencies}

O caso simples define o pacote de conteúdo mutável `ui.content` para depender do pacote de código imutável `ui.apps`.

+ `all` não possui dependências
   + `ui.apps` não possui dependências
   + `ui.content` depende de  `ui.apps`

### Dependências complexas do pacote de implantação {#complex-deploxment-package-dependencies}

Implantações complexas se expandem no caso simples e definem dependências entre o conteúdo mutável correspondente e os pacotes de código imutáveis. Conforme necessário, as dependências também podem ser estabelecidas entre pacotes de código imutáveis.

+ `all` não possui dependências
   + `common.ui.apps.common` não possui dependências
   + `site-a.ui.apps` depende de  `common.ui.apps`
   + `site-a.ui.content` depende de  `site-a.ui.apps`
   + `site-b.ui.apps` depende de  `common.ui.apps`
   + `site-b.ui.content` depende de  `site-b.ui.apps`

## Desenvolvimento local e implantação {#local-development-and-deployment}

As estruturas e a organização do projeto descritas neste artigo são **instâncias de desenvolvimento local** totalmente compatíveis.

## Trechos XML de POM {#pom-xml-snippets}

A seguir estão trechos de configuração Maven `pom.xml` que podem ser adicionados aos projetos Maven para alinhar às recomendações acima.

### Tipos de encapsulamento {#xml-package-types}

Os pacotes de código e conteúdo, que são implantados como pacotes secundários, devem declarar um tipo de pacote de **aplicativo** ou **conteúdo**, dependendo do que eles contêm.

#### Tipos de pacotes de container {#container-package-types}

O container `all/pom.xml` projeto **não** declara um `<packageType>`.

#### Tipos de encapsulamento de código (imutável) {#immutable-package-types}

Os pacotes de código devem definir `packageType` como `application`.

Em `ui.apps/pom.xml`, as `<packageType>application</packageType>` diretivas de configuração de compilação da declaração de plug-in `filevault-package-maven-plugin` declaram seu tipo de pacote.

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

#### Tipos de encapsulamento de conteúdo (variável) {#mutable-package-types}

Os pacotes de conteúdo devem definir `packageType` como `content`.

Na `ui.content/pom.xml`, a diretiva `<packageType>content</packageType>` de configuração de compilação da declaração de plug-in `filevault-package-maven-plugin` declara seu tipo de pacote.

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

### Marking Packages for Adobe Cloud Manager Deployment {#cloud-manager-target}

Em todos os projetos que geram um pacote, **exceto** do projeto do contêiner (`all`), adicione `<cloudManagerTarget>none</cloudManagerTarget>` à configuração `<properties>` da declaração do plug-in `filevault-package-maven-plugin` para garantir que eles **não sejam** implantados pelo Adobe Cloud Manager. O pacote de container (`all`) deve ser o único pacote implantado pelo Cloud Manager, que por sua vez incorpora todos os pacotes de código e conteúdo necessários.

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

### Inicialização do acordo{#snippet-repo-init}

Os scripts de Inicialização do Repo que contêm os scripts de Inicialização do Repo são definidos na configuração de fábrica `RepositoryInitializer` OSGi por meio da propriedade `scripts`. Observe que, como esses scripts são definidos nas configurações do OSGi, eles podem ser facilmente delimitados pelo modo de execução usando a semântica habitual de `../config.<runmode>` pasta.

Observe que, como os scripts normalmente são declarações de várias linhas, é mais fácil defini-los no arquivo `.config` do que no formato `.cfg.json` baseado em JSON.

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

No `ui.apps/pom.xml` e em qualquer outro `pom.xml` que declare um pacote de códigos (`<packageType>application</packageType>`), adicione a seguinte configuração de pacote de estrutura de repositório ao plug-in FileVault Maven. Você pode [criar seu próprio pacote de estrutura de repositório para seu projeto](repository-structure-package.md).

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

Na declaração `all/pom.xml`, adicione as seguintes diretivas `<embeddeds>` à declaração de plug-in `filevault-package-maven-plugin`. Lembre-se de que **não** usa a configuração `<subPackages>`, pois isso incluirá os subpacotes em `/etc/packages` em vez de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definição de Filtro do Pacote de container {#xml-container-package-filters}

No `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) do projeto `all`, **inclua** as pastas `-packages` que contêm pacotes secundários a serem implantados:

```xml
<filter root="/apps/my-app-packages"/>
```

Se vários `/apps/*-packages` forem usados nos públicos alvos incorporados, todos devem ser enumerados aqui.

### Repositórios Maven de terceiros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>A adição de mais repositórios Maven pode estender os tempos de criação de maven, já que repositórios Maven adicionais serão verificados quanto às dependências.

No `pom.xml` do projeto do reator, adicione quaisquer diretivas de repositório Maven público de terceiros necessárias. A configuração completa `<repository>` deve estar disponível no provedor de repositório de terceiros.

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

### Dependências do pacote entre `ui.apps` de `ui.content` pacotes {#xml-package-dependencies}

Na declaração `ui.content/pom.xml`, adicione as seguintes diretivas `<dependencies>` à declaração de plug-in `filevault-package-maven-plugin`.

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

No `all/pom.xml`, adicione o plug-in `maven-clean-plugin` que limpará o diretório do público alvo antes de uma construção de Maven.

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