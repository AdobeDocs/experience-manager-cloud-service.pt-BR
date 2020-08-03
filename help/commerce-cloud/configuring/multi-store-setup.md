---
title: Configuração de várias lojas
description: Configuração de várias lojas
translation-type: tm+mt
source-git-commit: 94c6abef36b6add300ba3b24855ebf3edf10e1ed
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Configuração de várias lojas {#multi-store}

Os componentes principais CIF AEM podem ser usados em várias estruturas AEM do site e a implementação subjacente do cliente GraphQL pode se conectar a diferentes Magento stores / visualizações de loja. Isso permite que os projetos implementem configurações complexas de várias lojas/vários sites.

Uma apresentação de vídeo detalhando opções para integrar várias Visualizações da Magento Store ao Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM recursos de Gerenciamento de vários sites do Live Copy e do Language Copy são usados em conjunto com a Commerce Integration Framework para gerenciar globalmente sites em regiões e localidades.

A configuração recomendada é usar uma relação 1:1 entre AEM site e visualização store.

Para conectar um site AEM e AEM componentes principais CIF, de modo que também a uma visualização de loja dedicada, siga as etapas abaixo:

## Configuração {#configuration}

1. Configure várias lojas e visualizações de loja de acordo com o padrão descrito em Sites do [Magento, Lojas e Visualizações](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Verifique se a conexão entre AEM e Magento está funcionando.

3. Crie uma configuração filho da configuração CIF Cloud Service, seguindo estas etapas:

   * AEM vá para Ferramentas -> Geral -> Navegador de configuração
   * Selecione a configuração básica criada
   * Criar uma nova configuração utilizando as etapas descritas no ponto 2 acima

   Esta nova configuração será criada como uma configuração secundária da base. Agora você pode acessar Ferramentas -> Geral -> Navegador de configuração e criar as configurações.

4. Atribuir a configuração secundária a um site AEM

   * Ir para o console AEM Sites
   * Navegue até a região ou raiz de idioma da estrutura do site, por exemplo, /content/venia/us __ ou /content/venia/us/en para a página de amostra de Venia
   * Selecionar a página e abrir as propriedades da página
   * Selecione a guia Avançado
   * Na `Configuration` seção selecione a configuração que você criou na etapa

## Recursos adicionais

* [Sites Magento, Lojas e Visualizações](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principais CIF AEM - Configuração de várias lojas/locais](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Uso do Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilizando conteúdo: Multi Site Manager e Live Copy](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
