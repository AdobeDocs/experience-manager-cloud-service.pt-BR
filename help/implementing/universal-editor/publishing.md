---
title: Publicação de conteúdo com o Editor visual universal
description: Saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 78%

---

# Publicação de conteúdo com o Editor visual universal {#publishing}

Saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.

## Semelhanças com o AEM {#similarities}

Para usuários do AEM, o processo de publicação de conteúdo do Editor visual universal funciona como de costume: ao publicar no AEM, o conteúdo é replicado da camada do autor para a camada de publicação.

## Diferenças {#differences}

O que torna a publicação com o Editor visual universal um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Editor universal possibilita.

Quando hospedado externamente, o objetivo do aplicativo web é garantir que o conteúdo seja carregado da camada do autor quando o aplicativo for aberto por autores no editor e carregado da camada de publicação quando o aplicativo for acessado por visitantes.

## Detecção da camada no aplicativo {#detecting}

Para determinar se a camada do autor ou de publicação deve ser acessada, uma simples declaração condicional pode ser utilizada no aplicativo ao detectar que seu conteúdo está sendo aberto no editor, a fim de escolher o ponto de acesso apropriado do autor ou da publicação.

Outra opção é implantar o aplicativo em dois ambientes configurados de forma diferente, para que um recupere o conteúdo da camada do autor e o outro o recupere da camada de publicação. Para permitir que os autores abram o URL publicado no Editor universal, um pequeno script pode ser criado para &quot;converter&quot; o URL do lado da publicação para seu equivalente no ambiente do autor (por exemplo, anexando um `author` subdomínio), para que os autores sejam automaticamente redirecionados.

## Resumo {#summary}

O objetivo do Editor Universal é não impor qualquer padrão específico, de modo que a implementação possa melhor alcançar seus objetivos de uma maneira totalmente dissociada, mantendo tudo simples e direto para a implementação.

Da mesma forma, o Editor universal não estabelece nenhum requisito sobre como um projeto específico deve se comportar ao determinar de qual camada fornecer o conteúdo. Em vez disso, ele proporciona várias possibilidades e permite que o projeto determine qual solução é a melhor para seus próprios requisitos.
