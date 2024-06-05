---
title: Habilitar o pipeline de front-end
description: Saiba como habilitar o pipeline de front-end para que os sites existentes usem temas de site para uma personalização mais rápida.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 98%

---

# Habilitar o pipeline de front-end {#enable-front-end-pipeline}

Saiba como habilitar o pipeline de front-end para que os sites existentes usem temas de site para uma personalização mais rápida.

## Visão geral {#overview}

O pipeline de front-end é um mecanismo que pode implantar rapidamente apenas o código front-end de seus sites, com base em [temas de site](site-themes.md) e [modelos de site.](site-templates.md)

Em vez de implantar a pilha completa, somente o código front-end é manipulado por esse pipeline, agilizando o processo e permitindo que os desenvolvedores de front-end personalizem seu site de maneira fácil e rápida, sem necessidade de ter conhecimento sobre o AEM.

Sites baseados em modelos de site podem usar o pipeline de front-end por padrão. Este documento descreve como você pode adaptar seus sites existentes para aproveitar o pipeline de front-end.

>[!TIP]
>
>Se não conhece o funcionamento do pipeline de front-end e como implantar sites rapidamente usando esse pipeline e os modelos de site, consulte [Jornada de criação rápida de sites](/help/journey-sites/quick-site/overview.md) para obter uma introdução.

Se você não tiver criado o site existente com base em modelos de site e temas, o AEM poderá configurar o site para carregar os temas que são implantados com o pipeline de front-end sobre as bibliotecas de clientes existentes.

## Detalhes técnicos {#technical-details}

Quando você ativa o pipeline de front-end para um site, o AEM faz as seguintes alterações na estrutura do site.

* Todas as páginas do site incluirão um arquivo CSS e JS adicional, que pode ser modificado ao implantar atualizações por meio de um pipeline de front-end dedicado do Cloud Manager.
* Os arquivos CSS e JS adicionados estarão inicialmente vazios, mas uma pasta de “fontes de temas” pode ser baixada para inicializar a estrutura da pasta que permite implantar atualizações de código CSS e JS por meio desse pipeline.
* Essa alteração só pode ser desfeita por um desenvolvedor, excluindo os nós `SiteConfig` e `HtmlPageItemsConfig` que esta operação cria abaixo de `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Essa ação não converterá automaticamente as bibliotecas de clientes existentes do site para usar o pipeline de front-end. Mover essas fontes da pasta da biblioteca do cliente para a pasta do pipeline de front-end é uma tarefa que requer o trabalho manual de um desenvolvedor front-end.

## Requisitos {#requirements}

O AEM pode adaptar automaticamente seu site existente para usar o pipeline de front-end. Para fazer isso, seu site deve usar a [versão v2 ou mais recente do Componente de página dos Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html?lang=pt-BR)

## Ativação do pipeline de front-end {#enabling}

A ativação do site é feita pelo console de sites, usando o [painel Site.](site-rail.md)

1. Faça logon no AEM e navegue até o site através de **Navegação global** > **Sites**.
1. Selecione seu site no console. Selecione a raiz do site e não qualquer página secundária.
1. Com seu site selecionado, abra o [seletor de painéis](/help/sites-cloud/authoring/basic-handling.md#rail-selector) à esquerda e escolha **Site**.
1. No painel **Site**, clique no botão **Ativar pipeline de front-end**.

   ![Ativar pipeline de front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. O AEM solicita sua confirmação com uma visão geral das alterações que serão feitas. Confirme e o site estará adaptado.

Agora, seu site está pronto para usar o pipeline de front-end. Para saber mais sobre o pipeline de front-end e gerenciar o tema do site, consulte:

* [Usar o painel Site para gerenciar o tema do site](site-rail.md)
* [Jornada de criação rápida de sites](/help/journey-sites/quick-site/overview.md) - esta jornada de documentação fornece a você uma visão geral do processo de implantação rápida de um site usando o pipeline de front-end e a ferramenta Criação rápida de site.
* [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - este documento descreve o pipeline de front-end no contexto dos pipelines de nível de pilha completa e Web.
