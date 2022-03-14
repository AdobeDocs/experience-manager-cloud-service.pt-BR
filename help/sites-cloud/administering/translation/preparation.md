---
title: Preparação de conteúdo para tradução
description: Saiba como preparar conteúdo para tradução.
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Preparação de conteúdo para tradução {#preparing-content-for-translation}

Sites multilíngues geralmente fornecem alguma quantidade de conteúdo em vários idiomas. O site é criado em um idioma e depois traduzido para outros idiomas. Geralmente, sites multilíngues consistem em ramificações de páginas, onde cada ramificação contém as páginas do site em um idioma diferente.

>[!TIP]
>
>Se você é novo em traduzir conteúdo, consulte nosso [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência de AEM ou tradução.

O [Site de tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) O inclui várias ramificações de idioma e usa a seguinte estrutura:

```text
/content
    |- wknd
        |- language-masters
            |- en
            |- de
            |- es
            |- fr
            |- it
        |- us
            |- en
            |- es
        |- ca
            |- en
            |- fr
        |- ch
            |- de
            |- fr
            |- it
        |- de
            |- de
        |- fr
            |- fr
        |- es
            |- es
        |- it
            |- it
```

A cópia de idioma para a qual você criou originalmente o conteúdo do site é o idioma principal. O idioma principal é a fonte traduzida para outros idiomas.

Cada ramificação de idioma de um site é chamada de cópia de idioma. A página raiz de uma cópia de idioma, conhecida como raiz de idioma, identifica o idioma do conteúdo na cópia de idioma. Por exemplo, `/content/wknd/fr` é a raiz do idioma para a cópia em francês. As cópias de idioma devem usar um [raiz de idioma configurada corretamente](preparation.md#creating-a-language-root) para que o idioma correto seja direcionado quando as traduções de um site de origem forem executadas.

Use as seguintes etapas para preparar seu site para tradução:

1. Crie a raiz do idioma do principal. Por exemplo, a raiz do idioma do site de demonstração WKND em inglês é `/content/wknd/language-masters/en`. Verifique se a raiz do idioma está configurada corretamente de acordo com as informações em [Criar uma raiz de idioma](preparation.md#creating-a-language-root).
1. Crie o conteúdo do seu idioma principal.
1. Crie a raiz de idioma de cada cópia de idioma para o site. Por exemplo, a cópia em francês do site de amostra WKND é `/content/wknd/language-masters/fr`.

Depois de preparar o conteúdo para tradução, você pode criar automaticamente as páginas ausentes em suas cópias de idioma e projetos de tradução associados. (Consulte [Criação de um projeto de tradução](managing-projects.md).) Para obter uma visão geral do processo de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

## Criar uma raiz de idioma {#creating-a-language-root}

Crie uma raiz de idioma como a página raiz de uma cópia de idioma que identifica o idioma do conteúdo. Depois de criar a raiz do idioma, você pode criar projetos de tradução que incluem a cópia de idioma.

Para criar a raiz de idioma, crie uma página e use um código de idioma ISO como o valor da variável **Nome** propriedade. O código de idioma deve estar em um dos seguintes formatos:

* `<language-code>` - O código de idioma suportado é um código de duas letras, conforme definido pela ISO-639-1, por exemplo `en`.
* `<language-code>_<country-code>` ou `<language-code>-<country-code>` - O código do país suportado é um código de duas letras em letras minúsculas ou maiúsculas, conforme definido pela norma ISO 3166, por exemplo `en_US`, `en_us`, `en_GB`, `en-gb`.

Você pode usar qualquer um dos formatos, de acordo com a estrutura escolhida para o site global.  Por exemplo, a página raiz da cópia em francês do site WKND tem `fr` como **Nome** propriedade. Observe que a variável **Nome** é usada como o nome do nó da página no repositório e, portanto, determina o caminho da página (`http://<host>:<4502>/content/wknd/language-masters/fr.html`).

1. Navegue até sites.
1. Clique ou toque no site para o qual deseja criar uma cópia de idioma.
1. Clique ou toque em **Criar** e, em seguida, clique ou toque em **Página**.

   ![Criar página](../assets/create-page.png)

1. Selecione o modelo de página e clique ou toque em **Próximo**.
1. No **Nome** digite o código do país no formato de `<language-code>` ou `<language-code>_<country-code>`, por exemplo `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Digite um título para a página.

   ![Criar página raiz do idioma](../assets/create-language-root.png)

1. Clique ou toque em **Criar**. Na caixa de diálogo de confirmação, clique ou toque em **Concluído** para retornar ao console Sites ou **Abrir** para abrir a cópia de idioma.

## Ver o status das raízes das línguas {#seeing-the-status-of-language-roots}

AEM fornece uma **Referências** que mostra uma lista de raízes de idioma que foram criadas.

![Raízes linguísticas](../assets/language-roots.png)

Use o procedimento a seguir para exibir as cópias de idioma de uma página usando o [seletor de painéis.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

1. No console Sites, selecione uma página do site e clique ou toque em **Referências**.

   ![Abrir painel de referências](../assets/opening-references-rail.png)

1. No painel de referências, clique ou toque em **Cópias de idioma**. O painel mostra as cópias de idioma do site.

## Cópias de idioma em vários níveis {#multiple-levels}

As raízes de idioma também podem ser agrupadas em nós, por exemplo, por região, enquanto ainda são reconhecidas como raízes de cópias de idioma.

```text
/content
    |- wknd
        |- language-masters
            |- europe
                |- de
                |- fr
                |- it
                |- es
                ]- pt
            |- americas
                |- en
                |- es
                |- fr
                |- pt
            |- asia
                |- ...
            |- africa
                |- ...
            |- oceania
                |- ...
        |- europe
        |- americas
        |- asia
        |- africa
        |- oceania            
```

>[!NOTE]
>
>Somente um nível é permitido. Por exemplo, o seguinte não permitirá a variável `es` página para resolver para uma cópia de idioma:
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> Essa `es` a cópia de idioma não será detectada, pois tem dois níveis (`americas/central-america`) longe da `en` nó .

>[!TIP]
>
>Nessa configuração, as raízes de idioma podem ter qualquer nome de página, em vez de apenas o código ISO do idioma. AEM sempre verificará o caminho e o nome primeiro, mas se o nome da página não identificar um idioma, AEM verificará o `cq:language` propriedade da página para a identificação do idioma.
