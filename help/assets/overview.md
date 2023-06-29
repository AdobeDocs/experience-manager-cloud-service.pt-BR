---
title: Introdução ao Assets as a [!DNL Cloud Service]
description: Novidades do Assets as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: d0deca8acbf6049d5be6c27275eedf9b52b27658
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 68%

---

# Introdução ao Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

O Adobe Experience Manager Assets as a [!DNL Cloud Service] oferece uma solução PaaS nativa em nuvem para que as empresas não somente executem suas operações de Gerenciamento de ativos digitais e Mídia dinâmica com velocidade e impacto, como também usem recursos inteligentes de próxima geração, como IA/ML, de dentro de um sistema que está sempre atualizado, disponível e aprendendo.

A assimilação simultânea de muitos ativos ou ativos complexos é uma tarefa que consome muitos recursos em uma instância do autor do Experience Manager. A instância principal consome recursos consideráveis de CPU, memória e I/O quando os ativos são adicionados, processados ou até mesmo migrados. Esses problemas de desempenho afetam a criação e a experiência de navegação dos usuários finais.

As empresas exigem suporte para uma grande variedade de formatos de arquivo e resoluções de conteúdo para uso em multidispositivos, geografia cruzada e multilíngue. Os requisitos de processamento e armazenamento de ativos exigem recursos e capacidades que podem sobrecarregar uma solução tradicional. Por vezes, as limitações técnicas do processamento de ativos não produzem os resultados desejados e, em outras ocasiões, o custo de armazenamento constitui um entrave às margens de lucro.

Para começar, entenda os [benefícios de uma oferta nativa em nuvem](#solution-benefits). Confira as notáveis [alterações no Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) que também afetam o Experience Manager Assets, seguida das significantes [alterações no Assets](/help/assets/assets-cloud-changes.md).

Leia para conhecer os [detalhes dos novos recursos do Assets](#whats-new-assets) e [problemas conhecidos](/help/release-notes/maintenance/latest.md). Veja uma lista de [funcionalidades obsoletas ou removidas](/help/release-notes/deprecated-removed-features.md) para saber o que foi removido nesta versão. Finalmente, entenda os termos do Experience Manager com a ajuda desse [glossário](/help/overview/terminology.md).

## Benefícios da solução {#solution-benefits}

Estes são os principais benefícios do Assets as a [!DNL Cloud Service]. Para saber mais, consulte a [visão geral do Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Serviços em nuvem modernos para processamento de ativos**: Os novos microsserviços de ativos são um serviço de processamento de ativos baseado em nuvem, escalável, confiável e sem complicações.
* **Altamente escalável**: Escalabilidade elástica em todos os tipos de implantações. Recursos praticamente ilimitados que estão disponíveis sob demanda, conforme e quando necessário. Economiza o custo do over-design em comparação com um sistema tradicional.
* **Software mais recente**: Sempre atual e sempre atualizado. Todos os usuários têm somente o software mais recente com todos os patches, recursos, segurança e correções de erros disponíveis para eles. Desenvolvedores e integrador trabalham com o conjunto mais recente de APIs sem problemas de suporte a várias versões.
* **Sempre online**: Tempo de inatividade zero (0dt), graças à instância implantada em um cluster com backups e redundância. As atualizações também são 0dt.
* **Monitoramento constante**: O monitoramento do sistema é automatizado e as verificações e acionadores integrados ajudam a manter o desempenho, a disponibilidade e a robustez geral.
* **Implantações sem complicações**: O Experience Manager nas operações na nuvem é totalmente automatizado e não requer intervenção manual. Para implantações automatizadas, o componente do Cloud Manager (CM) automatiza a criação de imagens implantáveis do Docker que contêm seu código personalizado.

## Experiências disponíveis com base em persona {#persona-based-experiences}

A Adobe oferece uma solução robusta de Gerenciamento de ativos digitais (DAM) para você aproveitar ao máximo seus ativos digitais. O Adobe Experience Manager Assets tem duas experiências separadas que usam o mesmo repositório de Cloud Services:

* **Exibição do administrador**: a interface do usuário as a Cloud Service do Assets. Use a Exibição de administrador para todos os recursos avançados de gerenciamento de ativos, incluindo integrações, fluxos de trabalho, automação de conteúdo, publicação e muito mais.

* **Exibição de ativos**: Adobe uma experiência leve de gerenciamento de ativos para armazenar, gerenciar, descobrir e usar ativos digitais. Interface do usuário simplificada com recursos essenciais de gerenciamento de ativos. Projetado para usuários leves de DAM, com foco em upload, gerenciamento de metadados, pesquisa, download e compartilhamento.

Os usuários com acesso à visualização Administrador também podem acessar a visualização Ativos. A Exibição de ativos fornece uma interface simplificada que facilita o gerenciamento, a descoberta e a distribuição de ativos digitais. Um amplo conjunto de usuários de diferentes funções, incluindo equipes criativas, de marketing e de linha de negócios, pode colaborar em ativos e acessar os ativos corretos e aprovados quando e onde for necessário. Muitos usuários casuais do DAM preferem a exibição de Ativos, pois ela contém apenas um subconjunto de recursos. A experiência é direcionada para criativos, consumidores de ativos somente leitura e usuários de DAM mais leves.

Bibliotecários, desenvolvedores e superusuários do DAM podem continuar a usar a visualização de Administrador ou alternar entre as interfaces do usuário, conforme necessário. Você pode selecionar a experiência que funciona melhor para sua função.

![adicionar-tags](assets/newui-overview.svg)

Para obter informações sobre como acessar a exibição de Ativos e algumas das simplificações que ela oferece em relação à exibição de Administrador, consulte [Introdução à exibição de ativos](/help/assets/assets-view-introduction.md).

## Novos recursos do Assets {#whats-new-assets}

Os novos recursos significativos são:

* [Microsserviços de ativos](/help/assets/asset-microservices-overview.md)
* [Métodos de upload de ativos](/help/assets/add-assets.md)

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
