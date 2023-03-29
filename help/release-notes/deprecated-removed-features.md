---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para recursos obsoletos e removidos do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 459e6cbf91f9b7f995bd1fd9c8758962c41c9341
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 100%

---

# Recursos obsoletos e removidos {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Recursos obsoletos e removidos do AEM as a Cloud Service"
>abstract="O AEM as a Cloud Service tem um modelo de implantação nativo em nuvem. Determinados recursos foram substituídos por equivalentes nativos em nuvem e esta guia mostra esses recursos."


A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores. Além disso, como o [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] fornece um modelo de implantação nativo em nuvem, certos recursos e funcionalidades foram substituídos por seus equivalentes nativos em nuvem.

Para comunicar a remoção/substituição iminente das funcionalidades do [!DNL Experience Manager], as seguintes regras de aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Os recursos obsoletos continuam disponíveis, mas não estão aprimorados.
1. Os recursos anunciados como obsoletos são removidos na versão principal subsequente, com a maior brevidade. A data de destino real para remoção é anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoletos no [!DNL Experience Manager] as a [!DNL Cloud Service]. Normalmente, os recursos planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, como uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação atual, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Recursos | Recurso obsoleto | Substituição |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Propriedades dos Fragmentos de experiência para **Status da rede social**. | O recurso será removido em breve. |
| [!DNL Sites] | Fragmentos de conteúdo simples baseados em modelo. | [Fragmentos de conteúdo estruturado com base em modelo](/help/assets/content-fragments/content-fragments-models.md) agora. |
| [!DNL Assets] | fluxo de trabalho `DAM Asset Update` para processar imagens ingeridas. | A assimilação de ativos usa [microsserviços de ativos](/help/assets/asset-microservices-overview.md) agora. |
| [!DNL Assets] | Upload de ativos diretamente no [!DNL Experience Manager]. Consulte [APIs de upload de ativos obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Use [Upload binário direto](/help/assets/add-assets.md). Para obter detalhes técnicos, consulte [APIs de upload direto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Determinadas etapas do fluxo de trabalho](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` não são compatíveis, incluindo a chamada de ferramentas de linha de comando, como o [!DNL ImageMagick]. | Os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) oferecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodificação FFmpeg de vídeos. | Para gerar miniaturas do FFmpeg, use os [Microserviços de ativos](/help/assets/asset-microservices-overview.md). Para a transcodificação FFmpeg, use o [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interface de replicação em árvore na guia &quot;Distribuir&quot; do agente de replicação (remoção após 30 de setembro de 2021) | Abordagens [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [fluxo de trabalho Publicar árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Nem a guia Distribuir da tela do administrador do agente de replicação nem a API de replicação podem ser usadas para replicar pacotes de conteúdo com mais de 10 MB (imposição após 12 de setembro de 2022) | Abordagens [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) |


| [!DNL Foundation] | Nem a guia Distribuir da tela do administrador do agente de replicação nem a API de replicação podem ser usadas para replicar pacotes de conteúdo com mais de 10 MB. Em vez disso, use [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou o [Fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades que foram removidas do [!DNL Experience Manager] com o [!DNL Experience Manager] as a [!DNL Cloud Service].

| Área | Destaque | Substituição | Data definida para remoção |
| ------------ | ------------------ | ----------- | ------------------- |
| Interface do usuário | A interface clássica é removida da interface do usuário do produto. Algumas caixas de diálogo da interface clássica estão disponíveis para alguns recursos selecionados, como o Verificador de links, a Limpeza de versão e algumas configurações do Cloud Service. As próximas [atualizações do produto](/help/release-notes/home.md) podem remover ainda mais a disponibilidade da interface clássica. | Interface do usuário padrão | Removido |
| [!DNL Dynamic Media] | As integrações anteriores com o [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=pt-BR#integration) e o [Dynamic Media Hybrid mode](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=pt-BR#dynamic) não estão disponíveis no [!DNL Experience Manager] as a [!DNL Cloud Service]. | Use o [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornecido com o [!DNL Experience Manager] as a [!DNL Cloud Service]. | Removido |
| [!DNL Sites] | Portal Director e Portlet Component | Estes recursos foram descontinuados no [!DNL Experience Manager] 6.4 e agora foram removidos do [!DNL Experience Manager]. | Removido |
| [!DNL Sites] | Importador de design | Este recurso foi removido porque as seções imutáveis do repositório do [!DNL Experience Manager] não estão acessíveis no tempo de execução. | Removido |
| [!DNL Assets] | O compartilhamento do [!DNL Assets] com os serviços Experience Cloud Assets Core Service e Creative Cloud não está disponível. | Para integração com a [!DNL Adobe Creative Cloud], use o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html). | Removido |
| [!DNL Foundation] | Suporte para fontes de dados do Apache Sling (pacote OSGi org.apache.sling.datasource) | N/A | Removido |
| [!DNL Foundation] | Suporte para modelos de script JST (pacote OSGi org.apache.sling.scripting.jst) | N/A | Removido |
| [!DNL Foundation] | Suporte para o quadro de permissões Apache Felix Http | OSGi Http Whiteboard | Março de 2022 |
| [!DNL Foundation] | Suporte para com.adobe.granite.oauth.server | Integração do Adobe IMS | Março de 2023 |


## API Java {#java-api}

Consulte [esta página](/help/release-notes/deprecated-apis.md) para quaisquer APIs Java obsoletas ou removidas que sejam ocasionalmente introduzidas.

## Configuração OSGI {#osgi-configuration}

Consulte [este artigo](/help/implementing/deploying/osgi-configuration-api.md) para quaisquer restrições sobre a configuração das propriedades OSGI, algumas das quais podem ser introduzidas ao longo do tempo.
