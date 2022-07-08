---
title: Conceitos de criação
description: Conceitos de criação no AEM
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '349'
ht-degree: 100%

---

# Conceitos de criação {#authoring-concepts}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Eles interagem para permitir que você disponibilize conteúdo no site, para que os visitantes possam acessá-lo.

O ambiente de criação oferece os mecanismos para criação, atualização e análise desse conteúdo, antes de realmente publicá-lo:

* Um autor cria e revisa o conteúdo. O conteúdo pode ser de vários tipos diferentes, como páginas, ativos, publicações, etc.
* Esse conteúdo será, em algum ponto, publicado no site.

![Diagrama do autor, editor e despachantes](/help/sites-cloud/authoring/assets/author-publish.png)

No ambiente de criação, a funcionalidade do AEM é disponibilizada por meio da interface do usuário do AEM. Para o ambiente de publicação, você projeta toda a aparência e comportamento da interface disponível para os usuários.

## Ambiente de criação {#author-environment}

O autor trabalha no que é conhecido como **ambiente do autor**. Isso oferece uma interface fácil de usar (interface gráfica do usuário (GUI ou UI)) para criar o conteúdo. Exige que o autor faça logon usando uma conta que recebeu os direitos de acesso apropriados.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados para criar, editar ou publicar conteúdos.

Dependendo do modo como sua instância e seus direitos de acesso pessoais estão configurados, você pode executar muitas tarefas no seu conteúdo, incluindo (dentre outras):

* Geração de conteúdo novo ou edição do conteúdo existente em uma página
* Uso de modelos predefinidos para criar novas páginas de conteúdo
* Criação, edição e gerenciamento de ativos e coleções
* Transferência, cópia e exclusão das páginas de conteúdo, ativos, etc.
* Publicação (ou cancelamento da publicação) de páginas, ativos, etc.

Além disso, há tarefas administrativas que o ajudam a gerenciar seu conteúdo:

* Fluxos de trabalho que controlam como as alterações são gerenciadas, como impor uma análise antes da publicação
* Projetos que coordenam tarefas individuais

>[!NOTE]
>
>O AEM também é administrado no ambiente do autor.

## Ambiente de publicação {#publish-environment}

Quando pronto, o conteúdo do site é publicado no **ambiente de publicação**. Aqui, as páginas do site são disponibilizadas para o público desejado de acordo com a aparência da interface projetada.

Para obter mais informações sobre publicação e cancelamento da publicação de páginas, consulte o documento [Publicação de páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

Para otimizar o desempenho para os visitantes do seu site, o **[dispatcher](/help/implementing/dispatcher/overview.md)** implementa o balanceamento de carga e o cache.
