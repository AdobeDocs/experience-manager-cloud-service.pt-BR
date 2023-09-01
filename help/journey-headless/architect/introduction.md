---
title: 'Modelagem de conteúdo para o AEM as a Headless CMS: uma introdução'
description: Uma introdução ao uso dos recursos do Adobe Experience Manager as a Cloud Service as a Headless CMS para modelar o conteúdo do seu projeto.
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 03cf688168106f71f2df2511782be7c1f3cc0dae
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 97%

---

# Modelagem de conteúdo para o AEM as a Headless CMS: uma introdução {#architect-headless-introduction}

Nesta parte da [Jornada do arquiteto de conteúdo headless do AEM](overview.md), você pode aprender os conceitos e a terminologia (básica) necessários para entender a modelagem de conteúdo ao usar o Adobe Experience Manager (AEM) as a Cloud Service as a Headless CMS.

Este documento ajuda você a entender a entrega de conteúdo headless, como o AEM é compatível com a tecnologia headless e como o conteúdo é modelado para a tecnologia headless. Depois de ler esse documento, você deverá:

* Entender os conceitos básicos de entrega de conteúdo headless.
* Familiarizar-se com o modo com que o AEM é compatível com a modelagem headless e de conteúdo.

## Objetivo {#objective}

* **Público**: iniciante
* **Objetivo**: apresentar os conceitos e a terminologia relevantes para a Modelagem de conteúdo headless.

## Entregar conteúdo em pilha completa {#full-stack}

Desde a ascensão dos sistemas de gerenciamento de conteúdo (CMS) de larga escala e fácil utilização, as organizações estão usando-os como um local central para gerenciar mensagens, comunicações e a identidade visual de sua marca. Usar o CMS como ponto central para administrar experiências melhorou a eficiência, eliminando a necessidade de duplicar tarefas em sistemas diferentes.

![O CMS clássico de pilha completa](/help/journey-headless/developer/assets/full-stack.png)

Em um CMS de pilha completa, toda a funcionalidade de manipulação de conteúdo está no CMS. Os recursos do sistema constituem componentes diferentes da pilha do CMS. A solução de pilha completa tem muitas vantagens.

* Há um sistema para manter.
* O conteúdo é gerenciado centralmente.
* Todos os serviços do sistema estão integrados.
* A criação de conteúdo é contínua.

Portanto, se um novo canal precisar ser adicionado ou se o suporte para novos tipos de experiências for necessário, um novo componente (ou mais) poderá ser inserido na pilha e as alterações são feitas em um único lugar.

![Adicionar um novo canal à pilha](/help/journey-headless/developer/assets/adding-channel.png)

No entanto, a complexidade das dependências na pilha rapidamente se torna aparente, pois outros itens na pilha precisam ser ajustados para acomodar as alterações.

## A interface no headless {#the-head}

A interface de qualquer sistema é geralmente o renderizador de saída, normalmente na forma de uma GUI ou outra saída gráfica.

Quando falamos de um CMS headless, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, apenas entregando o **conteúdo** de forma padronizada, um CMS headless omite a renderização final de saída, deixando a **apresentação** do conteúdo para o serviço de consumo.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, um webshop, experiências móveis, aplicativos web progressivos (PWAs) etc., absorvem conteúdo do CMS headless e fornecem sua própria renderização. Eles fornecem suas próprias interfaces para o conteúdo.

Omitir a interface simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Modelagem de conteúdo {#content-modeling}

A modelagem de conteúdo (também conhecida como modelagem de dados) é sua especialidade. Portanto, o que precisa ser considerado ao modelar para headless?

Para que os aplicativos headless possam acessar seu conteúdo e fazer algo com ele, o conteúdo precisa realmente ter uma estrutura predefinida. Seria possível ter seu conteúdo de forma livre, mas isso complicaria *muito* a vida dos aplicativos.

Para o AEM, você, como Arquiteto de conteúdo, executará a modelagem de conteúdo para projetar uma variedade de **Modelos de fragmentos de conteúdo**. Eles definem a estrutura usada quando os autores de conteúdo criam os **Fragmentos de conteúdo** que contêm o conteúdo.

### Acesso ao conteúdo {#access-content}

Isso é mais um detalhe de desenvolvimento, mas pode interessar a você, apenas para completar a história.

Após criar os modelos de fragmento de conteúdo e depois que os(as) autores(as) os tiverem usado para gerar conteúdo, os aplicativos headless precisarão acessar esse conteúdo.

O Adobe Experience Manager (AEM) as a Cloud Service pode acessar seletivamente seus Fragmentos de conteúdo usando a API GraphQL do AEM para retornar somente o conteúdo necessário. Usando a API, um desenvolvedor pode formular consultas que selecionam conteúdo específico. Esse processo de seleção se baseia em *seus* Modelos de fragmentos de conteúdo.

Isso significa que seu projeto pode realizar a entrega headless de conteúdo estruturado para uso em seus aplicativos.

## O que vem a seguir {#whats-next}

Agora que você aprendeu os conceitos e a terminologia, o próximo passo é [Saber mais sobre as noções básicas de modelagem com Modelos de fragmentos de conteúdo](basics.md).

## Recursos adicionais {#additional-resources}

* Jornada do desenvolvedor AEM headless
   * [Saiba mais sobre o desenvolvimento headless do CMS](/help/journey-headless/developer/learn-about.md)
   * [Saiba como modelar seu conteúdo](/help/journey-headless/developer/model-your-content.md)

* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)

* [Portal do desenvolvedor de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)

* [Tutorials para headless no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR)
