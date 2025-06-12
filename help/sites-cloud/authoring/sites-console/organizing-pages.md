---
title: Organizar páginas
description: Saiba como organizar seu site com o AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 9a700e9eb3116252f42bb08db9dadc0e8a6adbf7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 67%

---


# Organizar páginas {#creating-and-organizing-pages}

Saiba como organizar seu site com o AEM. Assim que você entender como precisa organizar suas páginas, poderá [criar novas páginas](/help/sites-cloud/authoring/sites-console/creating-pages.md) e [gerenciar páginas existentes](/help/sites-cloud/authoring/sites-console/managing-pages.md).

## Organizar seu site {#organizing-your-site}

Como autor, você precisa organizar seu site no AEM. Isso envolve criar e nomear suas páginas de conteúdo de modo que:

* Você pode encontrá-las facilmente no ambiente de criação
* Os visitantes do seu site possam navegar facilmente por elas no ambiente de publicação

Você também pode usar [pastas](#creating-a-new-folder) para ajudar a organizar o seu conteúdo.

A estrutura de um site pode ser considerada como uma árvore que armazena suas páginas de conteúdo. Os nomes dessas páginas de conteúdo são usadas para formar os URLs, ao passo que os títulos são mostrados quando o conteúdo da página é visualizado.

O exemplo a seguir mostra o site [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR), onde um artigo sobre skateparks (`la-skateparks`) é acessado:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Esta estrutura pode ser visualizada do console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), onde você pode navegar pelas páginas do seu site e executar ações nas páginas.

## Convenções de nomenclatura da página {#page-naming-conventions}

Ao criar uma página, há dois campos principais:

* **[Título](#title)**:
   * O título é exibido ao usuário no console, na parte superior do conteúdo da página ao editar.
   * Esse campo é obrigatório.
* **[Nome](#name)**:
   * Usado para gerar o URI.
   * A entrada do usuário para este campo é opcional. Se não especificado, o nome é derivado do título. Consulte a seguinte seção [Restrições de nome de página e práticas recomendadas](#page-name-restrictions-and-best-practices) para obter detalhes.

### Restrições de nome de página e práticas recomendadas {#page-name-restrictions-and-best-practices}

O **Título** da página e o **Nome** podem ser criados separadamente, mas estão relacionados:

* Ao criar uma página, somente o campo **Título** é obrigatório. Se nenhum **Nome** for fornecido na criação da página, o AEM gerará um nome a partir dos primeiros 64 caracteres do título (observando o conjunto definido abaixo). Somente os primeiros 64 caracteres são usados para seguir a prática recomendada de nomes de página curtos.
* Se um nome de página for especificado manualmente pelo autor, o limite de 64 caracteres não se aplicará. Contudo, outras limitações técnicas no comprimento de nome de página poderão ser aplicadas.

>[!TIP]
>
>Ao definir um nome de página, um princípio básico é manter o nome da página curto, mas tão expressivo e memorável quanto possível para facilitar a compreensão do leitor. Consulte o [guia de estilo W3C](https://www.w3.org/Provider/Style/TITLE.html) no elemento `title`para obter mais informações.
>
>Lembre-se também de que alguns navegadores (por exemplo, versões mais antigas do IE) só podem aceitar URLs com um limite de comprimento, por isso também há um motivo técnico para manter os nomes de página curtos.

Ao criar uma página, o AEM [valida o nome da página de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostas pelo AEM e JCR.

Os caracteres mínimos permitidos são:

* `a` a `z`
* `A` a `Z`
* `0` a `9`
* `_` (sublinhado)
* `-` (hífen/sinal de menos)

Detalhes completos sobre todos os caracteres permitidos podem ser encontrados nas [convenções de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Os nomes de página são limitados a 150 caracteres.

### Título {#title}

Se você fornecer apenas uma página **Título** ao criar uma página, a AEM derivará a página **Nome** desta cadeia de caracteres e [validará o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostas pelo AEM e JCR.

Um campo de **Título** contendo caracteres inválidos é aceito, mas o nome derivado terá os caracteres inválidos substituídos. Por exemplo:

| Título | Nome derivado |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### Nome {#name}

Quando você fornece uma página **Nome** ao criar uma página, o AEM [valida o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostas pelo AEM e JCR. Não é possível inserir caracteres inválidos no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é destacado com uma mensagem explicativa.

![Exemplo de inserção de um nome de página inválido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Evite usar um código de duas letras, conforme definido por ISO-639-1 como um nome de página, a menos que seja uma raiz de idioma.
>
>Consulte [Preparação de conteúdo para tradução](/help/sites-cloud/administering/translation/preparation.md) para obter mais informações.

## Modelos {#templates}

No AEM, um [modelo](/help/sites-cloud/authoring/page-editor/templates.md) é um tipo especializado de página usado como base para qualquer nova página que está sendo criada.

O modelo define a estrutura de uma página, incluindo uma imagem em miniatura e outras propriedades. Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de site e informações de contato. Os modelos são compostos de [componentes](#components).

O AEM vem com vários modelos prontos para uso. Os modelos disponíveis dependem do site individual. Os campos principais são:

* **Título** - O título exibido na página da Web resultante
* **Nome** - Usado ao nomear a página
* **Modelo** - Uma lista de modelos disponíveis para uso ao gerar a nova página

## Componentes {#components}

[Componentes](/help/implementing/developing/components/overview.md) são os elementos fornecidos pelo AEM para que você possa adicionar tipos específicos de conteúdo. O AEM vem com vários componentes prontos para uso, chamados [de Componentes principais](/help/implementing/developing/components/overview.md#core-components), que fornecem funcionalidade abrangente. Alguns exemplos dos componentes são:

* Texto
* Imagem
* Título
* Carrossel
* E muito mais

Depois de criar e abrir uma página, é possível [adicionar conteúdo usando os componentes](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component), que estão disponíveis no [navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>O console [Componentes](/help/sites-cloud/authoring/components-console.md) fornece uma visão geral dos componentes na instância.
