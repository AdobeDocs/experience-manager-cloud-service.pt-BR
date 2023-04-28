---
title: Baixar ativos
description: Baixar ativos de [!DNL Adobe Experience Manager Assets] e ative ou desative a funcionalidade de download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 5%

---

# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente do [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Os seguintes tipos de ativos não podem ser baixados: Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel.

Você pode baixar ativos do Experience Manager usando os seguintes métodos:

<!-- * [Link Share](#link-share-download) -->

* [Interface do usuário do Experience Manager](#download-assets)
* [Compartilhamento de ativos Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Baixar ativos usando [!DNL Experience Manager] interface {#download-assets}

O Experience Manager otimiza a experiência de download com base na quantidade e no tamanho do ativo. Arquivos menores são baixados da interface do usuário em tempo real. [!DNL Experience Manager] O baixa diretamente solicitações de ativos únicos para o arquivo original, em vez de incluir ativos únicos em um arquivo ZIP para permitir downloads mais rápidos. O Experience Manager suporta downloads grandes com solicitações assíncronas. As solicitações de download com mais de 100 GB são divididas em vários arquivos ZIP com um tamanho máximo de 100 GB cada.

Por padrão, [!DNL Experience Manager] aciona uma notificação no [[!DNL Experience Manager] Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) após a geração de um arquivo de download.

![Notificação da caixa de entrada](assets/inbox-notification-for-large-downloads.png)


### Ativar notificações por email para downloads grandes {#enable-emails-for-large-downloads}

Os downloads assíncronos são acionados em qualquer um dos seguintes casos:

* Se houver mais de dez ativos
* Se o tamanho de download for superior a 100 MB
* Se o download demorar mais de 30 segundos para se preparar

Embora o download assíncrono seja executado no back-end, o usuário pode continuar a explorar e trabalhar mais no Experience Manager. Além das notificações da caixa de entrada do Experience Manager, o Experience Manager pode enviar emails para notificar o usuário ao concluir o processo de download. Para habilitar esse recurso, os administradores podem configurar o serviço de email ao [configuração de uma conexão do servidor SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Após configurar o serviço de email, os administradores e usuários poderão ativar notificações por email na interface do Experience Manager.

Para ativar notificações por email:

1. Faça logon em [!DNL Experience Manager Assets].
1. Clique no ícone do usuário no canto superior direito e clique em **[!UICONTROL Minhas preferências]** para abrir a janela Preferências de usuário.
1. Selecione o **[!UICONTROL Notificações por email de download de ativos]** caixa de seleção e clique em **[!UICONTROL Aceitar]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Para baixar ativos, siga estas etapas:

1. Em [!DNL Experience Manager] interface do usuário, clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até os ativos que deseja baixar. Selecione a pasta ou selecione um ou mais ativos na pasta. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.

   ![Opções disponíveis ao baixar ativos do [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para criar uma pasta para cada ativo contendo todas as representações baixadas do ativo. Se não estiver selecionado, cada ativo (e suas renderizações, se selecionado para download) estará contido na pasta principal do arquivo gerado. |
   | **[!UICONTROL Email]** | Selecione essa opção para enviar uma notificação por email (contendo um link para download) para outro usuário. O usuário destinatário deve ser membro do `dam-users` grupo. Os modelos padrão de emails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos personalizados durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é a representação binária de um ativo. Os ativos têm uma representação principal: a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione esta opção para baixar todas as representações de recorte inteligente do ativo selecionado de dentro [!DNL Experience Manager]. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente, selecionando no [Predefinição de imagem](/help/assets/dynamic-media/image-presets.md) lista. <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cores, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] habilitado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]**.

   Se a notificação por email estiver ativada para downloads grandes, um email contendo um URL de download da pasta zip arquivada aparecerá em sua caixa de entrada. Clique no link de download do email para baixar o arquivo zip.

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   Você também pode exibir a notificação em [!DNL Experience Manager] Caixa de entrada.

   ![notificações da caixa de entrada para downloads grandes](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Baixar ativos compartilhados usando o compartilhamento de link {#link-share-download}

O compartilhamento de ativos usando um link é uma maneira conveniente de disponibilizá-lo para as pessoas interessadas, sem a necessidade de fazer logon no [!DNL Assets]. Consulte [Funcionalidade de compartilhamento de links](/help/assets/share-assets.md#sharelink).

Quando usuários baixam ativos de links compartilhados, [!DNL Assets] O usa um serviço assíncrono que oferece downloads mais rápidos e ininterruptos. Os ativos a serem baixados são enfileirados em segundo plano em uma caixa de entrada em arquivos ZIP com tamanho de arquivo gerenciável. Para downloads maiores, o download é fragmentado em arquivos de 100 GB.

O [!UICONTROL Baixar Caixa de entrada] exibe o status de processamento de cada arquivo. Após concluir o processamento, é possível baixar os arquivos da caixa de entrada.

![Baixar caixa de entrada](assets/link-sharing-download-inbox.png)

## Habilitar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] O permite que usuários autenticados emitam solicitações de download arbitrariamente grandes e simultâneas para criar arquivos ZIP de ativos. A preparação do download pode ter implicações de desempenho ou pode até mesmo sobrecarregar o servidor e a rede. Para mitigar esses potenciais riscos do tipo DoS causados por esse recurso, `AssetDownloadServlet` O componente OSGi está desabilitado para instâncias de publicação. Se você não precisar do recurso de download em instâncias do autor, desative o servlet no autor.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante a portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho de download permitido o mais baixo possível sem afetar os requisitos diários de download. Um alto valor pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que seja direcionada ao modo de execução de publicação, ou seja, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Na pasta de configuração, crie um novo arquivo do tipo `nt:file` nomeado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencher `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para download como valor de `asset.download.prezip.maxcontentsize`. A amostra abaixo configura o tamanho máximo do download do ZIP para não exceder 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

Se você não precisar da funcionalidade de download, desative o servlet para evitar riscos semelhantes a DoS. O `Asset Download Servlet` pode ser desativado em um [!DNL Experience Manager] crie e publique instâncias atualizando a configuração do dispatcher para bloquear qualquer solicitação de download de ativos. O servlet também pode ser desabilitado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração de dispatcher, edite a variável `dispatcher.any` e adicionar uma nova regra ao [seção de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Dicas e limitações {#tips-limitations}

* ao baixar uma pasta vazia, o [!DNL Experience Manager] transmite uma mensagem de sucesso sobre a criação de um arquivo ZIP, mas o arquivo não é criado.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Baixar ativos protegidos por DRM](drm.md)
>* [Baixe ativos usando o aplicativo de desktop do Experience Manager no desktop Win ou Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Baixar ativos usando o Link de ativos do Adobe nos aplicativos Adobe Creative Cloud compatíveis](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)

