---
title: Traduzir e localizar um formulário de serviços de entrega de borda do AEM Forms
description: Traduzir e localizar um formulário de serviços de entrega de borda do AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---


# Traduzir e localizar um formulário de serviços de entrega de borda do AEM Forms

Em Edge Delivery Services, a tradução de formulários envolve a conversão do conteúdo de formulários de um idioma para outro com foco na precisão, clareza e consistência. Os formulários traduzidos ou localizados permitem que um público-alvo maior alcance diferentes localizações geográficas, melhorando a experiência do usuário e facilitando uma melhor comunicação entre diversas preferências de idioma.


No final do artigo, você aprenderá a:

* [Traduzir formulários no Google Drive](#translate-form-google-drive)
* [Traduzir formulários no site do SharePoint](#translate-form-sharepoint)

## Traduzir formulários no Google Drive {#translate-form-google-drive}

A variável `GOOGLETRANSLATE` A função em folhas do Google traduz formulários ao tocar na ferramenta de tradução integrada, alterando o texto de um idioma para outro diretamente em uma folha do Google. Para traduzir formulários no Google Drive:

1. Vá para a pasta do Projeto AEM no Google Drive e abra a folha do Google.
2. Renomear a planilha existente (`shared-default`) para `shared-en`.
3. Adicionar uma planilha com nome `shared-default`. A variável `shared-default` A planilha contém o conteúdo a ser localizado para um idioma específico.
4. Adicione o conteúdo localizado na `shared-default` planilha usando o `GOOGLETRANSLATE` função.
Você pode usar uma fórmula para traduzir o conteúdo da célula D2 do `shared-en` em francês no prazo de `shared-default` planilha. Esta é a fórmula a ser usada:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Pesquisa Converter planilha](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Visualizar e publicar a planilha usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Você pode consultar a [planilha](/help/forms/assets/enquirytranslate.xlsx) contendo a definição de formulário para um `enquiry` formulário traduzido do inglês para o francês.

![Formulário de Consulta Traduzido](/help/forms/assets/translate-form-french.png)

Consulte a URL abaixo, onde você pode visualizar o formulário com sua tradução em francês: https://main--portal--wkndforms.hlx.live/enquirytranslate

## Traduzir formulários no site do SharePoint{#translate-form-sharepoint}

Para traduzir os formulários no site do Microsoft® SharePoint, é necessário alterar manualmente os rótulos dos campos usando qualquer serviço de tradução. Para traduzir os formulários no site do SharePoint:

1. Vá para a pasta Projeto AEM no Microsoft® SharePoint e abra a planilha.
2. Renomear a planilha existente (`shared-default`) para `shared-en`.
3. Adicionar uma planilha com nome `shared-default`. A variável `shared-default` A planilha contém o conteúdo a ser localizado para um idioma específico.
4. Adicione o conteúdo localizado na `shared-default` manualmente.

   ![Pesquisa Converter planilha](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Visualizar e publicar a planilha usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Consulte a [planilha](/help/forms/assets/enquirytranslate-sp.xlsx) contendo a definição de formulário para um `enquiry` formulário traduzido do inglês para o francês.

![Formulário de Consulta Traduzido](/help/forms/assets/translate-form-french.png)

Consulte a URL abaixo, onde você pode visualizar o formulário com sua tradução em francês: https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemas conhecidos {#known-issues}

* Os rótulos do formulário são traduzidos para o idioma localizado especificado na `shared-default` mas as mensagens de erro serão exibidas no idioma padrão do navegador.

  ![Mensagem de erro](/help/forms/assets/translate-error-message.png)

* Quando você abre o calendário, o menu suspenso de calendário é exibido no idioma padrão do navegador.

  ![Mensagem de erro](/help/forms/assets/translate-calender-display.png)


## Perguntas frequentes {#faq}

**Q**: Como posso digitar a entrada no idioma localizado especificado em um formulário?

**A**: para inserir texto em um idioma localizado específico, ajuste as configurações do teclado no dispositivo. Consulte os seguintes links para obter instruções sobre como fazer isso:

* [Configurar o Mac para receber entrada em outro idioma](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [Configurar o Windows para receber entrada em outro idioma](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [Configurar o Android ou iPhones/iPads para receber entrada em outro idioma](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**: como posso recuperar uma lista de localidades usadas na `GOOGLETRANSLATE` função?

**A**: Você pode consultar o [documentação oficial do Google](https://cloud.google.com/translate/docs/languages) para obter uma lista abrangente das localidades usadas no GOOGLETRANSLATE.

## Consulte também:

{{see-more-forms-eds}}

