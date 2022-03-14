---
title: Ativação do pipeline front-end
description: Saiba como você pode ativar o pipeline de front-end para sites existentes para aproveitar os temas do site para personalizar seu site mais rapidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Ativação do pipeline front-end {#enable-front-end-pipeline}

Saiba como você pode ativar o pipeline de front-end para sites existentes para aproveitar os temas do site para personalizar seu site mais rapidamente.

## Visão geral {#overview}

O pipeline front-end é um mecanismo que pode implantar rapidamente apenas o código front-end de seus sites, com base em [temas do site](site-themes.md) e [modelos de site.](site-templates.md)

Em vez de implantar a pilha completa, somente o código front-end é manipulado por esse pipeline, tornando o processo mais rápido e permitindo que os desenvolvedores de front-end personalizem seu site de forma fácil e rápida, sem conhecimento de AEM.

Sites com base em modelos de site podem aproveitar o pipeline de front-end por padrão. Este documento descreve como você pode adaptar seus sites existentes para aproveitar o pipeline de front-end.

>[!TIP]
>
>Se você não estiver familiarizado com o pipeline de front-end e como implantar sites rapidamente usando ele e modelos de site, revise o [Jornada Rápida de Criação de Site](/help/journey-sites/quick-site/overview.md) para uma introdução.

Se você não tiver criado seu site existente com base em modelos de site e temas, AEM poderá configurar seu site para carregar os temas que são implantados com o pipeline de front-end sobre as bibliotecas de clientes existentes.

## Detalhes técnicos {#technical-details}

Quando você ativa o pipeline de front-end para um site, o AEM faz as seguintes alterações na estrutura do site.

* Todas as páginas do site incluirão um arquivo CSS e JS adicional, que pode ser modificado ao implantar atualizações por meio de um pipeline front-end dedicado do Cloud Manager.
* Os arquivos CSS e JS adicionados estarão inicialmente vazios, mas uma pasta de &quot;fontes de temas&quot; pode ser baixada para inicializar a estrutura da pasta que permite implantar atualizações de código CSS e JS por meio desse pipeline.
* Essa alteração só pode ser desfeita por um desenvolvedor, excluindo o `SiteConfig` e `HtmlPageItemsConfig` nós que esta operação cria abaixo `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Essa ação não converterá automaticamente as bibliotecas de clientes existentes do site para usar o pipeline de fonte final. Mover essas fontes da pasta da biblioteca do cliente para a pasta de pipeline front-end é uma tarefa que requer trabalho manual de um desenvolvedor front-end.

## Requisitos {#requirements}

AEM pode adaptar automaticamente seu site existente para usar o pipeline de front-end. Para fazer isso, seu site deve usar [v2 ou mais recente do Componente de página dos Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Ativação do pipeline front-end {#enabling}

A ativação do site é feita pelo console Sites usando o [Painel do site.](site-rail.md)

1. Faça logon no AEM e navegue até seu site via **Navegação global** > **Sites**.
1. Selecione seu site no console. Você deve selecionar a raiz do site e não qualquer página secundária.
1. Com seu site selecionado, abra o [seletor de painéis](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) à esquerda e escolha **Site**.
1. No **Site** , clique no botão **Ativar pipeline de front-end**.

   ![Ativar pipeline de front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM solicita que você confirme com uma visão geral das alterações que serão feitas. Confirme se o site está adaptado.

Agora, seu site está pronto para usar o pipeline de front-end. Para saber mais sobre o pipeline de front-end e gerenciar o tema do site, consulte:

* [Usar o painel do site para gerenciar o tema do site](site-rail.md)
* [Jornada Rápida de Criação de Site](/help/journey-sites/quick-site/overview.md) - Esta jornada de documentação fornece a você uma visão geral do processo de implantação rápida de um site usando o pipeline front-end e a ferramenta Criação rápida de site .
* [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - Este documento descreve o pipeline de front-end no contexto dos pipelines de pilha completa e da camada da Web.
