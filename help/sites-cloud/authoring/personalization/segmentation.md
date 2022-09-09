---
title: Noções sobre segmentação
description: A segmentação é uma preocupação chave ao criar uma campanha
exl-id: 36a9623a-bb19-498a-a0e9-ef80582b1fcf
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 100%

---

# Noções sobre segmentação {#understanding-segmentation}

A segmentação é uma consideração importante ao criar uma campanha. Na maioria dos casos, você precisa ter segmentos já definidos antes de iniciar sua campanha.

Os visitantes têm interesses e objetivos diferentes quando chegam a um site. Compreender essas metas e atender às expectativas é um fator importante para o sucesso do marketing online.

A segmentação ajuda a conseguir isso ao analisar e caracterizar:

* Atividade no site
* Perfil
* Atividade em outros sites

O conteúdo pode então ser direcionado especificamente para as necessidades e os interesses do visitante, dependendo dos segmentos aos quais ele corresponde.

## Uso da segmentação {#using-segmentation}

Segmentos são definidos em Configuração da segmentação. Eles são usados para orientar o conteúdo real visto por um público-alvo específico.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Terminologia de segmentação {#segmentation-terminology}

Ao discutir segmentação, a seguinte terminologia é usada:

* **Visitante** - Um visitante é uma pessoa que visita um site. Normalmente, a visita dessa pessoa começa em uma página de referência e passa para uma ou mais visualizações de página no seu próprio site. Um perfil comportamental pode ser criado a partir dos detalhes da visita dessa pessoa.
* **Usuário** - Um usuário é um visitante que se registra no site para receber um perfil de conta. Para gerar seu perfil, ele fornece identificação adicional, como endereço de email e gênero, entre outras informações. Informações adicionais também podem ser coletadas, incluindo a atividade na comunidade e os padrões de compra, entre outros. Com base nas informações fornecidas no perfil, um perfil demográfico pode ser criado.
* **Característica** - Uma característica é uma qualidade ou propriedade de um visitante que pode ser usada para determinar a associação a um segmento específico.
* **Segmento** - Um segmento é uma coleção de visitantes que compartilham certas características. Segmentos devem ser distintos, com um mínimo de sobreposição com outros segmentos.
* **Características comportamentais** - Características comportamentais são aquelas que se relacionam ao comportamento de um visitante no site. Dentre elas:
   * Interesse no seu site; incluindo páginas visitadas e produtos comprados
   * Interesse no site de referência; incluindo termos de pesquisa usados ou anúncios clicados
   * Interesse em outros sites, determinado com o uso de ferramentas como o Spyjax
   * Fidelidade do visitante; duração da visita, frequência de visitas
* **Características demográficas** - São características da população selecionadas, incluindo:
   * Idade
   * Renda
   * Tamanho da família
   * Estado civil
   * Sexo
   * Local
* **Características derivadas** - Algumas características demográficas são difíceis de determinar sem registro, mas podem ser derivadas pela combinação de características comportamentais e demográficas.
   * Por exemplo, a combinação do URL de referência (como uma característica comportamental) com os dados demográficos (adquiridos de ferramentas como o [Google Ad Planner](https://www.google.com/adplanner/)) permite aos proprietários do site obterem características demográficas de seus visitantes.
* **Subsegmento** - Um segmento pode ser subdividido em vários subsegmentos. Isso é feito com a definição de características adicionais.
* **Página de teaser** - Uma página de teaser é direcionada a um público-alvo específico. Ela tem conteúdo reutilizável que pode ser usado no parágrafo de teaser.
* **Campanha** -Uma campanha é uma coleção de páginas de teaser e de páginas de marketing por email, como informativos ou convites. Normalmente, uma campanha é veiculada por um período limitado, sendo substituída por outra.
* **Parágrafo de teaser** - É um parágrafo que extrai o conteúdo de outra página, dependendo de uma estratégia de seleção. Essa estratégia de seleção pode considerar segmentos e campanhas.
* **Lista** - Uma lista é extraída de um segmento de usuários registrados. Por exemplo, a localização usada para orientar o conteúdo do parágrafo de teaser.
