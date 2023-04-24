---
title: Adicionar um formulário adaptável (Componentes principais) na página AEM Sites
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: É possível usar o Formulário adaptável (Componentes principais) em uma página do AEM Sites para preencher e enviar um formulário sem sair das páginas do AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 2%

---

# Adicionar Forms adaptável a uma página do AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

## Visão geral {#overview}

Você pode criar ou incorporar facilmente o Adaptive Forms em uma página do AEM Sites para permitir que os usuários preencham e enviem um formulário sem sair da página Sites . Ajuda o usuário a permanecer no contexto de outros elementos da página da Web e interagir simultaneamente com o formulário.

Você pode escolher um dos seguintes métodos para criar ou incorporar um formulário adaptável em uma página do AEM Sites:

* **Crie um formulário adaptável arrastando e soltando componentes do formulário no Componente adaptável do contêiner do Forms**: Use o [Contêiner Adaptive Forms](#af-container-component) para criar um espaço na página da Web que hospedaria o Formulário adaptável. Você pode arrastar e soltar o componente Formulário adaptável nesse espaço para criar um formulário. Por exemplo, veja o vídeo abaixo para saber como criar um formulário adaptável usando [!UICONTROL Contêiner Adaptive Forms] componente:

>[!VIDEO](/help/forms/assets/formcreationbyadaptiveformcontainer.mp4)

O [Contêiner de formulário adaptável](#af-container-component) permite criar experiências de registro digital utilizando componentes adaptáveis do Forms diretamente no editor do AEM Sites. Essa integração fornece uma experiência contínua aos autores do AEM Sites que desejam criar e gerenciar formulários em suas páginas do AEM Sites.

* **Incorporar um formulário adaptável existente**: O [Adaptável Forms - Incorporado](#embed-existing-af) permite incorporar facilmente um formulário adaptável pré-existente em uma página no AEM Sites. Por exemplo, incorpore um formulário adaptável usando o [!UICONTROL Adaptável Forms - Incorporado] na página do Site, conforme ilustrado no vídeo a seguir:

>[!VIDEO](/help/forms/assets/embednewform_embed.mp4)

Esse recurso melhora a adaptabilidade e a reutilização do Adaptive Forms. Essa integração oferece uma maneira conveniente de os clientes reutilizarem o Adaptive Forms que já criaram.

* **Usar o Assistente do Adaptive Forms para criar um formulário**:

   Use o [Adaptável Forms - Incorporado](#embed-new-af) para criar um formulário adaptável no editor do AEM Sites usando o assistente de criação de formulários. O formulário é salvo como uma entidade externa. É possível reutilizar esse formulário em outras páginas do Sites e também em formulários independentes.
Por exemplo, veja o vídeo abaixo para saber como criar e incorporar um formulário adaptável recém-criado usando o [!UICONTROL Adaptável Forms - Incorporado] na página do Site.

>[!VIDEO](/help/forms/assets/createnewform_embed.mp4)

### Consideração {#considerations}

Você pode usar o Editor de regras para adicionar ou controlar o comportamento dinâmico dos componentes do Formulário adaptável. Por exemplo, ocultar ou mostrar um componente. O Editor de regras não está disponível para componentes de Formulário não adaptável. Portanto, use sua diligência ao usar componentes de Formulário não adaptáveis no componente Contêiner do AEM Forms.

## Criar um formulário adaptável usando o componente adaptável do contêiner do Forms {#af-container-component}

O [!UICONTROL Contêiner de formulário adaptável] permite criar experiências de inscrição digital usando componentes adaptáveis do Forms no editor do AEM Sites. É possível criar um formulário adaptável arrastando e soltando os componentes do formulário.

### Pré-requisitos {#prerequisites-af-container}

+++ Habilitar **[!UICONTROL Contêiner Adaptive Forms]** na política do modelo associado.

Para ativar [!UICONTROL Contêiner Adaptive Forms] na política do modelo, execute as seguintes etapas:
1. Vá para o [!UICONTROL Informações da página] > [!UICONTROL Editar modelo]
1. Clique no botão [!UICONTROL Política] e selecione o **Exemplos de componentes principais - Formulário adaptável** caixa de seleção.
1. Clique em [!UICONTROL Concluído].

>[!VIDEO](/help/forms/assets/adaptiveformcontainer.mp4)

+++

+++ Incluir as clientlibs na página do site

Para usar componentes Adaptive Forms em uma página do AEM Sites, inclua as bibliotecas de clientes Customheaderlibs e Customfooterlibs na página do AEM Sites usando o Repositório AEM Archetype/Git e o pipeline de implantação.

1. Abra seu [Arquétipo AEM Forms ou Repositório Git Clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.
1. Vá até `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso sling](/help/forms/assets/slingresource.png)

1. Crie a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` Igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png)

1. Adicionar `customheaderlibs.html` e `customfooterlibs.html` arquivos.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   O customfooterlibs.html é usado para JavaScript e o customheaderlibs.html para o css.

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as alterações.

+++

### Criar um formulário adaptável usando o componente Adaptive Forms Container {#create-af-using-af-container}


Para criar um formulário adaptável usando [!UICONTROL Contêiner Adaptive Forms] componente:

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes , arraste e solte o **[!UICONTROL Contêiner Adaptive Forms]** na página.
1. Crie um formulário adaptável usando os componentes adaptáveis do Forms.
1. Salve as configurações.

>[!VIDEO](/help/forms/assets/af-container.mp4)

Seu formulário está pronto. Ao publicar a página do AEM Sites, ele publica automaticamente um formulário adaptável e seus ativos referenciados associados.

#### Configurar as propriedades do contêiner de formulário adaptável {#configure-additional-settings-container}

Você pode personalizar as configurações avançadas do [!UICONTROL Contêiner de formulário adaptável] componente. Por exemplo, você pode configurar o Serviço de preenchimento prévio para carregar um Formulário adaptável com valores pré-preenchidos na página de um site. As configurações do Modelo de dados são definidas para associar o Formulário adaptável a um modelo de dados. Se quiser salvar os dados no OneDrive ou SharePoint ao enviar um Formulário adaptável, configure as definições para a ação Enviar. Você também pode adicionar uma ação de Enviar personalizada para o seu Forms adaptável.

Para definir as propriedades da variável **[!UICONTROL Contêiner Adaptive Forms]** , clique no ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) na barra de ações. O **[!UICONTROL Editar contêiner adaptável do Forms]** será aberta.

![Caixa de diálogo de edição](/help/forms/assets/adaptiveformcontainer-editdialog.png)

No [!UICONTROL Editar contêiner adaptável do Forms] , é possível especificar o seguinte.
* **Guia Básico**
   * **Serviço de preenchimento prévio**: Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para obter informações sobre o serviço de preenchimento prévio, consulte [Preencher previamente campos do formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoria da biblioteca do cliente**: Especifique a [Funções do JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) que são usados em expressões e compatíveis com o Adaptive Forms.
* **Modelo de dados**: Um Modelo de dados permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Choose **[!UICONTROL Modelo de dados do formulário]** se o formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.
   * **Modelo de dados do formulário**: Um Modelo de dados de formulário permite que um Formulário adaptável se comunique com fontes de dados diferentes. Para obter informações sobre como configurar uma fonte de dados, consulte [Configurar fontes de dados.](/help/forms/configure-data-sources.md)
   * **Esquema**: O esquema representa a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. Você pode [associar o esquema a um formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) e use seus elementos para adicionar conteúdo dinâmico a um Formulário adaptável.

      >[!NOTE]
      >
      > Após configurar o modelo de dados de Formulário, não é possível alterar o Modelo de formulário associado. No entanto, é possível modificar o schema associado ao modelo de dados Form .

* **Guia Enviar**

   * **Redirecionar para o URL**

      **Redirecionar URL/caminho**: Especifica o URL ou caminho para o qual um Formulário adaptável é redirecionado após a ação de envio.

      **Enviar ação**: Uma ação de envio é acionada quando um usuário clica no botão Enviar em um formulário adaptável. Você pode [configurar a ação de envio no formulário adaptável](/help/forms/configuring-submit-actions.md). Os formulários adaptáveis fornecem algumas ações de envio prontas para uso:
      * Enviar para ponto de extremidade REST
      * Enviar e-mail
      * Enviar usando modelo de dados do formulário
      * Chamar um fluxo de trabalho AEM
      * Enviar para o SharePoint
      * Enviar para o OneDrive
      * Enviar para o Armazenamento de blob do Azure

   Você também pode [estender as ações de envio padrão](custom-submit-action-form.md) para criar sua própria ação de envio personalizada.

* **Mostrar mensagem**
   * **Conteúdo da mensagem**: Escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.

## Incorporar um formulário adaptável existente  {#aem-container-component}

Usando **[!UICONTROL Adaptável Forms - Incorporado]** , é possível incorporar o novo formulário adaptável ou incorporar um formulário adaptável existente na página do site. O [!UICONTROL Adaptável Forms - Incorporado] permite:

* [Incorporar um formulário adaptável existente](#embed-new-af)

* [Criar e incorporar um novo formulário adaptável](#embed-existing-af)

### Pré-requisitos {#prerequisites}

+++ Ative o **Adaptável Forms - Incorporado** na política do modelo associado.

Para ativar [!UICONTROL Adaptável Forms - Incorporado] na política do modelo, execute as seguintes etapas:
1. Vá para o [!UICONTROL Informações da página] > [!UICONTROL Editar modelo]
1. Clique no botão [!UICONTROL Política] e selecione o **Conteúdo principal** caixa de seleção.
1. Clique em [!UICONTROL Concluído].

>[!VIDEO](/help/forms/assets/enableadaptiveform-embedtemplate.mp4)

+++

+++ Incluir as clientlibs na página do site

Quando a variável **[!UICONTROL Quando o formulário cobre a largura inteira de uma página]** é selecionada na variável **[!UICONTROL Contêineres de formulário]** configurar caixa de diálogo e **Forms adaptável usando componentes principais** forem usadas, é necessário incluir as clientlibs na página do Site correspondente.

![Sobrepor Gif](/help/forms/assets/overlaycorecomponent.gif)

Para usar componentes Adaptive Forms em uma página do AEM Sites, inclua as bibliotecas de clientes Customheaderlibs e Customfooterlibs na página do AEM Sites usando o Repositório AEM Archetype/Git e o pipeline de implantação.

1. Abra seu [Arquétipo AEM Forms ou Repositório Git Clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.
1. Vá até `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso sling](/help/forms/assets/slingresource.png)

1. Crie a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` Igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png)

1. Adicionar `customheaderlibs.html` e `customfooterlibs.html` arquivos.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   O customfooterlibs.html é usado para JavaScript e o customheaderlibs.html para o CSS.

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as alterações.

+++

### Incorporar novo formulário adaptável {#embed-new-af}

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes , arraste e solte o [!UICONTROL Adaptável Forms - Incorporado] na página.
1. Clique no botão **Plus** e você será redirecionado para o assistente de criação de formulário.

   ![Adaptável Forms - Componente incorporado](/help/forms/assets/aemformcontainer.png)

1. Crie um novo formulário adaptável no [!UICONTROL Criação de formulário] assistente.
1. O [!UICONTROL Caminho do ativo] já inclui o caminho de um formulário adaptável criado
1. Salve as configurações. O formulário adaptável agora está incorporado na página.

### Incorporar formulário adaptável existente {#embed-existing-af}

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes , arraste e solte o [!UICONTROL Adaptável Forms - Incorporado] na página.
1. Toque no [!UICONTROL Adaptável Forms - Incorporado] na página sites e toque em ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) na barra de ações. O **[!UICONTROL Editar Forms adaptável - Incorporar]** será aberta.
1. Navegue e selecione o Formulário adaptável a ser incorporado no [!UICONTROL Caminho do ativo].
1. Salve as configurações. O formulário adaptável agora está incorporado na página.

#### Configurar formulário adaptável - Incorporar propriedades

Você pode personalizar as configurações avançadas do [!UICONTROL Formulário adaptável - Incorporar] componente. No [!UICONTROL Editar Forms adaptável - Incorporar] , é possível especificar o seguinte.
* **Caminho do ativo**: Navegue e selecione o Formulário adaptável a ser incorporado. Ele é preenchido automaticamente se você soltou no navegador Ativos.
* **Pós-envio** : Selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.
   * **Mostrar mensagem de agradecimento**: Escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
   * **Mostrar página de agradecimento**: Navegue e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
   * **Redirecionar para página de agradecimento**: Habilite a opção para substituir a página que contém o formulário adaptável incorporado pela página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável no [!UICONTROL Adaptável Forms - Incorporado] , sem atualizar sites subjacentes na página. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
* **Usar idioma da página**: Use o local da página do AEM Sites em vez do local do Formulário adaptativo.
* **Definir foco no formulário**: Selecione para definir o foco no primeiro campo do formulário adaptável.
* **O formulário cobre toda a largura do quadro**: Se marcado, o iframe não é usado para renderizar o formulário.
* **Altura**: Especifique a altura do contêiner. Deixe em branco para redimensionar automaticamente o contêiner.
* **Biblioteca de clientes CSS**: Especifique o caminho para uma biblioteca de cliente CSS.

### Publicar formulário adaptável incorporado {#publishing-embedded-adaptive-form}

Vamos considerar os seguintes cenários para a publicação de um formulário adaptável incorporado AEM página de sites:

* Se você estiver publicando a página AEM sites pela primeira vez e ela incluir um Formulário adaptável incorporado, publique a página sites e o ativo incorporado.
* Se você modificou apenas o Formulário adaptativo incorporado em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicado. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o Formulário adaptativo incorporado , republique a página de sites e o ativo incorporado.

### Modificar formulário adaptável incorporado  {#modifying-embedded-adaptive-form}

Para modificar qualquer configuração ou propriedade do Formulário adaptável incorporado, execute um dos procedimentos a seguir.

* Abra o formulário original em um Formulário adaptável no respectivo editor e modifique-o.
* Toque no Formulário adaptável na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que pode ser modificado.

>[!NOTE]
>
>As alterações feitas no formulário adaptável original refletem automaticamente no formulário incorporado. No entanto, republique o Formulário adaptativo ou a página do site para refletir as alterações na página publicada.

### Práticas recomendadas {#best-practices}

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos do usuário e os envios de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms enviados no Forms Portal.

[Na página AEM Sites, o modo Layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) permite redimensionar um formulário adaptável que foi criado ou incorporado em uma página de um site AEM.

![Suporte para layout de AF](/help/forms/assets/afsite-layoutsupport.gif)

AEM página de sites mantém uma referência ao formulário adaptável. Ao traduzir uma página do AEM Sites, ela traduz automaticamente um Formulário adaptável e seus ativos referenciados associados usando o [projetos de tradução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) em outros idiomas.

