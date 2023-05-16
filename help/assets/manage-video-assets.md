---
title: Gerenciar ativos de vídeo
description: Fazer upload, visualizar, anotar e publicar ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '4938'
ht-degree: 6%

---

# Gerenciar ativos de vídeo {#manage-video-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferece ofertas e recursos maduros para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e a transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando Perfis de processamento e [!DNL Dynamic Media] integração. Without [!DNL Dynamic Media] licença, [!DNL Experience Manager] O oferece suporte básico para vídeos, como transcodificação usando FFmpeg, extração de miniaturas de visualização para os formatos de arquivo compatíveis e visualização na interface do usuário para formatos compatíveis com reprodução diretamente no navegador.

## Fazer upload e visualizar ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera visualizações para ativos de vídeo com a extensão MP4. Você pode visualizar as representações no [!DNL Assets] interface do usuário.

1. Na pasta ou nas subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload do ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário do . Consulte [fazer upload de ativos](manage-digital-assets.md#uploading-assets) para obter detalhes.
1. Para visualizar um vídeo na exibição de cartão, clique no botão **[!UICONTROL Reproduzir]** ![opção de reprodução](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo somente na exibição de cartão. O [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na exibição de lista.
1. Para visualizar o vídeo na página de detalhes do ativo, selecione **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela cheia.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, é possível incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar [!DNL Dynamic Media] ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Publicar vídeos no YouTube {#publishing-videos-to-youtube}

Você pode publicar ativos de vídeo gerenciados no Experience Manager Assets diretamente em um canal do YouTube criado anteriormente.

Para publicar ativos de vídeo no YouTube, adicione tags a ativos de vídeo no Experience Manager Assets. Você associa essas tags a um canal YouTube. Se a tag de um ativo de vídeo corresponder à tag de um canal de YouTube, o vídeo será publicado no YouTube. Publicar no YouTube ocorre junto com uma publicação normal do vídeo, desde que uma tag associada seja usada.

O YouTube faz sua própria codificação. Dessa forma, o arquivo de vídeo original que foi carregado no Experience Manager é publicado no YouTube em vez de qualquer representação de vídeo criada pela codificação do Dynamic Media. Embora não seja necessário processar vídeos usando o Dynamic Media, espera-se que eles o façam caso uma predefinição do visualizador seja necessária para reprodução.

Ao ignorar o perfil de processamento de vídeo e publicar diretamente no YouTube, isso significa apenas que o ativo de vídeo no Experience Manager Asset não obtém uma miniatura visualizável. Também significa que os vídeos que não estão codificados não funcionam com nenhum dos tipos de ativos do Dynamic Media.

A publicação de ativos de vídeo em servidores da YouTube envolve a conclusão das seguintes tarefas para garantir a verificação segura de servidor para servidor com o YouTube:

1. [Definir as configurações da Google Cloud](#configuring-google-cloud-settings)
1. [Criar um canal YouTube](#creating-a-youtube-channel)
1. [Adicionar tags para publicação](#adding-tags-for-publishing)
1. [Configurar YouTube no Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatize a configuração das propriedades padrão do YouTube para seus vídeos carregados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicar vídeos no seu canal do YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verificar o vídeo publicado no YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincular URLs do YouTube à sua aplicação web](#linking-youtube-urls-to-your-web-application)

Você também pode [cancelar a publicação de vídeos para removê-los do YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Definir as configurações da Google Cloud {#configuring-google-cloud-settings}

Para publicar no YouTube, você precisa de uma conta do Google. Se tiver uma conta GMAIL, você já terá uma conta Google; se você não tiver uma conta do Google, poderá criar uma facilmente. Você precisa da conta, pois precisa de credenciais para publicar ativos de vídeo no YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

A conta usada com a Google Cloud e a conta da Google usada para o YouTube não precisam ser a mesma.

O Google altera periodicamente sua interface do usuário. Dessa forma, as etapas para publicar vídeos no YouTube podem variar um pouco do que está documentado abaixo. Esse aviso também se aplica ao YouTube quando você tenta verificar se os vídeos foram carregados nele.

>[!NOTE]
>
>As etapas a seguir eram precisas no momento da escrita. No entanto, o Google atualiza periodicamente suas páginas da Web em nuvem sem aviso prévio. Dessa forma, algumas opções de configuração podem ter um nome ligeiramente diferente na interface do usuário do Google do nome usado nas etapas.

**Para definir as configurações da Google Cloud:**

1. Crie uma conta do Google.
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   Se você já tiver uma conta do Google, pule para a próxima etapa.

1. Ir para [https://cloud.google.com/](https://cloud.google.com/).
1. No **[!UICONTROL Google Cloud]** , próximo ao canto superior direito, selecione **[!UICONTROL Console]**.

   Se necessário, **[!UICONTROL Fazer logon]** usando as credenciais da conta do Google para visualizar o **[!UICONTROL Console]** opção.

1. No **[!UICONTROL Painel]** à direita de **[!UICONTROL Google Cloud Platform]**, selecione o **[!UICONTROL Projeto]** lista suspensa para abrir o **[!UICONTROL Selecionar um projeto]** caixa de diálogo.
1. No **[!UICONTROL Selecionar um projeto]** caixa de diálogo, selecione **[!UICONTROL Novo projeto]**.
1. No **[!UICONTROL Novo projeto]** na caixa de diálogo , na **[!UICONTROL Nome do projeto]** digite o nome do novo projeto.

   A ID do projeto é baseada no nome do projeto. Como tal, escolha cuidadosamente o nome do projeto; ele não pode ser alterado após ser criado. Além disso, você deve inserir a mesma ID de projeto novamente quando configurar o YouTube no Experience Manager posteriormente. Portanto, anote.

1. Selecione **[!UICONTROL Criar]**.

1. Siga um destes procedimentos:

   * No Painel do seu projeto, no **[!UICONTROL Introdução]** cartão, selecione **[!UICONTROL Explorar e ativar APIs]**.
   * No Painel do seu projeto, no **[!UICONTROL APIs]** cartão, selecione **[!UICONTROL Visão geral das APIs]**.

1. Próximo do meio superior da **[!UICONTROL APIs e serviços]** página, selecione **[!UICONTROL ATIVAR APIS E SERVIÇOS]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. No **[!UICONTROL Biblioteca da API]** no lado esquerdo, em **[!UICONTROL Categoria]**, selecione **[!UICONTROL YouTube]**. No lado direito da página, selecione **[!UICONTROL YouTube]**.
1. No **[!UICONTROL YouTube]** página, selecione **[!UICONTROL API de dados do YouTube v3]**.
1. No **[!UICONTROL API de dados do YouTube v3]** página, selecione **[!UICONTROL GERENCIAR]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Para usar a API, você precisa de credenciais. Se necessário, no lado esquerdo do **[!UICONTROL APIs e serviços]** página, selecione **[!UICONTROL Credenciais]**.
1. No **[!UICONTROL Credenciais]** , próximo à parte superior, selecione **[!UICONTROL CRIAR CREDENCIAIS]**, em seguida selecione **[!UICONTROL ID de cliente OAuth]**.
1. No **[!UICONTROL Criar ID de cliente OAuth]** na página **[!UICONTROL Tipo de aplicativo]** , selecione **[!UICONTROL aplicação web]**.

   ![6_5_googleaccount-apis-application-type](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Siga uma das seguintes opções:

   * No **[!UICONTROL Nome]** , insira um nome exclusivo para o cliente OAuth 2.0.
   * Use o nome padrão que o Google já forneceu na **[!UICONTROL Nome]** campo.

1. Em **[!UICONTROL Origens JavaScript autorizadas]** título, selecione **[!UICONTROL ADICIONAR URI]**.

   ![6_5_googleaccount-apis-name-authorization](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. No **[!UICONTROL URIs]** , insira o seguinte caminho, substituindo seu próprio domínio e número da porta no caminho e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>`

   Por exemplo, `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >O exemplo de caminho URI acima é hipotético e somente para fins de explicação.

1. Em **[!UICONTROL URIs de redirecionamento autorizados]** selecione ADICIONAR URI.
1. No **[!UICONTROL URIs]** , insira o seguinte caminho, substituindo seu próprio domínio e número da porta no caminho e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por exemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >O exemplo de caminho URI acima é hipotético e somente para fins de explicação.

1. Próximo à parte inferior da **[!UICONTROL Criar ID de cliente OAuth]** página, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Cliente OAuth criado]** , faça o seguinte:

   * (Opcional) Copie os valores no **[!UICONTROL Sua ID do cliente]** e **[!UICONTROL Seu Segredo Do Cliente]** e salvar.
   * Selecionar **[!UICONTROL BAIXAR JSON]** e salve o arquivo JSON.

   Esse arquivo JSON é necessário quando você configura o YouTube no Adobe Experience Manager posteriormente.

   ![6_5_googleaccount-apis-authclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. No **[!UICONTROL Cliente OAuth criado]** caixa de diálogo, selecione **[!UICONTROL OK]**.
1. Faça logoff de sua conta do Google. Agora crie um canal YouTube.

### Criar um canal YouTube {#creating-a-youtube-channel}

A publicação de vídeos no YouTube requer um ou mais canais. Caso já tenha criado um canal YouTube, ignore esta tarefa e vá para [Adicionar tags para publicação](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Certifique-se de que você já configurou um ou mais canais no YouTube *before* você adiciona canais em Configurações do YouTube no Experience Manager (consulte [Configurar YouTube no Experience Manager](#setting-up-youtube-in-aem) abaixo). Se você não conseguir fazer a configuração do canal, não será avisado sobre nenhum canal existente. No entanto, a verificação do Google ainda ocorre ao adicionar um canal, mas não há uma opção para escolher qual canal o vídeo será enviado.

**Para criar um canal YouTube:**

1. Ir para [https://www.youtube.com](https://www.youtube.com/) e faça logon usando suas credenciais de conta do Google.
1. No canto superior direito da página do YouTube, selecione a imagem do perfil (também pode aparecer como uma letra num círculo de cor sólida) e selecione **[!UICONTROL Configurações do YouTube]** (ícone de engrenagem arredondada).
1. Na página Visão geral , no cabeçalho Recursos adicionais , selecione **[!UICONTROL Ver todos os meus canais ou criar um canal]**.
1. Na página Canais , selecione **[!UICONTROL Criar um novo canal]**.
1. Na página Conta de marca, no campo Nome da conta de marca , digite o nome de uma empresa ou qualquer outro nome de canal que você escolher onde deseja publicar seus ativos de vídeo e, em seguida, selecione **[!UICONTROL Criar]**.

   Lembre-se do nome inserido aqui; você deve inseri-lo novamente quando precisar configurar o YouTube no Experience Manager.

1. (Opcional) Se necessário, adicione mais canais.

   Agora, você adiciona tags para publicação.

### Adicionar tags para publicação {#adding-tags-for-publishing}

Para publicar seus vídeos no YouTube, o Experience Manager associa as tags a um ou mais canais do YouTube. Para adicionar tags para publicação, consulte [Administrar tags](/help/sites-cloud/authoring/features/tags.md).

Ou, se você pretende usar as tags padrão no Experience Manager, pode ignorar esta tarefa e acessar [Configurar YouTube no Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Depois que o Cloud Service é configurado, outra configuração não é necessária para habilitar o agente de replicação YouTube Publish neste ponto. O motivo é porque ele foi ativado quando a configuração de Cloud Service foi salva.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configurar YouTube no Experience Manager {#setting-up-youtube-in-aem}

A partir do Experience Manager 6.4, um novo método de interface de toque foi introduzido para configurar a publicação do YouTube no Experience Manager. Com base na instância instalada do Experience Manager que você está usando, execute um dos seguintes procedimentos:

* Para configurar o YouTube no Experience Manager antes da versão 6.4, consulte [Configurar o YouTube no Experience Manager antes da versão 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Para configurar o YouTube no Experience Manager 6.4 ou posterior, consulte [Configure o YouTube no Experience Manager 6.4 e posterior](#setting-up-youtube-in-aem-and-later).

#### Configure o YouTube no Experience Manager 6.4 e posterior {#setting-up-youtube-in-aem-and-later}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.
1. No canto superior esquerdo do Experience Manager, selecione o logotipo Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]**(ícone de martelo) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração de publicação do YouTube]**.
1. Selecionar **[!UICONTROL global]** (não selecione).

1. Ao lado do canto superior direito da página global, selecione **[!UICONTROL Criar]**.
1. Na página Criar configuração do YouTube, em Configurações da Google Cloud Platform, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto quando definiu as configurações da Google Cloud anteriormente.
Deixe a página Criar configuração do YouTube aberta; você está voltando a ela em um momento.

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa [Definir as configurações da Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**.

   Agora, configure os canais YouTube no Experience Manager.

1. Selecionar **[!UICONTROL Adicionar canal]**.
1. No campo Nome do canal , digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Selecionar **[!UICONTROL Adicionar]**.
1. A verificação YouTube/Google é exibida. Se você ainda não estiver conectado à conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir o acesso a este canal.

1. Selecionar **[!UICONTROL Permitir]**.

   Agora, configure as tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]** - Na página Cloud Services > YouTube , selecione o ícone de lápis para editar a lista de tags que deseja usar.
1. Para exibir a lista de tags disponíveis no Experience Manager, selecione o ícone da lista suspensa (sinal de interpolação).
1. Para adicioná-las, selecione uma ou mais tags.

   Para excluir uma tag adicionada, selecione a tag e selecione **[!UICONTROL X]**.

1. Quando terminar de adicionar as tags desejadas, selecione **[!UICONTROL Salvar]**.

   Agora você publica vídeos no seu canal do YouTube.

#### Configurar o YouTube no Experience Manager antes da versão 6.4 {#setting-up-youtube-in-aem-before}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.

1. No canto superior esquerdo do Experience Manager, selecione o logotipo Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. No cabeçalho Serviços de terceiros, em YouTube, selecione **[!UICONTROL Configurar agora]**.
1. Na caixa de diálogo Criar configuração , digite um título (obrigatório) e um nome (opcional) nos respectivos campos.
1. Selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Configurações da conta do YouTube, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao iniciar [configurações da Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) anteriormente.
Deixe a caixa de diálogo Configuração da conta do YouTube aberta; você está voltando a ela em um momento.

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa Configuração das configurações da Google Cloud.
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Selecionar **[!UICONTROL OK]**.

   Agora, configure os canais YouTube no Experience Manager.

1. À direita de **[!UICONTROL Canais disponíveis]**, selecione **+** (ícone de sinal de mais).
1. Na caixa de diálogo Configurações do canal do YouTube, no campo Título, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Selecionar **[!UICONTROL OK]**.
1. A verificação YouTube/Google é exibida. Se você ainda não estiver conectado à conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir o acesso a este canal.

1. Selecionar **[!UICONTROL Permitir]**.

   Agora, configure as tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]** - Na página Cloud Services > YouTube , selecione o ícone de lápis para editar a lista de tags que deseja usar.
1. Para exibir a lista de tags disponíveis no Experience Manager, selecione o ícone da lista suspensa (sinal de interpolação).
1. Para adicioná-las, selecione uma ou mais tags.

   Para excluir uma tag adicionada, selecione a tag e selecione **X**.

1. Quando terminar de adicionar as tags desejadas, selecione **[!UICONTROL OK]**.

   Agora você publica vídeos no seu canal do YouTube.

### (Opcional) Automatize a configuração das propriedades padrão do YouTube para seus vídeos carregados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Opcionalmente, é possível automatizar a configuração das propriedades do YouTube ao fazer upload dos vídeos. Crie um perfil de processamento de metadados no Experience Manager.

Para criar o perfil de processamento de metadados, você primeiro copiará valores dos campos **[!UICONTROL Rótulo do campo]**, **[!UICONTROL Mapear para a propriedade]** e **[!UICONTROL Opções]**, todos encontrados nos Esquemas de metadados do vídeo. Em seguida, crie seu perfil de processamento de metadados de vídeo do YouTube adicionando esses valores a ele.

**Para automatizar a configuração das propriedades padrão do YouTube para os vídeos carregados:**

1. No canto superior esquerdo do Experience Manager, selecione o logotipo Experience Manager e, no painel à esquerda, navegue até **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.
1. Selecionar **[!UICONTROL default]**. (Não adicione uma marca de seleção à caixa de seleção à esquerda de &quot;padrão&quot;.)
1. No **[!UICONTROL default]** marque a caixa à esquerda de **[!UICONTROL vídeo]**, em seguida selecione **[!UICONTROL Editar]**.
1. Na página Editor de esquema de metadados , selecione o **[!UICONTROL Avançado]** guia .
1. No cabeçalho Publicação no YouTube , selecione **[!UICONTROL Categoria do YouTube]**.
1. No lado direito da página, em **[!UICONTROL Configurações]** , faça o seguinte:

   * No **[!UICONTROL Mapear para propriedade]** , selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar (como People &amp; Blogs ou Science &amp; Technology).
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. No cabeçalho Publicação no YouTube , selecione **[!UICONTROL Privacidade da YouTube]**.
1. No lado direito da página, em **[!UICONTROL Configurações]** , faça o seguinte:

   * No **[!UICONTROL Mapear para propriedade]** , selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar. Observe que as Opções são agrupadas em pares de dois. O campo inferior do par é o valor padrão que você deseja copiar, como público, não listado ou privado.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. Próximo ao canto superior direito da página Editor de esquema de metadados, selecione **[!UICONTROL Cancelar]**.
1. No canto superior esquerdo do Experience Manager, selecione o logotipo Experience Manager e, em seguida, no painel à esquerda, selecione **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de metadados]**.

1. Na página Perfis de metadados , próximo ao canto superior direito da página, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Adicionar perfil de metadados , na **[!UICONTROL Título do perfil]** campo de texto, insira o nome `YouTube Video` em seguida, selecione **[!UICONTROL Criar]**.
1. Na página Editor de perfil de metadados , selecione o **[!UICONTROL Avanço]** guia .
1. Adicione os valores copiados de Publicação no YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, selecione o **[!UICONTROL Criar formulário]** guia .
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** à esquerda e solte-a na área do formulário.
   * (Opcional) Selecione **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Publishing`.
   * Selecione o **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do **[!UICONTROL Publicação no YouTube]** cabeçalho criado por você.

   * Para selecionar o componente, selecione **[!UICONTROL Rótulo do campo]**.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Adicione os valores copiados da Privacidade do YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, selecione o **[!UICONTROL Criar formulário]** guia .
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** à esquerda e solte-a na área do formulário.
   * (Opcional) Selecione **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Privacy`.
   * Selecione o **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do **[!UICONTROL Privacidade da YouTube]** cabeçalho criado por você.

   * Para selecionar o componente, selecione **[!UICONTROL Rótulo do campo]**.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**.
1. Aplique o perfil de metadados de Publicação do YouTube às pastas onde você fará upload de vídeos. Você deve ter o Perfil de metadados e o Perfil de vídeo definidos.

   Consulte [Perfis de metadados](/help/assets/metadata-profiles.md) e [Perfis de vídeo](/help/assets/dynamic-media/video-profiles.md).

### Publicar vídeos no seu canal do YouTube {#publishing-videos-to-your-youtube-channel}

Agora, associe as tags adicionadas anteriormente aos ativos de vídeo. Esse processo permite que o Experience Manager saiba quais ativos serão publicados no canal do YouTube.

>[!NOTE]
>
>Publicar imediatamente não publica automaticamente no YouTube. Quando o Dynamic Media estiver configurado, há duas opções de publicação para escolher: **[!UICONTROL Imediatamente]** ou **[!UICONTROL Após ativação]**.
>
>**[!UICONTROL Publicar imediatamente]** significa que o ativo carregado, depois de sincronizado com o IPS, é publicado automaticamente no sistema de delivery. Embora isso seja verdade para o Dynamic Media, não é verdadeiro para o YouTube. Para publicar no YouTube, você deve publicar por meio do Experience Manager Author.

>[!NOTE]
Para publicar conteúdo do YouTube, o Experience Manager usa a variável **[!UICONTROL Publicar no YouTube]** , que permite monitorar o progresso e exibir as informações de falha.
Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
Para obter informações de progresso mais detalhadas, você pode monitorar o log do YouTube em replicação. Esteja ciente, no entanto, de que tal monitoramento requer acesso de Administrador.

**Para publicar vídeos no seu canal do YouTube:**

1. No Experience Manager, navegue até um ativo de vídeo que deseja publicar no canal do YouTube.
1. Selecione o ativo de vídeo (o conjunto de vídeos adaptáveis).
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na guia Básico , abaixo do cabeçalho Metadados , selecione **[!UICONTROL Abrir caixa de diálogo de seleção]** à direita do campo Tags .
1. Na página Selecionar tags , navegue até as tags que deseja usar e selecione uma ou mais tags.

   Lembre-se de que as tags devem ser associadas ao canal do YouTube.

1. No canto superior direito da página, selecione **[!UICONTROL Selecionar]**.
1. No canto superior direito da página de propriedades do vídeo, selecione **[!UICONTROL Salvar e fechar]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**.

   Consulte também [Usar o gerenciamento de publicação com o Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Opcionalmente, é possível verificar o vídeo publicado no canal do YouTube.

### (Opcional) Verificar o vídeo publicado no YouTube {#optional-verifying-the-published-video-on-youtube}

Opcionalmente, é possível monitorar o progresso da publicação (ou desfazer a publicação) do YouTube.

Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Os tempos de publicação podem variar bastante, dependendo de vários fatores que incluem o formato do vídeo de origem primária, o tamanho do arquivo e o tráfego de upload. O processo de publicação pode levar de alguns minutos a várias horas. Além disso, os formatos de resolução mais alta são renderizados muito mais lentamente. Por exemplo, 720p e 1080p levam mais tempo para serem exibidas do que 480p.

Após oito horas, se você ainda vir uma mensagem de status que diz **[!UICONTROL Carregado (processando, aguarde)]**, tente remover o vídeo do site e carregá-lo novamente.

### Vincular URLs do YouTube à sua aplicação web {#linking-youtube-urls-to-your-web-application}

Você pode obter uma string de URL do YouTube gerada pelo Dynamic Media após publicar o vídeo. Ao copiar o URL do YouTube, ele chega à Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
O URL do YouTube não está disponível para cópia até que você tenha publicado o ativo de vídeo no YouTube.

Para vincular URLs do YouTube ao seu aplicativo da Web:

1. Navegue até o *YouTube publicado* ativo de vídeo cujo URL você deseja copiar e, em seguida, selecioná-lo.

   Lembre-se de que os URLs do YouTube só estão disponíveis para cópia *after* você tem primeiro *publicado* os ativos de vídeo para a YouTube.

1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Avançado]** guia .
1. No cabeçalho Publicação do YouTube, na Lista de URLs do YouTube, selecione e copie o texto do URL para o navegador da Web para visualizar o ativo ou adicionar à página de conteúdo da Web.

### Cancelar a publicação de vídeos para que você possa removê-los do YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Ao cancelar a publicação de um ativo de vídeo no Experience Manager, o vídeo é removido do YouTube.

>[!CAUTION]
Se você remover um vídeo diretamente do YouTube, o Experience Manager não estará ciente e continuará a se comportar como se o vídeo ainda estivesse publicado no YouTube. Sempre desfaça a publicação de um ativo de vídeo do YouTube por meio do Experience Manager.

>[!NOTE]
Para remover o conteúdo do YouTube, o Experience Manager usa a variável **[!UICONTROL Cancelar publicação do YouTube]** , que permite monitorar o progresso e exibir as informações de falha.
Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para cancelar a publicação de vídeos para removê-los do YouTube:**

1. Navegue até os ativos de vídeo que você deseja cancelar a publicação por meio do canal do YouTube.
1. Em um modo de seleção de ativo, selecione um ou mais ativos de vídeo publicados.
1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Se necessário, selecione o ícone de três pontos (`. . .`) na barra de ferramentas para ver **[!UICONTROL Gerenciar publicação]**.
1. Na página Gerenciar publicação , selecione **[!UICONTROL Cancelar publicação]**.
1. No canto superior direito da página, selecione **[!UICONTROL Próximo]**.
1. No canto superior direito da página, selecione **[!UICONTROL Cancelar publicação]**.

## Monitorar o progresso da codificação de vídeo e da publicação no YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Ao fazer o upload de um novo vídeo para uma pasta que tenha codificação de vídeo aplicada ou, você publicar seu vídeo no YouTube, monitore o progresso (ou falha) da codificação/publicação do YouTube. O progresso real da publicação do YouTube só está disponível por meio dos logs. Mas se ele falhar ou for bem-sucedido, ele será listado de outras maneiras descritas no procedimento a seguir. Além disso, você recebe notificações por email quando um fluxo de trabalho de publicação ou codificação de vídeo do YouTube é concluído ou interrompido.

### Monitorar progresso {#monitoring-progress}

Você pode monitorar o progresso, incluindo codificação com falha/publicação do YouTube.

1. Visualizar o progresso da codificação de vídeo na pasta de ativos:

   * Na exibição de cartão, o progresso da codificação de vídeo é exibido no ativo por porcentagem. Se houver um erro, essas informações também serão exibidas no ativo.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * Na exibição em lista, o progresso da codificação do vídeo é exibido na **[!UICONTROL Status do processamento]** coluna. Se houver um erro, essa mensagem será exibida nessa mesma coluna.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Essa coluna não é exibida por padrão. Para ativar a coluna, selecione **[!UICONTROL Exibir configurações]** no menu suspenso exibições e adicione o **[!UICONTROL Status do processamento]** e selecione **[!UICONTROL Atualizar]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Exibir o progresso nos detalhes do ativo. Ao selecionar um ativo, abra o menu suspenso e selecione **[!UICONTROL Linha do tempo]**. Para restringi-lo a atividades de fluxo de trabalho, como codificação ou publicação no YouTube, selecione **[!UICONTROL Fluxos de trabalho]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   Qualquer informação do fluxo de trabalho, como codificação, é exibida na linha do tempo. Para publicação do YouTube, a linha do tempo do Fluxo de trabalho também inclui o nome do canal do YouTube e o URL do vídeo do YouTube. Além disso, você vê notificações de falha na linha do tempo do fluxo de trabalho depois que a publicação é concluída.

   >[!NOTE]
   Pode levar muito tempo para que as mensagens de erro/falha sejam gravadas devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   * Configuração da fila de trabalhos do Apache Sling
   * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   * Fila de tempo limite do fluxo de trabalho do Granite

   Pode ajustar a variável **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** nessas configurações.

1. Nos fluxos de trabalho em andamento, consulte Instâncias de fluxo de trabalho disponíveis em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Instâncias]**.

   >[!NOTE]
   Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Selecione a instância e selecione **[!UICONTROL Abrir Histórico]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Na área Instâncias do fluxo de trabalho , também é possível suspender, encerrar ou renomear fluxos de trabalho. Consulte [Administrar workflows](/help/sites-cloud/authoring/workflows/overview.md) para obter mais informações.

1. Em tarefas com falha, consulte Falhas de fluxo de trabalho, disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Falhas]**. A **[!UICONTROL Falha do fluxo de trabalho]** lista todas as atividades do fluxo de trabalho com falha.

   >[!NOTE]
   Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   Pode levar muito tempo para que a mensagem de erro seja gravada devido a várias configurações de workflow em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   * Configuração da fila de trabalhos do Apache Sling
   * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   * Fila de tempo limite do fluxo de trabalho do Granite

   Pode ajustar a variável **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** nessas configurações.

1. Em fluxos de trabalho concluídos, consulte Arquivo de fluxo de trabalho disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Arquivar]**. O **[!UICONTROL Arquivo de fluxo de trabalho]** lista todas as atividades de fluxo de trabalho concluídas.

   >[!NOTE]
   Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Você recebe notificações por email sobre trabalhos de fluxo de trabalho abortados ou com falha. Essas notificações por email podem ser configuradas por um administrador. Consulte [Configurar notificações por email](#configuring-e-mail-notifications).

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

## Transcodificar usando o Perfil de processamento {#transcode-video}

[!DNL Experience Manager] como [!DNL Cloud Service] permite fazer a transcodificação básica de arquivos de vídeo MP4 usando Perfis de processamento. A funcionalidade permite que você não apenas faça upload, mas também visualize e dimensione um arquivo de vídeo MP4.

![Criar perfil de processamento para transcodificação de vídeo em [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Um Perfil de processamento para a transcodificação de vídeo em [!DNL Experience Manager].*

Se você fornecer somente largura ou apenas altura e deixar o outro campo em branco, as representações manterão a proporção. O codec de vídeo H.264 está disponível para transcodificação.

Para processar ativos usando um perfil de processamento, adicione um perfil a uma pasta. Consulte [usar perfis de processamento para processar ativos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar ativos de vídeo {#annotate-video-assets}

É possível adicionar anotações a ativos de vídeo. Ao anotar vídeos, o reprodutor pausa para permitir que você anote em um quadro. Para obter detalhes, consulte [gerenciamento de ativos de vídeo](manage-video-assets.md).

>[!NOTE]
O formato de vídeo MXF ainda não é compatível com anotações de ativos de vídeo.

1. No [!DNL Assets] , selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Visualizar]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao fazer anotações, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotação, clique em **[!UICONTROL Fechar]**.
1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.
1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

## Práticas recomendadas e limitações {#tips-limitations}

* Without [!DNL Dynamic Media] Você só pode processar arquivos MP4 usando perfis de processamento.
* Ao transcodificar arquivos MP4 usando Perfis de processamento, as seguintes diretrizes e limitações se aplicam:

   * Os arquivos Apple ProRes só podem transcodificar para uma resolução máxima de 1080p.
   * Se o arquivo de origem tiver uma taxa de bits > 200 Mbps, você só poderá transcodificar para uma resolução máxima de 1080p.
   * Se o fragmento de origem >=60 fps, o tamanho máximo do arquivo de origem que você pode usar é,

      * 400 MB para transcodificação 4k.
      * 800 MB para transcodificação de 1080p.
      * 8 GB para transcodificação de 720p.
   * O tamanho máximo de arquivo que você pode transcodificar para a resolução de 4 k é um arquivo MP4 de 2,55 GB com resolução de 4 k, taxa de bits de 12 Mbps e 23 fps.

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

>[!MORELIKETHIS]
* [Documentação de vídeo do Dynamic Media](/help/assets/dynamic-media/video.md).
* [Saiba mais sobre o uso, os tipos e a configuração de perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).

