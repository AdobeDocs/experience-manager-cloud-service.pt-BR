---
title: Noções sobre segmentação
description: A segmentação é uma preocupação chave ao criar uma campanha
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 58%

---


# Noções sobre segmentação {#understanding-segmentation}

A segmentação é uma consideração importante ao criar uma campanha. Na maioria dos casos, você precisa ter segmentos já definidos antes de iniciar sua campanha.

Os visitantes têm interesses e objetivos diferentes quando chegam a um site. Compreender essas metas e atender às expectativas é um fator importante para o sucesso do marketing online.

A segmentação ajuda a conseguir isso ao analisar e caracterizar:

* Atividade no site
* Perfil
* Atividade em outros sites

O conteúdo pode então ser direcionado especificamente para as necessidades e interesses do visitante, dependendo dos segmentos correspondentes.

## Uso da segmentação {#using-segmentation}

Segmentos são definidos em Configuração da segmentação. Eles são usados para orientar o conteúdo real visto por um público-alvo específico.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Segmentation Terminology {#segmentation-terminology}

Ao discutir segmentação, a seguinte terminologia é usada:

* **Visitor** - A visitor is a person visiting a website. Normalmente, a visita dessa pessoa começa em uma página de referência e passa para uma ou mais visualizações de página no seu próprio site. Um perfil comportamental pode ser criado a partir dos detalhes da visita dessa pessoa.
* **Usuário** - Um usuário é um visitante que se registra no site para receber um perfil de conta. Para gerar seu perfil, ele fornece identificação adicional, como endereço de email e gênero, entre outras informações. Informações adicionais também podem ser coletadas, incluindo a atividade na comunidade e os padrões de compra, entre outros. Com base nas informações fornecidas no perfil, um perfil demográfico pode ser criado.
* **Característica** - uma característica ou propriedade de um visitante que pode ser usada para determinar a associação em um segmento específico.
* **Segmento** - um segmento é uma coleção de visitantes que compartilham certas características. Segmentos devem ser distintos, com um mínimo de sobreposição com outros segmentos.
* **Behavioral Traits** - Behavioral traits are those that relate to a visitor&#39;s behavior on the website. Dentre elas:
   * Interesse no seu site; incluindo páginas visitadas e produtos comprados
   * Interesse no site de referência; incluindo termos de pesquisa usados ou anúncios clicados
   * Interesse em outros sites, determinado com o uso de ferramentas como o Spyjax
   * lealdade dos Visitantes; duração da visita, frequência das visitas
* **Características demográficas** - São características da população selecionadas, incluindo:
   * Idade
   * Renda
   * Tamanho da família
   * Estado civil
   * Sexo
   * Local
* **Características** derivadas - Algumas características demográficas são difíceis de determinar sem registro, mas podem ser derivadas pela combinação de características comportamentais e demográficas.
   * Por exemplo, a combinação do URL de referência (como uma característica comportamental) com os dados demográficos (adquiridos de ferramentas como o [Google Ad Planner](https://www.google.com/adplanner/)) permite aos proprietários do site obterem características demográficas de seus visitantes.
* **Subsegment** - A segment can be subdivided into several subsegments. Isso é feito com a definição de características adicionais.
* **Página** do teaser - Uma página do teaser é direcionada a uma audiência específica. Ela tem conteúdo reutilizável que pode ser usado no parágrafo de teaser.
* **Campaign** - A campaign is a collection of teaser pages and e-mail marketing pages, such as newsletters or invitations. Normalmente, uma campanha é executada por um período limitado e é substituída por outra campanha.
* **Parágrafo** do teaser - é um parágrafo que extrai o conteúdo de outra página dependendo de uma estratégia de seleção. Essa estratégia de seleção pode considerar segmentos e campanhas.
* **Lista** - uma lista é extraída de um segmento de usuários registrados. Por exemplo, a localização usada para orientar o conteúdo do parágrafo de teaser.
