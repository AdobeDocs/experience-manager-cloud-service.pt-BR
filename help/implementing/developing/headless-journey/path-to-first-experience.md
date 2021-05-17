---
title: Caminho para sua primeira experiência usando AEM headless
description: Nesta parte da Jornada de desenvolvedores sem cabeçalho do AEM, você entenderá as etapas para implementar sua primeira experiência sem periféricos em AEM incluindo considerações de planejamento e também aprenderá as práticas recomendadas para tornar seu caminho o mais tranquilo possível.
hide: true
hidefromtoc: true
index: false
exl-id: 257fc173-6bfb-4b60-b66c-6d6bdd5cf13f
source-git-commit: 3554c4a4ea1858ea5b4ffbe0fd223a540261cb5c
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 0%

---

# Caminho para sua primeira experiência usando AEM headless {#path-to-first-experience}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada de desenvolvedores headless,](overview.md) você entenderá as etapas para implementar sua primeira experiência headless em AEM incluindo considerações de planejamento e também aprenderá as práticas recomendadas para tornar seu caminho o mais suave possível.

## A história até agora {#story-so-far}

No documento anterior da jornada sem periféricos AEM, [Introdução AEM Sem Cabeça como Cloud Service](getting-started.md) você aprendeu a teoria básica do que é um CMS sem periféricos e agora deve:

* Entenda as noções básicas AEM recursos sem periféricos.
* Conheça os pré-requisitos para usar AEM recursos headless.
* Esteja ciente AEM níveis de integração sem periféricos.
* Pode definir seu projeto em termos de escopo.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto sem periféricos AEM.

## Objetivo {#objective}

Este documento ajuda você a entender as etapas necessárias para implementar seu primeiro projeto. Depois de lê-lo, você deve:

* Entenda considerações importantes sobre o planejamento para criar seu conteúdo.
* Entenda as etapas para implementar o headless no AEM.
* Saiba quais ferramentas e configurações de AEM necessárias são necessárias.
* Conheça as práticas recomendadas para tornar sua jornada sem interface suave, manter a geração de conteúdo eficiente e garantir que o conteúdo seja entregue rapidamente.

## Requisitos {#requirements}

Antes de continuar com este documento, verifique se você revisou o documento anterior na Jornada do desenvolvedor sem cabeçalho do AEM, [Introdução ao AEM Headless como um Cloud Service](getting-started.md), certificando-se de:

* Satisfazer os requisitos enumerados na lista.
* Consideraram sua própria definição de projeto, incluindo escopo, funções e desempenho.

## Planejamento para o sucesso {#planning-for-success}

Para iniciar seu primeiro projeto sem periféricos de AEM, é necessário garantir que você tenha um modelo de conteúdo compatível com a personalização e as atualizações que deseja fazer em todos os canais.

Separado de AEM, você também quer garantir que tenha um ambiente de desenvolvimento adequado configurado se estiver criando um aplicativo do lado do cliente para testar seu cliente em relação às chamadas de API para AEM como Cloud Service.

### Definir modelos de conteúdo e APIs {#defining-models}

Você deseja direcionar uma experiência consistente e gerenciar campanhas personalizadas em todos os canais, para que possa visualizar cada canal e superfície individual como sua própria estrutura de conteúdo distinta para entrega. No entanto, ter cada canal com seu próprio modelo de conteúdo será um desafio manter.

Em vez disso, você deve considerar como o conteúdo em diferentes superfícies é relacionado com base no princípio de organização, como hierarquias de marca e produto, categorias de bens ou superfícies, ou etapas na jornada do cliente. Por exemplo, se você tiver um conjunto de superfícies que suportam uma marca específica de carros que você fabrica, você pode começar com um modelo de conteúdo para informações gerais que seria verdadeiro para o carro inteiro e ter elementos específicos de contexto mais específicos, como conteúdo necessário quando o carro está iniciando até quando há problemas de serviço. Esse modelo imporá uma herança do conteúdo geral da marca de carro, permitindo, ao mesmo tempo, deslocamentos com base no contexto específico necessário. Também ajuda no gerenciamento futuro de atualizações desse conteúdo, pois é possível impor o controle com base em funções, como o profissional de marketing geral ou o gerente de produto de toda a marca de carro, em comparação com um autor responsável pela experiência de &quot;carro inicial&quot;.

Depois de ter o modelo de conteúdo e a visualização nítida dos vários clientes aos quais o conteúdo precisa ser revelado, é necessário garantir que GraphQL/APIs associadas ao acesso a vários modelos de conteúdo sejam publicadas para todos os clientes que precisam desse conteúdo. Há diferentes opções de como acessar determinado conteúdo. Você pode solicitar um conteúdo específico estático, que permite o armazenamento em cache do conteúdo e desempenho mais alto. Você também pode solicitar conteúdo gerado dinamicamente, o que exigirá mais processamento. Certifique-se de que os clientes estejam aproveitando as APIs mais eficientes para suas necessidades comerciais.

## Entendendo os ambientes {#understanding-environments}

No AEM há três tipos de ambientes: desenvolvimento, armazenamento temporário e produção.

Os ambientes de desenvolvimento (você pode ter vários) são um local seguro para experimentar e experimentar ideias. Durante a fase inicial do projeto, a Adobe recomenda o uso dos ambientes de desenvolvimento para experimentar variações de modelos de conteúdo e ver quais fornecem a saída pretendida para as superfícies.

O ambiente de preparo para projetos sem periféricos é usado para validar novas versões de produtos AEM antes de serem implantados na produção. Mantenha uma lista atualizada dos modelos de conteúdo de produção lá e um subconjunto do conteúdo, para que você possa renderizar arquivos JSON para comparar se eles ainda fornecerem o mesmo resultado, conforme você faz alterações ou a versão de AEM introduz alterações

A produção é onde os autores de conteúdo criam e gerenciam seu conteúdo real. As mudanças de modelo na produção devem ser realizadas com cuidado e tendo em mente a compatibilidade com versões anteriores.

Durante o estágio de desenvolvimento, é recomendável trabalhar com um ambiente de desenvolvimento e preparo. À medida que você migra para o teste de desempenho, é necessário migrar para o ambiente de produção.

### Cooperação de desenvolvedores e autores de conteúdo {#cooperation}

Os desenvolvedores precisam de um ambiente de desenvolvimento AEM configurado com os modelos de conteúdo preenchidos. O desenvolvedor desenvolve o cliente que consumirá conteúdo AEM sem periféricos à medida que os autores de conteúdo ainda estiverem criando o conteúdo. É por isso que as definições de API são realmente importantes. Ao utilizar o SDK do AEM, o desenvolvedor pode criar um gancho de teste para que os testes de unidade e do cliente possam ser criados para garantir que o cliente possa renderizar corretamente o conteúdo.

Os autores de conteúdo criam conteúdo com base nos modelos de conteúdo que foram definidos no ambiente de preparo. Usando a ferramenta de criação de fragmento de conteúdo, o autor criaria um novo fragmento de conteúdo ou editaria um fragmento de conteúdo existente. Antes de publicá-lo, o autor pode visualizar como será a aparência no cliente, trabalhando com o desenvolvedor para impulsionar o modelo de conteúdo para o desenvolvimento ou configurar um ambiente de desenvolvedor apenas para que os autores visualizem a aparência dele no cliente.

## Configurar {#setup}

Antes de começar a usar o headless no AEM, você precisa garantir que todos os recursos necessários estejam habilitados. Esta seção descreve o que é necessário. As etapas reais para executar essas etapas são detalhadas posteriormente em [AEM Jornada do desenvolvedor headless.](#overview.md)

Opcionalmente, também é possível consultar os [recursos adicionais](#additional-resources) para obter mais informações sobre os tópicos individuais.

### Configuração {#configuration}

1. Ativar fragmentos de conteúdo
1. Ativar GraphQL
1. Configurar o SDK sem cabeçalho

## Implementação do seu primeiro aplicativo sem periféricos AEM

Esta é uma visão geral do que é necessário para implementar seu primeiro aplicativo sem periféricos usando o AEM para fornecer seu conteúdo. Como executar essas etapas será descrito detalhadamente em partes posteriores da Jornada do desenvolvedor sem cabeçalho.

1. Criar modelos de fragmento de conteúdo
1. Criar fragmentos de conteúdo
1. Consultar conteúdo com GraphQL

## Práticas recomendadas     {#best-practices}

Um projeto sem cabeça não só é bem-sucedido devido à tecnologia implementada, como também devido ao bom planejamento e governança de projetos. Veja a seguir uma série de práticas recomendadas para autores e desenvolvedores de conteúdo que devem se lembrar ao planejar seu projeto.

### Organizar seu conteúdo {#organizing-content}

* Torne sua estrutura tão complexa quanto necessário, mas mantenha-a tão simples quanto possível. Estruturas de conteúdo mais simples ajudam a simplificar a governança de conteúdo e melhorar o desempenho do sistema.
* Priorize a reutilização do conteúdo em sua estratégia. Crie submodelos e referências de conteúdo que podem ser reutilizados em vários modelos e canais de nível superior.
* Torne as estruturas de conteúdo o mais autoexplicativas possível para que os autores de conteúdo possam aprender e se adaptar rapidamente às tarefas de criação.
* Se você tiver restrições de acesso, tente alinhar seu modelo de conteúdo aos requisitos de acesso.
* Quando você tem requisitos de acesso, eles devem direcionar sua hierarquia de conteúdo. Agrupe o conteúdo, que é editado pelo mesmo grupo de pessoas.
* Agrupe conteúdo semelhante em uma pasta.
   * É mais provável que um autor de conteúdo copie e cole o conteúdo existente para criar novo conteúdo. Portanto, fazer isso na mesma pasta o torna mais eficiente.
   * AEM permite definir modelos permitidos por pasta, de modo que o botão **Criar novo** mostre apenas os modelos suportados nesse local.
* A criação do editor de Fragmento de conteúdo em linha dos novos Fragmentos de conteúdo pode ser simplificada se a pasta raiz estiver definida no modelo. Então o profissional não precisa escolher um local, mas precisa apenas fornecer um nome e pode começar a editar a nova referência.

### Criar conteúdo {#authoring}

* Para versões específicas de canal do seu conteúdo, considere usar variações de fragmento de conteúdo. As variações são sincronizadas com o conteúdo principal para simplificar o gerenciamento de alterações de conteúdo.
* Convide outros produtores de conteúdo para revisar o conteúdo e fornecer feedback com anotações e comentários, que estão disponíveis no editor de fragmentos de conteúdo e globalmente em fragmentos no console de administração de fragmentos de conteúdo.
* Mantenha as coisas em movimento com o menor número possível de elementos obrigatórios. Os elementos obrigatórios podem bloquear o workflow.

### Criação de conteúdo global {#localization}

* Estabeleça regras e controle para a tradução de conteúdo. Para reduzir a carga do sistema, estabeleça a tradução como um processo assíncrono que pode ser executado em intervalos maiores. Aguarde tempo para o controle de qualidade de localização e a correção de erros.
* Aproveite todos os recursos fornecidos pelo seu sistema de tecnologia de tradução que você pode integrar com AEM, como a memória de tradução.
* Entenda se conteúdo de mídia avançada, como imagens e vídeos, precisa de localização.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda considerações importantes sobre o planejamento para criar seu conteúdo.
* Entenda as etapas para implementar o headless no AEM.
* Saiba quais ferramentas e configurações de AEM necessárias são necessárias.
* Conheça as práticas recomendadas para tornar sua jornada sem interface suave, manter a geração de conteúdo eficiente e garantir que o conteúdo seja entregue rapidamente.

Queremos que você se baseie nesse conhecimento fundamental para entender totalmente o poder e a flexibilidade de AEM sem Cabeça, para que possa aproveitar esse conhecimento para seus próprios projetos. Para fazer isso, você tem opções.

### Escolha seu próprio empreendimento {#choose-your-path}

Não importa qual o seu estilo de aprendizagem, o Adobe quer que você tenha sucesso à medida que inicia seu projeto AEM Headless.

* Se preferir continuar a **aprender sobre conceitos sem interface e AEM tecnologias sem periféricos**, continue sua jornada sem periféricos AEM revisando o documento [Como modelar seu conteúdo como AEM Modelos de conteúdo](model-your-content.md), onde você aprenderá a modelar sua estrutura de conteúdo em AEM.
* Se preferir **aprender ao fazer**, você pode ir para o [Tutorial Introdução AEM mãos sem cabeçalho](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html), onde você irá ir diretamente para AEM desenvolvimento sem cabeçalho implementando um projeto simples para expor AEM conteúdo sem interface.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de desenvolvimento sem periféricos revisando o documento [Como modelar seu conteúdo como modelos de conteúdo AEM,](model-your-content.md) os seguintes são alguns recursos adicionais e opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar na jornada sem periféricos.

* [Desenvolvimento sem periféricos para o AEM Sites as a Cloud Service](/help/implementing/developing/headless/introduction.md)  - Uma introdução rápida para orientar o desenvolvedor sem periféricos AEM com os recursos necessários
* [AEM Tutorials sem interface](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  - Use esses tutoriais práticos para explorar como usar as várias opções para fornecer conteúdo a endpoints sem interface com AEM e escolha o que é certo para você.
* [Gerenciamento de conteúdo sem cabeçalho usando APIs GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  - Siga este curso para obter uma visão geral da API GraphQL implementada no AEM. A autenticação via AdobeID é necessária.
* [AEM Guias WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  - Este projeto do GitHub inclui aplicativos de exemplo que destacam AEM APIs GraphQL.
* [Introdução à arquitetura do Adobe Experience Manager as a Cloud Service](/help/core-concepts/architecture.md)  - Uma visão geral completa AEM arquitetura
* [Guia de introdução sem cabeçalho](/help/implementing/developing/headless/introduction.md#getting-started)  - uma introdução rápida para AEM recursos sem periféricos para usuários que já conhecem AEM.
* [Criar modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md)  - Documentação técnica sobre modelos de fragmento de conteúdo
* [Criar fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)  - Documentação técnica sobre fragmentos de conteúdo
* [Consultar o conteúdo com GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)  - Documentação técnica da API GraphQL
