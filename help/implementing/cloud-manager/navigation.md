---
title: Navegação na interface do usuário do Cloud Manager
description: Saiba como a interface do usuário do Cloud Manager é organizada e como navegar para gerenciar seus programas e ambientes.
source-git-commit: a0f80a363cb47be9e3d8f7fa96ea3068eb077d42
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 5%

---


# Navegação na interface do Cloud Manager {#navigation}

Saiba como a interface do usuário do Cloud Manager é organizada e como navegar para gerenciar seus programas e ambientes.

A interface do Cloud Manager é composta principalmente por duas interfaces gráficas:

* [O console Meus programas](#my-programs) onde é possível exibir e gerenciar todos os seus programas.
* [A janela Visão geral do programa](#program-overview) onde você pode ver os detalhes e gerenciar um programa individual.

>[!TIP]
>
>Verifique também o [integração da jornada de documentação](/help/journey-onboarding/overview.md) para obter uma visão geral completa de como começar a usar o AEM as a Cloud Service usando o Cloud Manager.

## Console Meus programas {#my-programs}

Ao fazer logon no Cloud Manager em às [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada, você chegará à **Meus programas** console.

![Console Meus programas](assets/my-programs-console.png)

O console Meus programas fornece uma visão geral de todos os programas aos quais você tem acesso na organização selecionada. Ele é composto por várias partes.

1. [Barras de ferramentas](#toolbars-my-programs-toolbars) para seleção de organização, alertas e configurações de conta
1. [Estatísticas e frase de chamariz](#statistics) para obter uma visão geral de sua atividade recente
1. [Programas e licenças](#programs-license) para entender seu status de licença atual e gerenciar seus programas
1. [Links rápidos](#quick-links) para acessar facilmente os recursos relacionados

>[!TIP]
>
>Consulte o documento [Programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obter detalhes sobre programas.

### Barras de ferramentas {#my-programs-toolbars}

Há duas barras de ferramentas uma sobre a outra.

#### Cabeçalho do Cloud Manager {#cloud-manager-header}

O primeiro é o cabeçalho do Cloud Manager, que é mantido à medida que você navega pelo Cloud Manager. É uma âncora que dá acesso às configurações e informações que se aplicam aos programas do Cloud Manager.

![O cabeçalho da Experience Cloud](assets/experience-cloud-header.png)

1. O botão Cloud Manager o levará de volta ao console Meus programas do Cloud Manager, independentemente de onde você estiver no Cloud Manager.
1. Toque ou clique no botão Feedback para enviar feedback ao Adobe sobre o Cloud Manager.
1. O seletor de organização exibe a organização na qual você está conectado no momento (neste exemplo, Foundation Internal). Toque ou clique para alternar para outra organização se a Adobe ID estiver associada a mais do que uma.
1. Tocar ou clicar no alternador de soluções permite que você vá rapidamente para outras soluções Experience Cloud.
1. O ícone de ajuda fornece acesso rápido aos recursos de aprendizagem e suporte.
1. O ícone de notificações está marcado com o número de incompletos atribuídos no momento [notificações.](/help/implementing/cloud-manager/notifications.md)
1. Selecione o ícone que representa seu usuário para acessar as configurações do usuário. Se você não tiver uma imagem do usuário configurada, um ícone é atribuído aleatoriamente.

#### Barra de ferramentas do programa {#program-toolbar}

A barra de ferramentas do programa fornece links para alternar entre programas e ações do Cloud Manager adequados ao contexto.

![Barra de ferramentas do programa](assets/program-toolbar.png)

1. O seletor de programas é aberto em uma lista suspensa na qual você pode selecionar outros programas rapidamente ou realizar ações apropriadas ao contexto, como criar um novo programa
1. O link de introdução fornece acesso à [integração da jornada de documentação](/help/journey-onboarding/overview.md) para que você possa começar a usar o Cloud Manager.
1. O botão de ação oferece ações adequadas ao contexto, como a criação de um novo programa.

### Estatísticas {#statistics}

A seção de estatísticas fornece dados agregados para sua organização. Por exemplo, se você tiver configurado seus programas com êxito, as estatísticas das atividades nos últimos 90 dias poderão ser exibidas, incluindo:

* Número de [implantações](/help/implementing/cloud-manager/deploy-code.md)
* Número de [problemas de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) identificado
* Número de builds

Ou se você estiver apenas começando a configuração da organização, pode haver dicas sobre as próximas etapas ou recursos de documentação.

### Programas e Licenças {#programs-license}

O conteúdo principal do console Meus programas é a lista de programas e o status da sua licença.

#### Guia Programas {#programs}

A variável **Programas** A guia lista os cartões que representam cada programa ao qual você tem acesso. Toque ou clique em um cartão para acessar a **Visão geral do programa** página do programa para obter detalhes sobre ele.

Use as opções de classificação para encontrar melhor o programa necessário.

![Opções de classificação](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Classificar por
   * Data de criação (padrão)
   * Nome do programa
   * Status
* Crescente (padrão) / Decrescente
* Exibição em grade (padrão)
* Exibição de lista

Cada programa é representado por um cartão (ou linha em uma tabela), fornecendo uma visão geral do programa e links rápidos para tomar medidas.

![Cartão do programa](assets/program-card.png)

* Imagem do programa (se configurada)
* Nome do programa
* Tipo de serviço: **Experience Manager Cloud** para programas AEM as a * Cloud Service ou [**Experience Manager** para programas do AMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md): Sandbox ou produção
* Status
* Soluções configuradas
* Data de criação

Dependendo das opções escolhidas ao criar o programa, um programa de produção pode ser marcado para mostrar recursos adicionais.

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Selo HIPAA](assets/hipaa.png)

* [Proteção WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Selo WAF-DDOS](assets/waf-ddos-protection.png)

* [SLA de 99,99%](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![Selo de SLA de 99,99%](assets/9999-sla.png)

O ícone de informações também fornece acesso rápido a informações adicionais sobre o programa (útil na exibição em lista).

![Informações](assets/information-list-view.png)

O ícone de reticências fornece acesso a ações adicionais que você pode realizar no programa.

![Botão de reticências para programas](assets/program-ellipsis.png)

* Navegue até um determinado [ambiente](/help/implementing/cloud-manager/manage-environments.md) do programa
* Abra o [visão geral do programa](#program-overview)
* [Editar o programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [Excluir um programa de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Para obter mais informações sobre programas e sobre como criar e gerenciar programas, consulte os documentos a seguir.
>
>* [Programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Criação de programas do sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [Criação de programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### Guia Licença {#license-tab}

A variável **Licença** fornece acesso rápido à [Painel de licenças.](/help/implementing/cloud-manager/license-dashboard.md)

### Links rápidos {#quick-links}

A seção Links rápidos fornece acesso aos recursos relacionados comumente usados.

## Janela Visão geral do programa {#program-overview}

Depois de selecionar um programa no console Meus programas, você será direcionado à Visão geral do programa.

![Visão geral do programa](assets/program-overview.png)

A visão geral do programa fornece acesso a todos os detalhes de um programa do Cloud Manager. Assim como o console Meus programas, ele é composto de várias partes.

1. [Barras de ferramentas](#program-overview-toolbar) para voltar rapidamente ao console Meus programas e navegar pelo programa
1. [Guias](#program-tabs) alternar entre diferentes aspectos do programa
1. A [frase de chamariz](#cta) com base nas últimas ações do programa
1. Um [visão geral dos ambientes](#environments) do programa
1. Um [visão geral dos pipelines](#pipelines) do programa
1. Um [visão geral do desempenho](#performance) do programa
1. Links para [recursos úteis](#useful-resources)

### Barras de ferramentas {#program-overview-toolbar}

As barras de ferramentas para a visão geral do programa são muito semelhantes às do [Console Meus programas.](#my-programs-toolbars) Somente as diferenças são ilustradas aqui.

#### Cabeçalho do Cloud Manager {#cloud-manager-header-2}

O cabeçalho do Cloud Manager tem um menu de hambúrguer que é aberto automaticamente para mostrar as guias navegáveis da visão geral do programa.

![Menu de hambúrguer do Cloud Manager](assets/cloud-manager-hamburger.png)

Toque ou clique no ícone de menu de hambúrguer para ocultar as guias.

#### Barra de ferramentas do programa {#program-toolbar-2}

A barra de ferramentas do programa ainda oferece acesso para alternar rapidamente para outros programas, mas também dá acesso às ações adequadas ao contexto, como adicionar e editar o programa.

![Barra de ferramentas do programa](assets/cloud-manager-program-toolbar.png)

Além disso, a barra de ferramentas sempre fornece a guia em que você está se você optou por ocultar as guias usando o menu de hambúrguer.

### Guias Programa {#program-tabs}

Cada programa tem muitas opções e dados associados a ele. Esses dados são coletados em guias para simplificar a navegação pelo programa. As guias fornecem acesso a:

* Visão geral - A visão geral do programa conforme descrito no documento atual
* [Atividade](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - O histórico de execuções de pipeline do programa
* [Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - Todos os pipelines configurados para o programa
* [Repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Todos os repositórios configurados para o programa
* [Relatórios](/help/implementing/cloud-manager/sla-reporting.md) - Métricas como dados de SLA
* [Ambientes](/help/implementing/cloud-manager/manage-environments.md) - Todos os ambientes configurados para o programa
* [Conjuntos de conteúdo](/help/implementing/developing/tools/content-copy.md) - Conjuntos de conteúdo criados para fins de cópia
* [Atividade de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) - Atividades de cópia de conteúdo
* Caminhos de aprendizagem - Recursos de aprendizagem adicionais sobre o Cloud Manager

Por padrão, ao abrir um programa, você acessa o **Visão geral** guia. A guia atual está realçada. Selecione outra guia para exibir seus detalhes.

Use o menu de hambúrguer na [Cabeçalho do Cloud Manager](#cloud-manager-header-2) para ocultar as guias.

### Frase de chamariz {#cta}

A seção de frase de chamariz fornecerá informações úteis, dependendo do status do seu programa. Para um novo programa, você pode ver as próximas etapas oferecidas, bem como um lembrete de uma data de publicação, [definido durante a criação do programa.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Frase de chamariz para um novo programa](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

Para um programa em tempo real, o status da última implantação com links para obter detalhes e iniciar uma nova implantação.

![Frase de chamariz](/help/implementing/cloud-manager/assets/info-banner.png)

### Cartão Ambientes {#environments}

A variável **Ambientes** O cartão fornece uma visão geral de seus ambientes, bem como links para ações rápidas.

O cartão **Ambientes** lista apenas três ambientes. Clique em **Mostrar tudo** para ver todos os ambientes do programa.

Consulte o documento [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter detalhes sobre como gerenciar os ambientes.

### Cartão Pipelines {#pipelines}

A variável **Pipelines** O cartão fornece uma visão geral dos pipelines, bem como links para ações rápidas.

A variável **Pipelines** O cartão lista apenas três pipelines. Clique em **Mostrar tudo** para ver todos os pipelines do programa.

Consulte o documento [Gerenciamento de pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para obter detalhes sobre como gerenciar seus pipelines.

### Cartão de desempenho {#performance}

A variável **Desempenho** fornece uma visão geral do **[Painel CDN.](/help/implementing/cloud-manager/cdn-performance.md)**

![Cartão de desempenho](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Recursos úteis {#useful-resources}

A variável **Recursos úteis** fornece links para recursos de aprendizado adicionais do Cloud Manager.
