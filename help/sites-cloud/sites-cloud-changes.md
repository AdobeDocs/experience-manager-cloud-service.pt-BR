---
title: Alterações importantes do AEM Sites no AEM Cloud Service
description: Entenda como administrar e criar com o AEM Sites as a Cloud Service e conheça as principais alterações no AEM Sites no AEM Cloud Service.
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 88%

---


# Alterações importantes no AEM Sites as a Cloud Service {#notable-changes}

O AEM Sites as a Cloud Service oferece recursos de gerenciamento de experiência como parte da plataforma AEM as a Cloud Service nativa na nuvem. Além dos principais benefícios do AEM as a Cloud Service, como escalabilidade nativa em nuvem, tempo de atividade e estar sempre atualizado, o AEM Sites as a Cloud Service também fornece várias alterações e adições específicas do Sites.

>[!NOTE]
>Este documento destaca as alterações importantes no AEM Sites. Para conhecer as alterações gerais no AEM as a Cloud Service e em outros módulos, consulte:
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

No AEM Cloud Service, as operações que tradicionalmente bloqueavam a interface foram divididas em tarefas menores que são executadas em segundo plano.

* Mover páginas
* Páginas de implantação

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

Você pode exibir o status de trabalhos assíncronos no [painel Operações em Segundo Plano](/help/operations/asynchronous-jobs.md).

>[!NOTE]
>
>Não é necessário que o usuário do sistema faça alterações para usar esse novo recurso. Isso é registrado aqui simplesmente como uma mudança de comportamento em relação a versões anteriores do AEM no local.

## Novo site de referência e tutorial {#new-reference-site-and-tutorial}

O [WKND](https://wknd.site/), um novo site de referência do AEM, foi atualizado e publicado para refletir as práticas recomendadas de criação de sites do AEM e o conjunto abrangente de recursos, componentes e modelos de implantação que estão disponíveis no AEM. O novo site de referência e o [tutorial de acompanhamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) abordam tópicos fundamentais como a configuração de projetos, componentes principais, modelos editáveis, bibliotecas de clientes e o desenvolvimento de componentes com o Adobe Experience Manager Sites.

Anteriormente, o We.Retail vinha instalado por padrão com o AEM (exceto quando iniciado no modo de produção). No AEM as a Cloud Service, o site de referência não é instalado por padrão. Em vez disso, o [git repo](https://github.com/adobe/aem-guides-wknd/) e o [tutorial de acompanhamento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) com o código atualizado do site de referência WKND será fornecido.

## Recursos não disponíveis em Tempo de execução {#capabilities-not-available-at-runtime}

O AEM as a Cloud Service está sempre ativo e sempre atualizado. Para isso, é necessário separar o repositório do AEM em conteúdo imutável e mutável, proibindo o acesso a conteúdo imutável no tempo de execução. Para obter mais detalhes sobre conteúdo mutável ou imutável, consulte [Áreas mutáveis versus imutáveis do repositório](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado do conteúdo imutável estar inacessível no tempo de execução, as seguintes operações do AEM Sites não estão disponíveis no tempo de execução:

* Tradução de dicionário i18n
* Modo de desenvolvedor no editor de páginas do AEM Sites

Esses recursos podem ser usados por meio de instâncias de desenvolvedor independentes e locais do AEM as a Cloud Service, para atualizar o conteúdo e o código no repositório GIT do AEM as a Cloud Service, mas não em instâncias de tempo de execução hospedadas.
