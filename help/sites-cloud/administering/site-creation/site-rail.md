---
title: Usar o painel do site para gerenciar o tema do site
description: Conheça os recursos avançados do painel Site para ajudá-lo a personalizar e gerenciar facilmente o tema do site.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Usar o painel do site para gerenciar o tema do site {#site-rail}

Conheça os recursos avançados do painel Site para ajudá-lo a personalizar e gerenciar facilmente o tema do site.

## Visão geral {#overview}

O painel Site permite gerenciar os recursos de tema e modelo do site. [Como outros trilhos](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) como os painéis Árvore de conteúdo, Referências ou Linha do tempo, o painel Site é exibido como o painel mais à esquerda no console Sites, exibindo informações sobre o item selecionado. Ao contrário de outros trilhos, o painel Site se aplica somente às raízes do Site.

O painel Site é usado para gerenciar informações relacionadas ao tema e ao modelo para seu site, incluindo:

* [Download de fontes de tema](#downloading-theme-sources)
* [Download de recursos de modelo, como wireframes](#downloading-template-resources)
* [Exibir e alterar versões de temas](#theme-vrsions)
* [Ativação do pipeline de front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Revise o [Jornada Rápida de Criação de Site](/help/journey-sites/quick-site/overview.md) para se familiarizar com a ferramenta de Criação rápida de sites e o pipeline front-end para personalizar facilmente o tema do site.

##  Download de Fontes de Tema {#downloading-theme-sources}

Ao criar um site no AEM com base em um [modelo de site,](site-templates.md) você pode baixar a [tema do site](site-themes.md) usando o painel Site .

Com o painel Site exibido no console Sites , selecione a raiz do site para revelar informações de tema sobre o site.

![Baixar fontes de tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque ou clique **Baixar Fontes de Tema** para baixar uma cópia local do tema do site como `.zip` para fins de personalização.

##  Fazendo download de recursos do modelo {#downloading-template-resources}

[Modelos de site](site-templates.md) pode conter informações além da estrutura de conteúdo do site e [tema do site.](site-themes.md) Os modelos de site podem conter designs de wireframe ou outros arquivos relacionados ao site, por exemplo.

Se o site for baseado em um modelo de site, com o painel Site exibido no console Sites, selecione a raiz do site para revelar informações de tema sobre o site, incluindo recursos adicionais do site.

![Baixar fontes de tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque ou clique no botão ou nos botões abaixo do cabeçalho **Baixar recursos de modelo adicionais** para baixar uma cópia local dos arquivos disponíveis.

## Exibindo e Alterando Versões do Tema {#them-versions}

Se seu site se baseia em um modelo de site, é possível que seu tema já tenha sido personalizado por seu desenvolvedor de front-end. Usando o painel Site , você pode visualizar qual versão do tema do site está implantada no momento e alternar para versões anteriores.

Com o painel Site exibido no console Sites , selecione a raiz do site para revelar informações de tema sobre o site.

![Versões do site no painel](/help/sites-cloud/administering/assets/theme-versions.png)

A versão atual do tema é exibida com seu hash de confirmação junto com o carimbo de data e hora da última atualização.

Toque ou clique em **Selecionar versão** para exibir versões anteriores do tema.

![Selecionar versão do tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Toque ou clique na versão para a qual deseja alterar e toque ou clique em **Aplicar** para fazer a alteração.

Se o AEM detectar que uma versão mais recente do tema foi implantada por meio do pipeline de front-end, mas não aplicada ao site, um ícone de notificação será exibido.

![Nova versão do indicador de tema](/help/sites-cloud/administering/assets/new-theme-version.png)

Você pode usar o **Selecionar versão** botão para atualizar para a nova versão de tema.

## Ativação do pipeline front-end {#enabling-front-end-pipeline}

Se seu site não foi criado usando um modelo de site, não é possível usar o pipeline de front-end para personalizar e implantar seu tema.

No entanto, você pode ativar o pipeline de front-end para seu site usando o painel Site .

Com o painel Site exibido no console Sites, selecione a raiz do site para revelar informações de tema sobre o site e toque ou clique em **Ativar pipeline de front-end**.

![Ativação do pipeline de front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Para obter mais informações, consulte o documento [Ativação do pipeline front-end.](enable-front-end-pipeline.md)
