---
title: Compartilhar ativos, pastas e coleções como um link
description: Este artigo descreve como compartilhar ativos, pastas e coleções nos ativos do Experience Manager como um hiperlink.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Compartilhar e distribuir ativos gerenciados no Experience Manager {#share-assets-from-aem}

Os ativos Adobe Experience Manager (AEM) permitem que você compartilhe ativos, pastas e coleções com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. Você pode usar os seguintes métodos para compartilhar ativos dos Ativos do Experience Manager como um Serviço em nuvem:

* Compartilhar como um link
* Baixar ativos
* Compartilhar via aplicativo de desktop do AEM
* Compartilhar via Adobe Asset Link
* (Funcionalidade futura) Compartilhar usando o Brand Portal

## Compartilhar ativos como um link {#sharelink}

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem visualização os links compartilhados com eles. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon nos ativos AEM.

>[!NOTE]
>
>* Você precisa da permissão Editar ACL na pasta ou no ativo que deseja compartilhar como um link.
>* Antes de compartilhar um link com os usuários, verifique se o Day CQ Mail Service está configurado. Caso contrário, ocorrerá um erro.


1. Na interface do usuário Ativos, selecione o ativo a ser compartilhado como um link.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Compartilhar link]**.

   Um link de ativo é criado automaticamente no campo **[!UICONTROL Compartilhar link]** . Copie este link e compartilhe-o com os usuários. A hora de expiração padrão do link é um dia.

   Como alternativa, prossiga para executar as etapas 3 a 7 desse procedimento para adicionar recipient de e-mail, configurar o tempo de expiração do link e enviá-lo da caixa de diálogo.

   >[!NOTE]
   >
   >Se um ativo compartilhado for movido para um local diferente, seu link para de funcionar. Recrie o link e compartilhe-o novamente com os usuários.

1. No console da Web, abra a configuração do **[!UICONTROL Day CQ Link Externalizer]** e modifique as seguintes propriedades no campo **[!UICONTROL Domínios]** com os valores mencionados em relação a cada:

   * local
   * author
   * publicação
   Para as propriedades local e autor, forneça o URL para as instâncias local e autor, respectivamente. As propriedades local e de autor têm o mesmo valor se você executar uma única instância de autor de AEM. Para publicar, forneça o URL da instância de publicação.

1. Na caixa de endereço de email da caixa de diálogo **[!UICONTROL Compartilhamento de links]**, digite a ID de email do usuário com o qual deseja compartilhar o link. Além disso, é possível compartilhar o link com vários usuários.

   Se o usuário for membro de sua organização, selecione a ID de email do usuário nas IDs de email sugeridas que aparecem na lista abaixo da área de digitação. Para um usuário externo, digite a ID de email completa e selecione-a na lista.

   Para permitir o envio de emails para usuários, configure os detalhes do servidor SMTP no [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >Se você inserir uma ID de email de um usuário que não seja membro de sua organização, as palavras &quot;Usuário externo&quot; receberão o prefixo ID de email do usuário.

1. Na caixa **[!UICONTROL Assunto]** , informe um assunto para o ativo que deseja compartilhar.
1. Na caixa **[!UICONTROL Mensagem]** , digite uma mensagem opcional.
1. No campo **[!UICONTROL Expiração]** , especifique uma data e hora de expiração para o link usando o seletor de datas. Por padrão, a data de expiração é definida para uma semana a partir da data em que você compartilha o link.
1. Para permitir que os usuários baixem a imagem original junto com as execuções, selecione **[!UICONTROL Permitir download do arquivo]** original.

   >[!NOTE]
   >
   >Por padrão, os usuários podem baixar somente as representações do ativo que você compartilha como um link.

1. Clique em **[!UICONTROL Compartilhar]**. Uma mensagem confirma que o link é compartilhado com os usuários por meio de um email.
1. Para visualização do ativo compartilhado, clique/toque no link no email enviado ao usuário. O ativo compartilhado é exibido na página da **[!UICONTROL Adobe Marketing Cloud]** .

   Para alternar para a visualização da lista, clique/toque no ícone de layout na barra de ferramentas.

1. Para gerar uma visualização do ativo, clique/toque no ativo compartilhado. Para fechar a visualização e retornar à página da **[!UICONTROL Experience Cloud]**, clique/toque em **[!UICONTROL Voltar]** na barra de ferramentas. Se tiver compartilhado uma pasta, clique/toque em **[!UICONTROL Pasta pai]** para retornar à pasta principal.

   >[!NOTE]
   >
   >O AEM oferece suporte à geração de pré-visualização de ativos desses tipos MIME: JPG, PNG, GIF, BMP, INDD, PDF e PPT. Você só pode baixar os ativos dos outros tipos MIME.

1. Para baixar o ativo compartilhado, clique/toque em **[!UICONTROL Selecionar]** na barra de ferramentas, clique/toque no ativo e, em seguida, clique/toque em **[!UICONTROL Download]** na barra de ferramentas.
1. Para visualização dos ativos compartilhados como links, vá para a interface do usuário Ativos e clique/toque no ícone GlobalNav. Escolha **[!UICONTROL Navegação]** na lista para exibir o painel de Navegação.
1. No painel Navegação, escolha **[!UICONTROL Links compartilhados]** para exibir uma lista de ativos compartilhados.
1. Para descompartilhar um ativo, selecione-o e toque/clique em **[!UICONTROL Descompartilhar]** na barra de ferramentas.

Uma mensagem confirma que você não compartilhou o ativo. Além disso, a entrada do ativo é removida da lista.

## Baixar e compartilhar ativos {#download-and-share-assets}

Os usuários podem baixar alguns ativos e compartilhá-los fora do Experience Manager. Para obter mais informações, consulte [como pesquisar ativos](/help/assets/search-assets.md), [como baixar ativos](/help/assets/download-assets-from-aem.md)e [como baixar coleções](manage-collections.md#download-a-collection)

## Compartilhar ativos com profissionais de criação {#share-with-creatives}

Os profissionais de marketing e os usuários de linha de negócios podem facilmente compartilhar ativos aprovados com seus profissionais criativos usando,

* **Aplicativo** para desktop AEM: O aplicativo funciona no Windows e no Mac. Consulte Visão geral [do aplicativo para](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)desktop. Para saber como qualquer usuário autorizado do desktop pode acessar facilmente os ativos compartilhados, consulte [procurar, pesquisar e pré-visualização dos ativos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Os usuários da área de trabalho podem criar novos ativos e compartilhá-los de volta com seus colegas que são usuários do AEM, por exemplo, fazendo upload de novas imagens. Consulte [fazer upload de ativos usando o aplicativo](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)para desktop.

* **Link** do ativo da Adobe: Os profissionais criativos podem pesquisar e usar ativos diretamente do Adobe InDesign, Adobe Illustrator e Adobe Photoshop.

### Best practices and troubleshooting {#bestpractices}

* Pastas de ativos ou coleções que contêm um espaço em branco em seu nome podem não ser compartilhadas.
* Se os usuários não puderem baixar os ativos compartilhados, verifique com o administrador do AEM quais são os limites [de](/help/assets/configure-asset-sharing.md#maxdatasize) download.
* Se você não puder enviar emails com links para ativos compartilhados ou se os outros usuários não puderem receber seu email, verifique com o administrador do AEM se o serviço [de](/help/assets/configure-asset-sharing.md#configmailservice) email está configurado ou não.
* Se você não puder compartilhar ativos usando a funcionalidade de compartilhamento de links, verifique se você tem as permissões apropriadas. Consulte [compartilhar ativos](#sharelink).

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
