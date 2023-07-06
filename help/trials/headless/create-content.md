---
title: Criar conteúdo headless
description: Use o modelo de fragmento de conteúdo criado anteriormente para criar um conteúdo que possa ser usado na criação de páginas ou como a base do seu conteúdo headless.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 87%

---


# Criar conteúdo headless {#create-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Criar novo conteúdo"
>abstract="Usando o modelo criado no módulo anterior, você aprenderá a criar conteúdo que pode ser usado para a criação de páginas ou como a base do seu conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Iniciar o console de fragmentos de conteúdo"
>abstract="Criar um conteúdo consistente, de alta qualidade e que funciona perfeitamente em seus aplicativos e sites oferece excelentes experiências ao cliente. Este módulo orienta você a criar o seu primeiro fragmento de conteúdo para mostrar como alcançar isso.<br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e, em seguida, siga este guia."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide_footer"
>title="Excelente trabalho. Nesse módulo, você aprendeu a criar um fragmento de conteúdo com base no modelo criado anteriormente. Agora você sabe como as equipes de conteúdo podem criar e gerenciar conteúdo para aplicativos e sites, independentemente dos ciclos de desenvolvimento."
>abstract=""

## Criar um fragmento de conteúdo {#create-fragment}

Os fragmentos de conteúdo representam o conteúdo headless e são baseados em estruturas predefinidas, chamadas de modelos de fragmento de conteúdo. Você já criou um modelo em um módulo anterior.

Neste módulo, você cria um novo fragmento de conteúdo com base nesse modelo usando o console de Fragmentos de conteúdo. Pense no console de fragmentos de conteúdo como uma biblioteca de conteúdo headless. Use-o para criar novos fragmentos de conteúdo e gerenciar fragmentos existentes.

1. Toque ou clique no botão **Criar** na parte superior direita do console.

1. A variável **Novo fragmento de conteúdo** é aberta, onde você pode começar a criar um novo Fragmento de conteúdo. **Localização** é automaticamente preenchido com onde o novo conteúdo é salvo.

1. No menu suspenso **Modelo de Fragmentos de conteúdo**, selecione o modelo de Fragmento de conteúdo **Aventura** criado anteriormente.

1. Adicione `Tuscany` como um **Título** descritivo para o fragmento de conteúdo. Isso é para identificar o seu fragmento no console.

1. Toque ou clique em **Criar e abrir**.

![Criar um novo fragmento de conteúdo](assets/do-not-localize/create-content.png)

>[!TIP]
>
>Dependendo das configurações do seu navegador, a nova guia do navegador pode ser suprimida por um bloqueador de pop-up. Se o novo fragmento não abrir depois de clicar em **Criar e abrir**, verifique as configurações do navegador.

## Adicionar conteúdo ao fragmento de conteúdo {#add-content}

Depois de salvar e abrir o novo fragmento de conteúdo, o editor de fragmento de conteúdo é aberto em uma nova guia. Aqui, é possível adicionar o conteúdo do novo fragmento.

1. O editor de fragmentos de conteúdo mostra os campos definidos no modelo selecionado. Aqui, é possível adicionar conteúdo a cada campo para concluir o fragmento de conteúdo. Seu progresso é salvo automaticamente.

1. Forneça um **Título** para o fragmento, inserindo `Tuscan Adventure`.

1. Forneça uma **Descrição** para o fragmento colando o texto a seguir.

   ```text
   Visiting Tuscany on a bicycle is about experiencing the old world charm of Italy on your own terms. Your efforts on the climbs of Italy's rolling hills during this tour are rewarded with sunny Mediterranean landscapes and unmatched Italian hospitality. Tuscany's natural wonders have always been a well of inspiration for arts and culture. Find out why as you explore the Italian countryside and coastline on bicycle.
   ```

1. Forneça um **Preço** para o fragmento, inserindo `$700`.

1. Forneça uma **Imagem** que seja representativa da viagem tocando ou clicando em **Adicionar ativo** no campo **Imagem**.

1. Na janela pop-up do ativo, toque ou clique em **Procurar ativos** para selecionar um ativo existente na biblioteca de ativos.

   ![Adicionar ativo](assets/do-not-localize/add-asset.png)

1. A caixa de diálogo **Selecionar ativo** será aberta. Usando o navegador em árvore no painel esquerdo, navegue até **Todos os ativos** > **aem-demo-assets** > **en** > **aventuras** > **cycling-tuscany**.

1. O conteúdo da pasta **cycling-tuscany** será exibido à direita. Selecione a imagem `ADOBESTOCK_141786166.JPEG`.

1. Toque ou clique em **Selecionar**.

   ![Selecionar ativo](assets/do-not-localize/select-asset.png)

1. A imagem selecionada será mostrada no fragmento de conteúdo. O editor salvará as alterações automaticamente.

1. Quando terminar de adicionar conteúdo, toque ou clique no botão **Publicar** na parte superior direita do editor. Isso disponibiliza o fragmento de conteúdo para ser consumido por aplicativos externos. Em seguida, selecione **Agora** no menu suspenso. Também é possível agendar sua publicação para um momento posterior.

   ![Publicar conteúdo](assets/do-not-localize/publish.png)

1. A caixa de diálogo **Publicar fragmentos de conteúdo** será exibida. O AEM executa automaticamente uma verificação de referência para garantir que todos os recursos necessários sejam publicados para o fragmento de conteúdo. Nesse caso, também será necessário publicar o modelo criado. Toque ou clique em **Publicar**.

   ![Publicação e verificação de referência](assets/do-not-localize/publish-confirm.png)

1. A publicação é confirmada em um banner.

Seu conteúdo foi publicado e está pronto para ser entregue ao seu aplicativo ou site como um fragmento de conteúdo.
