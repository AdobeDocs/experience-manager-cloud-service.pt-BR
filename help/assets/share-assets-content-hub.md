---
title: Compartilhar Assets em  [!DNL the Content Hub]
description: Compartilhar Assets em  [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 12bb550ff275c84bc60869e91e953993aab57aa5
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Compartilhar ativos na Content Hub {#search-assets-as-a-link}

Crie um link para ativos selecionados para compartilhá-los facilmente com outras pessoas. Como usuário autorizado do [!DNL Content Hub], selecione um ou mais ativos disponíveis no ambiente [!DNL Content Hub], gere um link e envie-o para outros usuários públicos ou privados.

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## Pré-requisitos {#prerequisites}

[Os usuários do Content Hub](deploy-content-hub.md#onboard-content-hub-users) podem criar um link para os ativos selecionados e compartilhá-lo com outros usuários.

## Compartilhar ativos {#share-assets}

Para compartilhar um ou mais ativos com usuários privados ou públicos, execute as seguintes etapas:

1. Navegue até a página inicial do [!DNL Content Hub], selecione um ou mais ativos e clique em ![Compartilhar](/help/assets/assets/share.svg) **[!UICONTROL Compartilhar]** para exibir um único ativo selecionado ou uma lista de vários ativos selecionados na caixa de diálogo **[!UICONTROL Compartilhar ativos]**.

   Você também pode selecionar e compartilhar ativos disponíveis em ![coleções](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL Coleções]**.

1. Exiba um ativo ou revise a lista de ativos disponíveis na caixa de diálogo **[!UICONTROL Compartilhar ativos]**. Clique em ![desmarcar](/help/assets/assets/Close.svg) ao lado de um ativo para removê-lo da lista.

1. Especifique um título e uma descrição opcional que defina o conjunto de ativos selecionados.

1. Selecione **[!UICONTROL Período de expiração]**.

1. Em **[!UICONTROL Quem pode acessar]**, selecione as opções de acesso e clique em **[!UICONTROL Obter link]** para gerar um link para compartilhar com os usuários selecionados. Os usuários privados precisam entrar no ambiente [!DNL Content Hub] para acessar a página de ativos compartilhados. Enquanto isso, os usuários públicos, como convidados, podem acessar a página de ativos compartilhados sem entrar no [!DNL Content Hub].

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![link privado e público](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [Habilite o compartilhamento de link público na página de configuração](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) para exibir a opção **[!UICONTROL Link público]** na caixa de diálogo **[!UICONTROL Compartilhar ativos]**.

## Compartilhar um ativo da página de visualização {#share-asset-from-preview-page}

Execute as seguintes etapas para compartilhar um ativo ao pré-visualizá-lo:

1. Navegue até a página inicial do [!DNL Content Hub] e clique na miniatura do ativo para visualizar o ativo e exibir as opções de menu no painel direito da caixa de diálogo.
1. Selecione ![compartilhar](/help/assets/assets/share.svg) para exibir o painel **[!UICONTROL Compartilhar]**.
   ![compartilhar ativo ao visualizá-lo](/help/assets/assets/share-link-asset-preview.png)
1. Siga as etapas de 3 a 5 na seção [Compartilhar ativos](#share-assets) para gerar e compartilhar o link de ativos (Privado ou público) neste painel **[!UICONTROL Compartilhar]**.

## Acessar os ativos compartilhados {#access-shared-assets}

Acesse a página de ativos compartilhados por meio do link e faça o seguinte:

* Selecione um ou mais ativos e clique em ![Baixar](/help/assets/assets/download-icon.svg) **[!UICONTROL Baixar]** para selecionar as representações **[!UICONTROL Original]**, **[!UICONTROL Estático]** ou ambas das opções de download disponíveis.
  ![](/help/assets/assets/download-shared-assets.png)
* Clique na miniatura do ativo para ver os metadados do ativo.
* Na página de ativos compartilhados ([acessada por meio de um link privado](#share-assets)), clique em uma miniatura de ativo e selecione ![baixar](/help/assets/assets/download-icon.svg) para selecionar e exibir as representações dinâmicas disponíveis do ativo no painel **[!UICONTROL Baixar]** antes de selecioná-las e baixá-las.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## Perguntas frequentes {#faqs-share-assets-content-hub}

### O que significa compartilhar ativos no AEM Assets Content Hub?

O compartilhamento de ativos no AEM Assets Content Hub permite que usuários autorizados compartilhem facilmente um ou mais ativos ou coleções inteiras com outros gerando um link. Esse link pode ser enviado para usuários privados (que devem fazer logon) ou públicos (que podem acessar como convidados), dando aos destinatários acesso direto para exibir e baixar os ativos selecionados.

### Como faço para compartilhar ativos ou coleções com outras pessoas usando o AEM Assets Content Hub?

Para compartilhar ativos ou coleções no Content Hub, navegue até a página inicial do Content Hub, selecione um ou mais ativos (ou acesse a guia Coleções para coleções) e clique no ícone Compartilhar. Na caixa de diálogo Compartilhar, você pode visualizar os ativos, remover qualquer um, se necessário, adicionar um título e descrição, selecionar quem pode acessar o link (privado ou público), definir um período de expiração e, em seguida, clicar em Obter link para gerar e copiar o URL compartilhável. O link pode ser enviado para os membros da equipe ou para as partes interessadas.

### Quais opções de acesso estão disponíveis ao compartilhar ativos no AEM Assets Content Hub e como elas se diferem?

O Content Hub permite escolher entre duas opções de acesso para links compartilhados: privado e público. Os links privados exigem que os recipients façam logon no ambiente do Content Hub para visualizar e baixar ativos, fornecendo segurança adicional. Links públicos podem ser acessados por qualquer pessoa com o link, sem a necessidade de entrar. Cada tipo de link vem com suas próprias configurações de expiração, como de 24 horas a uma semana para links públicos e datas personalizadas para links privados.

### Existe alguma configuração gerenciada pelo administrador para gerar links públicos para ativos no AEM Assets Content Hub?

Sim, os administradores podem habilitar ou desabilitar a opção **Habilitar Link Público**, disponível na guia **Coleções e Compartilhamento** da interface de Configuração, para gerenciar a geração de links públicos para ativos no AEM Assets Content Hub.

### Posso definir datas de expiração para links de ativos compartilhados no AEM Assets Content Hub e por que isso é importante?

Sim, você pode definir datas de expiração para links compartilhados privados e públicos no Content Hub. Para links públicos, é possível escolher entre predefinições, como 24 horas e uma semana, enquanto links privados permitem selecionar entre predefinições ou definir uma data de expiração personalizada. As datas de expiração são importantes porque, quando o link expira, ele não pode mais ser usado para acessar ou baixar os ativos, o que ajuda a manter a segurança e o controle do conteúdo.

### O que os recipients podem fazer com o link de ativo compartilhado criado usando o AEM Assets Content Hub e há opções para baixar diferentes representações?

Os recipients que recebem um link de ativo compartilhado podem abri-lo no navegador para visualizar, selecionar e baixar os ativos fornecidos. Se as representações de ativos estiverem ativadas no Content Hub, os destinatários poderão escolher quais representações (como Original ou Estático) desejam baixar. Os ativos e as representações são baixados como um arquivo zip e os metadados podem ser visualizados clicando na miniatura do ativo. O link permanece funcional até sua data de expiração definida.




