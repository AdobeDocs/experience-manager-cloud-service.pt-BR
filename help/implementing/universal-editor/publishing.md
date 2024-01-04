---
title: Publicação de conteúdo com o Editor universal
description: Saiba como o Editor Universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 55%

---


# Publicação de conteúdo com o Editor universal {#publishing}

Saiba como o Editor Universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.

{{universal-editor-status}}

## Semelhanças com o AEM {#similarities}

Para usuários do AEM, o processo de publicar conteúdo com o Universal Editor funciona como você está acostumado: na publicação no AEM, o conteúdo é replicado do nível do autor para o nível de publicação.

## Diferenças {#differences}

O que torna a publicação com o Editor Universal um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Editor Universal possibilita.

Quando hospedado externamente, o objetivo do aplicativo web é garantir que o conteúdo seja carregado da camada do autor quando o aplicativo for aberto por autores no editor e carregado da camada de publicação quando o aplicativo for acessado por visitantes.

## Detecção da camada no aplicativo {#detecting}

Para determinar se a camada do autor ou de publicação deve ser acessada, uma simples declaração condicional pode ser utilizada no aplicativo ao detectar que seu conteúdo está sendo aberto no editor, a fim de escolher o ponto de acesso apropriado do autor ou da publicação.

Outra opção é implantar o aplicativo em dois ambientes configurados de forma diferente, para que um recupere o conteúdo da camada do autor e o outro o recupere da camada de publicação. Para permitir que os autores abram o URL publicado no Editor universal, um pequeno script pode ser criado para &quot;converter&quot; o URL do lado da publicação para seu equivalente no ambiente do autor (por exemplo, anexando um `author` subdomínio), para que os autores sejam automaticamente redirecionados.

## Resumo {#summary}

O Editor universal não impõe nenhum padrão específico, de modo que a implementação possa alcançar melhor os seus objetivos de uma forma totalmente dissociada, mantendo um processo simples e direto para a implementação.

Da mesma forma, o Editor universal não estabelece nenhum requisito sobre como um projeto específico deve se comportar ao determinar de qual camada fornecer o conteúdo. Em vez disso, permite várias possibilidades e que o projeto determine qual solução é a melhor para suas próprias necessidades.
