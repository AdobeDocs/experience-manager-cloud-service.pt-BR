---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: como enviar um email para um formulário adaptável, Ação enviar de email, Email do formulário adaptável, Email de envio do formulário, Guia de envio de email
feature: Adaptive Forms, Core Components
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: "Como configurar uma ação enviar para um formulário adaptável?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Configurar a ação de envio Enviar email para um formulário adaptável

A variável **[!UICONTROL Enviar e-mail]** A ação enviar permite enviar um email para um ou mais recipients após o envio bem-sucedido do formulário. Essa ação de envio permite criar um email que pode incluir dados de formulário em um formato predefinido. Por exemplo, considere o seguinte modelo em que o nome do cliente, o endereço de entrega, o nome do estado e o CEP são recuperados dos dados de formulário enviado:


    &quot;
    Olá ${customer_Name},
    
    O endereço a seguir é definido como o endereço de entrega padrão:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Atenciosamente,
    WKND
    
    &quot;


## Vantagens

Algumas vantagens de configurar um Formulário adaptável com a ação Enviar email de envio são:

* Ele permite a comunicação rápida, pois os dados do formulário são enviados diretamente para os destinatários de email designados.
* Ajuda a simplificar o fluxo de trabalho, integrando diretamente os envios de formulários às notificações por email.
* Ele ajuda as organizações a personalizar o conteúdo de email, tornando-o adequado para necessidades específicas de comunicação.

## Configurar ação de envio de email {#steps-to-configure-send-email-submit-action}

Para configurar a Ação de envio:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique em  **[!UICONTROL Envio]** guia.
1. No **[!UICONTROL Ação de envio]** selecione **[!UICONTROL Enviar e-mail]**.

   ![Configuração de ação de Enviar email](/help/forms/assets/send-email-action-configuration.gif)
1. Especificar a ID de email do remetente na **[!UICONTROL De]** caixa de texto.
1. Adicione a ID de email do recipient na **[!UICONTROL Para]** caixa de texto. É possível adicionar vários destinatários clicando no ícone **[!UICONTROL Adicionar]** botão.
1. [Opcional] Adicione o recipient para CC e CCO clicando no link **[!UICONTROL Adicionar]** botão.
1. Especifique uma linha de assunto na **[!UICONTROL Assunto]** caixa de texto.
1. Adicione um template de email para configurar a ação de envio de email.
   * Você pode especificar o caminho para o modelo de email externo salvo nos ativos AEM usando o **[!UICONTROL Caminho do modelo externo]** opção.
   * Você também pode adicionar um modelo de email personalizado para o envio do formulário na **[!UICONTROL Modelo de e-mail]** caixa de texto.
1. [Opcional] A variável **[!UICONTROL Enviar e-mail]** Submeter Ação fornece a opção de incluir anexos e uma [Documento de registro (DoR)](generate-document-of-record-core-components.md) com o email.
1. Clique em **[!UICONTROL Concluído]**.

## Práticas recomendadas {#best-practices}

* É recomendável manter o conteúdo do email claro e conciso. Os usuários devem entender a finalidade do email e quaisquer ações que precisem ser realizadas.
* É recomendável que todos os campos de formulário tenham nomes de elemento exclusivos, mesmo que eles sejam colocados em painéis diferentes em um Formulário adaptável.
* Ao usar o AEM as a Cloud Service, o email de saída requer criptografia. Por padrão, a funcionalidade de email de saída está desativada. Para ativá-lo, envie um tíquete de suporte para [solicitar acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


## Artigos relacionados

{{af-submit-action}}
