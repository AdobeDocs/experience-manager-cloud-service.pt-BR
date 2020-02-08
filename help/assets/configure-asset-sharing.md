---
title: Compartilhar ativos, pastas e coleções como um link
description: Este artigo descreve como compartilhar ativos, pastas e coleções nos ativos do Experience Manager como um hiperlink.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Configurar compartilhamento de links de ativos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem exibir os links compartilhados com eles. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon nos ativos AEM.

>[!NOTE]
>
>Se você quiser compartilhar links da instância do autor de AEM com entidades externas, certifique-se de expor apenas os seguintes URLs para `GET` solicitações. Bloqueie outros URLs para garantir que sua instância do autor de AEM esteja segura.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Configurar o serviço de correio Day CQ {#configmailservice}

Antes de compartilhar ativos como links, configure o serviço de email.

1. Clique ou toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web.
1. Na lista de serviços, localize o **[!UICONTROL Dia CQ Mail Service]**.
1. Clique no ícone **[!UICONTROL Editar]** ao lado do serviço e configure os seguintes parâmetros para o **Day CQ Mail Service]** com os detalhes mencionados em relação a seus nomes:

   * Nome do host do servidor SMTP: nome do host do servidor de email
   * Porta do servidor SMTP: porta do servidor de email
   * Usuário SMTP: nome de usuário do servidor de email
   * Senha SMTP: senha do servidor de email

1. Click/tap **Save**.

## Configurar tamanho máximo de dados {#maxdatasize}

Quando você baixa ativos do link compartilhado usando o recurso Compartilhamento de link, o AEM compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que pode ser compactada em um arquivo ZIP, grandes quantidades de dados são submetidas à compactação, o que causa erros de memória esgotada no JVM. Para proteger o sistema de um possível ataque de negação de serviço devido a essa situação, configure o tamanho máximo usando o parâmetro **Máximo de tamanho de conteúdo (descompactado)** para o Servlet Proxy de compartilhamento de ativos ad hoc Day CQ DAM no Configuration Manager. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download do ativo serão rejeitadas. O valor padrão é 100 MB.

1. Clique/toque no logotipo do AEM e vá até **Ferramentas** > **Operações** > Console **da** Web.
1. No console da Web, localize a configuração do Servlet **Adhoc de Compartilhamento de ativos Ad hoc do** Day CQ DAM.
1. Abra a configuração do Servlet **Proxy de Compartilhamento Atual de Ativos Ad hoc do** Dia CQ DAM no modo de edição e modifique o valor do parâmetro Tamanho **Máximo de Conteúdo (descompactado)** .
1. Salve as alterações.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
