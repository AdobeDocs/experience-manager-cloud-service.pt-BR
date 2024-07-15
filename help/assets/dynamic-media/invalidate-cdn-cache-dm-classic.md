---
title: Invalidar o cache CDN (Content Delivery Network) por meio do Dynamic Media Classic
description: Saiba como invalidar o conteúdo em cache do CDN (Content Delivery Network) para permitir que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar a expiração do cache.
contentOwner: Rick Brough
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 15%

---

# Invalidar o cache da CDN por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida. No entanto, quando você atualiza um ativo, deseja que essas alterações entrem em vigor imediatamente. Invalidar o conteúdo em cache do CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar a expiração do cache.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

>[!IMPORTANT]
>
>Essas etapas se aplicam somente ao Dynamic Media no Adobe Experience Manager 6.5, Service Pack 5 ou anterior. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar o cache da CDN por meio do Dynamic Media Classic:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente.

1. Vá para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]**.
1. Na página Configurações Gerais do Aplicativo, no cabeçalho do grupo Servidores, localize a caixa de texto **[!UICONTROL Modelo de Invalidação de CDN]**.

1. Especifique o modelo usado para invalidar o cache CDN (Content Delivery Network).

   Por exemplo, suponha que você insira uma URL de imagem (incluindo predefinições de imagem ou modificadores) referenciando `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo contiver apenas `<ID>`, o Dynamic Media preencherá `https://<server>/is/image`, onde `<server>` é o Nome do Servidor do Publish definido em Configurações Gerais e &lt;ID> são os ativos selecionados para serem invalidados.

1. No canto inferior direito da página, selecione **[!UICONTROL Fechar]**.
1. Na interface do Dynamic Media Classic (Scene7), selecione um ou mais ativos e vá para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**. Você verá uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Nome do servidor publicado&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você vai para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, isso resulta na seguinte URL gerada na interface de usuário de Invalidação da CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa de listagem URL, selecione **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. Você pode editar um URL ou adicionar um URL digitando ou colando-o na caixa de lista de URL; não é necessário definir o Modelo de invalidação CDN antecipadamente.

   Após selecionar **[!UICONTROL Continuar]**, será exibido um indicador que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos e foi para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, cada ativo é referenciado na **[!UICONTROL URL de modelo]** salva. Portanto, você pode definir um **[!UICONTROL Modelo de invalidação CDN]** referenciando cada predefinição de imagem da URL referenciada em seu site, como detalhes do produto e resultados de pesquisa. Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e ir para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com base na CDN. Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completas à lista **[!UICONTROL Invalidar CDN]**. Se você seguir esta abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a opção **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**.
