---
title: Experience Manager [!DNL AEM Forms] Arquitetura as a Cloud Service
description: Entenda a arquitetura de [!DNL AEM Forms] as a Cloud Service para saber mais sobre os aspectos de escalabilidade, resiliência e desempenho da plataforma.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 4%

---


# [!DNL AEM] Arquitetura as a Cloud Service {#architecture}

[!DNL AEM Forms] O as a Cloud Service padroniza a arquitetura de implantação para todos os clientes, com o objetivo de libertar totalmente os clientes das considerações de arquitetura. Por exemplo, embora a nova arquitetura AEM as a Cloud Service ainda dependa do conceito de microkernels para a persistência, os clientes não precisam se preocupar com qual microkernel escolher. Os microkernels usados tanto no autor quanto no lado da publicação são exclusivos do [!DNL AEM Cloud Service] e não estará disponível para clientes em instalações locais.

AEM as a Cloud Service tem uma arquitetura dinâmica com um número variável de instâncias AEM. Ele oferece ambientes de desenvolvimento, estágio, produção e demonstração. Ele fornece ferramentas para gerenciar instâncias de AEM (Cloud Manager), manter usuários e autenticações (sistema Admin Console e IMS (Adobe Identity Management), configurar o armazenamento em cache (Fastly CDN) e ambiente de desenvolvimento nativo de nuvem. Para obter mais informações sobre arquitetura, consulte [Uma introdução à arquitetura de [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

O Cloud Manager é um componente essencial para [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Cada novo locatário do [!DNL AEM Forms] O as a Cloud Service é provisionado pela primeira vez para acessar o Cloud Manager. O Cloud Manager é o ponto de entrada único para as operações e o persona do desenvolvedor de nossos clientes. É o local onde os programas e ambientes de AEM podem ser gerenciados. O Cloud Manager evoluiu como um portal de autoatendimento onde os principais componentes da AEM as a Cloud Service podem ser criados e configurados:

* Criação e gerenciamento de programas
* Criação e gerenciamento dos ambientes AEM nos programas
* Criação e gerenciamento de pipelines para implantação do código e da configuração do cliente em um ambiente específico
* Obter notificações de eventos importantes do ciclo de vida desses componentes (por exemplo, atualizações do produto) Para obter mais informações sobre o Cloud Manager, consulte [Entender o Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) e [Introdução ao Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=pt-BR).

## Usuários e autenticação {#users-and-authentication}

AEM as a Cloud Service inclui suporte ao Admin Console para instâncias AEM e autenticação baseada no Adobe Identity Management System (IMS). O Admin Console permite que os administradores gerenciem todos os usuários da Experience Cloud de maneira centralizada. Usuários e grupos podem ser atribuídos a perfis de produtos associados às instâncias do AEM as a Cloud Service, permitindo que façam logon nessa instância. Para obter mais informações sobre usuários, autenticação e acesso a uma instância de AEM as a Cloud Service, consulte [Suporte IMS para [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Várias personas estão envolvidas em um [!DNL AEM Forms] projeto. Depois de fazer logon no [!DNL AEM Forms] instância as a Cloud Service, você pode [adicionar usuários no admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) para pessoas aplicáveis à sua organização ou projeto e [atribuir usuários a grupos incorporados](forms-groups-privileges-tasks.md) fornecer-lhes os privilégios necessários.

Para aprender vários [!DNL AEM Forms] grupos de usuários específicos e privilégios disponíveis em [!DNL AEM Forms] como uma instância do Cloud Services, consulte [Configurar, usuário, funções e grupos](forms-groups-privileges-tasks.md).

## Experiência do desenvolvedor {#developer-experience}

A nova arquitetura que suporta AEM as a Cloud Service traz algumas mudanças importantes na experiência geral do desenvolvedor. Um dos principais objetivos das alterações na experiência do desenvolvedor é permitir que a migração AEM as a Cloud Service o mais rápido possível, com poucas modificações no código personalizado existente.

## Desenvolvimento na nuvem {#cloud-development}

Estas são as diretrizes para executar o código existente sem problemas em AEM ambiente as a Cloud Service:

* Armazene seu código e configurações no repositório Git do programa associado do Cloud Manager. Isso torna fácil gerenciar e integrar código com CI/CD.
* Tornar o código e a configuração do aplicativo compatíveis com a linha de base [!DNL AEM Forms] imagens. Usar as APIs mais recentes ajuda a criar aplicativos mais rápidos e seguros.
* Use o pipeline do Cloud Manager associado ao ambiente do Cloud Manager para criar e implantar aplicativos. Ajuda a trazer os recursos e o erro mais recentes corrigidos para [!DNL AEM Forms] as a Cloud Service ao seu ambiente.
* Tente que seus aplicativos personalizados passem todas as portas de qualidade, segurança e desempenho do código aplicadas no pipeline. Ajuda a criar aplicativos seguros e de melhor desempenho, o que leva a uma melhor experiência do cliente. Você sempre pode usar a interface do usuário do Cloud Manager para ignorar algumas verificações.
Esse processo é comumente chamado de desenvolvimento em nuvem. [!DNL AEM Forms] as a Cloud Service também fornece um SDK para oferecer suporte a desenvolvimento rápido antes que o código pendente e as alterações de configuração sejam tentadas na nuvem.
Algumas interfaces que anteriormente faziam parte do AEM QuickStart não estão mais disponíveis para os usuários do ambiente as a Cloud Service AEM. Por exemplo, o Console da Web, onde os pacotes OSGI e sua configuração associada são gerenciados. O navegador do repositório de conteúdo do CRXDE Lite torna-se acessível somente em tipos de ambiente que não sejam de produção. Um subconjunto das funcionalidades do Console da Web que os desenvolvedores exigem, especialmente quando se trata de diagnósticos e fins de status, é disponibilizado por meio de um novo console de desenvolvedor.
Além disso, um dos requisitos mais comuns para desenvolvedores é o acesso rápido aos arquivos de log dos vários ambientes. Com [!DNL AEM Cloud Service], os arquivos de log dos diferentes nós no Autor, Publicação são disponibilizados por meio do Cloud Manager, na forma de arquivos que podem ser baixados ou por meio de APIs para adaptar os logs. Devido à clara separação de código e conteúdo, os desenvolvedores podem aproveitar um processo específico de atualização de conteúdo como parte de uma implantação. Os casos de uso típicos de conteúdo mutável são:
* Conteúdo &quot;padrão&quot; padrão que faz parte do projeto do cliente (por exemplo, pastas, modelos, fluxos de trabalho...)
* Definições de índice de pesquisa
* ACLs e permissões
* Usuários do serviço e grupos de usuários Configurar o ambiente de desenvolvimento, [Configurar o pipeline de CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)e aprenda a [implante seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) sobre o ambiente.

## Desenvolvimento local {#local-development}

Ao configurar e configurar um [!DNL AEM Forms] Ambiente as a Cloud Service, você configura ambientes de desenvolvimento, armazenamento temporário e produção. Além disso, configure e configure um ambiente de desenvolvimento local para iterações e desenvolvimento rápidos. Você pode baixar e configurar AEM SDK e [!DNL AEM Forms] arquivo de recursos complementares para configurar um [!DNL Forms] as a Cloud Service ambiente de desenvolvimento.  Para obter instruções detalhadas, consulte [Configurar um ambiente de desenvolvimento local](setup-local-development-environment.md).

## Depuração {#debugging}

AEM as a Cloud Service é executado em autoatendimento, dimensionável e infraestrutura em nuvem. Ela requer que os desenvolvedores AEM entendam e depurem várias facetas AEM as a Cloud Service, desde a criação e implantação até obter detalhes sobre a execução de aplicativos AEM. Para obter informações detalhadas, consulte [Depuração AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
