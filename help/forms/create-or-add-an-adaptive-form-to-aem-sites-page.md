---
title: Como adicionar um formulário adaptável à página do AEM Sites?
description: Descubra como criar ou adicionar um Formulário adaptável à sua página do AEM Sites. Conheça também os benefícios e várias maneiras de integrar formulários ao seu site.
feature: Adaptive Forms, Page Editor, Authoring
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
source-git-commit: a1b63508ed7040c719778bd1c422728bc0e2e4f2
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 1%

---

# Adição de um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |
| AEM as a Cloud Service | Este artigo |

## Visão geral {#overview}

Com o AEM Forms, você pode adicionar um formulário facilmente à sua página do AEM Sites. Isso permite que seus visitantes preencham e enviem formulários de maneira conveniente sem nunca sair da página em que estão. Ao fazer isso, eles podem se envolver facilmente com outros elementos do site enquanto interagem ativamente com o formulário.

Você pode usar o Editor de páginas AEM para criar e adicionar rapidamente vários formulários às suas páginas do AEM Sites. Usar o Editor de páginas AEM permite que os autores de conteúdo criem experiências de captura de dados perfeitas em uma página do Sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos comerciais. Ele também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

O Cloud Service AEM Forms fornece Contêiner de formulário adaptável e Forms adaptável - Componentes incorporados. Você pode usar o Contêiner de formulário adaptável para criar um novo formulário em uma página do AEM Sites ou Fragmento de experiência, enquanto o componente Adaptive Forms - Incorporar permite adicionar um formulário adaptável existente ou criar um novo formulário usando o Editor Adaptive Forms.

![Um exemplo de um formulário adaptável em uma página do AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

## Por que usar os Componentes principais do Adaptive Forms para criar um Formulário adaptável na página do AEM Sites ou no Fragmento de experiência?

Se você já tiver criado o componente Adaptive Forms Foundation ou formulários baseados em HTML simples para seus Sites, o Adobe recomenda usar os Componentes principais do Adaptive Forms para criar um Formulário adaptável na página do AEM Sites ou Fragmento de experiência. Ele permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites, aprimorando a experiência geral de criação e gerenciamento de formulários para o Adaptive Forms. Vamos explorar alguns destes recursos:

* **Controle de versão:** Oferta de páginas do AEM Sites [recursos robustos de controle de versão](/help/sites-cloud/authoring/features/page-versions.md), permitindo rastrear e gerenciar diferentes versões dos formulários. Isso permite fazer alterações e aprimoramentos nos formulários, mantendo a capacidade de reverter para versões anteriores, se necessário. O controle de versão garante uma abordagem controlada e organizada para o desenvolvimento e evolução da forma.
* **Direcionamento (integração com o Adobe Target):** Com os recursos de direcionamento de páginas do AEM Sites, você também pode [personalizar a experiência do formulário para públicos diferentes](/help/sites-cloud/integrating/integration-adobe-target-ims.md). Ao utilizar segmentos de usuários e critérios de direcionamento, você pode adaptar o conteúdo, o design ou o comportamento do formulário a grupos específicos de usuários. Isso permite fornecer uma experiência de formulário personalizada e relevante, aumentando as taxas de engajamento e conversão.
* **Tradução:** AEM Sites [integração perfeita com serviços de tradução](/help/sites-cloud/administering/translation/overview.md), permitindo que você traduza formulários em vários idiomas facilmente. Esse recurso simplifica o processo de localização, garantindo que seus formulários estejam acessíveis para um público-alvo global. Você pode gerenciar traduções com eficiência em projetos de tradução AEM, reduzindo o tempo e o esforço necessários para o suporte a formulários multilíngues. Consulte a seção considerações para obter mais informações sobre tradução.
* **Gerenciamento de vários sites e Live Copy:** O AEM Sites oferece [Recursos de gerenciamento de vários sites e Live Copy](/help/sites-cloud/administering/msm/overview.md), permitindo criar e gerenciar vários sites em um único ambiente. Esse recurso agora permite reutilizar formulários em sites diferentes, garantindo a consistência e reduzindo os esforços de duplicação. Com controle e gerenciamento centralizados, você pode manter e atualizar formulários de maneira eficiente em vários sites.
* **Temas:** As páginas do AEM Sites fornecem uma estrutura para projetar e manter estilos visuais consistentes em várias páginas da Web. Eles definem cores, fontes, folhas de estilos e outros elementos visuais que contribuem para a aparência geral do site. [Você pode usar os temas criados para uma página do AEM Sites para um Formulário adaptável, economizando tempo e esforço](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Marcação:** As páginas do AEM Sites permitem [atribuir tags ou rótulos a uma página, um ativo ou outro conteúdo](/help/implementing/developing/introduction/tagging-framework.md). Tags são rótulos de palavras-chave ou metadados que fornecem uma maneira de categorizar e organizar o conteúdo com base em critérios específicos. É possível atribuir uma ou mais tags a páginas, ativos ou qualquer outro conteúdo no AEM para melhorar a pesquisa e a categorização dos ativos.
* **Bloquear e desbloquear conteúdo:** O AEM Sites permite que os usuários [controlar o acesso e as modificações nas páginas](/help/sites-cloud/authoring/fundamentals/editing-content.md) no ambiente do AEM Sites. Quando uma página é bloqueada, significa que ela está protegida contra alterações ou edições não autorizadas por outros usuários. Somente o usuário que bloqueou o conteúdo ou um administrador designado pode desbloqueá-lo para permitir modificações.

Além disso, o Forms adaptável no Editor de páginas AEM usa [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features). Esses Componentes principais fornecem métodos padrão e mais fáceis para estilizar e personalizar os componentes, idênticos a [Componentes WCM do AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR).


## Como criar ou adicionar um formulário adaptável na página do AEM Sites ou no Fragmento de experiência do AEM? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Você pode aproveitar ao máximo esse recurso utilizando as seguintes opções:

* **[Criar e adicionar um formulário adaptável personalizado a uma página do AEM Sites](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Você pode usar o componente de Contêiner de formulário adaptável para criar um formulário totalmente novo do zero, adaptando-o especificamente às suas necessidades e preferências de design.

* **[Criar e adicionar um formulário adaptável personalizado a Fragmentos de experiência](#create-an-adaptive-form-in-sites-editor):** Você pode estender o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites.

* **[Converter um formulário adaptável em fragmento de experiência](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Converta um formulário adaptável adicionado a uma página do AEM Sites em um Fragmento de experiência para reutilizar o formulário em várias páginas do AEM Sites.

* **[Criar e adicionar formulários com base em modelos aprovados a uma página do AEM Sites:](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)** Você pode aproveitar os modelos pré-aprovados para criar rapidamente o Forms adaptável que se alinha às diretrizes de marca e aos padrões de design de sua organização. A opção está disponível somente para o Forms adaptável criado com o Editor Forms adaptável ou o componente Forms adaptável - Incorporar.

* **[Adicionar formulários existentes a uma página do AEM Sites:](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)** É possível integrar facilmente formulários já criados em seus sites, permitindo que os visitantes interajam diretamente com eles. A opção está disponível somente para o Forms adaptável criado com o Editor Forms adaptável ou o componente Forms adaptável - Incorporar.


* **Adicionar vários formulários a uma página do AEM Sites ou Fragmento de experiência:**  Você pode criar ou adicionar várias Forms adaptáveis a uma página do AEM Sites para fornecer várias opções aos usuários com base em suas preferências e requisitos. Eles podem combinar formulários totalmente novos do zero com formulários existentes. Você pode usar o **[!UICONTROL Contêiner de formulário adaptável]** várias vezes para adicionar o Adaptive Forms em uma página do AEM Sites. Você pode usar o **[!UICONTROL Forms adaptável - Incorporado]** várias vezes em uma página do AEM Sites, somente se **[!UICONTROL O formulário cobre toda a largura do quadro]** for selecionada. Caso a variável **[!UICONTROL O formulário cobre toda a largura do quadro]** não estiver marcada, a página AEM Sites oferecerá suporte a apenas um Formulário adaptável para existir sem um iframe. Para adicionar mais Forms adaptável usando o **[!UICONTROL Forms adaptável - Incorporado]** componente, selecione **[!UICONTROL O formulário cobre toda a largura do quadro]** opção.

## Considerações para criar um formulário adaptável na página do AEM Sites ou no fragmento de experiência do AEM {#consideration}

* Quando você usa o Contêiner de formulário adaptável para criar ou adicionar um formulário, os formulários são submetidos a tradução e localização por meio do fluxo de tradução do AEM Sites. Para cada idioma, uma cópia separada (cópia de idioma) da página de sites e os formulários correspondentes são gerados e, quando um autor de conteúdo modifica uma regra em um formulário na página principal, as mesmas alterações devem ser feitas em todas as cópias de idioma do formulário. O Contêiner de formulário adaptável também permite usar vários recursos das páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

* Ao criar ou adicionar um formulário usando o componente de incorporação do formulário adaptável, os formulários são submetidos a tradução e localização usando o fluxo de tradução do AEM Forms. Nesse caso, um único formulário é mantido e referenciado em todas as cópias de idioma das páginas do Sites. O componente de Formulário incorporado adaptável não fornece acesso a vários recursos de páginas do AEM Sites, como o, controle de versão, direcionamento, tradução e gerenciador de vários sites.


## Requisitos para criar ou adicionar um formulário adaptável na página do AEM Sites ou no fragmento de experiência do AEM {#before-you-start-creating-an-adaptive-form}

Antes de começar a criar ou um formulário adaptável, ative os Componentes principais do Forms adaptável e adicione as bibliotecas de clientes do Forms adaptáveis à sua página do AEM Sites:

+++  Ativar os Componentes principais adaptáveis do Forms para o ambiente do AEM Cloud Service

Certifique-se de que o [Os Componentes principais adaptáveis do Forms são ativados para o ambiente as a Cloud Service do AEM Forms](enable-adaptive-forms-core-components.md).

+++

+++  Adicionar bibliotecas de clientes do Forms adaptáveis à sua página do AEM Sites ou Fragmento de experiência

Para ativar a funcionalidade completa do componente de Contêiner adaptável do Forms, adicione as bibliotecas de clientes Customheaderlibs e Customfooterlibs à sua página do AEM Sites usando o pipeline de implantação. Para adicionar as bibliotecas:

1. Acesse e clone seu [Repositório Git do AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Abra a pasta Repositório Git da AEM Cloud Service em um editor de texto de plano. Por exemplo, Microsoft Visual Code.
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

+++ Ativar o contêiner adaptável do Forms para sua página do AEM Sites ou fragmento de experiência

Para habilitar [!UICONTROL Contêiner adaptável do Forms] componente na política do modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites ou o Fragmento de experiência para edição. Para abrir a página para edição, selecione a página e clique em Editar.
1. Abra o modelo da página Sites ou Fragmento de experiência. Para abrir o template, vá para a [!UICONTROL Informações da página] ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar modelo]. Ele abre o modelo correspondente no editor de modelo.
1. Na visualização Estrutura, clique no botão **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) ícone na barra de menus. No **[!UICONTROL Componentes permitidos]** e selecione o **[!UICONTROL Contêiner adaptável do Forms]**  na caixa de seleção **[Nome do projeto do arquétipo AEM] - Formulário adaptável**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Criação de um Formulário adaptável {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Você pode criar um formulário totalmente novo do zero, ajustando-o especificamente às suas necessidades e preferências de design, diretamente em uma página do AEM Sites ou no Fragmento de experiência. Para formulários de uso único, recomenda-se a criação direta em uma página do AEM Sites, enquanto os Fragmentos de experiência são ideais para formulários que precisam ser reutilizados em várias páginas do site.

* [Criar um formulário em uma página do AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Criar um formulário em um Fragmento de experiência](#create-an-adaptive-form-in-experience-fragment)
* [Converter um formulário adaptável na página AEM Sites em um fragmento de experiência](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Criar um formulário em uma página do AEM Sites {#create-an-adaptive-form-in-sites-editor}

Você pode usar o componente de Contêiner de formulário adaptável no Editor de páginas AEM para criar um formulário personalizado. O componente permite criar um formulário arrastando e soltando os componentes do formulário. Os componentes de formulário são baseados nos Componentes principais. Você pode personalizá-los facilmente de acordo com os requisitos de sua organização.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para criar um Formulário adaptável em uma página do Sites:

1. Abra a página do AEM Sites no modo de edição.
1. Arraste e solte a variável **[!UICONTROL Contêiner adaptável do Forms]** componente do Navegador de componentes para a página Sites. Ele cria um espaço na página para o formulário. Você pode usar o modo de layout para alterar o Tamanho do espaço do container.
1. Arraste e solte os Componentes principais do formulário adaptável no espaço do contêiner para criar o formulário.
1. Adicione o botão Submit.

Em seguida, você [definir a ação enviar](#configure-submit-action-for-form) e propriedades avançadas.

### Criar um formulário em um Fragmento de experiência {#create-an-adaptive-form-in-experience-fragment}

Você pode estender o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites. Por exemplo, você pode incluir um formulário de inscrição de informativo em um Fragmento de experiência. Isso permite reutilizar convenientemente o fragmento em várias páginas do site, eliminando a necessidade de recriar o formulário repetidamente. Quaisquer atualizações ou modificações feitas no formulário de inscrição do boletim informativo no Fragmento de experiência são propagadas automaticamente para todas as páginas em que são utilizadas. Isso simplifica o processo e garante uma experiência perfeita para o usuário, simplificando o gerenciamento dos formulários de seu site.

Para criar um formulário adaptável em um fragmento de experiência:

1. Abra um Fragmento de experiência.
1. Arraste e solte a variável **[!UICONTROL Contêiner adaptável do Forms]** componente do Navegador de componentes para o Fragmento de experiência.
1. Arraste e solte os Componentes principais do formulário adaptável no espaço de contêiner no Fragmento de experiência para criar o formulário.
1. Adicione o botão Submit.

Em seguida, você [definir a ação enviar](#configure-submit-action-for-form) e propriedades avançadas.

### Converter um formulário na página do AEM Sites em um Fragmento de experiência {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Você pode converter um formulário adaptável existente em um Editor de páginas de sites em um Fragmento de experiência para reutilizar o formulário em várias páginas ou sites.

Para converter um formulário adaptável na página AEM Sites em um fragmento de experiência:

1. Abra a página do AEM Sites que contém o formulário adaptável (no componente Contêiner adaptável do Forms) no modo de edição.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Na barra de menus, selecione a opção ![Ícone Converter para fragmento de experiência](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Ícone Converter para variação de Fragmento de experiência.
   ![Clique no logotipo do gabinete de arquivo para converter um formulário adaptável na página AEM Sites em um fragmento de experiência](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Uma caixa de diálogo para converter o contêiner do Formulário adaptável em um novo Fragmento de experiência ou adicionar a um Fragmento de experiência existente é exibida
1. Na caixa de diálogo Converter em variação de Fragmento de experiência, defina valores para as seguintes opções:

   * **Ação:** Selecione para criar um novo fragmento de experiência ou Adicionar a um fragmento de experiência existente.
   * **Caminho principal:** Especifique o caminho da pasta na qual hospedar o fragmento de experiência. A opção está disponível somente para criar um novo Fragmento de experiência.
   * **Modelo:** Especifique o caminho do modelo do Fragmento de experiência. Se você não tiver um modelo de Fragmento de experiência, [criar](/help/implementing/developing/extending/experience-fragments.md). A opção está disponível somente para adicionar o Formulário adaptável a um Fragmento de experiência existente.
   * **Título do fragmento:** Especifique o título do Fragmento de experiência. O título identifica exclusivamente um Fragmento de experiência


## Configurar a ação enviar para um formulário na página do AEM Sites ou Fragmento de experiência {#configure-submit-action-for-form}

Uma ação enviar permite escolher o destino dos dados capturados por meio de um formulário adaptável. É acionado quando um usuário clica no botão Enviar em um Formulário adaptável. Os formulários adaptáveis incluem algumas ações de envio prontas para uso. Você também pode estender ações de envio padrão para criar sua própria ação de envio personalizada. Para configurar uma Ação de envio para o formulário:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar ações de envio é aberta.
   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar a ação enviar para um formulário adaptável](/help/forms/assets/adaptive-forms-container.png)
1. Selecione e configure uma ação Enviar, com base em seus requisitos. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de envio do formulário adaptável](/help/forms/configuring-submit-actions.md)


## Configurar um esquema ou modelo de dados de formulário para um formulário na página do AEM Sites ou Fragmento de experiência {#configure-schema-or-data-model-for-form}

Você pode usar o Modelo de dados de formulário para conectar um formulário a uma Fonte de dados para enviar e receber dados com base nas ações do usuário. Você também pode conectar um formulário a um esquema JSON para receber os dados enviados em um formato predefinido. Com base no requisito, conecte seu formulário a um esquema JSON ou modelo de dados de formulário:

* [Crie um esquema JSON e faça upload para o seu ambiente](/help/forms/adaptive-form-json-schema-form-model.md)  ou,
* [Criar um modelo de dados de formulário](/help/forms/create-form-data-models.md)

Para configurar um Esquema JSON ou um Modelo de dados de formulário para seu formulário:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Clique no ícone Chave inglesa para configurar modelos de dados para o formulário adaptável](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Selecione e configure um Esquema JSON ou Modelo de dados de formulário, com base em seus requisitos. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de envio do formulário adaptável](/help/forms/configuring-submit-actions.md).

   * Ao selecionar a variável **[!UICONTROL Modelo de formulário]** , use o **[!UICONTROL Selecionar modelo de dados do formulário]** opção para selecionar um modelo de dados de formulário pré-configurado.
   * Ao selecionar a variável **[!UICONTROL Esquema]** , use o **[!UICONTROL Esquema]** opção para selecionar um esquema JSON para o formulário.

1. Clique em **[!UICONTROL Concluído]**.

## Configurar um serviço de pré-preenchimento para um formulário na página do AEM Sites ou Fragmento de experiência {#configure-prefill-service-for-form}

Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. É possível:

* [Criar um serviço de preenchimento prévio personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Usar o serviço de preenchimento do modelo de dados de formulário](#fdm-prefill-service)

### Usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário na página do AEM Sites ou no fragmento de experiência {#fdm-prefill-service}

Você pode usar o serviço de Preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável na página do AEM Sites ou Fragmento de experiência usando um Modelo de dados de formulário ou um serviço de preenchimento prévio personalizado. O serviço de Preenchimento do modelo de dados de formulário usa o [Obter serviço do modelo de dados de formulário configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar dados. Para usar o serviço de Preenchimento de modelo de dados de formulário para um Formulário adaptável:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar o serviço de preenchimento prévio para o formulário adaptável](/help/forms/assets/adaptive-forms-container.png)
1. Selecionar um modelo de dados do formulário. Abra o **[!UICONTROL Básico]** guia. No serviço de preenchimento, selecione **[!UICONTROL Serviço de preenchimento do modelo de dados de formulário]**.
1. Clique em **[!UICONTROL Concluído]**. O formulário adaptável agora está configurado para usar o Preenchimento prévio do modelo de dados de formulário. Agora você pode, use o [editor de regras](rule-editor.md) para criar regras para preencher previamente os campos do formulário.


## Redirecionar o usuário para uma página ou mostrar uma mensagem de agradecimento no envio do formulário

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou uma mensagem. Para redirecionar o usuário ou configurar a mensagem de agradecimento:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.

1. Abra o **[!UICONTROL Envio]** guia.

   * Para configurar um URL de redirecionamento, para na opção Enviar, selecione o **[!UICONTROL Redirecionar para URL]** e procure e selecione uma página do AEM Sites ou forneça o URL de uma página externa.
   * Para configurar uma mensagem personalizada ou de agradecimento, para na opção Enviar, selecione o **[!UICONTROL Mostrar mensagem]** e forneça uma mensagem na caixa de diálogo **[!UICONTROL Conteúdo da mensagem]** caixa. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.

## Ver próximo

* [Criar estilo ou temas para seus formulários](using-themes-in-core-components.md)
* [Adicionar comportamento dinâmico a formulários usando o editor de regras](rule-editor.md)
* [Definir layout de formulários para diferentes tamanhos de tela e tipos de dispositivo](/help/sites-cloud/authoring/features/responsive-layout.md)


## Artigo relacionado {#related-article}

* [Criar um formulário adaptável independente baseado nos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)
