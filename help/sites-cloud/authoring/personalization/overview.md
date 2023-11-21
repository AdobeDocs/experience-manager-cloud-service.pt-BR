---
title: Personalização e direcionamento de conteúdo
description: Saiba como criar conteúdo personalizado e direcionado com o AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 91%

---


# Personalização e direcionamento de conteúdo {#personalization-and-content-targeting}

A personalização do conteúdo da Web que você fornece aos clientes significa personalizar essas experiências de acordo com os interesses e as necessidades deles. Você pode fazer isso com base nas informações que tem sobre eles; por exemplo, resumo de compras, idade, sexo, localização geográfica, entre outros.

Com o Adobe Experience Manager as a Cloud Service (AEM), é possível criar uma seleção de conteúdo e especificar quais públicos (grupos de usuários finais) verão cada experiência individual. Isso significa que você está direcionando suas experiências personalizadas para públicos específicos.

Quando seu leitor estiver online, seu mecanismo de direcionamento verificará as informações disponíveis sobre o usuário final e as comparará com as definições da experiência. Em seguida, o mecanismo *“decide”* qual experiência personalizada deve ser exibida.

O AEM fornece uma estrutura de ferramentas para:

* Criação de conteúdo direcionado, adequado para vários públicos, dependendo das informações disponíveis do cliente.
* Definir as regras usadas para resolver as informações do usuário conhecidas em relação a uma definição de público-alvo.
* Configurar suas páginas para apresentar experiências personalizadas direcionadas; para renderizar o conteúdo específico aplicável ao usuário final atual.

A visão geral a seguir apresenta alguns dos termos usados para personalização no AEM as a Cloud Service, seguidos por uma ordem de ação recomendada.

## Experiência {#experience}

Uma experiência é um conteúdo que você deseja mostrar aos usuários finais.

## Experiência personalizada {#personalized-experience}

Uma experiência personalizada é uma experiência exibida para um público limitado. O público é definido por você e o conteúdo é exibido somente quando as informações conhecidas sobre o usuário final atual correspondem a essa definição de público.

Ao criar páginas, você define várias experiências, com cada experiência resolvendo para um (ou mais) público(s). Se nenhum público for definido, a experiência padrão será exibida.

### Oferta {#offer}

Uma oferta é uma experiência personalizada, geralmente disponível por um período de tempo limitado.

Por exemplo, uma página de um site de amostra pode usar ofertas como a imagem do teaser que aparece na parte superior da página. Uma pessoa acima de 30 anos e uma pessoa abaixo de 30 anos podem ver diferentes ofertas como teaser de experiência.

## Público {#audience}

Um público é um grupo de usuários finais que você deseja direcionar com conteúdo personalizado. Quando um visitante abre uma página da Web, a lógica da página determina o público ao qual ele pertence com base em informações conhecidas. Com base nessa avaliação, o AEM exibe o conteúdo que você criou para esse público.

Os públicos são baseados em segmentos de marketing. Eles são criados no AEM ou no Adobe Target; você pode criar públicos do Adobe Target diretamente no AEM usando o console Públicos.

### Segmento {#segment}

No AEM ContextHub, um público é definido como um segmento, com base nas regras (condições). Eles são resolvidos para renderizar o conteúdo necessário.

## Atividade {#activity}

Uma atividade:

* define o mapeamento de um público (segmento) específico com uma experiência específica
* define o período para o qual o direcionamento é aplicado
* identifica o [mecanismo de direcionamento](#targeting-engine) que suas páginas usam

A atividade pode ser de personalização ou uma atividade de Teste A/B (no caso dos fluxos de trabalho de personalização do AEM e do Adobe Target).

Por exemplo, uma atividade define experiências para dois públicos separados: pessoas com mais de 30 anos e pessoas com menos de 30 anos. Uma página do site pode exibir produtos diferentes para cada público.

Para citar outro exemplo, seu catálogo de produtos pode incluir teasers que chamem a atenção para produtos sazonais. Assim, uma atividade Esportes de verão pode definir os públicos dos teasers durante os meses de verão.

Use o [console Atividades](/help/sites-cloud/authoring/personalization/activities.md) para criar e gerenciar as atividades das suas [marcas](#brand). Você também pode criar atividades ao criar seu [conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md) com o [Modo de direcionamento](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Marca {#brand}

Uma marca contém uma seleção de atividades e áreas de marketing.

Ao criar uma marca usando o console Atividades, ela também aparece no console Ofertas.

### Área {#area}

Uma área é uma subdivisão de uma marca.

## Modo de direcionamento {#targeting-mode}

Ao criar, esse é o modo de edição usado para ativar e configurar os componentes para personalização.

Você pode [Criar conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md) através da utilização do modo de direcionamento do AEM. O modo de direcionamento e o componente do Target fornecem ferramentas para criar conteúdo para as experiências das suas atividades de marketing.

## Fragmento de experiência {#experience-fragments}

Um conjunto agrupado de componentes que compõem uma experiência.

[Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) são feitos de conteúdo e informações (estilo etc.) para criar uma experiência; eles podem ser usados diretamente durante a criação da página. Eles podem ser considerados um subconjunto de uma página do AEM. Eles permitem que autores de conteúdo reutilizem conteúdo entre vários canais, incluindo páginas do Sites e sistemas de terceiros.

Para um exemplo de personalização, um Título, Imagem, Descrição e Botão de frases de chamariz podem ser combinados para formar uma experiência de teaser. O uso de Fragmentos de experiência é uma parte essencial do uso da personalização do Adobe Target.

## Mecanismo de direcionamento {#targeting-engine}

O mecanismo de direcionamento é o mecanismo que orienta a lógica do conteúdo direcionado. [Atividades](/help/sites-cloud/authoring/personalization/activities.md) são configuradas para usar um dos dois mecanismos de segmentação disponíveis: AEM e Adobe Target.

O mecanismo de direcionamento é a plataforma ou mecanismo que decide qual sistema de personalização usar.

Atualmente, o AEM pode usar:

* [AEM ContextHub](#aem-contexthub) (AEM padrão)
* o mecanismo de personalização do [Adobe Target](#adobe-target)

>[!CAUTION]
>
>Uma única página do AEM não pode usar ambos os mecanismos ao mesmo tempo.
>
>Você pode usar ambos os mecanismos em páginas separadas no mesmo site.

### AEM ContextHub {#aem-contexthub}

O AEM fornece um mecanismo de direcionamento [ContextHub](/help/implementing/developing/personalization/contexthub.md) integrado que processa solicitações de página e determina o conteúdo a ser exibido. Ao usar o mecanismo de direcionamento do AEM, você está limitado a usar segmentos criados no AEM para definir os públicos das suas experiências.

### Adobe Target {#adobe-target}

O mecanismo de direcionamento do [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) faz com que as informações coletadas das visitas às páginas sejam rastreadas no Adobe Target.

* Ao usar esse mecanismo de direcionamento, você utilizará os segmentos importados do Adobe Target para definir os públicos-alvo das suas experiências.
* As atividades que usam o mecanismo do Adobe Target são [sincronizadas com o Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Você pode usar esse mecanismo quando tiver [integrado com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

## Como configurar seu conteúdo personalizado {#how-to-setup-personalized-content}

Há várias etapas e definições necessárias para fornecer seu conteúdo personalizado:

1. Configure seu mecanismo de direcionamento:

   1. Configurando o [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. Integrando com o [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. Configure os públicos.

   1. Dependendo do mecanismo de direcionamento, defina o [Público do Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=pt-BR) ou o [Segmento do ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md), juntamente com as regras.

1. Crie sua [Marca e atividades](/help/sites-cloud/authoring/personalization/activities.md).

1. Crie a seleção de experiências que deseja exibir para os vários públicos.

1. Personalize essas experiências, [direcionando](/help/sites-cloud/authoring/personalization/targeted-content.md)-as para os públicos específicos (segmentos).