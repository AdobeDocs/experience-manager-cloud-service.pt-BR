---
title: Gerenciar ativos de vídeo
description: Carregar, visualizar, anotar e publicar ativos de vídeo no [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '4983'
ht-degree: 6%

---

# Gerenciar ativos de vídeo {#manage-video-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. O [!DNL Adobe Experience Manager] oferece ofertas e recursos completos para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo no [!DNL Adobe Experience Manager Assets]. A codificação e transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando Perfis de Processamento e a integração [!DNL Dynamic Media]. Sem a licença do [!DNL Dynamic Media], o [!DNL Experience Manager] oferece suporte básico a vídeos, como transcodificação usando FFmpeg, extração de miniaturas de visualização para os formatos de arquivo com suporte e visualização na interface de usuário para formatos com suporte para reprodução diretamente no navegador.

## Fazer upload e pré-visualizar ativos de vídeo {#upload-and-preview-video-assets}

Você pode carregar e visualizar ativos de vídeo de formato compatível para [!DNL Experience Manager Assets].
<!-- It generates previews for video assets with the extension MP4. -->

### Fazer upload de ativos de vídeo

Para fazer upload de um ativo de vídeo, siga estas etapas:

1. Na pasta ou subpastas de ativos digitais, navegue até o local em que você precisa adicionar o ativo.
1. Clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. <br>Como alternativa, arraste um arquivo para a interface.
Saiba mais sobre [como carregar ativos](manage-digital-assets.md#uploading-assets) no [!DNL Experience Manager Assets].

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### Visualizar ativos de vídeo

Você pode visualizar vídeos em representações com suporte na interface do usuário do [!DNL Assets]. Para visualizar um ativo de vídeo, siga estas etapas:

1. Carregue um ativo de vídeo com formato compatível para [!DNL Experience Manager Assets]. Saiba mais sobre os [formatos de vídeo compatíveis](file-format-support.md#video-formats). <br>Depois de carregado, o ativo de vídeo é processado e uma representação de pré-visualização é gerada.
1. Clique no ativo e selecione ![opção de detalhes](assets/do-not-localize/details_icon.svg) **[!UICONTROL Detalhes]** na barra de ferramentas superior. O ativo de vídeo é aberto no visualizador de vídeo.
1. Clique no ícone da ![opção de reprodução](assets/do-not-localize/play.png) na miniatura do vídeo. <br>Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela inteira.

Para ativos de vídeo existentes no [!DNL Experience Manager Assets], é necessário **[!UICONTROL Reprocessar]** os ativos no [!DNL Experience Manager] para habilitar o recurso de visualização de vídeo. Saiba como [reprocessar ativos digitais](reprocessing.md) no [!DNL Experience Manager].

### Limitações da pré-visualização de vídeo

* Os arquivos MXF não mostram visualizações de vídeo, mesmo que a representação seja gerada.
* Os arquivos WebM não geram representações de pré-visualização, pois podem ser reproduzidos nativamente por navegadores da Web.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, você pode incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar [!DNL Dynamic Media] ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Publicar vídeos no YouTube {#publishing-videos-to-youtube}

Você pode publicar ativos de vídeo gerenciados no Experience Manager Assets diretamente em um canal do YouTube criado anteriormente.

Para publicar ativos de vídeo no YouTube, você marca ativos de vídeo no Experience Manager Assets com tags. Você associa essas tags a um canal do YouTube. Se a tag de um ativo de vídeo corresponder à tag de um canal do YouTube, o vídeo será publicado no YouTube. A publicação na YouTube ocorre junto com uma publicação normal do vídeo, desde que uma tag associada seja usada.

O YouTube faz sua própria codificação. Dessa forma, o arquivo de vídeo original carregado no Experience Manager é publicado no YouTube, em vez de qualquer representação de vídeo criada pela codificação do Dynamic Media. Embora não seja necessário processar vídeos usando o Dynamic Media, espera-se que eles façam isso caso uma predefinição do visualizador seja necessária para a reprodução.

Ao ignorar o perfil de processamento de vídeo e publicar diretamente no YouTube, isso significa simplesmente que o ativo de vídeo no Experience Manager Asset não recebe uma miniatura visualizável. Também significa que os vídeos não codificados não funcionam com nenhum dos tipos de ativo do Dynamic Media.

A publicação de ativos de vídeo em servidores da YouTube envolve a conclusão das seguintes tarefas para garantir uma verificação segura de servidor para servidor com o YouTube:

1. [Definir configurações da Google Cloud](#configuring-google-cloud-settings)
1. [Criar um canal do YouTube](#creating-a-youtube-channel)
1. [Adicionar tags para publicação](#adding-tags-for-publishing)
1. [Configurar o YouTube no Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatize a configuração das propriedades padrão do YouTube para os vídeos carregados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicar vídeos no seu canal do YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verifique o vídeo publicado no YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincular URLs do YouTube à sua aplicação web](#linking-youtube-urls-to-your-web-application)

Você também pode [cancelar a publicação de vídeos para removê-los do YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Definir configurações da Google Cloud {#configuring-google-cloud-settings}

Para publicar no YouTube, você precisa de uma conta do Google. Se você tiver uma conta do GMAIL, já terá uma conta do Google; se não tiver uma conta do Google, poderá criar facilmente uma. Você precisa da conta porque precisa de credenciais para publicar ativos de vídeo no YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

A conta usada com a Google Cloud e a conta do Google usada para o YouTube não precisam ser a mesma.

A Google altera periodicamente a interface do usuário. Dessa forma, as etapas para publicar vídeos no YouTube podem variar um pouco do que está documentado abaixo. Esse aviso também se aplica ao YouTube quando você tenta verificar se os vídeos foram carregados para ele.

>[!NOTE]
>
>As etapas a seguir eram precisas no momento da escrita. No entanto, a Google atualiza periodicamente suas páginas da Web em nuvem sem aviso prévio. Dessa forma, algumas opções de configuração podem ser nomeadas de forma um pouco diferente na interface do usuário do Google do nome usado nas etapas.

**Para definir as configurações da Google Cloud:**

1. Crie uma conta do Google.

   Se você já tiver uma conta do Google, pule para a próxima etapa.

1. Ir para [https://cloud.google.com/](https://cloud.google.com/).
1. Na página **[!UICONTROL Google Cloud]**, próximo ao canto superior direito, selecione **[!UICONTROL Console]**.

   Se necessário, **[!UICONTROL Entre]** usando suas credenciais de conta da Google para ver a opção **[!UICONTROL Console]**.

1. Na página **[!UICONTROL Painel]**, à direita de **[!UICONTROL Google Cloud Platform]**, selecione a lista suspensa **[!UICONTROL Projeto]** para abrir a caixa de diálogo **[!UICONTROL Selecionar um projeto]**.
1. Na caixa de diálogo **[!UICONTROL Selecionar um projeto]**, selecione **[!UICONTROL Novo Projeto]**.
1. Na caixa de diálogo **[!UICONTROL Novo Projeto]**, no campo **[!UICONTROL Nome do projeto]**, digite o nome do novo projeto.

   A ID do projeto é baseada no nome do projeto. Sendo assim, escolha o nome do projeto com cuidado; ele não poderá ser alterado após sua criação. Além disso, você deve inserir a mesma ID de projeto novamente ao configurar o YouTube no Experience Manager posteriormente. Portanto, anote.

1. Selecione **[!UICONTROL Criar]**.

1. Siga um destes procedimentos:

   * No painel do seu projeto, no cartão **[!UICONTROL Introdução]**, selecione **[!UICONTROL Explorar e habilitar APIs]**.
   * No Painel do seu projeto, no cartão **[!UICONTROL APIs]**, selecione **[!UICONTROL Ir para a visão geral das APIs]**.

1. Próximo ao meio superior da página **[!UICONTROL APIs e serviços]**, selecione **[!UICONTROL HABILITAR APIS E SERVIÇOS]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. Na página **[!UICONTROL Biblioteca de API]**, no lado esquerdo, em **[!UICONTROL Categoria]**, selecione **[!UICONTROL YouTube]**. No lado direito da página, selecione **[!UICONTROL YouTube]**.
1. Na página **[!UICONTROL YouTube]**, selecione **[!UICONTROL API de Dados do YouTube v3]**.
1. Na página **[!UICONTROL API de Dados do YouTube v3]**, selecione **[!UICONTROL GERENCIAR]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Para usar a API, você precisa de credenciais. Se necessário, no lado esquerdo da página **[!UICONTROL APIs e serviços]**, selecione **[!UICONTROL Credenciais]**.
1. Na página **[!UICONTROL Credenciais]**, próximo à parte superior, selecione **[!UICONTROL CRIAR CREDENCIAIS]** e, em seguida, selecione **[!UICONTROL ID de cliente OAuth]**.
1. Na página **[!UICONTROL Criar ID de cliente OAuth]**, na lista suspensa **[!UICONTROL Tipo de aplicativo]**, selecione **[!UICONTROL Aplicativo Web]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Siga uma das seguintes opções:

   * No campo **[!UICONTROL Nome]**, digite um nome exclusivo para o cliente OAuth 2.0.
   * Use o nome padrão que a Google já forneceu no campo **[!UICONTROL Nome]**.

1. No cabeçalho **[!UICONTROL Origens autorizadas do JavaScript]**, selecione **[!UICONTROL ADICIONAR URI]**.

   ![6_5_googleaccount-apis-nameauthorization](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. No campo de texto **[!UICONTROL URIs]**, insira o seguinte caminho, substituindo seu próprio domínio e número de porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>`

   Por exemplo, `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >O exemplo de caminho URI acima é hipotético e apenas para fins explicativos.

1. No cabeçalho **[!UICONTROL URIs de redirecionamento autorizados]**, selecione ADICIONAR URI.
1. No campo de texto **[!UICONTROL URIs]**, insira o seguinte caminho, substituindo seu próprio domínio e número de porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por exemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >O exemplo de caminho URI acima é hipotético e apenas para fins explicativos.

1. Próximo à parte inferior da página **[!UICONTROL Criar ID de cliente OAuth]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Cliente OAuth criado]**, faça o seguinte:

   * (Opcional) Copie os valores nos campos **[!UICONTROL Sua ID do cliente]** e **[!UICONTROL Seu segredo do cliente]** e salve.
   * Selecione **[!UICONTROL BAIXAR JSON]** e salve o arquivo JSON.

   Você precisará desse arquivo JSON baixado ao configurar o YouTube no Adobe Experience Manager posteriormente.

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. Na caixa de diálogo **[!UICONTROL Cliente OAuth criado]**, selecione **[!UICONTROL OK]**.
1. Faça logout da sua conta da Google. Agora crie um canal do YouTube.

### Criar um canal do YouTube {#creating-a-youtube-channel}

Para publicar vídeos no YouTube, você precisa ter um ou mais canais. Se você já criou um canal YouTube, ignore esta tarefa e vá para [Adicionar marcas para publicação](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Verifique se você já configurou um ou mais canais no YouTube *antes* de adicionar canais em Configurações do YouTube no Experience Manager (consulte [Configurar o YouTube no Experience Manager](#setting-up-youtube-in-aem) abaixo). Se não conseguir fazer a configuração do canal, você não será avisado de que não há canais. No entanto, a verificação do Google ainda ocorre quando você adiciona um canal, mas não há uma opção para escolher qual canal o vídeo é enviado.

**Para criar um canal do YouTube:**

1. Vá para [https://www.youtube.com](https://www.youtube.com/) e entre usando suas credenciais de conta da Google.
1. No canto superior direito da página do YouTube, selecione a imagem do seu perfil (ela também pode aparecer como uma letra dentro de um círculo de cores sólidas) e selecione **[!UICONTROL Configurações do YouTube]** (ícone de roda dentada).
1. Na página Visão Geral, no cabeçalho Recursos Adicionais, selecione **[!UICONTROL Ver todos os meus canais ou criar um canal]**.
1. Na página Canais, selecione **[!UICONTROL Criar um novo canal]**.
1. Na página Conta da Marca, no campo Nome da Conta da Marca, digite o nome de uma empresa ou qualquer outro nome de canal que você escolher onde deseja publicar seus ativos de vídeo e selecione **[!UICONTROL Criar]**.

   Lembre-se do nome inserido aqui; você deve inseri-lo novamente quando precisar configurar o YouTube no Experience Manager.

1. (Opcional) Se necessário, adicione mais canais.

   Agora você adiciona tags para publicação.

### Adicionar tags para publicação {#adding-tags-for-publishing}

Para publicar em seus vídeos no YouTube, a Experience Manager associa tags a um ou mais canais da YouTube. Para adicionar marcas para publicação, consulte [Administrar marcas](/help/sites-cloud/authoring/sites-console/tags.md).

Ou, se você pretende usar as marcas padrão no Experience Manager, ignore esta tarefa e vá para [Configurar o YouTube no Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Depois que o Cloud Service é configurado, outra configuração não é necessária para habilitar o agente de replicação de publicação do YouTube neste momento. O motivo é que ele foi ativado quando a configuração do Cloud Service foi salva.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configurar o YouTube no Experience Manager {#setting-up-youtube-in-aem}

A partir do Experience Manager 6.4, um novo método de interface do usuário de toque foi introduzido para configurar a publicação do YouTube no Experience Manager. Com base na instância instalada do Experience Manager que você está usando, execute um dos procedimentos a seguir:

* Para configurar o YouTube no Experience Manager antes da versão 6.4, consulte [Configurar o YouTube no Experience Manager antes da versão 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Para configurar o YouTube no Experience Manager 6.4 ou posterior, consulte [Configurar o YouTube no Experience Manager 6.4 e posterior](#setting-up-youtube-in-aem-and-later).

#### Configurar o YouTube no Experience Manager 6.4 e posterior {#setting-up-youtube-in-aem-and-later}

1. Certifique-se de fazer logon na instância do Dynamic Media como administrador.
1. No canto superior esquerdo do Experience Manager, selecione o logotipo do Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]**(ícone de martelo) > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Configuração de publicação do YouTube]**.
1. Selecionar **[!UICONTROL global]** (não o selecione).

1. Próximo ao canto superior direito da página global, selecione **[!UICONTROL Criar]**.
1. Na página Criar configuração do YouTube, em Configurações da Google Cloud Platform, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao definir as configurações da Google Cloud anteriormente.
Deixe a página Criar configuração do YouTube aberta; você voltará a ela em alguns instantes.

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa [Definir configurações da Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Selecione e copie todo o texto JSON.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

   Agora, configure canais do YouTube no Experience Manager.

1. Selecione **[!UICONTROL Adicionar Canal]**.
1. No campo Nome do Canal, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejado.

1. Selecione **[!UICONTROL Adicionar]**.
1. A verificação YouTube/Google é exibida. Se você ainda não tiver feito logon na conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem, você verá dois ou mais itens. Selecione um canal. Não selecione o endereço de e-mail; ele não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir acesso a este canal.

1. Selecione **[!UICONTROL Permitir]**.

   Agora, configure tags para publicação.

1. **[!UICONTROL Configurando marcas para publicação]** - Na página Cloud Services > YouTube, selecione o ícone de lápis para editar a lista de marcas que deseja usar.
1. Para exibir a lista de tags disponíveis no Experience Manager, selecione o ícone de lista suspensa (cursor invertido).
1. Para adicioná-las, selecione uma ou mais tags.

   Para excluir uma marca adicionada, selecione-a e selecione **[!UICONTROL X]**.

1. Quando terminar de adicionar as marcas desejadas, selecione **[!UICONTROL Salvar]**.

   Agora você publica vídeos no seu canal do YouTube.

#### Configuração do YouTube no Experience Manager antes da versão 6.4 {#setting-up-youtube-in-aem-before}

1. Certifique-se de fazer logon na instância do Dynamic Media como administrador.

1. No canto superior esquerdo do Experience Manager, selecione o logotipo do Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Implantação]** > **[!UICONTROL Serviços da nuvem]**.
1. No cabeçalho Serviços de terceiros, em YouTube, selecione **[!UICONTROL Configurar agora]**.
1. Na caixa de diálogo Criar configuração, insira um título (obrigatório) e nome (opcional) nos respectivos campos.
1. Selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Configurações da conta do YouTube, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao [definir inicialmente as configurações da Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
Deixe aberta a caixa de diálogo Configuração de conta do YouTube; você voltará a ela em alguns instantes.

1. Usando um editor de texto simples, abra o arquivo JSON baixado e salvo anteriormente na tarefa Definição das configurações da Google Cloud.
1. Selecione e copie todo o texto JSON.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Selecione **[!UICONTROL OK]**.

   Agora, configure canais do YouTube no Experience Manager.

1. À direita de **[!UICONTROL Canais disponíveis]**, selecione **+** (ícone de adição).
1. Na caixa de diálogo Configurações do canal do YouTube, no campo Título, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejado.

1. Selecione **[!UICONTROL OK]**.
1. A verificação YouTube/Google é exibida. Se você ainda não tiver feito logon na conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem, você verá dois ou mais itens. Selecione um canal. Não selecione o endereço de e-mail; ele não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir acesso a este canal.

1. Selecione **[!UICONTROL Permitir]**.

   Agora, configure tags para publicação.

1. **[!UICONTROL Configurando marcas para publicação]** - Na página Cloud Services > YouTube, selecione o ícone de lápis para editar a lista de marcas que deseja usar.
1. Para exibir a lista de tags disponíveis no Experience Manager, selecione o ícone de lista suspensa (cursor invertido).
1. Para adicioná-las, selecione uma ou mais tags.

   Para excluir uma marca adicionada, selecione-a e selecione **X**.

1. Quando terminar de adicionar as marcas desejadas, selecione **[!UICONTROL OK]**.

   Agora você publica vídeos no seu canal do YouTube.

### (Opcional) Automatize a configuração das propriedades padrão do YouTube para os vídeos carregados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Como opção, você pode automatizar a configuração das propriedades do YouTube ao carregar seus vídeos. Crie um perfil de processamento de metadados no Experience Manager.

Para criar o perfil de processamento de metadados, você primeiro copiará valores dos campos **[!UICONTROL Rótulo do campo]**, **[!UICONTROL Mapear para a propriedade]** e **[!UICONTROL Opções]**, todos encontrados nos Esquemas de metadados do vídeo. Em seguida, crie seu perfil de processamento de metadados de vídeo do YouTube adicionando esses valores a ele.

**Para automatizar a configuração das propriedades padrão do YouTube para seus vídeos carregados:**

1. No canto superior esquerdo do Experience Manager, selecione o logotipo do Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados]**.
1. Selecione **[!UICONTROL padrão]**. (Não adicione uma marca de seleção à caixa de seleção à esquerda de &quot;padrão&quot;.)
1. Na página **[!UICONTROL padrão]**, marque a caixa à esquerda de **[!UICONTROL vídeo]** e selecione **[!UICONTROL Editar]**.
1. Na página Editor de esquema de metadados, selecione a guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação no YouTube, selecione **[!UICONTROL Categoria do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Configurações]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para a propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar (como Pessoas e Blogs ou Ciência e Tecnologia).
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

1. No cabeçalho Publicação no YouTube, selecione **[!UICONTROL Privacidade do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Configurações]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para a propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar. Observe que as Opções são agrupadas em pares de dois. O campo inferior no par é o valor padrão que você deseja copiar, como público, não listado ou privado.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

1. Próximo ao canto superior direito da página Editor de esquema de metadados, selecione **[!UICONTROL Cancelar]**.
1. No canto superior esquerdo do Experience Manager, selecione o logotipo do Experience Manager e, no painel à esquerda, selecione **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de metadados]**.

1. Na página Perfis de metadados, próximo ao canto superior direito da página, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Adicionar perfil de metadados, no campo de texto **[!UICONTROL Título do perfil]**, digite o nome `YouTube Video` e selecione **[!UICONTROL Criar]**.
1. Na página Editor de perfil de metadados, selecione a guia **[!UICONTROL Avanço]**.
1. Adicione os valores copiados do YouTube Publishing ao perfil fazendo o seguinte:

   * No lado direito da página, selecione a guia **[!UICONTROL Criar Formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área de formulário.
   * (Opcional) Selecione **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações, no campo de texto Rótulo do Campo, digite `YouTube Publishing`.
   * Selecione a guia **[!UICONTROL Criar Formulário]** e arraste o componente rotulado **[!UICONTROL Texto de Vários Valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Publicação do YouTube]** que você criou.

   * Para selecionar o componente, selecione **[!UICONTROL Rótulo do campo]**.
   * No lado direito da página, na guia Configurações, cole os valores de Publicação do YouTube (valor Rótulo do campo e valor Mapear para a propriedade ) que você copiou anteriormente, nos respectivos campos no formulário. Cole o valor de Choices no campo Default Value.

1. Adicione os valores copiados de Privacidade do YouTube ao perfil da seguinte maneira:

   * No lado direito da página, selecione a guia **[!UICONTROL Criar Formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área de formulário.
   * (Opcional) Selecione **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações, no campo de texto Rótulo do Campo, digite `YouTube Privacy`.
   * Selecione a guia **[!UICONTROL Criar Formulário]** e arraste o componente rotulado **[!UICONTROL Texto de Vários Valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Privacidade do YouTube]** que você criou.

   * Para selecionar o componente, selecione **[!UICONTROL Rótulo do campo]**.
   * No lado direito da página, na guia Configurações, cole os valores de Publicação do YouTube (valor Rótulo do campo e valor Mapear para a propriedade ) que você copiou anteriormente, nos respectivos campos no formulário. Cole o valor de Choices no campo Default Value.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.
1. Aplique o perfil de metadados de Publicação do YouTube às pastas nas quais você fará upload dos vídeos. Você deve ter o Perfil de metadados e o Perfil de vídeo definidos.

   Consulte [Perfis de metadados](/help/assets/metadata-profiles.md) e [Perfis de vídeo](/help/assets/dynamic-media/video-profiles.md).

### Publicar vídeos no seu canal do YouTube {#publishing-videos-to-your-youtube-channel}

Agora você associa as tags adicionadas anteriormente aos ativos de vídeo. Esse processo permite que a Experience Manager saiba quais ativos publicar no canal do YouTube.

>[!NOTE]
>
>Publicar imediatamente não publica automaticamente no YouTube. Quando o Dynamic Media estiver configurado, há duas opções de publicação para escolher: **[!UICONTROL Imediatamente]** ou **[!UICONTROL Após ativação]**.
>
>**[!UICONTROL Publicar imediatamente]** significa que o ativo carregado, após ser sincronizado com o IPS, é publicado automaticamente no sistema de entrega. Embora isso seja verdade para o Dynamic Media, não é verdade para o YouTube. Para publicar no YouTube, você deve publicar por meio do Experience Manager Author.

>[!NOTE]
>
>Para publicar conteúdo do YouTube, o Experience Manager usa o fluxo de trabalho **[!UICONTROL Publicar no YouTube]**, que permite monitorar o progresso e exibir informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obter informações mais detalhadas sobre o progresso, é possível monitorar o log do YouTube em replicação. No entanto, esteja ciente de que esse monitoramento requer acesso de administrador.

**Para publicar vídeos no seu canal do YouTube:**

1. No Experience Manager, navegue até um ativo de vídeo que deseja publicar no canal do YouTube.
1. Selecione o ativo de vídeo (o conjunto de vídeos adaptáveis).
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na guia Básico, no cabeçalho Metadados, selecione **[!UICONTROL Abrir caixa de diálogo de seleção]** à direita do campo Marcas.
1. Na página Selecionar tags, navegue até as tags que deseja usar e selecione uma ou mais tags.

   Lembre-se de que as tags devem ser associadas ao canal do YouTube.

1. No canto superior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto superior direito da página de propriedades do vídeo, selecione **[!UICONTROL Salvar e fechar]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**.

   Consulte também [Usar o Gerenciamento de Publicação com o Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html?lang=pt-BR#page-authoring).

   Como opção, verifique o vídeo publicado no canal do YouTube.

### (Opcional) Verifique o vídeo publicado no YouTube {#optional-verifying-the-published-video-on-youtube}

Como opção, é possível monitorar o progresso da publicação (ou do cancelamento da publicação) do YouTube.

Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Os tempos de publicação podem variar muito dependendo de vários fatores que incluem o formato do vídeo de origem principal, o tamanho do arquivo e o tráfego de upload. O processo de publicação pode levar de alguns minutos a várias horas. Além disso, os formatos de resolução mais alta são renderizados muito mais lentamente. Por exemplo, 720p e 1080p demoram mais para serem exibidos do que 480p.

Após oito horas, se você ainda vir uma mensagem de status que diz **[!UICONTROL Carregado (processando, aguarde)]**, tente remover o vídeo do site e carregá-lo novamente.

### Vincular URLs do YouTube à sua aplicação web {#linking-youtube-urls-to-your-web-application}

Você pode obter uma cadeia de caracteres de URL do YouTube que é gerada pelo Dynamic Media após a publicação do vídeo. Ao copiar o URL do YouTube, ele é colocado na Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL do YouTube não estará disponível para cópia até que você tenha publicado o ativo de vídeo no YouTube.

Para vincular URLs do YouTube ao seu aplicativo web:

1. Navegue até o ativo de vídeo *YouTube publicado* cuja URL você deseja copiar e selecione-o.

   Lembre-se de que as URLs do YouTube só estão disponíveis para cópia *depois* de você ter *publicado* os ativos de vídeo no YouTube.

1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação no YouTube, na Lista de URLs do YouTube, selecione e copie o texto do URL no navegador da Web para visualizar o ativo ou adicionar à página de conteúdo da Web.

### Desfazer a publicação de vídeos para poder removê-los do YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Ao cancelar a publicação de um ativo de vídeo no Experience Manager, o vídeo é removido do YouTube.

>[!CAUTION]
>
>Se você remover um vídeo diretamente do YouTube, o Experience Manager não estará ciente e continuará a se comportar como se o vídeo ainda estivesse publicado no YouTube. Sempre cancele a publicação de um ativo de vídeo do YouTube por meio do Experience Manager.

>[!NOTE]
>
>Para remover conteúdo do YouTube, o Experience Manager usa o fluxo de trabalho **[!UICONTROL Cancelar publicação do YouTube]**, que permite monitorar o progresso e exibir informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para desfazer a publicação de vídeos e removê-los do YouTube:**

1. Navegue até os ativos de vídeo que deseja cancelar a publicação do seu canal do YouTube.
1. Em um modo de seleção de ativo, selecione um ou mais ativos de vídeo publicados.
1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Se necessário, selecione o ícone de três pontos (`. . .`) na barra de ferramentas para ver **[!UICONTROL Gerenciar Publicação]**.
1. Na página Gerenciar publicação, selecione **[!UICONTROL Cancelar publicação]**.
1. No canto superior direito da página, selecione **[!UICONTROL Avançar]**.
1. No canto superior direito da página, selecione **[!UICONTROL Cancelar publicação]**.

## Monitorar o progresso da codificação de vídeo e da publicação no YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Ao fazer upload de um novo vídeo para uma pasta que tenha a codificação de vídeo aplicada ou, você publica o vídeo no YouTube, monitora o andamento (ou a falha) da codificação de vídeo/publicação do Youtube. O progresso real da publicação no YouTube só está disponível por meio dos logs. Mas se falhar ou for bem-sucedido, ele será listado de outras maneiras descritas no procedimento a seguir. Além disso, você recebe notificações por email quando um fluxo de trabalho de publicação ou codificação de vídeo do YouTube é concluído ou interrompido.

### Monitorar progresso {#monitoring-progress}

Você pode monitorar o progresso, incluindo falha de codificação/publicação no YouTube.

1. Exibir o progresso da codificação de vídeo na pasta de ativos:

   * Na exibição de cartão, o progresso de codificação do vídeo é exibido no ativo por porcentagem. Se houver um erro, essas informações também serão exibidas no ativo.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * Na exibição em lista, o progresso de codificação do vídeo é exibido na coluna **[!UICONTROL Status de Processamento]**. Se houver um erro, essa mensagem será exibida nessa mesma coluna.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Essa coluna não é exibida por padrão. Para habilitar a coluna, selecione **[!UICONTROL Configurações de Exibição]** no menu suspenso de exibições, adicione a coluna **[!UICONTROL Status de Processamento]** e selecione **[!UICONTROL Atualização]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visualize o progresso nos detalhes do ativo. Ao selecionar um ativo, abra o menu suspenso e selecione **[!UICONTROL Linha do tempo]**. Para restringir a atividades de fluxo de trabalho, como codificação ou publicação no YouTube, selecione **[!UICONTROL Fluxos de trabalho]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   Todas as informações do fluxo de trabalho, como codificação, são exibidas na linha do tempo. Para publicação no YouTube, a linha do tempo do Fluxo de trabalho também inclui o nome do canal do YouTube e o URL do vídeo do YouTube. Além disso, você verá todas as notificações de falha na linha do tempo do fluxo de trabalho depois que a publicação for concluída.

   >[!NOTE]
   >
   >Pode levar muito tempo para que as mensagens de erro/falha sejam gravadas devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >* Configuração da fila de trabalhos do Apache Sling
   >* Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite
   >* Fila de tempo limite de fluxo de trabalho do Granite
   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** propriedades nessas configurações.

1. Nos fluxos de trabalho em andamento, consulte Instâncias de fluxo de trabalho disponíveis em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Instâncias]**.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Selecione a instância e selecione **[!UICONTROL Abrir Histórico]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Na área Instâncias de fluxo de trabalho, também é possível suspender, encerrar ou renomear fluxos de trabalho. Consulte [Administrar fluxos de trabalho](/help/sites-cloud/authoring/workflows/overview.md) para obter mais informações.

1. Em tarefas com falha, consulte Falhas de fluxo de trabalho, disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Falhas]**. A **[!UICONTROL Falha do fluxo de trabalho]** lista todas as atividades do fluxo de trabalho com falha.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Pode levar muito tempo para que a mensagem de erro seja gravada devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >* Configuração da fila de trabalhos do Apache Sling
   >* Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite
   >* Fila de tempo limite de fluxo de trabalho do Granite
   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** propriedades nessas configurações.

1. Em fluxos de trabalho concluídos, consulte Arquivo de fluxo de trabalho disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Arquivar]**. O **[!UICONTROL Arquivo de fluxo de trabalho]** lista todas as atividades de fluxo de trabalho concluídas.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Você recebe notificações por email sobre tarefas de fluxo de trabalho interrompidas ou com falha. Essas notificações por email podem ser configuradas por um administrador. Consulte [Configurar notificações por email](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## Transcodificar usando o perfil de processamento {#transcode-video}

O [!DNL Experience Manager] as a [!DNL Cloud Service] permite que você faça transcodificação básica de arquivos de vídeo MP4 usando Perfis de Processamento. A funcionalidade permite não apenas fazer upload, mas também pré-visualizar e dimensionar um arquivo de vídeo MP4.

![Criar perfil de processamento para transcodificação de vídeo em [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: um perfil de processamento para transcodificação de vídeo em [!DNL Experience Manager].*

Se você fornecer apenas largura ou altura e deixar o outro campo em branco, as representações manterão a proporção. O codec de vídeo H.264 está disponível para transcodificação.

Para processar ativos usando um perfil de processamento, adicione um perfil a uma pasta. Consulte [usar perfis de processamento para processar ativos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar ativos de vídeo {#annotate-video-assets}

É possível adicionar anotações a ativos de vídeo. Ao anotar vídeos, o reprodutor faz uma pausa para permitir que você faça anotações em um quadro. Para obter detalhes, consulte [gerenciamento de ativos de vídeo](manage-video-assets.md).

>[!NOTE]
>
>O formato de vídeo MXF ainda não é compatível com anotações de ativos de vídeo.

1. No console do [!DNL Assets], selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Visualizar]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao anotar, é possível desenhar na tela de desenho e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotações, clique em **[!UICONTROL Fechar]**.
1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.
1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

## Práticas recomendadas e limitações {#tips-limitations}

* Sem a licença do [!DNL Dynamic Media], você só pode processar arquivos MP4 usando perfis de processamento.
* Ao transcodificar arquivos MP4 usando Perfis de processamento, as seguintes diretrizes e limitações se aplicam:

   * Os arquivos Apple ProRes só podem transcodificar para uma resolução máxima de 1080p.
   * Se o arquivo de origem tiver uma taxa de bits >200 Mbps, você só poderá transcodificar para uma resolução máxima de 1080p.
   * Se a taxa de quadros de origem >=60 fps, o tamanho máximo do arquivo de origem que você pode usar é,

      * 400 MB para transcodificação 4k.
      * 800 MB para transcodificação 1080p.
      * 8 GB para transcodificação 720p.

   * O tamanho máximo de arquivo que você pode transcodificar para resolução de 4k é um arquivo MP4 de 2,55 GB com resolução de 4k, taxa de bits de 12 Mbps e 23 fps.

  **Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documentação de vídeo do Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Saiba mais sobre uso, tipos e configuração de perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).
