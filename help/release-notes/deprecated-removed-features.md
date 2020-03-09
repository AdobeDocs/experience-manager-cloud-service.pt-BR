---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para os recursos obsoletos e removidos do Adobe Experience Manager as a Cloud Service.
translation-type: ht
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores. Além disso, como o Adobe Experience Manager as a Cloud Service fornece um modelo de implantação nativo em nuvem. Determinados recursos e funcionalidades foram substituídos por seus equivalentes nativos em nuvem.

As seguintes regras se aplicam para comunicar a remoção/substituição iminente das funcionalidades do AEM:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Os recursos obsoletos continuam disponíveis, mas não são aprimorados.
1. Os recursos anunciados como obsoletos são removidos na versão principal subsequente, com a maior brevidade. A data de destino real para remoção é anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoletos no Experience Manager as a Cloud Service. Normalmente, os recursos planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação no momento, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Área | Recurso | Substituição |
| ------------ | ------------------ | ----------- |
| Ativos | A assimilação e o processamento de ativos não usam mais o fluxo de trabalho `DAM Asset Update` | A assimilação de ativos usa [microsserviços de ativos](/help/assets/asset-microservices-overview.md) agora. |
| Ativos | Upload de ativos diretamente no AEM - consulte [APIs de upload de ativos obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | O [upload binário direto](/help/assets/add-assets.md) é usado no Experience Manager as a Cloud Service. Para obter detalhes técnicos, consulte [APIs de upload direto](/help/assets/developer-reference-material-apis.md#overview-binary-upload). |
| Ativos | [Determinadas etapas do fluxo de trabalho](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` não são compatíveis, incluindo a chamada de ferramentas de linha de comando, como o ImageMagick | Os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) oferecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades que foram removidos do AEM com o Experience Manager as a Cloud Service.

| Área | Recurso | Substituição |
| ------------ | ------------------ | ----------- |
| Interface | Embora algumas caixas de diálogo da interface do usuário clássica permaneçam por enquanto para alguns recursos selecionados, como o Link Checker, Version Purge e algumas configurações do Cloud Service, o acesso à interface do usuário clássica em geral foi removido na interface do usuário do produto AEM. | Interface do usuário padrão |
| Mídia dinâmica | As integrações anteriores com os modos [Mídia dinâmica clássica (Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) e [Mídia dinâmica híbrida](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) não estão disponíveis no AEM as a Cloud Service. | Use a [Mídia dinâmica](/help/assets/dynamic-media/dynamic-media.md) fornecida com o Experience Manager as a Cloud Service. |
| Sites | Portal Director e Portlet Component | Estes recursos foram descontinuados no AEM 6.4 e foram removidos do AEM. |
| Sites | Importador de design | Este recurso foi removido, pois seções inalteradas do repositório do AEM não estão acessíveis no tempo de execução. |
| Ativos | [O compartilhamento do AEM Assets com os serviços Marketing Cloud Assets Core Service e Creative Cloud](https://docs.adobe.com/content/help/br/experience-manager-65/administering/integration/configure-assets-cc-integration.html) não está disponível. | Para integração com a Creative Cloud, use o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html). |
