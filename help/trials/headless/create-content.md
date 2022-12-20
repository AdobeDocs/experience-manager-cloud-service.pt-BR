---
title: Criar conteúdo headless
description: Use o modelo de Fragmento de conteúdo criado anteriormente para criar conteúdo que pode ser usado para a criação de página ou como a base para o seu conteúdo sem periféricos.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
source-git-commit: 1456891dc3b13b3d79fa8ee9f3ded37e92cfbc85
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# Criar conteúdo headless {#create-content}

Ao seguir o módulo de aprendizado no produto, saiba como usar [os modelos de Fragmento de conteúdo criados anteriormente](content-structure.md) para criar conteúdo que pode ser usado para criação de página ou como a base para seu conteúdo sem periféricos. Este documento constitui um complemento da viagem interativa, que cobre as mesmas etapas e se vincula aos recursos adicionais, se for caso disso.

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Criar novo conteúdo"
>abstract="Com base nos modelos criados no módulo 1, você aprenderá a criar conteúdo que pode ser usado para criação de página ou como a base do seu conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Iniciar o console Fragmento de conteúdo"
>abstract="Em AEM CMS sem periféricos, &quot;fragmentos de conteúdo&quot; são todos pedaços de conteúdo que se encaixam na estrutura predefinida chamada de &quot;modelo de fragmento de conteúdo&quot;. Nesta apresentação, você aprenderá a criar conteúdo para o modelo de fragmento de conteúdo.<br><br>Clique abaixo para iniciar o recurso em uma nova guia e siga este documento de aprendizagem para criar seu primeiro fragmento de conteúdo."
>additional-url="https://video.tv.adobe.com/v/328618" text="Espaço reservado do vídeo de introdução"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home_c1.png" text="Miniatura do vídeo: Adição de conteúdo - a receita vencedora"

## Fragmentos de conteúdo {#introduction}

Em AEM as a Cloud Service, os Fragmentos de conteúdo são partes do conteúdo sem periféricos com base na estrutura definida por um modelo de Fragmento de conteúdo. Você pode criar seu próprio Fragmento de conteúdo começando pelo console Fragmento de conteúdo . O console Fragmento do conteúdo pode ser considerado como sua biblioteca de conteúdo sem periféricos. Use o console para criar novos Fragmentos de conteúdo e gerenciar fragmentos existentes. Seu console começa vazio, por isso vamos criar um novo fragmento!

![Edição do conteúdo do fragmento](assets/create-content/content-fragment-console.png)

Se você quiser navegar até o console Fragmento de conteúdo , fora da orientação no aplicativo, ele será encontrado usando o ícone Adobe no canto superior esquerdo da página. Isso abre a navegação global do AEM. Aqui, você escolhe o **Navegação** e depois **Fragmentos de conteúdo**.

>[!TIP]
>
>Se você quiser saber mais sobre navegação no AEM, consulte o [Seção Recursos adicionais](#additional-resources) deste documento para obter mais informações sobre AEM manuseio básico.

## Criar um fragmento de conteúdo {#create-fragment}

Os Fragmentos de conteúdo representam o conteúdo sem periféricos. Mas eles só podem ser criados com base em uma estrutura de conteúdo predefinida. O modelo de Fragmento do conteúdo criado anteriormente serve como essa estrutura.

1. Toque ou clique no botão **Criar** na parte superior direita do console para abrir o **Novo fragmento de conteúdo** para começar a criar um novo Fragmento do conteúdo.

   ![Caixa de diálogo Criar fragmento de conteúdo](assets/create-content/create-content-fragment.png)

1. Se você estiver seguindo a orientação no aplicativo, **Localização** serão automaticamente preenchidas.

   1. Se não estiver seguindo a orientação, use o navegador de caminho para selecionar a pasta do projeto.

   1. No **Novo fragmento de conteúdo** toque ou clique no botão **Escolher local** (o ícone que se parece com uma pasta) na **Localização** campo.

      ![Escolher caixa de diálogo de localização](assets/create-content/choose-location.png)
   * Como alternativa, selecione o caminho no painel de navegação esquerdo do console Fragmento de conteúdo antes de clicar em **Criar**.


1. No **Modelo do fragmento de conteúdo** selecione o modelo de Fragmento de conteúdo criado anteriormente na lista suspensa.

1. Adicione um **Título** para o Fragmento do conteúdo.

1. Toque ou clique **Criar e abrir**.

## Editor de fragmento de conteúdo {#edit-fragment}

Depois de salvar o novo Fragmento do conteúdo, o editor de Fragmento do conteúdo é aberto, onde é possível fornecer o conteúdo real do fragmento.

1. O editor mostra os campos definidos no modelo selecionado. Aqui, você pode editá-los para concluir o fragmento de conteúdo. Seu progresso é salvo automaticamente.

   ![Editor de fragmento de conteúdo](assets/create-content/content-fragment-editor.png)

1. Se o modelo do Fragmento de conteúdo tiver muitos campos, você poderá pular rapidamente para qualquer campo usando a variável **Variáveis** no lado esquerdo do editor. Os campos com erros serão sinalizados aqui.

1. Para que o Fragmento de conteúdo esteja disponível para consumo por aplicativo externo, é necessário publicá-lo. Toque ou clique no botão **Publicar** na parte superior direita do editor.

1. Selecionar **Agora** no menu suspenso . Você também pode agendá-lo para publicação posteriormente.

   ![Botão Publicar](assets/create-content/publish.png)

   >[!TIP]
   >
   >Se quiser saber mais sobre como publicar conteúdo no AEM, consulte o [Seção Recursos adicionais](#additional-resources) deste documento para obter mais informações sobre publicação.

1. O AEM executa automaticamente uma verificação de referência para garantir que todos os recursos necessários sejam publicados no Fragmento do conteúdo. Nesse caso, também será necessário publicar o modelo criado. Toque ou clique em **Publicar**.

   ![Verificação de referência](assets/create-content/references.png)

1. A publicação é confirmada em um banner.

   ![Confirmação da publicação](assets/create-content/publish-confirm.png)

## Você aprendeu a criar um Fragmento de conteúdo! {#conclusion}

Neste módulo, você aprendeu a criar um Fragmento de conteúdo com base no modelo criado anteriormente. É assim que um autor de conteúdo criaria conteúdo estruturado sem cabeçalho.

Agora que seu conteúdo foi criado e publicado, você pode extrair esse conteúdo via Graph QL via APIs AEM. Você aprenderá sobre isso no módulo [Extraia conteúdo por meio da API GraphQL.](extract-content.md)

Você pode retornar à sua tela inicial de avaliação clicando em **Soluções** botão na parte superior direita da barra de navegação e selecionando **Experience Manager**.

![Ir para casa](assets/create-content/home.png)

## Recursos adicionais {#additional-resources}

Para obter mais informações sobre Fragmentos de conteúdo e AEM, considere revisar esta documentação adicional.

* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Documentação sobre como navegar e usar AEM para novos usuários
* [Gerenciamento de fragmentos de conteúdo - Publicação e referência](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment) - Detalhes sobre como publicar conteúdo em AEM
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) - Visão geral dos fragmentos de conteúdo e links para concluir a documentação sobre os fragmentos de conteúdo
* [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md) - Como criar e gerenciar fragmentos de conteúdo
