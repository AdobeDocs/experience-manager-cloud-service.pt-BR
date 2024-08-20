---
title: Extrair conteúdo por meio da API GraphQL
description: Saiba como usar fragmentos de conteúdo e a API GraphQL como um sistema de gerenciamento de conteúdo headless.
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 100%

---


# Extrair conteúdo por meio da API GraphQL {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="Extrair conteúdo usando a API GraphQL"
>abstract="Neste módulo, você aprenderá a usar fragmentos de conteúdo e a API GraphQL como um sistema de gerenciamento de conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="Iniciar o GraphQL Explorer"
>abstract="O GraphQL fornece uma API baseada em consultas que permite que os aplicativos clientes externos consultem apenas o conteúdo necessário no AEM, usando uma única chamada de API. Siga este módulo para saber como executar dois tipos diferentes de consultas. Em seguida, saiba como recuperar o conteúdo do fragmento de conteúdo criado no módulo anterior.<br><br>Inicie esse módulo em uma nova guia clicando abaixo."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="Bom trabalho. Você aprendeu sobre os dois tipos básicos de consultas e como consultar seu próprio conteúdo. Agora você entende como usar a API GraphQL do AEM para criar consultas eficientes que fornecem conteúdo no formato esperado pelo aplicativo."
>abstract=""

## Consultar uma lista de conteúdo de amostra {#list-query}

O GraphQL Explorer é iniciado em uma nova guia. Aqui, é possível criar e validar consultas com o seu conteúdo headless antes de usá-las para fornecer conteúdo ao seu aplicativo ou site.

1. Sua avaliação do AEM Headless vem com um ponto de acesso pré-carregado com fragmentos de conteúdo, do qual você pode extrair conteúdo para fins de teste. Certifique-se de que o ponto de acesso **Ativos de demonstração do AEM** esteja selecionado no menu suspenso **Ponto de acesso** no canto superior direito do editor.

1. Copie o seguinte trecho de código para uma consulta de lista do ponto de acesso pré-carregado **Ativos de demonstração do AEM**. Uma consulta de lista retorna uma lista com todos os conteúdos que utilizam um modelo de fragmento de conteúdo específico. As páginas de inventário e categoria normalmente usam esse formato de consulta.

   ```text
   {
    adventureList {
     items {
       _path
       title
       price
       tripLength
       primaryImage {
         ... on ImageRef {
           _path
           mimeType
           width
           height
         }
       }
     }
    }
   }
   ```

1. Substitua o conteúdo existente no editor de consultas colando o código copiado.

1. Depois de colado, clique no botão **Reproduzir** na parte superior esquerda do editor de consultas para executar a consulta.

1. Os resultados serão exibidos no painel direito, ao lado do editor de consultas. Se a consulta estiver incorreta, um erro aparecerá no painel direito.

   ![Consulta de lista](assets/do-not-localize/list-query-1-3-4-5.png)

Você acabou de validar uma consulta de lista que contém uma lista completa de todos os fragmentos de conteúdo. Esse processo ajuda a garantir que a resposta seja a que seu aplicativo espera, com resultados que ilustram como seus aplicativos e sites recuperarão o conteúdo criado no AEM.

## Consultar uma parte específica do conteúdo de amostra {#bypath-query}

A execução de uma consulta byPath permite recuperar o conteúdo de um fragmento de conteúdo específico. As páginas de detalhes do produto e as que se concentram em um conjunto específico de conteúdo normalmente exigem esse tipo de consulta.

1. Copie o seguinte trecho de código para uma consulta byPath do ponto de acesso pré-carregado **Ativos de demonstração do AEM**.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. Substitua o conteúdo existente no editor de consultas colando o código copiado.

1. Depois de colado, clique no botão **Reproduzir** na parte superior esquerda do editor de consultas para executar a consulta.

1. Os resultados serão exibidos no painel direito, ao lado do editor de consultas. Se a consulta estiver incorreta, um erro aparecerá no painel direito.

   ![Resultados da consulta byPath](assets/do-not-localize/bypath-query-2-3-4.png)

Você acabou de validar uma consulta byPath para recuperar um fragmento de conteúdo específico identificado pelo caminho desse fragmento.

## Consultar seu próprio conteúdo {#own-queries}

Agora que executou os dois tipos principais de consulta, você está pronto para consultar seu próprio conteúdo.

1. Para executar consultas em seus próprios fragmentos de conteúdo, altere o ponto de acesso da pasta **Ativos de demonstração do AEM** para a pasta **Seu projeto**.

1. Exclua todo o conteúdo existente no editor de consultas. Em seguida, insira um colchete de abertura `{` e pressione Ctrl+Barra de espaço ou Option+Barra de espaço para obter uma lista de modelos de preenchimento automático que foram definidos no seu ponto de acesso. Dentre as opções, selecione o modelo criado que termina em `List`. Se você seguiu os exemplos dos módulos anteriores, deverá encontrar `adventureList` na lista de preenchimento automático.

   ![Iniciar consulta personalizada](assets/do-not-localize/custom-query-1.png)

1. Defina os itens que a consulta deve conter para o modelo de fragmento de conteúdo selecionado. Novamente, insira um colchete de abertura `{` e pressione Ctrl+Barra de espaço ou Option+Barra de espaço para obter uma lista de preenchimento automático. Selecione `items` nas opções.

1. Selecione o botão **Adornar** para formatar automaticamente o seu código e facilitar a leitura.

1. Depois de concluir, selecione o botão **Reproduzir** no canto superior esquerdo do editor para executar a consulta. O editor preenche automaticamente os `items`, que são brevemente destacados em amarelo, e a consulta é executada.

1. Os resultados são exibidos no painel direito, ao lado do editor de consultas.

   ![Executar consulta personalizada](assets/do-not-localize/custom-query-2.png)

É assim que o seu conteúdo pode ser entregue em experiências digitais omnicanal.

## Consultas persistentes {#persisted-queries}

As consultas persistentes são o mecanismo preferido para expor a API GraphQL aos aplicativos clientes. Depois que uma consulta persiste, ela pode ser solicitada usando uma solicitação GET e armazenada em cache para recuperação rápida.

Você criará uma consulta persistente que incluirá dados que gostaria de consumir do aplicativo cliente.

1. Você usará os dados criados como um fragmento de conteúdo anteriormente, portanto, certifique-se de que o ponto de acesso **Seu projeto** esteja selecionado no menu suspenso **Ponto de acesso** no canto superior direito do editor.

1. Copie o trecho de código a seguir.

   ```text
      {
      adventureList {
       items {
         title
         description {
           plaintext
         }
         price
         image {
           ... on ImageRef {
             _publishUrl
             mimeType
           }
         }
       }
     }
   }
   ```

1. Substitua o conteúdo existente no editor de consultas colando o código copiado.

   >[!NOTE]
   >
   >Se não tiver usado as mesmas descrições de campo descritas nos módulos anteriores, atualize os nomes de campo nesta consulta.
   >
   >Use o recurso de preenchimento automático (Ctrl+Espaço ou Option+Espaço) do GraphQL conforme descrito anteriormente para ajudar a identificar as propriedades disponíveis.

1. Depois de colado, clique no botão **Reproduzir** na parte superior esquerda do editor de consultas para executar a consulta.

1. Os resultados serão exibidos no painel direito, ao lado do editor de consultas. Se a consulta estiver incorreta, um erro aparecerá no painel direito.

   ![Criar consulta própria](assets/do-not-localize/own-query.png)

1. Quando estiver satisfeito com sua consulta, clique no botão **Salvar como** na parte superior do editor de consultas para persistir a consulta.

1. No pop-up **Nome da consulta**, dê o nome à sua consulta `adventure-list`.

1. Selecione **Salvar como**.

   ![Persistir consulta](assets/do-not-localize/persist-query.png)

1. A consulta é persistida como confirmado por uma mensagem em banner na parte inferior da tela. A consulta também aparece agora no painel esquerdo de consultas persistentes na janela.

1. Para que a consulta persistente esteja disponível publicamente, ela precisará ser publicada, assim como seus fragmentos de conteúdo precisam ser publicados. Clique em **Publicar** no canto superior direito do editor de consultas para publicar a consulta.

1. A publicação é confirmada por uma notificação em banner.

Agora você tem uma nova consulta persistente que conterá apenas as propriedades e os formatos específicos que você definiu.
