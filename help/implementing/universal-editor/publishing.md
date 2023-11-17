---
title: Publicação de conteúdo com o Editor universal
description: Saiba como o Editor universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 94%

---


# Publicação de conteúdo com o Editor universal {#publishing}

Saiba como o Editor universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.

## Semelhanças com o AEM {#similarities}

Para usuários do AEM, o processo de publicação de conteúdo do Editor universal funciona como de costume: ao publicar no AEM, o conteúdo é replicado da camada do autor para a camada de publicação.

## Diferenças {#differences}

O que torna a publicação com o Editor universal um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Editor universal possibilita.

Quando hospedado externamente, o objetivo do aplicativo web é garantir que o conteúdo seja carregado da camada do autor quando o aplicativo for aberto por autores no editor e carregado da camada de publicação quando o aplicativo for acessado por visitantes.

## Detecção da camada no aplicativo {#detecting}

Para determinar se a camada do autor ou de publicação deve ser acessada, uma simples declaração condicional pode ser utilizada no aplicativo ao detectar que seu conteúdo está sendo aberto no editor, a fim de escolher o ponto de acesso apropriado do autor ou da publicação.

Outra opção é implantar o aplicativo em dois ambientes configurados de forma diferente, para que um recupere o conteúdo da camada do autor e o outro o recupere da camada de publicação. Para permitir que autores(as) abram a URL publicada no Editor universal, um pequeno script pode ser criado para “converter” a URL do lado da publicação para seu equivalente no ambiente de criação (por exemplo, anexando um subdomínio `author`), a fim de que eles(as) sejam redirecionados automaticamente.

## Resumo {#summary}

O Editor universal não impõe nenhum padrão específico, de modo que a implementação possa alcançar melhor os seus objetivos de uma forma totalmente dissociada, mantendo um processo simples e direto para a implementação.

Da mesma forma, o Editor universal não estabelece nenhum requisito sobre como um projeto específico deve se comportar ao determinar de qual camada fornecer o conteúdo. Em vez disso, permite várias possibilidades e que o projeto determine qual solução é a melhor para suas próprias necessidades.
