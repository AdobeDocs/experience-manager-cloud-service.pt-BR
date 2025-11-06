---
title: Como usar o hCaptcha&reg; em componentes principais de formulários adaptáveis do AEM?
description: Melhore a segurança dos formulários com o serviço hCaptcha&reg; sem esforço. Guia passo a passo no interior.
topic-tags: Adaptive Forms, author
keywords: Captcha&reg; serviço, Forms adaptável, desafio de CAPTCHA, Prevenção de bot, Componentes principais, Segurança de envio de formulário, Prevenção de spam de formulário
feature: Adaptive Forms, Core Components
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 24%

---

# Conecte seu ambiente AEM Forms com o hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Este recurso está em Early Adoter Program. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms as a Cloud Service é compatível com as seguintes soluções CAPTCHA:

* [Captcha](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [Captcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## Integrar o ambiente do AEM Forms com o Captcha Captcha

O serviço hCaptcha® protege seus formulários contra bots, spam e abuso automatizado. O recurso representa um desafio de dispositivo de caixa de seleção e avalia a resposta do usuário para determinar se um humano ou um bot está interagindo com o formulário. Ele impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que os bots publiquem spam ou atividades mal-intencionadas.

O AEM Forms as a Cloud Service suporta o hCaptcha® nos componentes principais adaptáveis do Forms. Você pode usá-lo para apresentar um desafio de widget de caixa de seleção no envio do formulário.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Pré-requisitos para integrar o ambiente do AEM Forms com o Captcha® {#prerequisite}

Para configurar o hCaptcha® com AEM Forms, você precisa obter a [chave do site e a chave secreta do hCaptcha®](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) do site do hCaptcha®.

### Configurar o hCaptcha® {#steps-to-configure-hcaptcha}

Para integrar o AEM Forms com o serviço hCaptcha®, execute as seguintes etapas:

1. Crie um Contêiner de configuração em seu ambiente AEM Forms as a Cloud Service. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM a serviços externos. Para criar e configurar um Contêiner de configuração para conectar seu ambiente AEM Forms com o hCaptcha®:
   1. Abra a instância do AEM Forms as a Cloud Service.
   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   1. No Navegador de configuração, você pode selecionar uma pasta existente ou criar uma pasta. Você pode criar uma pasta e ativar a opção Configurações de nuvem para ela ou Ativar a opção Configurações de nuvem para uma pasta existente:

      * Para criar uma pasta e ativar a opção Configurações de nuvem para ela:
         1. No Navegador de Configuração, clique em **[!UICONTROL Criar]**.
         1. Na caixa de diálogo Criar Configuração, especifique um nome, título e selecione a opção **[!UICONTROL Configurações de Nuvem]**.
         1. Clique em **[!UICONTROL Criar]**.
      * Para ativar a opção Configurações de nuvem para uma pasta existente:
         1. No Navegador de Configuração, selecione a pasta e selecione **[!UICONTROL Propriedades]**.
         1. Na caixa de diálogo Propriedades de Configuração, habilite **[!UICONTROL Configurações de Nuvem]**.
         1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. Configure o Cloud Service:
   1. Na instância do autor do AEM, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** e selecione **[!UICONTROL hCaptcha®]**.
      ![hCaptcha® na interface do usuário](assets/hcaptcha-in-ui.png)
   1. Selecione um Contêiner de configuração, criado ou atualizado, conforme descrito na seção anterior. Selecione **[!UICONTROL Criar]**.
      ![Captcha de Configuração®](assets/config-hcaptcha.png)
   1. Especifique **[!UICONTROL Título]**, **[!UICONTROL Nome]**, **[!UICONTROL Chave do Site]** e **[!UICONTROL Chave Secreta]** para o serviço hCaptcha® [obtido no Pré-requisito](#prerequisite). Selecione **[!UICONTROL Criar]**.

      ![Configure o Cloud Service para conectar seu ambiente AEM Forms com o hCaptcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Os usuários não precisam modificar a [URL de validação do JavaScript do lado do cliente](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) e a [URL de validação do lado do servidor](https://docs.hcaptcha.com/#verify-the-user-response-server-side), pois já estão pré-preenchidos para validação do hCaptcha®.

   Após configurar o serviço hCAPTCHA, ele estará disponível para uso em um [Formulário adaptável com base nos Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Usar o Captcha® em um Forms Adaptive Core Components {#using-hCaptcha&reg;-core-components}

1. Abra a instância do AEM Forms as a Cloud Service.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione um Formulário adaptável e selecione **[!UICONTROL Propriedades]**. Para a opção **[!UICONTROL Contêiner de configuração]**, selecione o Contêiner de configuração que contém a Configuração na nuvem que conecta o AEM Forms com o hCaptcha® e selecione **[!UICONTROL Salvar e fechar]**.

   Se você não tiver um Contêiner de configuração como esse, consulte a seção [Conecte seu ambiente AEM Forms com o hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) para saber como criar um Contêiner de configuração.

   ![Selecionar Contêiner de Configuração](/help/forms/assets/captcha-properties.png)

1. Selecione um Formulário adaptável e selecione **[!UICONTROL Editar]**. O Formulário adaptável é aberto no Editor Forms adaptável.
1. No navegador de componentes, arraste e solte ou adicione o componente **[!UICONTROL Captcha®]** do Formulário adaptável no Formulário adaptável.
1. Selecione o componente **[!UICONTROL Captcha®]** do formulário adaptável e clique no ícone ![Propriedades](assets/configure-icon.svg). Ele abre a caixa de diálogo de propriedades. Especifique as seguintes propriedades:

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL Nome]:** Especifique o nome do componente Captcha. Você pode identificar facilmente um componente de formulário com seu nome exclusivo no formulário e no editor de regras.
   * **[!UICONTROL Título]:** Especifique o título para o componente Captcha.
   * **[!UICONTROL Configurações]:** selecione uma configuração na nuvem definida para o hCaptcha®.
   * **Tamanho do Captcha:** Você pode selecionar o tamanho de exibição da caixa de diálogo de desafio do hCaptcha®. Use a opção **[!UICONTROL Compacto]** para exibir uma uma caixa de diálogo de desafio hCaptcha® de tamanho pequeno e a opção **[!UICONTROL Normal]** para exibir uma de tamanho relativamente grande.<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL Mensagem de validação]:** Forneça uma mensagem de validação para a validação Captcha no envio do formulário.
   * **[!UICONTROL Mensagem de validação de script]**: essa opção permite inserir uma mensagem que será exibida se a validação do script falhar.

     >[!NOTE]
     >Você pode ter várias configurações de nuvem no seu ambiente para uma finalidade semelhante. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conectar seu ambiente AEM Forms com o hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) para saber como criar um Cloud Service que conecta seu ambiente AEM Forms com o serviço hCaptcha®.

   <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. Selecione **[!UICONTROL Concluído]**.


Agora, somente formulários legítimos, nos quais o preenchimento do formulário apaga com êxito o desafio imposto pelo serviço hCaptcha®, são permitidos no envio do formulário. hCaptcha®

**hCaptcha® é uma marca registrada da Intuition Machines, Inc.**


## Perguntas frequentes

* **P: Posso usar mais de um componente Captcha em um Formulário adaptável?**
* **Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar um componente Captcha em um fragmento ou painel marcado para carregamento lento.

## Consulte também {#see-also}

{{see-also}}
