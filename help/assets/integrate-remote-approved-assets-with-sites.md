---
title: Integrar o AEM Assets remoto com o AEM Sites
description: Saiba como configurar e conectar sites AEM com o Approved AEM Assets no Creative Cloud.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Integrar o AEM Assets remoto com o AEM Sites  {#integrate-approved-assets}

O gerenciamento eficaz de ativos digitais é fundamental para fornecer experiências de marca envolventes e consistentes em várias plataformas online. O Dynamic Media com recursos OpenAPI aprimora o gerenciamento de ativos digitais, permitindo uma integração perfeita entre o AEM Sites e o AEM Assets as a Cloud Service. Esse recurso inovador permite compartilhar e gerenciar facilmente diferentes tipos de ativos digitais aprovados em vários ambientes AEM, simplificando os fluxos de trabalho para autores de sites e editores de conteúdo.

O Dynamic Media com recursos OpenAPI permite que os autores de sites usem ativos do DAM remoto diretamente no Editor de páginas do AEM e [Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), simplificando os processos de criação e gerenciamento de conteúdo.

Os usuários podem conectar várias instâncias do AEM Sites, sem restrições quanto ao número máximo, a uma implantação remota do DAM, uma vantagem notável sobre o recurso [Assets conectado](use-assets-across-connected-assets-instances.md).

![imagem](/help/assets/assets/connected-assets-rdam.png)

Após a configuração inicial, os usuários podem criar páginas na instância do AEM Sites e adicionar ativos, conforme necessário. Ao adicionar ativos, eles podem selecionar ativos armazenados no DAM local ou procurar e usar os ativos disponíveis no DAM remoto.

O Dynamic Media com recursos OpenAPI oferece vários outros benefícios, como acessar e usar ativos remotos no fragmento de conteúdo, buscar metadados dos ativos remotos e muito mais. Saiba mais sobre os outros [benefícios do Dynamic Media com recursos OpenAPI sobre o Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Antes de começar {#pre-requisits-sites-integration}

* Configure as [variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) a seguir para o AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` refere-se à ID do programa <br>
     `eYYYY` refere-se à ID de ambiente

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  ou defina as [configurações de OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) para AEM 6.5 na instância do AEM Sites seguindo estas etapas:

   1. Entre no console e clique em **[!UICONTROL OSGi] >** ou
usar a URL direta; por exemplo: `http://localhost:4502/system/console/configMgr`

   1. Adicionar o **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; e **[!UICONTROL imsClient]**= [IMSClientId]
Saiba mais sobre [Autenticação IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* Acesso IMS para fazer logon na instância remota do AEM as a Cloud Service DAM.

* Ative o Dynamic Media com recursos OpenAPI alternados no DAM remoto.

* Configure o componente de Imagem v3 na instância do AEM Sites. Se o componente não estiver presente, baixe e instale o [pacote de conteúdo](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Acessar ativos do DAM remoto {#fetch-assets}

O Dynamic Media com recursos OpenAPI permite acessar ativos disponíveis em sua instância do DAM remoto no editor de páginas do AEM Sites local e no fragmento de conteúdo do AEM.

![imagem](/help/assets/assets/open-APIs.png)

### Acessar ativos remotos no Editor de páginas do AEM {#access-assets-page-editor}

Siga as etapas abaixo para usar ativos remotos no Editor de páginas AEM na sua instância do AEM Sites. Essa integração pode ser feita no AEM as a Cloud Service e no AEM 6.5.

1. Vá para **[!UICONTROL Sites]** > _seu site_ onde o AEM **[!UICONTROL Página]** está presente e no qual você precisa adicionar o ativo remoto.
1. Navegue até a **[!UICONTROL Página]** do AEM específica em seu site na seção **[!UICONTROL Sites]** onde você pretende adicionar o ativo remoto.
1. Selecione a página e clique em **[!UICONTROL Editar (_e_)]**. O AEM **[!UICONTROL Editor de páginas]** se abre.
1. Clique no Contêiner de layout e adicione um componente **[!UICONTROL Imagem]**.
1. Clique no componente **[!UICONTROL Imagem]** e clique no ícone ![configurações](/help/assets/assets/do-not-localize/settings-icon.svg).
1. Desmarque a opção **[!UICONTROL Herdar imagem em destaque da página]**.
1. Clique em **[!UICONTROL Escolher]** e selecione **[!UICONTROL Remoto]**.
   ![imagem](/help/assets/assets/uncheck-inherit-option.jpg)

   Você será solicitado a fazer logon.
1. Selecione o ativo e clique em **[!UICONTROL Selecionar]**.
1. Adicione um texto alternativo e clique em **[!UICONTROL Concluído]**.
   <br> O ativo remoto aparece no componente de imagem. Você também pode verificar o URL de entrega do ativo quando ele é carregado na página ou usando a guia &quot;Visualizar&quot;. A URL de entrega indica que o ativo está sendo acessado remotamente.

Você pode acessar ativos remotos no editor de página do AEM pronto para uso somente para o Componente principal de imagem v3 e Componente principal de teaser v2. Para outros componentes, incluindo componentes personalizados, são necessárias personalizações para integrar o Seletor de ativos a esses componentes.

#### Vídeo: acessar ativos remotos no editor de páginas AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Acessar ativos remotos no fragmento de conteúdo do AEM {#access-assets-content-fragment}

Siga as etapas abaixo para usar ativos remotos no Fragmento de conteúdo do AEM na sua instância do AEM Sites. Você pode fazer essa integração no AEM 6.5 e não no AEM as a Cloud Service.

1. Vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Selecione a pasta de ativos na qual o fragmento de conteúdo está presente.
1. Selecione o Fragmento do conteúdo e clique em **[!UICONTROL Editar (_e_)]**.

   >[!NOTE]
   >
   >Se você não tiver um modelo de Fragmento de conteúdo AEM, talvez precise [criar um](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Clique no ícone de ![marca de seleção](/help/assets/assets/do-not-localize/checkmark-icon.svg) ao lado do componente de texto.
1. Selecione **[!UICONTROL Remoto]** para buscar o ativo do DAM Remoto. <br>
Você pode escolher o repositório DAM **[!UICONTROL Local]** ou **[!UICONTROL Remoto]** de acordo com a sua necessidade.

   ![imagem](/help/assets/assets/cf-pick.jpg)
Você será solicitado a fazer logon.
1. Escolha o ativo e clique em **[!UICONTROL Selecionar]**.
   <br> A URL do ativo remoto aparece no componente de texto.

#### Vídeo: acessar ativos remotos no fragmento de conteúdo do AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Acessar ativos remotos no Edge Delivery Services {#access-assets-eds}

Você também pode acessar ativos remotos no Edge Delivery Services. Para obter mais informações, consulte [Utilização de ativos do Assets as a Cloud Service entregues usando o Dynamic Media com recursos OpenAPI](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi).
