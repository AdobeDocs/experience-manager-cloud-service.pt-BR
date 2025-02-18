---
title: Publicação de conteúdo com o Editor universal
description: Saiba como o Editor universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 64c257adc7e1f22531c0fe45b44b27ab4e0badb8
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 42%

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
1. Se você tiver um [serviço de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) disponível, poderá escolher onde publica o seu conteúdo, para **Visualizar** ou **Publicar**.
1. A seção **Itens** lista o conteúdo incluído na publicação, incluindo:
   * **Novos** itens que ainda não foram publicados.
   * **Conteúdo modificado** que foi publicado, mas modificado desde a última publicação.
   * **Publicado** conteúdo que foi publicado e não foi modificado desde a publicação.

   Toque ou clique nas caixas de seleção ao lado desses itens para incluí-los/excluí-los da publicação, conforme necessário. Toque ou clique em **Estender** para ver os itens individuais incluídos nos totais das três categorias e poder inseri-los/excluí-los individualmente.

   ![Publicar itens](assets/publish-items.png)

   Toque ou clique na seta para trás ao lado do cabeçalho **Itens** para retornar à visão geral.

1. Toque ou clique em **Publicar** para publicar ou em **Cancelar** para anular.

## Desfazer a publicação de conteúdo no Editor universal {#unpublishing-content}

Desfazer a publicação de conteúdo funciona de maneira semelhante à publicação de conteúdo. Quando você, como autor de conteúdo, estiver pronto para remover conteúdo da publicação, toque ou clique no ícone de reticências na barra de ferramentas do Editor Universal e **Cancelar publicação**.

Em seguida, você tem as mesmas opções para desfazer a publicação de conteúdo que tinha ao [publicar conteúdo.](#publishing-content) incluindo desfazer a publicação de uma instância de visualização, se disponível, e quais itens incluir no desfazer a publicação.

## Publicar e desfazer a publicação por meio do console Sites {#publishing-sites-console}

Você também pode publicar [no console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), que pode ser útil quando desejar publicar várias páginas de conteúdo ou agendar a publicação ou o cancelamento da publicação.

## Semelhanças com o Editor de páginas {#similarities}

Para usuários do [Editor de páginas do AEM](/help/sites-cloud/authoring/page-editor/introduction.md), o processo de publicação de conteúdo com o Editor Universal funciona como você está acostumado: na publicação no AEM, o conteúdo é replicado do nível de criação para o nível de publicação.

## Diferenças {#differences}

O que torna a publicação com o Editor Universal um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Editor Universal possibilita.

Quando hospedado externamente, o objetivo do aplicativo web é garantir que o conteúdo seja carregado da camada do autor quando o aplicativo for aberto por autores no editor e carregado da camada de publicação quando o aplicativo for acessado por visitantes.

## Detecção da camada no aplicativo {#detecting}

Para determinar se a camada do autor ou de publicação deve ser acessada, uma simples declaração condicional pode ser utilizada no aplicativo ao detectar que seu conteúdo está sendo aberto no editor, a fim de escolher o ponto de acesso apropriado do autor ou da publicação.

Outra opção é implantar o aplicativo em dois ambientes configurados de forma diferente, para que um recupere o conteúdo da camada do autor e o outro o recupere da camada de publicação. Para permitir que os autores abram a URL publicada no Editor Universal, um pequeno script pode ser criado para &quot;converter&quot; a URL do lado da publicação para seu equivalente no ambiente do autor (por exemplo, anexando um subdomínio `author`), para que os autores sejam automaticamente redirecionados.

## Resumo {#summary}

O Editor universal não impõe nenhum padrão específico, de modo que a implementação possa alcançar melhor os seus objetivos de uma forma totalmente dissociada, mantendo um processo simples e direto para a implementação.

Da mesma forma, o Editor universal não estabelece nenhum requisito sobre como um projeto específico deve se comportar ao determinar de qual camada fornecer o conteúdo. Em vez disso, permite várias possibilidades e que o projeto determine qual solução é a melhor para suas próprias necessidades.

## Recursos adicionais {#additional-resources}

Para saber como criar conteúdo com o editor universal, consulte este documento.

* [Criação de conteúdo com o Editor universal](authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo usando o Editor universal.

Para saber mais sobre os detalhes técnicos do Universal Editor, consulte estes documentos do desenvolvedor.

* [Introdução ao Editor universal](/help/implementing/universal-editor/introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.
* [Introdução ao Editor universal no AEM](/help/implementing/universal-editor/getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](/help/implementing/universal-editor/architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](/help/implementing/universal-editor/attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](/help/implementing/universal-editor/authentication.md): saiba como funciona a autenticação do Editor universal.
