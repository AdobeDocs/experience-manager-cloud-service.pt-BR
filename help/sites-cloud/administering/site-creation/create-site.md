---
title: Criação de um site
description: Saiba como usar o AEM para criar um site usando modelos de site para definir o estilo e a estrutura de seu site.
feature: Administering
role: Admin
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---


# Criação de um site {#creating-site}

Saiba como usar AEM criar um site usando modelos de site para definir o estilo e a estrutura de seu site.

>[!CAUTION]
>
>No momento, a ferramenta Criação rápida de site é uma visualização técnica. É disponibilizado para fins de ensaio e avaliação e não se destina à utilização da produção, a menos que acordado com o apoio ao Adobe.

## Visão geral {#overview}

Antes que os autores de conteúdo possam criar páginas com conteúdo, o site deve ser criado primeiro. Isso geralmente é executado por um administrador de AEM que define a estrutura inicial do site. Usar modelos de site torna a criação de sites rápida e flexível.

A ferramenta Criação de site rápido AEM permite que não desenvolvedores criem rapidamente um novo site do zero usando modelos de site.

Depois de criada, a ferramenta Criação rápida de site também permite a rápida personalização do tema e estilo do site AEM (JavaScript, CSS e recursos estáticos). Isso permite que o desenvolvedor de front-end, que precisa de conhecimento zero sobre AEM, funcione separadamente e em paralelo aos criadores de conteúdo. O administrador do AEM simplesmente baixa o tema do site e o fornece ao desenvolvedor front-end que o personaliza usando suas ferramentas favoritas e, em seguida, confirma as alterações no repositório de código AEM, que é implantado.

Este documento se concentra na criação do site usando a ferramenta Criação rápida de sites. Se você deseja ter uma visão geral do fluxo de trabalho de criação e personalização do site, consulte a seção [AEM Jornada de criação rápida de site](/help/journey-sites/quick-site/overview.md)

## Estrutura do Site de Planejamento {#structure}

Reserve tempo para considerar a finalidade do site e o conteúdo planejado com bastante antecedência. Isso impulsionará a criação da estrutura do site. Uma boa estrutura do site oferece suporte a navegação fácil e detecção de conteúdo para os visitantes do site, além de oferecer suporte a vários recursos AEM, como [gerenciamento multisite e tradução.](/help/sites-cloud/administering/msm-and-translation.md)

>[!TIP]
>
>[O site de referência WKND](https://wknd.site) O fornece uma implementação de práticas recomendadas de um site de marca de experiências externas totalmente funcional. Explore-o para ver como um site de AEM bem criado está estruturado.

## Modelos de site {#site-templates}

Como a estrutura do site é tão importante para o sucesso de um site, é conveniente ter estruturas predefinidas disponíveis para implantar rapidamente um novo site com base em um conjunto de padrões existentes. Os modelos de site são uma maneira de combinar conteúdo básico do site em um pacote conveniente e reutilizável.

Os modelos de site geralmente contêm conteúdo básico e estrutura do site, bem como informações de estilo do site para começar o novo site rapidamente. Os modelos são poderosos porque são reutilizáveis e personalizáveis. E como você pode ter vários modelos disponíveis na sua instalação do AEM, você tem a flexibilidade de criar sites diferentes para atender a várias necessidades comerciais.

>[!TIP]
>
>Para obter mais detalhes sobre modelos de site, reveja a [Modelos de site](site-templates.md) artigo 10. o

>[!NOTE]
>
>O modelo de site não deve ser confundido com modelos de página. Os modelos de site definem a estrutura geral de um site. Um modelo de página define a estrutura e o conteúdo inicial de uma página individual.

## Criação de um site {#create-site}

É simples usar um modelo para criar um site.

1. Faça logon no ambiente de criação do AEM e navegue até o console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Toque ou clique **Criar** no canto superior direito do ecrã e, no menu suspenso, selecione **Site a partir do modelo**.

   ![Criação de um site a partir de um modelo](../assets/create-site-from-template.png)

1. No assistente Criar site , toque ou clique em um modelo existente no painel esquerdo ou em **Importar** na parte superior da coluna à esquerda para importar um novo modelo.

   ![Assistente de criação do site](../assets/site-creation-wizard.png)

   1. Se você optar por importar, no navegador de arquivos, localize o modelo que deseja usar e toque ou clique em **Upload**.

   1. Depois de carregado, ele aparece na lista de modelos disponíveis.

1. Ao selecionar um template, ele revela informações sobre o template na coluna direita. Com o modelo desejado selecionado, toque ou clique em **Próximo**.

   ![Selecione um modelo](../assets/select-site-template.png)

1. Forneça um título para o seu site. Um nome de site pode ser fornecido ou será gerado a partir do título se omitido.

   * O título do site aparece na barra de título dos navegadores.
   * O nome do site se torna parte do URL.
   * O nome do site deve estar em conformidade com [AEM convenções de nomenclatura de página.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)

1. Toque ou clique **Criar** e o site é criado a partir do modelo do site.

   ![Detalhes do novo site](../assets/create-site-details.png)

1. Na caixa de diálogo de confirmação exibida, toque ou clique em **Concluído**.

   ![Caixa de diálogo de sucesso](../assets/success.png)

1. No console de sites, o novo site é visível e pode ser navegado para explorar sua estrutura básica, conforme definido pelo modelo.

   ![Nova estrutura de site](../assets/new-site.png)

Os autores de conteúdo agora podem começar a criar!

## Personalização do site {#site-customization}

Se seu site requer personalização além dos modelos disponíveis, você tem várias opções.

* Se a estrutura do site ou o conteúdo inicial precisar ser ajustado, [o modelo de site pode ser personalizado para atender aos seus requisitos.](site-templates.md)
* Se o estilo do site precisar ser ajustado, [o tema do site pode ser baixado e personalizado.](/help/journey-sites/quick-site/overview.md)
* Se a funcionalidade do site precisar ser ajustada, [o site pode ser totalmente personalizado.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

Qualquer personalização deve ser realizada com o apoio de uma equipe de desenvolvimento.
