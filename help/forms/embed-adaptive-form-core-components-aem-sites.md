---
title: Como adicionar ou criar componentes principais do formulário adaptável na página do AEM Sites?
description: Use os Componentes principais do formulário adaptável em uma página do AEM Sites para preencher e enviar um formulário sem sair das páginas do AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Criar ou adicionar um formulário adaptável usando o Editor do AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

Você pode criar ou incorporar facilmente o Adaptive Forms em uma página do AEM Sites para permitir que seus usuários preencham e enviem um formulário sem sair da página Sites. Ele ajuda o usuário a permanecer no contexto de outros elementos da página da Web e interagir simultaneamente com o formulário.

Você pode escolher um dos seguintes métodos para criar ou adicionar um Formulário adaptável a uma página do AEM Sites:

* **Criar um Formulário adaptável usando o componente Contêiner adaptável do Forms**: o componente [Contêiner adaptável do Formulário](#af-container-component) permite que você crie experiências de inscrição digital usando componentes adaptáveis do Forms diretamente no editor do AEM Sites. Essa integração fornece uma experiência perfeita para autores do AEM Sites que desejam criar e gerenciar formulários em suas páginas do AEM Sites.

* **Adicionar um Formulário adaptável existente**: o componente [Forms adaptável - Incorporado(v2)](#embed-existing-af) permite que você adicione facilmente um Formulário adaptável pré-existente em uma página no AEM Sites. Esse recurso melhora a adaptabilidade e a reutilização do Adaptive Forms. Essa integração oferece uma maneira conveniente para os clientes reutilizarem o Adaptive Forms que já criaram.

* **Usar o Assistente do Adaptive Forms para criar um formulário**: Use o componente [Adaptive Forms - Embed(v2)](#embed-new-af) para criar um Formulário Adaptável no editor do AEM Sites usando o Assistente de Criação de Formulário. O formulário é salvo como uma entidade externa. Você também pode reutilizar esse formulário em outras páginas do Sites e formulários independentes.

* **Adicionar várias Forms adaptáveis em uma página do AEM Sites**: para adicionar várias Forms adaptáveis em uma página do AEM Sites, use os componentes de contêiner do AEM Forms - [Forms adaptável - Incorporado(v2)](#embed-new-af) e [Contêiner de formulário adaptável](#af-container-component). Caso precise adicionar mais de um formulário adaptável como uma div em uma página do AEM Sites, você pode usar o componente de Contêiner de formulário adaptável.

Você pode usar o Editor de regras para adicionar ou controlar o comportamento dinâmico dos componentes de Formulário adaptável. Por exemplo, ocultar ou mostrar um componente. O Editor de regras não está disponível para componentes de formulário não adaptáveis. Portanto, use sua diligência ao usar componentes de formulário não adaptáveis no componente de Contêiner do AEM Forms.

## Criar um formulário adaptável usando o componente de Contêiner adaptável do Forms {#af-container-component}

O componente [!UICONTROL Contêiner de formulário adaptável] permite criar experiências de inscrição digital usando componentes do Adaptive Forms no editor do AEM Sites. Você pode criar um Formulário adaptável arrastando e soltando os componentes do formulário.

### Pré-requisitos {#prerequisites-af-container}

+++ Habilitar o componente **[!UICONTROL Contêiner de Forms Adaptável]**.

Para habilitar o componente [!UICONTROL Contêiner de Forms adaptável] na política do modelo, execute as seguintes etapas:

1. Vá para as [!UICONTROL Informações da Página] > [!UICONTROL Editar Modelo]
1. Clique na [!UICONTROL Política] e marque a caixa de seleção **[!UICONTROL Contêiner de Forms Adaptável]** em **[Nome do Projeto do Arquétipo AEM] - Formulário Adaptável**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Incluir bibliotecas de clientes Forms adaptáveis na página AEM Sites

Para usar os componentes do Adaptive Forms em uma página do AEM Sites, inclua as bibliotecas de clientes Customheaderlibs e Customfooterlibs à página do AEM Sites AEM usando o Repositório Git/Arquétipo de e o pipeline de implantação.

1. Abra o projeto [Arquétipo do AEM Forms ou Repositório Git Clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.
1. Vá até `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Criar a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png)

1. Adicionar arquivos `customheaderlibs.html` e `customfooterlibs.html`.

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

   O customfooterlibs.html é usado para o JavaScript e o customheaderlibs.html para o css.

1. [Execute o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as alterações.

+++

### Criar um formulário adaptável usando o componente de Contêiner adaptável do Forms {#create-af-using-af-container}


Para criar um formulário adaptável usando o componente [!UICONTROL Contêiner de Forms adaptável]:

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes, arraste e solte na página o componente **[!UICONTROL Contêiner de Forms adaptável]**.
1. Criar um formulário adaptável usando os componentes adaptáveis do Forms.
1. Salve as configurações.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Seu formulário está pronto. Ao publicar a página do AEM Sites, ele publica automaticamente o Formulário adaptável e seus ativos referenciados associados.

#### Configurar propriedades do contêiner de formulário adaptável {#configure-additional-settings-container}

Você pode personalizar as configurações avançadas do componente [!UICONTROL Contêiner de formulário adaptável]. Por exemplo,

* Você pode configurar o Serviço de preenchimento prévio para carregar um Formulário adaptável com valores preenchidos previamente na página de um Site.
* É possível definir as configurações do Modelo de dados para associar o Formulário adaptável a uma fonte de dados.
* Você pode configurar as ações de envio para enviar os dados no Microsoft® OneDrive, Microsoft® OneDrive ou outras fontes de dados no envio de um formulário. Você também pode criar e selecionar uma ação Enviar personalizada para o Forms adaptável.

Para definir as propriedades do componente **[!UICONTROL Contêiner de Forms adaptável]**, clique em ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) na barra de ações. A caixa de diálogo **[!UICONTROL Editar Contêiner de Forms Adaptável]** é aberta.

![Caixa de diálogo de edição](/help/forms/assets/adaptiveformcontainer-editdialog.png)

Na caixa de diálogo [!UICONTROL Editar Contêiner de Forms Adaptável], você pode especificar o seguinte.
* **Guia Básico**
   * **Serviço de preenchimento prévio**: você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para obter informações sobre o serviço de preenchimento prévio, consulte [Preencher previamente os campos do formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoria da biblioteca do cliente**: especifique as [funções do JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) usadas em expressões e com suporte do Adaptive Forms.
* **Modelo de Dados**: um Modelo de Dados permite integrar entidades e serviços de diferentes fontes de dados a um Formulário Adaptável. Escolha **[!UICONTROL Modelo de dados de formulário]** se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.
   * **Modelo de dados de formulário**: um modelo de dados de formulário (FDM) permite que um formulário adaptável se comunique com fontes de dados diferentes. Para obter informações sobre como configurar uma fonte de dados, consulte [Configurar fontes de dados](/help/forms/configure-data-sources.md).
   * **Esquema**: o esquema representa a estrutura em que os dados são produzidos ou consumidos pelo sistema back-end em sua organização. Você pode [associar o esquema a um Formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) e usar seus elementos para adicionar conteúdo dinâmico a um Formulário adaptável.

     >[!NOTE]
     >
     > Após configurar o Modelo de dados de formulário (FDM), não é possível alterar o Modelo de formulário associado. No entanto, é possível modificar o esquema associado ao Modelo de dados de formulário (FDM).

* **Guia Envio**

   * **Redirecionar para a URL**
      * **Redirecionar URL/Caminho**: especifica a URL ou o caminho para o qual um Formulário adaptável é redirecionado após o envio.

      * **Ação de envio**: uma ação de envio é acionada quando um usuário clica no botão Enviar em um Formulário adaptável. Você pode [configurar a ação de envio no Formulário adaptável](/help/forms/configuring-submit-actions.md). Os formulários adaptáveis fornecem as seguintes ações de envio prontas para uso:
         * Enviar para endpoint REST
         * Enviar e-mail
         * Enviar usando o Modelo de dados de formulário (FDM)
         * Chamar um fluxo de trabalho de AEM
         * Enviar para o SharePoint
         * Enviar para o OneDrive
         * Enviar para o Armazenamento de blob do Azure

  Você também pode [estender as Ações de Envio padrão](custom-submit-action-form.md) para criar sua própria Ação de Envio personalizada.

* **Mostrar mensagem**
   * **Conteúdo da Mensagem**: escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.

## Incorporar um formulário adaptável  {#aem-container-component}

Usando o componente **[!UICONTROL Forms Adaptável - Incorporado (V2)]**, você pode incorporar um novo Formulário Adaptável ou incorporar um Formulário Adaptável existente na página do Site. O componente [!UICONTROL Forms adaptável - Embed(v2)] permite:

* [Adicionar um formulário adaptável existente](#embed-new-af)

* [Criar e adicionar um novo Formulário adaptável](#embed-existing-af)

### Pré-requisitos {#prerequisites}

+++ Habilitar o componente **Forms Adaptável - Incorporado**.

Para habilitar o componente [!UICONTROL Forms Adaptável - Incorporado(v2)] na política do modelo, execute as seguintes etapas:

1. Vá para as [!UICONTROL Informações da Página] > [!UICONTROL Editar Modelo]

1. Clique na [!UICONTROL Política] e marque a caixa de seleção **[!UICONTROL Formulário adaptável - Incorporar (v2)]** no grupo **[!UICONTROL [Nome do projeto do Arquétipo AEM] - Forms]**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Incluir bibliotecas de clientes Forms adaptáveis na página AEM Sites

Quando a opção **[!UICONTROL Quando o formulário cobre toda a largura de uma página]** é selecionada na caixa de diálogo de configuração **[!UICONTROL Contêineres de Formulário]** e o **Forms Adaptável usando componentes principais** é usado, é necessário incluir as bibliotecas de clientes na página do Site correspondente.

![Sobrepor Gif](/help/forms/assets/overlaycorecomponent.gif)

Para usar os componentes do Adaptive Forms em uma página do AEM Sites, inclua as bibliotecas de clientes `Customheaderlibs` e `Customfooterlibs` na página do AEM Sites AEM usando o Arquétipo do/Repositório Git e o pipeline de implantação.

1. Abra o projeto [Arquétipo do AEM Forms ou Repositório Git Clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.
1. Vá até `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Criar a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png)

1. Adicionar arquivos `customheaderlibs.html` e `customfooterlibs.html`.

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

   O `customfooterlibs.html` é usado para o JavaScript e o `customheaderlibs.html` para o CSS.

1. [Execute o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as alterações.

+++

### Adicionar um formulário adaptável existente à página do AEM Sites {#embed-existing-af}

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes, arraste e solte o componente [!UICONTROL Forms adaptável - Incorporar] na página.
1. Selecione o componente [!UICONTROL Forms Adaptável - Incorporar] na página Sites e selecione ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) na barra de ações. A caixa de diálogo **[!UICONTROL Editar Forms Adaptável - Incorporar]** é aberta.
1. Procure e selecione o Formulário adaptável a ser incorporado no [!UICONTROL Caminho do ativo].
1. Salve as configurações. O Formulário adaptável agora está incorporado na página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Criar e adicionar novo formulário adaptável à página do AEM Sites {#embed-new-af}

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes, arraste e solte o componente [!UICONTROL Forms adaptável - Incorporado(v2)] na página.
1. Clique no ícone **Plus** e você será redirecionado para o assistente de criação de formulários.

   ![Forms Adaptável - Componente de Incorporação](/help/forms/assets/aemformcontainer.png)

1. Crie um novo Formulário adaptável a partir do assistente de [!UICONTROL Criação de Formulário].
1. O [!UICONTROL Caminho do ativo] já inclui o caminho de um Formulário adaptável criado
1. Salve as configurações. O Formulário adaptável agora está incorporado na página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Configurar o formulário adaptável - Propriedades Embed(v2) {#configure-adaptive-form-embed}

Você pode personalizar as configurações avançadas do componente [!UICONTROL Formulário adaptável - Incorporado(v2)]. Na caixa de diálogo [!UICONTROL Editar Forms Adaptável - Incorporado(v2)], você pode especificar o seguinte.

* **Caminho do ativo**: procure e selecione o Formulário adaptável a ser incorporado. Ela será preenchida automaticamente se você soltá-la no navegador Assets.
* **Envio de Post** : selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.
   * **Mostrar Mensagem de Agradecimento**: escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
   * **Mostrar página de agradecimento**: procure e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
   * **Redirecionar para a página de agradecimento**: habilite a opção para substituir a página que contém o Formulário adaptável inserido pela página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável no componente [!UICONTROL Forms adaptável - Incorporado], sem atualizar os sites subjacentes na página. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
* **Usar Idioma da Página**: Use o local da página do AEM Sites em vez da localidade do Formulário Adaptável.
* **Definir Foco no Formulário**: selecione para definir o foco no primeiro campo do Formulário adaptável.
* **Formulário abrange toda a largura do quadro**: se marcado, o iframe não será usado para renderizar o formulário.
* **Altura**: especifique a altura do container. Deixe em branco para redimensionar automaticamente o contêiner.
* **Biblioteca do cliente CSS**: especifique o caminho para uma biblioteca do cliente CSS.

### O Publish adicionou o Forms adaptável usando o componente Formulário adaptável - Incorporado(v2)  {#publish-embedded-adaptive-form}

Considere os seguintes cenários para a publicação de Forms adaptável adicionado usando o componente **[!UICONTROL Formulário adaptável - Incorporado(v2)]**:

* Ao publicar uma página do AEM Sites pela primeira vez, os formulários adicionados à página Sites são publicados automaticamente.
* Ao modificar um Formulário adaptável adicionado a uma página do Sites já publicada, publique manualmente o Forms adaptável correspondente.
* Ao modificar uma página do Sites e a Forms adaptável correspondente, republique a página Sites e todas as Forms adaptáveis adicionadas à página Sites.

### Modificar o Forms adaptável adicionado usando o componente Formulário adaptável - Incorporado (v2)  {#modifying-embedded-adaptive-form}

Para modificar qualquer configuração ou propriedade de um Formulário adaptável, siga um destes procedimentos:

* Abra o formulário original em um Formulário adaptável no respectivo editor e modifique-o.
* Selecione o Formulário adaptável na página do site no modo de edição e selecione **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que você pode modificar.

## Alterar layout de um formulário adaptável adicionado a uma página do AEM Sites {#change-layout-af-aem-sites-page}

Na página do AEM Sites, o [modo de Layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) permite que você redimensione um Formulário adaptável que é criado ou adicionado a uma página do AEM Sites.

![Suporte a layout AF](/help/forms/assets/afsite-layoutsupport.gif)

A página de sites AEM mantém uma referência ao Formulário adaptável. Quando você traduz uma página do AEM Sites, ele traduz automaticamente um Formulário adaptável e seus ativos referenciados associados usando os [projetos de tradução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) para outros idiomas.

## Práticas recomendadas {#best-practices}

* O cabeçalho e o rodapé no formulário original não estão incluídos no formulário incorporado.
* Os rascunhos e envios de formulários incorporados pelo usuário são suportados e ficam visíveis nas guias Rascunhos e Forms enviados no Portal do Forms.

>[!MORELIKETHIS]
>
>* [Incorporar formulário adaptável baseado em componentes principais a uma página da Web externa](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
>* [Incorporar formulário adaptável na página da Web externa](/help/forms/embed-adaptive-form-external-web-page.md)