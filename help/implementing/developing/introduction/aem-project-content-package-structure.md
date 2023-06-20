---
title: Estrutura de projetos do AEM
description: Saiba mais sobre como definir estruturas de pacote para implantação no Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2927'
ht-degree: 12%

---

# Estrutura de projetos do AEM

>[!TIP]
>
>Familiarize-se com as [Uso do Arquétipo de Projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), e o [Plug-in FileVault Content Maven](/help/implementing/developing/tools/maven-plugin.md) conforme este artigo se baseia nesses aprendizados e conceitos.

Este artigo descreve as alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM as a Cloud Service, garantindo que eles respeitem a divisão de conteúdo mutável e imutável, que as dependências sejam estabelecidas para criar implantações determinísticas e não conflitantes e que sejam compactadas em uma estrutura implantável.

As implantações de aplicativos de AEM devem ser compostas por um único pacote de AEM. Este pacote deve, por sua vez, conter pacotes secundários que incluem tudo o que o aplicativo exige para funcionar, incluindo código, configuração e qualquer conteúdo de linha de base de suporte.

O AEM exige uma separação de **conteúdo** e **código**, que significa um único pacote de conteúdo **não é possível** implantar em **ambos** `/apps` e áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home`, ou qualquer coisa que não `/apps`) do repositório. Em vez disso, o aplicativo deve separar código e conteúdo em pacotes separados para implantação no AEM.

A estrutura do pacote descrita neste documento é compatível com **ambas** as implantações de desenvolvimento locais e implantações do serviço da AEM Cloud.

>[!TIP]
>
>As configurações descritas neste documento são fornecidas por [Arquétipo Maven do projeto AEM 24 ou posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutáveis versus imutáveis do repositório {#mutable-vs-immutable}

`/apps` e `/libs`**são consideradas áreas imutáveis do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução).** Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

Todo o restante no repositório, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. são todos **mutável** áreas, o que significa que elas podem ser alteradas no tempo de execução.

>[!WARNING]
>
>Como em versões anteriores do AEM, `/libs` não deve ser modificado. Somente o código de produto AEM pode ser implantado em `/libs`.

### Índices Oak {#oak-indexes}

Índices Oak (`/oak:index`) são gerenciados especificamente pelo processo de implantação as a Cloud Service do AEM. Isso ocorre porque o Cloud Manager deve aguardar até que qualquer novo índice seja implantado e totalmente reindexado antes de alternar para a nova imagem de código.

Por esse motivo, embora os índices Oak sejam mutáveis em tempo de execução, eles devem ser implantados como código para que possam ser instalados antes que qualquer pacote mutável seja instalado. Portanto `/oak:index` as configurações fazem parte do Pacote de código e não do Pacote de conteúdo [conforme descrito abaixo](#recommended-package-structure).

>[!TIP]
>
>Para obter mais detalhes sobre a indexação no AEM as a Cloud Service, consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

## Estrutura de pacotes recomendada {#recommended-package-structure}

![Estrutura do pacote de projetos do Experience Manager](assets/content-package-organization.png)

Este diagrama fornece uma visão geral da estrutura de projeto recomendada e dos artefatos de implantação de pacote.

A estrutura de implantação de aplicativo recomendada é a seguinte:

### Pacotes de código / pacotes OSGi

+ O arquivo Jar do pacote OSGi é gerado e incorporado diretamente em todo o projeto.

+ A variável `ui.apps` contém todo o código a ser implantado e implanta somente em `/apps`. Elementos comuns da `ui.apps` incluem, mas não estão limitados a:
   + [Definições de componentes e HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=pt-BR) scripts
      + `/apps/my-app/components`
   + JavaScript e CSS (via [Bibliotecas de clientes](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Sobreposições](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurações sensíveis ao contexto de fallback
      + `/apps/settings`
   + ACLs (permissões)
      + Qualquer `rep:policy` para qualquer caminho em `/apps`
   + [Scripts agrupados pré-compilados](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>O mesmo código deve ser implantado em todos os ambientes. Esse código é necessário para garantir que validações de nível de confiança no ambiente de preparo também estejam em produção. Para obter mais informações, consulte a seção sobre [Runmodes](/help/implementing/deploying/overview.md#runmodes).


### Pacotes de conteúdo

+ A variável `ui.content` o pacote contém todo o conteúdo e configuração. O pacote de conteúdo contém todas as definições de nó que não estão no `ui.apps` ou `ui.config` pacotes ou, em outras palavras, qualquer coisa que não esteja em `/apps` ou `/oak:index`. Elementos comuns da `ui.content` incluem, mas não estão limitados a:
   + Configurações sensíveis ao contexto
      + `/conf`
   + Estruturas de conteúdo complexas obrigatórias (por exemplo, A criação de conteúdo que se baseia em e estende estruturas de conteúdo de linha de base anteriores definidas na Inicialização do repositório).
      + `/content`, `/content/dam`, etc.
   + Taxonomias de marcação controladas
      + `/content/cq:tags`
   + Nós etc herdados (idealmente, migre-os para locais que não sejam ou etc)
      + `/etc`

### Pacotes de contêineres

+ A variável `all` é um pacote de contêiner que APENAS inclui artefatos implantáveis, o arquivo Jar do pacote OSGI, `ui.apps`, `ui.config` e `ui.content` pacotes como incorporados. A variável `all` o pacote não deve ter **qualquer conteúdo ou código** por conta própria, mas delegue toda a implantação no repositório em seus pacotes secundários ou arquivos Jar do pacote OSGi.

  Agora os pacotes são incluídos usando o Maven [Configuração incorporada do plug-in FileVault Package Maven](#embeddeds), em vez de `<subPackages>` configuração.

  Para implantações complexas de Experience Manager, pode ser desejável criar vários `ui.apps`, `ui.config` e `ui.content` projetos/pacotes que representam sites ou locatários específicos no AEM. Se isso for feito, certifique-se de que a divisão entre conteúdo mutável e imutável seja respeitada e que os pacotes de conteúdo necessários e os arquivos Jar do pacote OSGi sejam incorporados como pacotes secundários na `all` pacote de conteúdo do container.

  Por exemplo, uma estrutura complexa de pacote de conteúdo de implantação pode ter esta aparência:

   + `all` o pacote de conteúdo incorpora os seguintes pacotes, para criar um artefato de implantação singular
      + `common.ui.apps` implanta o código exigido por **ambos** site A e site B
      + `site-a.core` Jar do pacote OSGi exigido pelo site A
      + `site-a.ui.apps` implanta o código exigido pelo site A
      + `site-a.ui.config` implanta as configurações de OSGi exigidas pelo Site A
      + `site-a.ui.content` implanta o conteúdo e a configuração exigidos pelo site A
      + `site-b.core` Jar do pacote OSGi necessário para o site B
      + `site-b.ui.apps` implanta o código exigido pelo site B
      + `site-b.ui.config` implanta as configurações de OSGi exigidas pelo site B
      + `site-b.ui.content` implanta o conteúdo e a configuração exigidos pelo site B

+ A variável `ui.config` o pacote contém tudo [Configurações do OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Código considerado e pertence a pacotes OSGi, mas não contém nós de conteúdo regulares. Assim, ele é marcado como um pacote de contêiner
   + Pasta organizacional contendo definições de configuração OSGi específicas do modo de execução
      + `/apps/my-app/osgiconfig`
   + Pasta de configuração OSGi comum contendo configurações OSGi padrão que se aplicam a todos os destinos de implantação do AEM de destino as a Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Executar pastas de configuração OSGi específicas do modo que contenham configurações OSGi padrão aplicáveis a todos os destinos de implantação as a Cloud Service do AEM
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Scripts de configuração do OSGi de inicialização do repositório
      + [Inicialização do repositório](#repo-init) é a maneira recomendada de implantar conteúdo (mutável) que logicamente faz parte do aplicativo AEM. As configurações do OSGi de inicialização do repositório devem estar no local `config.<runmode>` como descrito acima, e ser utilizado para definir:
         + Estruturas de conteúdo de linha de base
         + Usuários
         + Usuários de serviço
         + Grupos
         + ACLs (permissões)

### Pacotes de Aplicativos Adicionais{#extra-application-packages}

Se outros projetos de AEM, eles mesmos compostos de seu próprio código e pacotes de conteúdo, forem usados pela implantação do AEM, seus pacotes de contêiner deverão ser incorporados no `all` pacote.

Por exemplo, um projeto AEM que inclui aplicativos AEM de dois fornecedores pode se parecer com:

+ `all` o pacote de conteúdo incorpora os seguintes pacotes, para criar um artefato de implantação singular
   + `core` Jar do pacote OSGi necessário para o aplicativo AEM
   + `ui.apps` implanta o código exigido pelo aplicativo AEM
   + `ui.config` implanta as configurações de OSGi exigidas pelo aplicativo AEM
   + `ui.content` implanta o conteúdo e a configuração exigidos pelo aplicativo AEM
   + `vendor-x.all` implanta tudo (código e conteúdo) exigido pelo aplicativo do fornecedor X
   + `vendor-y.all` implanta tudo (código e conteúdo) exigido pelo aplicativo Y do fornecedor

## Tipos de encapsulamento {#package-types}

Os pacotes devem ser marcados com o tipo de pacote declarado. Os tipos de pacote ajudam a esclarecer a finalidade e a implantação de um pacote.

+ Os pacotes de contêineres devem definir seus `packageType` para `container`. Os pacotes de contêineres não devem conter nós regulares. Somente pacotes OSGi, configurações e pacotes secundários são permitidos. Os contêineres no AEM as a Cloud Service não podem usar [instalar ganchos](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Os pacotes de código (imutáveis) devem definir seus `packageType` para `application`.
+ Os pacotes de conteúdo (mutáveis) devem definir seus `packageType` para `content`.


Para obter mais informações, consulte [Apache Jackrabbit FileVault - documentação do plug-in Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipos de pacote do Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html), e o [Trecho de configuração do FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) abaixo.

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-package-types) abaixo para obter um trecho completo.

## Marcação de pacotes para implantação pelo Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Por padrão, o Adobe Cloud Manager coleta todos os pacotes produzidos pela compilação Maven. No entanto, como o pacote do contêiner (`all`) é o artefato de implantação singular que contém todos os pacotes de código e conteúdo, devemos garantir que **somente** o pacote do contêiner (`all`) seja implantado. Para garantir isso, outros pacotes gerados pela compilação Maven devem ser marcados com a configuração do Plug-in FileVault Content Package Maven do `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte a [Trechos XML POM](#pom-xml-snippets) abaixo para obter um trecho completo.

## Inicialização do repositório{#repo-init}

A Inicialização do repositório fornece instruções, ou scripts, que definem estruturas JCR, desde estruturas de nó comuns, como árvores de pastas, até usuários, usuários de serviço, grupos e definição de ACL.

Os principais benefícios da Inicialização do repositório são: eles têm permissões implícitas para executar todas as ações definidas por seus scripts e são chamados antecipadamente no ciclo de vida da implantação, garantindo que todas as estruturas JCR necessárias existam até o momento em que o código é executado.

Enquanto os scripts de inicialização do repositório vivem no `ui.config` projeto como scripts, eles podem e devem ser usados para definir as seguintes estruturas mutáveis:

+ Estruturas de conteúdo de linha de base
+ Usuários de serviço
+ Usuários
+ Grupos
+ ACLs

Os scripts de inicialização do repositório são armazenados como `scripts` entradas de `RepositoryInitializer` As configurações de fábrica do OSGi e, portanto, podem ser direcionadas implicitamente pelo modo de execução, permitindo diferenças entre o Autor do AEM e os scripts de inicialização de repositório do AEM Publish Services ou até mesmo entre ambientes (Desenvolvimento, Preparo e Produção).

As configurações de OSGi de inicialização de repositório são melhor gravadas no [`.config` Formato de configuração do OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) como suportam múltiplas linhas, o que constitui uma exceção às melhores práticas [`.cfg.json` para definir configurações de OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Observe que ao definir Usuários e Grupos, somente os grupos são considerados parte do aplicativo, e parte integrante de sua função deve ser definida aqui. Usuários e grupos da organização ainda devem ser definidos no tempo de execução no AEM; por exemplo, se um fluxo de trabalho personalizado atribuir trabalho a um grupo nomeado, esse grupo deve ser definido por meio da Inicialização do repositório no aplicativo AEM, no entanto, se o Agrupamento for meramente organizacional, como &quot;Equipe da Wendy&quot; e &quot;Equipe de Sean&quot;, eles são melhor definidos e gerenciados no tempo de execução no AEM.

>[!TIP]
>
>Scripts de inicialização do repositório *deve* ser definido na linha `scripts` e a variável `references` A configuração do não funcionará.

O vocabulário completo para scripts de inicialização de repositório está disponível no [Documentação de inicialização do Apache Sling Repo](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte a [Trechos de inicialização do repositório](#snippet-repo-init) abaixo para obter um trecho completo.

## Pacote de estrutura do repositório {#repository-structure-package}

Os pacotes de código exigem a configuração do plug-in FileVault Maven para fazer referência a uma `<repositoryStructurePackage>` que impõe a correção de dependências estruturais (para garantir que um pacote de códigos não seja instalado sobre outro). Você pode [criar seu próprio pacote de estrutura de repositório para o projeto](repository-structure-package.md).

Isso **só é necessário** em Pacotes de código, ou seja, qualquer pacote marcado com `<packageType>application</packageType>`.

Para saber como criar um pacote de estrutura do repositório para seu aplicativo, consulte [Desenvolver um pacote de estrutura do repositório](repository-structure-package.md).

Observe que os pacotes de conteúdo (`<packageType>content</packageType>`) **não** exigir este pacote de estrutura do repositório.

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-repository-structure-package) abaixo para obter um trecho completo.

## Incorporação de subpacotes no pacote de contêiner{#embeddeds}

O conteúdo ou os pacotes de código são colocados em uma pasta especial &quot;lateral&quot; e podem ser direcionados para instalação no autor do AEM, na publicação do AEM ou em ambos, usando o plug-in FileVault Maven `<embeddeds>` configuração. Observe que `<subPackages>` não deve ser usada.

Casos de uso comuns incluem:

+ ACLs/permissões que diferem entre usuários de autor de AEM e usuários de publicação de AEM
+ Configurações usadas para dar suporte a atividades somente em autor de AEM
+ Código, como integrações com sistemas de back-office, necessário apenas para execução em autor de AEM

![Incorporação de pacotes](assets/embeddeds.png)

Para direcionar o autor do AEM, a publicação do AEM ou ambos, o pacote é incorporado na `all` pacote de contêiner em um local de pasta especial, no seguinte formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Detalhar esta estrutura de pasta:

+ A pasta de primeiro nível **deve ser** `/apps`.
+ A pasta de segundo nível representa o aplicativo com `-packages` pós-corrigido para o nome da pasta. Geralmente, há apenas uma única pasta de segundo nível em que todos os pacotes secundários são incorporados. No entanto, qualquer número de pastas de segundo nível pode ser criada para melhor representar a estrutura lógica do aplicativo:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >Por convenção, as pastas incorporadas do pacote secundário são nomeadas com o sufixo `-packages`. Isso garante que o código de implantação e os pacotes de conteúdo **não** sejam implantados nas pastas de destino de qualquer pacote secundário `/apps/<app-name>/...` que resulte em comportamento de instalação destrutivo e cíclico.

+ A pasta de terceiro nível deve ser
  `application`, `content` ou `container`
   + A variável `application` a pasta contém pacotes de código
   + A variável `content` a pasta retém pacotes de conteúdo
   + A variável `container` a pasta contém qualquer [pacotes de aplicativos extras](#extra-application-packages) que pode ser incluído pelo aplicativo AEM.
Este nome de pasta corresponde ao [tipos de encapsulamento](#package-types) dos pacotes que contém.
+ A pasta de 4º nível contém os pacotes secundários e deve ser uma das seguintes:
   + `install` para instalar no autor do AEM **e** na publicação do AEM
   + `install.author` para instalar **somente** no autor do AEM
   + `install.publish` para **somente** instalar na publicação do AEM Observe que somente `install.author` e `install.publish` são alvos compatíveis. Outros modos de execução **não são** compatíveis.

Por exemplo, uma implantação que contém pacotes específicos do autor e da publicação do AEM pode ser semelhante ao seguinte:

+ `all` O pacote de contêiner incorpora os seguintes pacotes, para criar um artefato de implantação singular
   + `ui.apps` incorporado em `/apps/my-app-packages/application/install` implanta o código para o autor do AEM e para a publicação do AEM
   + `ui.apps.author` incorporado em `/apps/my-app-packages/application/install.author` implanta o código somente no autor do AEM
   + `ui.content` incorporado em `/apps/my-app-packages/content/install` implanta conteúdo e configuração para o autor do AEM e para a publicação do AEM
   + `ui.content.publish` incorporado em `/apps/my-app-packages/content/install.publish` implanta conteúdo e configuração somente para publicação no AEM

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-embeddeds) abaixo para obter um trecho completo.

### Definição de filtro do pacote de contêiner {#container-package-filter-definition}

Devido à incorporação dos pacotes secundários de código e conteúdo no pacote do contêiner, os caminhos de destino incorporados devem ser adicionados aos do projeto do contêiner `filter.xml` para garantir que os pacotes incorporados sejam incluídos no pacote do contêiner quando criados.

Basta adicionar o `<filter root="/apps/<my-app>-packages"/>` entradas para qualquer pasta de segundo nível que contenha pacotes secundários a serem implantados.

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-container-package-filters) abaixo para obter um trecho completo.

## Incorporação de pacotes de terceiros {#embedding-3rd-party-packages}

Todos os pacotes devem estar disponíveis por meio da [Repositório de artefatos Maven público do Adobe](https://repo1.maven.org/maven2/com/adobe/) ou um repositório de artefatos Maven de terceiros referenciável e público acessível.

Se os pacotes de terceiros estiverem no **repositório público de artefatos Maven da Adobe**, nenhuma configuração adicional será necessária para o Adobe Cloud Manager resolver os artefatos.

Se os pacotes de terceiros estiverem em um **repositório de artefatos Maven de terceiros público**, esse repositório deverá ser registrado no `pom.xml` do projeto e incorporado de acordo com o método [descrito acima](#embeddeds).

O aplicativo/conectores de terceiros devem ser incorporados usando sua `all` pacote como um contêiner no contêiner do projeto (`all`).

A adição de dependências do Maven segue as práticas padrão do Maven e a incorporação de artefatos de terceiros (pacotes de código e conteúdo) é [descrito acima](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-3rd-party-maven-repositories) abaixo para obter um trecho completo.

## Dependências de pacote entre o `ui.apps` de `ui.content` Pacotes {#package-dependencies}

Para garantir a instalação adequada dos pacotes, é recomendável que as dependências entre pacotes sejam estabelecidas.

A regra geral é pacotes com conteúdo mutável (`ui.content`) deve depender do código imutável (`ui.apps`) que suporta a renderização e uso do conteúdo mutável.

Uma exceção notável a essa regra geral é se o pacote de código imutável (`ui.apps` ou qualquer outro), __somente__ contém pacotes OSGi. Em caso afirmativo, nenhum pacote AEM deve declarar uma dependência dele. Isso ocorre porque pacotes de código imutáveis __somente__ contendo pacotes OSGi não estão registrados com AEM [Gerenciador de pacotes,](/help/implementing/developing/tools/package-manager.md) e, portanto, qualquer pacote AEM que dependa dele terá uma dependência insatisfeita e não será instalado.

>[!TIP]
>
>Consulte a [Trechos XML POM](#xml-package-dependencies) abaixo para obter um trecho completo.

Os padrões comuns para dependências de pacote de conteúdo são:

### Dependências do Pacote de Implantação Simples {#simple-deployment-package-dependencies}

O caso simples define o `ui.content` pacote de conteúdo mutável para depender do `ui.apps` pacote de código imutável.

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

As estruturas e a organização do projeto descritas neste artigo são **totalmente compatível** instâncias de desenvolvimento local do AEM.

## Trechos XML POM {#pom-xml-snippets}

Veja a seguir o Maven `pom.xml` trechos de configuração que podem ser adicionados aos projetos Maven para se alinharem às recomendações acima.

### Tipos de encapsulamento {#xml-package-types}

Os pacotes de código e conteúdo, que são implantados como pacotes secundários, devem declarar um tipo de pacote de **aplicativo** ou **conteúdo**, dependendo do que eles contêm.

#### Tipos de pacote de contêiner {#container-package-types}

O container `all/pom.xml` projeto **não** declarar um `<packageType>`.

#### Tipos de pacote de código (imutável) {#immutable-package-types}

Os pacotes de código devem definir seus `packageType` para `application`.

No `ui.apps/pom.xml`, o `<packageType>application</packageType>` criar diretivas de configuração do `filevault-package-maven-plugin` declaração de plug-in declara seu tipo de pacote.

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

Os pacotes de conteúdo devem definir seus `packageType` para `content`.

No `ui.content/pom.xml`, o `<packageType>content</packageType>` diretiva de configuração de build do `filevault-package-maven-plugin` declaração de plug-in declara seu tipo de pacote.

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

Em todos os projetos que geram um pacote, **exceto** do projeto do contêiner (`all`), adicione `<cloudManagerTarget>none</cloudManagerTarget>` à configuração `<properties>` da declaração do plug-in `filevault-package-maven-plugin` para garantir que eles **não sejam** implantados pelo Adobe Cloud Manager. O container (`all`) deve ser o único pacote implantado pelo Cloud Manager, que, por sua vez, incorpora todos os pacotes de código e conteúdo necessários.

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

Os scripts de Inicialização de repositório que contêm os scripts de Inicialização de repositório são definidos no `RepositoryInitializer` Configuração de fábrica do OSGi por meio do `scripts` propriedade. Observe que, como esses scripts são definidos nas configurações de OSGi, eles podem ser facilmente definidos pelo modo de execução usando o `../config.<runmode>` semântica da pasta.

Observe que, como os scripts normalmente são declarações de várias linhas, é mais fácil defini-los na variável `.config` do que o arquivo baseado em JSON `.cfg.json` formato.

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

A variável `scripts` A propriedade OSGi contém diretivas conforme definidas pelo [Idioma de inicialização do repositório do Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacote de estrutura do repositório {#xml-repository-structure-package}

No `ui.apps/pom.xml` e qualquer outro `pom.xml` que declara um pacote de código (`<packageType>application</packageType>`), adicione a seguinte configuração de pacote de estrutura de repositório ao plug-in FileVault Maven. Você pode [criar seu próprio pacote de estrutura de repositório para o projeto](repository-structure-package.md).

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

No `all/pom.xml`, adicione o seguinte `<embeddeds>` diretivas para a `filevault-package-maven-plugin` declaração do plug-in. Lembre-se: **não** use o `<subPackages>` configuração, pois incluirá os pacotes secundários em `/etc/packages` em vez de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

No `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) do projeto `all`, **inclua** as pastas `-packages` que contêm pacotes secundários a serem implantados:

```xml
<filter root="/apps/my-app-packages"/>
```

Se vários `/apps/*-packages` são usados nos destinos incorporados, todos eles devem ser enumerados aqui.

### Repositórios Maven de terceiros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Adicionar mais repositórios Maven pode estender os tempos de compilação do Maven, à medida que repositórios Maven adicionais forem verificados em busca de dependências.

No projeto do reator `pom.xml`, adicione as diretivas de repositório Maven públicas de terceiros necessárias. O conjunto `<repository>` A configuração do deve estar disponível no provedor de repositório de terceiros.

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

### Dependências de pacote entre o `ui.apps` de `ui.content` Pacotes {#xml-package-dependencies}

No `ui.content/pom.xml`, adicione o seguinte `<dependencies>` diretivas para a `filevault-package-maven-plugin` declaração do plug-in.

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

No `all/pom.xml` adicione o `maven-clean-plugin` plug-in que limpará o diretório de destino antes de uma compilação Maven.

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
+ [Plug-in FileVault Content Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
