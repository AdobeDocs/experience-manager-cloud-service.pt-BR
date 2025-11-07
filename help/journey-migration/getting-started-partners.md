---
title: Guia de migração para o Experience Manager as a Cloud Service para parceiros
description: Guia de migração para o Experience Manager as a Cloud Service para parceiros
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 18%

---

# Manual de migração do Adobe Experience Manager as a Cloud Service para parceiros {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migração para o AEM as a Cloud Service"
>abstract="Descreve a abordagem em fases recomendada para clientes de transição de várias implantações do Experience Manager para o Experience Manager as a Cloud Service e ajuda os clientes existentes a fornecer experiências contínuas e conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=pt-BR" text="Quais são as novidades e as diferenças?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=pt-BR" text="Introdução ao AEM as a Cloud Service."

O Adobe Experience Manager (AEM) as a Cloud Service oferece uma arquitetura atualizada para o Experience Manager. Essa base é criada com base em uma infraestrutura baseada em contêiner, desenvolvimento orientado por API e processo DevOps orientado. Isso permite que profissionais de marketing e desenvolvedores se mantenham à frente das inovações no gerenciamento de experiência do cliente.

O Cloud Service reúne recursos avançados prontos para uso e extensibilidade do Adobe Experience Manager com a agilidade da arquitetura moderna nativa em nuvem, permitindo que as marcas atendam à demanda cada vez maior do consumidor.

Esta página descreve a abordagem em fases recomendada para fazer a transição de clientes de implantações anteriores do Experience Manager para o Experience Manager as a Cloud Service. A nova plataforma criada para propósitos específicos ajuda a fornecer experiências conectadas e contínuas.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Consulte o diagrama abaixo para obter uma representação geral da jornada de migração.

![Representação geral da jornada de migração](/help/journey-migration/assets/migration-process.png)

## Introdução ao Adobe Experience Manager as a Cloud Service {#getting-started}

| O que é diferente? | Visão geral da arquitetura |
|--------------------------|--------------------------|
| <ul><li>[Arquitetura Moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=pt-BR)</li><li>[Atualizações Automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=pt-BR)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR)</li><li>[Microsserviços de ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=pt-BR)</li><li>[Binários de Acesso Direto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=pt-BR)</li><li>[Separação de código e conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR)</li><li>[Replicação como um serviço](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=pt-BR)</li><li>[Admin Console, Associação de Grupo/Usuário e ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR)</li></ul> | <ul><li>[Introdução à arquitetura do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=pt-BR#underlying-technology)</li><li>[Pilha de ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=pt-BR)</li><li>[Camada de Autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=pt-BR#underlying-technology)</li><li>[Nível de Publicação](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=pt-BR#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=pt-BR)</li><li>[CDN](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR)</li><li>[Serviço Asset Compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=pt-BR)</li></ul> |

![AEM as a Cloud Service - Arquitetura do tempo de execução](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - Arquitetura do tempo de execução")

<br>

## Jornada de desenvolvedor no Adobe Experience Manager as a Cloud Service {#developer-journey}

### Desenvolver

Os fundamentos do desenvolvimento de código no Adobe Experience Manager as a Cloud Service são semelhantes aos das soluções Adobe Experience Manager no local e Managed Services.

Os desenvolvedores gravam o código e o testam localmente, depois o enviam para ambientes remotos do Adobe Experience Manager as a Cloud Service.

Consulte recursos de autoajuda sobre implementação do Experience Manager as a Cloud Service para saber como personalizar sua implantação do Experience Manager as a Cloud Service.

| Configuração de desenvolvimento local | O que você deve saber antes de começar |
|-----------|------------|
| <ol><li>Consulte a documentação do [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR) para saber mais.</li><li>Assista [Instalar o Dispatcher SDK](https://video.tv.adobe.com/v/30601) para entender como instalar o Dispatcher SDK</li><li>Assista [Configurar o Dispatcher SDK](https://video.tv.adobe.com/v/33175?captions=por_br) para entender como configurar o Dispatcher SDK</li><li>Consulte a documentação da [Configuração de desenvolvimento local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR#local-development-environment-set-up) para saber mais</li><li>Configuração do acesso ao Experience Manager [walk-through](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=pt-BR#accessing)</li></ol> | <ol><li>[Fundamentos de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR)</li><li>[Diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR)</li><li>[Noções básicas sobre a estrutura de projetos do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR)</li><li>[Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction)</li><li>[Blueprint do Digital Foundation](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=pt-BR)</li><li>[Sobreposições](/help/implementing/developing/introduction/overlays.md)</li><li>[Referência da API do Experience Manager as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Consulte o tutorial sobre como [Desenvolver e implantar o WKND no Experience Manager SDK local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)

### Implantando

Os desenvolvedores gravam o código e o testam localmente, depois o enviam para ambientes remotos do AEM as a Cloud Service.

O Cloud Manager, que era uma ferramenta opcional de entrega de conteúdo para o Managed Services, agora é obrigatório. É o único mecanismo para implantar código em ambientes AEM as a Cloud Service.

Consulte recursos de autoajuda sobre como configurar e implantar em ambientes AEM as a Cloud Service.

1. [Configurar Pipelines CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=pt-BR)

   * Pipeline de produção
   * Pipelines somente de não produção e qualidade de código

1. [Implantar Código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR)
1. [Noções Básicas Sobre Os Resultados De Teste](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=pt-BR)
1. **Acessando Logs**

   * [via IU do CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=pt-BR)
   * [via cli do Adobe i/o](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=pt-BR#debugging)

1. [Operações e manutenção](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=pt-BR)

   * [Configurando OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=pt-BR)
   * [Backup e restauração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=pt-BR)

>[!TIP]
> Consulte o tutorial sobre como [Implantar WKND no Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)

### Ajuda e recursos

1. [Dicas e truques de depuração](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=pt-BR#debugging-aem-as-a-cloud-service)
1. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=pt-BR#debugging)
1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=pt-BR) (disponível somente em ambientes de desenvolvimento SDK e Experience Manager Cloud locais)
1. [Logs e logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=pt-BR#debugging)

   * [Logs CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=pt-BR#debugging) (teste de unidade de compilação, verificação de código, imagem de compilação, implantação)
   * [Logs do Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=pt-BR#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Logs locais do SDK (no host:port/crx-quickstart/logs)

>[!NOTE]
>
> Para obter ajuda adicional, talvez você queira:
>
>1. [Contate a Equipe de Suporte da Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=pt-BR)
>1. Explore [Fóruns e comunidades do Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=pt)

<br>

## Migração para o Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Migração para o Adobe Experience Manager as a Cloud Service"
>abstract="Este resumo descreve a abordagem em fases recomendada para fazer a transição de clientes de várias implantações do Experience Manager para o Experience Manager as a Cloud Service e ajudar os clientes existentes a fornecer experiências conectadas e contínuas nesta plataforma moderna e específica para gerenciamento de experiências."

**O Experience Manager as a Cloud Service fornece uma base de tecnologia escalável, segura e ágil para Experience Manager Sites e Assets, permitindo que profissionais de marketing e TI se concentrem em fornecer experiências de impacto em grande escala.**

Com o Experience Manager as a Cloud Service, suas equipes podem se concentrar em inovar em vez de planejar atualizações de produtos. Os novos recursos do produto são totalmente testados e entregues às suas equipes, sem interrupção, para que elas sempre tenham acesso ao aplicativo mais avançado.

A jornada de transição para o Cloud Service envolve três fases - Planejamento, Execução e Pós ativação.
Para uma transição tranquila e bem-sucedida, você deve garantir um planejamento adequado e seguir as melhores práticas descritas neste Guia.

A figura abaixo mostra uma representação de alto nível da jornada de transição recomendada para o Cloud Service.

![Representação de alto nível da jornada de transição recomendada para o Cloud Service](/help/journey-migration/assets/home-img1.png)

<br>

### Planejamento

Antes de iniciar a jornada de transição para o Cloud Service, você deve:

* familiarize-se com o Experience Manager as a Cloud Service
* revisar as alterações notáveis que foram feitas
* revise os recursos que foram substituídos ou descontinuados

<table>
<tr>
<td>Detecção e avaliação de projetos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=pt-BR">Alterações importantes no Experience Manager as a Cloud Service</a> para entender as diferenças importantes entre o Adobe Experience Manager as a Cloud Service e o Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=pt-BR">Recursos obsoletos</a> para saber mais sobre os recursos e funcionalidades que foram marcados como obsoletos.</li><li>[Somente para migrações do Cloud Service] Avaliando prontidão do Cloud Service: Execute o <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=pt-BR">Analisador de Práticas Recomendadas(BPA)</a> no ambiente de origem </li><li>Concluir uma avaliação contra alterações importantes e recursos obsoletos no Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Revisar</td>
<td><ul><li>Com base na detecção, realizar uma estimativa de esforço e exercícios de recursos</li></ul></td>
</tr>
<tr>
<td>Medir</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Estabelecer KPIs do projeto</a>, critérios de sucesso e linhas do tempo do projeto</li></ul></td>
</tr>
</table>

>[!NOTE]
>O Relatório do Analisador de práticas recomendadas acelera o processo de estimativa do tempo e o custo necessário para a transição para o AEM as a Cloud Service, fornecendo informações que de outra forma precisariam ser coletadas e avaliadas manualmente.


<br>

### Execução

Antes de iniciar a fase de execução de um projeto, você deve estar integrado ao Cloud Service. Você também precisa se familiarizar com o Cloud Manager. Esse é o mecanismo para implantar o código do projeto em uma instância do Experience Manager Cloud Service.

O Cloud Manager permite que as organizações gerenciem manualmente o Experience Manager na nuvem. Ele inclui uma estrutura de integração contínua e entrega contínua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=pt-BR)) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança.

#### Migração de conteúdo

1. [Ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=pt-BR#migration) : usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.
1. [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR#package-manager) : usado para importar e exportar conteúdo mutável do repositório.


#### Refatorar/Otimizar

| Introdução | Código de revisão e refatoração | Análise da Dispatcher |
|---|---|---|
| <ul><li>[Configuração de Desenvolvimento Local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR#local-development-environment-set-up)</li><li>[Instalação do Dispatcher Local](https://video.tv.adobe.com/v/33175?captions=por_br)</li><li>[Compilar o código usando o jar de API do SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR)</li><li>[Revisar Diretrizes de Desenvolvimento da AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR)<ul><li>Tarefas de segundo plano e tarefas de longa duração</li><li>Agendadores Sling</li><li>Uso do fluxo de entrada e muito mais</li></ul></li></ul> | <ul><li>Execute o [Analisador de Práticas Recomendadas(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=pt-BR) no ambiente de origem.[**Somente migração**]<ul><li>Considerações de Estruturação de Projeto (com base no [Arquétipo de Nuvem](https://github.com/adobe/aem-project-archetype))<ul><li>Separação de código e conteúdo (mutável vs. imutável)</li><li>[Definições de índice personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=pt-BR)</li><li>[Runmodes personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=pt-BR)</li></ul></li></ul></li><li>Revisar e executar as alterações necessárias</li><li>[Implantar](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) no SDK local</li><li>Realizar testes de fumaça por meio do AEM SDK</li></ul> | <ul><li>Revise as [configurações do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=pt-BR) para refatoração</li><li>Use a ferramenta [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=pt-BR) onde apropriado. [**Somente migração**]</li><li>Os testes podem ser conduzidos usando o [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=pt-BR#prerequisites)</li></ul> |

>[!TIP]
> Clientes do Assets: revise e refatore fluxos de trabalho do Assets usando a ferramenta [Migração da nuvem de ativos](https://github.com/adobe/aem-cloud-migration)


#### Implantação/ativação

1. [Implantar no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=pt-BR) Git
2. Execute o código do cliente por meio do [Cloud Manager Quality Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=pt-BR)
3. [Implantar no Ambiente de Desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=pt-BR#debugging)
4. **Somente migração** Transferência de conteúdo usando pacotes ou [Ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Executar ciclos de teste recomendados (fumaça, controle de qualidade e muito mais)
6. Promover para o pipeline de produção do Cloud Manager
7. Validação do teste de fumaça
8. Publicação

<br>

### Pós-ativação

Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

>[!TIP]
>
> As ferramentas estão disponíveis para solucionar problemas do ambiente do AEM as a Cloud Service
>
>1. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR)
>1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=pt-BR)
>1. [Gerenciamento de logs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=pt-BR)

<br>

### Ferramentas e recursos

| Avaliação | Refatoração | Modernização do Experience Manager | Migração de conteúdo |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=pt-BR)</li></li> | <ul><li>[Plug-in de Experiência Unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=pt-BR)</li></ul> | <ul><li>[Modelos estáticos em modelos editáveis](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Configurações de design para políticas](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componentes de base para Componentes principais](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[Interface clássica para interface habilitada para toque](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR)</li><li>[Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR#contentmanagement)</li></ul> |

>[!NOTE]
>
> Para obter ajuda adicional, talvez você queira:
>
>1. [Contate a Equipe de Suporte da Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=pt-BR)
>1. Explore [Fóruns e comunidades do Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=pt)
