---
title: Integrar o AEM Assets remoto com o AEM Sites
description: Saiba como configurar e conectar sites do AEM com o Approved AEM Assets.
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 11%

---

# Integrar o AEM Assets remoto com o AEM Sites  {#integrate-approved-assets}

O gerenciamento eficaz de ativos digitais é fundamental para fornecer experiências de marca envolventes e consistentes em várias plataformas online. O Dynamic Media com recursos de OpenAPI aprimora o gerenciamento de ativos digitais, permitindo uma integração perfeita entre o AEM Sites e o AEM Assets as a Cloud Service. Esse recurso inovador permite compartilhar e gerenciar facilmente diferentes tipos de ativos digitais aprovados em vários ambientes do AEM, simplificando os fluxos de trabalho para autores de sites e editores de conteúdo.

O Dynamic Media com recursos OpenAPI permite que os autores de sites usem ativos do DAM remoto diretamente no Editor de páginas do AEM e [Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html?lang=pt-BR), simplificando os processos de criação e gerenciamento de conteúdo.

Os usuários podem conectar várias instâncias do AEM Sites, sem restrições quanto ao número máximo, a uma implantação remota do DAM, uma vantagem notável sobre o recurso [Assets conectado](use-assets-across-connected-assets-instances.md).

![imagem](/help/assets/assets/connected-assets-rdam.png)

Após a configuração inicial, os usuários podem criar páginas na instância do AEM Sites e adicionar ativos, conforme necessário. Ao adicionar ativos, eles podem selecionar ativos armazenados no DAM local ou procurar e usar os ativos disponíveis no DAM remoto.

O Dynamic Media com recursos de OpenAPI oferece vários outros benefícios, como acessar e usar ativos remotos no fragmento de conteúdo, buscar metadados dos ativos remotos e muito mais. Saiba mais sobre os outros [benefícios do Dynamic Media com recursos OpenAPI em relação ao Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Antes de começar {#pre-requisites-sites-integration}

O suporte a ativos remotos usando o Dynamic Media com recursos OpenAPI exige:

* AEM 6.5 SP 18+ ou AEM as a Cloud Service

* Versão 2.23.2 ou posterior dos Componentes principais

* Configure as [variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) a seguir para o AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>

     `pXXXX` refere-se à ID do programa <br>
     `eYYYY` refere-se à ID de ambiente

  Essas variáveis são definidas usando a interface do usuário do Cloud Manager do ambiente do AEM as a Cloud Service que atua como a instância do Sites local.

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]: é necessário enviar um tíquete de suporte do Adobe para obter a ID do Cliente IMS.

     ou defina as [configurações do OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html?lang=pt-BR) para o AEM 6.5 na instância do AEM Sites seguindo estas etapas:

   1. Entre no console e clique em **[!UICONTROL OSGi] >** ou
usar a URL direta; por exemplo: `https://localhost:4502/system/console/configMgr`

   1. Configure a **Configuração de Mídia dinâmica de próxima geração** (`NextGenDynamicMediaConfigImpl`) com a seguinte configuração OSGi, substituindo os valores pelos do ambiente de ativos remoto.

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` não é uma entrada obrigatória.
      `repositoryId` = &quot;delivery-pxxxx-eyyyyy.adobeaemcloud.com&quot;
onde `pXXXX` refere-se à ID do programa
      `eYYYY` refere-se à ID de ambiente

      ![A janela de configuração OSGi do Dynamic Media de última geração](/help/assets/assets/remote-assets-osgi.png)

  Saiba mais sobre [Autenticação IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html?lang=pt-BR).

  Para obter detalhes sobre como configurar o OSGi, consulte os seguintes documentos:

   * [Configuração OSGi para o Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=pt-BR) no AEM as a Cloud Service
   * [Configuração do OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=pt-BR) para AEM 6.5

* Acesso IMS para fazer logon na instância remota do AEM as a Cloud Service DAM. Refere-se ao autor do Sites que tem acesso IMS ao ambiente remoto do DAM.

* Configure o componente de Imagem v3 na instância do AEM Sites. Se o componente não estiver presente, baixe e instale o [pacote de conteúdo](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Configurar HTTPS {#https}

Geralmente, é recomendável executar todas as instâncias de produção do AEM usando HTTPs. No entanto, os ambientes de desenvolvimento locais podem não estar configurados dessa forma. No entanto, os ativos remotos que usam o Dynamic Media com OpenAPI precisam de HTTPS para funcionar.

[Use este guia](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=pt-BR) para configurar HTTPS sempre que desejar usar ativos remotos, incluindo ambientes de desenvolvimento.

## Acessar ativos do DAM remoto {#fetch-assets}

O Dynamic Media com recursos OpenAPI permite acessar ativos disponíveis na instância do DAM remoto no editor de páginas do AEM Sites local e no fragmento de conteúdo do AEM.

![imagem](/help/assets/assets/open-APIs.png)

### Acessar ativos remotos no Editor de páginas do AEM {#access-assets-page-editor}

Siga as etapas abaixo para usar ativos remotos no Editor de páginas do AEM na instância do AEM Sites. Essa integração pode ser feita no AEM as a Cloud Service e no AEM 6.5.

1. Vá para **[!UICONTROL Sites]** > _seu site_ onde a **[!UICONTROL Página]** do AEM está presente e onde você precisa adicionar o ativo remoto.
1. Selecione a página e clique em **[!UICONTROL Editar (_e_)]**. O **[!UICONTROL Editor de páginas]** do AEM é aberto.
1. Clique no Contêiner de layout e adicione um componente **[!UICONTROL Imagem]**.
1. Clique no componente **[!UICONTROL Imagem]** e clique no ícone ![configurações](/help/assets/assets/do-not-localize/settings-icon.svg).
1. Desmarque a opção **[!UICONTROL Herdar imagem em destaque da página]**.
1. Clique em **[!UICONTROL Escolher]** e selecione **[!UICONTROL Remoto]**.
   ![imagem](/help/assets/assets/uncheck-inherit-option.jpg)

   Você será solicitado a fazer logon.
1. Selecione o ativo e clique em **[!UICONTROL Selecionar]**.
1. Adicione um texto alternativo e clique em **[!UICONTROL Concluído]**.
   <br> O ativo remoto aparece no componente de imagem. Você também pode verificar o URL de entrega do ativo quando ele é carregado na página ou usando a guia &quot;Visualizar&quot;. A URL de entrega indica que o ativo está sendo acessado remotamente.

Você pode acessar ativos remotos no editor de páginas do AEM pronto para uso somente para o Componente principal de imagem v3 e Componente principal de teaser v2. Para outros componentes, incluindo componentes personalizados, são necessárias personalizações para integrar o Seletor de ativos a esses componentes.

#### Vídeo: acessar ativos remotos no Editor de páginas do AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Acessar ativos remotos no fragmento de conteúdo do AEM {#access-assets-content-fragment}

Siga as etapas abaixo para usar ativos remotos no Fragmento de conteúdo do AEM na instância do AEM Sites. Essa integração pode ser feita no AEM 6.5 e não no AEM as a Cloud Service.

1. Vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Selecione a pasta de ativos na qual o fragmento de conteúdo está presente.
1. Selecione o Fragmento do conteúdo e clique em **[!UICONTROL Editar (_e_)]**.

   >[!NOTE]
   >
   >Se você não tiver o modelo de Fragmento de conteúdo do AEM, talvez precise [criar um](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=pt-BR).

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

Você pode acessar ativos remotos ao criar conteúdo no Microsoft Word, Google Docs ou Universal Editor e, em seguida, publicar o conteúdo no Edge Delivery Services. Você também pode usar o Dynamic Media com OpenAPI para fornecer ativos aprovados pela marca e utilizar muitos outros benefícios que ele oferece. Para obter mais informações, consulte [Integrar o AEM Assets ao criar conteúdo para o Edge Delivery Services](/help/assets/integrate-aem-assets-edge-delivery-services.md).
