---
title: Publicação de conteúdo com o Editor universal
description: Saiba como o Editor universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 73b1a318325e7641ee0fd7a76a3a73a7299c8b91
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 61%

---


# Publicação de conteúdo com o Editor universal {#publishing}

Saiba como o Editor universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.

## Publicação de conteúdo como autor {#publishing-content}

Quando você, como autor de conteúdo, estiver pronto para publicar seu conteúdo, basta tocar ou clicar no [ícone **Publicar** na barra de ferramentas do Editor Universal.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)

Você também pode publicar [no console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), que pode ser útil quando desejar publicar várias páginas de conteúdo.

>[!NOTE]
>
>O Editor Universal oferece suporte a [extensões e extensibilidade da interface do usuário](/help/implementing/universal-editor/extending.md) para permitir que os fluxos de trabalho ofereçam suporte ao seu processo de publicação.

## Semelhanças com o AEM {#similarities}

Para usuários do AEM, o processo de publicar conteúdo com o Universal Editor funciona como você está acostumado: na publicação no AEM, o conteúdo é replicado do nível do autor para o nível de publicação.

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
