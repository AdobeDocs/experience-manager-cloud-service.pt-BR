---
title: Usar o Google reCAPTCHA em um formulário adaptável com base nos componentes principais
description: Melhore a segurança dos formulários com o serviço Google reCAPTCHA sem esforço. Guia passo a passo no interior!
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: b81acc99b1d90b05b7c341253e7cbb46c6ea12ae
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Usar reCAPTCHA no Forms adaptável com base nos componentes principais {#using-reCAPTCHA-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) é um programa comumente usado em transações on-line para distinguir entre humanos e programas ou bots automatizados. Ele representa um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. Ele impede que o usuário continue se o teste falhar e ajuda a tornar as transações online seguras, impedindo que os bots publiquem spam ou fins mal-intencionados.

[!DNL AEM Forms] as a [!DNL Cloud Service] O é compatível com o Google reCAPTCHA v2 no Adaptive Forms. Você pode usá-lo para apresentar um desafio de CAPTCHA no envio do formulário. Para usar o reCAPTCHA em um formulário adaptável:

1. [Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA da Google](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [Configurar o formulário adaptável para exibir o desafio de CAPTCHA no envio do formulário](#using-reCAPTCHA)

## Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA da Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Para conectar seu ambiente do AEM Forms com o serviço reCAPTCHA da Google

1. Obter [Par de chaves da API do reCAPTCHA](https://www.google.com/recaptcha/admin) do Google. Inclui uma **chave do site** e uma **chave secreta**.

   ![Crie a configuração reCAPTCHA do Google do site da Google para obter as chaves reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Crie o Contêiner de configuração em seu ambiente as a Cloud Service do AEM Forms. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM a serviços externos. Para criar e configurar um Contêiner de configuração para conectar seu ambiente do AEM Forms com o serviço reCAPTCHA do Google:
   1. Abra a instância do AEM Forms as a Cloud Service.
   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**. No Navegador de configuração, é possível:
   1. Selecione uma pasta existente ou crie uma pasta. Você pode criar uma pasta e ativar a opção Configurações de nuvem para ela ou Ativar a opção Configurações de nuvem para uma pasta existente:

      * Para criar uma pasta e ativar a opção Configurações de nuvem para ela:
         1. No Navegador de configuração, clique em **[!UICONTROL Criar]**.
         1. Na caixa de diálogo Criar configuração, especifique o nome, o título e selecione a **[!UICONTROL Configurações da nuvem]** opção.
         1. Clique em **[!UICONTROL Criar]**
      * Para ativar a opção Configurações de nuvem para uma pasta existente:
         1. No Navegador de configuração, selecione a pasta e toque em **[!UICONTROL Propriedades]**.
         1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
         1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. Configure o Cloud Service:
   1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** e toque em **[!UICONTROL reCAPTCHA]**.
   1. Selecione um Contêiner de configuração, criado ou atualizado na seção anterior. Toque **[!UICONTROL Criar]**.
   1. Especificar **[!UICONTROL Título]**, **[!UICONTROL Nome]**, **[!UICONTROL Chave do site]**, e **[!UICONTROL Chave secreta]** para o serviço reCAPTCHA (Obtido na Etapa 1). Toque **[!UICONTROL Criar]**.


   ![Configure o Cloud Service para conectar seu ambiente AEM Forms com o serviço reCAPTCHA da Google](/help/forms/assets/captcha-configuration.gif)



   Depois que o serviço reCAPTCHA é configurado, ele é disponibilizado para uso em um Formulário adaptável. Para obter mais informações, consulte [uso do Google reCAPTCHA em um formulário adaptável](#using-reCAPTCHA).


## Usar o Google reCAPTCHA em um formulário adaptável {#using-reCAPTCHA}

Para usar o reCAPTCHA no Adaptive Forms:

1. Abra a instância do AEM Forms as a Cloud Service.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione um Forms adaptável e toque em **[!UICONTROL Propriedades]**. Para o **[!UICONTROL Contêiner de configuração]** selecione o Contêiner de configuração que contém a Configuração na nuvem que conecta o AEM Forms com o serviço reCAPTCHA pelo Google e toque em **[!UICONTROL Salvar e fechar]**.

   Se você não tiver um Contêiner de configuração, consulte a seção [Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA da Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para saber como criar esse Contêiner de configuração.

   ![Selecionar contêiner de configuração](/help/forms/assets/captcha-properties.png)

1. Selecione um Forms adaptável e toque em **[!UICONTROL Editar]**. O Formulário adaptável é aberto no Editor Forms adaptável.
1. No navegador de componentes, arraste e solte a **[!UICONTROL Formulário adaptável reCAPTCHA]** no Formulário adaptável.

   A validação do Google reCAPTCHA é sensível ao tempo e expira em cerca de dois minutos. Portanto, a Adobe recomenda colocar a variável **[!UICONTROL Formulário adaptável reCAPTCHA]** componente antes de **[!UICONTROL Enviar]** botão.

1. Selecione o **[!UICONTROL Formulário adaptável reCAPTCHA]** e toque nas propriedades ![Ícone Propriedades](assets/configure-icon.svg) ícone. Ele abre a caixa de diálogo de propriedades. Especifique as seguintes propriedades obrigatórias:
   * **[!UICONTROL Nome]:** É possível identificar facilmente um componente de formulário com seu nome exclusivo no formulário e no editor de regras, mas o nome não deve conter espaços ou caracteres especiais.
   * **[!UICONTROL Configuração CAPTCHA]:** Selecione uma Configuração na nuvem configurada para apresentar a caixa de diálogo Google reCAPTCHA para o formulário. Você pode ter várias configurações de nuvem no seu ambiente para fins semelhantes. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conecte seu ambiente do AEM Forms com o serviço reCAPTCHA da Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para saber como criar um Cloud Service que conecta seu ambiente do AEM Forms com o serviço reCAPTCHA da Google.
   * **Tamanho do Captcha:** Você pode selecionar o tamanho de exibição da caixa de diálogo de desafio do Google reCAPTCHA. Use o **[!UICONTROL Compacto]** opção para exibir um tamanho pequeno e a variável **[!UICONTROL Normal]** opção para exibir uma caixa de diálogo de desafio do Google reCAPTCHA de tamanho relativamente grande.

1. Toque **[!UICONTROL Concluído]**.

   Agora, a variável **protegido pelo reCAPTCHA** é exibido no seu Formulário adaptável. Ele é exibido em todas as Forms adaptáveis configuradas para usar o serviço reCAPTCHA do Google.

   Agora, somente formulários legítimos, nos quais o preenchimento do formulário apaga com êxito o desafio imposto pelo serviço reCAPTCHA do Google, são permitidos para envio.
   ![Google protegido pelo selo reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Perguntas frequentes

**P: Posso usar mais de um componente Captcha em um formulário adaptável?**
**Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar o componente Captcha em um fragmento ou painel marcado para carregamento lento.

