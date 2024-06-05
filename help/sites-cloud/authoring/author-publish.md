---
title: Conceitos de criação e publicação
description: Saiba mais sobre os conceitos de criação no AEM, usando os ambientes de criação, visualização e publicação.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 29%

---


# Conceitos de criação e publicação {#authoring-publishing}

Para um autor de conteúdo, uma instalação as a Cloud Service do AEM pode ser considerada como três camadas principais em seu nível mais básico

* Nível de criação
* Camada de visualização
* Publicar camada

Esses níveis interagem para permitir que você disponibilize conteúdo no seu site para que os visitantes possam acessá-lo. O fluxo de trabalho básico é:

1. Os autores de conteúdo criam seu conteúdo usando o nível de criação.
1. Os autores de conteúdo disponibilizam seu conteúdo para que os revisores visualizem usando o nível de visualização.
1. Quando o conteúdo estiver pronto para consumo público, os autores publicam o conteúdo usando o nível de publicação.

O conteúdo pode ser de vários tipos diferentes, incluindo páginas, ativos e publicações. A visualização do conteúdo pode ser ignorada a critério do autor.

![Diagrama do autor, editor e despachantes](assets/author-publish.jpg)

Para mais detalhes sobre a arquitetura técnica do AEM as a Cloud Service, consulte o documento [Uma introdução à arquitetura do Adobe Experience Manager as a Cloud Service.](/help/overview/architecture.md)

{{edge-delivery-authoring}}

## Criar conteúdo {#author-environment}

O ambiente de criação do nível do autor fornece uma interface gráfica de usuário fácil de usar para a criação de conteúdo. É necessário que o(a) autor(a) faça logon usando uma conta que possua os direitos de acesso apropriados.

Dependendo de como sua instância e seus direitos de acesso pessoal estão configurados, é possível executar muitas tarefas no conteúdo, incluindo (entre outras):

* Geração de um novo conteúdo ou edição do conteúdo existente em uma página
* Uso de modelos predefinidos para criar páginas de conteúdo
* Criação, edição e gerenciamento de ativos e coleções
* Mover, copiar e excluir páginas de conteúdo e ativos.
* Publicar (ou desfazer a publicação de) páginas e ativos.

Além disso, há tarefas administrativas que ajudam a gerenciar o conteúdo:

* Fluxos de trabalho que controlam como as alterações são gerenciadas, como impor uma análise antes da publicação
* Projetos que coordenam tarefas individuais

O AEM também é administrado no ambiente do autor.

Consulte o documento [Guia de início rápido para criação](/help/sites-cloud/authoring/quick-start.md) para obter uma visão geral do processo de criação.

## Visualização de conteúdo {#previewing-content}

O AEM também oferece um serviço de visualização que permite que desenvolvedores e autores de conteúdo visualizem a experiência final de um site antes que ele chegue ao ambiente de publicação e esteja disponível publicamente.

Consulte o documento [Visualização de conteúdo](/help/sites-cloud/authoring/sites-console/previewing-content.md) para obter mais detalhes.

## Ambiente de publicação {#publish-environment}

Quando pronto, o conteúdo do site é publicado no ambiente de publicação do nível de publicação. Aqui, as páginas do site são disponibilizadas para o público desejado de acordo com a aparência do seu modelo de conteúdo.

Consulte o documento [Publicar páginas](/help/sites-cloud/authoring/sites-console/publishing-pages.md) para obter mais informações sobre publicação e cancelamento da publicação de páginas.

## Dispatcher {#dispatcher}

Para otimizar o desempenho para os visitantes do seu site, a variável **[Dispatcher](/help/implementing/dispatcher/overview.md)** O implementa o balanceamento de carga e o cache para os níveis de publicação e visualização.
