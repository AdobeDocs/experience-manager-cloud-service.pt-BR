---
title: Exibir e gerenciar representações no Experience Manager Assets
description: Saiba como o AEM Assets e o Dynamic Media simplificam o gerenciamento eficiente de imagens com representações de imagem estáticas e dinâmicas.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Exibir e gerenciar representações no Experience Manager Assets{#renditions}

As representações no Adobe Experience Manager (AEM) são versões personalizadas de ativos digitais, como imagens, projetadas para diferentes dispositivos e plataformas para garantir o desempenho ideal. O AEM facilita a criação e o gerenciamento dessas representações, melhorando a experiência do usuário. Você pode criar miniaturas, otimizar imagens para Web ou dispositivos móveis, adicionar marcas d&#39;água, exibir e baixar representações dinâmicas ou representações de recorte inteligente e fazer muito mais.

As predefinições de imagem do Dynamic Media e as representações de Recorte inteligente promovem o gerenciamento sistemático de imagens que se alinha aos padrões da marca, maximizando a coesão da marca. Isso simplifica o processo de localizar e usar representações de imagem dinâmicas rapidamente, conforme necessário, sem acesso de administrador.

As representações são classificadas como estáticas e dinâmicas, cada tipo apresentando recursos e funcionalidades exclusivos que são discutidos mais detalhadamente.

## Representações estáticas {#static-renditions}

As representações estáticas são versões pré-geradas de ativos digitais, geralmente criadas durante a assimilação ou modificação de ativos. Essas representações são otimizadas para fins e plataformas específicos, como miniaturas da Web, formatos amigáveis para dispositivos móveis para design responsivo ou versões de alta resolução para impressão, garantindo uma experiência eficiente e consistente.
Saiba mais [como visualizar e baixar](#view-dynamic-renditions) representações estáticas no [!DNL Experience Manager Assets].

## Representações dinâmicas {#dynamic-renditions}

As representações dinâmicas são versões personalizadas de ativos criadas em tempo real para atender a necessidades específicas, como redimensionar imagens com base na resolução do dispositivo ou recortar para se ajustar a diferentes taxas de aspecto.
Essas representações permitem que as organizações entreguem experiências personalizadas e otimizadas para diversas necessidades do público-alvo. É possível visualizar e baixar representações dinâmicas no [!DNL Experience Manager Assets].

### Antes de começar

* Você deve ser um usuário licenciado do AEM Dynamic Media.

* Uso [!UICONTROL Exibição do administrador] para configurar:
   * [Perfis de imagem de corte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md)

  Você pode [alternar a exibição](/help/assets/assets-view-introduction.md#how-to-access-assets-view) posteriormente para visualizar representações dinâmicas na visualização de Ativos.

### Exibir e baixar representações dinâmicas {#view-renditions}

Para exibir ou baixar representações dinâmicas de imagens no [!DNL Experience Manager Assets], siga estas etapas:

1. Ir para **[!UICONTROL Gerenciamento de ativos]** > **[!UICONTROL Assets]**.

1. Navegue até a pasta de ativos aplicável.

1. Clique na imagem que precisa visualizar e clique em **[!UICONTROL Detalhes]**.

1. No menu direito, clique em **[!UICONTROL Representações]**. <br> A variável **[!UICONTROL Representações]** O painel é aberto com as **[!UICONTROL Dinâmico]** e **[!UICONTROL Corte inteligente]** representações.

   ![representações dinâmicas](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Clique na representação que precisa exibir ou baixar.

1. Clique em ![ícone de download](assets/do-not-localize/download-icon.png) ícone ao lado da representação dinâmica que você precisa baixar. <br> Como alternativa, selecione a representação da imagem e clique em **[!UICONTROL Baixar representação]** na parte inferior.

   Você pode clicar no link ![ícone de download](assets/do-not-localize/download-icon.png) ícone disponível na parte superior de **[!UICONTROL Corte inteligente]** representações para baixar todas as representações de Corte inteligente disponíveis para esse ativo.

>[!NOTE]
>
>As representações dinâmicas só estarão visíveis se os ativos forem carregados da exibição de Administrador.
