---
title: Alterações importantes para o AEM Sites no AEM Cloud Service
description: 'Alterações importantes para o AEM Sites no AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 21%

---


# Alterações importantes no AEM Sites as a Cloud Service {#notable-changes}

A AEM Sites como Cloud Service oferece recursos de gerenciamento de experiência como parte da AEM nativa da nuvem como uma plataforma Cloud Service. Além dos principais benefícios do AEM como Cloud Service, como a escalabilidade nativa da nuvem, o tempo de atividade e sempre atualizado, o AEM Sites como Cloud Service também fornece diversas mudanças e adições específicas do Sites.

>[!NOTE]
>Este documento destaca as mudanças notáveis no AEM Sites. Para obter as alterações gerais para AEM como Cloud Service, e outros módulos, consulte:
>
>* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* a [Visão geral do AEM as a Cloud Service: novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* A [Arquitetura](/help/core-concepts/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações importantes no AEM as a Cloud Service (notas de versão)](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Apresentando a AEM Assets como Cloud Service](/help/assets/overview.md)
>* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


As alterações e adições no AEM Sites como Cloud Service são as seguintes:

* [Operações assíncronas de página](#asynchronous-page-operations)
* [Novo site de referência e tutorial](#new-reference-site-and-tutorial)

## Operações assíncronas de página {#asynchronous-page-operations}

No serviço AEM Cloud, as operações que tradicionalmente bloquearam a interface do usuário foram divididas em tarefas menores que são executadas em segundo plano.

* Mover páginas
* Páginas de implantação

O iniciador dessas ações pode verificar seu status em uma nova interface do usuário em `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>O usuário do sistema não precisa alterar esse novo recurso. Isso é notado aqui simplesmente como uma mudança no comportamento de versões anteriores de AEM no local.

## Novo site de referência e tutorial {#new-reference-site-and-tutorial}

[A WKND](https://wknd.site/), um novo site de referência AEM, foi atualizada e publicada para refletir as práticas recomendadas para a criação de um site com AEM, e o conjunto abrangente de recursos, componentes e modelos de implantação disponíveis em AEM. O novo site de referência e o tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha abordam tópicos fundamentais como configuração de projeto, Componentes principais, Modelos editáveis, bibliotecas de clientes e desenvolvimento de componentes com a Adobe Experience Manager Sites.

Anteriormente, We.Retail era instalado por padrão com AEM (exceto quando iniciado no modo de produção).  Agora, um site de referência não será instalado por padrão a partir de agora.  Em vez disso, o [git repo](https://github.com/adobe/aem-guides-wknd/) e o tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha com o código do site de referência WKND atualizado são fornecidos.

## Recursos não disponíveis em tempo de execução {#capabilities-not-available-at-runtime}

AEM como Cloud Service está sempre ativada e sempre atualizada. Para alcançar isso, é necessário separar o repositório AEM em conteúdo imutável e mutável, além de proibir o acesso a conteúdo imutável em tempo de execução. Para obter mais detalhes sobre o conteúdo mutável ou imutável, consulte Áreas [mutáveis vs. imutáveis do repositório](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado do conteúdo imutável estar inacessível no tempo de execução, as seguintes operações do AEM Sites não estão disponíveis no tempo de execução:

* Tradução do dicionário i18n
* Modo de desenvolvedor no AEM Sites Page Editor

Esses recursos podem ser usados por meio de instâncias de desenvolvedor independentes e locais de AEM como Cloud Service, para atualizar o conteúdo e o código no AEM como um repositório GIT Cloud Service, mas não em instâncias de tempo de execução hospedadas.
