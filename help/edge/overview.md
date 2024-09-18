---
title: Visão geral do Edge Delivery Services
description: Entenda como o AEM as a Cloud Service pode se beneficiar do desempenho e das pontuações perfeitas do Lighthouse, oferecidas pelos Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: fa50e661d05a5083be3605a8c6e26450357f4aec
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 2%

---


# Visão geral do Edge Delivery Services {#edge-delivery-services}

Com o Edge Delivery Services, o AEM oferece experiências excepcionais que impulsionam o engajamento e as conversões. O AEM faz isso fornecendo experiências de alto impacto que são rápidas de serem criadas e desenvolvidas. É um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar e publicar rapidamente e novos sites são lançados rapidamente. Dessa forma, com os Edge Delivery Services você pode melhorar a conversão, reduzir custos e fornecer velocidade de conteúdo extrema.

Ao usar os Edge Delivery Services, é possível:

* Crie sites rápidos com uma pontuação Lighthouse perfeita e monitore continuamente o desempenho do site por meio do monitoramento de uso real (RUM).
* Aumente a eficiência da criação desvinculando as fontes de conteúdo. Você pode usar o WYSIWYG e a criação baseada em documento imediatamente. Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo site.
* Use uma estrutura de experimentação integrada que permita a criação rápida de testes, a execução sem impacto no desempenho e a liberação rápida para a produção de um vencedor de testes.

## Reação ágil às necessidades dos negócios {#agile-reaction}

Como líder de longa data do setor, a Adobe sabe como é importante poder criar e publicar rapidamente conteúdo novo e significativo para seus clientes. Os desafios comuns no dimensionamento da criação de conteúdo foram esclarecidos pelo mercado, incluindo:

1. **A demanda por conteúdo continua crescendo.**
   * É necessário desbloquear novos autores de conteúdo para atender a essa demanda.
   * O processo de criação de conteúdo deve ser dimensionado de maneira eficaz em toda a empresa.
   * Os autores devem ser capazes de reagir rapidamente às mudanças de tendências.
1. **O conteúdo omnicanal é necessário.**
   * O controle de layout é necessário independentemente da entrega de conteúdo.
   * Os autores precisam estar capacitados para alterar o layout de conteúdo diretamente.
1. **A pressão aumenta para direcionar o ROI do conteúdo.**
   * Os próprios autores precisam ter a capacidade de otimizar o conteúdo que criam.

Essas tendências têm se mostrado consistentes em todo o setor. No entanto, os requisitos individuais variam inevitavelmente de projeto para projeto. O objetivo de qualquer projeto do Edge Delivery Services é encontrar a solução que funcione para os usuários.

1. **Concentre-se no valor em vez de recursos.** - Determine o fluxo de trabalho mais otimizado para atender aos seus autores, em vez de se perder no extenso conjunto de recursos do AEM.
1. **Aproveite a flexibilidade do AEM.** - Os recursos do AEM não precisam ser usados no vácuo. Use os recursos necessários para cada caso de uso.
1. **Aproveite a experiência do autor.** - Envolva autores de conteúdo reais no projeto desde o início para garantir que você esteja agregando o valor de que eles precisam, implementando os recursos que fazem sentido.

Ao se concentrar no valor para seus autores, o projeto Edge Delivery Services pode atender às demandas modernas do setor enfrentadas por seus criadores de conteúdo e fornecer conteúdo rapidamente para agradar seus clientes.

## Ferramentas de criação flexíveis para seus criadores de conteúdo {#overview}

O Edge Delivery Services é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Você pode usar o [gerenciamento de conteúdo AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) e a criação do WYSIWYG usando o [Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md) e a [criação baseada em documentos.](https://www.aem.live/docs/authoring)

O diagrama a seguir ilustra como você pode editar conteúdo no Microsoft Word (criação baseada em documento) e publicar no Edge Delivery Services. Ele também mostra a edição do WYSIWYG usando o Editor universal.

![Arquitetura do Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

O Edge Delivery Services usa o GitHub para que você possa gerenciar e implantar o código diretamente do seu repositório GitHub. O novo conteúdo é adicionado instantaneamente, sem um processo de reconstrução.

### Criação baseada em documento {#document-based}

Com a criação baseada em documentos, é possível usar o conteúdo diretamente do Microsoft Word ou do Google Docs, de modo que essas fontes se tornem páginas do site. Cabeçalhos, listas, imagens e elementos de fonte podem ser transferidos da origem inicial para o site.

* Com a criação baseada em documentos, todos os profissionais de marketing são habilitados a criar conteúdo rapidamente com ferramentas de criação conhecidas (Microsoft Word, Google Docs etc.).
* A criação de conteúdo é simplificada permitindo a criação, a revisão e a publicação diretamente nos documentos de origem.
* Como as ferramentas conhecidas são usadas, a integração zero é necessária para os autores de conteúdo, aumentando a velocidade do conteúdo.
* A funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub.

![Criação baseada em documentos](assets/document-based-authoring.png)

Leitura adicional na documentação de criação baseada em documento:

* Para obter detalhes sobre como começar a usar o Edge Delivery, consulte a seção [Build.](https://www.aem.live/docs/#build)
* Para entender como criar e publicar conteúdo usando o Edge Delivery, consulte a [seção Publish.](https://www.aem.live/docs/authoring)
* Para entender como iniciar corretamente o projeto do seu site, consulte a [seção Iniciar.](https://www.aem.live/docs/#launch)

### Criação no WYSIWYG {#wysiwyg-authoring}

A criação do WYSIWYG (What-You-See-is-What-You-Get, o que você vê é o que você obtém) aproveita o Universal Editor, um local personalizável e completo para editar conteúdo em tempo real e em contexto, com uma visualização visual.

* Com a criação no WYSIWYG, você aumenta a eficiência do autor, seja headless ou headful.
* Você pode aproveitar os recursos abrangentes de gerenciamento de conteúdo do AEM, incluindo fluxo de trabalho e governança.
* Aproveite vários pontos de extensão para dar suporte a seus próprios processos e integrações.
* A funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub.

![criação no WYSIWYG](assets/wysiwyg-authoring.png)

Leitura adicional na documentação de criação do WYSIWYG:

* Para obter uma visão geral do Editor universal e da criação do WYSIWYG, consulte o documento [Criação de conteúdo do WYSIWYG para o Edge Delivery Services.](/help/edge/wysiwyg-authoring/authoring.md)
* Para obter uma visão geral do desenvolvedor, consulte o documento [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### Decidindo sobre seu método de criação {#authoring-method}

A flexibilidade do AEM garante que suas necessidades de criação sejam atendidas. O Adobe pode ajudá-lo a determinar qual método (ou métodos) melhor atende às suas necessidades.

* Sempre envolva seus autores de conteúdo na decisão.
* É possível implementar vários métodos de criação.
* Você sempre pode alterar o método de criação depois do fato.
* Você não deve decidir antes da implementação, mas como parte da implementação.

Consulte o documento [Escolhendo um método de criação](authoring-methods.md) para obter mais informações.

## Edge Delivery Services e outros produtos da Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services fazem parte do Adobe Experience Manager e, como tal, os sites Edge Delivery Services e AEM podem coexistir no mesmo domínio, que é um caso de uso comum para sites maiores. Além disso, o conteúdo dos Edge Delivery Services pode ser facilmente consumido pelas páginas do AEM Sites e vice-versa.

Consulte o [Guia de Introdução do Desenvolvedor para WYSIWYG com Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para ser autor com AEM e Edge Delivery Services.

Você também pode usar Edge Delivery Services com o [Adobe Target](https://www.aem.live/developer/target-integration) [RUM (Monitoramento de Uso Real)](https://www.aem.live/developer/rum) para diagnosticar o uso e o desempenho de seus sites e o [Launch.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Introdução aos Edge Delivery Services. {#getting-started}

É fácil começar a usar o Edge Delivery Services seguindo o [Guia de Introdução - Tutorial do Desenvolvedor.](https://www.aem.live/developer/tutorial)

## Obtendo ajuda do Adobe {#getting-help}

O Adobe fornece três canais para ajudá-lo com Edge Delivery Services:

* Interagir com [recursos da comunidade](#community-resources) para consultas gerais.
* Acesse seu [canal de colaboração do produto](#collaboration-channel) para perguntas específicas.
* [Registre um tíquete de suporte](#support-ticket) para resolver problemas graves e críticos.

### Acessar recursos da comunidade {#community-resources}

O Adobe tem o compromisso de capacitá-lo com o melhor envolvimento e suporte da comunidade para o Edge Delivery Services, o WYSIWYG e a criação baseada em documentos.

* Participe da [Comunidade Experience League](https://adobe.ly/3Q6kTKl) para fazer perguntas, compartilhar feedback, iniciar discussões, buscar assistência de especialistas em Adobe e consultores/campistas do AEM, e conectar-se com indivíduos que pensam da mesma maneira em tempo real.
* Junte-se ao nosso [canal Discord](https://discord.gg/aem-live), uma plataforma mais casual para interações em tempo real e trocas rápidas de ideias.

### Como acessar o canal do Collaboration do seu produto {#collaboration-channel}

Dado o valor do canal de comunicação direta com os usuários, todos os projetos AEM no lançamento estabelecerão um canal Slack para velocidade, atualizações críticas e relatórios dimensionados sobre a qualidade da experiência. Você receberá um convite do Adobe para se associar a um canal de Slack específico da sua organização.

Para obter mais informações, consulte o documento [Uso do Slack Bot](https://www.aem.live/docs/slack) para obter mais detalhes.

Você pode entrar em contato com as equipes de produtos Adobe por meio do canal de colaboração provisionado para responder a perguntas sobre o uso do produto ou sobre as práticas recomendadas. Não há metas de nível de serviço (SLT) associadas às conversas por meio do canal de colaboração do produto.

### Registrando um tíquete de suporte {#support-ticket}

Se um problema do produto precisar de investigação e solução de problemas adicionais e precisar atender aos SLTs de resposta, você poderá enviar um tíquete de suporte.

Para registrar um tíquete de suporte, primeiro registre o site do Edge Delivery no Cloud Manager. O registro do seu site com o Cloud Manager é recomendado a todos os usuários do AEM as a Cloud Service e o [traz vários benefícios.](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) Consulte [a documentação do Cloud Manager](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) para obter detalhes se você ainda não tiver registrado seu site.

Depois que o site for registrado na Cloud Manager, siga este processo usando o Admin Console para enviar um tíquete de suporte:

1. [Após o processo de suporte padrão](https://experienceleague.adobe.com/?support-tab=home&amp;lang=pt-BR#support), crie um tíquete.
1. Adicionar **Edge Delivery** no título do tíquete.
1. Na descrição, forneça os seguintes detalhes além da descrição do problema:

   * URL do site ativo. Por exemplo: `www.mydomain.com`.
   * URL do site de origem (`.hlx` URL).

## O que vem a seguir {#whats-next}

Comece revisando [Usando Edge Delivery Services.](/help/edge/using.md)
