---
title: Como invalidar o cache CDN por meio do Dynamic Media Classic
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.
translation-type: tm+mt
source-git-commit: 20e37c385c2d3df91e37095bcf8a630fbfccbd16
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 25%

---


# Invalidar o cache CDN por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos Dynamic Media são armazenados em cache pela CDN (Content Delivery Network, Rede de conteúdo) para delivery rápido. No entanto, ao fazer atualizações em um ativo, você pode desejar que essas alterações entrem em vigor imediatamente. A invalidação do conteúdo em cache do CDN permite atualizar rapidamente ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.

>[!NOTE]
>
>Este recurso exige que você use o CDN pronto para uso fornecido com a Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é suportado com este recurso.

>[!IMPORTANT]
>
>Estas etapas aplicam-se somente à Dynamic Media no AEM 6.5, Service Pack 5 ou anterior. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

Consulte também [Visão geral do cache no Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o cache CDN por meio do Dynamic Media Classic:**

1. Abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.
1. Na página Configurações gerais do aplicativo, no cabeçalho do grupo Servidores, localize a caixa de texto **[!UICONTROL Modelo de invalidação CDN]**.

1. Especifique o modelo usado para invalidar o cache CDN (Rede de Delivery de Conteúdo).

   Por exemplo, suponha que você insira um URL de imagem (incluindo predefinições ou modificadores de imagem) referenciando `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo contiver apenas `<ID>`, a Dynamic Media preencherá `https://<server>/is/image`, onde `<server>` é o Nome do Servidor de Publicação definido em Configurações Gerais, e &lt;ID> serão os ativos selecionados para serem invalidados.

1. No canto inferior direito da página, clique em **[!UICONTROL Fechar]**.
1. Na interface do usuário do Dynamic Media Classic (Scene7), selecione um ou mais ativos e clique em **[!UICONTROL Arquivo > Invalidar CDN]**. Você verá uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Published Server Name&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de Invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você clica em **[!UICONTROL Arquivo > Invalidar CDN]**, o resultado é o seguinte URL gerado na interface do usuário de Invalidação CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa lista do URL, clique em **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. Observe que é possível editar um URL ou adicioná-lo digitando-o ou colando-o na caixa lista do URL; não é necessário definir CDN Invalidate Template antecipadamente.

   Após clicar em **[!UICONTROL Continuar]**, um indicador é exibido que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos e clicou em **[!UICONTROL Arquivo > Invalidar CDN]**, cada ativo é referenciado no **[!UICONTROL URL de modelo]** salvo. Portanto, você pode definir um **[!UICONTROL Modelo de invalidação CDN]** referenciando cada predefinição de imagem do URL referenciada em seu site (como detalhes do produto, resultados de pesquisa e assim por diante). Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e, em seguida, clicar em **[!UICONTROL Arquivo > Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com o objetivo de invalidar a partir da Rede de fornecimento de conteúdo (CDN). Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completos à lista **[!UICONTROL Invalidar CDN]**. Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a opção **[!UICONTROL Arquivo > Invalidar CDN]**.

