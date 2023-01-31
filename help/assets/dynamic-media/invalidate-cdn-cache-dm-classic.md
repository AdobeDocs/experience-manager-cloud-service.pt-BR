---
title: Invalidar o cache CDN (Content Delivery Network) por meio do Dynamic Media Classic
description: Saiba como invalidar o conteúdo em cache do CDN (Content Delivery Network) para permitir que você atualize rapidamente os ativos entregues pela Dynamic Media, em vez de esperar que o cache expire.
contentOwner: Rick Brough
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 15%

---

# Invalidar o cache da CDN por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida. No entanto, quando você faz atualizações em um ativo, deseja que essas alterações entrem em vigor imediatamente. A invalidação do conteúdo em cache do CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar que o cache expire.

>[!NOTE]
>
>Esse recurso exige que você use a CDN predefinida fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.

>[!IMPORTANT]
>
>Essas etapas se aplicam somente ao Dynamic Media no Adobe Experience Manager 6.5, Service Pack 5 ou anterior. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar o cache CDN por meio do Dynamic Media Classic:**

1. Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente.

1. Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**.
1. Na página Configurações gerais do aplicativo , abaixo do cabeçalho do grupo Servidores , localize o **[!UICONTROL Modelo de Invalidação CDN]** caixa de texto.

1. Especifique o modelo que é usado para invalidar o cache CDN (Content Delivery Network).

   Por exemplo, suponha que você insira um URL de imagem (incluindo predefinições ou modificadores de imagem) que faça referência a `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o modelo contiver apenas `<ID>`, em seguida, o Dynamic Media preenche `https://<server>/is/image` em que `<server>` é o Nome do servidor de publicação definido nas Configurações gerais e &lt;id> é o ativo selecionado para invalidação.

1. No canto inferior direito da página, selecione **[!UICONTROL Fechar]**.
1. Na interface do usuário do Dynamic Media Classic (Scene7), selecione um ou mais ativos e, em seguida, acesse **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**. Você vê uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Nome do servidor publicado&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de Invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você vai para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, resulta no seguinte URL gerado na interface do usuário de Invalidação de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa de listagem do URL, selecione **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. Você pode editar um URL ou adicionar um URL digitando-o ou colando-o na caixa de listagem do URL; não é necessário definir o Modelo de Invalidação CDN antecipadamente.

   Após selecionar **[!UICONTROL Continuar]**, é exibido um indicador que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos, então foi para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, cada ativo é referenciado na variável **[!UICONTROL URL do modelo]**. Portanto, você pode definir uma **[!UICONTROL Modelo de invalidação CDN]** referenciando cada predefinição de imagem do URL referenciada em seu site, como detalhes do produto e resultados da pesquisa. Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e, em seguida, acessar **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente para invalidar a partir do CDN. Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completos à variável **[!UICONTROL Invalidar CDN]** lista. Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]** opção.
