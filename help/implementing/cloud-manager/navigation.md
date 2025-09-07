---
title: Navegar na interface do usuário do Cloud Manager
description: Saiba como a interface do Cloud Manager é organizada e como navegar e gerenciar seus programas e ambientes.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 71311bfffefec8d2c2f71b0c69e6fec4ce3f299b
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 37%

---


# Navegar na interface do usuário do Cloud Manager {#navigation}

Saiba como a interface do Cloud Manager é organizada e como encontrar e gerenciar seus programas e ambientes.


A interface do Cloud Manager é composta principalmente por duas interfaces gráficas:

* [O console Meus programas](#my-programs-console), onde é possível exibir e gerenciar todos os programas.
* [A janela Visão geral do programa](#program-overview), onde é possível ver os detalhes e gerenciar um programa individual.

>[!TIP]
>
>Verifique também a [jornada de documentação de integração](/help/journey-onboarding/overview.md) para obter uma visão geral completa de como começar a usar o AEM as a Cloud Service usando o Cloud Manager.


## Assistente de IA no AEM

Para clientes que possuem [critérios de pré-requisito concluídos](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), o Assistente de IA no AEM está disponível para usuários de suas organizações. Consulte [Assistente de IA no AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).


## Console Meus programas {#my-programs-console}

Ao fazer logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecionar a organização apropriada, você acessará o console **Meus programas**.

![Console Meus programas](assets/my-programs-console.png)

O console Meus programas fornece uma visão geral de todos os programas aos quais você tem acesso na organização selecionada. Ele é composto por várias partes.

1. [Barras de ferramentas](#toolbars-my-programs-toolbars) para seleção de organização, alertas e configurações da conta
1. Guias que permitem alternar a exibição atual dos programas.
   * Exibição da **Página Inicial** (padrão) que seleciona a exibição de **Meus programas** com uma visão geral de todos os programas
   * **Licença** que acessa o [Painel de Licenças](/help/implementing/cloud-manager/license-dashboard.md).
   * Observe que o padrão de guias é fechado e pode ser revelado usando o ![ícone Mostrar menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) no [cabeçalho do Cloud Manager](#cloud-manager-header).
1. [As estatísticas e a frase de chamariz](#statistics) que fornecem uma visão geral das atividades recentes
1. Seção [**Meus programas**](#my-programs-section) que fornece uma visão geral de todos os seus programas
1. [Links rápidos](#quick-links-section) para acessar recursos relacionados facilmente.

>[!TIP]
>
>Consulte o documento [Programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obter mais detalhes sobre esse assunto.

### Barras de ferramentas {#my-programs-toolbars}

Há duas barras de ferramentas uma sobre a outra.

#### Cabeçalho do Cloud Manager {#cloud-manager-header}

A primeira é o cabeçalho do Cloud Manager, que permanece fixo ao navegar pelo Cloud Manager. Ele é uma âncora que dá acesso às configurações e informações que se aplicam aos programas do Cloud Manager.

![O cabeçalho da Experience Cloud](assets/experience-cloud-header.png)

1. Clique no ![ícone Mostrar menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) (mostrar ou ocultar menu lateral) para ter acesso a uma variedade de guias que podem levá-lo a partes específicas de um programa individual. Ou você pode alternar entre o [Painel de Licenças](/help/implementing/cloud-manager/license-dashboard.md) e o console **[Meus Programas](#my-programs-console)**, dependendo do contexto.
1. Clique no botão Adobe Cloud Manager para voltar ao console Meus programas do Cloud Manager, onde quer que você esteja no Cloud Manager.
1. Clique em **Feedback** para fornecer feedback à Adobe sobre o Cloud Manager.
1. Clique no seletor de organizações para exibir a organização na qual você está conectado no momento (neste exemplo, Foundation Internal). Clique para alternar para outra organização se a Adobe ID estiver associada a várias.
1. Clique no ![ícone Aplicativos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (alternador de Soluções) para acessar rapidamente outras soluções da Experience Cloud.
1. Clique no ![ícone da Ajuda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Help_18_N.svg) para fornecer acesso rápido aos recursos de aprendizado e suporte.
1. Clique no ![ícone de Campainha](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) ([Notificações](/help/implementing/cloud-manager/notifications.md)) para ver notificações e anúncios, entre outras coisas.
1. Clique no ícone que representa o acesso do usuário às configurações do usuário. Se você não tiver uma imagem de usuário configurada, um ícone será atribuído aleatoriamente.

#### Barra de ferramentas do programa {#program-toolbar}

A barra de ferramentas do programa fornece links para alternar entre programas e ações do Cloud Manager adequados ao contexto.

![Barra de ferramentas do programa](assets/program-toolbar.png)

1. O seletor **Meus Programas** abre uma lista suspensa onde você pode selecionar outros programas rapidamente ou realizar ações apropriadas ao contexto, como criar um novo programa
1. O link **Introdução** fornece acesso à [jornada de documentação de integração](/help/journey-onboarding/overview.md) para que você possa começar a usar o Cloud Manager.
1. O botão de ação oferece ações apropriadas ao contexto, como adicionar um programa.

### Estatísticas e frases de chamariz {#statistics}

A seção Estatísticas e call-to-action fornece dados agregados para sua organização. Por exemplo, se você tiver configurado seus programas com êxito, as estatísticas das atividades nos últimos 90 dias poderão ser exibidas, incluindo:

* Número de [implantações](/help/implementing/cloud-manager/deploy-code.md)
* Número de [problemas de qualidade de código](/help/implementing/cloud-manager/code-quality-testing.md) identificados
* Número de builds

Ou se você estiver apenas começando a configurar a organização, encontrará dicas sobre as próximas etapas ou recursos de documentação.

### seção Meus Programas {#my-programs-section}

O conteúdo principal do console **Meus Programas** é a lista de programas na seção **Meus Programas**.

A seção **Meus Programas** lista os cartões que representam cada programa. Clique em um cartão para acessar a página **Visão geral do programa** e obter detalhes sobre o programa.

>[!NOTE]
>
>Dependendo dos seus privilégios, talvez não seja possível selecionar determinados programas.


Para localizar o programa necessário com mais facilidade, use as opções de classificação.

![Opções de classificação](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Classificar por:
   * **Data de criação** (padrão)
   * **Nome do programa**
   * **Status**
* ![Ícone de Ordem de classificação regressiva](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg) Crescente (padrão) / ![Ícone de Ordem de classificação ascendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg) Decrescente
* ![Ícone de exibição de grade clássica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg) Exibição de grade (padrão)
* ![Ícone da lista de exibições](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) Exibição da lista

#### Cartões de programa {#program-cards}

Um cartão (ou linha em uma tabela) representa cada programa, fornecendo uma visão geral do programa e links rápidos para executar uma ação.

![Cartão do programa](assets/program-card.png)

* Imagem associada ao programa, se configurado. A imagem acima é &quot;WKND&quot;.
* Nome atribuído ao programa. A imagem acima mostra &quot;SecurBank Sample&quot; como o nome do programa.
* Tipo de serviço:
   * **Experience Manager Cloud** — para programas do AEM as a Cloud Service
   * **Experience Manager** — para [programas do AMS (Adobe Managed Services)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md):
   * Sandbox
   * Produção
* Status. Na imagem acima, o status é Pronto com uma marca de seleção.
* Soluções configuradas. Na imagem acima, o Sites e o Assets são as soluções configuradas.
* Data de criação.

Um programa de produção pode receber uma medalha para mostrar os recursos adicionais escolhidos no momento em que foi adicionado, como os seguintes:

* ![Selo HIPAA](assets/hipaa.png) [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* ![Selo WAF-DDOS](assets/waf-ddos-protection.png) [Proteção WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* [99,99% SLA (Service level agreement)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

O ícone de informações também fornece acesso rápido a informações adicionais sobre o programa (útil na exibição de lista).

![Informações](assets/information-list-view.png)

O ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_22/Smock_More_22_N.svg) dá a você acesso a ações adicionais que você pode realizar no programa.

![Botão de reticências para programas](assets/program-ellipsis.png)

* Navegue até um ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Data_22_N.svg) [Ambiente](/help/implementing/cloud-manager/manage-environments.md) específico do programa
* Abra o ![ícone de visão geral do programa](/help/implementing/cloud-manager/assets/program-overview.svg) [Visão geral do programa](#program-overview)
* ![Ícone Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) [Editar o programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* ![Excluir ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) [Excluir um programa de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Para obter mais informações sobre programas e adicionar e gerenciar programas, consulte o seguinte:
>
>* [Programas e Tipos de Programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Criar programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [Criar programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### Seção de Links rápidos {#quick-links-section}

A seção Links rápidos fornece acesso aos recursos comumente usados relacionados ao.

## Página de visão geral do programa {#program-overview}

Quando um programa é selecionado no console **[Meus Programas](#my-programs-console)**, você é direcionado para a página **Visão Geral do Programa**.

![Visão geral do programa](assets/program-overview.png)

A visão geral do programa fornece acesso a todos os detalhes de um programa do Cloud Manager. Assim como o console **Meus Programas**, ele é composto de várias partes.

1. [Barras de ferramentas](#program-overview-toolbar) para voltar rapidamente ao console Meus Programas e navegar pelo programa
1. [Guias](#program-tabs) para alternar entre diferentes aspectos do programa
1. Uma [frase de chamariz](#cta) baseada nas últimas ações do programa
1. Uma [visão geral dos ambientes](#environments) do programa
1. Uma [visão geral dos pipelines](#pipelines) do programa
1. Uma [visão geral do desempenho](#performance) do programa
1. Links para [recursos úteis](#useful-resources)

### Barras de ferramentas {#program-overview-toolbar}

As barras de ferramentas para a visão geral do programa são semelhantes às do [console Meus Programas](#my-programs-toolbars). Somente as diferenças são ilustradas aqui.

#### Cabeçalho do Cloud Manager {#cloud-manager-header-2}

No canto superior esquerdo da página, está o cabeçalho Cloud Manager do Adobe. Você pode clicar no ![ícone do menu lateral](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar ou ocultar o menu lateral de guias para outras áreas do software.

![menu lateral do Cloud Manager](assets/cloud-manager-hamburger.png)

Clique em Adobe Cloud Manager para retornar à Página inicial.

#### Barra de ferramentas do programa {#program-toolbar-2}

A barra de ferramentas do programa possibilita alternar rapidamente para outros programas, mas também permite acessar ações adequadas ao contexto, como adicionar e editar o programa.

![Barra de ferramentas do programa](assets/cloud-manager-program-toolbar.png)

A barra de ferramentas sempre mostra a guia em que você está no momento, mesmo que você tenha ocultado as guias usando o ![ícone Mostrar menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg).

### Guias do programa {#program-tabs}

Cada programa tem diversas opções e dados associados. Essas opções e dados são coletados em guias para simplificar a navegação pelo programa. As guias fornecem acesso a:

**Programa**

* ![Ícone de exibição de grade moderna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg) Visão geral - A visão geral do programa conforme descrito no documento atual
* ![Ícone de Campainha](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) [Atividade](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - O histórico de execuções de pipeline do programa
* ![Ícone de fluxo de trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) [Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - Todos os pipelines configurados para o programa
* ![Ícone de pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) [Repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - Todos os repositórios configurados para o programa
* ![Ícone de pizza de gráfico](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg) [Relatórios](/help/implementing/cloud-manager/sla-reporting.md) - Métricas como dados do SLA

**Serviços**

* ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) [Ambientes](/help/implementing/cloud-manager/manage-environments.md) - Todos os ambientes configurados para o programa
* ![Ícone de páginas da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Sites do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) - Gerenciar sites do Edge Delivery
* ![Ícone de Configurações](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) [Configurações de Domínio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Gerenciar nomes de domínio personalizados para o programa
* ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) - Gerenciar certificados SSL para o programa
* ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) [Mapeamentos de Domínio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Gerenciar Mapeamentos de Domínio
* ![Ícone de lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) [Listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) - Definir listas de permissões para determinados endereços IP
* ![Ícone de caixa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) [Conjuntos de conteúdo](/help/implementing/developing/tools/content-copy.md) - Conjuntos de conteúdo criados para fins de cópia
* ![Ícone de histórico](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) [Atividade de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) - Atividades de cópia de conteúdo
* ![Ícone de canal](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg) [Infraestrutura de Rede](/help/security/configuring-advanced-networking.md) - Gerenciar opções avançadas de rede para o programa

**Recursos**

* ![Ícone de livro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Book_18_N.svg) Caminhos de aprendizagem - Recursos de aprendizagem adicionais sobre o Cloud Manager

Por padrão, ao abrir um programa, você acessa a guia **Visão geral**. A guia atual está realçada. Selecione outra guia para exibir seus detalhes.

No canto superior esquerdo do [cabeçalho do Cloud Manager](#cloud-manager-header-2), clique em ![Ícone Mostrar menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar ou ocultar o menu lateral de guias.

### Frase de chamariz {#cta}

A seção da frase de chamariz fornece informações úteis de acordo com o status do seu programa. Para um novo programa, você pode ver as próximas etapas fornecidas e um lembrete de uma data de ativação, [definida durante a criação do programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).

![Call-to-action para um novo programa](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

No caso de um programa em tempo real, é possível ver o status da última implantação e links para obter detalhes e iniciar uma nova implantação.

![Frase de chamariz](/help/implementing/cloud-manager/assets/info-banner.png)

### Cartão de ambientes {#environments}

O cartão **Ambientes** fornece uma visão geral dos seus ambientes e links para ações rápidas.

O cartão **Ambientes** lista apenas três ambientes. Clique no ![ícone do Fluxo de Trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar Tudo** para ver todos os ambientes do programa.

Consulte também [Gerenciar ambientes](/help/implementing/cloud-manager/manage-environments.md).

### Cartão de pipelines {#pipelines}

O cartão **Pipelines** fornece uma visão geral dos seus pipelines e links para ações rápidas.

O cartão **Pipelines** lista apenas três pipelines. Clique em ![ícone do Fluxo de Trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar Tudo** para ver todos os pipelines do programa.

Consulte também [Gerenciar pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para obter detalhes sobre como gerenciar seus pipelines.

### Cartão de desempenho {#performance}

O cartão **Desempenho** fornece uma visão geral do **[Painel CDN](/help/implementing/cloud-manager/cdn-performance.md)**.

![Cartão de desempenho](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Recursos úteis {#useful-resources}

A seção **Recursos úteis** fornece links para recursos de aprendizado adicionais do Cloud Manager.
