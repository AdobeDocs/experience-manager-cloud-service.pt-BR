---
title: Como alterar o conteúdo da Página zero no Designer?
description: Altere a mensagem exibida na Página Zero de um PDF XFA para visualizadores que não sejam do Adobe PDF.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Alteração do conteúdo da Página zero no Designer {#changing-page-zero-content-in-designer}

O conteúdo da Página Zero é exibido por padrão quando um visualizador que não seja da Adobe PDF, como o visualizador de PDF padrão em [!DNL Chrome] ou [!DNL Firefox], não consegue ler o conteúdo do formulário PDF/XFA. A mensagem padrão de Página zero é mostrada abaixo.

![defaultpage0message](assets/defaultpage0message.png)

A versão [!DNL AEM Forms] do Designer permite alterar a mensagem que é exibida na Página Zero. Para alterar a mensagem Página zero, execute as seguintes etapas:

1. Verifique se você tem a versão [!DNL AEM Forms] do Designer instalada. Você pode verificar a versão na tela Sobre do designer.

1. Abra o formulário para o qual deseja alterar o conteúdo da Página zero.

1. Clique em **[!UICONTROL Arquivo]** > **[!UICONTROL Propriedades do Formulário]**.

1. Na caixa de diálogo [!UICONTROL Propriedades do Formulário], clique em ![mais](assets/plus.png) (ícone de adição) para adicionar uma propriedade personalizada.

1. Especifique **_pagezerocontent** como o nome da propriedade.
1. Adicione a nova mensagem Página zero, em formato Rich Text, como valor. Por exemplo:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download_br.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader_br.</p></body>`

1. Salve o formulário como PDF.

1. Exiba o formulário PDF no navegador para confirmar que a mensagem foi atualizada. O exemplo de valor acima aparece da seguinte maneira:

   ![mensagem alterada](assets/changedmessage.png)

>[!NOTE]
>
>A propriedade personalizada criada pode não aparecer corretamente na caixa de diálogo Propriedades do formulário quando você reabrir o formulário. No entanto, funciona bem e o formulário exibe a mensagem Página zero atualizada.

>[!MORELIKETHIS]
>
>* [Baixe e instale o Forms Designer para criar modelos de documento de registro](/help/forms/installing-configuring-designer.md)
>* [Usar o Forms Designer para criar modelos de Documento de Registro (DoR) e fragmentos de formulário?](/help/forms/use-forms-designer.md)
