---
title: Uso AEM fluxo de trabalho de tradução para localizar o Adaptive Forms e o Document of Record
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: Saiba como usar AEM fluxos de trabalho de tradução para localizar o Adaptive Forms e Document of Record.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Uso AEM fluxo de trabalho de tradução para localizar o Adaptive Forms e o Document of Record {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Formulários localizados ajudam você a oferecer um público-alvo maior em várias regiões. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar o Adaptive Forms e seus documentos de registro . Você pode usar **tradução automática** ou **tradutores humanos** para localizar um formulário adaptável.

Este artigo explica o processo para usar AEM fluxo de trabalho de tradução com o Adaptive Forms e documentos de registro.

## Localização de um formulário adaptável e documento de registro usando tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática imediatamente traduz o conteúdo no Formulário adaptável e no Documento de registro. [!DNL AEM Forms] está pré-configurado para usar uma versão de avaliação de [!DNL Microsoft Translator] para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para o Adaptive Forms e Document of Record:

1. No [!DNL AEM Forms] Na interface do usuário, selecione um formulário e toque no **Adicionar dicionário** opção.
1. Em **Adicionar dicionário ao projeto de tradução** selecione o **Criar um novo projeto de tradução** ou **Adicionar a um projeto de tradução existente** opção.
1. No **Título do projeto** , especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No **Idiomas de destino** , especifique uma localidade (por exemplo, `German(de)`) e clique em **Concluído**. Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas na variável **Idiomas de destino** campo.
1. Na caixa de diálogo Dicionário adicionado, clique em **Projetos abertos**. Na tela Projetos , abra o projeto recém-criado.
1. Clique no botão **elipses** na parte inferior do **Resumo da tradução** mosaico. A tela Resumo da tradução é aberta.
1. Clique no botão **Editar** na parte superior do **Resumo da tradução** tela. Abra o **Tradução** e selecione Tradução automática na guia **Método de tradução** tela. Selecione o **Provedor de Tradução** e **Configuração na nuvem**. Clique no botão **Concluído** na parte superior da tela.
1. No **Tarefa de tradução** bloco , clique no botão ![aem62forms_downseta](assets/aem62forms_downarrow.png) e clique em **Iniciar**. O status do bloco é alterado para Rascunho. Ao concluir a tradução, o status é alterado para **Pronto para revisão**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Pronto para revisão** no **Tarefa de tradução** em mosaico, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão(de), defina a localidade do navegador como alemão(de).
   >* Os componentes do Formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.


   Juntamente com o Formulário adaptativo, o Documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do Documento de registro, consulte:

[Documento de configuração modelo de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configurações do documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizar as informações de marca do Documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e verifique se a localidade do navegador está definida com o mesmo idioma no qual você localizou o Formulário adaptável usando o idioma do computador. A localidade do navegador ajuda a localizar as informações de marca no Documento de registro.
1. Para exibir o Documento de registro localizado, toque em Gerar visualização. O PDF Document of Record é gerado e aberto em uma nova guia no seu navegador.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that will be displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

