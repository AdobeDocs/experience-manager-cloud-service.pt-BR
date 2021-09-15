---
title: Alterações importantes para o AEM Sites no AEM Cloud Service
description: Alterações importantes para o AEM Sites no AEM Cloud Service
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 17%

---

# Alterações importantes no AEM Sites as a Cloud Service {#notable-changes}

O AEM Sites as a Cloud Service fornece recursos de gerenciamento de experiência como parte do AEM nativo em nuvem como uma plataforma de Cloud Service. Além dos principais benefícios do AEM as a Cloud Service, como escalabilidade nativa em nuvem, tempo de atividade e sempre atualizado, o AEM Sites as a Cloud Service também fornece diversas alterações e adições específicas do Sites.

>[!NOTE]
>Este documento destaca as alterações importantes no AEM Sites. Para obter as alterações gerais em AEM como Cloud Service e outros módulos, consulte:
>
>* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* a [Visão geral do AEM as a Cloud Service: novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* A [Arquitetura](/help/overview/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações importantes no AEM as a Cloud Service (notas de versão)](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Apresentação do AEM Assets as a Cloud Service](/help/assets/overview.md)
>* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=pt-BR)


As alterações e adições no AEM Sites as a Cloud Service são as seguintes:

* [Operações assíncronas de página](#asynchronous-page-operations)
* [Novo site de referência e tutorial](#new-reference-site-and-tutorial)

## Operações assíncronas de página {#asynchronous-page-operations}

No AEM Cloud Service, as operações que tradicionalmente bloquearam a interface do usuário foram divididas em tarefas menores que são executadas em segundo plano.

* Mover páginas
* Páginas de implantação

O iniciador dessas ações pode verificar seu status em uma nova interface do usuário em `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>Não é necessário que o usuário do sistema faça alterações com esse novo recurso. Isso é notado aqui simplesmente como uma mudança de comportamento de versões anteriores no local do AEM.

## Novo site de referência e tutorial {#new-reference-site-and-tutorial}

[A WKND](https://wknd.site/), um novo site de referência de AEM, foi atualizada e publicada para refletir as práticas recomendadas para criar um site com AEM e o conjunto abrangente de recursos, componentes e modelos de implantação que estão disponíveis em AEM. O novo site de referência e o [tutorial associado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) aborda tópicos fundamentais como configuração do projeto, Componentes principais, Modelos editáveis, bibliotecas de clientes e desenvolvimento de componentes com o Adobe Experience Manager Sites.

Anteriormente, o We.Retail era instalado por padrão com o AEM (exceto quando iniciado no modo de produção).  Agora, um site de referência não será instalado por padrão a partir de agora.  Em vez disso, o [git repo](https://github.com/adobe/aem-guides-wknd/) e o [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que acompanha o código do site de referência WKND atualizado são fornecidos.

## Recursos não disponíveis em Tempo de execução {#capabilities-not-available-at-runtime}

AEM como Cloud Service está sempre ativo e sempre atualizado. Para isso, é necessário separar o repositório de AEM em conteúdo imutável e mutável e proibir o acesso a conteúdo imutável no tempo de execução. Para obter mais detalhes sobre conteúdo mutável vs imutável, consulte [Áreas mutáveis vs. imutáveis do repositório](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado do conteúdo imutável estar inacessível no tempo de execução, as seguintes operações do AEM Sites não estão disponíveis no tempo de execução:

* Tradução do dicionário i18n
* Modo de desenvolvedor no editor de páginas do AEM Sites

Esses recursos podem ser usados por meio de instâncias de desenvolvedor independentes e locais do AEM como um Cloud Service, para atualizar o conteúdo e o código no AEM como um repositório GIT Cloud Service, mas não em instâncias de tempo de execução hospedadas.
