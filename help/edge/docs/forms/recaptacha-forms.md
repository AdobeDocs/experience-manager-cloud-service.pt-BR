---
title: Usar reCAPTCHA com Edge Delivery Services para AEM Forms as a Cloud Service
description: Usar o Google reCAPTCHA em um formulário do Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Usar reCAPTCHA com Edge Delivery Services para AEM Forms as a Cloud Service

<!--
<span>The **reCAPTCHA** feature is under the pre-release program. To request access to the **reCAPTCHA** feature for Edge Delivery Services for AEM Forms, send an email from your work address to mailto:aem-forms-ea@adobe.com.</span>
-->

O reCAPTCHA é uma ferramenta popular usada para proteger sites contra atividades fraudulentas, spam e uso indevido. No Edge Delivery Services, o Adaptive Forms Block fornece a capacidade de adicionar o Google reCAPTCHA para distinguir entre humanos e bots. Esse recurso permite que os usuários protejam seu site contra spam e uso indevido.
Por exemplo, considere um formulário de pesquisa que coleta dados como datas de viagem inicial e final, orçamento de sala, custo de viagem estimado e informações do viajante. Nesses casos, há o risco de usuários mal-intencionados explorarem o formulário para propósitos como enviar emails de phishing ou inundá-lo com conteúdo irrelevante ou prejudicial usando spambots. A integração do reCAPTCHA oferece maior segurança ao verificar se os envios são de usuários genuínos, minimizando efetivamente as entradas de spam.

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

O Edge Delivery Services só oferece suporte a **Score based(v3)-reCAPTCHA** para o Bloco de Formulário Adaptável.

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


No final deste artigo, você aprenderá a:

- [Ativar o Google reCAPTCHA para um único formulário](#enable-google-recaptchas-for-a-single-form)
- [Ativar o reCAPTCHA para todos os formulários do site](#enable-recaptcha-for-all-the-forms)

## Pré-requisitos

- Comece o desenvolvimento do Edge Delivery Services Forms seguindo as etapas explicadas em [Criar um formulário usando o Bloco do Adaptive Forms](/help/edge/docs/forms/create-forms.md).
- Registre seu domínio com o [Google reCAPTCHA e obtenha credenciais](https://www.google.com/recaptcha/admin/create).

## Ativar o Google reCAPTCHA para um único formulário {#enable-google-recaptchas-for-a-single-form}

A habilitação do Google reCAPTCHA para um único formulário envolve a integração do serviço reCAPTCHA da Google em um formulário web específico para evitar abuso automatizado ou envios de spam.

Para ativar o Google reCAPTCHA para um único formulário:

1. [Configure a chave secreta do reCAPTCHA no arquivo de configuração do projeto](#configure-secret-key)
1. [Adicionar a chave do site reCAPTCHA ao formulário](#add-site-key)

Para começar a configurar o reCaptcha no Edge Delivery Services Forms, consulte a seguinte [planilha](/help/edge/docs/forms/assets/recaptcha.xlsx) que inclui a definição de formulário para um formulário.

### Configure a chave secreta do reCAPTCHA no arquivo de configuração do projeto {#configure-secret-key}

O Segredo do Site para o domínio registrado com o Google reCAPTCHA é adicionado para projetar o arquivo de configuração (`.helix/config`) na pasta Projeto do AEM na Microsoft SharePoint ou Google Drive. Para adicionar o Segredo do site ao arquivo de configuração:

1. Vá para a pasta do Projeto AEM no Microsoft® SharePoint ou Google Drive.
1. Crie o arquivo `.helix/config.xlsx` na pasta Projeto do AEM no Site do Microsoft SharePoint ou o arquivo `.helix/config` na pasta Projeto do AEM na Unidade Google.

   >[!NOTE]
   >
   > O [arquivo de configuração do projeto](https://www.aem.live/docs/configuration) é uma planilha localizada em `/.helix/config`. Crie o arquivo, caso ele não exista.

1. Abra o arquivo `config` e adicione os seguintes pares de chave e valor:

   - **captcha.secret**: valor da chave secreta do Google reCAPTCHA
   - **captcha.type**: reCAPTCHA v2

   >[!NOTE]
   >
   >  - Você pode recuperar as chaves reCAPTCHA do [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).
   >  - Especifique o valor de **captcha.type** no arquivo `config` como **reCAPTCHA v2**.

   Consulte abaixo a captura de tela de um arquivo de configuração de projeto:

   ![Arquivo de configuração do projeto](/help/forms/assets/recaptcha-config-file.png)

1. Salve o arquivo `config`.

1. Visualize e publique o arquivo `config` usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

### Adicionar a chave do site reCAPTCHA ao formulário {#add-site-key}

A Chave do site para um domínio registrado com o Google reCAPTCHA é adicionada à planilha do formulário que deve ser protegido. Para adicionar a chave do Site a um formulário:

1. Vá para a pasta do Projeto AEM no Microsoft® SharePoint ou Google Drive e abra a planilha. Você também pode criar uma nova planilha para um formulário.
1. Insira uma linha na planilha para adicionar um novo campo como CAPTCHA, incluindo os seguintes detalhes:
   - **tipo**: captcha
   - **value**: valor da chave do site Google reCAPTCHA

   Consulte a captura de tela abaixo, que representa a planilha com o novo tipo de linha como CAPTCHA:

   ![Planilha Recaptcha](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  Você pode recuperar as chaves reCAPTCHA do [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Salve a planilha.
1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha.

Depois de adicionar uma nova linha na definição do formulário, um símbolo reCAPTCHA é exibido no canto inferior direito do formulário. Isso garante que o formulário agora esteja protegido contra atividades fraudulentas, spam e uso indevido.

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## Ativar o reCAPTCHA para todos os formulários do site{#enable-recaptcha-for-all-the-forms}

Para aplicar o Google reCAPTCHA a todos os formulários do seu Site que usam o Bloco de Forms Adaptável, ignore as etapas anteriores e incorpore diretamente o valor `sitekey` ao arquivo `recaptcha.js`. Para incluir o valor da chave do site no arquivo `recaptcha.js`:

1. [Atualize a chave do site Google reCAPTCHA no arquivo recaptcha.js](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [Implante o arquivo e crie o projeto](#2-deploy-the-file-and-build-the-project)
1. [Visualizar o site usando o sidekick do AEM](#3-preview-the-site-using-the-aem-sidekick)

### Atualizar a chave do site Google reCAPTCHA no arquivo recaptcha.js

1. Abra o repositório GitHub correspondente em seu computador local.
1. Navegue até a pasta `[../Form Block/integrations]` e abra o arquivo `recaptcha.js`.
1. Substitua o `siteKey` pelo valor da chave do site Google reCAPTCHA.

   ![Recaptcha se aplica a todos os formulários](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  Você pode recuperar as chaves reCAPTCHA do [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Salve o arquivo `recaptcha.js`.

### Implante o arquivo e crie o projeto

Implante o arquivo `recaptcha.js` atualizado em seu projeto GitHub e verifique se a compilação foi bem-sucedida.

### Visualizar o site usando o sidekick do AEM

Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar o site.

O selo do reCAPTCHA começa a aparecer em todos os formulários do site.

