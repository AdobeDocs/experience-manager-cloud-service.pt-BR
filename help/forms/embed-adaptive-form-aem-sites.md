---
title: Como adicionar um formulário adaptável a uma página do AEM Sites?
description: Incorpore facilmente o Adaptive Forms em uma página do AEM Sites ou em uma página da Web hospedada fora do AEM.
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '3145'
ht-degree: 0%

---

# Incorporar um formulário adaptável à página de sites do AEM {#embed-an-adaptive-form-to-aem-sites-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | Este artigo |


## Visão geral {#overview}

O AEM Forms permite que os desenvolvedores de formulários incorporem facilmente o Adaptive Forms em uma página do AEM Sites AEM ou em uma página da Web hospedada fora do. O Formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário. Isso permite que seus usuários preencham e enviem formulários de maneira conveniente sem nunca sair da página em que estão. Essa integração oferece uma maneira conveniente de reutilizar o Adaptive Forms que eles já criaram.

Você pode usar o Editor de páginas AEM para incorporar rapidamente vários formulários às suas páginas do AEM Sites. Usar o Editor de páginas AEM permite que os autores de conteúdo criem experiências de captura de dados perfeitas em uma página do Sites, usando o potencial dos componentes do Forms adaptáveis, incluindo comportamento dinâmico, validações, integração de dados e geração de documentos de registro e automação de processos comerciais. Ele também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

AEM Forms fornece **[!UICONTROL Contêiner de formulário adaptável]** e **[!UICONTROL Forms adaptável - incorporado(v2)]** componentes. Você pode usar **[!UICONTROL Forms adaptável - incorporado(v2)]** para adicionar um formulário adaptável existente ou criar um formulário usando o Editor Forms adaptável , enquanto **[!UICONTROL Contêiner de formulário adaptável]** para criar um novo formulário em um Fragmento de experiência ou página do AEM Sites.

![Um exemplo de um formulário adaptável em uma página do AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integration-adobe-target-ims.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## Como criar ou incorporar um Formulário adaptável na página do AEM Sites ou no Fragmento de experiência do AEM? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Você pode aproveitar esse recurso usando as seguintes opções:

* **[Criar um formulário adaptável usando modelos aprovados e incorporá-lo a uma página do AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites):** Você pode usar modelos pré-aprovados para criar e incorporar rapidamente o Adaptive Forms que se alinham às diretrizes de marca e padrões de design de sua organização.

* **[Incorporar formulários existentes a uma página do AEM Sites](#embed-an-adaptive-form-in-sites-editor):** É possível integrar facilmente formulários já criados em seus sites, permitindo que os visitantes interajam diretamente com eles.

* **[Converter um formulário adaptável incorporado em fragmento de experiência](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Converta um formulário adaptável incorporado adicionado a uma página do AEM Sites em um Fragmento de experiência para reutilizar o formulário em várias páginas do AEM Sites.

* **[Criar e adicionar um formulário adaptável personalizado a uma página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Você pode usar o **[!UICONTROL Contêiner de formulário adaptável]** para criar um formulário totalmente novo do zero, adaptando-o especificamente às suas necessidades e preferências de design.

* **[Criar e adicionar um formulário adaptável personalizado a Fragmentos de experiência](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** Você pode estender o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites.

* **Adicionar vários formulários a uma página do AEM Sites ou Fragmento de experiência:**  Você pode criar ou adicionar várias Forms adaptáveis a uma página do AEM Sites para fornecer várias opções aos usuários com base em suas preferências e requisitos. Você pode usar o Editor de páginas AEM para incorporar rapidamente vários formulários às suas páginas do AEM Sites. Você pode usar o **[!UICONTROL Contêiner de formulário adaptável]** várias vezes para adicionar o Adaptive Forms em uma página do AEM Sites. Você pode usar o **[!UICONTROL Forms adaptável - Incorporado]** várias vezes em uma página do AEM Sites, somente se **[!UICONTROL O formulário cobre toda a largura do quadro]** for selecionada. Caso a variável **[!UICONTROL O formulário cobre toda a largura do quadro]** não estiver marcada, a página AEM Sites oferecerá suporte a apenas um Formulário adaptável para existir sem um iframe. Para adicionar mais Forms adaptável usando o **[!UICONTROL Forms adaptável - Incorporado]** componente, selecione **[!UICONTROL O formulário cobre toda a largura do quadro]** opção.

## Considerações para incorporar um formulário adaptável na página do AEM Sites ou no Fragmento de experiência do AEM {#consideration}

* Ao criar ou adicionar um formulário usando a variável **[!UICONTROL Forms adaptável - incorporado(v2)]** , os formulários são traduzidos e localizados usando o fluxo de tradução do AEM Forms. Nesse caso, um único formulário é mantido e referenciado em todas as cópias de idioma das páginas do Sites. **[!UICONTROL Forms adaptável - incorporado(v2)]** O componente não fornece acesso a vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

* Quando você usa o **[!UICONTROL Contêiner de formulário adaptável]** para criar um formulário, os formulários são submetidos a tradução e localização por meio do fluxo de tradução do AEM Sites. Para cada idioma, uma cópia separada (cópia de idioma) da página de sites e os formulários correspondentes são gerados e, quando um autor de conteúdo modifica uma regra em um formulário na página principal, as mesmas alterações devem ser feitas em todas as cópias de idioma do formulário. **[!UICONTROL Contêiner de formulário adaptável]** O também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.


## Requisitos para incorporar um formulário adaptável na página do AEM Sites ou no fragmento de experiência do AEM {#before-you-start-embedding-an-adaptive-form}

Antes de começar a incorporar um novo Formulário adaptável ou um Formulário adaptável pré-existente usando **[!UICONTROL Forms adaptável - incorporado(v2)]**, ativar **Componentes principais adaptáveis do Forms** e adicionar **Bibliotecas de clientes do Forms adaptáveis** para sua página do AEM Sites:

+++  Ativar os Componentes principais adaptáveis do Forms para o ambiente do AEM Cloud Service

Certifique-se de que o [Os Componentes principais adaptáveis do Forms são ativados para o ambiente as a Cloud Service do AEM Forms](enable-adaptive-forms-core-components.md).

+++

+++  Adicionar bibliotecas de clientes do Forms adaptáveis à sua página do AEM Sites ou Fragmento de experiência

Quando a variável **[!UICONTROL Quando o formulário cobre toda a largura de uma página]** estiver selecionada na caixa **[!UICONTROL Contêineres de formulário]** Quando forem usadas a caixa de diálogo de configuração e o Adaptive Forms usando os Componentes principais, será necessário incluir as bibliotecas de clientes na página do site correspondente.

![Quando o formulário cobre toda a largura de uma página, a opção é selecionada e o formulário adaptável com os componentes principais é usado](/help/forms/assets/overlaycorecomponent.gif)


Adicione o **Customheaderlibs** e **Customfooterlibs** bibliotecas de clientes à sua página do AEM Sites usando o pipeline de implantação. Para adicionar as bibliotecas de clientes:

1. Acesse e clone seu [Repositório Git do AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Abra a pasta Repositório Git da AEM Cloud Service em um editor de texto de plano. Por exemplo, Microsoft® Visual Code.
1. Abra o `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` e adicione o seguinte código ao arquivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Abra o `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` e adicione o seguinte código ao arquivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Abra o `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` e adicione o seguinte código ao arquivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Abra o `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` e adicione o seguinte código ao arquivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [Executar o pipeline de implantação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as bibliotecas de clientes no ambiente as a Cloud Service AEM.

+++

+++ Ativar **[!UICONTROL Forms adaptável - incorporado(v2)]** para sua página do AEM Sites ou Fragmento de experiência

Para habilitar **[!UICONTROL Forms adaptável - incorporado(v2)]** componente na política do modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites ou o Fragmento de experiência para edição. Para abrir a página para edição, selecione a página e clique em **[!UICONTROL Editar]**.
1. Abra o modelo da página Sites ou Fragmento de experiência. Para abrir o template, vá para a **[!UICONTROL Informações da página]** ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Editar modelo]**. Ele abre o modelo correspondente no editor de modelo.
1. Na visualização Estrutura, clique no botão **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) ícone na barra de menus. No **[!UICONTROL Componentes permitidos]** e selecione o **[!UICONTROL Forms adaptável - incorporado(v2)]**  na caixa de seleção **[Nome do projeto do arquétipo AEM] - Formulário adaptável**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

## Incorporar um formulário adaptável usando o componente Forms - Embed(v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Use o **[!UICONTROL Forms adaptável - incorporado(v2)]** para criar um Formulário adaptável diretamente no editor do AEM Sites usando o assistente de Criação de formulários. O formulário resultante é salvo como uma entidade externa, permitindo sua reutilização em outras páginas do Sites e formulários independentes. Você pode incorporar um formulário totalmente novo do zero, adaptando-o especificamente às suas necessidades e preferências de design, diretamente em uma página do AEM Sites ou em um Fragmento de experiência. Para formulários de uso único, recomenda-se a criação direta em uma página do AEM Sites, enquanto os Fragmentos de experiência são ideais para formulários que devem ser reutilizados em várias páginas do site.

É possível incorporar facilmente um novo formulário usando **[!UICONTROL Forms adaptável - incorporado(v2)]**.  Por exemplo, imagine incorporar um novo formulário entre em contato conosco em uma página do AEM Sites ou em um Fragmento de experiência de AEM. Quaisquer atualizações ou modificações feitas no formulário de contato na página do AEM Sites ou no Fragmento de experiência se aplicam automaticamente a todas as páginas em que é implantado. Isso simplifica o gerenciamento dos formulários do seu site, garantindo uma experiência perfeita para o usuário e simplificando o processo geral.

Usar **[!UICONTROL Forms adaptável - incorporado(v2)]**, você pode:

* [Incorporar novo formulário usando o Assistente de Forms adaptável na página AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Incorporar novo formulário usando o Assistente do Forms adaptável em um fragmento de experiência](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Incorporar um formulário adaptável existente em uma página do AEM Sites](#embed-an-adaptive-form-in-sites-editor)
* [Incorporar um formulário existente em um Fragmento de experiência](#embed-an-adaptive-form-in-experience-fragment)
* [Converter um formulário adaptável na página AEM Sites em um fragmento de experiência](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Incorporar novo formulário usando o Assistente de Forms adaptável na página AEM Sites {#embed-form-using-adaptive-form-wizzard-aem-sites}

As etapas para incorporar o novo formulário a uma página do AEM Sites são:

1. Abra a página do AEM Sites no modo de edição.
1. No painel Navegador de componentes, arraste e solte a **[!UICONTROL Forms adaptável - incorporado(v2)]** componente na página.
1. Clique em **Plus** e você será redirecionado para o assistente de criação de formulários.

   ![Forms adaptável - Componente de incorporação](/help/forms/assets/aemformcontainer.png)

1. Crie um novo Formulário adaptável a partir do **[!UICONTROL Criação do formulário]** assistente.
A variável **[!UICONTROL Caminho do ativo]** já inclui o caminho de um Formulário adaptável criado
1. Salve as configurações. O Formulário adaptável agora está incorporado na página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

Em seguida, é possível [definir a ação enviar](/help/forms/configuring-submit-actions.md) e avançadas de um Formulário adaptável incorporado usando o Assistente de criação de Formulário.


### Incorporar novo formulário usando o Assistente do Forms adaptável em um fragmento de experiência {#embed-form-using-adaptive-form-wizzard-experience-fragment}

As etapas para incorporar um novo formulário a um Fragmento de experiência são:

1. Abra o Fragmento de experiência no modo de edição.
1. No painel Navegador de componentes, arraste e solte a **[!UICONTROL Forms adaptável - incorporado(v2)]** componente na página.
1. Clique em **Plus** e você será redirecionado para o assistente de criação de formulários.

   ![Forms adaptável - Componente de incorporação](/help/forms/assets/aemformcontainer.png)

1. Crie um novo Formulário adaptável a partir do **[!UICONTROL Criação do formulário]** assistente.
A variável **[!UICONTROL Caminho do ativo]** já inclui o caminho de um Formulário adaptável criado
1. Salve as configurações. O Formulário adaptável agora está incorporado no Fragmento de experiência.

Em seguida, é possível [definir a ação enviar](/help/forms/configuring-submit-actions.md) e avançadas de um Formulário adaptável incorporado usando o Assistente de criação de Formulário.

### Incorporar um formulário adaptável existente em uma página do AEM Sites {#embed-an-adaptive-form-in-sites-editor}

Com o **[!UICONTROL Forms adaptável - incorporado(v2)]** , você pode integrar facilmente um Formulário adaptável pré-existente em uma página no AEM Sites. Esse recurso melhora significativamente a adaptabilidade e a reutilização do Adaptive Forms, oferecendo aos clientes uma maneira conveniente de reutilizar formulários já criados. Por exemplo, imagine incorporar um formulário de contato a uma página do AEM Sites, eliminando a necessidade de recriar o formulário várias vezes.

Para incorporar um formulário adaptável existente em uma página do Sites:

1. Abra a página do AEM Sites no modo de edição.
1. Arraste e solte a variável **[!UICONTROL Forms adaptável - incorporado(v2)]** componente do Navegador de componentes para a página Sites.
1. Selecione o **[!UICONTROL Forms adaptável - Incorporado]** componente na página Sites e selecione ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) na barra de ações. A variável **[!UICONTROL Editar Forms adaptável - incorporado(v2)]** será aberta.
1. Procure e selecione o Formulário adaptável a ser incorporado no **[!UICONTROL Caminho do ativo]**.
1. Salve as configurações. O Formulário adaptável agora está incorporado na página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

Em seguida, é possível [definir a ação enviar](/help/forms/configuring-submit-actions.md) e avançadas de um Formulário adaptável incorporado usando o Assistente de criação de Formulário.

### Incorporar um formulário adaptável existente em um fragmento de experiência {#embed-an-adaptive-form-in-experience-fragment}

Você também pode estender a acessibilidade de seus formulários incorporando-os ao Fragmento de experiência do AEM. Para incorporar um formulário adaptável em um fragmento de experiência:

1. Abra um Fragmento de experiência no modo de edição.
1. Arraste e solte a variável **[!UICONTROL Forms adaptável - incorporado(v2)]** componente do Navegador de componentes para o Fragmento de experiência.
1. Selecione o **[!UICONTROL Forms adaptável - Incorporado]** no Fragmento de experiência e selecione ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) na barra de ações. A variável **[!UICONTROL Editar Forms adaptável - incorporado(v2)]** será aberta.
1. Procure e selecione o Formulário adaptável a ser incorporado no **[!UICONTROL Caminho do ativo]**.
1. Salve as configurações. O Formulário adaptável agora está incorporado ao Fragmento de experiência.

Em seguida, é possível [definir a ação enviar](/help/forms/configuring-submit-actions.md) e avançadas de um Formulário adaptável incorporado usando o Assistente de criação de Formulário.

### Converter um formulário na página do AEM Sites em um Fragmento de experiência {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Você pode converter um formulário adaptável existente em um Editor de páginas de sites em um Fragmento de experiência para reutilizar o formulário em várias páginas ou sites.

Para converter um formulário adaptável na página AEM Sites em um fragmento de experiência:

1. Abra a página do AEM Sites que contém o formulário adaptável (no componente Contêiner adaptável do Forms) no modo de edição.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Na barra de menus, selecione a opção ![Ícone Converter para variação de fragmento de experiência](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Ícone Converter para variação de Fragmento de experiência.

   ![Clique no logotipo do gabinete de arquivo para converter um formulário adaptável na página AEM Sites em um fragmento de experiência](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Uma caixa de diálogo para converter o contêiner do Formulário adaptável em um novo Fragmento de experiência ou adicionar a um Fragmento de experiência existente é exibida.

1. No **[!UICONTROL Converter em fragmento de experiência]** variação, defina valores para as seguintes opções:

   * **Ação:** Selecione para criar um fragmento de experiência ou Adicionar a um fragmento de experiência existente.
   * **Caminho principal:** Especifique o caminho da pasta na qual hospedar o fragmento de experiência. A opção está disponível somente para criar um novo Fragmento de experiência.
   * **Modelo:** Especifique o caminho do modelo do Fragmento de experiência. Se você não tiver um modelo de Fragmento de experiência, [criar](/help/implementing/developing/extending/experience-fragments.md). A opção está disponível somente para adicionar o Formulário adaptável a um Fragmento de experiência existente.
   * **Título do fragmento:** Especifique o título do Fragmento de experiência. O título identifica exclusivamente um Fragmento de experiência.
   * **Tags de fragmento:** Especifique a tag do Fragmento de experiência. A tag identifica exclusivamente a categoria de um Fragmento de experiência.

## Configurar as propriedades de incorporação do formulário adaptável (v2)

É possível personalizar as configurações avançadas do **[!UICONTROL Formulário adaptável - Embed(v2)]** componente. No **[!UICONTROL Editar Forms adaptável - Incorporado]** poderá especificar o seguinte:

* **Caminho do ativo**: Procure e selecione um Formulário adaptável para incorporar. Ela será preenchida automaticamente se você soltá-la no navegador de ativos.
* **Envio de publicação** : selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.
   * **Mostrar mensagem de agradecimento**: escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
   * **Mostrar página de agradecimento**: navegue e selecione a página que será exibida no envio do formulário. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
   * **Redirecionar para a página de agradecimento**: habilite a opção para substituir a página que contém o Formulário adaptável incorporado pela página de agradecimento. Caso contrário, a página de agradecimento substituirá o Formulário adaptável na **[!UICONTROL Forms adaptável - incorporado(v2)]** sem atualizar os sites subjacentes na página. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
   * **Mensagem de agradecimento**: Confirmação ou confirmação breve que é exibida na tela após o envio bem-sucedido de um formulário.
   * **Página de agradecimento**: procure e selecione a página que será exibida após enviar um formulário com êxito.

* **Usar idioma da página**: Use o local da página do AEM Sites em vez do local do Formulário adaptável. Essa opção só é aplicável para o Formulário adaptável (Foundation).
* **Definir Foco no formulário**: selecione para definir o foco no primeiro campo do Formulário adaptável. Essa opção só é aplicável para o Formulário adaptável (Foundation).
* **Tema**: selecione um tema que defina o estilo dos componentes do seu Formulário adaptável. O estilo inclui propriedades de aparência, como estilo da fonte, cor do plano de fundo, dimensões e alinhamento. Essa opção só é aplicável para o Formulário adaptável (Foundation).

  >[!NOTE]
  >
  > Você pode usar o **Usar idioma da página**, **Definir Foco no formulário** e **Tema** opções somente para Formulário adaptável (Foundation).

* **O formulário cobre toda a largura do quadro**: um quadro em linha (iframe) é um elemento de HTML que carrega um formulário adaptável para uma página do AEM Sites.

   * Se a variável **[!UICONTROL O formulário cobre toda a largura do quadro]** estiver marcada, um Formulário adaptável ocupará toda a largura do container no qual ele é colocado. Nesse caso, um iframe não é usado para renderizar o formulário. O layout e o design de um Formulário adaptável se adaptam para abranger toda a largura do contêiner, tornando-o responsivo e capaz de se ajustar a diferentes tamanhos de tela. Essa opção permite incorporar vários Forms adaptáveis em uma página do AEM Sites.

     >[!NOTE]
     >
     > Para incorporar vários formulários em uma página do AEM Sites, selecione **[!UICONTROL O formulário cobre toda a largura do quadro]** caixa de seleção

   * Se a variável **[!UICONTROL O formulário cobre toda a largura do quadro]** não estiver marcada, um formulário adaptável não cobrirá toda a largura do contêiner. Em vez disso, um iframe é usado para renderizar o formulário, que não pode ser estendido além de uma largura específica. Essa abordagem é útil quando um Formulário adaptável tem limites definidos e deve coexistir com outros componentes AEM ao lado dele no contêiner. Se essa opção não estiver marcada, permitirá que apenas uma Forms adaptável na página do AEM Sites seja incorporada sem um iframe.

     >[!NOTE]
     >
     > A página do AEM Sites oferece suporte a apenas um Formulário adaptável para existir sem um iframe. Para adicionar mais Forms adaptável usando o **[!UICONTROL Forms adaptável - Incorporado]** componente, selecione **[!UICONTROL O formulário cobre toda a largura do quadro]** opção.

* **Altura**: especifique a altura do container. Deixe em branco para redimensionar automaticamente o contêiner.
* **Biblioteca cliente CSS**: especifique o caminho para uma biblioteca de cliente CSS.

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## Publicar formulário adaptável incorporado {#publishing-embedded-adaptive-form}

Considere os seguintes cenários para a publicação de um Formulário adaptável incorporado na página de sites AEM:

* Se você estiver publicando a página de sites do AEM pela primeira vez e ela incluir um Formulário adaptável incorporado, publique a página de sites e o ativo incorporado.
* Se você modificou somente o Formulário adaptável incorporado em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicada. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o Formulário adaptável incorporado, republique a página de sites e o ativo incorporado.

## Modificar formulário adaptável incorporado  {#modifying-embedded-adaptive-form}

Para modificar qualquer configuração ou propriedade do Formulário adaptável incorporado, execute um dos procedimentos a seguir.

* Abra o formulário original em um Formulário adaptável no respectivo editor e modifique-o.
* Selecione o formulário adaptável na página do site no modo de edição e selecione **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que você pode modificar.

>[!NOTE]
>
>As alterações feitas no Formulário adaptável original são refletidas automaticamente no formulário inserido. No entanto, publique novamente o Formulário adaptável ou a página do site para refletir as alterações na página publicada.

## Práticas recomendadas {#best-practices}

Lembre-se dos seguintes pontos ao incorporar o Adaptive Forms nas páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não estão incluídos no formulário incorporado.
* Os rascunhos e envios de formulários incorporados pelo usuário são suportados e ficam visíveis nas guias Rascunhos e Forms enviados no Portal do Forms.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.

## Consulte também {#see-also}

* [Criar Forms adaptável independente baseado em Componente principal](/help/forms/creating-adaptive-form-core-components.md)
* [Criar componente principal baseado no Formulário adaptável diretamente em uma página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
