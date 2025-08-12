---
title: Visualizar ativos antes de usá-los nas páginas do AEM Sites
description: O Dynamic Media com recursos de OpenAPI permite visualizar ativos nas páginas de visualização do Adobe Experience Manager (AEM) Sites. Essa visualização de ativos permite que você e suas partes interessadas revisem e validem as atualizações dos ativos antes de publicar as páginas do autor (com ativos atualizados) para consumo público.
role: Admin, User
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: 3f3e091d09b94418fc2cda0bd3b3ce950555b7a9
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# Visualizar ativos antes de usá-los nas páginas do AEM Sites {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

O [!DNL Dynamic Media with OpenAPI capabilities] permite que você visualize ativos disponíveis nas páginas do autor do [!DNL Adobe Experience Manager (AEM) Sites] antes de disponibilizá-los publicamente. A visualização do ativo está disponível no autor do site e no nível de visualização.

Para [visualizar os ativos nas páginas de visualização do AEM Sites](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities), atualize as páginas do autor do site adicionando os ativos que deseja visualizar ou substituindo os existentes disponíveis na página de sites em tempo real. Publique as páginas do autor atualizadas no nível de visualização para gerar um URL de visualização.

Compartilhe a página de visualização com as partes interessadas para coletar feedback sobre a qualidade visual e o alinhamento contextual dos ativos atualizados. Refine os ativos com base no feedback. Crie e gerencie várias versões do ativo durante o ciclo de revisão.

Depois de finalizar os ativos para uso público, atualize-os nas páginas do autor e publique as páginas no nível de publicação para acesso público.

## Antes de começar{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

Verifique se você tem:

* Acesso a [!DNL AEM Assets as a Cloud Service].
* Permissão para editar a propriedade Status dos ativos.
* [Adicionou o valor [!UICONTROL Preview] à propriedade de metadados [!UICONTROL  Status], disponível na guia [!UICONTROL Basic]](/help/assets/metadata-assets-view.md#edit-metadata-forms) do formulário de metadados aplicado à pasta que contém os ativos a serem visualizados.
  ![Adicionar opção de Visualização](/help/assets/assets/metedata-form-preview.png)
* A chave para gerar o token de visualização. [Contate o suporte da Adobe](https://helpx.adobe.com/in/contact.html) e solicite a chave.

## Visualizar ativos na página de visualização dos sites {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

Você pode visualizar novos ativos ou ativos que já foram aprovados. Os ativos aprovados são exibidos somente nas páginas ativas do Sites.

Execute as seguintes etapas para definir o status do ativo para visualização no [!DNL Assets View] e, em seguida, publique sua página de criação do Sites no nível de visualização para gerar uma URL de visualização da página:

1. Defina o status do ativo como **[!UICONTROL Visualizar]** executando as seguintes etapas:

   1. Em [!DNL Assets View], selecione **[!UICONTROL Assets]** e navegue até a pasta.
   1. Selecione o ativo para visualizar.
   1. Clique em **[!UICONTROL Detalhes]**.
   1. No [!UICONTROL Painel de Informações], defina o **[!UICONTROL Status]** como **[!UICONTROL Visualização]** e clique em **[!UICONTROL Salvar]**.
      ![Visualização](/help/assets/assets/preview-boat-at-bay.png)

1. Navegue até a página de criação do Sites. Execute as etapas na seção [Acessar ativos remotos no Editor de páginas do AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) para usar o painel Seletor de ativos para selecionar o ativo que você definiu recentemente para Visualização (status).

   >[!NOTE]
   >
   > O Seletor de ativos exibe ativos com a atualização de status mais recente definida como Aprovado ou Visualizar.

1. Publique sua página no nível de visualização usando a opção **[!UICONTROL Gerenciar publicação]**. Execute as etapas na seção [Publicar conteúdo para visualização](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content) para publicar sua página no nível de visualização. Após a publicação, gere um URL de pré-visualização da página. A página Visualizar exibe os ativos (com as atualizações de status mais recentes) na página Sites.

Compartilhe este URL de visualização com as partes interessadas para análise e feedback. Certifique-se de que as partes interessadas tenham acesso à página de visualização. Consulte [Acessar o serviço de visualização](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service) para obter informações sobre como fornecer acesso às páginas de visualização.

>[!NOTE]
>
>O [componente principal da Imagem V3](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility) dá suporte à versão de visualização de ativos por padrão. Ao selecionar uma versão de visualização de um ativo (ativo com status de visualização) usando o painel [Seletor de ativos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload), o componente de Imagem V3 o renderiza automaticamente no nível de Visualização (uma versão de visualização na página do autor do Sites).

Depois de finalizar a versão do ativo, [publique suas páginas no nível de publicação](#publish-your-pages-to-publish-tier) para consumo público.

## Publicar suas páginas com ativos aprovados para uso público{#publish-your-pages-to-publish-tier}

Depois de finalizar a versão do ativo para uso público, defina o status do ativo como **[!UICONTROL Aprovado]**. Em seguida, publique suas páginas no nível de publicação. Execute as seguintes etapas para publicar suas páginas:

1. Siga a etapa 1 na seção [Visualizar ativos na página de visualização de sites](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) acima para alterar o status do ativo para **[!UICONTROL Aprovado]**.
1. Navegue até a página do autor do Sites e publique-a no [!DNL Publish tier]. Publique as páginas executando as etapas em [Publicação na seção Editor de páginas](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor).
Como alternativa, siga as etapas da seção [Publicação de páginas no Console de sites](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console) para publicar sua página no console do site.

   >[!NOTE]
   >
   > Somente ativos aprovados podem ser entregues no nível de Publicação. Aprove os ativos antes de publicar sua página no nível de Publicação para uso público.

   ![A página foi publicada](/help/assets/assets/the-page-has-been-publushed.png)
Uma mensagem de confirmação **[!UICONTROL The page has been published]** é exibida após a publicação bem-sucedida. Navegue até a página publicada no nível de publicação para confirmar se as atualizações estão ativas e se o conteúdo é exibido conforme esperado.
