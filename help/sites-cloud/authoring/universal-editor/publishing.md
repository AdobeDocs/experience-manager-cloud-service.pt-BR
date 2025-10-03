---
title: Publicação de conteúdo com o Editor universal
description: Saiba como o Editor universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: c0714a7b74cd223ad4a405934c89a3146fb8b5c4
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 31%

---


# Publicação de conteúdo com o Editor universal {#publishing}

Saiba como o Editor universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.

>[!TIP]
>
>O processo de publicação descrito aqui é o recurso padrão pronto para uso do Universal Editor.
>
>O Editor Universal também oferece suporte a [extensões e extensibilidade da interface do usuário](/help/implementing/universal-editor/extending.md) para permitir que os fluxos de trabalho ofereçam suporte ao seu processo de publicação, de modo que o fluxo de publicação possa variar.

## Publicar conteúdo por meio do Editor universal {#publishing-content}

Quando você, como autor de conteúdo, estiver pronto para publicar seu conteúdo, basta tocar ou clicar no ícone **Publicar** na barra de ferramentas do Editor Universal.

![Publicando páginas](assets/publish-menu.png)

1. No Editor Universal, toque ou clique [no ícone **Publicar** na barra de ferramentas do Editor Universal.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)
1. Se você tiver um [serviço de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) disponível, poderá escolher onde publica seu conteúdo, para **[Visualizar](/help/sites-cloud/authoring/sites-console/previewing-content.md)** (se disponível) ou **Publicar**.
1. A seção **Itens** lista o conteúdo incluído na publicação. Toque ou clique em **Exibir** para mostrar os detalhes, incluindo:
   * **Novos** itens que ainda não foram publicados.
   * **Modificado** conteúdo que foi publicado, mas modificado desde a última publicação.
   * **Publicado** conteúdo que foi publicado e não foi modificado desde a publicação.

   Toque ou clique nas caixas de seleção ao lado desses itens para incluí-los/excluí-los da publicação, conforme necessário. Toque ou clique em **Estender** para ver os itens individuais incluídos nos totais das três categorias e poder inseri-los/excluí-los individualmente.

   ![Publicar itens](assets/publish-items.png)

   Toque ou clique na seta para trás ao lado do cabeçalho **Itens** para retornar à visão geral.

1. Toque ou clique em **Publicar** para publicar ou em **Cancelar** para anular.

>[!NOTE]
>
>A opção de publicar para visualização [pode ser desabilitada](/help/implementing/universal-editor/customizing.md#publish-preview) e, portanto, pode não aparecer no editor.

## Desfazer a publicação de conteúdo no Editor universal {#unpublishing-content}

Desfazer a publicação de conteúdo funciona de maneira semelhante à publicação de conteúdo. Quando você, como autor de conteúdo, estiver pronto para remover conteúdo da publicação, toque ou clique no ícone de reticências na barra de ferramentas do Editor Universal e **Cancelar publicação**.

Em seguida, você tem as mesmas opções para desfazer a publicação de conteúdo que tinha ao [publicar conteúdo.](#publishing-content) incluindo desfazer a publicação de uma instância de visualização, se disponível, e quais itens incluir no desfazer a publicação.

## Publicar e desfazer a publicação por meio do console Sites {#publishing-sites-console}

Você também pode publicar [no console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), que pode ser útil quando desejar publicar várias páginas de conteúdo ou agendar a publicação ou o cancelamento da publicação.

## Recursos adicionais {#additional-resources}

Para saber como criar conteúdo com o editor universal, consulte este documento.

* [Criação de conteúdo com o Editor universal](authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo usando o Editor universal.

Para saber mais sobre os detalhes técnicos do Universal Editor, consulte estes documentos do desenvolvedor.

* [Introdução ao Editor universal](/help/implementing/universal-editor/introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.
* [Introdução ao Editor universal no AEM](/help/implementing/universal-editor/getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](/help/implementing/universal-editor/architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](/help/implementing/universal-editor/attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](/help/implementing/universal-editor/authentication.md): saiba como funciona a autenticação do Editor universal.
