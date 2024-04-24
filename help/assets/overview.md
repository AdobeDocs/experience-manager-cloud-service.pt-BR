---
title: Gerenciamento de ativos digitais (DAM) do Adobe usando AEM
description: Entenda como usar e administrar o Adobe Digital Asset Management (DAM) usando o Experience Manager Assets as a Cloud Service.
contentOwner: AK
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4844d736d3791b376b7ad9cafa005c856c114837
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 76%

---


# Introdução aos Assets as a [!DNL Cloud Service] para gerenciamento de ativos digitais no AEM {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

O Adobe Experience Manager Assets as a [!DNL Cloud Service] oferece uma solução PaaS nativa em nuvem para que as empresas não somente executem suas operações de Gerenciamento de ativos digitais e Mídia dinâmica com velocidade e impacto, como também usem recursos inteligentes de próxima geração, como IA/ML, de dentro de um sistema que está sempre atualizado, disponível e aprendendo.

A assimilação simultânea de muitos ativos ou ativos complexos é uma tarefa que consome muitos recursos em uma instância do autor do Experience Manager. A instância principal consome recursos consideráveis de CPU, memória e I/O quando os ativos são adicionados, processados ou até mesmo migrados. Esses problemas de desempenho afetam a criação e a experiência de navegação dos usuários finais.

As empresas exigem suporte para uma grande variedade de formatos de arquivo e resoluções de conteúdo para uso em multidispositivos, geografia cruzada e multilíngue. Os requisitos de processamento e armazenamento de ativos exigem recursos e capacidades que podem sobrecarregar uma solução tradicional. Por vezes, as limitações técnicas do processamento de ativos não produzem os resultados desejados e, em outras ocasiões, o custo de armazenamento constitui um entrave às margens de lucro.

Para começar, entenda a [benefícios de uma oferta nativa em nuvem](#solution-benefits) para o Gerenciamento de ativos digitais. Confira as notáveis [alterações no Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) que também afetam o Experience Manager Assets, seguida das significantes [alterações no Assets](/help/assets/assets-cloud-changes.md).

Leia para conhecer os [detalhes dos novos recursos do Assets](#whats-new-assets) e [problemas conhecidos](/help/release-notes/maintenance/latest.md). Veja uma lista de [funcionalidades obsoletas ou removidas](/help/release-notes/deprecated-removed-features.md) para saber o que foi removido nesta versão. Finalmente, entenda os termos do Experience Manager com a ajuda desse [glossário](/help/overview/terminology.md).

## Benefícios da solução {#solution-benefits}

A seguir estão os principais benefícios do Assets as a [!DNL Cloud Service] para o Gerenciamento de ativos digitais. Para saber mais, consulte a [visão geral do Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Serviços em nuvem modernos para processamento de ativos**: Os novos microsserviços de ativos são um serviço de processamento de ativos baseado em nuvem, escalável, confiável e sem complicações.
* **Altamente escalável**: Escalabilidade elástica em todos os tipos de implantações. Recursos praticamente ilimitados que estão disponíveis sob demanda, conforme e quando necessário. Economiza o custo do over-design em comparação com um sistema tradicional.
* **Software mais recente**: Sempre atual e sempre atualizado. Todos os usuários têm somente o software mais recente com todos os patches, recursos, segurança e correções de erros disponíveis para eles. Desenvolvedores e integrador trabalham com o conjunto mais recente de APIs sem problemas de suporte a várias versões.
* **Sempre online**: Tempo de inatividade zero (0dt), graças à instância implantada em um cluster com backups e redundância. As atualizações também são 0dt.
* **Monitoramento constante**: O monitoramento do sistema é automatizado e as verificações e acionadores integrados ajudam a manter o desempenho, a disponibilidade e a robustez geral.
* **Implantações sem complicações**: O Experience Manager nas operações na nuvem é totalmente automatizado e não requer intervenção manual. Para implantações automatizadas, o componente do Cloud Manager (CM) automatiza a criação de imagens implantáveis do Docker que contêm seu código personalizado.

## Experiências personalizadas disponíveis para o Gerenciamento de ativos digitais {#persona-based-experiences}

A Adobe oferece uma solução robusta de gerenciamento de ativos digitais (DAM) para você aproveitar ao máximo seus ativos digitais. O Adobe Experience Manager Assets tem duas experiências separadas que usam o mesmo repositório do Cloud Services:

* **Visualização de admin**: a interface existente do Assets as a Cloud Service. Use a Exibição de administrador para todos os recursos avançados de Gerenciamento de ativos digitais, incluindo integrações, fluxos de trabalho, automação de conteúdo, publicação e muito mais.

* **Visualização de ativos**: a experiência leve de gerenciamento de ativos da Adobe para armazenar, gerenciar, descobrir e usar ativos digitais. Interface do usuário simplificada com recursos essenciais de gerenciamento de ativos digitais. Desenvolvida para usuários leves de DAM, com foco no upload, gerenciamento de metadados, pesquisa, download e compartilhamento.

Usuários que possuem acesso à visualização de admin também podem acessar a visualização de ativos. A visualização de ativos oferece uma interface simplificada que facilita o gerenciamento, a descoberta e a distribuição de seus ativos digitais. Um extenso conjunto de usuários com diferentes funções, incluindo equipes criativas, de marketing e de linha de negócios, pode colaborar em ativos e acessar os ativos corretos e aprovados quando e onde for necessário. Muitos usuários casuais de DAM preferem a visualização de ativos, visto que ela contém apenas um subconjunto de recursos. A experiência é direcionada para consumidores de ativos criativos do tipo somente leitura e que não exigem muito do DAM.

Bibliotecários, desenvolvedores e superusuários do DAM podem continuar a usar a visualização de admin ou alternar entre as interfaces, conforme necessário. Você pode selecionar a experiência que funciona melhor para sua função.

![add-tags](assets/newui-overview.svg)

Para obter informações sobre como acessar a visualização de ativos e alguns dos recursos simplificados que ela oferece em relação à visualização de admin, consulte [Introdução à visualização de ativos](/help/assets/assets-view-introduction.md).

## Integração com a criação baseada em documentos para Edge Delivery Services {#integrate-doc-authoring-edge-and-assets}

O Edge Delivery permite criar sites rápidos e cativantes, nos quais autores(as) podem atualizar, publicar conteúdo e inicializar novos sites, tudo de maneira rápida.

Integre o AEM Assets com a Criação baseada em documentos para que o Edge Delivery Services permita que os autores de sites usem imagens disponíveis em repositórios do AEM Assets ao criar documentos no Microsoft Word ou Google Docs. Para obter mais informações, consulte [Integrar o AEM Assets com a criação baseada em documentos](/help/edge/using.md#integrate-assets-edge).

## Integração com o Adobe Journey Optimizer {#integration-with-ajo}

[Adobe Journey Optimizer](https://business.adobe.com/br/products/journey-optimizer/adobe-journey-optimizer.html) O simplifica o gerenciamento de jornadas para que os clientes forneçam campanhas omnicanais com insights e decisões inteligentes. Ao criar mensagens usando o Journey Optimizer, você pode acessar o repositório as a Cloud Service do Assets diretamente de dentro da interface do Journey Optimizer. Os usuários obtêm acesso aos ativos usando a interface incorporada do Experience Manager Assets. Para obter mais informações, consulte [Criar e gerenciar ativos com o Experience Manager Assets](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/assets-images/assets.html).

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
