---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para recursos obsoletos e removidos no Adobe Experience Manager como um serviço em nuvem.
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Deprecated and removed features {#deprecated-and-removed-features}

A Adobe avalia constantemente os recursos do produto, para reinventar ou substituir os recursos mais antigos por alternativas mais modernas para melhorar o valor geral do cliente, sempre considerando cuidadosamente a compatibilidade com versões anteriores. Além disso, como o Adobe Experience Manager como um serviço em nuvem fornece um modelo de implantação nativo da nuvem, determinados recursos e recursos foram substituídos por parceiros nativos da nuvem.

As seguintes regras se aplicam para comunicar a remoção/substituição iminente das funcionalidades do AEM:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Os recursos obsoletos continuam disponíveis, mas não são aprimorados ainda mais.
1. Os recursos anunciados como obsoletos são removidos na versão principal subsequente, o mais tardar. A data de destino real para remoção é anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Deprecated features {#deprecated-features}

Esta seção lista os recursos e recursos que foram marcados como obsoletos no Experience Manager como um serviço em nuvem. Normalmente, os recursos que estão planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação no momento, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Área | Recurso | Substituição |
| ------------ | ------------------ | ----------- |
| Assets | A inclusão e o processamento de ativos não usam mais o fluxo de trabalho `DAM Asset Update` | A ingestão de ativos usa microserviços [de](/help/assets/asset-microservices-overview.md) ativos agora. |
| Assets | Fazer upload de ativos diretamente para o AEM - consulte APIs de upload de ativos [obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [O upload](/help/assets/add-assets.md) binário direto é usado no Experience Manager como um serviço em nuvem. Para obter detalhes técnicos, consulte APIs [de upload](/help/assets/developer-reference-material-apis.md#overview-binary-upload)direto. |
| Assets | [Determinadas etapas](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` do fluxo de trabalho no fluxo de trabalho não são suportadas, incluindo a chamada de ferramentas de linha de comando como ImageMagick | [Os microserviços](/help/assets/asset-microservices-overview.md) de ativos fornecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use fluxos de trabalho [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)pós-processamento. |

## Removed features {#removed-features}

Esta seção lista os recursos e recursos que foram removidos do AEM com o Experience Manager como um serviço em nuvem.

| Área | Recurso | Substituição |
| ------------ | ------------------ | ----------- |
| Interface | Embora algumas caixas de diálogo da interface clássica permaneçam por enquanto para alguns recursos selecionados, como o Verificador de links, a Expurgação da versão e algumas configurações do Serviço em nuvem, o acesso à interface clássica em geral foi removido na interface do usuário do produto AEM. | Interface padrão |
| Dynamic Media | As integrações anteriores com o [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) e o modo [Híbrido de mídia](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) dinâmica não estão disponíveis no AEM como um serviço em nuvem. | Use o [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornecido com o Experience Manager como um serviço em nuvem. |
| Sites | Portal Diretor e Componente de Portlet | Esses recursos foram descontinuados no AEM 6.4 e foram removidos do AEM. |
| Sites | Importador de design | Esse recurso foi removido, pois seções imutáveis do repositório do AEM não estão acessíveis em tempo de execução. |
| Assets | [O compartilhamento de ativos AEM com os principais serviços](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) da Marketing Cloud Assets e da Creative Cloud não está disponível. | Para integração com a Creative Cloud, use o [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). |
