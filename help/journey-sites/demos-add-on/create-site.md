---
title: Criar Site de Demonstração
description: Crie um site de demonstração no AEM com base em uma biblioteca de modelos pré-configurados.
source-git-commit: df9b777e24e56ed0329895f833f50b45ecf2defa
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 2%

---


# Criar Site de Demonstração {#creating-a-site}

Crie um site de demonstração no AEM com base em uma biblioteca de modelos pré-configurados.

## A História Até Agora {#story-so-far}

No documento anterior da jornada do complemento Demonstrações de Referência AEM, [Criar programa,](create-program.md) você deu a primeira etapa de configuração para criar um programa para fins de teste e usou um pipeline para implantar o conteúdo complementar. Agora você deve:

* Entenda como usar o Cloud Manager para criar um novo programa.
* Saiba como ativar o Suplemento de Demonstrações de Referência para o novo programa.
* Pode executar um pipeline para implantar o conteúdo complementar.

Este artigo descreve a próxima etapa do processo, criando um novo site ou projeto do AEM Screens no AEM com base nos modelos do Suplemento de demonstração de referência.

## Objetivo {#objective}

Este documento ajuda você a entender como criar um novo site com base nos modelos do Complemento de demonstração de referência. Depois de ler, você deve:

* Entenda como acessar o ambiente de criação do AEM.
* Saiba como criar um site com base em um modelo.
* Entenda as noções básicas de navegação na estrutura do site e edição de uma página.

## Criar um site de demonstração ou um projeto do Screens {#create-site}

Depois que o pipeline tiver implantado o Reference Demo Add-On, você poderá acessar o ambiente de criação de AEM para criar sites de demonstração com base no conteúdo complementar.

1. Na página Visão geral do programa no Cloud Manager, toque ou clique no link para o ambiente de criação do AEM.

   ![Ambiente de criação de acesso](assets/access-author.png)

1. No menu principal de AEM, toque ou clique em **Sites**.

   ![Acessar sites](assets/access-sites.png)

1. No console Sites, toque ou clique em **Criar** no canto superior direito da tela e selecione **Site a partir do modelo** no menu suspenso .

   ![Criar site a partir de modelo](assets/create-site-from-template.png)

1. O assistente de criação de sites é iniciado. Na coluna da esquerda, é possível ver os modelos de demonstração que o pipeline implantou em sua instância de criação. Toque ou clique em um para selecioná-lo e mostrar detalhes na coluna direita. Se desejar testar ou demonstrar o AEM Screens, certifique-se de escolher a variável **Modelo de site We.Cafe**. Toque ou clique em **Próximo**.

   ![Assistente de criação do site](assets/site-creation-wizard.png)

1. Na próxima tela, forneça um título para o seu site ou projeto do Screens. Um nome de site pode ser fornecido ou será gerado a partir do título se omitido. Toque ou clique em **Criar**.

   * O título do site aparece na barra de título dos navegadores.
   * O nome do site se torna parte do URL.
   * O nome do site deve estar em conformidade com AEM convenções de nomenclatura de página, cujos detalhes estão disponíveis no [Recursos adicionais](#additional-resources) seção.

   ![Detalhes do site](assets/site-details.png)

1. A criação do site é confirmada com uma caixa de diálogo. Toque ou clique **Concluído**.

   ![Criação do site concluída](assets/site-creation-complete.png)

Agora você criou seu próprio site de demonstração!

## Use o site de demonstração {#use-site}

Agora que seu site de demonstração foi criado, você pode navegar e usá-lo como faria com qualquer outro site no AEM.

1. O site agora aparece no console de sites.

   ![Novo site de demonstração no console Sites](assets/new-demo-site.png)

1. No canto superior direito da tela, verifique se a exibição do console está definida como **Exibição de coluna**.

   ![Exibição de coluna](assets/column-view.png)

1. Toque ou clique no site para explorar sua estrutura e conteúdo. A exibição de coluna é expandida continuamente à medida que você navega pela árvore de conteúdo do site de demonstração.

   ![Estrutura do site](assets/site-structure.png)

1. Toque ou clique em uma página para selecioná-la e, em seguida, toque ou clique **Editar** na barra de ferramentas.

   ![Selecionar página](assets/select-page.png)

1. É possível editar a página como qualquer outra página de conteúdo AEM, como adicionar ou editar componentes ou ativos e testar a funcionalidade do AEM.

   ![Editar página](assets/edit-page.png)

Parabéns! Agora você pode explorar o conteúdo do seu site de demonstração e descobrir tudo o que o AEM precisa oferecer através do conteúdo de práticas recomendadas do Complemento de demonstração de referência.

Crie sites adicionais com base em outros modelos para explorar mais funcionalidades AEM.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada AEM Reference Demo Add-On (Complemento de demonstração de referência), deve:

* Entenda como acessar o ambiente de criação do AEM.
* Saiba como criar um site com base em um modelo.
* Entenda as noções básicas de navegação na estrutura do site e edição de uma página.

Agora é possível testar os recursos do AEM usando conteúdo complementar. Você tem duas opções para continuar sua jornada:

* Se desejar demonstrar e testar totalmente o conteúdo do AEM Screens, certifique-se de implantar um site com base na variável **Modelo de site We.Cafe** conforme descrito anteriormente e continue [Ative o AEM Screens para seu site de demonstração.](screens.md)
* Se você estiver somente com o conteúdo do Sites de demonstração, continue com [Gerencie seus sites de demonstração,](manage.md) onde você aprenderá sobre as ferramentas disponíveis para ajudá-lo a gerenciar seus sites de demonstração e como removê-los.

## Recursos adicionais {#additional-resources}

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
* [Criar Site](/help/sites-cloud/administering/site-creation/create-site.md) - Saiba como usar o AEM para criar um site usando modelos de site para definir o estilo e a estrutura do site.
* [AEM convenções de nomenclatura de página.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices) - Consulte esta página para entender as convenções para organizar AEM páginas.
* [Manuseio básico de AEM](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Explore este documento se você é novo em AEM para entender conceitos básicos como navegação e organização do console.