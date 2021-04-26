---
title: Introdução ao AEM Headless como um Cloud Service
description: Nesta parte do AEM Headless Developer Jornada, saiba mais sobre AEM pré-requisitos headless.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 9fb18dbe60121f46dba1e11d4133e5264a6d538d
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 0%

---


# Introdução ao AEM Headless como um Cloud Service {#getting-started}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada do desenvolvedor headless,](overview.md) saiba mais sobre o que é necessário para iniciar seu próprio projeto com AEM Headless.

## A história até agora {#story-so-far}

No documento anterior da jornada sem periféricos AEM, [Saiba mais sobre o desenvolvimento sem periféricos do CMS](learn-about.md) você aprendeu a teoria básica do que é um CMS sem periféricos e agora deve:

* Entenda os conceitos básicos e a terminologia da entrega de conteúdo sem periféricos
* Entenda por que e quando o headless é necessário
* Saiba em alto nível como os conceitos sem interface são usados e como eles se relacionam

Este artigo se baseia nesses fundamentos para que você entenda como usar o AEM para implementar uma solução sem periféricos.

## Objetivo {#objective}

Este documento ajuda você a entender AEM headless no contexto de seu próprio projeto. Depois de ler, você deve:

* Entenda as noções básicas AEM recursos sem periféricos.
* Conheça os pré-requisitos para usar AEM recursos headless.
* Esteja ciente AEM níveis de integração sem periféricos.
* Pode definir seu projeto em termos de escopo.

## Noções básicas do AEM {#aem-basics}

Antes de definir seu projeto sem periféricos no AEM, é importante entender alguns conceitos básicos de AEM.

### Instância do autor {#author}

Em sua forma mais simples, o AEM consiste em uma instância de autor e uma [instância de publicação](#publish) que trabalham juntas para criar, gerenciar e publicar seu conteúdo.

O conteúdo começa na instância do autor. É aqui que os autores de conteúdo criam o conteúdo. O ambiente de criação oferece várias ferramentas para que os autores criem, organizem e reutilizem seu conteúdo.

### Publicar instância {#publish}

Depois que o conteúdo é criado na instância do autor, ele deve ser publicado para estar disponível a outros serviços para consumo. Uma instância de publicação contém todo o conteúdo que foi publicado.

### Replicação {#replication}

Replicação é o ato de transferir conteúdo da instância do autor para a instância de publicação. Isso é feito automaticamente por AEM quando um autor ou outro usuário com direitos apropriados publica conteúdo.

### Resumo das noções básicas do AEM {#aem-basics-summary}

No nível mais simples, a criação de experiências digitais no AEM requer as seguintes etapas:

1. Seus autores de conteúdo criarão seu conteúdo headless na instância do autor.
1. Quando esse conteúdo estiver pronto, ele será replicado para a instância de publicação. As APIs podem ser chamadas para recuperar esse conteúdo.

AEM a base técnica se desenvolve sem periféricos oferecendo ferramentas poderosas para gerenciar conteúdo sem periféricos, que é [descrito na próxima seção.](#aem-headless-basics)

## Noções básicas sem cabeçalho do AEM {#aem-headless-basics}

Os recursos sem periféricos do AEM são baseados em alguns recursos principais. Elas serão explicadas em detalhes em partes posteriores da jornada. Agora é importante apenas conhecer os princípios básicos do que fazem e do que são chamados.

### Modelos de fragmentos do conteúdo {#content-fragment-models}

Os Modelos de fragmentos de conteúdo definem a estrutura dos dados e do conteúdo que você criará e gerenciará no AEM. Eles servem como uma espécie de scaffolding para o seu conteúdo. Ao optar por criar o conteúdo, os autores selecionarão entre os Modelos de fragmento de conteúdo definidos, que os orientarão na criação do conteúdo.

### Fragmentos de conteúdo {#content-fragments}

Os Fragmentos de conteúdo permitem que você crie, crie, prepare e publique conteúdo independente da página. Eles permitem que você prepare conteúdo pronto para uso em vários locais e em vários canais.

Os fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

### APIs GraphQL e REST {#apis}

Para modificar o conteúdo sem interrupções, o AEM oferece duas APIs robustas.

* A API GraphQL permite criar solicitações para acessar e fornecer Fragmentos de conteúdo.
* A API REST de ativos permite criar e modificar Fragmentos de conteúdo (e outros ativos).

Você aprenderá sobre essas APIs e como usá-las em uma parte posterior da jornada sem periféricos AEM. Ou consulte a seção [recursos adicionais](#additional-resources) abaixo para obter documentação adicional.

## Níveis de integração sem cabeçalho {#integration-levels}

O AEM suporta tanto a pilha completa como a pilha completa tradicional ou os modelos potentes de um CMS. No entanto, AEM oferece não apenas essas duas opções exclusivas, mas a capacidade de suportar modelos híbridos que combinam as vantagens de ambas, oferecendo flexibilidade exclusiva para seu projeto sem periféricos.

Para garantir a compreensão dos conceitos sem periféricos, essa Jornada de desenvolvedores sem periféricos AEM se concentra no modelo sem periféricos puro para fazer você funcionar o mais rápido possível sem codificação na AEM.

No entanto, você deve estar ciente das possibilidades híbridas adicionais abertas a você, assim que entender AEM recursos headless. Nós explicamos estes casos abaixo para sua consciência. No final da jornada, você será apresentado a esses conceitos com mais detalhes caso essa flexibilidade seja necessária para o seu projeto.

### Você já tem um consumo externo de conteúdo sem periféricos, como um aplicativo de página única (SPA). {#already-have-a-spa}

Vamos supor que seu requisito básico é o mínimo para fornecer conteúdo de AEM para um serviço externo existente.

#### Nível 1: Integração de fragmentos de conteúdo - modelo autônomo tradicional {#level-1}

Esse nível de integração é o modelo sem cabeçalho tradicional e permite que os autores de conteúdo criem conteúdo no AEM e o entreguem sem aviso a qualquer número de serviços externos que usam GraphQL ou para editá-los a partir de serviços externos usando a API do Assets. Nenhuma codificação é necessária no AEM.

Neste modelo, o AEM é usado apenas para criar e veicular o conteúdo por meio do uso de Fragmentos de conteúdo AEM. A renderização e a interação com o conteúdo são delegadas ao aplicativo externo de consumo, geralmente um aplicativo de página única (SPA).

#### Nível 2: Incorpore o SPA no AEM - Modelo híbrido {#level-2}

Esse nível de integração baseia-se no primeiro nível, mas também permite que o aplicativo externo (SPA) seja incorporado no AEM para que os autores de conteúdo possam visualizar o conteúdo no contexto do aplicativo externo no AEM. O aplicativo também pode oferecer suporte à edição limitada do aplicativo externo no AEM.

Esse nível tem a vantagem de permitir que os autores de conteúdo criem conteúdo de forma flexível no AEM de uma maneira headful, com o conteúdo apresentado em contexto com um SPA externo incorporado, enquanto ainda entregam o conteúdo sem interrupções.

#### Nível 3: Incorporar e ativar totalmente SPA no AEM - Modelo híbrido {#level-3}

Esse nível de integração baseia-se no nível dois, permitindo que a maioria do conteúdo no SPA externo seja editável no AEM.

### Você ainda não tem um consumidor externo do conteúdo sem periféricos, como um aplicativo de página única (SPA). {#do-not-have-a-spa}

Se o objetivo for criar um novo SPA que consuma sem periféricos conteúdo de AEM, você poderá usar recursos como Fragmentos de conteúdo para gerenciar o conteúdo sem periféricos e também criar um SPA com AEM estrutura SPA Editor.

Usando o Editor de SPA, o SPA não apenas consome conteúdo de AEM, como também é totalmente editável em AEM pelos autores de conteúdo, proporcionando a flexibilidade da entrega sem periféricos e da edição no contexto dentro do AEM.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de iniciar seu projeto sem periféricos AEM.

### Conhecimento {#knowledge}

* GraphQL
* Experiência de desenvolvimento criando SPA com estruturas React ou Angular
* Habilidades básicas de AEM como criar Fragmentos de conteúdo e usar o editor

### Ferramentas {#tools}

* Acesso ao Sandbox para testar a implantação do seu projeto
* Instância de desenvolvimento local para modelagem e teste de dados
* SPA externos existentes ou outro consumidor do seu conteúdo AEM sem periféricos

## Definir o projeto {#defining-your-project}

Para qualquer projeto bem-sucedido, é importante definir claramente não apenas os requisitos do projeto, mas também as funções e responsabilidades.

### Escopo {#scope}

É muito importante ter um âmbito claramente definido para o projeto. O escopo informa os critérios de aceitação e permite que você estabeleça uma definição de concluído.

A primeira pergunta que você precisa fazer a si mesmo é &quot;O que estou tentando alcançar com AEM sem Cabeça?&quot; A resposta deve ser, em geral, que você tem ou terá no futuro um aplicativo de experiência que você criou com suas próprias ferramentas de desenvolvimento, não juntamente com o AEM. Esse aplicativo de experiência pode ser um aplicativo móvel, um site ou qualquer outro aplicativo de experiência voltado para o cliente final. O objetivo de usar o AEM Headless é alimentar seu aplicativo de experiência com conteúdo criado, armazenado e gerenciado no AEM com APIs de última geração que chamariam AEM Headless para buscar conteúdo ou até mesmo conteúdo totalmente CRUD diretamente do seu aplicativo de experiência. Se isso não for o que você deseja fazer, provavelmente quer [retornar à documentação AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) e encontrar a seção que melhor se adapta ao que você deseja realizar.

### Funções e responsabilidades {#roles-responsibilities}

As funções de cada projeto individual variam, mas as funções importantes a serem consideradas no conteúdo AEM desenvolvimento sem periféricos são:

* [Administrador](#administrator)
* [Autor do conteúdo](#content-author)
* [Modelador de conteúdo](#content-modeler)
* [Desenvolvedor](#developer)

#### Administrador {#administrator}

O administrador é responsável pela configuração básica do sistema. Por exemplo, o administrador configurará sua organização no sistema de gerenciamento de usuários do Adobe, referido ao Sistema Identity Management (IMS). O administrador será o primeiro usuário da organização a receber um convite por email do Adobe depois que sua organização tiver sido criada pelo Adobe no IMS. O administrador terá a capacidade de fazer logon no IMS e adicionar usuários de outras personas.

Depois que os usuários forem configurados pelo administrador, eles receberão as permissões para acessar todos os recursos do AEM para realizar seu trabalho como contribuidores no delivery do aplicativo de experiência usando AEM Headless.

O administrador deve ser o usuário que configura o AEM e prepara o ambiente de tempo de execução para permitir que [autores de conteúdo](#content-author) crie e atualize o conteúdo e [desenvolvedores](#developer) usem APIs que busquem ou modifiquem o conteúdo de seus aplicativos de experiência.

#### Autor do conteúdo {#content-author}

Os autores de conteúdo criam e gerenciam o conteúdo que é entregue sem cabeçalho pelo AEM. Os autores de conteúdo usam AEM recursos como Fragmentos de conteúdo e o Console de ativos para gerenciar seu conteúdo.

Os autores de conteúdo devem ter em mente as seguintes práticas recomendadas.

#### Plano de localização {#localization}

Plano de tradução e localização no início do projeto. Considere o &quot;Gerenciador de projetos de internacionalização&quot; como uma persona separada, cuja responsabilidade é definir qual conteúdo deve ser traduzido e o que não, e qual conteúdo traduzido pode ser modificado pelos produtores de conteúdo regionais ou locais.

Crie um plano sobre qual localização de conteúdo será necessária.

* Você precisa apenas de línguas diferentes ou também de linguagem para adotar para especificidades regionais?
* Você precisa que conteúdo de mídia avançada, como imagens ou vídeos, seja diferente para diferentes locais?

Esclareça sobre o fluxo de trabalho de atualização de conteúdo. Qual é o processo de aprovação que o sistema precisa suportar? AEM workflows podem ser aproveitados para automatizar esse processo?

Observe que sua [hierarquia de conteúdo](#content-hierarchy) pode ser aproveitada para facilitar a localização.

Consulte a seção [recursos adicionais](#additional-resources) para obter documentação adicional sobre fluxos de trabalho AEM e ferramentas de localização.

##### Aproveite a hierarquia de conteúdo {#content-hierarchy}

A hierarquia de pastas pode atender a duas principais preocupações com relação à gestão de conteúdo:

* [Localização](#localization)  - o AEM gerencia a localização do conteúdo, mantendo cópias do conteúdo em pastas específicas de localidade.
* Organização - As pastas são usadas para definir uma hierarquia de conteúdo necessária para oferecer suporte às necessidades de localização, bem como para gerenciar logicamente os Fragmentos de conteúdo.

AEM permite uma estrutura de conteúdo muito flexível e uma hierarquia pode ser arbitrariamente grande. No entanto, é importante perceber que qualquer alteração na estrutura da pasta pode ter consequências não intencionais para as consultas existentes que [dependem do caminho do conteúdo.](#developer) Portanto, uma hierarquia bem definida, claramente definida e previamente, pode ser extremamente útil para os autores de conteúdo.

As pastas também podem ser restritas para permitir apenas determinados tipos de conteúdo (com base nos Modelos de fragmento de conteúdo). Geralmente, é recomendável sempre especificar explicitamente quais modelos são permitidos para todas as pastas na hierarquia. Especificação do conteúdo permitido para uma determinada pasta:

* Impede que os autores de conteúdo criem conteúdo que não pertence à pasta.
* Otimiza o processo de criação de conteúdo filtrando os tipos de conteúdo permitidos na pasta durante a criação para mostrar apenas tipos válidos de conteúdo.

Ao criar uma estrutura de conteúdo apropriada, torna-se mais fácil coordenar a criação de conteúdo sem periféricos em todos os canais para maximizar a reutilização do conteúdo. O aproveitamento do conteúdo em vários canais melhorará muito a eficiência da produção de conteúdo e o gerenciamento de alterações.

##### Estabeleça boas convenções de nomenclatura {#naming-conventions}

Os nomes dos Fragmentos de conteúdo devem ser descritivos para os autores de conteúdo. AEM lidar de forma transparente com o escape e/ou truncamento dos nomes usados nas IDs no nível do repositório. Portanto, os nomes lógicos fornecidos pelos autores de conteúdo devem sempre ser legíveis e representar o conteúdo.

* Nome incorreto: `cta_btn_1`
* Nome correto: `Call To Action Button`

Consulte a seção [recursos adicionais](#additional-resources) para obter documentação adicional sobre AEM convenções de nomenclatura de página.

##### Não estenda o aninhamento de conteúdo {#content-nesting}

[Os ](#content-fragments) Fragmentos de conteúdo são usados no AEM para criar conteúdo sem periféricos. AEM suporta até dez níveis de aninhamento de conteúdo para Fragmentos de conteúdo. No entanto, é importante ter em mente que AEM precisará resolver iterativamente cada referência definida no Fragmento de conteúdo pai e verificar se há referências filho em todos os irmãos. Essas operações podem ser adicionadas rapidamente e se tornarem uma preocupação com o desempenho.

Como regra geral, as referências do Fragmento de conteúdo não devem ser aninhadas além de cinco níveis.

#### Modelador de conteúdo {#content-modeler}

Os modeladores de conteúdo analisam os requisitos para os dados que precisam ser entregues sem periféricos e definem a estrutura desses dados. Essas estruturas são chamadas de [Modelos de fragmento de conteúdo](#content-fragment-models) no AEM. Os Modelos de fragmentos do conteúdo são usados como a base dos Fragmentos do conteúdo criados pelos autores do conteúdo.

Uma abordagem útil ao definir Modelos de fragmento de conteúdo é criar modelos que mapeiam para os componentes UX do(s) aplicativo(s) que consumirão o conteúdo.

Como os autores de conteúdo interagem com os modelos continuamente à medida que criam novo conteúdo, o alinhamento dos modelos ao UX os ajuda a visualizar a experiência digital resultante. Levando esse alinhamento um passo além, você pode atribuir ícones aos Modelos de fragmento de conteúdo que representam o elemento UX para que os autores possam intuitivamente selecionar o modelo correto com base em dicas visuais.

#### Desenvolvedor {#developer}

Os desenvolvedores são responsáveis por unir o conteúdo que está sendo criado sem periféricos no AEM ao consumidor desse conteúdo, que geralmente pode ser um aplicativo de página única (SPA), um aplicativo da Web progressivo (PWA), uma loja da Web ou outro serviço externo ao AEM.

GraphQL serve como a &quot;cola&quot; entre o AEM e os consumidores de conteúdo sem interface. GraphQL é o idioma que consulta AEM o conteúdo necessário.

Os desenvolvedores devem ter em mente algumas recomendações básicas, pois planejam suas consultas:

* As consultas não devem depender de um caminho fixo (`ByPath`) para recuperar Fragmentos de conteúdo.
   * [Os autores de conteúdo têm controle total sobre a ](#content-hierarchy) hierarquia do fragmento de conteúdo e podem fazer alterações que podem quebrar tal consulta.
   * Em vez disso, as consultas devem optar por referências do modelo de fragmento de conteúdo com parâmetros de consulta dinâmicos para filtrar os resultados para gerar a carga útil desejada.
* Para obter o melhor desempenho da consulta, sempre use consultas persistentes no AEM. Eles são discutidos posteriormente na jornada.
* O GraphQL foi projetado para ser declarativo seguindo o lema &quot;Pergunte exatamente o que você precisa e obtenha exatamente isso&quot;. Isso significa que ao criar consultas GraphQL, sempre evite consultas do tipo `select *` que você pode criar em um banco de dados relacional.

Para uma implementação sem cabeçalho [típica usando AEM,](#level-1) o desenvolvedor não requer conhecimento de codificação de AEM.

### Requisitos de desempenho {#performance-requirements}

Para que qualquer projeto seja um sucesso, o desempenho deve ser considerado antes que qualquer conteúdo seja criado.

Você deve entender suas expectativas de usuários/visitantes e criar projetos para eles. Defina os SLOs (Service Level Objetives, objetivos de nível de serviço) e os meça para entender se você atende às expectativas do usuário.

#### Padrões de tráfego {#traffic-patterns}

Começar a entender o tráfego e os padrões de tráfego com o que você sabe do passado e depois projetar para o crescimento esperado nos próximos anos. Algumas das variáveis mais importantes a serem consideradas:

* Quantas chamadas de API por hora/dia/mês você espera e há potencial para picos e sazonalidade?
* Quantos autores de conteúdo diferentes há?
* Quantos autores de conteúdo você prevê trabalhar simultaneamente?
* Qual é a frequência das atualizações de conteúdo?
* Quantos modelos de conteúdo são necessários?
* Quantas instâncias de modelos serão necessárias?

#### Atualizar Frequência {#update-frequency}

Frequentemente, seções diferentes de experiências têm frequências diferentes de atualizações de conteúdo. Entender isso é importante para ajustar as configurações de CDN e cache. Isso também é importante para os [Content Modelers](#content-modeler), pois eles projetam modelos para representar seu conteúdo. Considere:

* Alguns tipos de conteúdo devem expirar após um determinado período?
* Há elementos que são específicos do usuário e, portanto, não podem ser armazenados em cache?

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda as noções básicas AEM recursos sem periféricos.
* Conheça os pré-requisitos para usar AEM recursos headless.
* Esteja ciente AEM níveis de integração sem periféricos.
* Pode definir seu projeto em termos de escopo.

Você deve continuar sua jornada sem periféricos de AEM revisando o documento [Caminho para sua primeira experiência usando AEM headless](path-to-first-experience.md), onde você aprenderá a configurar as ferramentas necessárias e a começar a pensar em modelar seus dados no AEM.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de desenvolvimento sem periféricos revisando o documento [Caminho para a sua primeira experiência usando AEM headless,](path-to-first-experience.md) a seguir estão alguns recursos adicionais opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar com a jornada sem periféricos.

* [Uma introdução à arquitetura do Adobe Experience Manager as a Cloud Service](/help/core-concepts/architecture.md)  - Entenda o AEM como uma estrutura Cloud Service
* [AEM Tutorials sem interface](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  - Use esses tutoriais práticos para explorar como usar as várias opções para fornecer conteúdo a endpoints sem interface com AEM e escolha o que é certo para você.
* [Gerenciamento de conteúdo sem cabeçalho usando APIs GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  - Siga este curso para obter uma visão geral da API GraphQL implementada no AEM. A autenticação via AdobeID é necessária.
* [AEM Guias WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  - Este projeto do GitHub inclui aplicativos de exemplo que destacam AEM APIs GraphQL.
* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)  - Documentação técnica do ambiente de criação de AEM, incluindo detalhes sobre a configuração de publicação do autor
* [Publicação de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  - Documentação técnica para publicação de conteúdo no AEM
* [Convenções de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md)  - Documentação técnica das restrições de nomenclatura de página no AEM
* [Multi Site Manager e Translation](/help/sites-cloud/administering/msm-and-translation.md)  - Documentação técnica AEM recursos avançados de tradução
* [AEM workflows](/help/sites-cloud/authoring/workflows/overview.md)  - Documentação técnica sobre como automatizar workflows no AEM
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)  - Documentação técnica dos Fragmentos de conteúdo.
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)  - Documentação técnica dos modelos de fragmentos do conteúdo.
* [Documentação técnica GraphQL](https://graphql.org)  - A definição GraphQL (link externo)
* [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)  - Documentação técnica que explica como criar solicitações para acessar e fornecer Fragmentos de conteúdo
* [API REST de ativos](/help/assets/content-fragments/assets-api-content-fragments.md)  - Documentação técnica que explica como criar e modificar Fragmentos de conteúdo (e outros ativos)
* [Consultas Persistentes](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching)  - Documentação técnica sobre consultas persistentes em AEM
* [Cabeça e vazia no AEM](/help/implementing/developing/headful-headless.md)  - Uma discussão completa dos níveis de integração sem periféricos disponíveis no AEM
