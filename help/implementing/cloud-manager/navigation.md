---
title: Navegar pela interface do Cloud Manager
description: Saiba como a interface do Cloud Manager é organizada e como encontrar e gerenciar seus programas e ambientes.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 89%

---

# Navegar pela interface do Cloud Manager {#navigation}

Saiba como a interface do Cloud Manager é organizada e como encontrar e gerenciar seus programas e ambientes.

A interface do Cloud Manager é composta principalmente por duas interfaces gráficas:

* [O console Meus programas](#my-programs), onde é possível exibir e gerenciar todos os seus programas.
* [A janela Visão geral do programa](#program-overview), onde é possível ver os detalhes e gerenciar um programa individual.

>[!TIP]
>
>Verifique também a [jornada de documentação de integração](/help/journey-onboarding/overview.md) para obter uma visão geral completa de como começar a usar o AEM as a Cloud Service usando o Cloud Manager.

## Console Meus programas {#my-programs}

Ao fazer logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecionar a organização apropriada, você acessará o console **Meus programas**.

![Console Meus programas](assets/my-programs-console.png)

O console Meus programas fornece uma visão geral de todos os programas aos quais você tem acesso na organização selecionada. Ele é composto por várias partes.

1. [Barras de ferramentas](#toolbars-my-programs-toolbars) para seleção de organização, alertas e configurações da conta
1. [As estatísticas e a frase de chamariz](#statistics) que fornecem uma visão geral das atividades recentes
1. [Programas e licenças](#programs-license) que permitem entender o status atual da licença e gerenciar programas
1. [Links rápidos](#quick-links) para acessar facilmente os recursos relacionados

>[!TIP]
>
>Consulte o documento [Programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obter mais detalhes sobre esse assunto.

### Barras de ferramentas {#my-programs-toolbars}

Há duas barras de ferramentas uma sobre a outra.

#### Cabeçalho do Cloud Manager {#cloud-manager-header}

A primeira é o cabeçalho do Cloud Manager, que permanece fixo ao navegar pelo Cloud Manager. Ele é uma âncora que dá acesso às configurações e informações que se aplicam aos programas do Cloud Manager.

![O cabeçalho da Experience Cloud](assets/experience-cloud-header.png)

1. O botão Cloud Manager leva de volta ao console Meus programas, independentemente de onde você estiver no Cloud Manager.
1. Toque ou clique no botão Feedback para enviar feedback à Adobe sobre o Cloud Manager.
1. O seletor de organização exibe a organização que você está utilizando no momento (neste exemplo, Foundation Internal). Toque ou clique para alternar para outra organização se a Adobe ID estiver associada a mais do que uma.
1. Tocar ou clicar no alternador de soluções permite acessar rapidamente as outras soluções da Experience Cloud.
1. O ícone de ajuda fornece acesso rápido aos recursos de aprendizagem e suporte.
1. O ícone de notificações exibe o número de [notificações incompletas atribuídas atualmente.](/help/implementing/cloud-manager/notifications.md)
1. Clique no ícone que representa seu usuário para acessar as configurações de usuário. Se você não tiver uma imagem de usuário configurada, um ícone será atribuído aleatoriamente.

#### Barra de ferramentas do programa {#program-toolbar}

A barra de ferramentas do programa fornece links para alternar entre programas e ações do Cloud Manager adequados ao contexto.

![Barra de ferramentas do programa](assets/program-toolbar.png)

1. O seletor de programas abre em uma lista suspensa na qual você pode selecionar outros programas rapidamente ou realizar ações apropriadas ao contexto, como criar um novo programa
1. O link de introdução fornece acesso à [jornada de integração à documentação](/help/journey-onboarding/overview.md) para que você possa começar a usar o Cloud Manager.
1. O botão de ação oferece ações adequadas ao contexto, como a criação de um novo programa.

### Estatísticas {#statistics}

A seção de estatísticas fornece dados agregados para sua organização. Por exemplo, se você tiver configurado seus programas com êxito, é possível ver as estatísticas das atividades nos últimos 90 dias, incluindo:

* Número de [implantações](/help/implementing/cloud-manager/deploy-code.md)
* Número de [problemas de qualidade de código](/help/implementing/cloud-manager/code-quality-testing.md) identificados
* Número de builds

Ou se você estiver apenas começando a configurar a organização, encontrará dicas sobre as próximas etapas ou recursos de documentação.

### Programas e licença {#programs-license}

O conteúdo principal do console Meus programas é a lista de programas e o status da sua licença.

#### Guia Programas {#programs}

A guia **Programas** lista os cartões que representam cada programa ao qual você tem acesso. Toque ou clique em um cartão para acessar a página **Visão geral do programa** e obter detalhes sobre ele.

Use as opções de classificação para encontrar mais facilmente o programa necessário.

![Opções de classificação](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Classificar por
   * Data de criação (padrão)
   * Nome do programa
   * Status
* Crescente (padrão)/Decrescente
* Exibição de grade (padrão)
* Exibição de lista

Cada programa é representado por um cartão (ou linha em uma tabela), o qual fornece uma visão geral do programa e links rápidos para realizar ações.

![Cartão do programa](assets/program-card.png)

* Imagem do programa (se configurada)
* Nome do programa
* Tipo de serviço: **Experience Manager Cloud** para programas AEM as a * Cloud Service ou [**Experience Manager** para programas AMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md): sandbox ou produção
* Status
* Soluções configuradas
* Data de criação

Dependendo das opções escolhidas ao criar o programa, um programa de produção pode ser marcado para mostrar recursos adicionais.

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Selo HIPAA](assets/hipaa.png)

* [Proteção WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Selo WAF-DDOS](assets/waf-ddos-protection.png)

* [SLA de 99,99%](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99,99% selo de SLA](assets/9999-sla.png)

O ícone de informações também fornece acesso rápido a informações adicionais sobre o programa (útil na exibição de lista).

![Informações](assets/information-list-view.png)

O ícone de reticências fornece acesso a ações adicionais que você pode realizar no programa.

![Botão de reticências para programas](assets/program-ellipsis.png)

* Navegue até um determinado [ambiente](/help/implementing/cloud-manager/manage-environments.md) do programa
* Abra a [visão geral do programa](#program-overview)
* [Editar o programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [Excluir um programa de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Para obter mais informações sobre programas e sobre como criar e gerenciar programas, consulte os documentos a seguir.
>
>* [Programas e Tipos de Programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Criando Programas de Sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [Criando Programas de Produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### Guia Licença {#license-tab}

A guia **Licença** fornece acesso rápido ao [Painel de Licenças.](/help/implementing/cloud-manager/license-dashboard.md)

### Links rápidos {#quick-links}

A seção de links rápidos fornece acesso aos recursos relacionados usados com frequência.

## Janela Visão geral do programa {#program-overview}

Depois de selecionar um programa no console Meus programas, há um redirecionamento para a Visão geral do programa.

![Visão geral do programa](assets/program-overview.png)

A visão geral do programa fornece acesso a todos os detalhes de um programa do Cloud Manager. Assim como o console Meus programas, essa seção é composta de várias partes.

1. [Barras de ferramentas](#program-overview-toolbar) que permitem voltar rapidamente ao console Meus programas e navegar pelo programa
1. [Guias](#program-tabs) para alternar entre diferentes aspectos do programa
1. Uma [frase de chamariz](#cta) baseada nas últimas ações do programa
1. Uma [visão geral dos ambientes](#environments) do programa
1. Uma [visão geral dos pipelines](#pipelines) do programa
1. Uma [visão geral do desempenho](#performance) do programa
1. Links para [recursos úteis](#useful-resources)

### Barras de ferramentas {#program-overview-toolbar}

As barras de ferramentas da visão geral do programa são muito semelhantes às do [console Meus programas.](#my-programs-toolbars) Somente as diferenças são ilustradas aqui.

#### Cabeçalho do Cloud Manager {#cloud-manager-header-2}

O cabeçalho do Cloud Manager tem um menu de opções que abre automaticamente para mostrar as guias navegáveis da visão geral do programa.

![Menu de opções do Cloud Manager](assets/cloud-manager-hamburger.png)

Toque ou clique no ícone do menu de opções para ocultar as guias.

#### Barra de ferramentas do programa {#program-toolbar-2}

A barra de ferramentas do programa ainda oferece acesso para alternar rapidamente para outros programas, mas também permite acessar ações adequadas ao contexto, como adicionar e editar o programa.

![Barra de ferramentas do programa](assets/cloud-manager-program-toolbar.png)

Além disso, a barra de ferramentas sempre mostra em qual guia você está se tiver optado por ocultar as guias usando o menu de opções.

### Guias do programa {#program-tabs}

Cada programa tem muitas opções e dados associados. Esses dados são coletados em guias para simplificar a navegação no programa. As guias fornecem acesso a:

* Visão geral: a visão geral do programa conforme descrito no documento atual
* [Atividade](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity): o histórico de execuções de pipeline do programa
* [Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines): todos os pipelines configurados para o programa
* [Repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md): todos os repositórios configurados para o programa
* [Relatórios](/help/implementing/cloud-manager/sla-reporting.md): métricas, como dados de SLA
* [Ambientes](/help/implementing/cloud-manager/manage-environments.md): todos os ambientes configurados para o programa
* [Conjuntos de conteúdo](/help/implementing/developing/tools/content-copy.md): conjuntos de conteúdo criados para fins de cópia
* [Atividade de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md): atividades de cópia de conteúdo
* Caminhos de aprendizagem: recursos de aprendizagem adicionais sobre o Cloud Manager

Por padrão, ao abrir um programa, você acessa a guia **Visão geral**. A guia atual está realçada. Selecione outra guia para exibir seus detalhes.

Use o menu de opções no [cabeçalho do Cloud Manager](#cloud-manager-header-2) para ocultar as guias.

### Frase de chamariz {#cta}

A seção da frase de chamariz fornece informações úteis de acordo com o status do programa. No caso de um novo programa, é possível ver as próximas etapas, bem como um lembrete de uma data de ativação, [definida durante a criação do programa.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Frase de chamariz para um novo programa](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

No caso de um programa em tempo real, é possível ver o status da última implantação e links para obter detalhes e iniciar uma nova implantação.

![Frase de chamariz](/help/implementing/cloud-manager/assets/info-banner.png)

### Cartão Ambientes {#environments}

O cartão **Ambientes** fornece uma visão geral de seus ambientes, bem como links para ações rápidas.

O cartão **Ambientes** lista apenas três ambientes. Clique em **Mostrar tudo** para ver todos os ambientes do programa.

Consulte o documento [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter detalhes sobre como gerenciar os ambientes.

### Cartão Pipelines {#pipelines}

O cartão **Pipelines** fornece uma visão geral dos pipelines, bem como links para ações rápidas.

O cartão **Pipelines** lista apenas três pipelines. Clique em **Mostrar tudo** para ver todos os pipelines do programa.

Consulte o documento [Gerenciamento de pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para obter detalhes sobre como gerenciar seus pipelines.

### Cartão de desempenho {#performance}

O cartão **Desempenho** fornece uma visão geral do **[Painel CDN.](/help/implementing/cloud-manager/cdn-performance.md)**

![Cartão de desempenho](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Recursos úteis {#useful-resources}

A seção **Recursos úteis** fornece links para recursos de aprendizado adicionais do Cloud Manager.
