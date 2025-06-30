---
title: Exibir e gerenciar representações no Experience Manager Assets
description: Saiba como o AEM Assets e o Dynamic Media simplificam o gerenciamento eficiente de imagens com representações de imagem estáticas e dinâmicas.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Exibir e gerenciar representações no Experience Manager Assets{#renditions}

As representações no Adobe Experience Manager (AEM) são versões personalizadas de ativos digitais, como imagens, projetadas para diferentes dispositivos e plataformas para garantir o desempenho ideal. O AEM facilita a criação e o gerenciamento dessas representações, melhorando a experiência do usuário. Você pode criar miniaturas, otimizar imagens para Web ou dispositivos móveis, adicionar marcas d&#39;água, exibir e baixar representações dinâmicas ou representações de Recorte inteligente e fazer muito mais.

As predefinições de imagem do Dynamic Media e as representações de Recorte inteligente promovem um gerenciamento sistemático de imagens que se alinha aos padrões da marca, maximizando a coesão da marca. Isso simplifica o processo de localizar e usar representações de imagem dinâmicas rapidamente, conforme necessário, sem acesso de administrador.

As representações são classificadas como estáticas e dinâmicas, cada tipo apresentando recursos e funcionalidades exclusivos que são discutidos mais detalhadamente.

## Representações estáticas {#static-renditions}

As representações estáticas são versões pré-geradas de ativos digitais, geralmente criadas durante a assimilação ou modificação de ativos. Essas representações são otimizadas para fins e plataformas específicos, como miniaturas da Web, formatos amigáveis para dispositivos móveis para design responsivo ou versões de alta resolução para impressão, garantindo uma experiência eficiente e consistente.
Saiba como [exibir e baixar representações estáticas](#view-and-download-static-renditions) no Experience Manager Assets.

### Exibir e baixar representações estáticas{#view-and-download-static-renditions}

Para ver as representações de ativos e baixá-las, siga estas etapas:

1. No Modo de Exibição do Assets, clique em **Assets**, navegue até uma pasta, selecione um ativo e clique em **Detalhes**.
1. Clique no ícone da representação disponível no painel direito.
1. Selecione uma representação para visualizá-la e clique em ![ícone de download](/help/assets/assets/download-icon.svg) para baixá-la.

   ![Exibir e baixar representações dinâmicas](/help/assets/assets/view-download-static-rendition.png)

## Representações dinâmicas {#dynamic-renditions}

As representações dinâmicas são versões personalizadas de ativos criadas em tempo real para atender a necessidades específicas, como redimensionar imagens com base na resolução do dispositivo ou recortar para se ajustar a diferentes taxas de aspecto.
Essas representações permitem que as organizações entreguem experiências personalizadas e otimizadas para diversas necessidades do público-alvo. É possível visualizar e baixar representações dinâmicas no Experience Manager Assets.

## Representações do Dynamic Media {#dynamic-media-renditions}

### Antes de começar

* Você deve ser um usuário licenciado do AEM Dynamic Media.
* Use a [!UICONTROL Exibição de administração] para configurar:
   * [Perfis de imagem de corte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md)

  Você pode [alternar o modo de exibição](/help/assets/assets-view-introduction.md#how-to-access-assets-view) posteriormente para visualizar representações dinâmicas no modo de exibição do Assets.
* Publique ativos no Dynamic Media para disponibilizar representações do Dynamic Media na visualização do Assets. Para obter mais informações, consulte [Publicar Assets no AEM e Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm).


### Exibir e baixar representações do Dynamic Media {#view-download-dm-renditions}

Para exibir ou baixar representações dinâmicas de imagens no Experience Manager Assets, siga estas etapas:

1. Vá para **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navegue até a pasta de ativos aplicável.

1. Clique no ativo que você precisa exibir e em **[!UICONTROL Detalhes]**.

1. No menu direito, clique no ícone **[!UICONTROL Dynamic Media]**. O painel **[!UICONTROL Dynamic Media]** exibe as representações do Dynamic Media e do Smart Crop.

   ![representações dinâmicas](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Selecione a representação a ser visualizada e clique em **Copiar URL** para copiar a URL da representação selecionada. Clique em **Baixar representação** para baixar as representações dos ativos de imagem.
1. Selecione a representação de Recorte inteligente a ser visualizada e clique em **Copiar URL** para copiar a URL da representação selecionada.
1. Clique em ![ícone de download](assets/do-not-localize/download-icon.png) para baixar todas as representações do Corte Inteligente disponíveis como um único arquivo zip.
   ![ícone de download](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >Essas representações estão disponíveis somente para ativos de imagem.

## Representações do Dynamic Media com recursos OpenAPI {#dm-with-openapi-renditions}

### Antes de começar {#prereqs-dm-with-openapi-renditions}

* Você deve ser um usuário licenciado do AEM Dynamic Media.
* O Assets deve ser aprovado para exibir representações do Dynamic Media com recursos OpenAPI. Para obter mais informações, consulte [Aprovar ativos no Experience Manager](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* O Dynamic Media com recursos OpenAPI deve estar ativado na instância do AEM as a Cloud Service.

### Exibir representações do Dynamic Media com recursos OpenAPI {#view-download-dm-with-openapi-renditions}

1. Selecione o ativo e clique em **Detalhes**.
1. Clique no ícone Dynamic Media disponível no painel direito. O painel Dynamic Media exibe a representação Dynamic Media com recursos OpenAPI para todos os tipos de ativos.
   ![ícone de download](/help/assets/assets/dm-with-open-api-copy-url.png)
1. Selecione a opção **Dynamic Media com OpenAPI** e clique em **Copiar URL** para copiar a URL de entrega do ativo.


