---
title: O que é diferente e o que é novo - Adobe Experience Manager como Cloud Service
description: 'O que é diferente e o que é novo - Adobe Experience Manager (AEM) como Cloud Service. '
translation-type: tm+mt
source-git-commit: 9882c95972675ee1e0af5de30119d764638f53f3
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 10%

---


# Novidades e diferenças {#what-is-new-and-what-is-different}

Há muitos anos AEM está disponível:

* No local

* como um serviço gerenciado

Há diferenças intrínsecas entre essas abordagens anteriores e AEM como Cloud Service:

* [Arquitetura](#architecture)
* [Atualizações](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Integração](#onboarding)
* [Desenvolvimento](#developing)
* [Operações e desempenho](#operations-and-performance)
* [Gerenciamento de identidade](#identity-management)
* [Interface do usuário de criação](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [Ativos AEM](#aem-assets)

>[!NOTE]
>
>Essas visões gerais não são exaustivas, mas têm como objetivo fornecer uma introdução.

>[!NOTE]
>
>Para obter mais detalhes sobre as versões On-Premise e Managed Service, consulte a documentação definida para [AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html).

## Arquitetura {#architecture}

>[!NOTE]
>
>Para obter mais detalhes, consulte [Arquitetura](/help/core-concepts/architecture.md).

O AEM as a Cloud Service agora tem:

* Uma arquitetura dinâmica com diversas imagens do AEM.

![Arquitetura dinâmica](assets/introduction-03.png "Arquitetura dinâmica")

Essa arquitetura:

* É dimensionada com base no tráfego *real* e na atividade *real* .

* Possui instâncias individuais que são executadas somente quando necessário.

* Usa aplicativos modulares.

* Possui um cluster de criação como padrão; isso evita o tempo de inatividade para tarefas de manutenção.

Isso permite o dimensionamento automático para vários padrões de uso:

![Dimensionamento automático para vários padrões de uso](assets/introduction-04.png "Dimensionamento automático para vários padrões de uso")


## Atualizações {#upgrades}

>[!NOTE]
>
>Para obter mais detalhes, consulte a Introdução à [implantação](/help/implementing/deploying/overview.md).

AEM como Cloud Service agora usa a Integração contínua e o Delivery contínuo (CI/CD) para garantir que seus projetos estejam totalmente atualizados. Isso significa que todas as operações de atualização são totalmente automatizadas, portanto, não é necessário interromper o serviço para os usuários.

O Adobe toma cuidado de atualizar proativamente todas as instâncias operacionais do serviço para a versão mais recente da base de código AEM:

* Correções de erros:

   * Pode ser lançado diariamente.

   * As instâncias são atualizadas com frequência com as correções de erros mais recentes. Como as mudanças são aplicadas regularmente, o impacto é incremental, reduzindo o impacto sobre seu serviço.

   * A maioria das atualizações é feita por motivos de manutenção e segurança.

* Novos recursos:

   * Será lançado por meio de uma programação mensal previsível.

>[!NOTE]
>
>Para obter mais detalhes, consulte Arquitetura [de implantação](/help/core-concepts/architecture.md#deployment-architecture).

## Cloud Manager {#cloud-manager}

O Adobe Cloud Manager é parte integrante da abordagem de atualização contínua do AEM como Cloud Service, pois controla todas as atualizações em suas instâncias - isso é obrigatório.

As atualizações podem ser acionadas pelo Adobe quando uma nova versão do serviço em nuvem estiver disponível. Como alternativa, você pode acionar as atualizações do aplicativo usando os pipelines fornecidos pelo Cloud Manager.

O Cloud Manager é:

* utilizado para gerir programas e ambientes AEM,

* Uma componente essencial da AEM como Cloud Service; cada novo inquilino é provisionado pela primeira vez para acesso ao Cloud Manager,

* o ponto de entrada único para sua equipe de operações e desenvolvimento.

Especificamente, o número e o tipo de programas de AEM que podem ser criados no Gerenciador de nuvem são derivados:

* do contrato de licença do cliente,

* de intervenientes internos, quando AEM como Cloud Service for utilizado para a ativação, ou para a formação,

* de processos externos, como testes iniciados em Adobe.com.

O Cloud Manager evoluiu como um portal de autoatendimento onde os principais componentes do AEM como Cloud Service podem ser criados e configurados:

* Criação e gerenciamento de novos programas. Consulte [Como entender Programas e tipos](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) de Programas para obter mais detalhes.

* Criação e gerenciamento dos ambientes AEM nesses programas. Consulte [Gerenciamento de Ambientes](/help/implementing/cloud-manager/manage-environments.md) para obter mais detalhes.

* Criação e gerenciamento de pipelines para a implantação do código do cliente e da configuração relacionada a um ambiente específico. Consulte [Configuração do seu pipeline](/help/implementing/cloud-manager/configure-pipeline.md) CI-CD para obter mais detalhes.

* Ser notificado sobre eventos importantes do ciclo de vida desses componentes (por exemplo, atualizações de produtos).

Atualmente, o Cloud Manager pode criar ambientes em três regiões geográficas (com mais regiões a seguir):

* EUA (Leste)

* EMEA (Países Baixos)

* APAC (Austrália)

>[!NOTE]
>Consulte [Acessar o Experience Manager como Cloud Service](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) para começar a usar o Cloud Manager em AEM como Cloud Service.

## Integração {#onboarding}

>[!NOTE]
>
>Para obter mais detalhes, consulte [Onboard (Onboard](/help/onboarding/home.md)).

Iniciar e gerenciar um projeto AEM é simples ao usar o AEM como um serviço da Cloud como Adobe é responsável por vários aspectos:

* As imagens da linha de base AEM são otimizadas para casos de uso específicos.

* Muitas das tarefas de configuração manuais foram redundantes.

Também é significativamente diferente, já que agora existe:

* Uma fase de avaliação para garantir que todos os pré-requisitos foram cumpridos; incluindo, por exemplo:

   * Requisitos legais

   * Acordos contratuais

   * Requisitos técnicos para qualquer conteúdo existente e/ou código personalizado pelo cliente

* Requisitos de implantação:

   * Atualizações de código; todos os aplicativos do cliente desenvolvidos para uma versão anterior do AEM precisarão ser revisados e possivelmente atualizados.

   * Migração de conteúdo

## Desenvolvimento {#developing}

>[!NOTE]
>
>Para obter mais detalhes, você pode start com as diretrizes [de](/help/implementing/developing/introduction/development-guidelines.md) desenvolvimento e [desenvolvimento - o tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)da WKND.

A nova arquitetura que suporta AEM como Cloud Service envolve algumas mudanças importantes na experiência geral do desenvolvedor. Um dos principais objetivos da AEM como Cloud Service é permitir que clientes experientes (tendo usado AEM no local ou no contexto dos Serviços gerenciados da Adobe) migrem para o AEM o mais rápido possível, sem precisar reescrever a maior parte de seus códigos personalizados. No entanto, poderão ainda ser necessários alguns ajustamentos.

### Desenvolvimento em nuvem {#aem-as-a-cloud-service-developing-cloud-development}

Para que os aplicativos AEM existentes sejam executados em AEM como um Cloud Service, as seguintes etapas são esperadas:

* O código e a configuração do aplicativo devem ser armazenados no repositório de código Git do programa associado do Cloud Manager.
* O código e a configuração do aplicativo devem ser compatíveis com a versão mais recente da imagem de AEM da linha de base (que pode estar mudando diariamente).
   * O aplicativo do cliente deve ser criado e implantado usando o pipeline do Gerenciador de nuvem associado ao ambiente do Gerenciador de nuvem.
* O aplicativo do cliente deve passar por todas as portas de qualidade, segurança e desempenho do código aplicadas no pipeline.
* As imagens criadas para o aplicativo do cliente devem ser implantadas pelo pipeline do Gerenciador de nuvem.

Esse processo é comumente chamado de desenvolvimento em nuvem. Como a duração completa deve levar minutos (de 20 a 50, dependendo da complexidade do aplicativo), é necessário adotar metodologias de desenvolvimento rápido antes que o código pendente e as alterações de configuração sejam tentadas na nuvem.

O Console da Web, onde os pacotes OSGI e suas configurações associadas são gerenciados e anteriormente parte do AEM QuickStart, não é mais diretamente acessível aos usuários de um AEM como ambiente. Essa interface ainda pode ser acessada no modo somente leitura usando um novo console do desenvolvedor. Com esse console, os desenvolvedores podem selecionar e fazer logon diretamente em qualquer nó específico de um autor ou serviço de publicação e, em seguida, acessar as áreas bloqueadas por padrão.

>[!NOTE]
>
>Consulte também Configuração [OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Outro requisito comum para desenvolvedores é o acesso rápido aos arquivos de registro dos vários ambientes. Com o AEM como um Cloud Service, os arquivos de log dos diferentes nós do autor e publicação são disponibilizados pelo Gerenciador de nuvem, na forma de arquivos que podem ser baixados ou por meio de APIs.

Devido à clara separação de código e conteúdo, os desenvolvedores podem usar um processo específico para atualizar o conteúdo como parte de uma implantação. Os casos de uso típicos para conteúdo mutável são:

* Conteúdo *padrão* que faz parte do projeto do cliente (por exemplo, pastas, modelos, workflows etc.)

* Definições de índice de pesquisa

* ACLs e permissões

* Usuários do serviço e grupos de usuários

### Desenvolvimento local {#aem-as-a-cloud-service-developing-local-development}

A fim de apoiar iterações e desenvolvimento rápidos, é também possível desenvolver aplicações AEM fora do AEM como um contexto Cloud Service. Para esse efeito, os seguintes artefatos são disponibilizados aos desenvolvedores:

* O AEM como um QuickStart Cloud Service: um instalador independente e `.jar` baseado na última base de código AEM, com a mesma superfície funcional e de API.

* O AEM como um SDK do Dispatcher Cloud Service: um processo baseado em imagem para testar e validar configurações do Dispatcher localmente

>[!NOTE]
>
>Observe que o Cloud QuickStart não permite todas as funcionalidades do AEM Sites e do AEM Assets. Consiste num simples ambiente de autor, no qual a maioria das extensões pode ser desenvolvida e testada.

## Operações e desempenho {#operations-and-performance}

>[!NOTE]
>
>Para obter mais detalhes, comece com [Backup](/help/operations/backup.md), [Indexação](/help/operations/indexing.md) e [outras Tarefas de manutenção](/help/operations/maintenance.md).

Com AEM como Cloud Service, essas operações são automatizadas para que não seja mais necessário interromper o serviço.

Nestas áreas:

* Muitas tarefas foram automatizadas.

* As topologias são otimizadas para a máxima resistência e eficiência; por exemplo, a replicação sem binários é o padrão.

* Tarefas pesadas, como filas, trabalhos e tarefas de processamento em massa, foram removidas da instância principal AEM para serem tratadas por microserviços compartilhados e dedicados.

As operações para AEM como Cloud Service também são suportadas por uma nova infraestrutura de monitoramento, relatórios e alerta. Isso permite que os Adobe SREs (Site Reliability Engineers, engenheiros de confiabilidade do site) mantenham o serviço saudável de forma proativa. Os vários elementos da arquitetura estão equipados com uma variedade de controlos sanitários. Se, por algum motivo, um nó específico da arquitetura for considerado insalubre, ele será removido do serviço e silenciosamente substituído por um novo nó saudável.

## Gerenciamento de identidade {#identity-management}

>[!NOTE]
>
>Para obter mais detalhes, consulte [Segurança - Suporte](/help/security/ims-support.md)IMS.

Uma grande mudança para AEM como Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar a camada do autor.

Isso requer o uso do console [de administração de](https://helpx.adobe.com/br/enterprise/using/admin-console.html) Adobe para gerenciar usuários e grupos de usuários. As contas de usuário permitem que seus usuários acessem produtos e serviços do Adobe, já que as informações do perfil do usuário estão centralizadas no Adobe Identity Management System (IMS) para serem compartilhadas em todos os serviços em nuvem. Depois de ter recebido acesso ao AEM, as contas de usuário podem ser referenciadas em AEM como Cloud Service (como antes); por exemplo, para definir funções e permissões das interfaces de usuário do AEM Security.

Isso combina os benefícios de:

* Usando o sistema Adobe Identity Management (IMS) para fornecer logon único em todos os aplicativos de nuvem do Adobe.

* As preferências do usuário permanecem locais para cada instância específica do AEM como um Cloud Service.

## Interface do usuário de criação {#authoring-user-interface}

>[!NOTE]
>
>Para obter mais detalhes, o Manuseio [](/help/sites-cloud/authoring/getting-started/basic-handling.md) básico é um bom ponto de partida.

Os princípios básicos da interface do usuário de criação, tanto para Sites quanto para Ativos, serão familiares a qualquer pessoa que tenha usado AEM no passado.

A principal diferença é que a interface do usuário está habilitada para toque; a interface clássica não está mais disponível. Caso contrário, os fundamentos permanecerão inalterados, sendo apenas visíveis pequenas alterações.

## AEM Sites {#aem-sites}

A Adobe Experience Manager Sites como Cloud Service permite que você forneça a seus clientes experiências personalizadas e orientadas por conteúdo, combinando o poder do Sistema de Gestão de conteúdo AEM com AEM Gerenciamento de ativos digitais.

Para obter detalhes, consulte a visão geral de [Alterações em sites](/help/sites-cloud/sites-cloud-changes.md).

## Ativos AEM {#aem-assets}

O Adobe Experience Manager Assets como Cloud Service oferta uma solução SaaS nativa para nuvem para que as empresas não só executem suas operações de Gerenciamento de ativos digitais e Mídia dinâmica com velocidade e impacto, como também usem recursos inteligentes da próxima geração, como o AI/ML, em um sistema que é sempre atual, sempre disponível e sempre aprendendo.

A oferta de ativos inclui o processamento de ativos da próxima geração na nuvem e a inclusão e pesquisa de ativos de alto desempenho.

Para obter detalhes, consulte [Visão geral e introdução aos Ativos como Cloud Service](/help/assets/overview.md).

## Noções básicas sobre o Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Para obter mais informações, consulte:

* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* A [Arquitetura](/help/core-concepts/architecture.md) do Adobe Experience Manager as a Cloud Service
* [Alterações importantes no AEM as a Cloud Service (notas de versão)](/help/release-notes/aem-cloud-changes.md)
* [Alterações importantes no AEM Sites as a  Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Alterações importantes no AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Apresentando a AEM Assets como Cloud Service](/help/assets/overview.md)
* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
