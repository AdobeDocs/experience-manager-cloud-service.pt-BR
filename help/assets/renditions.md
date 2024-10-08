---
title: Exibir e gerenciar representações no Experience Manager Assets
description: Saiba como o AEM Assets e o Dynamic Media simplificam o gerenciamento eficiente de imagens com representações de imagem estáticas e dinâmicas.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Exibir e gerenciar representações no Experience Manager Assets{#renditions}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

As representações no Adobe Experience Manager (AEM) são versões personalizadas de ativos digitais, como imagens, projetadas para diferentes dispositivos e plataformas para garantir o desempenho ideal. O AEM facilita a criação e o gerenciamento dessas representações, melhorando a experiência do usuário. Você pode criar miniaturas, otimizar imagens para Web ou dispositivos móveis, adicionar marcas d&#39;água, exibir e baixar representações dinâmicas ou representações de recorte inteligente e fazer muito mais.

As predefinições de imagem do Dynamic Media e as representações de Recorte inteligente promovem o gerenciamento sistemático de imagens que se alinha aos padrões da marca, maximizando a coesão da marca. Isso simplifica o processo de localizar e usar representações de imagem dinâmicas rapidamente, conforme necessário, sem acesso de administrador.

As representações são classificadas como estáticas e dinâmicas, cada tipo apresentando recursos e funcionalidades exclusivos que são discutidos mais detalhadamente.

## Representações estáticas {#static-renditions}

As representações estáticas são versões pré-geradas de ativos digitais, geralmente criadas durante a assimilação ou modificação de ativos. Essas representações são otimizadas para fins e plataformas específicos, como miniaturas da Web, formatos amigáveis para dispositivos móveis para design responsivo ou versões de alta resolução para impressão, garantindo uma experiência eficiente e consistente.
Saiba [como exibir e baixar](#view-dynamic-renditions) representações estáticas em [!DNL Experience Manager Assets].

## Representações dinâmicas {#dynamic-renditions}

As representações dinâmicas são versões personalizadas de ativos criadas em tempo real para atender a necessidades específicas, como redimensionar imagens com base na resolução do dispositivo ou recortar para se ajustar a diferentes taxas de aspecto.
Essas representações permitem que as organizações entreguem experiências personalizadas e otimizadas para diversas necessidades do público-alvo. Você pode exibir e baixar representações dinâmicas em [!DNL Experience Manager Assets].

### Antes de começar

* Você deve ser um usuário licenciado do AEM Dynamic Media.

* Use o [!UICONTROL modo de exibição de Administração] para configurar:
   * [Perfis de imagem de corte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md)

  Você pode [alternar o modo de exibição](/help/assets/assets-view-introduction.md#how-to-access-assets-view) posteriormente para visualizar representações dinâmicas no modo de exibição do Assets.

### Exibir e baixar representações dinâmicas {#view-renditions}

Para exibir ou baixar representações dinâmicas de imagens no [!DNL Experience Manager Assets], siga estas etapas:

1. Vá para **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navegue até a pasta de ativos aplicável.

1. Clique na imagem que você precisa exibir e em **[!UICONTROL Detalhes]**.

1. No menu direito, clique em **[!UICONTROL Representações]**. <br> O painel **[!UICONTROL Representações]** é aberto com as representações **[!UICONTROL Dinâmicas]** e **[!UICONTROL Recorte inteligente]** disponíveis.

   ![representações dinâmicas](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Clique na representação que precisa exibir ou baixar.

1. Clique no ícone de ![download](assets/do-not-localize/download-icon.png) ao lado da representação dinâmica que você precisa baixar. <br> Como alternativa, você pode selecionar a representação da imagem e clicar na opção **[!UICONTROL Baixar representação]** na parte inferior.

   Você pode clicar no ícone de ![download](assets/do-not-localize/download-icon.png) disponível na parte superior da seção de representações do **[!UICONTROL Recorte inteligente]** para baixar todas as representações de Recorte inteligente disponíveis para esse ativo.

>[!NOTE]
>
>As representações dinâmicas só estarão visíveis se os ativos forem carregados da exibição de Administrador.
