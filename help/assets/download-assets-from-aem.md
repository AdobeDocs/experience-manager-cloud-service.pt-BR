---
title: Baixar ativos
description: Baixe ativos de [!DNL Adobe Experience Manager Assets] e ative ou desative a funcionalidade de download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---


# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Você pode baixar ativos, incluindo representações estáticas e dinâmicas. Como alternativa, você pode enviar emails com links para ativos diretamente de [!DNL Adobe Experience Manager Assets]. Os ativos baixados são agrupados em um arquivo ZIP. O arquivo ZIP compactado tem um tamanho máximo de 1 GB para o trabalho de exportação. São permitidos no máximo 500 ativos por trabalho de exportação.

>[!NOTE]
>
>Recipient de e-mails devem ser membros do grupo `dam-users` para acessar o link de download ZIP na mensagem de e-mail. Para poder baixar os ativos, os membros devem ter permissões para iniciar workflows que acionam o download de ativos.

Os tipos de ativos Conjuntos de imagens, Conjuntos de rotação, Conjuntos de mídia mista e Conjuntos de carrossel não podem ser baixados.

Você pode baixar ativos do Experience Manager usando os seguintes métodos:

* [interface do usuário Experience Manager](#download-in-aem)
* Interface do usuário do compartilhamento do link de ativo
* [Commons de compartilhamento de ativos](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicativo para desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Baixar ativos usando AEM interface {#download-in-aem}

O serviço de download assíncrono fornece uma estrutura para o download ininterrupto de ativos de grande porte. Arquivos menores são baixados da interface do usuário em tempo real. Os arquivos grandes são baixados de forma assíncrona e os usuários são informados da conclusão por meio de notificações de Experience Manager na Caixa de entrada. Consulte [compreendendo a caixa de entrada do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html).

![Notificação de download](assets/download-notification.png)

*Figura: Baixar notificação via  [!DNL Experience Manager] Caixa de entrada.*

Os downloads assíncronos são acionados em um dos seguintes casos:

* Se houver mais de 10 ativos ou mais de 100 MB a serem baixados.
* Se o download levar mais de 30 segundos para ser preparado.

Para baixar ativos, siga estas etapas:

1. Na interface do usuário [!DNL Experience Manager], clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até os ativos que deseja baixar. Selecione a pasta ou selecione um ou mais ativos na pasta. Na barra de ferramentas, clique em **[!UICONTROL Download]**.

   ![Opções disponíveis ao baixar ativos de  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Figura: Opções da caixa de diálogo de download.*

1. Na caixa de diálogo Download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para incluir cada ativo que você baixar, incluindo ativos em pastas filhas aninhadas sob a pasta pai do ativo, em uma pasta no computador local. Quando essa opção for *not* selecione, por padrão, a hierarquia de pastas será ignorada e todos os ativos serão baixados em uma pasta no computador local. |
   | **[!UICONTROL E-mail]** | Selecione essa opção para que uma notificação por email seja enviada ao recipient. Os modelos padrão de e-mails estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em seu formulário original sem execuções.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representações]** | Uma representação é uma representação binária de um ativo. Os ativos têm uma representação principal - a do arquivo carregado. Podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Cortes inteligentes]** | Selecione esta opção para baixar todas as representações de recorte inteligente do ativo selecionado de dentro de [!DNL Experience Manager]. Um arquivo zip com as execuções de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Execução(ões) dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente selecionando na lista [Predefinição de imagem](/help/assets/dynamic-media/image-presets.md). <br>Além disso, é possível selecionar o tamanho e a unidade de medida, o formato, o espaço de cor, a resolução e qualquer modificador de imagem opcional, como inverter a imagem. A opção só estará disponível se você tiver [!DNL Dynamic Media] ativado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Download]**.

## Habilitar servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] permite que os usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos. A preparação para download pode ter implicações de desempenho ou pode até mesmo sobrecarregar o servidor e a rede. Para atenuar esses riscos potenciais do tipo DoS causados por esse recurso, o componente `AssetDownloadServlet` OSGi está desabilitado para instâncias de publicação.

Para permitir o download de ativos do DAM, digamos ao usar algo como o Asset Share Commons ou outra implementação semelhante ao portal, ative manualmente o servlet por meio de uma configuração OSGi. O Adobe recomenda que o tamanho de download permitido seja o mais baixo possível, sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que público alvo o modo de execução de publicação, ou seja, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Na pasta de configuração, crie um novo arquivo do tipo `nt:file` chamado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencha `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como valor de `asset.download.prezip.maxcontentsize`. A amostra abaixo configura o tamanho máximo do download ZIP para não exceder 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

O `Asset Download Servlet` pode ser desativado em [!DNL Experience Manager] instâncias de publicação atualizando a configuração do dispatcher para bloquear quaisquer solicitações de download de ativos. O servlet também pode ser desabilitado manualmente por meio do console OSGi diretamente.

1. Para bloquear as solicitações de download de ativos por meio de uma configuração do dispatcher, edite a configuração `dispatcher.any` e adicione uma nova regra à seção [filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Baixar ativos protegidos pelo DRM](drm.md)
>* [Baixar ativos usando o aplicativo de desktop Experience Manager no desktop Win ou Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Baixe ativos usando o Link de ativos do Adobe nos aplicativos Adobe Creative Cloud suportados](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)

