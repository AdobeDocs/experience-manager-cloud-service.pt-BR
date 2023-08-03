---
title: Conceitos de criação
description: Saiba mais sobre os conceitos de criação no AEM, usando os ambientes de criação, visualização e publicação.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 31e6ec8e9977c8787e14481ee3a94df767262aec
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 40%

---

# Conceitos de criação {#authoring-concepts}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Esses ambientes interagem para permitir que você disponibilize conteúdo no seu site para que os visitantes possam acessá-lo.

O ambiente de criação oferece os mecanismos para criação, atualização e análise desse conteúdo, antes de realmente publicá-lo:

* Um autor cria e revisa o conteúdo. O conteúdo pode ser de vários tipos diferentes, incluindo páginas, ativos e publicações.
* Esse conteúdo será, em algum ponto, publicado no site.

![Diagrama do autor, editor e despachantes](/help/sites-cloud/authoring/assets/author-publish.png)

No ambiente de criação, a funcionalidade do AEM é disponibilizada por meio da interface do usuário de criação do AEM. Para o ambiente de publicação, você projeta toda a aparência e comportamento da interface disponibilizada para os usuários.

## Ambiente de criação {#author-environment}

O autor trabalha no que é conhecido como **ambiente do autor**. Esse ambiente fornece uma interface fácil de usar (interface gráfica do usuário (GUI ou UI)) para criar o conteúdo. Exige que o autor faça logon usando uma conta que receba os direitos de acesso apropriados.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados para criar, editar ou publicar conteúdo.

Dependendo de como sua instância e seus direitos de acesso pessoal estão configurados, você pode executar muitas tarefas no conteúdo, incluindo (entre outras):

* Geração de conteúdo novo ou edição do conteúdo existente em uma página
* Utilização de modelos predefinidos para criar páginas de conteúdo
* Criação, edição e gerenciamento de ativos e coleções
* Movimentação, cópia e exclusão de páginas de conteúdo e ativos.
* Publicar (ou desfazer a publicação) páginas e ativos.

Além disso, há tarefas administrativas que ajudam você a gerenciar seu conteúdo:

* Fluxos de trabalho que controlam como as alterações são gerenciadas, como impor uma análise antes da publicação
* Projetos que coordenam tarefas individuais

>[!NOTE]
>
>O AEM também é administrado no ambiente do autor.

## Visualização de conteúdo {#previewing-content}

O AEM também oferece um serviço de visualização do Sites que permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Consulte [Visualização de conteúdo](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obter mais detalhes.

## Ambiente de publicação {#publish-environment}

Quando pronto, o conteúdo do site é publicado no **ambiente de publicação**. Aqui, as páginas do site são disponibilizadas para o público desejado de acordo com a aparência da interface projetada.

Para obter mais informações sobre publicação e cancelamento da publicação de páginas, consulte o documento [Publicação de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

Para otimizar o desempenho para os visitantes do seu site, a variável **[Dispatcher](/help/implementing/dispatcher/overview.md)** O implementa o balanceamento de carga e o cache.
