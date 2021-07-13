---
title: Fase de preparação
description: Fase de preparação
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 87%

---

# Prontidão {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planejamento da transição"
>abstract="Antes de iniciar sua jornada de transição para o Cloud Service, você deve se familiarizar com o AEM as a Cloud Service e rever as alterações notáveis que foram feitas nele, além de revisar os recursos que foram substituídos ou preteridos."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Analisador de práticas recomendadas"

Antes de iniciar sua jornada de transição para o Cloud Service, você deve se familiarizar com o AEM as a Cloud Service e rever as alterações notáveis que foram feitas nele, além de revisar os recursos que foram substituídos ou preteridos.

## Alterações importantes {#notable-changes}

O AEM as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar seus projetos do AEM.

No entanto, existem várias diferenças entre o AEM no local ou no AMS (Adobe Managed Services) em comparação com o AEM as a Cloud Service.

Consulte [Alterações notáveis no AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html) para compreender as diferenças importantes.

## Recursos obsoletos {#deprecated-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

Consulte [Recursos obsoletos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) para saber mais sobre os recursos e funcionalidades que foram marcados como obsoletos no Experience Manager as a Cloud Service.

## Noções gerais sobre a fase de planejamento {#introduction}

A figura a seguir mostra as principais etapas envolvidas durante a fase de Planejamento:

![imagem](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Avaliação da prontidão do Cloud Service {#access-cloud-readiness}

A primeira etapa da Fase de planejamento é avaliar sua prontidão para migrar da versão existente do AEM para o Cloud Service e determinar as áreas que exigirão que a refatoração seja compatível com o AEM as a Cloud Service.

Será necessário fazer uma avaliação abrangente do código-fonte atual do AEM em relação às alterações notáveis e aos recursos obsoletos para determinar o nível de esforço esperado na jornada de transição.

Você pode acelerar a etapa de avaliação executando o Analisador de práticas recomendadas na versão atual do AEM. Para obter mais detalhes, consulte [Best Practices Analyzer](/help/move-to-cloud-service/best-practices-analyzer/overview-best-practices-analyzer.md).

>[!NOTE]
>Se você já tem acesso ao Cloud Manager e a um ambiente do Cloud Service, é recomendável executar seu código atual em um pipeline de qualidade de código do Cloud Manager para avaliar as alterações de código necessárias para compatibilidade com o Cloud Service.

### Revisão do planejamento de recursos {#review-resource-planning}

Depois de estimar o nível de esforço que será necessário para migrar para o Cloud Service, você deve identificar recursos, criar uma equipe e mapear funções e responsabilidades para o processo de transição.

### Estabelecimento de KPIs {#establish-kpis}

Se você não tiver estabelecido Indicadores-chave de desempenho (KPIs) anteriormente, é recomendável estabelecer KPIs para sua implementação do Adobe Experience Manager (AEM) para ajudar sua equipe a se concentrar naquilo que é mais importante.

Consulte [Desenvolvimento de KPIs](https://guided.adobe.com/welcome/aem/part6.html) para saber como escolher os KPIs certos para seus objetivos de negócios.
