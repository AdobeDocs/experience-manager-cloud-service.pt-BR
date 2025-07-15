---
title: Criação de um site
description: Saiba como usar o AEM para criar um site usando modelos de site para definir o estilo e a estrutura de seu site.
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 4d45e7ef626ad0b46f5323263cca791b14f9732f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 52%

---


# Criação de um site {#creating-site}

Saiba como usar o AEM para criar um site usando modelos de site para definir o estilo e a estrutura de seu site.

## Visão geral {#overview}

Antes que os autores de conteúdo possam criar páginas com conteúdo, o site deve ser criado primeiro. Isso geralmente é feito por um administrador do AEM que define a estrutura inicial do site. Usar modelos de site torna a criação de sites rápida e flexível para não desenvolvedores.

## Planejamento da estrutura do site {#structure}

Reserve tempo para considerar a finalidade do site e o conteúdo planejado com bastante antecedência. Isso conduzirá a maneira como você desenha a estrutura do site. Uma boa estrutura de site permite uma fácil navegação e descoberta de conteúdo pelos visitantes do site, além de oferecer suporte a vários recursos do AEM, como o [gerenciamento multisite e tradução.](/help/sites-cloud/administering/msm-and-translation.md)

## Modelos de site {#site-templates}

Como a estrutura do site é muito importante para o sucesso dele, é conveniente ter estruturas predefinidas disponíveis para implantar rapidamente um novo site com base em um conjunto de padrões existentes. Os modelos de site são uma maneira de combinar conteúdos básicos de sites em um pacote conveniente e reutilizável.

Os modelos de site geralmente contêm o conteúdo básico e a estrutura do site, bem como informações de estilo para iniciar o novo site rapidamente. Esses modelos são bastante eficientes pois podem ser reutilizados e personalizados. E como é possível ter vários modelos disponíveis na sua instância do AEM, você tem a flexibilidade de criar sites diferentes para atender a várias necessidades comerciais.

>[!TIP]
>
>Para obter mais detalhes sobre modelos de site, consulte o documento [Modelos de Site.](site-templates.md)

>[!NOTE]
>
>O modelo de site não deve ser confundido com [modelos de página.](/help/sites-cloud/authoring/page-editor/templates.md) Os modelos de site definem a estrutura geral de um site. Um modelo de página define a estrutura e o conteúdo inicial de uma página individual.

### Modelos de site fornecidos pela Adobe {#adobe-templates}

{{adobe-templates}}

## Criação de um site {#create-site}

É simples usar um modelo para criar um site.

1. Faça logon no ambiente de criação do AEM e navegue até o console de sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Selecione **Criar** no canto superior direito da tela e, no menu suspenso, selecione **Site do modelo**.

   ![Criação de um site a partir de um modelo](../assets/create-site-from-template.png)

1. No assistente Criar Site, selecione um modelo existente no painel esquerdo ou em **Importar** na parte superior da coluna à esquerda para importar um novo modelo.

   ![Assistente de criação de site](../assets/site-creation-wizard.png)

   1. Se você optar por importar, no navegador de arquivos, localize o modelo que deseja usar e selecione **Carregar**.

   1. Depois que o upload for concluído, ele aparece na lista de modelos disponíveis.

1. Ao selecionar um modelo, informações sobre ele são reveladas na coluna da direita. Com o modelo desejado selecionado, selecione **Próximo**.

   ![Selecione um modelo](../assets/select-site-template.png)

1. Forneça um título para o site. É possível fornecer um nome de site ou gerá-lo a partir do título (caso seja omitido).

   * O título do site aparece na barra de título dos navegadores.
   * O nome do site se torna parte do URL.
   * O nome do site deve estar em conformidade com as [convenções de nomenclatura de páginas do AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices).

1. Forneça detalhes adicionais do site, conforme exigido pelo modelo de site.

   * Modelos diferentes podem exigir detalhes adicionais.
   * Por exemplo, modelos para [projetos Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) exigem o repositório GitHub do seu projeto.

1. Selecione **Criar** e o site é criado a partir do modelo de site.

   ![Detalhes do novo site](../assets/create-site-details.png)

1. Na caixa de diálogo de confirmação exibida, selecione **Concluído**.

   ![Caixa de diálogo de sucesso](../assets/success.png)

1. No console do Sites, o novo site é visível e pode ser navegado para explorar sua estrutura básica, conforme definido pelo modelo.

   ![Nova estrutura de site](../assets/new-site.png)

Os autores de conteúdo agora podem começar a criar!

## Personalização do site {#site-customization}

Os modelos são úteis para configurar rapidamente a estrutura básica e o estilo de um site. No entanto, a maioria dos projetos exige estilo e personalização adicionais. Os modelos de site ajudam a dissociar o estilo do site para que os desenvolvedores de front-end não precisem de conhecimento do AEM para estilizar o site e possam
trabalhar separadamente e em paralelo aos criadores de conteúdo. Dependendo do tipo de projeto, isso pode assumir duas formas.

* Para projetos com criação de página do AEM com o Universal Editor e entrega através de [entrega de borda](/help/edge/overview.md), todo o estilo é feito no projeto GitHub.
   * Consulte o documento [Introdução - Tutorial do desenvolvedor do Universal Editor](https://www.aem.live/developer/ue-tutorial) para obter mais informações.
* Para projetos com criação e entrega de página tradicional do AEM por meio de [entrega de publicação](/help/sites-cloud/authoring/author-publish.md), o administrador do AEM simplesmente baixa o tema do site e o fornece ao desenvolvedor front-end, que o personaliza usando suas ferramentas favoritas e, em seguida, confirma as alterações no repositório de código do AEM, que é então implantado.
   * Consulte o documento [Jornada de Criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter mais informações.
