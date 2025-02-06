---
title: Habilitar o pipeline de front-end
description: Saiba como você pode ativar o pipeline de front-end para sites existentes a fim de usar temas de site para personalizar seu site mais rapidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 35%

---

# Habilitar o pipeline de front-end {#enable-front-end-pipeline}

Saiba como você pode ativar o pipeline de front-end para sites existentes a fim de usar temas de site para personalizar seu site mais rapidamente.

## Visão geral {#overview}

O pipeline de front-end é um mecanismo que pode implantar rapidamente apenas o código front-end de seus sites, com base em [temas de site](site-themes.md) e [modelos de site](site-templates.md).

Esse pipeline lida somente com o código front-end, tornando o processo de implantação mais rápido do que as implantações de pilha completa. Ele permite que desenvolvedores de front-end personalizem seu site facilmente sem precisar de conhecimento sobre AEM.

Sites baseados em modelos de site podem usar o pipeline de front-end por padrão. Este documento descreve como você pode adaptar seus sites existentes para aproveitar o pipeline de front-end.

>[!TIP]
>
>Se você não estiver familiarizado com o pipeline de front-end e não souber como implantar sites rapidamente usando ele e os modelos de site, consulte a [Jornada de Criação Rápida de Sites](/help/journey-sites/quick-site/overview.md) para obter uma introdução.

O AEM pode configurar seu site para carregar temas implantados com o pipeline de front-end, mesmo que ele não tenha sido criado usando modelos de site e temas, colocando-os em cima das bibliotecas de clientes existentes.

## Detalhes técnicos {#technical-details}

Quando você ativa o pipeline de front-end para um site, o AEM faz as seguintes alterações na estrutura do site.

* Todas as páginas do site incluem um arquivo CSS e JS adicional, que pode ser modificado ao implantar atualizações por meio de um pipeline de front-end dedicado do Cloud Manager.
* Os arquivos CSS e JS adicionados estão inicialmente vazios. No entanto, você pode baixar uma pasta de &quot;fontes de tema&quot; para configurar a estrutura de pastas necessária para implantar atualizações de código CSS e JS por meio do pipeline.
* Somente um desenvolvedor pode desfazer a alteração, excluindo os nós `SiteConfig` e `HtmlPageItemsConfig` que esta operação cria abaixo de `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Essa ação não converte automaticamente as bibliotecas de clientes existentes do site para usar o pipeline de front-end. Mover essas fontes da pasta da biblioteca do cliente para a pasta do pipeline de front-end é uma tarefa que requer o trabalho manual de um desenvolvedor front-end.

## Requisitos {#requirements}

O AEM pode adaptar automaticamente seu site existente para usar o pipeline de front-end. Para fazer esse fluxo de trabalho, seu site deve usar [v2 ou mais recente do Componente de Página dos Componentes Principais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page).

## Ativação do pipeline de front-end {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

A habilitação do site é feita pelo console de Sites, usando o [painel Site](site-rail.md).

1. Faça logon no AEM e navegue até o site através de **Navegação global** > **Sites**.
1. Selecione seu site no console. Selecione a raiz do site e não qualquer página secundária.
1. Com seu site selecionado, abra o [seletor de painéis](/help/sites-cloud/authoring/basic-handling.md#rail-selector) à esquerda e escolha **Site**.
1. No painel **Site**, clique no botão **Ativar pipeline de front-end**.

   ![Ativar pipeline de front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. O AEM solicita sua confirmação com uma visão geral das alterações feitas. Confirme e o site estará adaptado.

Agora, seu site está pronto para usar o pipeline de front-end. Para saber mais sobre o pipeline de front-end e gerenciar o tema do site, consulte:

* [Usar o painel Site para gerenciar o tema do site](site-rail.md)
* [Jornada de criação rápida de sites](/help/journey-sites/quick-site/overview.md) - esta jornada de documentação fornece a você uma visão geral do processo de implantação rápida de um site usando o pipeline de front-end e a ferramenta Criação rápida de site.
* [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - este documento descreve o pipeline de front-end no contexto dos pipelines de nível de pilha completa e Web.

## Pipeline de front-end e domínios personalizados {#custom-domains}

Conforme descrito na seção [Detalhes Técnicos](#technical-details), ativar o recurso de Pipeline de Front-End para um site cria um `SiteConfig` e `HtmlPageItemsConfig` nós abaixo de `/conf/<site-name>/sling:configs`.

Se você quiser usar o [recurso de domínios personalizados do Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/introduction.md) para o seu site junto com o Pipeline de Front-End, será necessário adicionar outras propriedades a esses nós.

1. Defina a propriedade `customFrontendPrefix` em `SiteConfig` para o site.
1. Isso atualiza o valor `prefixPath` de `HtmlPageItemsConfig` com o domínio personalizado.

As páginas para o site fazem referência a artefatos de tema desse URL atualizado.
