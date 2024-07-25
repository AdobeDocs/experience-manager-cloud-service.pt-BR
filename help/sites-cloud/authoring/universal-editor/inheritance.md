---
title: Herança de conteúdo no editor universal
description: Saiba como o Editor universal oferece suporte à herança de conteúdo para o Gerenciamento de vários sites e Inicializações para oferecer suporte à reutilização e localização de conteúdo.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---


# Herança de conteúdo no editor universal {#inheritance}

Saiba como o Editor universal oferece suporte à herança de conteúdo para o Gerenciamento de vários sites e Inicializações para oferecer suporte à reutilização e localização de conteúdo.

## Caso de uso {#use-case}

Para muitos usuários do AEM, criar uma página é apenas o começo. Para dimensionar o conteúdo de maneira eficaz, as seguintes etapas normalmente são envolvidas após a criação da página:

1. **Traduza a página** usando cópias de idioma e fluxos de trabalho de tradução.
1. **Localize a página** usando o Gerenciamento de Vários Sites para implantar a página traduzida em diferentes mercados.
1. **Crie novas versões** usando Inicializações para preparar iterações futuras da página e ativando essas alterações.

Essas etapas podem acelerar a velocidade do conteúdo e garantir a consistência do conteúdo. O Editor universal oferece suporte à herança de conteúdo, que é o mecanismo no qual essas etapas se baseiam.

## Herança {#what-is-inheritance}

Herança é o mecanismo no qual o conteúdo pode ser vinculado de modo que a alteração de um altere automaticamente o outro. Componentes herdados podem ser o resultado de vários cenários, incluindo:

* [Gerenciamento de vários sites (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md)

O MSM e o Launches são ferramentas eficientes para ajudar você a reutilizar o conteúdo. As páginas podem ser copiadas de uma fonte central (o blueprint) para permitir que os autores façam alterações específicas no contexto dessas cópias, enquanto o restante do conteúdo permanece herdado do blueprint. Isso é extremamente útil ao localizar sites.

Para modificar algum conteúdo das cópias, os autores interrompem a herança nos componentes afetados para garantir que suas alterações locais não sejam substituídas quando as cópias forem sincronizadas do blueprint.

## Herança de conteúdo e o editor universal {#universal-editor}

Quando uma página faz parte do MSM ou de uma Inicialização e o conteúdo é editado com o Editor universal, o editor desativa automaticamente a herança de todas as alterações feitas pelos autores nessa página, garantindo que o conteúdo modificado seja retido quando as atualizações forem sincronizadas do blueprint.

O autor não precisa clicar em um botão ou executar outras etapas para desativar a herança antes de fazer edições locais. Assim que uma alteração é feita, a herança é cancelada implicitamente. Isso contrasta com o [Editor de páginas.](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)

## Limitações {#limitations}

* Os autores não podem reverter a herança de componentes únicos.
   * A herança só pode ser revertida para toda a página através do [Console de Visão Geral da Live Copy](/help/sites-cloud/administering/msm/live-copy-overview.md) ou do [Console de Inicializações](/help/sites-cloud/authoring/launches/overview.md#the-launches-console).
* Os autores não têm feedback visual para ver quais componentes têm sua herança desabilitada e quais ainda a têm preservada.
* No momento, esses recursos estão limitados a componentes em páginas e ainda não se aplicam a [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md), apesar de também terem recursos do MSM e do Launch.
