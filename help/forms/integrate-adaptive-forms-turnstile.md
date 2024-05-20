---
title: Como usar o Torniquete em um formulário adaptável AEM?
description: Melhore a segurança dos formulários com o serviço de Tornição sem esforço. Guia passo a passo no interior!
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: d2c6514eb1f38b06dfa58daa03b781920b8928f6
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 9%

---

<span class="preview"> Esse recurso está em Early Adoter Program. Você pode escrever para aem-forms-ea@adobe.com a partir de sua ID de e-mail oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso. </span>

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms as a Cloud Service é compatível com as seguintes soluções CAPTCHA:

* [Cilindro de nuvens](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)
* [Captcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Integrar o ambiente do AEM Forms com o Captcha de tartaruga

O Captcha de torniquete da Cloudflare é uma medida de segurança que visa proteger formulários e sites contra bots automatizados, ataques mal-intencionados, spams e tráfego automatizado indesejado. Ele apresenta uma caixa de seleção no envio do formulário para verificar se ele é humano, antes de permitir que ele envie o formulário. O AEM Forms as a Cloud Service é compatível com o Captcha de tarja nos componentes principais adaptáveis do Forms.

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

### Pré-requisitos para integrar o ambiente do AEM Forms com o Captcha giratório {#prerequisite}

Para configurar o Borboleta para os Componentes principais do AEM Forms, obtenha a [Tecla de site com barra de rotação e chave secreta](https://developers.cloudflare.com/turnstile/get-started/) no site Turnstile.

### Etapas para configurar o Turnstile para AEM Forms{#steps-to-configure-turnstile}

1. Crie um Contêiner de configuração em seu ambiente as a Cloud Service do AEM Forms. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM a serviços externos. Para criar e configurar um Contêiner de configuração para conectar seu ambiente do AEM Forms com o Turnstile:
   1. Abra a instância do AEM Forms as a Cloud Service.
   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   1. No Navegador de configuração, você pode selecionar uma pasta existente ou criar uma pasta. É possível criar uma pasta e habilitar a opção Configurações de nuvem para ela ou habilitar a opção Configurações de nuvem para uma pasta existente:

      * **Para criar uma pasta e ativar a opção Configurações de nuvem para ela**:
         1. No Navegador de configuração, clique em **[!UICONTROL Criar]**.
         1. Na caixa de diálogo Criar configuração, especifique um nome, título e selecione a variável **[!UICONTROL Configurações da nuvem]** opção.
         1. Clique em **[!UICONTROL Criar]**.
      * Para ativar a opção Configurações de nuvem para uma pasta existente:
         1. No Navegador de configuração, selecione a pasta e selecione **[!UICONTROL Propriedades]**.
         1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
         1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. Configure o Cloud Service:
   1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e selecione **[!UICONTROL Turnstile]**.
      ![Borboleta na interface](assets/turnstile-in-ui.png)
   1. Selecione um Contêiner de configuração, criado ou atualizado, conforme descrito na seção anterior. Selecione **[!UICONTROL Criar]**.
      ![Turnstile de configuração](assets/config-hcaptcha.png)
   1. Especificar **[!UICONTROL Tipo de widget]** como gerenciado, o tipo de widget pode mudar, o que depende da chave obtida no pré-requisito, **[!UICONTROL Título]**, **[!UICONTROL Nome]**, **[!UICONTROL Chave do site]**, e **[!UICONTROL Chave secreta]** para serviço de torniquete [obtido no pré-requisito](#prerequisite). Selecione **[!UICONTROL Criar]**.

      ![Configure o Cloud Service para conectar seu ambiente AEM Forms com o Turnstile](assets/config-turntstile.png)

>[!NOTE]
> Os usuários não precisam modificar o URL de validação do JavaScript do lado do cliente e o URL de validação do lado do servidor, pois já estão pré-preenchidos para validação do módulo de montagem.

Depois que o serviço Captcha de tartaruga é configurado, ele é disponibilizado para uso em um Formulário adaptável.

## Usar a estrutura giratória em um formulário adaptável{#using-turnstile-foundation-components}

1. Abra a instância do AEM Forms as a Cloud Service.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione um formulário adaptável e **[!UICONTROL Propriedades]**. Para o **[!UICONTROL Contêiner de configuração]** selecione o Contêiner de configuração que contém a Configuração na nuvem que conecta o AEM Forms com o módulo e selecione **[!UICONTROL Salvar e fechar]**.

   Se você não tiver um Contêiner de configuração, consulte a seção [Conecte seu ambiente do AEM Forms com o Turnstile](#connect-your-forms-environment-with-turnstile-service) para saber como criar um Contêiner de configuração.

   ![Selecionar contêiner de configuração](/help/forms/assets/captcha-properties.png)

1. Selecione um formulário adaptável e **[!UICONTROL Editar]**. O Formulário adaptável é aberto no Editor Forms adaptável.
1. No navegador de componentes, arraste e solte a **[!UICONTROL Captcha]** no Formulário adaptável.
1. Selecione o **[!UICONTROL Captcha]** e clique em propriedades ![Ícone Propriedades](assets/configure-icon.svg) ícone. Ele abre a caixa de diálogo de propriedades.

   ![Configurações](assets/turnstile-setting-v1.png)

   Especifique as seguintes propriedades:

   * **[!UICONTROL Título]:** Especifique o título para o componente Captcha. Você pode identificar facilmente um componente de formulário com seu nome exclusivo no formulário e no editor de regras.
   * **[!UICONTROL Mensagem de validação]:** Forneça uma mensagem de validação para validar o Captcha no envio do formulário.
   * **[!UICONTROL Validar Captcha]:** É possível selecionar uma das opções para validar o Captcha:
      * No envio do formulário
      * Em uma ação do usuário.
   * **[!UICONTROL Serviço de Captcha]:** Selecione o seu serviço Captcha, aqui você seleciona Cloudfare Turnstile Captcha serviço.
   * **[!UICONTROL Configuração do Captcha]:** Selecione uma Configuração na nuvem configurada para o torniquete. por exemplo, aqui você seleciona a variável **chave gerenciada**.
     >[!NOTE]
     >Você pode ter várias configurações de nuvem no seu ambiente para uma finalidade semelhante. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conecte seu ambiente do AEM Forms com o Turnstile](#connect-your-forms-environment-with-turnstile-service) para saber como criar um Cloud Service que conecta seu ambiente do AEM Forms com o serviço de Borboleta.

   * **Mensagem de erro:** Forneça a mensagem de erro a ser exibida ao usuário quando o envio do Captcha falhar.
   * **Tamanho do Captcha:** Você seleciona o tamanho de exibição da caixa de diálogo Desafio de Borboleta. Use o **[!UICONTROL Compacto]** opção para exibir um tamanho pequeno e a variável **[!UICONTROL Normal]** opção para exibir uma caixa de diálogo de desafio de Tornição de tamanho relativamente grande.


     >[!NOTE]
     >Isso se aplica ao tipo de widget Gerenciado e Não interativo. Se o tipo de widget for invisível, a propriedade de tamanho não é necessária e está desativada.

1. Selecionar **[!UICONTROL Concluído]**.

Agora, somente formulários legítimos, em que o preenchimento de formulário apaga com êxito o desafio imposto pelo serviço de Borboleta, são permitidos para o envio do formulário.

![Desafio de Tornição](assets/turnstile-challenge.png)

## Perguntas frequentes

* **P: Posso usar mais de um componente Captcha em um formulário adaptável?**
* **Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar um componente Captcha em um fragmento ou painel marcado para carregamento lento.

## Consulte também {#see-also}

{{see-also}}