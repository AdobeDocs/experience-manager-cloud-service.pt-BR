---
title: Temas do site
description: Saiba como AEM temas do site podem ser usados para personalizar o estilo e o design do site.
feature: Administering
role: Admin
source-git-commit: 0b00d579886a106f5f66cfc54d90eab9563724cd
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---


# Temas do site {#site-themes}

Saiba como AEM temas do site podem ser usados para personalizar o estilo e o design do site.

## Visão geral {#overview}

Um tema de site AEM é um pacote que contém o CSS, o JavaScript e os recursos estáticos que definem o estilo do site AEM e estão em conformidade com a estrutura de um tema de site AEM.

Os sites criados com modelos de site AEM permitem fácil download, personalização e reimplantação dos temas.

>[!NOTE]
>
>AEM temas do site não devem ser confundidos com [AEM modelos de site.](site-templates.md) AEM temas do site contêm apenas as informações de estilo de um site AEM. AEM modelos de site definem a estrutura do site e o conteúdo inicial, bem como contêm um tema de site AEM para permitir [criação rápida do site.](create-site.md)

## Utilização de Temas do Site {#using-themes}

Os temas do site são usados de duas maneiras diferentes:

* Eles são usados como parte de um modelo de site para definir o estilo ao [criação de um site.](create-site.md)
* Eles são baixados depois de criar um site com base em um modelo de site, para que um desenvolvedor de front-end possa personalizar ainda mais o estilo.

>[!TIP]
>
>Uma descrição completa do processo de criação de um site a partir de um modelo e personalização de seu tema pode ser encontrada no [Jornada Rápida de Criação de Site.](/help/journey-sites/quick-site/overview.md)

## Estrutura de Tema do Site {#structure}

Os temas do site são simplesmente pacotes com uma estrutura lógica que reflete claramente a finalidade do conteúdo do pacote. Um tema de site tem a seguinte estrutura típica de um projeto front-end.

* `src/main.ts`: O principal ponto de entrada do seu tema JS &amp; CSS
* `src/site`: Arquivos JS e CSS que se aplicam a todo o site
* `src/components`: Arquivos JS e CSS específicos para componentes AEM
* `src/resources`: Arquivos estáticos como ícones, logotipos e fontes

## Tema do Site Padrão {#standard-site-theme}

O Adobe fornece um tema de referência de práticas recomendadas que pode ser usado como base para a criação de seu próprio tema. [O Tema do site padrão está disponível no GitHub.](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## Desenvolver temas do site {#developing-themes}

O Adobe fornece um AEM Criador de Temas do Site como um conjunto de scripts para criar novos temas do site.

[O AEM Site Theme Builder está disponível junto com a documentação de uso no GitHub.](https://github.com/adobe/aem-site-theme-builder) É necessária experiência de desenvolvimento front-end para personalizar o tema.
