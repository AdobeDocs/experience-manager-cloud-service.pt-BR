---
title: Como podemos traduzir um Formulário adaptável baseado em Componentes principais?
description: Saiba como criar um Modelo de dados de formulário (FDM) no AEM Forms, testar o modelo com dados e serviços de amostra e configurar várias opções para um modelo.
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---

# Usar tradução automática ou tradução humana para traduzir um Formulário adaptável baseado em Componentes principais {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Os formulários localizados ajudam você a atender um público-alvo maior em todas as regiões geográficas. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar o Adaptive Forms e seus documentos de registro. Você pode usar a **tradução automática** ou os **tradutores humanos** para localizar um Formulário adaptável.

## Traduzir um formulário adaptável e um documento de registro usando a tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática traduz imediatamente seu conteúdo no Formulário adaptável e no [Documento de registro](/help/forms/generate-document-of-record-core-components.md). O AEM Forms as a Cloud Service é pré-configurado para usar uma versão de avaliação do Microsoft Translator para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para o Forms adaptável e o Documento de registro:

1. Na interface do usuário do AEM Forms, selecione um formulário e a opção **[!UICONTROL Adicionar dicionário]**.
1. Na tela Adicionar Dicionário ao Projeto de Tradução, para a opção **[!UICONTROL Projeto]**

   * Para criar um projeto de tradução, selecione a opção **[!UICONTROL Criar um novo projeto de tradução]** e, no campo **Título do projeto**, especifique o título. Por exemplo, `Government Reference Site - German locale.`
   * Para adicionar um novo dicionário a um projeto de tradução existente, selecione a opção **[!UICONTROL Adicionar a um projeto de tradução existente]** e selecione um **[!UICONTROL Projeto de tradução existente]**.
1. No campo **Idiomas de Destino**, especifique uma localidade (por exemplo, `German(de)`). Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas no campo **Idiomas de Destino**. Clique em **Concluído**.
1. Na caixa de diálogo Dicionário Adicionado, clique em **Abrir Projetos**.
1. Na tela Projetos, clique no projeto criado. Por exemplo, clique no bloco **Site de Referência do Governo - Local alemão**.
1. No bloco **Trabalho de Tradução**, clique no ícone ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Iniciar**. O status do bloco muda para Rascunho. Na conclusão da tradução, o status muda para **Aprovado**. Atualize a página após alguns minutos e verifique o status.

   ![Iniciar tradução](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. Depois que o status for alterado para **Aprovado** no bloco **Trabalho de Tradução**, clique no ícone ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Concluído**.

1. Para visualizar o formulário localizado, na interface do usuário do AEM Forms, selecione o formulário localizado. Clique em **[!UICONTROL Visualizar]** >**[!UICONTROL Visualizar como HTML]**. Reabra o formulário depois de adicionar o `afAcceptLang=<locale code>` à URL do formulário. Por exemplo, adicione `afAcceptLang=de` para abrir a versão em alemão do formulário.


   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão (de), defina o local do navegador como alemão (de).
   >* Os componentes do formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## Localizar um formulário adaptável e seu documento de registro usando a Tradução humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Na Tradução humana, o conteúdo é enviado a um provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.

Para tradução, um dicionário contendo arquivos no formato XLIFF é compartilhado com os tradutores profissionais. O dicionário inclui um arquivo XLIFF separado para cada localidade. Cada arquivo XLIFF contém texto que é exibido aos usuários finais e espaços reservados para o texto localizado correspondente.

Execute as seguintes etapas para localizar um formulário e seu documento de registro usando Tradutores Humanos:

1. Na interface do usuário do AEM Forms, selecione um formulário e a opção **[!UICONTROL Adicionar dicionário]**.
1. Na tela Adicionar Dicionário ao Projeto de Tradução, para a opção **[!UICONTROL Projeto]**

   * Para criar um projeto de tradução, selecione a opção **[!UICONTROL Criar um novo projeto de tradução]** e, no campo **Título do projeto**, especifique o título. Por exemplo, `Government Reference Site - German locale.`
   * Para adicionar um novo dicionário a um projeto de tradução existente, selecione a opção **[!UICONTROL Adicionar a um projeto de tradução existente]** e selecione um **[!UICONTROL Projeto de tradução existente]**.
1. No campo **Idiomas de Destino**, especifique uma localidade (por exemplo, `German(de)`). Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas no campo **Idiomas de Destino**. Clique em **Concluído**.
1. Na caixa de diálogo Dicionário Adicionado, clique em **Abrir Projetos**.
1. Na tela Projetos, clique no projeto criado. Por exemplo, clique no bloco **Site de Referência do Governo - Local alemão**.
1. Na parte inferior do bloco **Resumo**, clique nas **reticências**. A tela Propriedades do projeto de tradução é aberta.
1. Abra a guia **[!UICONTROL Avançado]** na parte superior da tela **Propriedades do projeto de tradução**. Para o **[!UICONTROL Campo de tradução]**, selecione **[!UICONTROL Tradução humana]**. Clique em **Salvar e fechar** na parte superior da tela.
1. No bloco **Trabalho de Tradução**, clique no ícone ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Exportar**. Na caixa de diálogo Exportar, clique na opção Baixar arquivo exportado. Ele baixa um arquivo .zip.
   ![Exportar arquivo de tradução](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. Extraia o arquivo .zip baixado. A pasta extraída tem dois arquivos:
   * Translation_export_summary.xml
   * [arquivo-campos-formulário].xml.
1. Abra o [arquivo-campos-formulário].xml para edição. Adicione as cadeias de caracteres e mensagens localizadas para campos de formulário. Salvar e fechar o arquivo.
1. Compacte os arquivos de Translation_export_summary.xml e [form-fields-file].xml.
1. No bloco **Trabalho de Tradução**, clique no ícone ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Importar**. Selecione o arquivo contendo [form-fields-file].xml. com strings e mensagens localizadas para campos de formulário.

   ![Importar arquivo de tradução](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. Para visualizar o formulário localizado, na interface do usuário do AEM Forms, selecione o formulário localizado. Clique em **[!UICONTROL Visualizar]** >**[!UICONTROL Visualizar como HTML]**. Reabra o formulário depois de adicionar o `afAcceptLang=<locale code>` à URL do formulário. Por exemplo, adicione `afAcceptLang=de` para abrir a versão em alemão do formulário.

## Consulte também {#see-also}

{{see-also}}