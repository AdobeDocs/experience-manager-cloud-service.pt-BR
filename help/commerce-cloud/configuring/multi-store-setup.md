---
title: Configuração de várias lojas do Commerce
description: Saiba como mapear várias exibições de loja do Adobe Commerce para o Adobe Experience Manager. Isso permite que os projetos sejam compatíveis com casos de uso de vários locatários e vários idiomas.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 18%

---

# Configuração de várias lojas do Commerce {#multi-store}

Os Componentes principais do CIF do Adobe Experience Manager (AEM) podem ser usados em várias estruturas de site do AEM e a implementação de cliente GraphQL subjacente pode se conectar a diferentes lojas/visualizações de loja do Adobe Commerce. Assim, os projetos podem implementar configurações complexas de várias lojas/vários sites.

Uma apresentação em vídeo detalhando as opções para integrar várias visualizações da Adobe Commerce Store ao Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Os recursos de gerenciamento de vários sites do AEM para Live Copy e Language Copy são usados com a Commerce Integration Framework para gerenciar sites em várias regiões e localidades.

A configuração recomendada é usar uma relação 1:1 entre o site do AEM e a exibição da loja da Adobe Commerce.

Para conectar um site de AEM AEM e os Componentes principais do CIF a uma exibição de loja dedicada, faça o seguinte:

## Configuração {#configuration}

1. Configure várias lojas e visualizações de loja de acordo com o padrão descrito em [Sites, lojas e visualizações do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. Verifique se a conexão entre AEM e Adobe Commerce está funcionando.

3. Crie uma configuração secundária da configuração do CIF Cloud Service seguindo estas etapas:

   * No AEM, acesse Ferramentas -> Geral -> [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Selecione a configuração básica que você criou
   * Crie uma configuração usando as etapas descritas no ponto 2 acima

   Essa nova configuração é criada como uma configuração secundária da base. Agora você pode acessar Ferramentas -> Geral -> Navegador de configuração e criar as configurações.

   >[!TIP]
   >
   > Os catálogos de comércio podem ser endereçados usando IDs ou UIDs. Os UIDs foram introduzidos no Adobe Commerce 2.4.2. Habilite isso somente se o back-end de comércio suportar um esquema do GraphQL versão 2.4.2 ou posterior.

4. Atribua a configuração secundária a um site do AEM

   * Acesse o console do AEM Sites
   * Navegue até a raiz de região ou idioma da estrutura do site. Por exemplo, `/content/venia/us _or_ /content/venia/us/en` para a página de exemplo Venia
   * Selecione a página e abra as propriedades dela
   * Selecione a guia Avançado
   * No `Configuration` selecione a configuração que você criou na etapa 3

## Recursos adicionais

* [Sites, lojas e visualizações do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [Componentes principais da CIF do AEM — Configuração de várias lojas/sites](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Usar o gerenciamento de vários sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-cloud/administering/msm/overview.md)
