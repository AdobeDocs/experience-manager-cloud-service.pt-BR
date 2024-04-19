---
title: Integrar o AEM Assets remoto com o AEM Sites
description: Saiba como configurar e conectar sites AEM com o Approved AEM Assets no Creative Cloud.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Integrar o AEM Assets remoto com o AEM Sites  {#integrate-approved-assets}

O gerenciamento eficaz de ativos digitais é fundamental para fornecer experiências de marca envolventes e consistentes em várias plataformas online. O Dynamic Media com recursos OpenAPI aprimora o gerenciamento de ativos digitais, permitindo uma integração perfeita entre o AEM Sites e o AEM Assets remoto. Esse recurso inovador permite compartilhar e gerenciar facilmente diferentes tipos de ativos digitais aprovados em vários ambientes AEM, simplificando os fluxos de trabalho para autores de sites e editores de conteúdo.

O Dynamic Media com recursos OpenAPI permite que os autores de sites usem ativos do DAM remoto diretamente no Editor de páginas AEM e [Fragmento do conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), simplificando os processos de criação e gerenciamento de conteúdo.

Os usuários podem conectar várias instâncias do AEM Sites, sem restrições quanto ao número máximo, a uma implantação remota de DAM, uma vantagem notável sobre o [Connected Assets](use-assets-across-connected-assets-instances.md) recurso.

![imagem](/help/assets/assets/connected-assets-rdam.png)

Após a configuração inicial, os usuários podem criar páginas na instância do AEM Sites e adicionar ativos, conforme necessário. Ao adicionar ativos, eles podem selecionar ativos armazenados no DAM local ou procurar e usar os ativos disponíveis no DAM remoto.

O Dynamic Media com recursos OpenAPI oferece vários outros benefícios, como acessar e usar ativos remotos no fragmento de conteúdo, buscar metadados dos ativos remotos e muito mais. Saber mais sobre o outro [benefícios do Dynamic Media com recursos OpenAPI em relação ao Connected Assets](/help/assets/new-dynamic-media-apis-faqs.md).

## Antes de começar

* Configurar o seguinte [variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` refere-se à ID do programa <br>
     `eYYYY` refere-se à ID de ambiente

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  ou configure o [Configurações de OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) para AEM 6.5 na instância do AEM Sites, siga estas etapas:

   1. Faça logon no console e clique em **[!UICONTROL OSGi] >** ou use o URL direto; por exemplo: `http://localhost:4502/system/console/configMgr`

   1. Adicione o **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; e **[!UICONTROL imsClient]**= [IMSClientId]
Saiba mais sobre [Autenticação IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* Acesso IMS para fazer logon na instância remota DAM AEM as a Cloud Service.

* Ative o Dynamic Media com recursos OpenAPI alternados no DAM remoto.

* Configure o componente de Imagem v3 na instância do AEM Sites. Se o componente não estiver presente, baixe e instale o [pacote de conteúdo](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Acessar ativos do DAM remoto {#fetch-assets}

O Dynamic Media com recursos OpenAPI permite acessar ativos disponíveis em sua instância do DAM remoto no editor de páginas do AEM Sites local e no fragmento de conteúdo do AEM.

![imagem](/help/assets/assets/open-APIs.png)

### Acessar ativos remotos no Editor de páginas do AEM

Siga as etapas abaixo para usar ativos remotos no Editor de páginas AEM na sua instância do AEM Sites. Você pode fazer essa integração no AEM as a Cloud Service e no AEM 6.5.

1. Ir para **[!UICONTROL Sites]** > _seu site_ em que o AEM **[!UICONTROL Página]** O está presente no qual você precisa adicionar o ativo remoto.
1. Navegar até o AEM específico **[!UICONTROL Página]** no seu site sob o **[!UICONTROL Sites]** seção na qual você pretende adicionar o ativo remoto.
1. Selecione a página e clique em **[!UICONTROL Editar (_e_)]**. O AEM **[!UICONTROL Editor de páginas]** é aberto.
1. Clique no Contêiner de layout e adicione um **[!UICONTROL Imagem]** componente.
1. Clique em **[!UICONTROL Imagem]** e clique em ![ícone de configurações](/help/assets/assets/do-not-localize/settings-icon.svg) ícone.
1. Desmarque a opção **[!UICONTROL Herdar imagem em destaque da página]** opção.
1. Clique em **[!UICONTROL Escolher]** e selecione **[!UICONTROL Remoto]**.
   ![imagem](/help/assets/assets/uncheck-inherit-option.jpg)

   Você será solicitado a fazer logon.
1. Selecione o ativo e clique em **[!UICONTROL Selecionar]**.
1. Adicione um texto alternativo e clique em **[!UICONTROL Concluído]**.
   <br> O ativo remoto aparece no componente de imagem. Você também pode verificar o URL de entrega do ativo quando ele é carregado na página ou usando a guia &quot;Visualizar&quot;. A URL de entrega indica que o ativo está sendo acessado remotamente.

#### Vídeo: acessar ativos remotos no editor de páginas AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Acessar ativos remotos no fragmento de conteúdo do AEM

Siga as etapas abaixo para usar ativos remotos no Fragmento de conteúdo do AEM na sua instância do AEM Sites. Você pode fazer essa integração no AEM 6.5 e não no AEM as a Cloud Service.

1. Ir para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Selecione a pasta de ativos na qual o fragmento de conteúdo está presente.
1. Selecione o fragmento de conteúdo e clique em **[!UICONTROL Editar (_e_)]**.

   >[!NOTE]
   >
   >Se você não tiver um modelo de fragmento de conteúdo do AEM, talvez seja necessário [criar um](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Clique em ![ícone de marca de seleção](/help/assets/assets/do-not-localize/checkmark-icon.svg) ícone ao lado do componente de texto.
1. Selecionar **[!UICONTROL Remoto]** para buscar o ativo do DAM remoto. <br>
Você pode escolher **[!UICONTROL Local]** ou **[!UICONTROL Remoto]** Repositório DAM com base em suas necessidades.

   ![imagem](/help/assets/assets/cf-pick.jpg)
Você será solicitado a fazer logon.
1. Escolha o ativo e clique em **[!UICONTROL Selecionar]**.
   <br> O URL do ativo remoto aparece no componente de texto.

#### Vídeo: acessar ativos remotos no fragmento de conteúdo do AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
