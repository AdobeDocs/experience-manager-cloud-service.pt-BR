---
title: Traduzir e localizar um Edge Delivery Services para AEM Forms
description: Traduzir e localizar um Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Traduzir e localizar um Edge Delivery Services para AEM Forms

No Edge Delivery Services, a tradução de formulários envolve a conversão do conteúdo do formulário de um idioma para outro com foco na precisão, na clareza e na consistência. Os formulários traduzidos ou localizados permitem que um público-alvo maior alcance diferentes localizações geográficas, melhorando a experiência do usuário e facilitando uma melhor comunicação entre diversas preferências de idioma.


No final do artigo, você aprenderá a:

- [Traduzir formulários no Google Drive](#translate-form-google-drive)
- [Traduzir formulários no site do SharePoint](#translate-form-sharepoint)

## Traduzir formulários no Google Drive {#translate-form-google-drive}

A função `GOOGLETRANSLATE` nas planilhas do Google traduz formulários ao tocar na ferramenta de tradução interna, alterando o texto de um idioma para outro diretamente em uma planilha do Google. Para traduzir formulários no Google Drive:

1. Vá para a pasta AEM Project no Google Drive e abra a planilha do Google.
2. Renomeie a planilha existente (`shared-default`) para `shared-en`.
3. Adicione uma planilha chamada `shared-default`. A planilha `shared-default` contém o conteúdo para localização em um idioma específico.
4. Adicione o conteúdo localizado na planilha `shared-default` usando a função `GOOGLETRANSLATE`.
Você pode usar uma fórmula para traduzir o conteúdo da célula D2 da folha `shared-en` para o francês na folha `shared-default`. Esta é a fórmula a ser usada:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Consulta - Traduzir planilha](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Você pode consultar a [planilha](/help/forms/assets/enquirytranslate.xlsx) contendo a definição de formulário para um formulário `enquiry` traduzido do inglês para o francês.

![Formulário Traduzido de Consulta](/help/forms/assets/translate-form-french.png)

Consulte a URL abaixo, onde você pode visualizar o formulário com sua tradução em francês:
https://main--portal--wkndforms.hlx.live/enquirytranslate

## Traduzir formulários no site do SharePoint{#translate-form-sharepoint}

Para traduzir os formulários no site do Microsoft® SharePoint, é necessário alterar manualmente os rótulos dos campos usando qualquer serviço de tradução. Para traduzir os formulários no site do SharePoint:

1. Vá para a pasta do Projeto AEM no Microsoft® SharePoint e abra a planilha.
2. Renomeie a planilha existente (`shared-default`) para `shared-en`.
3. Adicione uma planilha chamada `shared-default`. A planilha `shared-default` contém o conteúdo para localização em um idioma específico.
4. Adicione o conteúdo localizado na planilha `shared-default` manualmente.

   ![Consulta - Traduzir planilha](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Consulte a [planilha](/help/forms/assets/enquirytranslate-sp.xlsx) contendo a definição de formulário para um formulário `enquiry` traduzido do inglês para o francês.

![Formulário Traduzido de Consulta](/help/forms/assets/translate-form-french.png)

Consulte a URL abaixo, onde você pode visualizar o formulário com sua tradução em francês:
https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemas conhecidos {#known-issues}

- Os rótulos do formulário são traduzidos para o idioma localizado especificado na folha `shared-default`, mas as mensagens de erro são exibidas no idioma padrão do navegador.

  ![Mensagem de erro](/help/forms/assets/translate-error-message.png)

- Quando você abre o calendário, o menu suspenso de calendário é exibido no idioma padrão do navegador.

  ![Mensagem de erro](/help/forms/assets/translate-calender-display.png)


## Perguntas frequentes {#faq}

**Q**: como posso digitar a entrada no idioma localizado especificado em um formulário?

**A**: para inserir texto em um idioma localizado específico, ajuste as configurações de teclado do dispositivo. Consulte os seguintes links para obter instruções sobre como fazer isso:

- [Configure seu Mac para receber entrada em outro idioma](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
- [Configurar o Windows para receber entrada em outro idioma](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
- [Configure seu Android ou iPhones/iPads para receber entrada em outro idioma](https://support.google.com/gboard/answer/7068494?hl=en&co=GENIE.Platform%3DAndroid)


**Q**: como posso recuperar uma lista de localidades usadas na função `GOOGLETRANSLATE`?

**A**: você pode consultar a [documentação oficial do Google](https://cloud.google.com/translate/docs/languages) para obter uma lista abrangente das localidades usadas no GOOGLETRANSLATE.


