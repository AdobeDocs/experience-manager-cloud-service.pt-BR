---
title: Como usar o Google reCAPTCHA em um formulário adaptável AEM?
description: Melhore a segurança dos formulários com o serviço Google reCAPTCHA sem esforço. Guia passo a passo no interior.
topic-tags: Adaptive Forms, author
keywords: Serviço Google reCAPTCHA, Forms adaptável, Desafio de CAPTCHA, Prevenção de bot, Componentes principais, Segurança de envio de formulário, Prevenção de spam de formulário
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 10%

---

# Usar o Google reCAPTCHA em um formulário adaptável AEM com base em componentes principais {#using-reCAPTCHA-in-adaptive-forms}

| Aplica-se a | Link do artigo |
| -------- | ---------------------------- |
| Formulário adaptável com base nos Componentes principais | Este artigo |
| Formulário adaptável baseado em componentes de base | [Clique aqui](/help/forms/captcha-adaptive-forms.md) |

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms as a Cloud Service é compatível com as seguintes soluções CAPTCHA:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [Cilindro de nuvens](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [Captcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA da Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Os autores de formulários podem usar o serviço reCAPTCHA pelo Google para implementar o reCAPTCHA no Adaptive Forms. Ele oferece recursos avançados de CAPTCHA para proteger o site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). O [!DNL AEM Forms] as a [!DNL Cloud Service] oferece suporte ao Google reCAPTCHA v2 no Adaptive Forms. Você pode usá-lo para apresentar um desafio de CAPTCHA no envio do formulário. Para conectar seu ambiente do AEM Forms com o serviço reCAPTCHA da Google

1. Obtenha o [par de chaves da API do reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Inclui uma **chave do site** e uma **chave secreta**.

   ![Criar configuração do Google reCAPTCHA do site da Google para obter chaves reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Crie o contêiner de configuração em seu ambiente as a Cloud Service do AEM Forms. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM a serviços externos. Para criar e configurar um Contêiner de configuração para conectar seu ambiente do AEM Forms com o serviço reCAPTCHA do Google:
   1. Abra a instância as a Cloud Service do AEM Forms.
   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**. No Navegador de configuração, é possível:
   1. Selecione uma pasta existente ou crie uma pasta. Você pode criar uma pasta e ativar a opção Configurações de nuvem para ela ou Ativar a opção Configurações de nuvem para uma pasta existente:

      * Para criar uma pasta e ativar a opção Configurações de nuvem para ela:
         1. No Navegador de Configuração, clique em **[!UICONTROL Criar]**.
         1. Na caixa de diálogo Criar Configuração, especifique o nome, o título e selecione a opção **[!UICONTROL Configurações de Nuvem]**.
         1. Clique em **[!UICONTROL Criar]**
      * Para ativar a opção Configurações de nuvem para uma pasta existente:
         1. No Navegador de Configuração, selecione a pasta e selecione **[!UICONTROL Propriedades]**.
         1. Na caixa de diálogo Propriedades de Configuração, habilite **[!UICONTROL Configurações de Nuvem]**.
         1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. Configure o Cloud Service:
   1. Na instância do autor AEM, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e selecione **[!UICONTROL reCAPTCHA]**.
   1. Selecione um Contêiner de configuração, criado ou atualizado na seção anterior. Selecione **[!UICONTROL Criar]**.
   1. Especifique **[!UICONTROL Título]**, **[!UICONTROL Nome]**, **[!UICONTROL Chave do Site]** e **[!UICONTROL Chave Secreta]** para o serviço reCAPTCHA (Obtido na Etapa 1). Selecione **[!UICONTROL Criar]**.

   ![Configure o Cloud Service para conectar seu ambiente do AEM Forms com o serviço reCAPTCHA da Google](/help/forms/assets/captcha-configuration.gif)

   Depois que o serviço reCAPTCHA é configurado, ele é disponibilizado para uso em um Formulário adaptável. Para obter mais informações, consulte [usando o Google reCAPTCHA em um Formulário adaptável](#using-reCAPTCHA).

## Usar o Google reCAPTCHA em um formulário adaptável {#using-reCAPTCHA}

Para usar o reCAPTCHA no Adaptive Forms:

1. Abra a instância as a Cloud Service do AEM Forms.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione um Forms adaptável e selecione **[!UICONTROL Propriedades]**. Para a opção **[!UICONTROL Contêiner de Configuração]**, selecione o Contêiner de Configuração que contém a Configuração na Nuvem que conecta o AEM Forms com o serviço reCAPTCHA pelo Google e selecione **[!UICONTROL Salvar e Fechar]**.

   Se você não tiver um Contêiner de Configuração como esse, consulte a seção [Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA do Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para saber como criar esse Contêiner de Configuração.

   ![Selecionar Contêiner de Configuração](/help/forms/assets/captcha-properties.png)

1. Selecione um Forms adaptável e selecione **[!UICONTROL Editar]**. O Formulário adaptável é aberto no Editor Forms adaptável.
1. No navegador de componentes, arraste e solte o componente **[!UICONTROL Formulário adaptável reCAPTCHA]** no Formulário adaptável.

   A validação do Google reCAPTCHA é sensível ao tempo e expira em cerca de dois minutos. Portanto, a Adobe recomenda colocar o componente **[!UICONTROL Formulário adaptável reCAPTCHA]** antes do botão **[!UICONTROL Enviar]**.

1. Selecione o componente **[!UICONTROL Formulário adaptável reCAPTCHA]** e selecione o ícone de propriedades ![Propriedades](assets/configure-icon.svg). Ele abre a caixa de diálogo de propriedades. Especifique as seguintes propriedades obrigatórias:
   * **[!UICONTROL Nome]:** É possível identificar facilmente um componente de formulário com seu nome exclusivo no formulário e no editor de regras, mas o nome não deve conter espaços ou caracteres especiais.
   * **[!UICONTROL Configuração do CAPTCHA]:** Selecione uma Configuração na Nuvem configurada para apresentar a caixa de diálogo do Google reCAPTCHA para o formulário. Você pode ter várias configurações de nuvem no seu ambiente para fins semelhantes. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA do Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para saber como criar um Cloud Service que conecte seu ambiente do AEM Forms com o serviço reCAPTCHA do Google.
   * **Tamanho do Captcha:** Você pode selecionar o tamanho de exibição da caixa de diálogo de desafio do Google reCAPTCHA. Use a opção **[!UICONTROL Compactar]** para exibir uma opção de tamanho pequeno e a opção **[!UICONTROL Normal]** para exibir uma caixa de diálogo de desafio do Google reCAPTCHA de tamanho relativamente grande.

1. Selecione **[!UICONTROL Concluído]**.

   Agora, o **protegido pelo reCAPTCHA** é exibido no Formulário adaptável. Ele é exibido em todas as Forms adaptáveis configuradas para usar o serviço reCAPTCHA do Google.

   Agora, somente formulários legítimos, nos quais o preenchimento do formulário apaga com êxito o desafio imposto pelo serviço reCAPTCHA do Google, são permitidos para envio.
   ![Google protegido pelo selo reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Perguntas frequentes

**P: Posso usar mais de um componente Captcha em um Formulário adaptável?**
**Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar o componente Captcha em um fragmento ou painel marcado para carregamento lento.

## Consulte também {#see-also}

{{see-also}}