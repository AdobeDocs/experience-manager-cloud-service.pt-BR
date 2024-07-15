---
title: Como criar uma marca d'água em seus ativos no AEM?
description: Saiba como adicionar uma marca d'água digital a seus ativos no AEM. As marcas d'água podem ajudar os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos.
contentOwner: AG
feature: Asset Management,Publishing
role: User, Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 14%

---

# Marca d&#39;água em seus ativos {#watermark-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service | Este artigo |

O [!DNL Adobe Experience Manager Assets] permite que você adicione uma marca d&#39;água digital a imagens e vídeos. [!DNL Assets] dá suporte à aplicação de uma imagem como marca d&#39;água a outros arquivos de imagem. As marcas d&#39;água podem ajudar os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. Além disso, uma marca d&#39;água pode ser usada para indicar o estado de um documento como confidencial, rascunho, validade e assim por diante.

Para configurar o [!DNL Experience Manager] para ativos de marca d&#39;água:

1. Um arquivo PNG é aplicado como marca d&#39;água. Faça upload desse arquivo para o repositório DAM.

1. Navegue até **[!UICONTROL Ferramentas > Assets > Configurações do Assets]**.

1. Clique em **[!UICONTROL Perfil de marca d&#39;água do sistema]**.

1. Na [!UICONTROL página Perfil de marca d&#39;água do sistema], especifique o caminho da imagem carregada no repositório DAM na etapa 1.

1. Especifique a escala da marca d&#39;água, variando de 0,0 a 1,0, relativa à largura da representação, no campo **[!UICONTROL Escala]**.

1. Clique em **[!UICONTROL Salvar]**.

   ![Detector de duplicação de ativos](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Se você tiver configurado o Perfil de Marcas D&#39;Água do Sistema usando o arquivo de configuração `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` (configuração OSGi), poderá continuar a usá-lo. No entanto, a Adobe recomenda o uso do novo método.


1. [Crie um perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) para usar microsserviços de ativos para aplicar a marca d&#39;água.

   ![Perfil de processamento de ativo para criar marca d&#39;água](assets/watermark-processing-profile.png)

   Certifique-se de habilitar a opção de alternância **[!UICONTROL Marca d&#39;água]** ao criar o perfil de processamento.

1. [Aplique os perfis de processamento a uma pasta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para criar ativos com marca d&#39;água.

## Dicas e limitações {#tips-limitations-bestpractices}

* Você pode usar uma única configuração para criar uma marca d&#39;água em todos os seus ativos. Somente uma imagem é usada para marca d&#39;água e sua largura é fixa.
* Você pode colocar a marca d&#39;água no centro sem colocar ladrilhos.
* Não há suporte para marcas d&#39;água baseadas em texto.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publish Assets para AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Visão geral dos microsserviços de ativos](/help/assets/asset-microservices-overview.md).
>* [Usar microsserviços de ativos com perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).
