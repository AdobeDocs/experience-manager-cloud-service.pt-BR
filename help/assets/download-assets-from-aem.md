---
title: Baixar ativos
description: Baixe ativos a partir de [!DNL Adobe Experience Manager Assets] e ative ou desative a funcionalidade de download.
contentOwner: AG
feature: Gerenciamento de ativos
role: Business Practitioner
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 4c3007b9e38f8a18d61b781ddbcd00bd45b67729
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 4%

---

# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente de [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

>[!NOTE]
>
>Os recipients de emails devem ser membros do grupo `dam-users` para acessar o link de download do ZIP na mensagem de email. Para baixar os ativos, os membros devem ter permissões para iniciar fluxos de trabalho que acionam o download de ativos.

Os tipos de ativos Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

Você pode baixar ativos do Experience Manager usando os seguintes métodos:

<!-- * [Link Share](#link-share-download) -->

* [Interface do usuário do Experience Manager](#download-assets)
* [Compartilhamento de ativos Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Baixar ativos usando a interface [!DNL Experience Manager] {#download-assets}

O serviço de download assíncrono fornece uma estrutura para o download perfeito de ativos de grande porte. Arquivos menores são baixados da interface do usuário em tempo real. [!DNL Experience Manager] não arquiva downloads de ativos únicos onde o arquivo original é baixado. Essa funcionalidade permite downloads mais rápidos. Os arquivos grandes são baixados de forma assíncrona e [!DNL Experience Manager] notifica a conclusão através de notificações na Caixa de entrada. Consulte [entender [!DNL Experience Manager] Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

![Baixar notificação](assets/download-notification.png)

*Figura: Baixar notificação por meio da  [!DNL Experience Manager] Caixa de entrada.*

Os downloads assíncronos são acionados em um dos seguintes casos:

* Se houver mais de 10 ativos ou mais de 100 MB para download.
* Se o download demorar mais de 30 segundos para se preparar.

Para baixar ativos, siga estas etapas:

1. Na interface do usuário [!DNL Experience Manager], clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até os ativos que deseja baixar. Selecione a pasta ou selecione um ou mais ativos na pasta. Na barra de ferramentas, clique em **[!UICONTROL Download]**.

   ![Opções disponíveis ao baixar ativos do  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Figura: Opções da caixa de diálogo Download.*

1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo que você baixar, incluindo ativos em pastas filhas aninhadas na pasta principal do ativo, em uma pasta no computador local. Quando essa opção é *not*, selecione, por padrão, a hierarquia de pastas é ignorada e todos os ativos são baixados em uma pasta no computador local. |
   | **[!UICONTROL E-mail]** | Selecione essa opção para enviar uma notificação por email para o recipient. Os modelos padrão de emails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos personalizados durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original sem nenhuma representação.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal: a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione esta opção para baixar todas as representações de recorte inteligente do ativo selecionado de dentro de [!DNL Experience Manager]. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente selecionando na lista [Predefinição de imagem](/help/assets/dynamic-media/image-presets.md). <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cores, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] ativado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Download]**.

<!-- TBD: Commenting from May release because the feature is moved to June release 2021.6.0.
## Download assets shared using link sharing {#link-share-download}

Sharing assets using a link is a convenient way to make it available to interested people without them having to first log in to [!DNL Assets]. To generate a URL to share assets, use the [Link Share functionality](/help/assets/share-assets.md#sharelink). 

When users download assets from shared links, [!DNL Assets] uses an asynchronous service that offers faster and and uninterrupted downloads. The assets to be downloaded are queued in the background in an inbox into ZIP archives of manageable file size. For very large downloads, the download is chunked into files of 100 GB in size.

The inbox displays the processing status of each archive. Once the processing is complete, you can download the archives from the inbox.

![Download inbox](assets/download-inbox.png)
-->

## Habilitar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] permite que usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos. A preparação do download pode ter implicações de desempenho ou pode até mesmo sobrecarregar o servidor e a rede. Para mitigar esses potenciais riscos do tipo DoS causados por esse recurso, o componente `AssetDownloadServlet` OSGi é desabilitado para instâncias de publicação. Se você não precisar do recurso de download em instâncias do autor, desative o servlet no autor.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante a portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho de download permitido o mais baixo possível sem afetar os requisitos diários de download. Um alto valor pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que seja direcionada ao modo de execução de publicação, ou seja, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Na pasta de configuração, crie um novo arquivo do tipo `nt:file` chamado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencha `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como valor de `asset.download.prezip.maxcontentsize`. A amostra abaixo configura o tamanho máximo do download ZIP para não exceder 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

Se você não precisar da funcionalidade de download, desative o servlet para evitar riscos semelhantes a DoS. O `Asset Download Servlet` pode ser desativado em [!DNL Experience Manager] instâncias de autor e publicação, atualizando a configuração do dispatcher para bloquear qualquer solicitação de download de ativos. O servlet também pode ser desabilitado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração de dispatcher, edite a configuração `dispatcher.any` e adicione uma nova regra à seção de filtro [a2/>.](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Baixar ativos protegidos por DRM](drm.md)
* [Baixar ativos usando o aplicativo de desktop do Experience Manager no desktop Win ou Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR)
* [Baixar ativos usando o Link de ativos do Adobe nos aplicativos Adobe Creative Cloud compatíveis](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)

