---
title: Visão geral do Edge Delivery Services
description: Entenda como o AEM as a Cloud Service pode se beneficiar do desempenho e das pontuações perfeitas do Lighthouse, oferecidas pelos Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 2%

---


# Visão geral do Edge Delivery Services {#edge-delivery-services}

>[!TIP]
>
>**Deseja colocar as mãos na prática imediatamente?**
>
>Se você quiser participar do Edge Delivery Services imediatamente, tem duas opções.
>
>* [Comece a criar imediatamente com um ambiente de tutorial pré-construído - totalmente configurado e pronto para uso.](https://www.aem.live/developer/ue-trial)
>* Acesse mais detalhes e configure seu próprio ambiente em menos de 30 minutos [conferindo o tutorial no aem.live.](https://www.aem.live/developer/ue-tutorial)

## O que é o Edge Delivery Services? {#what-is-edge}

O Edge Delivery Services é uma estrutura moderna de entrega de conteúdo que recria como os sites são criados e entregues, otimizando a velocidade, a simplicidade e a escalabilidade. É uma parte essencial do Adobe Experience Manager e permite experiências digitais mais rápidas, aproximando a renderização e o delivery do usuário, na borda da rede.

Não é uma substituição de uma rede de entrega de conteúdo (CDN), mas se integra perfeitamente à sua própria CDN ou à [CDN gerenciada pela Adobe incluída.](/help/implementing/dispatcher/cdn.md)

## Por que Edge Delivery Services? {#why-edge}

### Aumenta a descoberta e o tráfego {#increase-traffic}

Os sites do Edge Delivery são SEO (mecanismos de pesquisa otimizados) e GEO (mecanismo gerativo otimizado) para LLMs. Isso garante alta visibilidade e capacidade de descoberta em todas as fontes existentes e futuras de tráfego orgânico. A **arquitetura de ponta a ponta de desempenho** garante uma experiência agradável para o cliente que afetará positivamente o engajamento.

### Eficiência do desenvolvedor {#developer-efficientcy}

Entre em operação em dias e semanas em vez de meses e anos! O Edge Delivery oferece todas as ferramentas que **os desenvolvedores da web modernos** adoram: GitHub, desenvolvimento local com recarregamento automático, desempenho, simplicidade e nenhuma das complicações: sem transpilação, sem pacotes, sem configurações, sem sobrecarga.

A simplicidade do Edge Delivery não requer que você use estruturas, ferramentas ou processos complicados, ideais para a criação de código de IA. Use HTML simples, CSS moderno e JavaScript padrão para criar experiências excepcionais mais rápido do que nunca. Concentre-se no trabalho e gaste menos tempo para treinar e aprender novas ferramentas.

O Edge Delivery permite que cada desenvolvedor atinja uma pontuação mínima de 100.

### Suporte para várias fontes de conteúdo {#multiple-content-sources}

O conteúdo de várias soluções pode se integrar diretamente com o Edge Delivery, **incluindo todas as instâncias existentes do AEM**. Os autores podem gerenciar e **publicar conteúdo de qualquer sistema, como o SharePoint no Edge Delivery**, para ganhar mais velocidade com as ferramentas que já conhecem.

### Arquitetura combinável {#composable-architeture}

Seja headless ou headful, você pode fornecer o conteúdo certo no formato certo e adicionar a decoração correta para torná-la uma experiência que se destaca em qualquer canal.

## Como funciona {#how-does-it-work}

O Edge Delivery Services é um conjunto combinável de serviços que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Ele substitui o AEM Publish/Dispatcher e a maneira tradicional de criar experiências com os Componentes principais do AEM por uma solução SaaS de várias nuvens e uma abordagem de desenvolvimento de front-end puro.

![Arquitetura do Edge Delivery](assets/aem-with-eds-architecture.png)

O Edge Delivery Services usa o GitHub para que você possa gerenciar e implantar o código diretamente do seu repositório GitHub. O novo conteúdo é adicionado instantaneamente, sem um processo de reconstrução.

## Criação {#authoring}

### Edição do contexto interno {#in-context-editing}

[O Editor Universal](/help/implementing/universal-editor/introduction.md) é um WYSIWYG (what-you-see-is-what-you-get, um local personalizável e com um único local para editar conteúdo em tempo real e em contexto com uma visualização visual.

* Com a criação do AEM e o Editor universal, você aumenta a eficiência do autor, seja headless ou headful.
* Você pode aproveitar os recursos abrangentes de gerenciamento de conteúdo do AEM, incluindo fluxo de trabalho e governança.
* Você pode aproveitar vários pontos de extensão para dar suporte a seus próprios processos e integrações.
* A funcionalidade do site pode ser desenvolvida usando CSS e JavaScript no GitHub.

![Criação do AEM com o Editor Universal](assets/wysiwyg-authoring.png)

### Edição baseada em documento {#document-based-editing}

[Outra abordagem é a criação baseada em documentos](https://www.aem.live/docs/authoring), onde o conteúdo é gerenciado como documentos. O Microsoft Word é uma escolha popular, pois muitas empresas têm o SharePoint em vigor onde o conteúdo inicial é criado. Não é necessário aprender uma nova ferramenta, e a publicação de conteúdo diretamente do SharePoint e do Word elimina a inconveniência de copiar e colar conteúdo no AEM. Os clientes sem SharePoint também podem usar o Google Drive como alternativa.

## Telemetria operacional {#telemetry}

A Adobe Experience Manager usa a [Telemetria Operacional](https://www.aem.live/docs/operational-telemetry) para coletar dados de operações estritamente necessários para descobrir e corrigir problemas funcionais e de desempenho em sites viabilizados pela Adobe Experience Manager. Os dados de Telemetria Operacional podem ser usados para diagnosticar problemas de desempenho e medir a eficácia dos experimentos. A Telemetria Operacional preserva a privacidade dos visitantes por meio de [amostragem](https://www.aem.live/docs/operational-telemetry#operational-telemetry-data-is-sampled) (somente uma pequena parte de todas as exibições de página serão monitoradas) e [exclusão criteriosa de informações de identificação pessoal](https://www.aem.live/docs/operational-telemetry#what-data-is-being-collected) (PII).

## Comece a explorar {#start-exploring}

Introdução ao uso da criação do AEM com o Universal Editor e o Edge Delivery Services:

* Documentação do Edge Delivery Services [Edge Delivery Services](https://www.aem.live)
* Para obter uma visão geral da criação do AEM com o Universal Editor, consulte o documento [Criação com o AEM para Edge Delivery Services](https://www.aem.live/docs/aem-authoring) na documentação aem.live.
* Para obter uma visão geral do desenvolvedor, consulte o documento [Introdução - Tutorial do desenvolvedor do Universal Editor](https://www.aem.live/developer/ue-tutorial) na documentação do aem.live.

## Edge Delivery Services e outros produtos da Adobe Experience Cloud {#edge-other-products}

O Edge Delivery Services faz parte do Adobe Experience Manager. Dessa forma, o Edge Delivery Services e o AEM Sites podem coexistir no mesmo domínio, que é um caso de uso comum para sites maiores. Além disso, suas páginas do AEM Sites podem consumir conteúdo do Edge Delivery Services sem problemas, e o contrário também é verdadeiro.

Você também pode usar o Edge Delivery Services com o [Adobe Target](https://www.aem.live/developer/target-integration) e o [Launch.](https://experienceleague.adobe.com/pt-br/docs/experience-platform/tags/home)

## Obtendo ajuda do Adobe {#getting-help}

O Adobe fornece três camadas para ajudá-lo com o Edge Delivery Services:

* Interagir com [recursos da comunidade](#community-resources) para consultas gerais.
* Acesse seu [canal de colaboração do produto](#collaboration-channel) para perguntas específicas.
* [Registre um tíquete de suporte](#support-ticket) para resolver problemas graves e críticos **na SLA de suporte contratual**.

### Acessar recursos da comunidade {#community-resources}

A Adobe tem o compromisso de capacitá-lo com o melhor envolvimento e suporte da comunidade para o Edge Delivery Services, criação no AEM com o editor universal e criação baseada em documentos.

* Participe da [Comunidade Experience League](https://adobe.ly/3Q6kTKl) para fazer perguntas, compartilhar feedback, iniciar discussões, buscar assistência de especialistas da Adobe e consultores/campeões da AEM e conectar-se com indivíduos que pensam da mesma maneira em tempo real.
* Participe do [Canal de discórdia](https://discord.gg/aem-live), uma plataforma mais casual para interações em tempo real e trocas rápidas de ideias.

### Registrando um tíquete de suporte {#support-ticket}

{{support-ticket}}
