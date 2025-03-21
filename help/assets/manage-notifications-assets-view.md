---
title: Gerenciar notificações
description: Monitore as operações realizadas nos ativos ou pastas disponíveis no repositório usando as notificações de exibição do Assets.
exl-id: 1fe6a845-37d5-43c2-bb96-c5b149c238ab
feature: Assets Essentials
role: User, Leader
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 66%

---

# Monitorar ativos, pastas e coleções {#watch-assets-folders}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

As notificações de exibição do Assets permitem monitorar as operações realizadas nos ativos, pastas ou coleções disponíveis no repositório. Você precisa selecionar e assinar o conteúdo sobre o qual deseja receber notificações. Você também pode configurar as categorias para as quais receberá notificações.

## Assinar categorias de notificação {#subscribe-to-notification-categories}

Você pode assinar e escolher dentre uma lista de categorias para as quais receberá notificações. A visualização Assets envia notificações somente para as categorias selecionadas dentre as opções disponíveis:

<table>
    <tbody>
     <tr>
      <th><strong>Categoria de notificação</strong></th>
      <th><strong>Descrição</strong></th>
     </tr>
     <tr>
      <td>Solicitações</td>
      <td>Ao atribuir uma tarefa a um usuário, você recebe notificações quando esse usuário executa ações nessa tarefa.</td>
     </tr>
     <tr>
      <td>Atribuído a mim</td>
      <td>Você recebe uma notificação quando há uma tarefa atribuída a você por outro usuário.</td>
     </tr>
     <tr>
      <td>Comentário sobre o conteúdo assinado</td>
      <td>Você recebe uma notificação quando um usuário comenta no ativo que você assinou.</td>
     </tr>
     <tr>
      <td>Exclusão do conteúdo assinado</td>
      <td>Você recebe uma notificação quando um usuário exclui o ativo, pasta ou coleção que você assinou.</td>
     </tr>
     <tr>
      <td>Compartilhamento externo do conteúdo assinado</td>
      <td>Você recebe uma notificação quando um usuário gera um link público para o ativo, pasta ou coleção que você assinou.</td>
     </tr>
     <tr>
      <td>Modificação do conteúdo assinado</td>
      <td>Você recebe uma notificação quando um usuário cria uma nova versão do ativo que você assinou.</td>
     </tr>
     <tr>
      <td>Mover/renomear o conteúdo assinado</td>
      <td>Você recebe uma notificação quando um usuário move ou renomeia o ativo ou pasta que você assinou.</td>
     </tr>
     <tr>
      <td>Atualizações em pastas e coleções assinadas</td>
      <td>Você recebe uma notificação quando um usuário adiciona ou remove um ativo de uma pasta ou coleção que você assinou.</td>
     </tr>    
    </tbody>
   </table>

Para assinar as categorias de notificação:

1. Clique em ![ícone de sino](assets/bell-icon.svg) na extremidade direita da barra de menus da interface de usuário do Assets View.

1. Clique no ![ícone de configurações](assets/settings-icon.svg) para visualizar a página [!UICONTROL Preferências da Experience Cloud].

1. Clique na opção **[!UICONTROL Notificações]** disponível no painel esquerdo.

1. Na seção **[!UICONTROL Notificações]**, navegue até a seção [!UICONTROL Modo de Exibição do Assets] e verifique se a opção está definida como ATIVADO.

   ![Notificações no modo de exibição Assets](assets/enable-notifications.png)

1. Clique em **[!UICONTROL Personalizar]** para visualizar as categorias de notificação.
   ![Notificações no modo de exibição Assets](assets/enable-notification-categories.png)

1. Selecione as categorias de notificação sobre as quais você precisa ser notificado.

## Observar e deixar de observar pastas, ativos ou coleções {#watch-unwatch-assets}

Depois de [assinar as categorias de notificação](#subscribe-to-notification-categories), você deve assinar o conteúdo para começar a receber notificações.

>[!NOTE]
>
>* Para as categorias de notificação **[!UICONTROL Solicitações]** e **[!UICONTROL Atribuído a mim]**, não é necessário assinar o conteúdo após ter assinado as categorias de notificação. Você recebe notificações automaticamente sobre solicitações que criou e quando uma tarefa é atribuída a você.
>* A exibição do Assets envia notificações somente quando outros usuários executam ações no conteúdo assinado. Você não recebe notificações para ações que você executou no conteúdo assinado.

Para assinar o conteúdo, selecione a pasta, ativo ou coleção que você precisa assinar e clique em **[!UICONTROL Observar]**.

A visualização do Assets exibe uma mensagem de sucesso. Você pode clicar em **[!UICONTROL Ir para as preferências de notificação]** disponível na mensagem de sucesso para editar a [assinatura de categorias de notificação](#subscribe-to-notification-categories).

![Notificações no modo de exibição Assets](assets/watch-assets.png)

A exibição do Assets agora envia notificações para as categorias que você assinou. Você também pode selecionar vários ativos, pastas ou coleções e clicar em **[!UICONTROL Observar]** para economizar tempo. No entanto, se você selecionar várias entidades, dentre as quais algumas você já assinou algumas, a opção **[!UICONTROL Observar]** não é exibida.

De maneira similar, para cancelar a assinatura, selecione o ativo, pasta ou coleção que você assinou e clique em **[!UICONTROL Deixar de observar]**.

## Visualizar notificações {#view-notifications}

As notificações são exibidas na extremidade direita da barra de menus da interface de usuário de visualização do Assets.

![Notificações no modo de exibição Assets](assets/notifications-assets-essentials.png)

Ao clicar em uma notificação, a visualização Assets navega até o ativo ou pasta apropriada que é referenciado na notificação.
