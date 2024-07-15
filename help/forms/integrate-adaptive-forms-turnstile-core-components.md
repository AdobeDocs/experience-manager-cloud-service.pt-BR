---
title: Como usar o módulo de torção em um AEM Formulário adaptável Componentes principais?
description: Melhore a segurança dos formulários com o serviço de Tornição sem esforço. Guia passo a passo no interior.
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: e9c13228-0857-4936-9c39-12ed2bddf429
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 12%

---

# Conecte seu ambiente do AEM Forms com o Turnstile {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> Este recurso está em Early Adoter Program. Você pode escrever para aem-forms-ea@adobe.com da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms as a Cloud Service é compatível com as seguintes soluções CAPTCHA:


* [Cilindro de nuvens](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [Captcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)



<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Integrar o ambiente do AEM Forms com o Captcha de tartaruga

O Captcha de torniquete da Cloudflare é uma medida de segurança que visa proteger formulários e sites contra bots automatizados, ataques mal-intencionados, spams e tráfego automatizado indesejado. Ele apresenta uma caixa de seleção no envio do formulário para verificar se ele é humano, antes de permitir que ele envie o formulário. O AEM Forms as a Cloud Service é compatível com o Captcha de tarja nos componentes principais adaptáveis do Forms.

### Pré-requisitos para integrar o ambiente do AEM Forms com o Captcha giratório {#prerequisite}

Para configurar o Turnstile para os Componentes principais do AEM Forms, você precisa obter [Turnstile sitekey e secret key](https://developers.cloudflare.com/turnstile/get-started/) do site do Turnstile.

### Configurar título {#steps-to-configure-hcaptcha}

Para integrar o AEM Forms ao serviço de Borboleta, execute as seguintes etapas:

1. Crie um contêiner de configuração no ambiente as a Cloud Service do AEM Forms. Um Contêiner de configuração contém as Configurações de nuvem usadas para conectar o AEM a serviços externos. Para criar e configurar um Contêiner de configuração para conectar seu ambiente do AEM Forms com o Turnstile:
   1. Abra a instância as a Cloud Service do AEM Forms.
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
   1. Na instância do autor do AEM, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e selecione **[!UICONTROL Turnstile]**.
      ![Borboleta na interface do usuário](assets/turnstile-in-ui.png)
   1. Selecione um Contêiner de configuração, criado ou atualizado, conforme descrito na seção anterior. Selecione **[!UICONTROL Criar]**.
      ![Estrutura de configuração](assets/config-hcaptcha.png)
   1. Especifique **[!UICONTROL Tipo de Widget]** como gerenciado, **[!UICONTROL Título]**, **[!UICONTROL Nome]**, **[!UICONTROL Chave do Site]** e **[!UICONTROL Chave Secreta]** para o serviço de Borracha [obtido no pré-requisito](#prerequisite).
   1. Clique em **[!UICONTROL Criar]**.

      ![Configure o Cloud Service para conectar seu ambiente do AEM Forms com o Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Os usuários não precisam modificar o URL de validação do JavaScript do lado do cliente e o URL de validação do lado do servidor, pois já estão pré-preenchidos para validação do módulo de montagem.

   Após configurar o serviço Captcha com estrutura de rotação, ele estará disponível para uso em um [Formulário adaptável com base nos Componentes principais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Usar a estrutura giratória em um formulário adaptável {#using-turnstile-core-components}

1. Abra a instância as a Cloud Service do AEM Forms.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione um Formulário adaptável e selecione **[!UICONTROL Propriedades]**. Para a opção **[!UICONTROL Contêiner de Configuração]**, selecione o Contêiner de Configuração que contém a Configuração na Nuvem que conecta o AEM Forms com o Turnstile e selecione **[!UICONTROL Salvar e Fechar]**.

   Se você não tiver um Contêiner de Configuração como esse, consulte a seção [Conectar o ambiente do AEM Forms com o Turnstile](#connect-your-forms-environment-with-turnstile-service) para saber como criar um Contêiner de Configuração.

   ![Selecionar Contêiner de Configuração](/help/forms/assets/captcha-properties.png)

1. Selecione um Formulário adaptável e selecione **[!UICONTROL Editar]**. O Formulário adaptável é aberto no Editor Forms adaptável.
1. No navegador de componentes, arraste e solte ou adicione o componente **[!UICONTROL EIXO do formulário adaptável]** no formulário adaptável.
1. Selecione o componente **[!UICONTROL Estrutura de formulário adaptável]** e clique no ícone de propriedades ![ícone de Propriedades](assets/configure-icon.svg). Ele abre a caixa de diálogo de propriedades. Especifique as seguintes propriedades:

   ![Turnstile v2](assets/turnstile-settings-v2.png)

   * **[!UICONTROL Nome]:** Especifique o nome do componente Captcha. Você pode identificar facilmente um componente de formulário com seu nome exclusivo no formulário e no editor de regras.
   * **[!UICONTROL Título]:** Especifique o título para o componente Captcha.
   * **[!UICONTROL Configurações]:** Selecione uma Configuração na Nuvem definida para o Turnstile.
   * **[!UICONTROL Mensagem de Validação]:** Forneça uma mensagem de validação para validar o Captcha no envio do formulário.
   * **[!UICONTROL Mensagem de Validação do Script]**: esta opção permite que você insira uma mensagem a ser exibida se a validação do script falhar.
     >[!NOTE]
     >Você pode ter várias configurações de nuvem no seu ambiente para uma finalidade semelhante. Então, escolha o serviço com cuidado. Se nenhum serviço estiver listado, consulte [Conectar seu ambiente do AEM Forms com o Turnstile](#connect-your-forms-environment-with-turnstile-service) para saber como criar um Cloud Service que conecta seu ambiente do AEM Forms com o serviço Turnstile.
   * **Mensagem de Erro:** Forneça a mensagem de erro a ser exibida ao usuário quando o envio do Captcha falhar.

1. Selecione **[!UICONTROL Concluído]**.


Agora, somente formulários legítimos, em que o preenchimento de formulário apaga com êxito o desafio imposto pelo serviço de Borboleta, são permitidos para o envio do formulário.

![Desafio de tartaruga](assets/turnstile-challenge.png)


## Perguntas frequentes

* **P: Posso usar mais de um componente Captcha em um Formulário adaptável?**
* **Ans:** Não há suporte para o uso de mais de um componente Captcha em um Formulário adaptável. Além disso, não é recomendável usar um componente Captcha em um fragmento ou painel marcado para carregamento lento.

## Consulte também {#see-also}

{{see-also}}
