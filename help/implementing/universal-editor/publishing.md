---
title: Publicação de conteúdo com o Editor visual universal
description: Saiba como o Editor visual universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
source-git-commit: 7eeebade0255263a240476bc32f9530574495751
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Publicação de conteúdo com o Editor visual universal {#publishing}

Saiba como o Editor visual universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.

## Semelhanças com AEM {#similarities}

Para usuários de AEM, o processo para publicar conteúdo com o Universal Visual Editor funciona conforme você está acostumado: na publicação no AEM, o conteúdo é replicado do nível de criação para o nível de publicação.

## Diferenças {#differences}

O que torna a publicação com o Universal Visual Editor um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Universal Editor permite.

Quando hospedado externamente, o objetivo do aplicativo da Web é garantir que o conteúdo seja carregado da camada do autor quando o aplicativo for aberto por autores no editor e carregado da camada de publicação quando o aplicativo for acessado por visitantes.

## Detecção da camada no aplicativo {#detecting}

Determinar se o nível de criação ou publicação deve ser acessado pode ser obtido por uma simples declaração condicional no aplicativo para escolher o ponto de extremidade de autor ou publicação apropriado ao detectar que seu conteúdo está sendo aberto no editor.

Outra opção é implantar o aplicativo em dois ambientes diferentes, que são configurados de forma diferente, para que você recupere seu conteúdo do nível de criação e um que o recupere do nível de publicação. Para permitir que os autores abram o URL publicado no Editor Universal, um pequeno script pode ser criado para &quot;converter&quot; o URL do lado da publicação para seu equivalente no ambiente de criação (por exemplo, ao anexar um `author` (subdomínio), para que os autores sejam redirecionados automaticamente.

## Resumo {#summary}

O objetivo do Editor Universal é não impor qualquer padrão específico, de modo que a implementação possa alcançar melhor os seus objetivos de uma forma totalmente dissociada, mantendo ao mesmo tempo tudo simples e inovador para a implementação.

Da mesma forma, o Editor Universal não faz nenhum requisito sobre como qualquer projeto específico deve continuar determinando a partir de qual camada fornecer o conteúdo. Em vez disso, ele permite várias possibilidades e permite que o projeto determine qual solução é a melhor para suas próprias necessidades.
