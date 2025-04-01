---
title: Introdução à criação no AEM como um CMS headless
description: Uma introdução ao uso dos recursos do Adobe Experience Manager as a Cloud Service como um CMS headless para criar conteúdo para seu projeto.
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: cc2e73da123d3e0676a8e175a18c1dc0bdff1daa
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 94%

---

# Introdução à criação no AEM como um CMS headless {#author-headless-introduction}

Nesta parte da [jornada do autor de conteúdo headless do AEM](overview.md), você pode aprender os conceitos (básicos) e terminologias necessários para entender sobre a criação de conteúdo ao usar o Adobe Experience Manager (AEM) as a Cloud Service como um CMS headless. Isso envolve criar e estruturar seu conteúdo para uma entrega de conteúdo headless.

## Objetivo {#objective}

* **Público**: iniciante
* **Objetivo**: apresentar os conceitos e terminologias relevantes para a criação headless.

## Sistema de gerenciamento de conteúdo (CMS) {#content-management-system}

O que é um sistema de gerenciamento de conteúdo?

Um sistema de gerenciamento de conteúdo (CMS) é exatamente isso: um sistema de computador usado para gerenciar conteúdo. Isso é um pouco vago, portanto, para ser mais preciso, ele é (normalmente) usado para gerenciar um conteúdo que você quer disponibilizar em seu(s) site(s).

## CMS headless {#headless-cms}

Headless é um termo usado para descrever sistemas que efetivamente desconectam o conteúdo da maneira tradicional de exibir esse conteúdo na web.

Tradicionalmente, você gerenciaria seu conteúdo em um CMS, o qual também seria responsável pela renderização desse conteúdo em suas páginas da web.

Agora, utilizar o método headless significa que o conjunto de conteúdo pode ser gerenciado no CMS e, em seguida, acessado por um ou mais aplicativos (independentes).

Isso significa que seu conteúdo pode ser entregue a qualquer dispositivo, em uma grande variedade de formatos. Isso torna todo o processo muito mais flexível e também significa que você não precisa se preocupar com layout e formatação.

>[!NOTE]
>
>Se quiser saber mais sobre os detalhes técnicos do CMS headless, leia a seção Saiba mais sobre o desenvolvimento do CMS headless.

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

Mas, o que é o AEM?

Em primeiro lugar, o AEM é um sistema de gerenciamento de conteúdo com uma grande variedade de recursos que também podem ser personalizados para atender às suas necessidades.

Isso significa que ele pode ser usado como um:

* CMS headless
   * No método headless, o conteúdo pode ser criado como **fragmentos de conteúdo**.
Estes são itens autônomos de conteúdo que podem ser acessados diretamente por uma variedade de aplicativos, pois têm uma estrutura predefinida com base em **modelos de fragmentos de conteúdo**.
Isso significa que o conteúdo pode atingir uma grande variedade de dispositivos, em uma grande variedade de formatos e com uma ampla seleção de funcionalidades.
(E como acréscimo, esses fragmentos também podem ser usados na criação de páginas da web do AEM, se assim desejar).

* CMS “tradicional”
   * O conteúdo é criado para páginas da Web usando uma série de componentes que definem como o conteúdo é renderizado em seu site. Até mesmo nesse caso, o AEM é extremamente flexível, pois a equipe do projeto pode desenvolver componentes personalizados.

## Modelagem de conteúdo {#content-modeling}

Portanto, a modelagem de conteúdo (também conhecida como modelagem de dados) é outro termo técnico. Por que ela deve interessar a você como autor?

Para que os aplicativos headless possam acessar seu conteúdo e fazer algo com ele, seu conteúdo realmente deve ter uma estrutura predefinida. Seria possível ter seu conteúdo em forma livre, mas isso complicaria *muito* o processo dos aplicativos.

Basicamente, o processo de definir a estrutura com a qual o seu conteúdo deve ser compatível envolve criar um modelo, e isso é chamado de modelagem de dados.

Para o AEM, o Arquiteto de conteúdo (geralmente uma pessoa diferente) realiza a modelagem de dados para criar uma variedade de **modelos de fragmentos de conteúdo**, os quais serão usados como a base do seu conteúdo por meio de **fragmentos de conteúdo**.

>[!NOTE]
>
>Se quiser saber mais sobre a modelagem de dados, leia mais na Jornada do arquiteto de conteúdo do AEM Headless.

## O que vem a seguir {#whats-next}

Agora que você aprendeu os conceitos e a terminologia, o próximo passo é [Saber mais sobre as noções básicas da criação de fragmentos de conteúdo](basics.md). Isso introduzirá os conceitos básicos de utilização do AEM, além de como criar fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)

* [Tutoriais do Headless no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR)

* Jornada do desenvolvedor AEM headless
   * [Saiba mais sobre o desenvolvimento headless do CMS](/help/journey-headless/developer/learn-about.md)
   * [Saiba como modelar seu conteúdo](/help/journey-headless/developer/model-your-content.md)

* [Portal do Desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)

* [Jornada do arquiteto de conteúdo do AEM Headless](/help/journey-headless/architect/overview.md)

* [Jornada de tradução de conteúdo do AEM Headless](/help/journey-headless/translation/overview.md)
