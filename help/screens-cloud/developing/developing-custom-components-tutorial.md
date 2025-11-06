---
title: Desenvolvimento de um componente personalizado para o Screens as a Cloud Service
description: O tutorial a seguir percorre as etapas para criar um componente personalizado para o AEM Screens. A AEM Screens reutiliza muitos padrões e tecnologias de design existentes de outros produtos da AEM. O tutorial destaca as diferenças e considerações especiais ao desenvolver para o AEM Screens.
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 2%

---

# Desenvolvimento de um componente personalizado para o AEM Screens as a Cloud Service{#developing-a-custom-component-for-aem-screens}

O tutorial a seguir percorre as etapas para criar um componente personalizado para o AEM Screens. A AEM Screens reutiliza muitos padrões e tecnologias de design existentes de outros produtos da AEM. O tutorial destaca as diferenças e considerações especiais ao desenvolver para o AEM Screens.

## Visão geral {#overview}

Este tutorial destina-se a desenvolvedores novos no AEM Screens. Neste tutorial, um componente simples &quot;Olá, mundo&quot; é criado para um canal de sequência no AEM Screens. Uma caixa de diálogo permite que os autores atualizem o texto exibido.


## Pré-requisitos {#prerequisites}

Para concluir este tutorial, você precisa do seguinte:

1. Pacote de recursos mais recente do Screens

1. Player do AEM Screens

1. Ambiente de desenvolvimento local

As etapas e capturas de tela do tutorial são executadas usando o **CRXDE Lite**. IDEs também podem ser usados para concluir o tutorial. Mais informações sobre o uso de um IDE para desenvolver [com o AEM podem ser encontradas aqui](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=pt-BR).


## Configuração do projeto {#project-setup}

O código-fonte de um projeto Screens geralmente é gerenciado como um projeto Maven de vários módulos. Para acelerar o tutorial, um projeto foi pré-gerado usando o [Arquétipo de Projetos AEM 13](https://github.com/adobe/aem-project-archetype). Consulte [Configuração do projeto](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=pt-BR) para obter mais detalhes sobre como criar um projeto com o Arquétipo de projeto Maven AEM.

1. Baixe e instale os seguintes pacotes usando o [Gerenciador de Pacotes do CRX](http://localhost:4502/crx/packmgr/index.jsp):

[Obter arquivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [Obter arquivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **Opcionalmente** se trabalhar com o Eclipse ou outro IDE, baixe o pacote de origem abaixo. Implante o projeto em uma instância local do AEM usando o comando Maven:

   **`mvn -PautoInstallPackage clean install`**

   Inicie o projeto de execução We.Retail do HelloWorld SRC Screens

[Obter arquivo](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. No [Gerenciador de Pacotes do CRX](http://localhost:4502/crx/packmgr/index.jsp), verifique se os dois pacotes a seguir estão instalados:

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens We.Retail Executar pacotes Ui.Apps e Ui.Content instalados via Gerenciador de Pacotes do CRX](assets/crx-packages.png)

   Screens We.Retail Executar pacotes Ui.Apps e Ui.Content instalados via Gerenciador de pacotes do CRX

1. O pacote **screens-weretail-run.ui.apps** instala o código abaixo de `/apps/weretail-run`.

   Este pacote contém o código responsável pela renderização dos componentes personalizados do projeto. Esse pacote inclui o código do componente e qualquer JavaScript ou CSS necessário. Este pacote também incorpora o **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** que contém qualquer código Java™ necessário ao projeto.

   >[!NOTE]
   >
   >Neste tutorial, nenhum código Java™ é gravado. Se uma lógica de negócios mais complexa for necessária, o Java™ de back-end pode ser criado e implantado usando o pacote Core Java™.

   ![Representação do código ui.apps no CRXDE Lite](/help/screens-cloud/developing/assets/uipps-contents.png)

   Representação do código ui.apps no CRXDE Lite

   O componente **`helloworld`** é apenas um espaço reservado. Ao longo do tutorial, uma funcionalidade é adicionada, permitindo que um autor atualize a mensagem exibida pelo componente.

1. O pacote **screens-weretail-run.ui.content** instala o código abaixo de:

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   Este pacote contém o conteúdo inicial e a estrutura de configuração necessária para o projeto. **`/conf/we-retail-run`** contém todas as configurações para o projeto We.Retail Run. **`/content/dam/we-retail-run`** inclui iniciar ativos digitais para o projeto. **`/content/screens/we-retail-run`** contém a estrutura de conteúdo do Screens. O conteúdo sob esses caminhos é atualizado principalmente no AEM. Para promover a consistência entre ambientes (local, desenvolvimento, preparo, produção), geralmente uma estrutura de conteúdo básica é salva no controle de origem.

1. **Navegue até AEM Screens > Projeto de execução do We.Retail:**

   Na Navegação global do AEM > Clique no ícone da Screens. Verifique se o projeto executado We.Retail pode ser visto.

   ![we-retail-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## Criar o componente Hello World {#hello-world-cmp}

O componente Olá, mundo é um componente simples que permite que um usuário insira uma mensagem para ser exibida na tela. O componente é baseado no [Modelo de Componente do AEM Screens: https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

O AEM Screens tem algumas restrições interessantes que não são necessariamente verdadeiras para componentes WCM tradicionais do Sites.

* A maioria dos componentes do Screens deve ser executada em tela cheia nos dispositivos de sinalização digital de destino
* A maioria dos componentes do Screens deve ser incorporada aos canais de sequência para gerar apresentações de slides
* A criação deve permitir a edição de componentes individuais em um canal de sequência, portanto, renderizá-los em tela cheia está fora de questão

1. No **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` (ou IDE de escolha), navegue até `/apps/weretail-run/components/content/helloworld.`

   Adicionar as seguintes propriedades ao componente `helloworld`:

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![Propriedades de /apps/weretail-run/components/content/helloworld](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld

   O componente **`helloworld`** estende o componente **foundation/components/parbase** para que ele possa ser usado corretamente dentro de um canal de sequência.

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` chamado `helloworld.html.`

   Preencha o arquivo com o seguinte:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (that is, on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, that is, edit, design, scaffolding, and so on. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   Os componentes do Screens exigem duas renderizações diferentes, dependendo de qual [modo de criação](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/author-environment-tools.html?lang=pt-BR#page-modes) está sendo usado:

   1. **Produção**: modo de Visualização ou Publicação (wcmmode=disabled)
   1. **Editar**: usado para todos os outros modos de criação, ou seja, editar, design, andaime, desenvolvedor...

   `helloworld.html`age como uma opção, verificando qual modo de criação está ativo e redirecionando para outro script HTL. Uma convenção comum usada por componentes de telas é ter um script `edit.html` para o modo de Edição e um script `production.html` para o modo de Produção.

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` chamado `production.html.`

   Preencha o arquivo com o seguinte:

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   A marcação de produção acima é para o componente Hello World. Um atributo `data-duration` foi incluído, pois o componente é usado em um canal de Sequência. O atributo `data-duration` é usado pelo canal de sequência para saber por quanto tempo um item de sequência deve ser exibido.

   O componente renderiza uma marca `div` e uma marca `h1` com texto. `${properties.message}` é uma parte do script HTL que gera o conteúdo de uma propriedade JCR chamada `message`. Uma caixa de diálogo será criada posteriormente permitindo que um usuário insira um valor para o texto de propriedade `message`.

   Observe também que a notação BEM (Block Element Modifier) é usada com o componente. BEM é uma convenção de codificação CSS que facilita a criação de componentes reutilizáveis. BEM é a notação usada pelos [Componentes principais do AEM](https://github.com/adobe/aem-core-wcm-components/wiki/CSS-coding-conventions). <!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` chamado `edit.html.`

   Preencha o arquivo com o seguinte:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   A marcação de edição acima é para o componente Hello World. O primeiro bloco exibe uma versão de edição do componente se a mensagem de diálogo tiver sido preenchida.

   O segundo bloco é renderizado se nenhuma mensagem de diálogo for inserida. O `cq-placeholder` e o `data-emptytext` renderizam o rótulo ***Olá, mundo*** como um espaço reservado nesse caso. A string do rótulo pode ser internacionalizada usando i18n para oferecer suporte à criação em vários locais.

1. **A caixa de diálogo Copiar Imagem do Screens a ser usada para o componente Olá, Mundo.**

   É mais fácil começar com uma caixa de diálogo existente e, em seguida, fazer modificações.

   1. Copiar a caixa de diálogo de: `/libs/screens/core/components/content/image/cq:dialog`
   1. Colar a caixa de diálogo abaixo de `/apps/weretail-run/components/content/helloworld`

   ![copiar-imagem-caixa-de-diálogo](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **Atualize a caixa de diálogo Olá, Mundo para incluir uma guia para a mensagem.**

   Atualize a caixa de diálogo para que corresponda ao seguinte. A estrutura do nó JCR da caixa de diálogo final é apresentada abaixo em XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image is shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   O `textfield` da Mensagem é salvo em uma propriedade chamada `message` e o `numberfield` da Duração é salvo em uma propriedade chamada `duration`. Essas duas propriedades são referenciadas em `/apps/weretail-run/components/content/helloworld/production.html` pelo HTL como `${properties.message}` e `${properties.duration}`.

   ![Olá, Mundo - caixa de diálogo concluída](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Olá, mundo - caixa de diálogo concluída

## Criar bibliotecas do lado do cliente {#clientlibs}

As bibliotecas do lado do cliente fornecem um mecanismo para organizar e gerenciar arquivos CSS e JavaScript necessários para uma implementação do AEM.

Os componentes do AEM Screens são renderizados de forma diferente no modo Editar versus no modo Pré-visualização/Produção. Duas bibliotecas de clientes são criadas: uma para o modo Editar e outra para Pré-visualização/Produção.

1. Crie uma pasta para bibliotecas do lado do cliente para o componente Hello World.

   Abaixo de `/apps/weretail-run/components/content/helloworld`, crie uma pasta chamada `clientlibs`.

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. Abaixo da pasta `clientlibs`, crie um nó chamado `shared` do tipo `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. Adicione as seguintes propriedades à biblioteca de cliente compartilhada:

   * `allowProxy` | Booleano | `true`

   * `categories`| Cadeia de caracteres[] | `cq.screens.components`

   ![Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/shared](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/shared

   A propriedade categories é uma string que identifica a biblioteca do cliente. A categoria cq.screens.components é usada nos modos Editar e Visualizar/Produção. Portanto, qualquer CSS/JS definido no sharedclientlib é carregado em todos os modos.

   É uma prática recomendada nunca expor nenhum caminho diretamente para /apps em um ambiente de produção. A propriedade allowProxy garante que o CSS e o JS da biblioteca do cliente sejam referenciados por meio de um prefixo of/etc.clientlibs.

1. Crie o arquivo chamado `css.txt` abaixo da pasta compartilhada.

   Preencha o arquivo com o seguinte:

   ```
   #base=css
   
   styles.less
   ```

1. Crie uma pasta chamada `css` abaixo da pasta `shared`. Adicione um arquivo chamado `style.less` abaixo da pasta `css`. A estrutura das bibliotecas de clientes agora deve ficar assim:

   ![2018-04-30_às_3_11h](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   Em vez de escrever CSS diretamente, este tutorial usa MENOS. [LESS](https://lesscss.org/) é um pré-compilador de CSS popular que oferece suporte a variáveis, mixins e funções de CSS. As bibliotecas de clientes do AEM oferecem suporte nativo à compilação LESS. Sass ou outros pré-compiladores podem ser usados, mas devem ser compilados fora do AEM.

1. Popular `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` com o seguinte:

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. Copie e cole a pasta da biblioteca cliente `shared` para criar uma biblioteca cliente chamada `production`.

   ![Copie a biblioteca de cliente compartilhada para criar uma biblioteca de cliente de produção](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   Copie a biblioteca de cliente compartilhada para criar uma biblioteca de cliente de produção.

1. Atualize a propriedade `categories` da biblioteca de cliente de produção para `cq.screens.components.production.`

   Isso garante que os estilos só sejam carregados quando estiverem no modo de Pré-visualização/Produção.

   ![Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/production](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/production

1. Popular `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` com o seguinte:

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   Os estilos acima exibem a mensagem centralizada no meio da tela, mas somente no modo de produção.

Uma terceira categoria clientlibrary: `cq.screens.components.edit` pode ser usada para adicionar estilos específicos somente Edição ao componente.

| Categoria do Clientlib | Uso |
|---|---|
| `cq.screens.components` | Estilos e scripts compartilhados entre os modos de edição e de produção |
| `cq.screens.components.edit` | Estilos e scripts que são usados somente no modo de edição |
| `cq.screens.components.production` | Estilos e scripts que são usados somente no modo de produção |

## Criar uma página de design {#design-page}

O AEM Screens usa [Modelos de página estáticos](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-static.html?lang=pt-BR) e [Configurações de design](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/default-components-designmode.html?lang=pt-BR) para alterações globais. As configurações de design são usadas com frequência para configurar componentes permitidos para o Parsys em um canal. Uma prática recomendada é armazenar essas configurações de uma maneira específica do aplicativo.

Uma página de design de execução do We.Retail é criada abaixo, que armazena todas as configurações específicas do projeto de execução do We.Retail.

1. Em **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs`, navegue até `/apps/settings/wcm/designs`
1. Crie um nó abaixo da pasta de designs, chamado `we-retail-run`, com um tipo de `cq:Page`.
1. Abaixo da página `we-retail-run`, adicione outro nó chamado `jcr:content` do tipo `nt:unstructured`. Adicione as seguintes propriedades ao nó `jcr:content`:

   | Nome | Tipo | Valor |
   |---|---|---|
   | jcr:title | String | Execução do We.Retail |
   | sling:resourceType | String | wcm/core/components/designer |
   | cq:doctype | String | html_5 |

   ![Página de Design em /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   Página de design em /apps/settings/wcm/designs/we-retail-run

## Criar um canal de sequência {#create-sequence-channel}

O componente Hello World deve ser usado em um canal de sequência. Para testar o componente, um novo Canal de sequência é criado.

1. Na Navegação Global do AEM, navegue até **Screens** > **We.Retail Ru** n > e selecione **Canais**.

1. Clique no botão **Criar**

   1. Escolher **Criar Entidade**

   ![2018-04-30_às_5_18h](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. No assistente Criar:

1. Etapa de Modelo - escolher **Canal de Sequência**

   1. Etapa Propriedades

   * Guia Básica > Título = **Canal Ocioso**
   * Guia Canal > verificar **Tornar o canal online**

   ![canal ocioso](/help/screens-cloud/developing/assets/idle-channel.gif)

1. Abra as propriedades de página do Canal ocioso. Atualize o campo Design para que ele aponte para `/apps/settings/wcm/designs/we-retail-run,`a página de design criada na seção anterior.

   ![Configuração de design /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   Configuração de design apontando para /apps/settings/wcm/designs/we-retail-run

1. Edite o canal ocioso criado para que você possa abri-lo.

1. Mudar o modo de página para o Modo de **Design**.

   1. Clique na **chave inglesa** no Parsys para poder configurar os componentes permitidos.

   1. Selecione o grupo **Screens** e o grupo **We.Retail Run - Content**.

   ![2018-04-30_às_5_43h](assets/2018-04-30_at_5_43pm.png)

1. Mudar o modo de página para **Editar**. O componente Hello World agora pode ser adicionado à página e combinado com outros componentes de canal de sequência.

   ![2018-04-30_às_5_53h](assets/2018-04-30_at_5_53pm.png)

1. Em **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par`, navegue até `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. Observe que a propriedade `components` agora inclui `group:Screens`, `group:We.Retail Run - Content`.

   ![Configuração de design em /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   Configuração de design em /apps/settings/wcm/designs/we-retail-run

## Modelo para manipuladores personalizados {#custom-handlers}

Caso seu componente personalizado esteja usando recursos externos, como ativos (imagens, vídeos, fontes e ícones), representações de ativos específicas ou bibliotecas do lado do cliente (css e js), esses recursos não são adicionados automaticamente à configuração offline. O motivo é que o Adobe agrupa somente a marcação do HTML por padrão.

Para permitir que você personalize e otimize os ativos exatos que são baixados no reprodutor, o Adobe oferece um mecanismo de extensão para que os componentes personalizados exponham suas dependências à lógica de armazenamento em cache offline no Screens.

A seção abaixo mostra o modelo para manipuladores de recursos offline personalizados e os requisitos mínimos no `pom.xml` para esse projeto específico.

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

O código a seguir fornece os requisitos mínimos em `pom.xml` para esse projeto específico:

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## Tudo junto na prática {#putting-it-all-together}

O vídeo abaixo mostra o componente concluído e como ele pode ser adicionado a um canal de sequência. O Canal é então adicionado a uma exibição de Localização e, por fim, atribuído a um reprodutor do Screens.

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## Código concluído {#finished-code}

Abaixo está o código concluído do tutorial. Os **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** e **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** são os pacotes compilados do AEM. O **SRC-screens-weretail-run-0.0.1.zip** é o código-fonte não compilado que pode ser implantado usando Maven.

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
