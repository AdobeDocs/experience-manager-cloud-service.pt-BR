---
title: Alterações notáveis nos sites AEM no serviço da AEM Cloud
description: 'Alterações notáveis nos sites AEM no serviço da AEM Cloud '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Alterações notáveis em sites AEM como um serviço na nuvem {#notable-changes}

O AEM Sites como um serviço em nuvem fornece recursos de gerenciamento de experiência como parte do AEM nativo da nuvem como uma plataforma de serviço em nuvem. Além dos principais benefícios do AEM como um serviço em nuvem, como escalabilidade nativa da nuvem, tempo de atividade e sempre atualizado, o AEM Sites como um serviço em nuvem também fornece várias alterações e adições específicas do Sites.

>[!NOTE]
>Este documento destaca as alterações importantes no AEM Sites. Para obter alterações gerais no AEM na nuvem, consulte:
>
>* [Alterações notáveis no Adobe Experience Manager (AEM) como um serviço em nuvem](/help/release-notes/aem-cloud-changes.md)


As alterações e adições no AEM Sites como um serviço em nuvem são as seguintes:

* [Operações assíncronas de página](#asynchronous-page-operations)
* [Novo site de referência e tutorial](#new-reference-site-and-tutorial)

## Operações assíncronas de página {#asynchronous-page-operations}

No serviço da AEM Cloud, as operações que tradicionalmente bloquearam a interface do usuário foram divididas em tarefas menores que são executadas em segundo plano.

* Mover páginas
* Páginas de implantação

O iniciador dessas ações pode verificar seu status em uma nova interface do usuário em `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>O usuário do sistema não precisa alterar esse novo recurso. Isso é notado aqui simplesmente como uma mudança no comportamento de versões anteriores do AEM no local.

## Novo site de referência e tutorial {#new-reference-site-and-tutorial}

[O WKND](https://wknd.site/), um novo site de referência do AEM, foi atualizado e publicado para refletir as práticas recomendadas para a criação de um site com o AEM, e o conjunto abrangente de recursos, componentes e modelos de implantação disponíveis no AEM. O novo site de referência e o tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha abordam tópicos fundamentais como configuração de projeto, Componentes principais, Modelos editáveis, bibliotecas de clientes e desenvolvimento de componentes com os Sites do Adobe Experience Manager.

Anteriormente, o We.Retail era instalado por padrão com o AEM (exceto quando iniciado no modo de produção).  Agora, um site de referência não será instalado por padrão a partir de agora.  Em vez disso, o [git repo](https://github.com/adobe/aem-guides-wknd/) e o tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) que o acompanha com o código do site de referência WKND atualizado são fornecidos.

## Recursos não disponíveis em tempo de execução {#capabilities-not-available-at-runtime}

O AEM como um serviço em nuvem está sempre ativado e sempre atualizado. Para isso, é necessário separar o repositório do AEM em conteúdo imutável e mutável, além de proibir o acesso a conteúdo imutável em tempo de execução. Para obter mais detalhes sobre o conteúdo mutável ou imutável, consulte Áreas [mutáveis vs. imutáveis do repositório](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado do conteúdo imutável estar inacessível no tempo de execução, as seguintes operações do AEM Sites não estão disponíveis no tempo de execução:

* Tradução do dicionário i18n
* Modo de desenvolvedor no editor de página do AEM Sites

Esses recursos podem ser usados por meio de instâncias de desenvolvedor independentes e locais do AEM como um serviço em nuvem, para atualizar o conteúdo e o código no AEM como um repositório GIT do serviço em nuvem, mas não em instâncias de tempo de execução hospedadas.
