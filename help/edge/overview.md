---
title: Visão geral do Edge Delivery Services
description: Entenda como o AEM as a Cloud Service pode se beneficiar do desempenho e das pontuações perfeitas do Lighthouse, oferecidas pelos Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: bf0e840fb3cd1ea5bc832823c522415c066f0018
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---


# Visão geral do Edge Delivery Services {#edge-delivery-services}

Com o Edge Delivery Services, a AEM oferece experiências excepcionais que impulsionam o engajamento e as conversões. O AEM faz isso fornecendo experiências de alto impacto, que são rápidas de serem criadas e desenvolvidas. É um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar e publicar rapidamente e novos sites são lançados rapidamente. Dessa forma, com o Edge Delivery Services você pode melhorar a conversão, reduzir custos e fornecer velocidade de conteúdo extrema.

Ao usar o Edge Delivery Services, você pode:

* Crie sites rápidos com uma pontuação Lighthouse perfeita e monitore continuamente o desempenho do site por meio do monitoramento de uso real (RUM).
* Aumente a eficiência da criação desvinculando as fontes de conteúdo. Pronto para uso, você pode usar a criação do AEM com o Editor universal e a criação baseada em documento. Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo site.
* Use uma estrutura de experimentação integrada que permita a criação rápida de testes, a execução sem impacto no desempenho e a liberação rápida para a produção de um vencedor de testes.

## Reação ágil às necessidades dos negócios {#agile-reaction}

Como líder reconhecido há muito tempo no setor, a Adobe sabe como é importante poder criar e publicar conteúdo novo e significativo rapidamente para seus clientes. Os desafios comuns no dimensionamento da criação de conteúdo foram esclarecidos pelo mercado, incluindo:

1. **A demanda por conteúdo continua crescendo.**
   * É necessário desbloquear novos autores de conteúdo para atender a essa demanda.
   * O processo de criação de conteúdo deve ser dimensionado de maneira eficaz em toda a empresa.
   * Os autores devem ser capazes de reagir rapidamente às mudanças de tendências.
1. **O conteúdo omnicanal é necessário.**
   * O controle de layout é necessário independentemente da entrega de conteúdo.
   * Os autores precisam estar capacitados para alterar o layout de conteúdo diretamente.
1. **A pressão aumenta para direcionar o ROI do conteúdo.**
   * Os próprios autores precisam ter a capacidade de otimizar o conteúdo que criam.

Essas tendências têm se mostrado consistentes em todo o setor. No entanto, os requisitos individuais inevitavelmente variam de projeto para projeto. O objetivo de qualquer projeto do Edge Delivery Services é concentrar-se em encontrar a solução que funcione para os usuários.

1. **Concentre-se no valor em vez de recursos.** - Determine o fluxo de trabalho mais otimizado para atender aos seus autores, em vez de se perder no extenso conjunto de recursos do AEM.
1. **Aproveite a flexibilidade da AEM.** - Os recursos do AEM não precisam ser usados no vácuo. Use os recursos necessários para cada caso de uso.
1. **Aproveite a experiência do autor.** - Envolva autores de conteúdo reais no projeto desde o início para garantir que você esteja agregando o valor de que eles precisam, implementando os recursos que fazem sentido.

Ao se concentrar no valor para seus autores, o projeto do Edge Delivery Services pode atender às demandas modernas do setor enfrentadas por seus criadores de conteúdo e fornecer conteúdo rapidamente para agradar seus clientes.

## Ferramentas de criação flexíveis para seus criadores de conteúdo {#overview}

O Edge Delivery Services é um conjunto combinável de serviços que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Você pode usar o [gerenciamento de conteúdo do AEM](/help/sites-cloud/authoring/author-publish.md) e a criação de conteúdo usando o [Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md) e a [criação baseada em documentos.](https://www.aem.live/docs/authoring)

O diagrama a seguir ilustra como você pode editar conteúdo no Microsoft Word (criação baseada em documento) e publicar no Edge Delivery Services junto com a criação de conteúdo do AEM usando o Editor universal.

![Arquitetura do Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

O Edge Delivery Services usa o GitHub para que você possa gerenciar e implantar o código diretamente do seu repositório GitHub. O novo conteúdo é adicionado instantaneamente, sem um processo de reconstrução.

### Criação baseada em documento {#document-based}

Com a criação baseada em documentos, é possível usar o conteúdo diretamente do Microsoft Word ou Google Docs, de modo que essas fontes se tornem páginas no site. Cabeçalhos, listas, imagens e elementos de fonte podem ser transferidos da origem inicial para o site.

* Com a criação baseada em documentos, todos os profissionais de marketing são habilitados a criar conteúdo rapidamente com ferramentas de criação conhecidas (Microsoft Word, Google Docs etc.).
* A criação de conteúdo é simplificada permitindo a criação, a revisão e a publicação diretamente nos documentos de origem.
* Como as ferramentas conhecidas são usadas, a integração zero é necessária para os autores de conteúdo, aumentando a velocidade do conteúdo.
* A funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub.

![Criação baseada em documentos](assets/document-based-authoring.png)

Leitura adicional na documentação de criação baseada em documento:

* Para obter detalhes sobre como começar a usar o Edge Delivery, consulte a seção [Build da documentação aem.live.](https://www.aem.live/docs/#build)
* Para entender como criar e publicar conteúdo usando o Edge Delivery, consulte a [seção Publicar da documentação do aem.live.](https://www.aem.live/docs/authoring)
* Para entender como iniciar corretamente o projeto do seu site, consulte a [seção Launch da documentação aem.live](https://www.aem.live/docs/#launch)

### Criação no AEM com o editor universal{#wysiwyg-authoring}

O Editor universal é um local personalizado com tudo o que você vê é o que você obtém (WYSIWYG) para editar conteúdo em tempo real e em contexto com uma visualização visual.

* Com a criação do AEM com o Editor universal, você aumenta a eficiência do autor, seja headless ou headful.
* Você pode aproveitar os recursos abrangentes de gerenciamento de conteúdo do AEM, incluindo fluxo de trabalho e governança.
* Aproveite vários pontos de extensão para dar suporte a seus próprios processos e integrações.
* A funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub.

![Criação do AEM com o Editor Universal](assets/wysiwyg-authoring.png)

Introdução à criação do AEM com o Editor universal e o Edge Delivery Services:

* Para obter uma visão geral da criação do AEM com o Universal Editor, consulte o documento [Criação com o AEM para Edge Delivery Services](https://www.aem.live/docs/aem-authoring) na documentação aem.live.
* Para obter uma visão geral do desenvolvedor, consulte o documento [Introdução - Tutorial do desenvolvedor do Universal Editor](https://www.aem.live/developer/ue-tutorial) na documentação do aem.live.

### Decidindo sobre seu método de criação {#authoring-method}

A flexibilidade da AEM garante que suas necessidades de criação sejam atendidas. O Adobe pode ajudá-lo a determinar qual método (ou métodos) melhor atende às suas necessidades.

* Sempre envolva seus autores de conteúdo na decisão.
* É possível implementar vários métodos de criação.
* Você sempre pode alterar o método de criação depois do fato.
* Não é necessário tomar uma decisão antes da implementação, mas como parte dela.

## Edge Delivery Services e outros produtos da Adobe Experience Cloud {#edge-other-products}

O Edge Delivery Services faz parte do Adobe Experience Manager. Dessa forma, o Edge Delivery Services e o AEM Sites podem coexistir no mesmo domínio, que é um caso de uso comum para sites maiores. Além disso, suas páginas do AEM Sites podem consumir conteúdo do Edge Delivery Services sem problemas, e o contrário também é verdadeiro.

Consulte o documento [Introdução - Tutorial do desenvolvedor do Universal Editor](https://www.aem.live/developer/ue-tutorial) na documentação do aem.live para saber como iniciar seu próprio projeto para criar com o AEM e o Edge Delivery Services.

Você também pode usar o Edge Delivery Services com o [Adobe Target](https://www.aem.live/developer/target-integration), o [Monitoramento de Uso Real (RUM)](https://www.aem.live/developer/rum) para diagnosticar o uso e o desempenho de seus sites e o [Launch.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Obtendo ajuda do Adobe {#getting-help}

A Adobe fornece três canais para ajudá-lo com o Edge Delivery Services:

* Interagir com [recursos da comunidade](#community-resources) para consultas gerais.
* Acesse seu [canal de colaboração do produto](#collaboration-channel) para perguntas específicas.
* [Registre um tíquete de suporte](#support-ticket) para resolver problemas graves e críticos.

### Acessar recursos da comunidade {#community-resources}

A Adobe tem o compromisso de capacitá-lo com o melhor envolvimento e suporte da comunidade para o Edge Delivery Services, criação no AEM com o editor universal e criação baseada em documentos.

* Participe da [Comunidade Experience League](https://adobe.ly/3Q6kTKl) para fazer perguntas, compartilhar feedback, iniciar discussões, buscar assistência de especialistas da Adobe e consultores/campeões da AEM e conectar-se com indivíduos que pensam da mesma maneira em tempo real.
* Participe do [Canal de discórdia](https://discord.gg/aem-live), uma plataforma mais casual para interações em tempo real e trocas rápidas de ideias.

### Como acessar o canal do Collaboration do seu produto {#collaboration-channel}

Dado o valor do canal de comunicação direta com os usuários, todos os projetos do AEM no lançamento estabelecem um canal do Slack para velocidade, atualizações críticas e relatórios dimensionados sobre a qualidade da experiência. Você recebe um convite da Adobe para participar de um canal do Slack específico da sua organização.

Para obter mais informações, consulte o documento [Uso do Slack Bot](https://www.aem.live/docs/slack) para obter mais detalhes.

Você pode entrar em contato com as equipes de produtos da Adobe por meio do canal de colaboração provisionado do produto para responder a perguntas sobre o uso do produto ou sobre as práticas recomendadas. Não há metas de nível de serviço (SLT) associadas às conversas por meio do canal de colaboração do produto.

### Registrando um tíquete de suporte {#support-ticket}

{{support-ticket}}
