---
title: Baixar ativos
description: Baixar ativos em [!DNL Adobe Experience Manager Assets] e ativar ou desativar a funcionalidade de download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 42f7d82b69bed703f5f619c0b1d44046209ef7f2
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---

# Baixar ativos em [!DNL Adobe Experience Manager] {#download-assets-from-aem}

É possível baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente do [!DNL Adobe Experience Manager Assets]. Os ativos baixados são incluídos em um arquivo ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Os seguintes tipos de ativos não podem ser baixados: Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel.

Você pode baixar ativos do Experience Manager usando os seguintes métodos:

<!-- * [Link Share](#link-share-download) -->

* [Interface do usuário do Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Baixar ativos usando [!DNL Experience Manager] interface {#download-assets}

O Experience Manager otimiza a experiência de download com base na quantidade e no tamanho do ativo. Arquivos menores são baixados da interface do usuário em tempo real. [!DNL Experience Manager] O baixa diretamente solicitações de um único ativo para o arquivo original, em vez de incluir ativos únicos em um arquivo ZIP para permitir downloads mais rápidos. O Experience Manager suporta downloads grandes com solicitações assíncronas. As solicitações de download maiores que 100 GB são divididas em vários arquivos ZIP com um tamanho máximo de 100 GB cada.

Por padrão, [!DNL Experience Manager] aciona uma notificação na variável [[!DNL Experience Manager] Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) após a geração de um arquivo de download.

![Notificação na Caixa de entrada](assets/inbox-notification-for-large-downloads.png)


### Ativar notificações por email para downloads grandes {#enable-emails-for-large-downloads}

Os downloads assíncronos são acionados em qualquer um dos seguintes casos:

* Se houver mais de dez ativos
* Se o tamanho do download for superior a 100 MB
* Se o download levar mais de 30 segundos para se preparar

Enquanto o download assíncrono é executado no back-end, o usuário pode continuar a explorar e trabalhar mais no Experience Manager. Além das notificações da caixa de entrada de Experience Manager, o Experience Manager pode enviar emails para notificar o usuário após concluir o processo de download. Para ativar esse recurso, os administradores podem configurar o serviço de email [configuração de uma conexão de servidor SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Depois que o serviço de email é configurado, os administradores e usuários podem ativar notificações por email na interface do Experience Manager.

Para ativar notificações por email:

1. Efetue logon no [!DNL Experience Manager Assets].
1. Clique no ícone do usuário no canto superior direito e clique em **[!UICONTROL Minhas preferências]** para abrir a janela Preferências do Usuário.
1. Selecione o **[!UICONTROL Notificações por email para download de ativos]** e clique em **[!UICONTROL Aceitar]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Para baixar ativos, siga estas etapas:

1. Entrada [!DNL Experience Manager] clique em **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Navegue até os ativos que deseja baixar. Selecione a pasta ou selecione um ou mais ativos na pasta. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.

   ![Opções disponíveis ao baixar ativos do [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Na caixa de diálogo de download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para criar uma pasta para cada ativo contendo todas as representações baixadas do ativo. Se não estiver selecionada, cada ativo (e suas representações, se selecionado para download) estará contido na pasta principal do arquivo gerado. |
   | **[!UICONTROL Email]** | Selecione essa opção para enviar uma notificação por email (contendo um link para o download) para outro usuário. O usuário destinatário deve ser membro do `dam-users` grupo. Os modelos padrão de email estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em sua forma original.<br>A opção subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal - a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, é possível selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione esta opção para baixar todas as representações de corte inteligente do ativo selecionado no [!DNL Experience Manager]. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente, selecionando entre as [Predefinição de imagem](/help/assets/dynamic-media/image-presets.md) lista. <br>Além disso, você pode selecionar o tamanho e a unidade de medida, o formato, o espaço de cor, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você [!DNL Dynamic Media] ativado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]**.

   Se a notificação por email estiver ativada para downloads grandes, um email contendo um URL de download da pasta zip arquivada será exibido em sua caixa de entrada. Clique no link de download do email para baixar o arquivo zip.

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   Você também pode visualizar a notificação em sua [!DNL Experience Manager] Caixa de entrada.

   ![caixa de entrada-notificações-para-downloads-grandes](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Baixar ativos compartilhados usando o compartilhamento de link {#link-share-download}

O compartilhamento de ativos usando um link é uma maneira conveniente de disponibilizá-lo para as pessoas interessadas sem que elas precisem fazer logon no [!DNL Assets]. Consulte [Funcionalidade Compartilhamento de link](/help/assets/share-assets.md#sharelink).

Quando os usuários baixam ativos de links compartilhados, [!DNL Assets] O usa um serviço assíncrono que oferece downloads mais rápidos e ininterruptos. Os ativos a serem baixados são enfileirados em segundo plano em uma caixa de entrada em arquivos ZIP de tamanho de arquivo gerenciável. Para downloads maiores, o download é dividido em arquivos de 100 GB.

A variável [!UICONTROL Baixar caixa de entrada] exibe o status de processamento de cada arquivo. Quando o processamento estiver concluído, você poderá baixar os arquivos da caixa de entrada.

![Baixar caixa de entrada](assets/link-sharing-download-inbox.png)

## Ativar o servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] O permite que usuários autenticados emitam solicitações de download simultâneas arbitrariamente grandes para criar arquivos ZIP de ativos. A preparação do download pode ter implicações de desempenho ou pode até sobrecarregar o servidor e a rede. Para atenuar esses possíveis riscos semelhantes a DoS causados por esse recurso, `AssetDownloadServlet` O componente OSGi está desativado para instâncias de publicação. Se você não precisar do recurso de download nas instâncias do autor, desative o servlet no autor.

Para permitir o download de ativos do seu DAM, ao usar algo como o Asset Share Commons ou outra implementação semelhante a um portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho permitido do download o mais baixo possível, sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura direcionada ao modo de execução de publicação, ou seja, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Na pasta de configuração, crie um novo arquivo do tipo `nt:file` nomeado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencher `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como o valor de `asset.download.prezip.maxcontentsize`. O exemplo abaixo configura o tamanho máximo do download do ZIP para não exceder 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

Se você não precisar da funcionalidade de download, desative o servlet para evitar riscos semelhantes ao DoS. A variável `Asset Download Servlet` pode ser desativado em um [!DNL Experience Manager] crie e publique instâncias atualizando a configuração do dispatcher para bloquear qualquer solicitação de download de ativo. O servlet também pode ser desativado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração do Dispatcher, edite o `dispatcher.any` e adicionar uma nova regra à variável [seção de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Dicas e limitações {#tips-limitations}

* ao baixar uma pasta vazia, o [!DNL Experience Manager] transmite uma mensagem de sucesso sobre a criação de um arquivo ZIP, mas o arquivo não é criado.

>[!MORELIKETHIS]
>
>* [Baixar ativos protegidos DRM](drm.md)
>* [Baixe ativos usando o aplicativo de desktop Experience Manager no Win ou no Mac desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Baixe ativos usando o Link de ativos do Adobe nos aplicativos compatíveis da Adobe Creative Cloud](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)

