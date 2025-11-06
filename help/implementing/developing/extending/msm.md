---
title: Extensão do gerenciador de vários sites
description: Saiba como estender a funcionalidade do Gerenciador de vários sites.
exl-id: 4b7a23c3-65d1-4784-9dea-32fcceca37d1
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2336'
ht-degree: 0%

---

# Extensão do gerenciador de vários sites {#extending-the-multi-site-manager}

Este documento ajuda você a entender como estender a funcionalidade do Gerenciador de vários sites e aborda os seguintes tópicos.

* Saiba mais sobre os principais membros da API Java do MSM
* Criar uma nova ação de sincronização que pode ser usada em uma configuração de implantação
* Modificar os códigos de idioma e país padrão

>[!TIP]
>
>Esta página é mais facilmente entendida no contexto do documento [Reutilização de Conteúdo: Gerenciador de Vários Sites](/help/sites-cloud/administering/msm/overview.md).

>[!CAUTION]
>
>O Gerenciador de vários sites e sua API são usados ao criar um site e, como tal, só devem ser usados em um ambiente de autor.

## Visão geral da API do Java {#overview-of-the-java-api}

O Gerenciamento de vários sites consiste nos seguintes pacotes:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

Os principais objetos da API do MSM interagem da seguinte maneira (consulte também a seção [Termos usados](/help/sites-cloud/administering/msm/overview.md#terms-used)):

![Principais objetos de API do MSM](assets/msm-api-interaction.png)

* **`Blueprint`** - Uma `Blueprint` (como em [configuração de blueprint](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)) especifica as páginas das quais uma live copy pode herdar conteúdo.

  ![Blueprint](assets/msm-blueprint-interaction.png)

   * O uso de uma configuração de blueprint ( `Blueprint`) é opcional, mas:

      * Ele permite que o autor use a opção **Implantação** na origem para enviar modificações explicitamente para as live copies que herdam desta origem.
      * Ele permite que o autor use o **Criar Site**, o que permite que o usuário selecione idiomas facilmente e configure a estrutura da live copy.
      * Ela define a configuração de implantação padrão para quaisquer live copies resultantes.

* **`LiveRelationship`** - `LiveRelationship` especifica a conexão (relação) entre um recurso na ramificação da live copy e seu recurso de origem/blueprint equivalente.

   * As relações são usadas ao realizar a herança e a implantação.
   * `LiveRelationship` objetos fornecem acesso (referências) às configurações de implantação ( `RolloutConfig`), `LiveCopy` e `LiveStatus` objetos relacionados à relação.

   * Por exemplo, uma live copy é criada em `/content/copy/us` da origem/blueprint em `/content/wknd/language-masters`. Os recursos `/content/wknd/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` formam uma relação.

* **`LiveCopy`** - Um `LiveCopy` contém os detalhes de configuração das relações (`LiveRelationship`) entre os recursos de live copy e seus recursos de origem/blueprint.

   * Use a classe `LiveCopy` para acessar o caminho da página, o caminho da página de origem/blueprint, as configurações de implantação e se as páginas filhas também estão incluídas em `LiveCopy`.

   * Um nó `LiveCopy` é criado sempre que **Criar Site** ou **Criar Live Copy** é usado.

* **`LiveStatus`** - `LiveStatus` objetos fornecem acesso ao status de tempo de execução de um `LiveRelationship`. Use para consultar o status de sincronização de uma live copy.

* **`LiveAction`** - `LiveAction` é uma ação executada em cada recurso envolvido na implantação.

   * `LiveAction`s são gerados apenas por `RolloutConfig`s.

* **`LiveActionFactory`** - Um `LiveActionFactory` cria objetos `LiveAction` a partir de uma configuração `LiveAction`. As configurações são armazenadas como recursos no repositório.

* **`RolloutConfig`** - O `RolloutConfig` contém uma lista de `LiveActions`, a ser usada quando acionada. `LiveCopy` herda `RolloutConfig` e o resultado está presente em `LiveRelationship`.

   * Configurar uma live copy pela primeira vez também usa um `RolloutConfig` (que aciona o `LiveAction`s).

## Criando uma Nova Ação de Sincronização {#creating-a-new-synchronization-action}

Você pode criar ações de sincronização personalizadas para usar com as configurações de implantação. Isso pode ser útil quando as [ações instaladas](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) não atenderem aos requisitos específicos do aplicativo.

Para fazer isso, crie duas classes:

* Uma implementação da interface [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) que executa a ação.
* Um componente OSGi que implementa a interface [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) e cria instâncias da classe `LiveAction`

O `LiveActionFactory` cria instâncias da classe `LiveAction` para uma determinada configuração:

* As classes `LiveAction` incluem os seguintes métodos:

   * `getName` - Retorna o nome da ação

      * O nome é usado para se referir à ação, por exemplo, em configurações de implantação.

   * `execute` - Executa as tarefas da ação

* `LiveActionFactory` classes incluem os seguintes membros:

   * `LIVE_ACTION_NAME` - Um campo que contém o nome do `LiveAction` associado

      * Este nome deve coincidir com o valor retornado pelo método `getName` da classe `LiveAction`.

   * `createAction` - Cria uma instância de `LiveAction`

      * O parâmetro `Resource` opcional pode ser usado para fornecer informações de configuração.

   * `createsAction` - Retorna o nome do `LiveAction` associado

### Acessando o nó de configuração do LiveAction {#accessing-the-liveaction-configuration-node}

Use o nó de configuração `LiveAction` no repositório para armazenar informações que afetam o comportamento do tempo de execução da instância `LiveAction`. O nó no repositório que armazena a configuração `LiveAction` está disponível para o objeto `LiveActionFactory` em tempo de execução. Portanto, você pode adicionar propriedades ao nó de configuração a e usá-las na implementação `LiveActionFactory`, conforme necessário.

Por exemplo, um `LiveAction` deve armazenar o nome do autor do blueprint. Uma propriedade do nó de configuração inclui o nome da propriedade da página do blueprint que armazena as informações. No tempo de execução, o `LiveAction` recupera o nome da propriedade da configuração e obtém o valor da propriedade.

O parâmetro do método [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) é um objeto `Resource`. Esse objeto `Resource` representa o nó `cq:LiveSyncAction` dessa ação ativa na configuração de implantação.

Consulte [Criando uma Configuração de Implantação](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) para obter mais informações.

Como de costume, ao usar um nó de configuração, você deve adaptá-lo a um objeto `ValueMap`:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Acesso aos nós do Target, nós do Source e LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Os seguintes objetos são fornecidos como parâmetros do método `execute` do objeto `LiveAction`:

* Um objeto [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) que representa a origem da live copy
* Um objeto `Resource` que representa o destino da live copy.
* O objeto [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) para a live copy
   * O valor `autoSave` indica se `LiveAction` deve salvar as alterações feitas no repositório
   * O valor `reset` indica o modo de redefinição de implantação.

A partir desses objetos, você pode obter informações sobre o `LiveCopy`. Você também pode usar os objetos `Resource` para obter objetos `ResourceResolver`, `Session` e `Node`. Esses objetos são úteis para manipular o conteúdo do repositório:

Na primeira linha do código a seguir, a origem é o objeto `Resource` da página de origem:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Os argumentos `Resource` podem ser objetos `null` ou `Resources` que não se adaptam a objetos `Node`, como objetos [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html).

## Criação de uma nova configuração de implantação {#creating-a-new-rollout-configuration}

Você pode criar uma configuração de implantação quando as configurações instaladas não atenderem aos requisitos do aplicativo seguindo duas etapas:

* [Criar a configuração de implantação](#create-the-rollout-configuration)
* [Adicionar ações de sincronização à configuração de implantação](#add-synchronization-actions-to-the-rollout-configuration)

A nova configuração de implantação está então disponível ao definir configurações de implantação em uma página de blueprint ou Live Copy.

>[!TIP]
>
>Consulte também as [práticas recomendadas para personalizar implantações](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### Criar a configuração de implantação {#create-the-rollout-configuration}

Para criar uma configuração de implantação:

1. Abra o CRXDE Lite em `https://<host>:<port>/crx/de`.

1. Navegue até `/apps/msm/<your-project>/rolloutconfigs`, a versão personalizada do seu projeto do `/libs/msm/wcm/rolloutconfigs`.

   * Se esta for sua primeira configuração, esta ramificação `/libs` deverá ser usada como modelo para criar a nova ramificação em `/apps`.

1. Nesse local, crie um nó com as seguintes propriedades:

   * **Nome**: o nome do nó da configuração de implantação, por exemplo, `contentCopy` ou `workflow`
   * **Tipo**: `cq:RolloutConfig`

1. Adicione as seguintes propriedades a este nó:

   * **Nome**: `jcr:title`
     **Tipo**: `String`
     **Valor**: um título de identificação que aparecerá na interface

   * **Nome**: `jcr:description`
     **Tipo**: `String`
     **Valor**: uma descrição opcional.

   * **Nome**: `cq:trigger`
     **Tipo**: `String`
     **Valor**: o [Gatilho de Implantação](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) a ser usado
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Clique em **Salvar tudo**.

### Adicionar ações de sincronização à configuração de implantação {#add-synchronization-actions-to-the-rollout-configuration}

As configurações de implantação são armazenadas abaixo do [nó de configuração de implantação](#create-the-rollout-configuration) criado no nó `/apps/msm/<your-project>/rolloutconfigs`.

Adicione nós filhos do tipo `cq:LiveSyncAction` para adicionar ações de sincronização à configuração de implantação. A ordem dos nós de ação de sincronização determina a ordem em que as ações ocorrem.

1. No CRXDE Lite, selecione o nó [Configuração de implantação](#create-the-rollout-configuration), por exemplo, `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. Crie um nó com as seguintes propriedades de nó:

   * **Nome**: o nome do nó da ação de sincronização
      * O nome deve ser igual ao **Nome da Ação** na tabela em [Ações de Sincronização](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions), como `contentCopy` ou `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Adicione e configure quantos nós de ação de sincronização forem necessários.

1. Reorganize os nós de ação para que sua ordem corresponda à ordem em que você deseja que eles ocorram.
   * O nó de ação mais acima ocorre primeiro.

## Criação e uso de uma classe simples do LiveActionFactory {#creating-and-using-a-simple-liveactionfactory-class}

Siga os procedimentos desta seção para desenvolver um `LiveActionFactory` e usá-lo em uma configuração de implantação. Os procedimentos usam o Maven e o Eclipse para desenvolver e implantar o `LiveActionFactory`:

1. [Crie o projeto maven](#create-the-maven-project) e importe-o para o Eclipse.
1. [Adicionar dependências](#add-dependencies-to-the-pom-file) ao arquivo POM.
1. [Implemente a `LiveActionFactory` interface](#implement-liveactionfactory) e implante o pacote OSGi.
1. [Criar a configuração de implantação](#create-the-example-rollout-configuration).
1. [Criar a live copy](#create-the-live-copy).

[O projeto Maven e o código-fonte da classe Java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) estão disponíveis no repositório Git público.

### Criar o projeto Maven {#create-the-maven-project}

O procedimento a seguir requer que você tenha adicionado o perfil do `adobe-public` ao seu arquivo de configurações Maven.

* Para obter informações sobre o perfil adobe-public, consulte [Obtendo o plug-in Maven do pacote de conteúdo](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* Para obter informações sobre o arquivo de configurações Maven, consulte a [Referência de configurações](https://maven.apache.org/settings.html) do Maven.

1. Abra um terminal ou uma sessão de linha de comando e altere o diretório para apontar para o local onde criar o projeto.
1. Digite o seguinte comando:

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Especifique os seguintes valores no prompt interativo:

   * **`groupId`**: `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. Iniciar o Eclipse e [importar o projeto Maven](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse).

### Adicionar dependências ao arquivo POM {#add-dependencies-to-the-pom-file}

Adicione dependências para que o compilador Eclipse possa referenciar as classes usadas no código `LiveActionFactory`.

1. No Eclipse Project Explorer, abra o arquivo `MyLiveActionFactory/pom.xml`.

1. No editor, clique na guia `pom.xml` e localize a seção `project/dependencyManagement/dependencies`.

1. Adicione o seguinte XML dentro do elemento `dependencyManagement` e salve o arquivo.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Abra o arquivo POM para o pacote do **Project Explorer** em `MyLiveActionFactory-bundle/pom.xml`.

1. No editor, clique na guia `pom.xml` e localize a seção projeto/dependências. Adicione o seguinte XML dentro do elemento dependencies e salve o arquivo:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementar o LiveActionFactory {#implement-liveactionfactory}

A seguinte classe `LiveActionFactory` implementa um `LiveAction` que registra mensagens sobre as páginas de origem e destino e copia a propriedade `cq:lastModifiedBy` do nó de origem para o nó de destino. O nome da ação dinâmica é `exampleLiveAction`.

1. No Eclipse Project Explorer, clique com o botão direito do mouse no pacote `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` e clique em **Novo** > **Classe**.

1. Para o **Nome**, digite `ExampleLiveActionFactory` e clique em **Concluir**.

1. Abra o arquivo `ExampleLiveActionFactory.java`, substitua o conteúdo pelo seguinte código e salve o arquivo.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Usando o terminal ou a sessão de comando, altere o diretório para o diretório `MyLiveActionFactory` (o diretório do projeto Maven). Em seguida, insira o seguinte comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. O arquivo `error.log` do AEM deve indicar que o pacote foi iniciado, visível nos logs em `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Criar o exemplo de configuração de implantação {#create-the-example-rollout-configuration}

Crie a configuração de implantação do MSM que usa o `LiveActionFactory` que você criou:

1. Crie e configure uma [Configuração de implantação com o procedimento padrão](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) usando as propriedades:

   * **Título**: Exemplo de Configuração de Implantação
   * **Nome**: examplerolloutconfig
   * **cq:trigger**: `publish`

### Adicione a ação ativa à configuração de implantação de exemplo {#add-the-live-action-to-the-example-rollout-configuration}

Configure a configuração de implantação criada no procedimento anterior para que ela use a classe `ExampleLiveActionFactory`.

1. Abra o CRXDE Lite.

1. Criar o seguinte nó em `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Clique em **Salvar tudo**.

1. Selecione o nó `exampleLiveAction` e adicione uma propriedade para indicar à classe `ExampleLiveAction` que a propriedade `cq:LastModifiedBy` deve ser replicada do nó de origem para o nó de destino.

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

1. Clique em **Salvar tudo**.

### Criar a Live Copy {#create-the-live-copy}

[Crie uma Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) da ramificação em inglês/produtos do site de referência WKND usando sua configuração de implantação:

* **Source**: `/content/wknd/language-masters/en/products`

* **Configuração de Implantação**: Exemplo de Configuração de Implantação

Ative a página **Produtos** (inglês) da ramificação de origem e observe as mensagens de log geradas pela classe `LiveAction`:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## Alterando Nomes de Idiomas e Países Default {#changing-language-names-and-default-countries}

O AEM usa um conjunto padrão de códigos de idioma e país.

* O código de idioma padrão é o código de duas letras em minúsculas, conforme definido pela ISO-639-1.
* O código de país padrão é o código de duas letras em minúsculas ou maiúsculas, conforme definido pela norma ISO 3166.

O MSM usa uma lista armazenada de códigos de idioma e de país para determinar o nome do país associado ao nome da versão do idioma da sua página. Você pode alterar os seguintes aspectos da lista, se necessário:

* Títulos de idioma
* Nomes dos países
* Países padrão para idiomas (para códigos como `en`, `de`, entre outros)

A lista de idiomas é armazenada abaixo do nó `/libs/wcm/core/resources/languages`. Cada nó secundário representa um idioma ou um país de idioma:

* O nome do nó é o código de idioma (como `en` ou `de`) ou o código language_country (como `en_us` ou `de_ch`).

* A propriedade `language` do nó armazena o nome completo do idioma do código.
* A propriedade `country` do nó armazena o nome completo do país do código.
* Quando o nome do nó consiste apenas em um código de idioma (como `en`), a propriedade country é `*`, e uma propriedade `defaultCountry` adicional armazena o código do idioma-país para indicar o país a ser usado.

![Definição de idioma](assets/msm-language-manager.png)

Para modificar os idiomas:

1. Abra o CRXDE Lite.
1. Selecione a pasta `/apps` e clique em **Criar** e depois em **Criar Pasta.**

1. Nomeie a nova pasta `wcm`.

1. Repita a etapa anterior para criar a árvore de pastas `/apps/wcm/core`. Crie um nó do tipo `sling:Folder` em `core` chamado `resources`.

1. Clique com o botão direito no nó `/libs/wcm/core/resources/languages` e clique em **Copiar**.
1. Clique com o botão direito na pasta `/apps/wcm/core/resources` e clique em **Colar**. Modifique os nós filhos conforme necessário.
1. Clique em **Salvar tudo**.
1. Clique em **Ferramentas**, **Operações** e depois em **Console da Web**. Neste console, clique em **OSGi** e depois em **Configuração**.
1. Localize e clique em **Gerenciador de Idiomas do WCM do Day CQ**, altere o valor de **Lista de Idiomas** para `/apps/wcm/core/resources/languages` e clique em **Salvar**.

   ![Gerenciador de Idiomas WCM CQ do Dia](assets/msm-language-manager.png)

## Configuração de bloqueios do MSM nas propriedades da página {#configuring-msm-locks-on-page-properties}

Ao criar uma propriedade de página personalizada, talvez seja necessário considerar se a nova propriedade deve ser qualificada para implantação em qualquer live copy.

Por exemplo, se duas novas propriedades de página estiverem sendo adicionadas:

* E-mail de contato:

   * Não é necessário implantar esta propriedade, pois ela será diferente em cada país (ou marca e assim por diante).

* Estilo visual da chave:

   * O requisito do projeto é que essa propriedade seja implementada, pois é (geralmente) comum a todos os países (ou marcas e assim por diante).

Em seguida, é necessário garantir que:

* E-mail de contato:

   * É excluído das propriedades implantadas.
   * Consulte [Configurando a sincronização da Live Copy](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) para obter mais informações.

* Estilo visual da chave:

   * Certifique-se de que você não tem permissão para editar essa propriedade, a menos que a herança seja cancelada.
   * Além disso, certifique-se de que você possa restaurar a herança. Isso é controlado clicando nos links de cadeia/cadeia interrompida que alternam para indicar o status da conexão.

Se uma propriedade de página está sujeita à implantação e, portanto, sujeita ao cancelamento/restabelecimento da herança ao editar, é controlada pela propriedade de diálogo:

* `cq-msm-lockable`

   * Isso criará o símbolo de vínculo em cadeia na caixa de diálogo.
   * Isso só permitirá a edição se a herança for cancelada (o vínculo em cadeia é interrompido).
   * Isso se aplica somente ao primeiro nível secundário do recurso
      * **Tipo**: `String`
      * **Valor**: mantém o nome da propriedade em consideração e é comparável ao valor da propriedade `name`
         * Por exemplo, consulte
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Quando `cq-msm-lockable` for definido, quebrar/fechar a cadeia interagirá com o MSM da seguinte maneira:

* Se o valor de `cq-msm-lockable` for:

   * **Relativo** (por exemplo, `myProperty` ou `./myProperty`)

      * Quebrar a cadeia adicionará e removerá a propriedade de `cq:propertyInheritanceCancelled`.

   * **Absoluto** (por exemplo, `/image`)

      * Quebrar a cadeia cancelará a herança adicionando o mixin `cq:LiveSyncCancelled` a `./image` e definindo `cq:isCancelledForChildren` como `true`.

      * Fechar a cadeia reverterá a herança.

>[!NOTE]
>
>`cq-msm-lockable` se aplica ao primeiro nível filho do recurso a ser editado e não é funcional em nenhum ancestral de nível mais profundo, independentemente se o valor for definido como absoluto ou relativo.

>[!NOTE]
>
>Quando você reativa a herança, a propriedade da página de live copy não é sincronizada automaticamente com a propriedade de origem. Você pode solicitar manualmente uma sincronização, se necessário.
