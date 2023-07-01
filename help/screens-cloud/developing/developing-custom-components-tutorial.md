---
title: Desenvolvimento de um componente personalizado para o Screens as a Cloud Service
description: O tutorial a seguir percorre as etapas para criar um componente personalizado para o AEM Screens. A AEM Screens reutiliza muitos padrões e tecnologias de design existentes de outros produtos AEM. O tutorial destaca as diferenças e considerações especiais ao desenvolver para o AEM Screens.
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 3%

---

# Desenvolvimento de um componente personalizado para o AEM Screens as a Cloud Service{#developing-a-custom-component-for-aem-screens}

O tutorial a seguir percorre as etapas para criar um componente personalizado para o AEM Screens. A AEM Screens reutiliza muitos padrões e tecnologias de design existentes de outros produtos AEM. O tutorial destaca as diferenças e considerações especiais ao desenvolver para o AEM Screens.

## Visão geral {#overview}

Este tutorial destina-se a desenvolvedores novos no AEM Screens. Neste tutorial, um componente simples &quot;Olá, mundo&quot; é criado para um canal de sequência no AEM Screens. Uma caixa de diálogo permite que os autores atualizem o texto exibido.


## Pré-requisitos {#prerequisites}

Para concluir este tutorial, você precisa do seguinte:

1. Pacote de recursos do Screens mais recente

1. Player do AEM Screens

1. Ambiente de desenvolvimento local

As etapas e capturas de tela do tutorial são executadas usando **CRXDE Lite**. IDEs também podem ser usados para concluir o tutorial. Mais informações sobre o uso de um IDE para desenvolvimento [com AEM podem ser encontrados aqui.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en)


## Configuração do projeto {#project-setup}

O código-fonte de um projeto do Screens geralmente é gerenciado como um projeto Maven de vários módulos. Para acelerar o tutorial, um projeto foi pré-gerado usando o [Arquétipo de projeto 13 do AEM](https://github.com/adobe/aem-project-archetype). Mais detalhes sobre [a criação de um projeto com o Arquétipo de projeto Maven AEM pode ser encontrada aqui](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en).

1. Baixe e instale os seguintes pacotes usando [Gerenciador de pacotes CRX](http://localhost:4502/crx/packmgr/index.jsp):

[Obter arquivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [Obter arquivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **Opcionalmente** se trabalhar com o Eclipse ou outro IDE, faça o download do pacote de código-fonte abaixo. Implante o projeto em uma instância AEM local usando o comando Maven:

   **`mvn -PautoInstallPackage clean install`**

   Inicie o projeto We.Retail de telas SRC do HelloWorld

[Obter arquivo](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. Entrada [Gerenciador de pacotes CRX](http://localhost:4502/crx/packmgr/index.jsp), verifique se os dois pacotes a seguir estão instalados:

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens We.Retail Executar pacotes Ui.Apps e Ui.Content instalados via Gerenciador de pacotes do CRX](assets/crx-packages.png)

   Screens We.Retail Executar pacotes Ui.Apps e Ui.Content instalados via Gerenciador de pacotes do CRX

1. A variável **screens-weretail-run.ui.apps** o pacote instala o código abaixo de `/apps/weretail-run`.

   Este pacote contém o código responsável pela renderização dos componentes personalizados do projeto. Este pacote inclui o código do componente e qualquer JavaScript ou CSS necessário. Este pacote também incorpora **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** que contém qualquer código Java™ necessário para o projeto.

   >[!NOTE]
   >
   >Neste tutorial, nenhum código Java™ é gravado. Se uma lógica de negócios mais complexa for necessária, o Java™ de back-end pode ser criado e implantado usando o pacote Core Java™.

   ![Representação do código ui.apps no CRXDE Lite](/help/screens-cloud/developing/assets/uipps-contents.png)

   Representação do código ui.apps no CRXDE Lite

   A variável **`helloworld`** é apenas um espaço reservado. Ao longo do tutorial, uma funcionalidade é adicionada, permitindo que um autor atualize a mensagem exibida pelo componente.

1. A variável **screens-weretail-run.ui.content** o pacote instala o código abaixo de:

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   Este pacote contém o conteúdo inicial e a estrutura de configuração necessária para o projeto. **`/conf/we-retail-run`** contém todas as configurações do projeto de execução We.Retail. **`/content/dam/we-retail-run`** inclui a inicialização de ativos digitais para o projeto. **`/content/screens/we-retail-run`** contém a estrutura de conteúdo do Screens. O conteúdo sob todos esses caminhos é atualizado principalmente no AEM. Para promover a consistência entre ambientes (local, desenvolvimento, preparo, produção), geralmente uma estrutura de conteúdo básica é salva no controle de origem.

1. **Navegue até o projeto AEM Screens > We.Retail Executar:**

   No menu Iniciar AEM > Clique no ícone Screens. Verifique se o projeto executado We.Retail pode ser visto.

   ![we-retail-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## Criar o componente Hello World {#hello-world-cmp}

O componente Olá, mundo é um componente simples que permite que um usuário insira uma mensagem para ser exibida na tela. O componente é baseado no [Modelo do componente de AEM Screens: https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

O AEM Screens tem algumas restrições interessantes que não são necessariamente verdadeiras para componentes WCM tradicionais do Sites.

* A maioria dos componentes do Screens deve ser executada em tela cheia nos dispositivos de sinalização digital de destino
* A maioria dos componentes do Screens deve ser incorporada aos canais de sequência para gerar apresentações de slides
* A criação deve permitir a edição de componentes individuais em um canal de sequência, portanto, renderizá-los em tela cheia está fora de questão

1. Entrada **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` (ou IDE de escolha), navegue até `/apps/weretail-run/components/content/helloworld.`

   Adicione as seguintes propriedades à `helloworld` componente:

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![Propriedades de /apps/weretail-run/components/content/helloworld](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld

   A variável **`helloworld`** O componente estende a **foundation/components/parbase** para que possa ser usado corretamente dentro de um canal de sequência.

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` nomeado `helloworld.html.`

   Preencha o arquivo com o seguinte:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (that is, on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, that is, edit, design, scaffolding, etc. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   Os componentes do Screens exigem duas renderizações diferentes, dependendo de qual [modo de criação](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/author-environment-tools.html?lang=en#page-modes) está sendo usada:

   1. **Produção**: modo de Visualização ou Publicação (wcmmode=disabled)
   1. **Editar**: usado para todos os outros modos de criação, ou seja, edição, design, andaimes, desenvolvedor...

   `helloworld.html`O atua como um switch, verificando qual modo de criação está ativo e redirecionando para outro script HTL. Uma convenção comum usada por componentes de telas é ter uma `edit.html` script para o modo de Edição e um `production.html` para o modo de Produção.

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` nomeado `production.html.`

   Preencha o arquivo com o seguinte:

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   A marcação de produção acima é para o componente Hello World. A `data-duration` O atributo é incluído porque o componente é usado em um canal de Sequência. A variável `data-duration` O atributo é usado pelo canal de sequência para saber por quanto tempo um item de sequência deve ser exibido.

   O componente renderiza um `div` e uma `h1` com texto. `${properties.message}` é uma parte do script HTL que gera o conteúdo de uma propriedade JCR chamada `message`. Uma caixa de diálogo é criada posteriormente permitindo que um usuário insira um valor para a variável `message` texto da propriedade.

   Observe também que a notação BEM (Block Element Modifier) é usada com o componente. BEM é uma convenção de codificação CSS que facilita a criação de componentes reutilizáveis. BEM é a notação usada por [Componentes principais do AEM](https://github.com/adobe/aem-core-wcm-components/wiki/CSS-coding-conventions). <!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. Criar um arquivo abaixo de `/apps/weretail-run/components/content/helloworld` nomeado `edit.html.`

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

   O segundo bloco é renderizado se nenhuma mensagem de diálogo for inserida. A variável `cq-placeholder` e `data-emptytext` renderizar o rótulo ***Olá, mundo*** nesse caso, como titular. A string do rótulo pode ser internacionalizada usando i18n para oferecer suporte à criação em vários locais.

1. **A caixa de diálogo Copiar imagem do Screens a ser usada para o componente Olá, mundo.**

   É mais fácil começar com uma caixa de diálogo existente e, em seguida, fazer modificações.

   1. Copiar a caixa de diálogo de: `/libs/screens/core/components/content/image/cq:dialog`
   1. Colar a caixa de diálogo abaixo `/apps/weretail-run/components/content/helloworld`

   ![copy-image-dialog](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **Atualize a caixa de diálogo Olá, mundo para incluir uma guia para a mensagem.**

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

   A variável `textfield` para a mensagem for salva em uma propriedade chamada `message` e que o `numberfield` para a Duração for salva em uma propriedade chamada `duration`. Essas duas propriedades são referenciadas na `/apps/weretail-run/components/content/helloworld/production.html` por HTL como `${properties.message}` e `${properties.duration}`.

   ![Olá, mundo - caixa de diálogo concluída](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Olá, mundo - caixa de diálogo concluída

## Criar bibliotecas do lado do cliente {#clientlibs}

As bibliotecas do lado do cliente fornecem um mecanismo para organizar e gerenciar arquivos CSS e JavaScript necessários para uma implementação do AEM.

Os componentes do AEM Screens são renderizados de forma diferente no modo Editar versus no modo Pré-visualização/Produção. Duas bibliotecas de clientes são criadas: uma para o modo Editar e outra para Pré-visualização/Produção.

1. Crie uma pasta para bibliotecas do lado do cliente para o componente Hello World.

   Abaixo `/apps/weretail-run/components/content/helloworld`, crie uma pasta chamada `clientlibs`.

   ![04/2018/30_às_1046h](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. Abaixo de `clientlibs` , crie um nó chamado `shared` do tipo `cq:ClientLibraryFolder.`

   ![2018-04-30_às_1115h](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. Adicione as seguintes propriedades à biblioteca de cliente compartilhada:

   * `allowProxy` | Booleano | `true`

   * `categories`| String[] | `cq.screens.components`

   ![Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/shared](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/shared

   A propriedade categories é uma string que identifica a biblioteca do cliente. A categoria cq.screens.components é usada nos modos Editar e Visualizar/Produção. Portanto, qualquer CSS/JS definido no sharedclientlib é carregado em todos os modos.

   É uma prática recomendada nunca expor nenhum caminho diretamente para /apps em um ambiente de produção. A propriedade allowProxy garante que o CSS e o JS da biblioteca do cliente sejam referenciados por meio de um prefixo of/etc.clientlibs.

1. Criar arquivo chamado `css.txt` abaixo da pasta compartilhada.

   Preencha o arquivo com o seguinte:

   ```
   #base=css
   
   styles.less
   ```

1. Crie uma pasta chamada `css` abaixo de `shared` pasta. Adicionar um arquivo chamado `style.less` abaixo de `css` pasta. A estrutura das bibliotecas de clientes agora deve ficar assim:

   ![2018-04-30_às_3_11h](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   Em vez de escrever CSS diretamente, este tutorial usa MENOS. [MENOS](https://lesscss.org/) O é um pré-compilador de CSS popular que oferece suporte a variáveis, mixins e funções de CSS. Bibliotecas de clientes AEM nativamente oferecem suporte à compilação LESS. Sass ou outros pré-compiladores podem ser usados, mas devem ser compilados fora do AEM.

1. Preencher `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` com o seguinte:

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

1. Copie e cole o `shared` pasta da biblioteca do cliente para criar uma biblioteca do cliente chamada `production`.

   ![Copie a biblioteca de cliente compartilhada para criar uma nova biblioteca de cliente de produção](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   Copie a biblioteca de cliente compartilhada para criar uma biblioteca de cliente de produção.

1. Atualize o `categories` propriedade da biblioteca de cliente de produção a ser `cq.screens.components.production.`

   Isso garante que os estilos só sejam carregados quando estiverem no modo de Pré-visualização/Produção.

   ![Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/production](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   Propriedades de /apps/weretail-run/components/content/helloworld/clientlibs/production

1. Preencher `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` com o seguinte:

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

Uma terceira categoria de clientlibrary: `cq.screens.components.edit` pode ser usado para adicionar estilos específicos somente edição ao componente.

| Categoria do Clientlib | Uso |
|---|---|
| `cq.screens.components` | Estilos e scripts compartilhados entre os modos de edição e de produção |
| `cq.screens.components.edit` | Estilos e scripts que são usados somente no modo de edição |
| `cq.screens.components.production` | Estilos e scripts que são usados somente no modo de produção |

## Criar uma página de design {#design-page}

O AEM Screens usa [Modelos de página estáticos](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-static.html?lang=pt-BR) e [Configurações de design](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/default-components-designmode.html?lang=en) para alterações globais. As configurações de design são usadas com frequência para configurar componentes permitidos para o Parsys em um canal. Uma prática recomendada é armazenar essas configurações de uma maneira específica do aplicativo.

Uma página de design de execução do We.Retail é criada abaixo, que armazena todas as configurações específicas do projeto de execução do We.Retail.

1. Entrada **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs`, navegue até `/apps/settings/wcm/designs`
1. Crie um nó abaixo da pasta de designs, chamado `we-retail-run` com um tipo de `cq:Page`.
1. Abaixo de `we-retail-run` adicione outro nó chamado `jcr:content` do tipo `nt:unstructured`. Adicione as seguintes propriedades à `jcr:content` nó:

   | Nome | Tipo | Valor |
   |---|---|---|
   | jcr:title | String | Execução do We.Retail |
   | sling:resourceType | String | wcm/core/components/designer |
   | cq:doctype | String | html_5 |

   ![Página de design em /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   Página de design em /apps/settings/wcm/designs/we-retail-run

## Criar um canal de sequência {#create-sequence-channel}

O componente Hello World deve ser usado em um canal de sequência. Para testar o componente, um novo Canal de sequência é criado.

1. No menu Iniciar do AEM, navegue até **Screens** > **Execução do We.Retail** n > e selecione **Canais**.

1. Clique em **Criar** botão

   1. Escolher **Criar entidade**

   ![2018-04-30_às_5_18h](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. No assistente Criar:

1. Etapa de modelo - Escolher **Canal de sequência**

   1. Etapa Propriedades

   * Guia Básica > Título = **Canal ocioso**
   * Guia Canal > verificar **Tornar o canal online**

   ![idle-channel](/help/screens-cloud/developing/assets/idle-channel.gif)

1. Abra as propriedades de página do Canal ocioso. Atualizar o campo Design para que aponte para `/apps/settings/wcm/designs/we-retail-run,`a página de design criada na seção anterior.

   ![Configuração de design /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   Configuração de design apontando para /apps/settings/wcm/designs/we-retail-run

1. Edite o canal ocioso recém-criado para que você possa abri-lo.

1. Alternar o modo de página para **Design** Modo.

   1. Clique em **chave inglesa** no Parsys para que você possa configurar os componentes permitidos.

   1. Selecione o **Screens** e o **Execução do We.Retail - Conteúdo** grupo.

   ![2018-04-30_às_5_43h](assets/2018-04-30_at_5_43pm.png)

1. Alternar o modo de página para **Editar**. O componente Hello World agora pode ser adicionado à página e combinado com outros componentes de canal de sequência.

   ![2018-04-30_às_5_53h](assets/2018-04-30_at_5_53pm.png)

1. Entrada **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par`, navegue até `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. Observe a `components` A propriedade agora inclui `group:Screens`, `group:We.Retail Run - Content`.

   ![Configuração de design em /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   Configuração de design em /apps/settings/wcm/designs/we-retail-run

## Modelo para manipuladores personalizados {#custom-handlers}

Caso seu componente personalizado esteja usando recursos externos, como ativos (imagens, vídeos, fontes e ícones), representações de ativos específicas ou bibliotecas do lado do cliente (css e js), esses recursos não são adicionados automaticamente à configuração offline. O motivo é que o Adobe só agrupa a marcação HTML por padrão.

Para permitir que você personalize e otimize os ativos exatos que são baixados para o reprodutor, o Adobe oferece um mecanismo de extensão para que os componentes personalizados exponham suas dependências à lógica de armazenamento em cache offline no Screens.

A seção abaixo mostra o modelo para manipuladores de recursos offline personalizados e os requisitos mínimos na `pom.xml` para esse projeto específico.

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

O código a seguir fornece os requisitos mínimos nas `pom.xml` para esse projeto específico:

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

Abaixo está o código concluído do tutorial. A variável **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** e **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** são os pacotes de AEM compilados. O **SRC-screens-weretail-run-0.0.1.zip **é o código-fonte não compilado que pode ser implantado usando Maven.

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[Obter arquivo](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
