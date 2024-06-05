---
title: Temas do site
description: Saiba como temas de site do AEM podem ser usados para personalizar o estilo e o design do site.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 100%

---

# Temas do site {#site-themes}

Saiba como temas de site do AEM podem ser usados para personalizar o estilo e o design do site.

## Visão geral {#overview}

Um tema de site do AEM é um pacote que contém o CSS, o JavaScript e os recursos estáticos que definem o estilo do seu site do AEM e está em conformidade com a estrutura de um tema de site do AEM.

Os sites criados com modelos de site do AEM permitem fácil download, personalização e reimplantação dos temas.

>[!NOTE]
>
>Os temas de site do AEM não devem ser confundidos com os [modelos de site do AEM](site-templates.md). Os temas de site do AEM contêm apenas as informações de estilo de um site do AEM. Os modelos de site do AEM definem a estrutura e o conteúdo inicial do site e contêm um tema de site do AEM para permitir a [criação rápida de sites](create-site.md).

## Usar temas de site {#using-themes}

Os temas de site são usados de duas maneiras diferentes:

* Eles são usados como parte de um modelo de site para definir o estilo durante a [criação de um site.](create-site.md)
* Eles são baixados depois de criar um site com base em um modelo de site, para que um desenvolvedor de front-end possa personalizar ainda mais o estilo.

>[!TIP]
>
>Uma descrição completa do processo de criação de um site a partir de um modelo e personalização de seu tema pode ser encontrada na [Jornada de criação rápida de sites](/help/journey-sites/quick-site/overview.md).

## Estrutura de tema do site {#structure}

Os temas do site são pacotes com uma estrutura lógica que reflete claramente a finalidade do conteúdo do pacote. Um tema de site tem a seguinte estrutura típica de um projeto de front-end.

* `src/main.ts`: o principal ponto de entrada do seu JavaScript e tema CSS
* `src/site`: arquivos JS e CSS que se aplicam a todo o site
* `src/components`: arquivos JS e CSS específicos para componentes do AEM
* `src/resources`: arquivos estáticos como ícones, logotipos e fontes

## Tema do site padrão {#standard-site-theme}

A Adobe fornece um tema de referência de práticas recomendadas que pode ser usado como base para a criação de seu próprio tema. [O tema de site padrão está disponível no GitHub](https://github.com/adobe/aem-site-template-standard/tree/main/theme).

## Desenvolver temas de site {#developing-themes}

A Adobe fornece um Criador de temas de site do AEM como um conjunto de scripts para criar novos temas de site.

[O Criador de temas de site do AEM está disponível junto com a documentação de uso no GitHub](https://github.com/adobe/aem-site-theme-builder). É necessária experiência em desenvolvimento de front-end para personalizar o tema.
