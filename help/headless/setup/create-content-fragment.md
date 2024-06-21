---
title: Criação de fragmentos de conteúdo - Configuração do headless
description: Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 85%

---

# Criação de fragmentos de conteúdo - Configuração do headless {#creating-content-fragments}

Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.

## O que são fragmentos de conteúdo? {#what-are-content-fragments}

[Agora que você criou uma pasta de ativos](create-assets-folder.md) onde você pode armazenar os fragmentos de conteúdo, é possível criar os fragmentos.

Os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem que você deixe o conteúdo pronto para uso em vários locais e em vários canais.

Fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

## Como criar um fragmento de conteúdo {#how-to-create-a-content-fragment}

Os autores de conteúdo criarão qualquer quantidade de fragmentos de conteúdo para representar o conteúdo que eles criam. Esta é sua principal tarefa no AEM. Para os propósitos deste guia de introdução, só será necessário criar um.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Navegação** > **Fragmentos de conteúdo**.

1. Selecione o [pasta criada anteriormente.](create-assets-folder.md)
1. Selecione **Criar**.
1. A criação de um fragmento de conteúdo é apresentada como uma caixa de diálogo.
Selecione o local e o modelo que deseja usar para criar o fragmento de conteúdo.

   * Os modelos disponíveis dependem da [**Configuração na nuvem** que foi definida para a pasta de ativos](create-assets-folder.md) na qual você está criando o fragmento de conteúdo.
   * Se o modelo não estiver disponível, verifique a configuração da pasta de ativos.

   Adicione o Título, o Nome e, se necessário, a Descrição.

   ![Caixa de diálogo Criar novo fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. Selecionar **Criar** ou  **Criar e abrir**.

Os fragmentos de conteúdo podem fazer referência a outros fragmentos de conteúdo, permitindo uma estrutura de conteúdo aninhada, se necessário.

Fragmentos de conteúdo também podem fazer referência a outros ativos no AEM. [Esses ativos precisam estar armazenados no AEM](/help/assets/manage-digital-assets.md) antes da criação de um fragmento de conteúdo de referência.

## Próximas etapas {#next-steps}

Agora que você criou um fragmento de conteúdo, poderá seguir para a parte final do guia de introdução e [criar solicitações de API para acessar e entregar fragmentos de conteúdo.](create-api-request.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
