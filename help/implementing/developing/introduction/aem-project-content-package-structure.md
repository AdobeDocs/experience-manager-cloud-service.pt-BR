---
title: Estrutura de projetos do AEM
description: Saiba mais sobre como definir estruturas de pacote para implantação no Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 4%

---

# Estrutura de projetos do AEM

>[!TIP]
>
>Familiarize-se com o [uso do Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) básico e com o [Plug-in FileVault Content Maven](/help/implementing/developing/tools/maven-plugin.md), pois este artigo se baseia nesses aprendizados e conceitos.

Este artigo descreve as alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM as a Cloud Service, garantindo que eles respeitem a divisão de conteúdo mutável e imutável. Além disso, as dependências são estabelecidas para criar implantações determinísticas e não conflitantes e são agrupadas em uma estrutura implantável.

As implantações de aplicativos do AEM devem ser compostas por um único pacote do AEM. Este pacote deve, por sua vez, conter subpacotes que incluem tudo o que o aplicativo exige para funcionar, incluindo código, configuração e qualquer conteúdo de linha de base de suporte.

O AEM requer uma separação de **conteúdo** e **código**, o que significa que um único pacote de conteúdo **não pode** ser implantado em **ambas** `/apps` e áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer coisa que não seja `/apps`) do repositório. Em vez disso, o aplicativo deve separar código e conteúdo em pacotes separados para implantação no AEM.

A estrutura do pacote descrita neste documento é compatível com **ambas** as implantações de desenvolvimento locais e implantações do serviço da AEM Cloud.

>[!TIP]
>
>As configurações descritas neste documento são fornecidas pelo [Arquétipo Maven de projeto do AEM 24 ou posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutáveis versus imutáveis do repositório {#mutable-vs-immutable}

As áreas `/apps` e `/libs` do AEM são consideradas **imutáveis** porque não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução). Qualquer tentativa de alterar uma área imutável no tempo de execução falha.

Todo o restante no repositório, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp` e assim por diante, são áreas **mutáveis**, o que significa que podem ser alteradas em tempo de execução.

>[!WARNING]
>
>Como nas versões anteriores do AEM, `/libs` não deve ser modificado. Somente o código de produto da AEM pode ser implantado em `/libs`.

### Índices Oak {#oak-indexes}

Os índices Oak (`/oak:index`) são gerenciados pelo processo de implantação do AEM as a Cloud Service. O motivo é que o Cloud Manager deve aguardar até que qualquer novo índice seja implantado e totalmente reindexado antes de alternar para a nova imagem de código.

Por isso, embora os índices Oak sejam mutáveis no tempo de execução, eles devem ser implantados como código para que possam ser instalados antes que qualquer pacote mutável seja instalado. Portanto, as configurações de `/oak:index` fazem parte do Pacote de Código e não do Pacote de Conteúdo [conforme descrito abaixo](#recommended-package-structure).

>[!TIP]
>
>Para obter mais detalhes sobre indexação no AEM as a Cloud Service, consulte [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

## Estrutura de pacotes recomendada {#recommended-package-structure}

![Estrutura do Pacote de Projetos Experience Manager](assets/content-package-organization.png)

Este diagrama fornece uma visão geral da estrutura de projeto recomendada e dos artefatos de implantação de pacote.

A estrutura de implantação de aplicativo recomendada é a seguinte:

### Pacotes de código / pacotes OSGi

+ O arquivo Jar do pacote OSGi é gerado e incorporado diretamente em todo o projeto.

+ O pacote `ui.apps` contém todo o código a ser implantado e só é implantado em `/apps`. Elementos comuns do pacote `ui.apps` incluem, mas não estão limitados a:
   + [Definições de componentes e scripts HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR)
      + `/apps/my-app/components`
   + JavaScript e CSS (via [Bibliotecas de Clientes](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Sobreposições](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/` e assim por diante.
   + Configurações sensíveis ao contexto de fallback
      + `/apps/settings`
   + ACLs (permissões)
      + Qualquer `rep:policy` para qualquer caminho em `/apps`
   + [Scripts agrupados pré-compilados](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>O mesmo código deve ser implantado em todos os ambientes. Esse código garante um nível de confiança de que as validações no ambiente de preparo também estão em produção. Para obter mais informações, consulte a seção sobre [Runmodes](/help/implementing/deploying/overview.md#runmodes).


### Pacotes de conteúdo

+ O pacote `ui.content` contém todo o conteúdo e configuração. O Pacote de Conteúdo contém todas as definições de nó que não estão nos pacotes `ui.apps` ou `ui.config` ou, em outras palavras, que não estão em `/apps` ou `/oak:index`. Elementos comuns do pacote `ui.content` incluem, mas não estão limitados a:
   + Configurações sensíveis ao contexto
      + `/conf`
   + Estruturas de conteúdo complexas e necessárias (ou seja, criação de conteúdo que se baseia em e estende estruturas de conteúdo de linha de base anteriores definidas na inicialização de repositório).
      + `/content`, `/content/dam` e assim por diante.
   + Taxonomias de marcação controladas
      + `/content/cq:tags`
   + Nós etc herdados (idealmente, migre esses nós para locais que não são/etc)
      + `/etc`

### Pacotes de contêineres

+ O pacote `all` é um pacote de contêiner que APENAS inclui artefatos implantáveis, o arquivo Jar do pacote OSGI, `ui.apps`, `ui.config` e `ui.content` pacotes como incorporados. O pacote `all` não deve ter **nenhum conteúdo ou código** próprio, mas deve delegar toda a implantação no repositório em seus subpacotes ou arquivos Jar de pacote OSGi.

  Agora os pacotes são incluídos usando a [&#x200B; configuração incorporada do plug-in Maven &#x200B;](#embeddeds)FileVault Package Maven, em vez da `<subPackages>` configuração.

  Para implantações complexas do Experience Manager, pode ser desejável criar vários projetos/pacotes do `ui.apps`, `ui.config` e `ui.content` que representem sites ou locatários específicos no AEM. Se essa abordagem for feita, verifique se a divisão entre conteúdo mutável e imutável é respeitada, e se os pacotes de conteúdo necessários e os arquivos Jar do pacote OSGi estão incorporados como subpacotes no pacote de conteúdo do contêiner `all`.

  Por exemplo, uma estrutura complexa de pacote de conteúdo de implantação pode ter esta aparência:

   + O pacote de conteúdo `all` incorpora os seguintes pacotes, para criar um artefato de implantação singular
      + `common.ui.apps` implanta o código exigido por **ambos** site A e site B
      + `site-a.core` Jar do pacote OSGi exigido pelo site A
      + `site-a.ui.apps` implanta o código exigido pelo site A
      + `site-a.ui.config` implanta as configurações de OSGi exigidas pelo Site A
      + `site-a.ui.content` implanta o conteúdo e a configuração exigidos pelo site A
      + Jar do pacote OSGi `site-b.core` exigido pelo site B
      + `site-b.ui.apps` implanta o código exigido pelo site B
      + `site-b.ui.config` implanta as configurações de OSGi exigidas pelo site B
      + `site-b.ui.content` implanta o conteúdo e a configuração exigidos pelo site B

+ O pacote `ui.config` contém todas as [configurações OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Código considerado e pertence a pacotes OSGi, mas não contém nós de conteúdo regulares. Assim, ele é marcado como um pacote de contêiner
   + Pasta organizacional contendo definições de configuração OSGi específicas do modo de execução
      + `/apps/my-app/osgiconfig`
   + Pasta de configuração OSGi comum contendo configurações OSGi padrão que se aplicam a todos os destinos de implantação do AEM as a Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Executar pastas de configuração OSGi específicas do modo que contenham configurações OSGi padrão aplicáveis a todos os destinos de implantação do AEM as a Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Scripts de configuração do OSGi de inicialização do repositório
      + [Inicialização do repositório](#repo-init) é a maneira recomendada de implantar conteúdo (mutável) que logicamente faz parte do aplicativo do AEM. As configurações do OSGi de inicialização do repositório devem ser colocadas na pasta `config.<runmode>` apropriada, conforme descrito acima, e devem ser usadas para definir:
         + Estruturas de conteúdo de linha de base
         + Usuários
         + Usuários do serviço
         + Grupos
         + ACLs (permissões)

### Pacotes de Aplicativos Adicionais{#extra-application-packages}

Se outros Projetos do AEM - que são eles mesmos compostos de seus próprios pacotes de código e conteúdo - forem usados pela implantação do AEM, seus pacotes de contêiner deverão ser incorporados ao pacote `all` do projeto.

Por exemplo, um projeto do AEM que inclui aplicativos AEM de dois fornecedores pode ser semelhante a:

+ O pacote de conteúdo `all` incorpora os seguintes pacotes, para criar um artefato de implantação singular
   + Jar do pacote OSGi `core` exigido pelo aplicativo AEM
   + `ui.apps` implanta o código exigido pelo aplicativo AEM
   + O `ui.config` implanta as configurações de OSGi exigidas pelo aplicativo do AEM
   + `ui.content` implanta o conteúdo e a configuração exigidos pelo aplicativo AEM
   + `vendor-x.all` implanta tudo (código e conteúdo) exigido pelo aplicativo X do fornecedor
   + `vendor-y.all` implanta tudo (código e conteúdo) exigido pelo aplicativo Y do fornecedor

## Tipos de encapsulamento {#package-types}

Os pacotes devem ser marcados com o tipo de pacote declarado. Os tipos de pacote ajudam a esclarecer a finalidade e a implantação de um pacote.

+ Os pacotes de contêineres devem definir seu `packageType` como `container`. Os pacotes de contêineres não devem conter nós regulares. Somente pacotes OSGi, configurações e pacotes secundários são permitidos. Os contêineres no AEM as a Cloud Service não podem usar [ganchos de instalação](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Os pacotes de código (imutáveis) devem definir seus `packageType` como `application`.
+ Os pacotes de conteúdo (mutáveis) devem definir seus `packageType` como `content`.


Para obter mais informações, consulte [Apache Jackrabbit FileVault - documentação do plug-in Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipos de pacote Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html) e o [trecho de configuração FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) abaixo.

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-package-types) abaixo para obter um trecho completo.

## Marcação de pacotes para implantação pelo Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Por padrão, o Adobe Cloud Manager coleta todos os pacotes produzidos pela compilação Maven. No entanto, como o pacote do contêiner (`all`) é o artefato de implantação singular que contém todos os pacotes de código e conteúdo, você deve garantir que **somente** o pacote do contêiner (`all`) seja implantado. Para garantir isso, outros pacotes gerados pela compilação Maven devem ser marcados com a configuração do Plug-in FileVault Content Package Maven do `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#pom-xml-snippets) abaixo para obter um trecho completo.

## Inicialização do repositório{#repo-init}

A Inicialização do repositório fornece instruções, ou scripts, que definem estruturas JCR, que variam de estruturas de nó comuns, como árvores de pastas, a usuários, usuários de serviço, grupos e definição de ACL.

Os principais benefícios do Repo Init são que eles têm permissões implícitas para executar todas as ações definidas por seus scripts. E esses scripts são chamados no início do ciclo de vida da implantação, garantindo que todas as estruturas JCR necessárias existam até o código ser executado.

Embora os scripts de Inicialização de repositório estejam no projeto `ui.config` como scripts, eles podem e devem ser usados para definir as seguintes estruturas mutáveis:

+ Estruturas de conteúdo de linha de base
+ Usuários do serviço
+ Usuários
+ Grupos
+ ACLs

Os scripts de Inicialização de repositório são armazenados como `scripts` entradas de `RepositoryInitializer` configurações de fábrica OSGi. Dessa forma, eles podem ser direcionados implicitamente pelo modo de execução, permitindo diferenças entre o Autor do AEM e os scripts de Inicialização de repositório do AEM Publish Services ou até mesmo entre ambientes (Desenvolvimento, Preparo e Produção).

As configurações OSGi de Inicialização de repositório são escritas com êxito no [`.config` formato de configuração OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1), pois oferecem suporte a várias linhas, o que é uma exceção às práticas recomendadas de uso do [`.cfg.json` para definir configurações OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Ao definir Usuários e Grupos, somente os grupos são considerados parte do aplicativo e parte integrante de sua função. Você ainda define Usuários e grupos da organização no tempo de execução no AEM. Por exemplo, se um fluxo de trabalho personalizado atribuir trabalho a um Grupo nomeado, defina esse Grupo por meio da Inicialização de repositório no aplicativo do AEM. No entanto, se o Agrupamento é meramente organizacional, como &quot;Wendy&#39;s Team&quot; e &quot;Sean&#39;s Team&quot;, esses grupos são melhor definidos e gerenciados no tempo de execução no AEM.

>[!TIP]
>
>Os scripts de Inicialização de repositório *devem* ser definidos no campo `scripts` embutido ou a configuração `references` não funciona.

O vocabulário completo para scripts de inicialização de repositório está disponível na [documentação de inicialização de repositório do Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte a seção [Snippets de inicialização de repositório](#snippet-repo-init) abaixo para obter um trecho completo.

## Pacote de estrutura do repositório {#repository-structure-package}

Os pacotes de código exigem a configuração do plug-in FileVault Maven para referenciar um `<repositoryStructurePackage>` que imponha a correção de dependências estruturais (para garantir que um pacote de código não seja instalado sobre outro). Você pode [criar seu próprio pacote de estrutura de repositório para o projeto](repository-structure-package.md).

**Necessário** somente para pacotes de código, ou seja, qualquer pacote marcado com `<packageType>application</packageType>`.

Para saber como criar um pacote de estrutura de repositório para seu aplicativo, consulte [Desenvolver um Pacote de Estrutura de Repositório](repository-structure-package.md).

Os pacotes de conteúdo (`<packageType>content</packageType>`) **não** exigem esse Pacote de estrutura de repositório.

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-repository-structure-package) abaixo para obter um trecho completo.

## Incorporação de subpacotes no pacote de container{#embeddeds}

O conteúdo ou os pacotes de código são colocados em uma pasta especial de &quot;carro lateral&quot; e podem ser direcionados para instalação no autor do AEM, na publicação do AEM ou em ambos, usando a configuração `<embeddeds>` do plug-in FileVault Maven. Não use a configuração `<subPackages>`.

Casos de uso comuns incluem:

+ ACLs/permissões que diferem entre os usuários autores do AEM e os usuários de publicação do AEM
+ Configurações usadas para oferecer suporte a atividades somente no autor do AEM
+ Código, como integrações com sistemas de back-office, necessário apenas para execução no autor do AEM

![Incorporando Pacotes](assets/embeddeds.png)

Para direcionar o autor do AEM, o AEM publica ou ambos, o pacote é incorporado no pacote de contêiner `all` em um local de pasta especial, no seguinte formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Analisando a estrutura desta pasta:

+ A pasta de primeiro nível **deve ser** `/apps`.
+ A pasta de segundo nível representa o aplicativo com `-packages` pós-corrigido para o nome da pasta. Geralmente, há apenas uma única pasta de segundo nível em que todos os subpacotes são incorporados. No entanto, qualquer número de pastas de segundo nível pode ser criada para melhor representar a estrutura lógica do aplicativo:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >Por convenção, as pastas incorporadas do subpacote são nomeadas com o sufixo `-packages`. Esse nome garante que o código de implantação e os pacotes de conteúdo sejam **não** implantados nas pastas de destino de qualquer subpacote `/apps/<app-name>/...`, o que resulta em comportamento de instalação destrutivo e cíclico.

+ A pasta de terceiro nível deve ser
  `application`, `content` ou `container`
   + A pasta `application` contém pacotes de código
   + A pasta `content` contém pacotes de conteúdo
   + A pasta `container` contém [pacotes de aplicativos extras](#extra-application-packages) que podem ser incluídos pelo aplicativo AEM.
Este nome de pasta corresponde aos [tipos de pacote](#package-types) dos pacotes que ele contém.
+ A pasta de 4º nível contém os subpacotes e deve ser uma das seguintes:
   + `install` para que você instale em **o autor do AEM e a publicação do AEM**
   + `install.author` para instalar **somente** no autor do AEM
   + `install.publish` para instalar **somente** na publicação do AEM
Somente `install.author` e `install.publish` são destinos com suporte. Outros modos de execução **não são** compatíveis.

Por exemplo, uma implantação que contém pacotes específicos do autor e da publicação do AEM pode ser semelhante ao seguinte:

+ O pacote de contêiner `all` incorpora os seguintes pacotes, para criar um artefato de implantação singular
   + O `ui.apps` incorporado no `/apps/my-app-packages/application/install` implanta o código para o autor do AEM e para a publicação do AEM
   + `ui.apps.author` incorporado em `/apps/my-app-packages/application/install.author` implanta o código somente para o autor do AEM
   + O `ui.content` incorporado ao `/apps/my-app-packages/content/install` implanta conteúdo e configuração para o autor do AEM e para a publicação do AEM
   + O `ui.content.publish` incorporado no `/apps/my-app-packages/content/install.publish` implanta conteúdo e configuração somente para publicação do AEM

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-embeddeds) abaixo para obter um trecho completo.

### Definição de filtro do pacote de contêiner {#container-package-filter-definition}

Devido à incorporação dos subpacotes de código e conteúdo no pacote de contêiner, os caminhos de destino incorporados devem ser adicionados ao `filter.xml` do projeto do contêiner. Isso garante que os pacotes incorporados sejam incluídos no pacote de contêiner quando criados.

Basta adicionar as `<filter root="/apps/<my-app>-packages"/>` entradas para qualquer pasta de segundo nível que contenha subpacotes para implantar.

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-container-package-filters) abaixo para obter um trecho completo.

## Incorporação de pacotes de terceiros {#embedding-3rd-party-packages}

Todos os pacotes devem estar disponíveis por meio do [repositório público de artefatos Maven da Adobe](https://repo1.maven.org/maven2/com/adobe/) ou de um repositório de artefatos Maven de terceiros referenciável e público acessível.

Se os pacotes de terceiros estiverem no **repositório público de artefatos Maven da Adobe**, nenhuma configuração adicional será necessária para o Adobe Cloud Manager resolver os artefatos.

Se os pacotes de terceiros estiverem em um **repositório público de artefatos Maven de terceiros**, esse repositório deverá ser registrado no `pom.xml` do projeto e incorporado de acordo com o método [descrito acima](#embeddeds).

Aplicativo/conectores de terceiros devem ser incorporados usando seu pacote `all` como um contêiner no pacote do contêiner do projeto (`all`).

A adição de dependências do Maven segue as práticas padrão do Maven. A incorporação de artefatos de terceiros (pacotes de código e conteúdo) está [descrita acima](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-3rd-party-maven-repositories) abaixo para obter um trecho completo.

## Dependências de Pacote entre o `ui.apps` de `ui.content` Pacotes {#package-dependencies}

Para garantir a instalação adequada dos pacotes, é recomendável que as dependências entre pacotes sejam estabelecidas.

A regra geral é que os pacotes com conteúdo mutável (`ui.content`) devem depender do código imutável (`ui.apps`) que dá suporte à renderização e ao uso do conteúdo mutável.

Uma exceção notável a essa regra geral é se o pacote de código imutável (`ui.apps` ou qualquer outro), __somente__ contiver pacotes OSGi. Em caso afirmativo, nenhum pacote do AEM deve declarar uma dependência nele. O motivo é porque pacotes de código imutáveis que __only__ contêm pacotes OSGi não estão registrados no [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md) do AEM. Portanto, qualquer pacote do AEM que dependa dele tem uma dependência insatisfeita e não é instalado.

>[!TIP]
>
>Consulte a seção [Fragmentos XML de POM](#xml-package-dependencies) abaixo para obter um trecho completo.

Os padrões comuns para dependências de pacote de conteúdo são:

### Dependências do Pacote de Implantação Simples {#simple-deployment-package-dependencies}

O caso simples define o pacote de conteúdo mutável `ui.content` para depender do pacote de código imutável `ui.apps`.

+ `all` não tem dependências
   + `ui.apps` não tem dependências
   + `ui.content` depende de `ui.apps`

### Dependências complexas do pacote de implantação {#complex-deploxment-package-dependencies}

Implantações complexas se expandem no caso simples e definem dependências entre o conteúdo mutável correspondente e pacotes de código imutáveis. Conforme necessário, as dependências também podem ser estabelecidas entre pacotes de código imutáveis.

+ `all` não tem dependências
   + `common.ui.apps.common` não tem dependências
   + `site-a.ui.apps` depende de `common.ui.apps`
   + `site-a.ui.content` depende de `site-a.ui.apps`
   + `site-b.ui.apps` depende de `common.ui.apps`
   + `site-b.ui.content` depende de `site-b.ui.apps`

## Desenvolvimento e implantação local {#local-development-and-deployment}

As estruturas e a organização do projeto descritas neste artigo são **totalmente compatíveis** com as instâncias de desenvolvimento locais do AEM.

## Trechos XML POM {#pom-xml-snippets}

A seguir estão trechos de configuração do Maven `pom.xml` que podem ser adicionados aos projetos do Maven para se alinharem às recomendações acima.

### Tipos de encapsulamento {#xml-package-types}

Os pacotes de código e conteúdo, que são implantados como subpacotes, devem declarar um tipo de pacote de **aplicativo** ou **conteúdo**, dependendo do que eles contêm.

#### Tipos de pacote de contêiner {#container-package-types}

O contêiner `all/pom.xml` projeto **não** declara um `<packageType>`.

#### Tipos de pacote de código (imutável) {#immutable-package-types}

Os pacotes de código devem definir seu `packageType` como `application`.

No `ui.apps/pom.xml`, as diretivas de configuração de compilação `<packageType>application</packageType>` da declaração de plug-in `filevault-package-maven-plugin` declaram seu tipo de pacote.

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

#### Tipos de encapsulamento de conteúdo (mutável) {#mutable-package-types}

Os pacotes de conteúdo devem definir `packageType` como `content`.

No `ui.content/pom.xml`, a diretiva de configuração de compilação `<packageType>content</packageType>` da declaração de plug-in `filevault-package-maven-plugin` declara seu tipo de pacote.

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

### Marcação de pacotes para implantação do Adobe Cloud Manager {#cloud-manager-target}

Em todos os projetos que geram um pacote, **exceto** do projeto do contêiner (`all`), adicione `<cloudManagerTarget>none</cloudManagerTarget>` à configuração `<properties>` da declaração do plug-in `filevault-package-maven-plugin` para garantir que eles **não sejam** implantados pelo Adobe Cloud Manager. O pacote do contêiner (`all`) deve ser o único pacote implantado via Cloud Manager, que, por sua vez, incorpora todos os pacotes de código e conteúdo necessários.

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

### Inicialização do repositório{#snippet-repo-init}

Os scripts de Inicialização de repositório que contêm os scripts de Inicialização de repositório são definidos na configuração de fábrica OSGi `RepositoryInitializer` por meio da propriedade `scripts`. Como esses scripts são definidos nas configurações de OSGi, eles podem ser facilmente definidos pelo modo de execução usando a semântica de pasta `../config.<runmode>` usual.

Como os scripts geralmente são declarações de várias linhas, é mais fácil defini-los no arquivo `.config` do que no formato `.cfg.json` baseado em JSON.

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

A propriedade OSGi `scripts` contém diretivas conforme definidas pela [linguagem de inicialização de repositório do Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacote de estrutura do repositório {#xml-repository-structure-package}

No `ui.apps/pom.xml` e em qualquer outro `pom.xml` que declare um pacote de código (`<packageType>application</packageType>`), adicione a seguinte configuração de pacote de estrutura de repositório ao plug-in FileVault Maven. Você pode [criar seu próprio pacote de estrutura de repositório para o projeto](repository-structure-package.md).

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

### Incorporação de subpacotes no pacote de container {#xml-embeddeds}

Em `all/pom.xml`, adicione as seguintes diretivas `<embeddeds>` à declaração de plug-in `filevault-package-maven-plugin`. Lembre-se, **não** use a configuração `<subPackages>`. O motivo é porque inclui os subpacotes em `/etc/packages` em vez de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definição de filtro do pacote de contêiner {#xml-container-package-filters}

No `all` (`filter.xml`) do projeto `all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`, **inclua** qualquer pasta `-packages` que contenha subpacotes a serem implantados:

```xml
<filter root="/apps/my-app-packages"/>
```

Se vários `/apps/*-packages` forem usados nos destinos inseridos, todos eles deverão ser enumerados aqui.

### Repositórios Maven de terceiros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Adicionar mais repositórios Maven pode estender os tempos de compilação do Maven, à medida que repositórios Maven adicionais forem verificados em busca de dependências.

No `pom.xml` do projeto do reator, adicione quaisquer diretivas de repositório Maven públicas de terceiros necessárias. A configuração `<repository>` completa deve estar disponível no Provedor do Repositório de terceiros.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
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

### Dependências de Pacote entre o `ui.apps` de `ui.content` Pacotes {#xml-package-dependencies}

Em `ui.content/pom.xml`, adicione as seguintes diretivas `<dependencies>` à declaração de plug-in `filevault-package-maven-plugin`.

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

No `all/pom.xml`, adicione o plug-in `maven-clean-plugin`, que limpa o diretório de destino antes de uma compilação Maven.

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
+ [Plug-in Maven do Pacote de Conteúdo do FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
