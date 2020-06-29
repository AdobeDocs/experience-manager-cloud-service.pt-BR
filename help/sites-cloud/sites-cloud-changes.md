---
title: Alterações importantes para o AEM Sites no AEM Cloud Service
description: 'Alterações importantes para o AEM Sites no AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 16%

---


# Alterações importantes para AEM Sites as a Cloud Service {#notable-changes}

O AEM Sites como Cloud Service fornece recursos de gerenciamento de experiência como parte do AEM nativo da nuvem como uma plataforma Cloud Service. Além dos principais benefícios do AEM como um Cloud Service, como a escalabilidade nativa da nuvem, o tempo de atividade e sempre atualizado, os AEM Sites como Cloud Service também oferecem diversas alterações e adições específicas do Sites.

>[!NOTE]
>Este documento destaca as mudanças notáveis nos AEM Sites. Para obter as alterações gerais no AEM como Cloud Service e em outros módulos, consulte:
>
>* [Uma introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Uma [visão geral do AEM como um Cloud Service - Novidades e diferentes](/help/overview/what-is-new-and-different.md)
>* A [Arquitetura](/help/core-concepts/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações notáveis no AEM como Cloud Service (Notas de versão)](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Apresentando AEM Assets como Cloud Service](/help/assets/overview.md)
>* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/br/experience-manager-learn/cloud-service/overview.html)


As alterações e adições em AEM Sites como Cloud Service são as seguintes:

* [Operações assíncronas de página](#asynchronous-page-operations)
* [Novo site de referência e tutorial](#new-reference-site-and-tutorial)

## Operações assíncronas de página {#asynchronous-page-operations}

No serviço da AEM Cloud, as operações que tradicionalmente bloquearam a interface do usuário foram divididas em tarefas menores executadas em segundo plano.

* Mover páginas
* Páginas de implantação

O iniciador dessas ações pode verificar seu status em uma nova interface do usuário em `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>O usuário do sistema não precisa alterar esse novo recurso. Isso é notado aqui simplesmente como uma mudança no comportamento de versões anteriores do AEM no local.

## Novo site de referência e tutorial {#new-reference-site-and-tutorial}

[O WKND](https://wknd.site/), um novo site de referência do AEM, foi atualizado e publicado para refletir as práticas recomendadas para a criação de um site com o AEM, e o conjunto abrangente de recursos, componentes e modelos de implantação disponíveis no AEM. O novo site de referência e o tutorial [](https://docs.adobe.com/content/help/br/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha abordam tópicos fundamentais como configuração de projeto, Componentes principais, Modelos editáveis, bibliotecas de clientes e desenvolvimento de componentes com Sites Adobe Experience Manager.

Anteriormente, o We.Retail era instalado por padrão com o AEM (exceto quando iniciado no modo de produção).  Agora, um site de referência não será instalado por padrão a partir de agora.  Em vez disso, o [git repo](https://github.com/adobe/aem-guides-wknd/) e o tutorial [](https://docs.adobe.com/content/help/br/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha com o código do site de referência WKND atualizado são fornecidos.

## Recursos não disponíveis em tempo de execução {#capabilities-not-available-at-runtime}

O AEM como Cloud Service está sempre ativo e sempre atualizado. Para isso, é necessário separar o repositório do AEM em conteúdo imutável e mutável, além de proibir o acesso a conteúdo imutável em tempo de execução. Para obter mais detalhes sobre o conteúdo mutável ou imutável, consulte Áreas [mutáveis vs. imutáveis do repositório](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado do conteúdo imutável estar inacessível no tempo de execução, as seguintes operações de AEM Sites não estão disponíveis no tempo de execução:

* Tradução do dicionário i18n
* Modo de desenvolvedor no editor de páginas do AEM Sites

Esses recursos podem ser usados por meio de instâncias de desenvolvedor independentes e locais do AEM como um Cloud Service, para atualizar o conteúdo e o código no AEM como um repositório GIT de Cloud Service, mas não em instâncias de tempo de execução hospedadas.
