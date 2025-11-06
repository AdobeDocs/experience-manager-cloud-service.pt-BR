---
title: Como o editor universal publica conteúdo
description: Saiba como o Editor universal publica seu conteúdo, como ele difere do processo no Console de sites e considerações ao desenvolver seus próprios aplicativos para trabalhar com ele.
feature: Developing
role: Admin, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 25%

---

# Como o editor universal publica conteúdo {#publishing}

Saiba como o Editor universal publica seu conteúdo, como ele difere do processo no Console de sites e considerações ao desenvolver seus próprios aplicativos para trabalhar com ele.

>[!TIP]
>
>Este artigo aborda detalhes do processo de publicação do Editor universal para o desenvolvedor. Para o autor do conteúdo, [o processo de publicação do conteúdo está descrito aqui.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Semelhanças com o processo do console Sites {#similarities}

Para usuários do [Editor de Páginas do AEM](/help/sites-cloud/authoring/page-editor/introduction.md) e do [Console de Sites](/help/sites-cloud/authoring/sites-console/introduction.md), o processo de publicação de conteúdo com o Editor Universal funciona como você está acostumado: na publicação no AEM, o conteúdo é replicado do serviço de autoria para o serviço de publicação (ou para o [serviço de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md), se disponível, e dependendo das opções que o autor escolher ao publicar.)

## Diferenças {#differences}

O que torna a publicação com o Editor Universal um pouco diferente não é tanto o próprio editor, mas sim a hospedagem externa do aplicativo que o Editor Universal possibilita.

Quando hospedado externamente, é preocupação do aplicativo web garantir que o conteúdo seja carregado do serviço do autor quando o aplicativo for aberto por autores no editor e carregado do serviço de publicação quando o aplicativo for acessado por visitantes.

## Detecção do serviço no aplicativo {#detecting}

Determinar se o serviço de autoria ou publicação deve ser acessado pode ser realizado por uma simples declaração condicional no aplicativo para escolher o ponto de extremidade de autoria ou publicação apropriado ao detectar que está sendo aberto no editor.

Outra opção é implantar o aplicativo em dois ambientes diferentes que são configurados de forma diferente, para que um recupere o conteúdo do serviço de autoria e outro que o recupere do serviço de publicação. Para permitir que os autores abram a URL publicada no Editor Universal, um pequeno script pode ser criado para &quot;converter&quot; a URL do lado da publicação para seu equivalente no ambiente do autor (por exemplo, anexando um subdomínio `author`), para que os autores sejam automaticamente redirecionados.

## Resumo {#summary}

O Editor universal não impõe nenhum padrão específico, de modo que a implementação possa alcançar melhor os seus objetivos de uma forma totalmente dissociada, mantendo um processo simples e direto para a implementação.

Da mesma forma, o Editor Universal não faz requisitos sobre como um projeto específico deve determinar a partir de qual serviço entregar o conteúdo. Em vez disso, permite várias possibilidades e que o projeto determine qual solução é a melhor para suas próprias necessidades.

## Recursos adicionais {#additional-resources}

Para saber mais sobre os detalhes técnicos do Universal Editor, consulte estes documentos do desenvolvedor.

* [Introdução ao Editor universal](/help/implementing/universal-editor/introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.
* [Introdução ao Editor universal no AEM](/help/implementing/universal-editor/getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](/help/implementing/universal-editor/architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](/help/implementing/universal-editor/attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](/help/implementing/universal-editor/authentication.md): saiba como funciona a autenticação do Editor universal.
