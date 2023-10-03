---
title: Como usar o fluxo de trabalho de tradução do AEM para localizar o Forms adaptável e o Documento de registro?
description: O fluxo de trabalho de tradução do AEM ajuda a localizar o Adaptive Forms e seus documentos de registro usando tradução automática ou humana.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Localizar o Forms adaptável e o documento de registro{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Os formulários localizados ajudam você a atender um público-alvo maior em todas as regiões geográficas. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar o Adaptive Forms e seus documentos de registro. Você pode usar **tradução automática** ou **tradutores humanos** para localizar um Formulário adaptável.

Este artigo explica o processo de uso do fluxo de trabalho de tradução do AEM com o Adaptive Forms e documentos de registro.

## Localizar um formulário adaptável e um documento de registro usando a tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática traduz imediatamente seu conteúdo no formulário adaptável e no documento de registro. [!DNL AEM Forms] O é pré-configurado para usar uma versão de avaliação do [!DNL Microsoft Translator] para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para o Forms adaptável e o Documento de registro:

1. No [!DNL AEM Forms] Selecione um formulário e toque na guia **Adicionar dicionário** opção.
1. Entrada **Adicionar dicionário ao projeto de tradução** , selecione a **Criar um novo projeto de tradução** ou **Adicionar a um projeto de tradução existente** opção.
1. No **Título do projeto** especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No **Idiomas de destino** especifique um local (Por exemplo, `German(de)`) e clique em **Concluído**. Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas no **Idiomas de destino** campo.
1. Na caixa de diálogo Dicionário adicionado, clique em **Abrir Projetos**. Na tela Projetos, abra o projeto recém-criado.
1. Clique em **reticências** na parte inferior do **Resumo da tradução** bloco. A tela Resumo da tradução é aberta.
1. Clique em **Editar** ícone na parte superior do **Resumo da tradução** tela. Abra o **Tradução** e selecione Tradução automática na guia **Método de tradução** tela. Selecione o apropriado **Provedor de tradução** e **Configuração na nuvem**. Clique em **Concluído** no topo da tela.
1. No **Tarefa de tradução** lado a lado, clique no link ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Início**. O status do bloco muda para Rascunho. Na conclusão da tradução, o status muda para **Pronto para revisão**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Pronto para revisão** no **Tarefa de tradução** bloco, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão (de), defina o local do navegador como alemão (de).
   >* Os componentes do Formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.

   Junto com o formulário adaptável, o documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do documento de registro, consulte:

[Documento de configuração modelo de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configurações do documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizar as informações de marca do documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e certifique-se de que a localidade do navegador esteja definida com o mesmo idioma para o qual você localizou o Formulário adaptável usando o idioma do computador. O local do navegador ajuda a localizar as informações de marca no Documento de registro.
1. Para exibir o documento de registro localizado, toque em Gerar visualização. O PDF de documento de registro é gerado e aberto em uma nova guia no navegador.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that is displayed to the end users and placeholders for the corresponding localized text.

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

