---
title: Usar reCAPTCHA com Edge Delivery Services para AEM Forms as a Cloud Service
description: Usar o Google reCAPTCHA em um formulário do Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA em formulários, Uso de reCAPTCHA no Universal Editor, Adição de reCAPTCHA em formulários
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# Usar reCAPTCHA na criação do WYSIWYG

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) é uma ferramenta popular usada para proteger sites contra atividades fraudulentas, spam e uso indevido.

Por exemplo, considere um formulário que calcula o imposto com base em deduções adicionais e a alíquota do imposto. Nesses casos, há o risco de usuários mal-intencionados explorarem o formulário para propósitos como enviar emails de phishing ou inundá-lo com conteúdo irrelevante ou prejudicial usando spambots. A integração do CAPTCHA oferece maior segurança ao verificar se os envios são de usuários genuínos, minimizando efetivamente as entradas de spam.

![recaptcha do Google](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

No Edge Delivery Services Forms, o Bloco de Formulários permite [conectar o Google reCAPTCHA com formulários](#connect-forms-with-recaptcha-service-by-google) usando o componente **Captcha(Invisível)** para distinguir entre humanos e bots. Essa funcionalidade ajuda os autores a proteger seus formulários contra spam e uso indevido.

## Conectar o Forms com o serviço reCAPTCHA da Google

Você pode criar Edge Delivery Services Forms para implementar o serviço reCAPTCHA fornecido pela Google. Dependendo das suas necessidades, você pode configurar um dos seguintes serviços reCAPTCHA para o Edge Delivery Services Forms:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Configurar o reCAPTCHA Enterprise

O reCAPTCHA Enterprise é um serviço premium de detecção e prevenção de fraudes de nível empresarial oferecido pela Google. Ele se baseia na base do reCAPTCHA (com base em pontuação), mas fornece recursos adicionais, escalabilidade e personalização para atender às necessidades complexas das empresas.

#### Antes de começar

Antes de configurar o Google reCAPTCHA Enterprise para o Edge Delivery Services Forms, verifique se você concluiu as seguintes etapas:

1. Crie ou selecione um [projeto do Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) e recupere a [ID do Projeto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Habilite a API corporativa do reCAPTCHA](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) para o seu projeto na nuvem do Google e [crie uma chave de API](https://console.cloud.google.com/apis/credentials).

1. Crie uma [chave do site para o seu projeto do Google Cloud](https://console.cloud.google.com/security/recaptcha) e copie a chave do site.

Depois de ter essas credenciais, você pode continuar com a configuração do reCAPTCHA Enterprise para seus formulários:

1. [Criar contêiner de configuração na nuvem](#1-create-cloud-configuration-container)
1. [Criar a configuração do serviço de nuvem para o reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Criar contêiner de configuração na nuvem

Para criar o contêiner de configuração da nuvem, execute as seguintes etapas:

1. Faça logon na instância do autor.
1. Vá para **[!UICONTROL Ferramentas]** ![Ferramentas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.

   ![Contêiner de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. No **[!UICONTROL Navegador de Configuração]**, navegue até o formulário e selecione **[!UICONTROL Propriedades]**.

   ![Propriedades de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Na caixa de diálogo **[!UICONTROL Propriedades da Configuração]**, habilite as **[!UICONTROL Configurações de Nuvem]**.

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

   ![Habilitar propriedades de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
Depois de criar o contêiner de configuração da nuvem, publique-o.

   ![Publicar configuração de nuvem](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Criar a configuração do Cloud Service para o reCAPTCHA Enterprise

Para criar a configuração do Cloud Service para o reCAPTCHA Enterprise, execute as seguintes etapas:

1. Faça logon na instância do autor.
1. Navegue até **[!UICONTROL Ferramentas]** ![ferramentas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuração de nuvem do Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   A caixa de diálogo **Configurações** é aberta.

1. Navegue até o formulário e selecione **[!UICONTROL Criar]**.

   ![Configuração de captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   A caixa de diálogo **[!UICONTROL Criar configuração do reCAPTCHA]** é aberta.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Selecione a versão como [!DNL ReCAPTCHA Enterprise] e especifique Título, Nome, ID do Projeto, Chave do Site e Chave da API.

   >[!NOTE]
   >
   > Você pode obter a ID do projeto, a Chave do site e a Chave da API na seção [Antes de começar](#before-you-start) para o reCAPTCHA Enterprise.

1. Selecione **[!UICONTROL Tipo de chave]** como **Chave do site baseada em pontuação**.
1. Especifique uma pontuação de limite [ no intervalo de 0 a 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). Pontuações maiores ou iguais às pontuações de limite identificam a interação humana, caso contrário, são consideradas como interação de bot.
1. Selecione **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.

   Depois de criar a configuração de nuvem do reCAPTCHA, publique-a.

   ![Publicar configuração Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Agora é possível criar ou editar um formulário e adicionar o componente reCAPTCHA usando a criação baseada em WYSIWYG. Para obter instruções detalhadas sobre como integrar o Google reCAPTCHA ao formulário, consulte [Usar reCAPTCHA no formulário](#use-recaptcha-in-your-form).

## Configurar o reCAPTCHA

O reCAPTCHA é um serviço gratuito oferecido pela Google que ajuda sites a detectar e evitar tráfego abusivo, incluindo bots e spam. Ele é compatível com uma versão baseada em pontuação que opera em segundo plano e atribui uma pontuação de risco (variando de 0,0 a 1,0) a cada interação do usuário. Pontuações maiores ou iguais às pontuações de limite identificam a interação humana, caso contrário, são consideradas como interação de bot.

#### Antes de começar

Antes de configurar o Google reCAPTCHA para o Edge Delivery Services Forms, recupere o [par de chaves da API do reCAPTCHA do Console do Google](https://www.google.com/recaptcha/admin). O par inclui uma chave do Site e uma chave Secreta.

>[!NOTE]
>
> * O Edge Delivery Services Forms só oferece suporte à versão **reCAPTCHA Score based**.

Depois de ter o par de chaves da API, você pode continuar com a configuração do reCAPTCHA para seus formulários:

1. [Criar contêiner de configuração na nuvem](#1-create-cloud-configuration-container-1)
1. [Criar a configuração do serviço de nuvem para o reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Criar contêiner de configuração na nuvem

Para criar o contêiner de configuração da nuvem, execute as seguintes etapas:

1. Faça logon na instância do autor.
1. Vá para **[!UICONTROL Ferramentas]** ![Ferramentas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.

   ![Contêiner de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. No **[!UICONTROL Navegador de Configuração]**, navegue até o formulário e selecione **[!UICONTROL Propriedades]**.

   ![Propriedades de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Na caixa de diálogo **[!UICONTROL Propriedades da Configuração]**, habilite as **[!UICONTROL Configurações de Nuvem]**.

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

   ![Habilitar propriedades de configuração da nuvem](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Depois de criar o contêiner de configuração da nuvem, publique-o.

   ![Publicar configuração de nuvem](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Criar a configuração do Cloud Service para reCAPTCHA

Para criar a configuração do Cloud Service para o reCAPTCHA, execute as seguintes etapas:

1. Faça logon na instância do autor.
1. Navegue até **[!UICONTROL Ferramentas]** ![ferramentas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuração de nuvem do Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   A caixa de diálogo **Configurações** é aberta.

1. Navegue até o formulário e selecione **[!UICONTROL Criar]**.

   ![Configuração de captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   A caixa de diálogo **[!UICONTROL Criar configuração do reCAPTCHA]** é aberta.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Selecione versão como [!DNL ReCAPTCHA v2] e especifique Título e Nome.
1. Especifique a Chave do site e a Chave secreta.

   >[!NOTE]
   >
   > Você pode obter a Chave do site e a Chave secreta da seção [Antes de começar](#before-you-begin) para o reCAPTCHA.

1. Selecione **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.

   Depois de criar a configuração de nuvem do reCAPTCHA, publique-a.

   ![Publicar configuração Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Agora é possível criar e editar um formulário e adicionar o componente reCAPTCHA usando a criação baseada em WYSIWYG. Para obter instruções detalhadas sobre como integrar o Google reCAPTCHA ao formulário, consulte [Usar reCAPTCHA no formulário](#use-recaptcha-in-your-form).

### Usar reCAPTCHA no seu formulário

Para criar um formulário e adicionar o componente reCAPTCHA (Invisível), execute as seguintes etapas:

1. Abra um formulário no Universal Editor para edição.
1. Navegue até a seção Formulário adaptável adicionada na árvore Conteúdo.
1. Clique no ícone **[!UICONTROL Adicionar]** e adicione o componente **[!UICONTROL Captcha (Invisível)]** da lista **Componentes de Formulário Adaptáveis**.

   ![Adicionar componente reCaptcha](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   Você também pode arrastar e soltar o componente Adaptive Forms necessário, pois o Editor universal oferece um recurso intuitivo de arrastar e soltar.

1. Clique em **Publicar** para publicar o formulário novamente depois de adicionar o componente **[!UICONTROL Captcha (Invisível)]**.

   ![republicar formulário](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Agora você pode exibir o formulário com o serviço reCAPTCHA no seguinte URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

Formulário ![com reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Perguntas frequentes

* **O que acontece se um usuário não criar uma configuração de nuvem do reCAPTCHA?**

  **A**: se um usuário não criar uma configuração de nuvem do reCAPTCHA, o servidor do AEM pesquisará a configuração de nuvem do reCAPTCHA no Contêiner de Configuração Global. Se não houver nenhuma configuração no Contêiner de configuração global, o servidor do AEM emitirá um erro.

* **O que acontece se um usuário criar várias configurações de nuvem do reCAPTCHA?**
  **A**: se um usuário criar mais de uma configuração de nuvem do reCAPTCHA, o sistema selecionará automaticamente a primeira configuração criada do reCAPTCHA.

* **Por que as modificações ou alterações não estão visíveis na URL publicada?**
Se as modificações ou alterações não estiverem visíveis na URL publicada, verifique se o formulário foi republicado para aplicar as atualizações.

* **A qual serviço reCAPTCHA o Edge Delivery Services Forms oferece suporte?**
  **A**: o Edge Delivery Services Forms oferece suporte somente ao serviço reCAPTCHA baseado em pontuação fornecido pela Google.


## Consulte também:

{{universal-editor-see-also}}

