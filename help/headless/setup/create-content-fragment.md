---
title: Criação de fragmentos de conteúdo - Configuração do headless
description: Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: d35b60810a1624390d3d9c82c2a364140ea37536
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 100%

---

# Criação de fragmentos de conteúdo - Configuração do headless {#creating-content-fragments}

Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.

## O que são fragmentos de conteúdo? {#what-are-content-fragments}

[Agora que você criou uma pasta de ativos](create-assets-folder.md) onde você pode armazenar os fragmentos de conteúdo, é possível criar os fragmentos.

Os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem que você deixe o conteúdo pronto para uso em vários locais e em vários canais.

Fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

## Como criar um fragmento de conteúdo {#how-to-create-a-content-fragment}

Os autores de conteúdo criarão qualquer quantidade de fragmentos de conteúdo para representar o conteúdo que eles criam. Esta será a principal tarefa deles no AEM. Para os propósitos deste guia de introdução, só será necessário criar um.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Navegação -> Ativos**.
1. Toque ou clique na [pasta criada anteriormente.](create-assets-folder.md)
1. Toque ou clique em **Criar -> Fragmento de conteúdo**.
1. A criação de um fragmento de conteúdo é apresentada como um assistente de duas etapas. Primeiro, selecione qual modelo deseja usar para criar o fragmento de conteúdo e toque ou clique em **Próximo**.
   * Os modelos disponíveis dependem da [**Configuração na nuvem** que foi definida para a pasta de ativos](create-assets-folder.md) na qual você está criando o fragmento de conteúdo.
   * Se você receber a mensagem `We could not find any models`, verifique a configuração da pasta de ativos.

   ![Selecionar modelo de fragmento de conteúdo](../assets/content-fragment-model-select.png)
1. Forneça o **Título**, a **Descrição** e as **Tags** conforme necessário, e toque ou clique em **Criar**.

   ![Criar fragmento do conteúdo](../assets/content-fragment-create.png)
1. Toque ou clique em **Abrir** na janela de confirmação.

   ![Confirmação da criação do fragmento de conteúdo](../assets/content-fragment-confirmation.png)
1. Forneça os detalhes do fragmento de conteúdo no Editor de fragmento de conteúdo.

   ![Editor de fragmento de conteúdo](../assets/content-fragment-edit.png)
1. Toque ou clique em **Salvar** ou **Salvar e fechar**.

Os fragmentos de conteúdo podem fazer referência a outros fragmentos de conteúdo, permitindo uma estrutura de conteúdo aninhada, se necessário.

Fragmentos de conteúdo também podem fazer referência a outros ativos no AEM. [Esses ativos precisam estar armazenados no AEM](/help/assets/manage-digital-assets.md) antes da criação de um fragmento de conteúdo de referência.

## Próximas etapas {#next-steps}

Agora que você criou um fragmento de conteúdo, poderá seguir para a parte final do guia de introdução e [criar solicitações de API para acessar e entregar fragmentos de conteúdo.](create-api-request.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
