---
title: Criando Fragmentos de Conteúdo Guia de Start Rápido Sem Cabeçalho
description: Os Fragmentos de conteúdo permitem que você crie, prepare e use conteúdo independente de página que pode ser entregue sem cabeçalho por AEM.
translation-type: tm+mt
source-git-commit: fa2fee3139acd60ea96222752785cf397978a2bc
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Criando Fragmentos de Conteúdo Guia de Start Rápido Sem Cabeçalho {#creating-content-fragments}

Os Fragmentos de conteúdo permitem que você crie, prepare e use conteúdo independente de página que pode ser entregue sem cabeçalho por AEM.

## O que são Fragmentos de conteúdo? {#what-are-content-fragments}

[Agora que você criou uma ](create-assets-folder.md) pasta de ativos na qual pode armazenar seus Fragmentos de conteúdo, agora é possível criar os fragmentos!

Fragmentos de conteúdo permitem que você crie, prepare e publique conteúdo independente de página. Eles permitem que você prepare conteúdo pronto para uso em vários locais e em vários canais.

Os fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

## Como criar um fragmento de conteúdo {#how-to-create-a-content-fragment}

Os autores de conteúdo criarão qualquer número de Fragmentos de conteúdo para representar o conteúdo que criarem. Esta será a sua principal tarefa em AEM. Para os fins deste guia de introdução, só precisaremos criar um.

1. Efetue login AEM como um Cloud Service e, no menu principal, selecione **Navegação -> Ativos**.
1. Toque ou clique na pasta [criada anteriormente.](create-assets-folder.md)
1. Toque ou clique em **Criar -> Fragmento de conteúdo**.
1. A criação de um Fragmento de conteúdo é apresentada como um assistente em duas etapas. Primeiro, selecione o modelo que deseja usar para criar seu fragmento de conteúdo e toque ou clique em **Próximo**.
   * Os modelos disponíveis dependem da [**Configuração da nuvem** definida para a pasta de ativos](create-assets-folder.md) na qual você está criando o Fragmento de conteúdo.
   * Se você receber a mensagem `We could not find any models`, verifique a configuração da sua pasta de ativos.

   ![Selecionar modelo de fragmento do conteúdo](../assets/content-fragment-model-select.png)
1. Forneça um **Título**, **Descrição** e **Tags** conforme necessário e toque ou clique em **Criar**.

   ![Criar fragmento do conteúdo](../assets/content-fragment-create.png)
1. Toque ou clique em **Abrir** na janela de confirmação.

   ![Confirmação de criação do Fragmento de conteúdo](../assets/content-fragment-confirmation.png)
1. Forneça os detalhes do Fragmento do conteúdo no Editor de fragmentos do conteúdo.

   ![Editor de conteúdo do fragmento](../assets/content-fragment-edit.png)
1. Toque ou clique em **Salvar e fechar**.

Fragmentos de conteúdo podem fazer referência a outros Fragmentos de conteúdo, permitindo uma estrutura de conteúdo aninhada, se necessário.

Fragmentos de conteúdo também podem fazer referência a outros ativos no AEM. [Esses ativos precisam ser armazenados no ](/help/assets/manage-digital-assets.md) AEM antes de criar um Fragmento de conteúdo de referência.

## Próximas etapas {#next-steps}

Agora que criou um Fragmento de conteúdo, você pode seguir para a parte final do guia de introdução e [criar solicitações de API para acessar e fornecer fragmentos de conteúdo.](create-api-request.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de Fragmentos de conteúdo, consulte a [documentação de Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
