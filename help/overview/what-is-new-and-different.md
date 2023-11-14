---
title: O que é diferente e quais são as novidades - Adobe Experience Manager as a Cloud Service
description: O que é diferente e quais são as novidades - Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: 83b5d9a3ff0e9a3c69e36a97a3f733b05f827d3b
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 99%

---

# Novidades e diferenças {#what-is-new-and-what-is-different}

Há muitos anos, o AEM está disponível:

* No local

* as a Managed Service

Existem diferenças intrínsecas entre estas abordagens anteriores e o AEM as a Cloud Service:

* [Arquitetura](#architecture)
* [Atualizações](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Integração](#onboarding)
* [Desenvolvimento](#developing)
* [Operações e desempenho](#operations-and-performance)
* [Gerenciamento de identidade](#identity-management)
* [Criação da interface do usuário](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Essas visões gerais não são exaustivas, mas destinam-se a fornecer uma introdução.

>[!NOTE]
>
>Para obter mais detalhes sobre as versões no local e o Managed Service, consulte o conjunto de documentações para o [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR).

## Arquitetura {#architecture}

>[!NOTE]
>
>Para mais detalhes, consulte [Arquitetura](/help/overview/architecture.md).

O AEM as a Cloud Service agora tem:

* Uma arquitetura dinâmica com diversas imagens do AEM.

![Arquitetura dinâmica](assets/introduction-03.png "Arquitetura dinâmica")

Essa arquitetura:

* É dimensionada com base no tráfego *real* e na atividade *real*.

* Possui instâncias individuais que são executadas somente quando necessário.

* Usa aplicativos modulares.

* Possui um cluster de criação como padrão; isso evita o tempo de inatividade para tarefas de manutenção.

Isso permite o dimensionamento automático para vários padrões de uso:

![Dimensionamento automático para vários padrões de uso](assets/introduction-04.png "Dimensionamento automático para vários padrões de uso")


## Atualizações do AEM {#aem-updates}

O AEM as a Cloud Service agora usa a integração/entrega contínua (CI/CD) para garantir que seus projetos estejam sempre na versão do AEM mais recente. Isso significa que as instâncias de produção e preparação são atualizadas para a versão mais recente do AEM sem a interrupção do serviço dos usuários.

>[!NOTE]
>
>Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.

Há dois tipos de atualizações de versão do AEM:

* **Atualizações de manutenção do AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Têm um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * Elas são liberadas em um cronograma mensal previsível.

>[!TIP]
>
>Para mais detalhes, consulte as [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md).

## Cloud Manager {#cloud-manager}

O Adobe Cloud Manager é parte integrante da abordagem de atualização contínua do AEM as a Cloud Service, pois controla todas as atualizações das instâncias. Isso é obrigatório.

As atualizações podem ser acionadas pela Adobe quando uma nova versão do Cloud Service estiver disponível. Como alternativa, você pode acionar as atualizações do aplicativo usando os pipelines fornecidos pelo Cloud Manager.

O Cloud Manager é:

* utilizado para gerenciar programas e ambientes do AEM,

* um componente essencial do AEM as a Cloud Service; cada novo locatário é primeiramente provisionado para acesso ao Cloud Manager,

* o ponto de entrada único para suas operações e equipe de desenvolvimento.

Especificamente, o número e o tipo de programas do AEM que podem ser criados no Cloud Manager são derivados:

* do acordo de licenciamento do cliente,

* de intervenientes internos, quando o AEM as a Cloud Service for utilizado para ativação ou formação,

* de processos externos, como avaliações iniciadas em Adobe.com.

O Cloud Manager evoluiu como um portal de autoatendimento, em que os principais componentes do AEM as a Cloud Service podem ser criados e configurados:

* Criação e gerenciamento de novos programas. Consulte [Noções básicas sobre programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obter mais detalhes.

* Criação e gerenciamento dos ambientes do AEM nesses programas. Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais detalhes.

* Criação e gerenciamento de pipelines para implantação do código do cliente e da configuração relacionada a um ambiente específico. Consulte [Configuração do pipeline de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais detalhes.

* Ser notificado sobre eventos importantes do ciclo de vida desses componentes (por exemplo, atualizações de produtos).

O Cloud Manager cria ambientes em data centers em várias regiões geográficas, fornecendo cobertura global. Os pontos de presença (PoPs) da CDN garantem a entrega de conteúdo de baixa latência para clientes localizados em todo o mundo.


## Integração {#onboarding}

Iniciar e gerenciar um projeto AEM é simples quando se usa o AEM as a Cloud Service, pois a Adobe é responsável por vários aspectos:

* As imagens AEM da linha de base são otimizadas para casos de uso específicos.

* Muitas das tarefas de configuração manual foram tornadas redundantes.

Também é significativamente diferente, pois agora há:

* Uma fase de avaliação para garantir que todos os pré-requisitos foram cumpridos; incluindo, por exemplo:

   * Requisitos legais

   * Acordos contratuais

   * Requisitos técnicos para qualquer conteúdo e/ou código existente personalizado pelo cliente

* Requisitos de implantação:

   * Atualizações de código: todos os aplicativos de clientes desenvolvidos para uma versão anterior do AEM precisarão ser revisados e possivelmente atualizados.

   * Migração de conteúdo

>[!TIP]
>
>Para obter uma visão geral completa do processo de integração, consulte a [jornada de integração](/help/journey-onboarding/overview.md).

## Desenvolvimento {#developing}

>[!NOTE]
>
>Para obter mais detalhes, comece com [Diretrizes de desenvolvimento](/help/implementing/developing/introduction/development-guidelines.md) e [Desenvolvimento - O tutorial da WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

A nova arquitetura compatível com o AEM as a Cloud Service envolve algumas alterações importantes na experiência geral do desenvolvedor. Um dos principais objetivos do AEM as a Cloud Service é permitir que clientes experientes (que usaram AEM local ou no contexto do Adobe Managed Services) migrem para o AEM as a Cloud Service o mais rápido possível, sem precisar reescrever a maior parte de seu código personalizado. No entanto, alguns ajustes podem ser necessários.

### Desenvolvimento na nuvem {#aem-as-a-cloud-service-developing-cloud-development}

Para que os aplicativos do AEM existentes sejam executados no AEM as a Cloud Service, as seguintes etapas são esperadas:

* O código e a configuração do aplicativo devem ser armazenados no repositório de código Git do programa associado do Cloud Manager.
* O código e a configuração do aplicativo devem ser compatíveis com a versão mais recente da imagem de linha de base do AEM (que pode estar mudando diariamente).
   * O aplicativo do cliente deve ser criado e implantado usando o pipeline do Cloud Manager associado ao ambiente do Cloud Manager.
* O aplicativo do cliente deve passar por todas as portas de qualidade, segurança e desempenho do código aplicadas no pipeline.
* As imagens criadas para o aplicativo do cliente devem ser implantadas pelo pipeline do Cloud Manager.

Esse processo é comumente chamado de desenvolvimento Cloud-first. Como a duração de ponta a ponta deve demorar minutos (de 20 a 50, dependendo da complexidade do aplicativo), é necessário adotar metodologias de desenvolvimento rápidas antes que as alterações pendentes no código e na configuração sejam tentadas na nuvem.

O console da Web, onde os pacotes OSGI e suas configurações associadas são gerenciados e que anteriormente fazia parte do QuickStart do AEM, não está mais disponível no AEM as a Cloud Service. O novo console do desenvolvedor fornece uma interface somente leitura para a maioria das informações de tempo de execução. Com esse console, os desenvolvedores podem selecionar e fazer logon diretamente em qualquer nó específico de um serviço de autor ou publicação e visualizar informações relevantes.

>[!NOTE]
>
>Consulte também [Configuração OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Outro requisito comum para desenvolvedores é o acesso rápido aos arquivos de log dos vários ambientes. Com o AEM as a Cloud Service, os arquivos de log dos diferentes nós do autor e da publicação são disponibilizados por meio do Cloud Manager, na forma de arquivos que podem ser baixados ou por meio de APIs.

Devido à clara separação de código e conteúdo, os desenvolvedores podem usar um processo específico para atualizar o conteúdo como parte de uma implantação. Os casos de uso típicos de conteúdo mutável são:

* Conteúdo *padrão* que faz parte do projeto do cliente (por exemplo, pastas, modelos, fluxos de trabalho, etc.)

* Definições de índice de pesquisa

* ACLs e permissões

* Usuários do serviço e grupos de usuários

### Desenvolvimento local {#aem-as-a-cloud-service-developing-local-development}

Para apoiar iterações e desenvolvimento rápidos, também é possível desenvolver aplicativos do AEM fora do contexto do AEM as a Cloud Service. Para essa finalidade, os seguintes artefatos são disponibilizados aos desenvolvedores:

* O QuickStart do AEM as a Cloud Service: um instalador independente e com base em `.jar` da base de código do AEM mais recente, com a mesma superfície funcional e de API.

* O SDK do Dispatcher do AEM as a Cloud Service: um processo baseado em imagens para testar e validar as configurações do Dispatcher localmente

>[!NOTE]
>
>Observe que o QuickStart do Cloud não permite todas as funcionalidades do AEM Sites e do AEM Assets. Consiste em um ambiente de autor simples, no qual a maioria das extensões pode ser desenvolvida e testada.

## Operações e desempenho {#operations-and-performance}

>[!NOTE]
>
>Para obter mais detalhes, comece com [restauração de conteúdo](/help/operations/backup.md), [Indexação](/help/operations/indexing.md), e [outras tarefas de manutenção](/help/operations/maintenance.md).

Com o AEM as a Cloud Service, essas operações são automatizadas de modo que não seja mais necessário qualquer interrupção do serviço.

Nestas áreas:

* Muitas tarefas foram automatizadas.

* As topologias são otimizadas para obter o máximo de resiliência e eficiência; por exemplo, a replicação sem binários é o padrão.

* As tarefas de carregamento pesado, como filas, tarefas e tarefas de processamento em massa, foram movidas para fora da instância principal do AEM para serem tratadas por microsserviços compartilhados e dedicados.

As operações para o AEM as a Cloud Service também são suportadas por uma nova infraestrutura de monitoramento, geração de relatórios e alerta. Isso permite que os Adobe SREs (engenheiros de confiabilidade do site) mantenham o serviço saudável de forma proativa. Os diferentes elementos da arquitetura estão equipados com uma variedade de verificações de integridade. Se, por algum motivo, um determinado nó da arquitetura for considerado não íntegro, ele será removido do serviço e silenciosamente substituído por um nó novo e saudável.

## Gerenciamento de identidade {#identity-management}

>[!NOTE]
>
>Para obter mais detalhes, consulte [Segurança - Suporte IMS](/help/security/ims-support.md).

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor.

Isso requer o uso do [Adobe Admin console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As contas de usuário permitem que seus usuários acessem produtos e serviços da Adobe, já que as informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) para serem compartilhadas em todos os serviços em nuvem. Após ter atribuído o acesso ao AEM, as contas de usuário podem ser referenciadas no AEM as a Cloud Service (como antes); por exemplo, para definir funções e permissões das interfaces de usuário do AEM Security.

Isso combina os benefícios de:

* Uso do Sistema Adobe Identity Management (IMS) para fornecer logon único em todos os aplicativos de nuvem da Adobe.

* As preferências do usuário permanecem locais para cada instância específica do AEM as a Cloud Service.

## Criação da interface do usuário {#authoring-user-interface}

>[!NOTE]
>
>Para obter mais detalhes, o [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md) é um bom ponto de partida.

Os princípios básicos da interface (UI) de criação, tanto para o Sites quanto para o Assets, serão reconhecíveis a qualquer pessoa que já tenha usado o AEM no passado.

A principal diferença é que a interface é habilitada para toque; a interface clássica não está mais disponível. No mais, as funcionalidades básicas permanecem inalteradas, verificando-se apenas pequenas alterações.

## AEM Sites {#aem-sites}

O Adobe Experience Manager Sites as a Cloud Service permite proporcionar experiências personalizadas e orientadas por conteúdo aos clientes, combinando o poder do Sistema de gerenciamento de conteúdo do AEM com o Gerenciamento de ativos digitais do AEM.

Para obter detalhes, consulte a visão geral de [Alterações no Sites](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

O Adobe Experience Manager Assets as a Cloud Service oferece uma solução PaaS em nuvem para que as empresas não somente executem suas operações de Gerenciamento de ativos digitais e Mídia dinâmica com velocidade e impacto, como também usem recursos inteligentes de próxima geração, como IA/aprendizado de máquina, de um sistema que está sempre atualizado, disponível e aprendendo.

A oferta de ativos inclui o processamento de ativos da próxima geração na nuvem e a assimilação e pesquisa de ativos de alto desempenho.

Para obter detalhes, consulte [visão geral e introdução ao Assets as a Cloud Service](/help/assets/overview.md).

## Noções básicas sobre o Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Para obter mais informações, consulte:

* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* A [Arquitetura](/help/overview/architecture.md) do Adobe Experience Manager as a Cloud Service
* [Alterações importantes no AEM as a Cloud Service (notas de versão)](/help/release-notes/aem-cloud-changes.md)
* [Alterações importantes no AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Apresentação do AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=pt-BR)

>[!TIP]
>
>Depois de ver uma visão geral do AEM as a Cloud Service, será possível integrar-se rapidamente revisando a [Jornada de integração](/help/journey-onboarding/overview.md).
>
>Já integrado ou pronto para mergulhar nos recursos de AEM de teste? Instale o [Complemento de demonstrações de referência do AEM](/help/journey-sites/demos-add-on/overview.md) para explorar recursos avançados do AEM usando exemplos bem colocados.
