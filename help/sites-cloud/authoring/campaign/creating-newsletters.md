---
title: Criação de informativos de campanha com o AEM
description: Saiba como usar o AEM as a Cloud Service para criar informativos que podem ser enviados com o Adobe Campaign Classic.
feature: Authoring
role: User
exl-id: 60a6a9d0-f5e6-424f-b320-dd4943c55d45
source-git-commit: 6196f3fc67dbcfe03a71bb6a0796dd5d1d0f8546
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 100%

---


# Criação de informativos de campanha com o AEM {#creating-newsletters}

Neste documento, você aprenderá como usar o AEM as a Cloud Service para criar informativos que podem ser enviados com o Adobe Campaign Classic.

Ao aproveitar a integração entre o AEM as a Cloud Service e o Adobe Campaign Classic, você pode criar informativos usando as ferramentas de criação avançadas do AEM. Depois, quando estiver pronto para enviar o informativo, você poderá usar os recursos de gestão e distribuição de destinatários do Campaign para enviá-lo.

## Pré-requisitos {#prerequisites}

Antes de criar um informativo no AEM e enviá-lo com o Campaign, primeiro você deve [integrar o Adobe Campaign Classic ao AEM as a Cloud Service.](/help/sites-cloud/integrating/integrating-campaign-classic.md)

## Criar estrutura do informativo {#create-structure}

O conteúdo do informativo é gerenciado no AEM da mesma maneira que você gerenciaria o conteúdo do seu site. Você começa criando um “site” para conter o seu conteúdo. Neste “site”, você pode coletar os informativos por marca.

1. Faça logon na instância de autor do AEM.

1. Na página de navegação principal, abra o console **Sites**.

1. Em uma instalação padrão do AEM, haverá uma pasta **Campanha** existente. Selecione-a e clique no botão **Criar** e depois em **Página**.

   ![Criar página](assets/create-page.png)

1. Selecione **Marca** como modelo do site e clique em **Próximo**.

   ![Criar marca](assets/create-brand.png)

1. Insira um **Título**, clique em **Criar** e depois em **Concluído**.

   ![Fornecer detalhes da marca](assets/create-brand-page.png)

Agora você tem uma estrutura básica de conteúdo para criar as suas campanhas.

![Estrutura de conteúdo](assets/content-structure.png)

## Criar uma campanha {#create-campaign}

Agora que você tem uma estrutura básica de conteúdo para a sua campanha, você pode criar a campanha em si. A campanha será usada para organizar, possivelmente, vários informativos.

1. Usando a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) no console Sites, selecione a marca criada anteriormente (nesse caso, **WKND Escapes**) e depois selecione a **Área principal**, que foi criada automaticamente para você. Em seguida, clique no botão **Criar** e depois em **Página**.

   ![Criar página de campanha](assets/create-campaign-page.png)

1. Selecione **Campanha** como o modelo e clique em **Próximo** e **Concluído**.

   ![Selecionar modelo de campanha](assets/select-campaign-template.png)

1. Insira um **Título** para a campanha e clique em **Criar** e **Concluído**.

   ![Título da campanha](assets/campaign-title.png)

Agora você tem uma campanha onde pode criar seus informativos.

![Estrutura da campanha](assets/campaign-structure.png)

## Selecionar configuração da campanha {#campaign-configuration}

O AEM é compatível com várias configurações de integração. Na sua nova campanha, é preciso definir quais configurações você usará para enviar o conteúdo do informativo.

1. Usando a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) no console Sites, localize a campanha criada anteriormente (nesse caso, **Campanha de verão WKND Escape**), selecione-a usando a caixa de seleção e depois clique no botão **Propriedades** na barra de ferramentas.

   ![Selecionar campanha](assets/select-campaign.png)

1. Na janela **Propriedades**, selecione a guia **Cloud Service** para definir a integração a ser usada com essa campanha.

   * Selecione o **Adobe Campaign** na lista suspensa **Configurações de Cloud Service**.
   * Selecione a configuração de integração do Adobe Campaign desejada na lista suspensa **Adobe Campaign**.
   * Clique em **Salvar e fechar**.

   ![Propriedades de configuração da campanha](assets/campaign-configuration-properties.png)

Sua campanha agora está vinculada à integração do Adobe Campaign. Agora você está pronto para criar um informativo no AEM e enviá-lo com o Adobe Campaign.

## Criar um informativo {#create-newsletter}

Crie e gerencie seus informativos na estrutura de conteúdo da campanha que você já criou e configurou.

1. Usando a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) no console Sites, localize a campanha configurada anteriormente (neste caso, **Campanha de verão WKND Escape**), selecione-a, clique no botão **Criar** e depois em **Página**.

   ![Criar informativo](assets/create-newsletter.png)

1. No assistente de criação de página, selecione o modelo **Email do Adobe Campaign (AC 6.1)** e clique em **Próximo**.

   ![Selecionar modelo de email da campanha](assets/adobe-campaign-email-template.png)

1. Na etapa **Propriedades** do assistente, insira o **Título** do informativo, clique em **Criar** e **Abrir**.

   ![Título do informativo](assets/create-newsletter-wizard-properties.png)

1. Edite a página do informativo como faria com qualquer outra página de conteúdo do AEM para atender às suas necessidades.

Agora você tem um informativo pronto para enviar com o Adobe Campaign.

## Publicar seu informativo {#publishing-newsletter}

Você deve publicar o seu informativo para disponibilizá-lo para envio no Adobe Campaign.

1. Usando a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) no console Sites, localize o informativo criado anteriormente (neste caso, **Primeiro boletim informativo para a campanha de verão WKND Escape**), selecione-o, clique no botão **Informações da página** no canto superior esquerdo e clique em **Publicar página**.

1. Selecione as configurações de publicação da página e clique em **Publicar**.

   ![Publicar página](assets/publish.png)

A página do informativo agora está publicada na instância de publicação do AEM e está visível no Adobe Campaign Classic. Para poder selecioná-la no Adobe Campaign, ela deve ser aprovada.

1. Clique no botão **Informações da página** do informativo mais uma vez e selecione **Iniciar fluxo de trabalho**.

1. Selecione **Aprovar para o Adobe Campaign** como o modelo de fluxo de trabalho (opcionalmente, forneça uma descrição) e clique no botão **Iniciar fluxo de trabalho**.

   ![Iniciar fluxo de trabalho](assets/start-workflow.png)

1. Um banner é exibido na parte superior do editor de página do informativo, fornecendo as próximas etapas do processo de aprovação. Clique em **Concluído**.

   ![Aprovar fluxo de trabalho](assets/approve-workflow.png)

1. Na caixa de diálogo **Item de trabalho concluído**, selecione a **Revisão do informativo (Administrador)** na lista suspensa **Próxima etapa** e clique no botão **OK**.

   ![Revisão do informativo](assets/newsletter-review.png)

1. No banner exibido na parte superior do editor de página do informativo, clique novamente em **Concluído**.

1. Na caixa de diálogo **Item de trabalho concluído**, selecione a **Aprovação de informativo** na lista suspensa **Próxima etapa** e clique no botão **OK**.

   ![Aprovação do informativo](assets/newsletter-approval.png)

1. Quando a caixa de diálogo é fechada, o banner exibido na parte superior do editor de página do informativo desaparece porque o fluxo de trabalho de aprovação foi concluído.

O informativo agora está publicado no AEM e aprovado para uso no Adobe Campaign.

>[!TIP]
>
>As etapas do fluxo de trabalho descritas aqui foram simplificadas para ilustrar o processo. Em um fluxo de trabalho normal, as etapas de criação e aprovação do informativo normalmente têm diferentes funções
>
>Consulte o documento [Trabalhar com fluxos de trabalho](/help/sites-cloud/authoring/workflows/overview.md) para obter mais detalhes sobre o uso de fluxos de trabalho.

## Criar um destinatário {#creating-recipient}

Para enviar o informativo criado no AEM, você deve primeiro definir os destinatários no Adobe Campaign Classic.

1. Faça logon no Adobe Campaign Classic usando o console do cliente.

1. Selecione **Ferramentas** -> **Explorador** na barra de menus.

1. No explorador, navegue até o nó **Perfis e destinos** -> **Destinatários**.

   ![Destinatários](assets/recipients.png)

1. Clique em **Novo** na barra de ferramentas e forneça os detalhes do destinatário.

   * Nome
   * Sobrenome
   * Endereço de e-mail

1. Clique em **Salvar**.

Agora você tem um destinatário para o qual enviar seu informativo usando o Adobe Campaign Classic.

## Criar uma entrega de email {#create-delivery}

A etapa final é enviar o informativo criado no AEM ao destinatário adicionado no Adobe Campaign Classic.

1. Faça logon no Adobe Campaign Classic usando o console do cliente.

1. Selecione **Ferramentas** -> **Explorador** na barra de menus.

1. No explorador, navegue até o nó **Gerenciamento de campanhas** -> **Entregas** e clique em **Novo**.

   ![Entrega de conteúdo do AEM](assets/delivery-aem-content.png)

1. Na caixa de diálogo de **Entrega**, selecione **Entrega de email com conteúdo do AEM** como o **Modelo de entrega** na lista suspensa e clique em **Continuar**.

   ![Entrega de conteúdo do AEM](assets/aem-content-delivery.png)

1. Na seção **Parâmetros de email**, clique no link **De**, insira as informações do remetente e clique em **OK**.

   * Endereço do remetente
   * Campo “De”

   ![Definir campo “De”](assets/delivery-from.png)

1. Na seção **Parâmetros de email**, clique no link **Para**, que abrirá a caixa de diálogo **Selecionar destino** e, em seguida, clique em **Adicionar**.

   ![Selecionar destino](assets/select-target.png)

1. Na caixa de diálogo **Selecionar elemento de destino**, selecione **Um destinatário** e clique em **Próximo**.

   ![Selecionar elemento de destino](assets/select-target-element.png)

1. Usando os filtros, selecione o destinatário que você [criou anteriormente](#creating-recipient) e clique em **Concluir**.

   ![Selecionar destinatário](assets/select-target-element-recipient.png)

1. De volta à caixa de diálogo **Selecionar destino**, clique em **OK**.

1. Na janela de entrega, clique em **Sincronizar**.

   ![Sincronizar](assets/synchronize.png)

1. Na caixa de diálogo **Sincronizar com conteúdo do AEM**, selecione na lista o informativo criado anteriormente e clique em **OK**.

1. O conteúdo de email do Adobe Campaign é sincronizado com o conteúdo do informativo criado no AEM.

   * Clique em **Atualizar conteúdo** se o conteúdo não for carregado automaticamente.

1. Clique em **Enviar** para enviar o email.

1. Na caixa de diálogo **Enviar para o destino de entrega principal**, selecione **Enviar assim que possível** e, em seguida, clique em **Analisar**.

   ![Análise da entrega](assets/delivery-analysis.png)

1. A etapa de análise cria a entrega, combinando o conteúdo com os destinatários. Agora que a entrega foi criada, clique em **Confirmar entrega** para enviar o email. Clique em **Sim** para confirmar.

1. A entrega foi iniciada. Clique em **Fechar**.

   ![Entrega](assets/delivering.png)

1. Clique em **Salvar** para salvar a entrega.

Seu informativo foi enviado.

>[!TIP]
>
>Este exemplo mostrou uma entrega simplificada de um informativo a um único destinatário. É claro que uma entrega normal conteria muitos destinatários diferentes, porém o Adobe Campaign facilita o gerenciamento dessa tarefa. Consulte a [Documentação do Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR) para obter mais detalhes sobre entrega e gestão de destinatários.
