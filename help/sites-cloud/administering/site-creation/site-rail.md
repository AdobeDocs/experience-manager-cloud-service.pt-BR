---
title: Usar o painel Site para gerenciar o tema do site
description: Conheça os recursos avançados do painel Site para ajudá-lo a personalizar e gerenciar facilmente o tema do site.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 95%

---

# Usar o painel Site para gerenciar o tema do site {#site-rail}

Conheça os recursos avançados do painel Site para ajudá-lo a personalizar e gerenciar facilmente o tema do site.

## Visão geral {#overview}

O painel Site permite gerenciar os recursos de tema e modelo do site. [Assim como os painéis](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) Árvore de conteúdo, Referências ou Linha do tempo, o painel Site é exibido mais à esquerda do console de sites, exibindo informações sobre o item selecionado. Ao contrário de outros painéis, o painel Site se aplica somente às raízes do Site.

O painel Site é usado para gerenciar informações relacionadas ao tema e ao modelo do site, incluindo:

* [Baixar fontes de tema](#downloading-theme-sources)
* [Baixar recursos de modelo, como wireframes](#downloading-template-resources)
* [Exibição e alteração de versões de temas](#theme-vrsions)
* [Ativação do pipeline front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Revise a [Jornada de criação rápida de sites](/help/journey-sites/quick-site/overview.md) e familiarize-se com a ferramenta de criação rápida de sites e com o pipeline front-end para personalizar facilmente o tema do site.

## Baixar fontes de tema {#downloading-theme-sources}

Ao criar um site no AEM com base em um [modelo de site,](site-templates.md) você pode baixar o [tema do site](site-themes.md) usando o painel Site.

Com o painel Site sendo exibido no console de sites, selecione a raiz do site para revelar informações de tema sobre ele.

![Baixar fontes de tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque ou clique em **Baixar fontes de tema** para fazer o download de uma cópia local do tema do site no formato `.zip` para fins de personalização.

## Baixar recursos do modelo {#downloading-template-resources}

[Modelos de site](site-templates.md) podem conter informações que vão além da estrutura de conteúdo do site e do [tema do site.](site-themes.md) Por exemplo, os modelos de site podem conter designs de wireframe ou outros arquivos relacionados ao site.

Se o site for baseado em um modelo de site, com o painel Site sendo exibido no console de sites, selecione a raiz do site para revelar informações de tema sobre ele, incluindo recursos adicionais.

![Baixar fontes de tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque ou clique no botão ou nos botões abaixo do cabeçalho **Baixar recursos de modelo adicionais** para fazer download de uma cópia local dos arquivos disponíveis.

## Exibir e alterar versões do tema {#them-versions}

Se o site se baseia em um modelo de site, é possível que o tema dele já tenha sido personalizado pelo desenvolvedor de front-end. Usando o painel Site, é possível visualizar qual versão do tema do site está implantada no momento e alternar para versões anteriores.

Com o painel Site sendo exibido no console de sites, selecione a raiz do site para revelar informações de tema sobre ele.

![Versões do site no painel](/help/sites-cloud/administering/assets/theme-versions.png)

A versão atual do tema é exibida com seu hash de confirmação junto com o carimbo de data e hora da última atualização.

Toque ou clique **Selecionar versão** para exibir versões anteriores do tema.

![Selecionar versão do tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Toque ou clique na versão para a qual deseja alterar e, em seguida, em **Aplicar** para fazer a alteração.

Se o AEM detectar que uma versão mais recente do tema foi implantada por meio do pipeline de front-end, mas não aplicada ao site, um ícone de notificação será exibido.

![Nova versão do indicador de tema](/help/sites-cloud/administering/assets/new-theme-version.png)

É possível usar o botão **Selecionar versão** para atualizar para a nova versão do tema.

## Ativação do pipeline de front-end {#enabling-front-end-pipeline}

Se o site não foi criado usando um modelo de site, não é possível usar o pipeline de front-end para personalizar e implantar seu tema.

No entanto, você pode ativar o pipeline de front-end para o site usando o painel Site.

Com o painel Site sendo exibido no console de sites, selecione a raiz do site para revelar informações de tema sobre ele e toque ou clique em **Ativar pipeline de front-end**.

![Ativação do pipeline de front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Para obter mais informações, consulte o documento [Ativação do pipeline de front-end.](enable-front-end-pipeline.md)
