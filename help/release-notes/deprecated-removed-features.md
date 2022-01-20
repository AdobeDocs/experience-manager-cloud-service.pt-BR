---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para recursos obsoletos e removidos do [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: bbd8277fc5ed81bc656900ec3a993630aa5ffad5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 34%

---

# Recursos obsoletos e removidos {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Recursos obsoletos e removidos em AEM as a Cloud Service"
>abstract="AEM as a Cloud Service tem um modelo de implantação nativo em nuvem. Determinados recursos foram substituídos por equivalentes nativos em nuvem e esta guia mostra esses recursos."


A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores. Também, como [!DNL Adobe Experience Manager] como [!DNL Cloud Service] O fornece um modelo de implantação nativo em nuvem, alguns recursos e funcionalidades foram substituídos por equivalentes nativos em nuvem.

Para comunicar a remoção/substituição iminente de [!DNL Experience Manager] , as seguintes regras se aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Os recursos obsoletos permanecem disponíveis, mas não são aprimorados.
1. Os recursos anunciados como obsoletos são removidos na versão principal subsequente, com a maior brevidade. A data de destino real para remoção é anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades marcados como obsoletos no [!DNL Experience Manager] como [!DNL Cloud Service]. Normalmente, os recursos a serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma alternativa fornecida.

Os clientes são aconselhados a verificar se usam o recurso/funcionalidade em sua implantação atual e a fazer planos para alterar sua implementação para usar a alternativa fornecida.

| Recursos | Recurso obsoleto | Substituição |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Propriedades de fragmentos de experiência para **Status da rede social**. | O recurso será removido em breve. |
| [!DNL Sites] | Fragmentos de conteúdo simples baseados em modelo. | [Fragmentos de conteúdo estruturado com base em modelo](/help/assets/content-fragments/content-fragments-models.md) agora. |
| [!DNL Assets] | fluxo de trabalho `DAM Asset Update` para processar imagens ingeridas. | A assimilação de ativos usa [microsserviços de ativos](/help/assets/asset-microservices-overview.md) agora. |
| [!DNL Assets] | Fazer upload de ativos diretamente em [!DNL Experience Manager]. Consulte [APIs de upload de ativos obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Use [Upload binário direto](/help/assets/add-assets.md). Para obter detalhes técnicos, consulte [APIs de upload direto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Determinadas etapas do fluxo de trabalho](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` não são compatíveis, incluindo a chamada de ferramentas de linha de comando, como o [!DNL ImageMagick]. | Os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) oferecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodificação FFmpeg de vídeos. | Para gerar miniaturas do FFmpeg, use os [Microserviços de ativos](/help/assets/asset-microservices-overview.md). Para a transcodificação FFmpeg, use o [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interface do usuário de replicação em árvore na guia &quot;Distribuir&quot; do agente de replicação (remoção após 30 de setembro de 2021) | [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [fluxo de trabalho da árvore de conteúdo de publicação](/help/operations/replication.md#publish-content-tree-workflow) abordagens |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades removidos do [!DNL Experience Manager] com [!DNL Experience Manager] como [!DNL Cloud Service].

| Área | Recurso | Substituição |
| ------------ | ------------------ | ----------- |
| Interface do usuário | A interface clássica é removida da interface do usuário do produto. Algumas caixas de diálogo da interface clássica estão disponíveis para alguns recursos selecionados, como o Verificador de links, a Limpeza de versão e algumas configurações do Cloud Service. Em breve [atualizações do produto](/help/release-notes/home.md) pode remover ainda mais a disponibilidade da interface clássica. | Interface do usuário padrão |
| [!DNL Dynamic Media] | Integrações anteriores com [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) e [Modo híbrido do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) não estão disponíveis em [!DNL Experience Manager] como [!DNL Cloud Service]. | Use [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) com [!DNL Experience Manager] como [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director e Portlet Component | Esses recursos foram descontinuados em [!DNL Experience Manager] 6.4 e agora foram retiradas de [!DNL Experience Manager]. |
| [!DNL Sites] | Importador de design | Esse recurso foi removido como seções imutáveis do [!DNL Experience Manager] O repositório não está acessível no tempo de execução. |
| [!DNL Assets] | [!DNL Assets]O compartilhamento do com os serviços Marketing Cloud Assets Core Service e Creative Cloud não está disponível. | Para integração com [!DNL Adobe Creative Cloud], use [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html). |
| [!DNL Foundation] | Suporte para fontes de dados do Apache Sling (pacote OSGi org.apache.sling.datasource) | N/A |
| [!DNL Foundation] | Suporte para modelos de script JST (pacote OSGi org.apache.sling.scripting.jst) | N/D |
| [!DNL Foundation] | Suporte para o quadro branco Apache Felix Http | Quadro de permissões HTTP OSGi |

## API Java {#java-api}

Consulte [esta página](/help/release-notes/deprecated-apis.md) para quaisquer APIs Java obsoletas ou removidas, que sejam ocasionalmente introduzidas.

## Configuração OSGI {#osgi-configuration}

Consulte [este artigo](/help/implementing/deploying/osgi-configuration-api.md) para quaisquer restrições sobre a configuração de propriedades OSGI, algumas das quais podem ser introduzidas ao longo do tempo.
