---
title: Visão geral do Edge Delivery Services
description: Entenda como o AEM as a Cloud Service pode se beneficiar do desempenho e das pontuações perfeitas do Lighthouse, oferecidas pelos Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 3%

---


# Visão geral do Edge Delivery Services {#edge-delivery-services}

Com o Edge Delivery Services, o AEM oferece experiências excepcionais que impulsionam o engajamento e as conversões. O AEM faz isso fornecendo experiências de alto impacto que são rápidas de serem criadas e desenvolvidas. É um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar e publicar rapidamente e novos sites são lançados rapidamente. Dessa forma, com os Edge Delivery Services você pode melhorar a conversão, reduzir custos e fornecer velocidade de conteúdo extrema.

Ao usar os Edge Delivery Services, é possível:

* Crie sites rápidos com uma pontuação Lighthouse perfeita e monitore continuamente o desempenho do site por meio do monitoramento de uso real (RUM).
* Aumente a eficiência da criação desvinculando as fontes de conteúdo. Pronto para uso, você pode usar a WYSIWYG e a Criação baseada em documento. Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo site.
* Use uma estrutura de experimentação integrada que permita a criação rápida de testes, a execução sem impacto no desempenho e a liberação rápida para a produção de um vencedor de testes.

## Visão geral {#overview}

O Edge Delivery Services é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Você pode usar ambos [Gestão de conteúdo AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) e criação WYSIWYG usando o [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) bem como [criação baseada em documento.](https://www.aem.live/docs/authoring)

O diagrama a seguir ilustra como você pode editar conteúdo no Microsoft Word (criação baseada em documento) e publicar no Edge Delivery Services. Ele também mostra a edição WYSIWYG usando o editor universal.

![Arquitetura de entrega de borda](assets/AEM-with-EDS-publishing-simple2.png)

Você pode usar o conteúdo diretamente do Microsoft Word ou do Google Docs, de modo que essas fontes se tornem páginas no seu site. Além disso, cabeçalhos, listas, imagens e elementos de fonte podem ser transferidos da fonte inicial para o site. O novo conteúdo é adicionado instantaneamente, sem um processo de reconstrução.

O Edge Delivery Services usa o GitHub para que você possa gerenciar e implantar o código diretamente do seu repositório GitHub. Por exemplo, você escreve conteúdo no Google Docs ou no Microsoft Word e a funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub. Quando estiver pronto, use a extensão do navegador Sidekick para visualizar e publicar atualizações de conteúdo.

Leitura adicional na documentação do Edge Delivery Services:

* Para obter detalhes sobre como começar a usar o Edge Delivery, consulte o [Criar seção.](https://www.aem.live/docs/#build)
* Para entender como criar e publicar conteúdo usando o Edge Delivery, consulte [Seção de publicação.](https://www.aem.live/docs/authoring)
* Para entender como iniciar corretamente o projeto do seu site, consulte [Lançar seção.](https://www.aem.live/docs/#launch)

## Edge Delivery Services e outros produtos da Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services fazem parte do Adobe Experience Manager e, como tal, os sites Edge Delivery Services e AEM podem coexistir no mesmo domínio, que é um caso de uso comum para sites maiores. Além disso, o conteúdo dos Edge Delivery Services pode ser facilmente consumido pelas páginas do AEM Sites e vice-versa.

Consulte a [Guia de introdução do desenvolvedor para WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para criar com AEM e Edge Delivery Services.

Também é possível usar o Edge Delivery Services com [Adobe Target,](https://www.aem.live/developer/target-integration) [Monitoramento de uso real (RUM)](https://www.aem.live/developer/rum) para diagnosticar o uso e o desempenho de seus sites e [Iniciar.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Introdução aos Edge Delivery Services. {#getting-started}

É fácil começar a usar o Edge Delivery Services seguindo o [Introdução - Tutorial do desenvolvedor.](https://www.aem.live/developer/tutorial)

## Obtendo ajuda do Adobe {#getting-help}

O Adobe fornece três canais para ajudá-lo com Edge Delivery Services:

* Interagir com [recursos da comunidade](#community-resources) para consultas gerais.
* Acessar o [canal de colaboração do produto](#collaboration-channel) para perguntas específicas.
* [Registrar um tíquete de suporte](#support-ticket) para resolver problemas importantes e críticos.

### Acessar recursos da comunidade {#community-resources}

O Adobe tem o compromisso de capacitá-lo com o melhor envolvimento e suporte da comunidade para o Edge Delivery Services, o WYSIWYG e a criação baseada em documentos.

* Participar de [Comunidade Experience League](https://adobe.ly/3Q6kTKl) fazer perguntas, compartilhar feedback, iniciar discussões, buscar assistência de especialistas em Adobe e AEM Advisors/Champs, e conectar-se com indivíduos que pensam da mesma maneira em tempo real.
* Associe-se ao nosso [Canal de discórdia,](https://discord.gg/aem-live) uma plataforma mais casual para interações em tempo real e trocas rápidas de ideias.

### Como acessar o canal de colaboração do produto {#collaboration-channel}

Dado o valor do canal de comunicação direta com os usuários, todos os projetos AEM no lançamento estabelecerão um canal Slack para velocidade, atualizações críticas e relatórios dimensionados sobre a qualidade da experiência. Você receberá um convite do Adobe para se associar a um canal de Slack específico da sua organização.

Para obter mais informações, consulte o documento [Uso do Slack Bot](https://www.aem.live/docs/slack) para obter mais detalhes.

Você pode entrar em contato com as equipes de produtos Adobe por meio do canal de colaboração provisionado para responder a perguntas sobre o uso do produto ou sobre as práticas recomendadas. Não há metas de nível de serviço (SLT) associadas às conversas por meio do canal de colaboração do produto.

### Registrando um tíquete de suporte {#support-ticket}

Se um problema do produto exigir investigação e solução de problemas adicionais e precisar atender aos SLTs de resposta, você poderá enviar um tíquete de suporte seguindo esse processo usando o Admin Console:

1. [Seguindo o processo de suporte padrão,](https://experienceleague.adobe.com/?support-tab=home&amp;lang=pt-BR#support) e criar um ticket.
1. Adicionar **Entrega de borda** no título do ticket.
1. Na descrição, forneça os seguintes detalhes além da descrição do problema:

   * URL do site ativo. Por exemplo: `www.mydomain.com`.
   * URL do site de origem (`.hlx` URL).

## O que vem a seguir {#whats-next}

Introdução à revisão [Utilização do Edge Delivery Services.](/help/edge/using.md)
