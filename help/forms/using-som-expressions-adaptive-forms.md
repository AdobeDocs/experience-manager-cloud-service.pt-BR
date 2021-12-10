---
title: Uso de expressões SOM no Adaptive Forms
seo-title: Using SOM expressions in Adaptive Forms
description: Saiba como extrair expressões SOM de um painel de um formulário adaptável.
seo-description: Learn how to extract SOM expressions of a panel of an Adaptive Form.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Uso de expressões SOM no Adaptive Forms{#using-som-expressions-in-adaptive-forms}

Os Forms adaptáveis são modelados como Página AEM, que é representada como estrutura de conteúdo JCR em AEM repositório. O elemento principal da estrutura de conteúdo é o nó guideContainer . Abaixo guideContainer, há um rootPanel que pode conter campos e painel aninhados.

Você pode usar um SOM (Modelo de objeto de script) para fazer referência a valores, propriedades e métodos em um DOM (Modelo de objeto de documento) específico. Um DOM organiza os objetos e as propriedades da memória em uma hierarquia de árvore. Uma expressão SOM faz referência a elementos e painéis Campos/Desenhar .

A imagem a seguir descreve uma estrutura de nó para a qual um Formulário adaptável é convertido ao adicionar componentes a um formulário. Por exemplo, você pode adicionar um painel ao painel raiz e um botão de opção no painel que é transformado em DOM no tempo de execução. A expressão SOM do campo de botão de opção no Formulário adaptável é especificada como `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Árvore DOM](assets/hierarchy.png)

Árvore DOM

Uma expressão SOM para qualquer elemento em um Formulário adaptável tem o prefixo `guide[0].guide1[0]`. A posição de um componente na hierarquia da estrutura do nó é usada para derivar sua expressão SOM.

![Árvore DOM com dois botões de opção](assets/hierarchy_radio_button.png)

Árvore DOM com dois botões de opção

A expressão SOM muda quando você altera a posição dos botões de opção no Formulário adaptável. No modo de criação, você pode exibir a expressão SOM de um campo ou elemento dentro de [!DNL AEM Forms] usando a opção Exibir expressão SOM . A opção é exibida no painel e quando você clica com o botão direito do mouse no campo ou elemento.

![Extraindo expressões SOM em um formulário adaptável](assets/som-expressions.png)

Extraindo expressões SOM em um formulário adaptável

Em painéis, você pode acessar o recurso na barra de ferramentas do painel. O recurso facilita os scripts de autores do formulário adaptativo.

![Extraindo expressões SOM usando a barra de ferramentas do painel](assets/som-expression.png)

Extraindo expressões SOM usando a barra de ferramentas do painel

Algumas APIs listadas em [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) use a expressão SOM de um elemento. Por exemplo, para trazer o foco para um campo específico em um Formulário adaptável, passe a expressão SOM correspondente para a variável `getFocus`API em `guideBridge`.
