---
title: Baixar ativos
description: Baixe ativos do  [!DNL Adobe Experience Manager Assets] e habilite ou desabilite a funcionalidade de download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 4%

---

# Baixar ativos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

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
* [Comuns de compartilhamento de ativos](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=pt-BR)
* [Aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR#download-assets)

## Baixar ativos usando a interface [!DNL Experience Manager] {#download-assets}

O Experience Manager otimiza a experiência de download com base na quantidade e no tamanho do ativo. Arquivos menores são baixados da interface do usuário em tempo real. O [!DNL Experience Manager] baixa diretamente solicitações de ativos únicos para o arquivo original, em vez de colocar ativos únicos em um arquivo ZIP para permitir downloads mais rápidos. O Experience Manager permite downloads grandes com solicitações assíncronas. As solicitações de download maiores que 100 GB são divididas em vários arquivos ZIP com um tamanho máximo de 100 MB cada.

Por padrão, [!DNL Experience Manager] aciona uma notificação na [[!DNL Experience Manager] Caixa de Entrada](/help/sites-cloud/authoring/inbox.md) ao gerar um arquivo de download.

![Notificação da Caixa de entrada](assets/inbox-notification-for-large-downloads.png)


### Ativar notificações por email para downloads grandes {#enable-emails-for-large-downloads}

Os downloads assíncronos são acionados em qualquer um dos seguintes casos:

* Se houver mais de dez ativos
* Se o tamanho do download for superior a 100 MB
* Se o download levar mais de 30 segundos para se preparar

Enquanto o download assíncrono é executado no back-end, o usuário pode continuar a explorar e trabalhar mais no Experience Manager. Além das notificações da caixa de entrada do Experience Manager, o Experience Manager pode enviar emails para notificar o usuário na conclusão do processo de download. Para habilitar este recurso, os administradores podem configurar o serviço de email [configurando uma conexão de servidor SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR#sending-email).

Depois que o serviço de email é configurado, os administradores e usuários podem ativar notificações por email na interface do Experience Manager.

Para ativar notificações por email:

1. Faça logon em [!DNL Experience Manager Assets].
1. Clique no ícone do usuário no canto superior direito e em **[!UICONTROL Minhas Preferências]** para abrir a janela Preferências do Usuário.
1. Marque a caixa de seleção **[!UICONTROL Notificações por email de download de ativos]** e clique em **[!UICONTROL Aceitar]**.

   ![habilitar-email-notificações-para-downloads-grandes](/help/assets/assets/enable-email-for-large-downloads.png)


Para baixar ativos, siga estas etapas:

1. Na interface de usuário do [!DNL Experience Manager], clique em **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Navegue até os ativos que deseja baixar. Selecione a pasta ou selecione um ou mais ativos na pasta. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.

   ![Opções disponíveis ao baixar ativos de [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Na caixa de diálogo de download, selecione as opções de download desejadas.

   | Opção de download | Descrição |
   |---|---|
   | **[!UICONTROL Criar uma pasta separada para cada ativo]** | Selecione essa opção para criar uma pasta para cada ativo que contenha todas as representações baixadas do ativo. Se não estiver selecionada, cada ativo (e suas representações, se selecionado para download) estará contido na pasta principal do arquivo gerado. |
   | **[!UICONTROL Email]** | Selecione essa opção para enviar uma notificação por email (contendo um link para o download) para outro usuário. O usuário destinatário deve ser membro do grupo `dam-users`. Os modelos padrão de email estão disponíveis nos seguintes locais:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Os modelos que você personaliza durante a implantação estão disponíveis nos seguintes locais: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Você pode armazenar modelos personalizados específicos do locatário nos seguintes locais:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ativo(s)]** | Selecione essa opção para baixar o ativo em sua forma original.<br>A opção de subativos estará disponível se o ativo original tiver subativos. |
   | **[!UICONTROL Representação(ões)]** | Uma representação é a representação binária de um ativo. O Assets tem uma representação principal - a do arquivo carregado. Eles podem ter qualquer número de representações. <br> Com essa opção, você pode selecionar as representações que deseja baixar. As representações disponíveis dependem do ativo selecionado. |
   | **[!UICONTROL Recortes inteligentes]** | Selecione esta opção para baixar todas as representações de corte inteligente do ativo selecionado no [!DNL Experience Manager]. Um arquivo zip com as representações de Recorte inteligente é criado e baixado no computador local. |
   | **[!UICONTROL Representação(ões) Dinâmica(s)]** | Selecione essa opção para gerar uma série de representações alternativas em tempo real. Ao selecionar essa opção, você também seleciona as representações que deseja criar dinamicamente, selecionando na lista [Predefinição de imagem](/help/assets/dynamic-media/image-presets.md). <br>Além disso, você pode selecionar o tamanho e a unidade de medida, o formato, o espaço de cores, a resolução e qualquer modificador de imagem opcional, como a inversão da imagem. A opção só estará disponível se você tiver o [!DNL Dynamic Media] habilitado. |

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]**.

   Se a notificação por email estiver ativada para downloads grandes, um email contendo um URL de download da pasta zip arquivada será exibido em sua caixa de entrada. Clique no link de download no email para baixar o arquivo zip.

   ![notificações por email para downloads grandes](/help/assets/assets/email-for-large-notification.png)

   Você também pode exibir a notificação em sua Caixa de Entrada do [!DNL Experience Manager].

   ![caixa de entrada-notificações-para-downloads-grandes](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Baixar ativos compartilhados usando o compartilhamento de link {#link-share-download}

O compartilhamento de ativos usando um link é uma maneira conveniente de disponibilizá-lo às pessoas interessadas sem que elas precisem fazer logon no [!DNL Assets]. Consulte [funcionalidade de Compartilhamento de Links](/help/assets/share-assets.md#sharelink).

Quando os usuários baixam ativos de links compartilhados, o [!DNL Assets] usa um serviço assíncrono que oferece downloads mais rápidos e ininterruptos. Os ativos a serem baixados são enfileirados em segundo plano em uma caixa de entrada em arquivos ZIP de tamanho de arquivo gerenciável. Para downloads maiores, o download é dividido em arquivos de 100 GB.

A [!UICONTROL Caixa de Entrada de Download] exibe o status de processamento de cada arquivo. Quando o processamento estiver concluído, você poderá baixar os arquivos da caixa de entrada.

![Baixar caixa de entrada](assets/link-sharing-download-inbox.png)

## Ativar o servlet de download de ativos {#enable-asset-download-servlet}

O servlet padrão em [!DNL Experience Manager] permite que usuários autenticados emitam arbitrariamente grandes solicitações de download simultâneas para criar arquivos ZIP de ativos. A preparação do download pode ter implicações de desempenho ou pode até sobrecarregar o servidor e a rede. Para mitigar esses possíveis riscos semelhantes ao DoS causados por esse recurso, o componente OSGi `AssetDownloadServlet` é desabilitado para instâncias de publicação. Se você não precisar do recurso de download nas instâncias do autor, desative o servlet no autor.

Para permitir o download de ativos do seu DAM, ao usar algo como o Asset Share Commons ou outra implementação semelhante a um portal, ative manualmente o servlet por meio de uma configuração OSGi. A Adobe recomenda definir o tamanho permitido do download o mais baixo possível, sem afetar os requisitos diários de download. Um valor alto pode afetar o desempenho.

1. Crie uma pasta com uma convenção de nomenclatura que direcione ao modo de execução de publicação, ou seja, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Na pasta de configuração, crie um arquivo do tipo `nt:file` chamado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Preencha `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` com o seguinte. Define um tamanho máximo (em bytes) para o download como o valor de `asset.download.prezip.maxcontentsize`. O exemplo abaixo configura o tamanho máximo do download do ZIP para não exceder 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Desativar o servlet de download de ativos {#disable-asset-download-servlet}

Se você não precisar da funcionalidade de download, desative o servlet para evitar riscos semelhantes ao DoS. O `Asset Download Servlet` pode ser desativado em instâncias de autor e publicação [!DNL Experience Manager] ao atualizar a configuração do Dispatcher para bloquear qualquer solicitação de download de ativos. O servlet também pode ser desativado manualmente por meio do console OSGi diretamente.

1. Para bloquear solicitações de download de ativos por meio de uma configuração do Dispatcher, edite a configuração `dispatcher.any` e adicione uma nova regra à [seção de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Representação OnTime ou OffTime {#on-off-time-rendition}

Para habilitar o serviço `OnOffTimeAssetAccessFilter`, é necessário criar uma configuração OSGi. Esse serviço permite o bloqueio de acesso a representações e metadados, além do próprio ativo, com base em configurações de tempo de ativação/desativação. A configuração OSGi deve ser para `com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`. Siga as etapas abaixo:

1. No código do projeto no Git, crie um arquivo de configuração em `/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`. O arquivo deve conter `{}` como conteúdo, o que significa uma configuração OSGi vazia para o componente OSGi correspondente. Essa ação ativa o serviço.
1. Implante seu código, incluindo esta nova configuração, através de [!DNL Cloud Manager].
1. Depois de implantados, as representações e os metadados ficam acessíveis de acordo com as configurações de tempo de ativação/desativação dos ativos. Se a data ou a hora atual for anterior à hora de ativação ou posterior à hora de desativação, uma mensagem de erro será exibida.
Para obter mais detalhes sobre como adicionar uma configuração OSGi vazia, consulte este [guia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=pt-BR).

## Dicas e limitações {#tips-limitations}

* Se você baixar uma pasta vazia, o [!DNL Experience Manager] transmitirá uma mensagem de sucesso sobre a criação de um arquivo ZIP, mas o arquivo não será criado.

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
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Baixar ativos protegidos por DRM](drm.md)
>* [Baixar ativos usando o aplicativo de desktop Experience Manager no Win ou no Mac desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR)
>* [Baixe ativos usando o Adobe Assets Link nos aplicativos Adobe Creative Cloud compatíveis](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)
