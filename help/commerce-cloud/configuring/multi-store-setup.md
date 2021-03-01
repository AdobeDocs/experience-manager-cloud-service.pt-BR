---
title: Configuração de várias lojas
description: Saiba como mapear várias visualizações de loja da Magento para o AEM. Isso permite que os projetos suportem casos de uso de vários locatários e várias línguas.
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Estrutura de integração de comércio
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: 95ac5e5f6c49d5a2d7aef5dcf30d8298fd459457
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 91%

---


# Configuração de várias lojas {#multi-store}

Os Componentes principais da CIF do AEM podem ser usados em várias estruturas de site do AEM e a implementação de cliente GraphQL subjacente pode se conectar a diferentes lojas/visualizações de loja da Magento. Assim, os projetos podem implementar configurações complexas de várias lojas/vários sites.

Veja abaixo um vídeo que detalha passo a passo as opções para integrar várias visualizações da loja da Magento ao Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Os recursos de gerenciamento de vários sites do AEM para Live Copy e Language Copy são usados junto com a Commerce Integration Framework para gerenciar sites em várias regiões e locales.

A configuração recomendada é usar uma relação 1:1 entre um site do AEM e uma visualização de loja da Magento.

Para conectar um site do AEM e os Componentes principais da CIF do AEM a uma visualização de loja dedicada, siga as etapas abaixo:

## Configuração {#configuration}

1. Configure várias lojas e visualizações de loja de acordo com o padrão descrito em [Sites, lojas e visualizações da Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Verifique se a conexão entre o AEM e a Magento está funcionando.

3. Crie uma configuração secundária da configuração do CIF Cloud Service seguindo estas etapas:

   * No AEM, acesse Ferramentas -> Geral -> [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Selecione a configuração básica que você criou
   * Criar uma nova configuração usando as etapas descritas no ponto 2 acima

   Essa nova configuração será criada como uma configuração secundária da base. Agora você pode acessar Ferramentas -> Geral -> Navegador de configuração e criar as configurações.

4. Atribua a configuração secundária a um site do AEM

   * Acesse o console do AEM Sites
   * Acesse a raiz de região ou idioma da estrutura do site, por exemplo, /content/venia/us _ou_ /content/venia/us/en para a página de exemplo Venia.
   * Selecione a página e abra as propriedades da página
   * Selecione a guia Avançado
   * Na seção `Configuration` selecione a configuração que você criou na etapa 3

## Recursos adicionais

* [Sites, lojas e visualizações da Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principais da CIF do AEM — Configuração de várias lojas/sites](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Usar o gerenciamento de vários sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-cloud/administering/msm/overview.md)
