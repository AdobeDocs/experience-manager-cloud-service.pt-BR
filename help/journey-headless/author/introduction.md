---
title: jornada do autor de conteúdo sem cabeçalho do AEM
description: Uma introdução aos recursos avançados e flexíveis sem periféricos do Adobe Experience Manager as a Cloud Service e como criar conteúdo para seu projeto.
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# Criação para headless com AEM - uma introdução {#author-headless-introduction}

Nesta parte da [AEM Jornada do autor de conteúdo sem cabeçalho](overview.md), você pode aprender os conceitos (básicos) e a terminologia necessários para entender a criação de conteúdo para entrega de conteúdo sem periféricos com o Adobe Experience Manager (AEM) as a Cloud Service.

## Objetivo {#objective}

* **Público-alvo**: Iniciante
* **Objetivo**: Apresente os conceitos e a terminologia relevantes para a criação sem cabeçalho.

## Sistema de gerenciamento de conteúdo (CMS) {#content-management-system}

O que é um sistema de gerenciamento de conteúdo?

Um Sistema de Gerenciamento de Conteúdo (CMS) é exatamente o que diz ser - um sistema de computador usado para gerenciar conteúdo. Isso é um pouco geral, portanto, para ser mais preciso, ele é (normalmente) usado para gerenciar conteúdo que você deseja disponibilizar em seu(s) site(s).

## CMS sem periféricos {#headless-cms}

Headless é um termo usado para descrever sistemas que efetivamente desconectam o conteúdo da maneira de exibir esse conteúdo na Web.

Tradicionalmente, você gerenciava seu conteúdo em um CMS e o mesmo CMS seria responsável pela renderização desse conteúdo em suas páginas da Web.

Agora, sem periféricos significa que o conjunto de conteúdo pode ser gerenciado no CMS e, em seguida, acessado por um ou mais aplicativos (independentes).

Isso significa que seu conteúdo pode ser entregue a qualquer dispositivo, em uma grande variedade de formatos. Isso torna todo o processo muito mais flexível e também significa que você não precisa se preocupar com layout e formatação.

>[!NOTE]
>
>Se quiser saber mais sobre os detalhes técnicos do CMS sem periféricos, leia mais em Saiba mais sobre o desenvolvimento sem periféricos do CMS.

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

Então, o que é AEM?

Em primeiro lugar, AEM é um sistema de gerenciamento de conteúdo com uma grande variedade de recursos que também podem ser personalizados para atender às suas necessidades.

Isso significa que ele pode ser usado como um:

* CMS sem periféricos
   * Para ficar sem cabeçalho, seu conteúdo pode ser criado como **Fragmentos de conteúdo**.
São itens de conteúdo autocontidos que podem ser acessados diretamente por uma variedade de aplicativos, pois têm uma estrutura predefinida, com base em **Modelos de fragmento de conteúdo**.
Isso significa que o conteúdo pode atingir uma grande variedade de dispositivos, em uma grande variedade de formatos e com uma ampla seleção de funcionalidade.
(E como um whammy duplo, esses fragmentos também podem ser usados na construção de páginas AEM da Web, se desejar).

* CMS &quot;tradicional&quot;
   * O conteúdo é criado para páginas da Web, usando uma variedade de componentes que definem como o conteúdo será renderizado em seu site. Mesmo aqui AEM é extremamente flexível, pois a equipe de projeto pode desenvolver componentes personalizados.

## Modelagem de conteúdo {#content-modeling}

Portanto, a modelagem de conteúdo (também conhecida como modelagem de dados) é outro termo técnico - por que ela deve interessá-lo como autor?

Para que os aplicativos sem periféricos possam acessar seu conteúdo e fazer algo com ele, seu conteúdo precisa realmente ter uma estrutura predefinida. Seria possível ter seu conteúdo como forma livre, mas isso tornaria a vida *muito* complicada para os aplicativos.

Basicamente, o processo de definição da estrutura para que o seu conteúdo adira ao envolve o design de um modelo, chamado de modelagem de dados.

Para AEM a função de Arquiteto de conteúdo (geralmente uma pessoa diferente), executará a modelagem de dados para projetar um intervalo de **Modelos de fragmento de conteúdo** - que você usará como base para o seu conteúdo usando **Fragmentos de conteúdo**.

>[!NOTE]
>
>Se quiser saber mais sobre a modelagem de dados, leia mais na Jornada AEM Headless Content Architect .

## O que vem a seguir {#whats-next}

Agora que você aprendeu os conceitos e a terminologia, a próxima etapa é [Saiba mais sobre as noções básicas da criação de Fragmentos de conteúdo](basics.md). Isso introduzirá a manipulação básica de AEM, além de como criar Fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* jornada do desenvolvedor sem periféricos do AEM
   * [Saiba mais sobre o desenvolvimento sem periféricos do CMS](/help/journey-headless/developer/learn-about.md)
   * [Saiba como modelar seu conteúdo](/help/journey-headless/developer/model-your-content.md)

* jornada do AEM Headless Content Architect

* jornada de tradução de conteúdo sem cabeçalho do AEM