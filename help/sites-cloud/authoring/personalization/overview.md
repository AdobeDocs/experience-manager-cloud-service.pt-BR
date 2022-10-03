---
title: Personalização e direcionamento de conteúdo
description: Saiba como criar conteúdo personalizado e direcionado com o AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 635a9e577f03c865cdb31f539598fb8fe034d7b7
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 12%

---


# Personalização e direcionamento de conteúdo {#personalization-and-content-targeting}

Personalização do conteúdo da Web que você fornece aos clientes, significa personalizar essas experiências de acordo com seus interesses e necessidades. Você pode fazer isso com base nas informações que tem sobre eles; por exemplo, resumo de compras, idade, gênero, geografia, entre outros.

Com o Adobe Experience Manager as a Cloud Service (AEM), é possível criar uma seleção de conteúdo e especificar quais públicos-alvo (grupos de usuários finais) verão cada experiência individual. Isso significa que você está direcionando suas experiências personalizadas para públicos-alvo específicos.

Quando seu leitor estiver online, seu mecanismo de direcionamento verificará as informações disponíveis sobre o usuário final e as comparará com as definições da experiência. Em seguida, o motor *&quot;decide&quot;* qual experiência personalizada deve ser exibida.

O AEM fornece uma estrutura de ferramentas para:

* Criação de conteúdo direcionado, adequado para vários públicos-alvo, dependendo das informações disponíveis do cliente.
* Definir as regras usadas para resolver as informações do usuário conhecidas em relação a uma definição de público-alvo.
* Configurar suas páginas para apresentar experiências personalizadas direcionadas; para renderizar o conteúdo específico aplicável ao usuário final atual.

A visão geral a seguir apresenta alguns termos usados para personalização em AEM as a Cloud Service, seguidos por uma ordem de ação recomendada.

## Experiência {#experience}

Uma experiência é um conteúdo que você deseja mostrar aos usuários finais.

## Experiência personalizada {#personalized-experience}

Uma experiência personalizada é uma experiência exibida para um público-alvo limitado. O público-alvo é definido por você e o conteúdo é exibido somente quando as informações conhecidas sobre o usuário final atual correspondem a essa definição de público-alvo.

Ao criar páginas, você define várias experiências, com cada experiência resolvendo para um (ou mais) público-alvo. Se nenhum público-alvo for resolvido, a experiência padrão será exibida.

### Oferta {#offer}

<!-- not clear - needs clarification -->
<!-- is an offer a personalized experience, or an activity? -->

Uma oferta é uma experiência personalizada, geralmente disponível por um período de tempo limitado.

Por exemplo, uma página de um site de exemplo pode usar ofertas como a imagem de teaser que aparece na parte superior da página. Uma Pessoa acima de 30 anos e uma Pessoa abaixo de 30 anos verão diferentes ofertas como o teaser de experiência.

## Público {#audience}

Um público-alvo é um grupo de usuários finais que você deseja direcionar com conteúdo personalizado. Quando um visitante abre uma página da Web, a lógica da página determina o público ao qual ele pertence com base em informações conhecidas. Com base nessa avaliação, o AEM exibe o conteúdo que você criou para esse público-alvo.

Os públicos-alvo são baseados em segmentos de marketing. Eles são criados no AEM ou no Adobe Target; você pode criar públicos-alvo do Adobe Target diretamente no AEM usando o console Públicos-alvo .

### Segmento {#segment}

No AEM ContextHub, um público-alvo é definido como um segmento, com base nas regras (condições). Eles são resolvidos para renderizar o conteúdo necessário.

## Atividade {#activity}

Uma atividade :

* define o mapeamento de um público-alvo (segmento) específico com uma experiência específica
* define o período para o qual o direcionamento é aplicado
* identifica a [mecanismo de direcionamento](#targeting-engine) que suas páginas usam

<!-- an example for each of the two types would be good -->

A atividade pode ser uma atividade de personalização ou uma atividade de Teste A/B (no caso do fluxo de trabalho de personalização AEM e Adobe Target).

Por exemplo, uma atividade pode definir experiências para dois públicos separados: pessoas com mais de 30 anos e menores de 30 anos. Uma página do site pode exibir produtos diferentes para cada público-alvo.

Ou, como outro exemplo, seu catálogo de produtos pode incluir teasers que focalizam a atenção em produtos sazonais. Assim, uma atividade Esportes de verão pode definir os públicos alvo dos teasers durante os meses de verão.

Use o [Console de atividades](/help/sites-cloud/authoring/personalization/activities.md) para criar e gerenciar as atividades do [Marcas](#brand). Você também pode criar atividades ao criar seu [conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md) com [Modo de direcionamento](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Marca {#brand}

Uma Marca contém uma seleção de atividades e áreas de marketing.

Ao criar uma marca usando o console Atividades, ela também aparece no console Ofertas .

### Área {#area}

Uma área é uma subdivisão de uma Marca.

## Modo de direcionamento {#targeting-mode}

Ao criar, esse é o modo de edição usado para ativar e configurar os componentes para personalização.

Você pode [Criar conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md) uso do modo de Direcionamento de AEM. O modo de direcionamento e o componente do Target fornecem ferramentas para criar conteúdo para as experiências das suas atividades de marketing.

## Fragmento de experiência {#experience-fragments}

Um conjunto agrupado de componentes que compõem uma experiência.

[Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) são feitas de conteúdo e informações (estilo, etc.) para criar uma experiência; eles podem ser usados diretamente durante a criação da página. Eles podem ser considerados um subconjunto de uma página de AEM. Eles permitem que autores de conteúdo reutilizem conteúdo em canais, incluindo páginas de Sites e sistemas de terceiros.

Para um exemplo de personalização, um Botão de ação Título, Imagem, Descrição e Chamada para formar uma experiência de teaser. O uso de Fragmentos de experiência é uma parte essencial do uso da personalização do Adobe Target.

## Mecanismo de direcionamento {#targeting-engine}

O mecanismo de direcionamento é o mecanismo que resolve a lógica do conteúdo direcionado. [Atividades](/help/sites-cloud/authoring/personalization/activities.md) são configuradas para usar um dos dois mecanismos de segmentação disponíveis: AEM e Adobe Target.

O mecanismo de direcionamento é a plataforma ou mecanismo que decide qual sistema de personalização usar.

Atualmente, AEM pode usar:

* [AEM ContextHub](#aem-contexthub) (AEM padrão)
* o [Adobe Target](#adobe-target) mecanismo de personalização

>[!CAUTION]
>
>Uma única página de AEM não pode usar ambos os mecanismos ao mesmo tempo.
>
>Você pode usar ambos os mecanismos em páginas separadas no mesmo site.

### AEM ContextHub {#aem-contexthub}

AEM fornece o mecanismo de direcionamento integrado ContextHub que processa solicitações de página e determina o conteúdo a ser exibido. Ao usar o mecanismo de direcionamento do AEM, você está limitado a usar segmentos criados no AEM para definir os públicos das suas experiências.

### Adobe Target {#adobe-target}

O mecanismo de direcionamento do Adobe Target faz com que as informações coletadas das visitas às páginas sejam rastreadas no Adobe Target.

* Ao usar esse mecanismo de direcionamento, você usa segmentos importados do Adobe Target para definir os públicos das suas experiências.
* As atividades que usam o mecanismo do Adobe Target são [sincronizadas com o Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Você pode usar esse mecanismo quando tiver [integrado ao Adobe Target](/help/sites-cloud/integrating/integration-adobe-target-ims.md).

## Como configurar seu conteúdo personalizado {#how-to-setup-personalized-content}

Há várias etapas e definições necessárias para fornecer seu conteúdo personalizado:

1. Integre o AEM ao seu mecanismo de direcionamento.

1. Configure os públicos.

   1. Dependendo do mecanismo de direcionamento, defina o público-alvo ou o segmento, juntamente com as regras.

1. Crie sua marca e atividades.

1. Crie a seleção de experiências que deseja exibir para os vários públicos-alvo.

1. Personalize essas experiências, direcionando-as para públicos-alvo específicos (segmentos).