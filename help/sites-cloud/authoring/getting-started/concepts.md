---
title: Conceitos de criação
description: Conceitos de criação no AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Criação Conceitos {#authoring-concepts}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Elas interagem para permitir que você disponibilize conteúdo em seu site, para que seus visitantes possam acessá-lo.

O ambiente do autor fornece os mecanismos para criar, atualizar e revisar esse conteúdo antes de publicá-lo:

* Um autor cria e revisa o conteúdo. O conteúdo pode ser de vários tipos diferentes, como páginas, ativos, publicações etc.
* Este conteúdo será, em algum momento, publicado em seu site.

![Diagrama do autor, editor e despachantes](/help/sites-cloud/authoring/assets/author-publish.png)

No ambiente do autor, a funcionalidade do AEM é disponibilizada pela interface de criação do AEM. Para o ambiente de publicação, você projeta toda a aparência e comportamento da interface disponível para os usuários.

>[!NOTE]
>
>O próprio AEM é usado para publicar a documentação do AEM.

## Ambiente de criação {#author-environment}

O autor trabalha no que é conhecido como ambiente **do** autor. Isso fornece uma interface fácil de usar (interface gráfica do usuário (GUI ou UI)) para criar o conteúdo. Exige que o autor faça logon usando uma conta que recebeu os direitos de acesso apropriados.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados para criar, editar ou publicar conteúdos.

Dependendo do modo como sua instância e seus direitos de acesso pessoais estão configurados, você pode executar muitas tarefas no seu conteúdo, incluindo (dentre outras):

* Geração de novo conteúdo ou edição de conteúdo existente em uma página
* Uso de modelos predefinidos para criar novas páginas de conteúdo
* Criação, edição e gerenciamento de ativos e coleções
* Mover, copiar e excluir páginas de conteúdo, ativos etc.
* Publicar (ou desfazer a publicação) páginas, ativos etc.

Além disso, há tarefas administrativas que o ajudam a gerenciar seu conteúdo:

* Fluxos de trabalho que controlam como as alterações são gerenciadas, como impor uma revisão antes da publicação
* Projetos que coordenam tarefas individuais

>[!NOTE]
>
>O AEM também é administrado a partir do ambiente do autor.

## Ambiente de publicação {#publish-environment}

When ready, your site&#39;s content is published to the **publish environment**. Aqui, as páginas do site são disponibilizadas ao público-alvo pretendido de acordo com a aparência da interface projetada.

Para obter mais informações sobre como publicar e cancelar a publicação de páginas, consulte o documento [Publicando páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](/help/implementing/dispatcher/overview.md)**implements load balancing and caching.
