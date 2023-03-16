---
title: Guia de migração para o Experience Manager as a Cloud Service para parceiros
description: Guia de migração para o Experience Manager as a Cloud Service para parceiros
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 13%

---

# Guia de migração para o Adobe Experience Manager as a Cloud Service for Partners {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migração para o AEM as a Cloud Service"
>abstract="Descreve a abordagem em fases recomendada para clientes de transição de várias implantações de Experience Manager para o Experience Manager as a Cloud Service e ajuda os clientes existentes a fornecer experiências contínuas e conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="Novidades e diferenças?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="Introdução ao AEM as a Cloud Service."

O Adobe Experience Manager (AEM) as a Cloud Service oferece uma base reformulada para o Experience Manager, baseada em uma infraestrutura baseada em contêiner, desenvolvimento orientado por API e processo DevOps orientado, permitindo que os profissionais de marketing e desenvolvedores continuem sempre à frente da curva nas inovações de gerenciamento de experiência do cliente.

O Cloud Service reúne recursos avançados e prontos para uso do Adobe Experience Manager com a agilidade da arquitetura moderna nativa em nuvem, permitindo que as marcas atendam às demandas sempre em evolução do consumidor.

Esse único pager descreve a abordagem de fases recomendada para clientes de transição de várias implantações de Experience Manager para o Experience Manager as a Cloud Service e ajuda os clientes existentes a fornecer experiências contínuas e conectadas nessa plataforma moderna e criada especificamente para o gerenciamento de experiências.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Consulte o diagrama abaixo para obter uma representação geral da jornada de migração.

![imagem](/help/journey-migration/assets/migration-process.png)

## Introdução ao Adobe Experience Manager as a Cloud Service {#getting-started}

| O que é diferente? | Visão geral da arquitetura |
|--------------------------|--------------------------|
| <ul><li>[Arquitetura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Atualizações automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[Microsserviços de ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Binários de acesso direto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[Separação de código e conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Replicação como um serviço](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=en)</li><li>[Admin Console, Associação de Grupo/Usuário e ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[Introdução à arquitetura de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Pilha de ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Camada do autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Publicar camada](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[Serviço Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - Arquitetura do tempo de execução](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - Arquitetura do tempo de execução")

<br>

## Jornada do desenvolvedor no Adobe Experience Manager as a Cloud Service {#developer-journey}

### Desenvolvimento

Os fundamentos do desenvolvimento de código são semelhantes no Adobe Experience Manager as a Cloud Service em comparação às soluções Adobe Experience Manager no local e Managed Services.

Os desenvolvedores gravam o código e o testam localmente, que é então enviado para ambientes remotos de Adobe Experience Manager as a Cloud Service.

Consulte os recursos de autoajuda sobre implementação do Experience Manager as a Cloud Service para saber como personalizar a implantação as a Cloud Service do Experience Manager.

| Configuração de desenvolvimento local | O que você deve saber antes de começar |
|-----------|------------|
| <ol><li>Revisão [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) documentação para saber mais.</li><li>Observar [Instalar o SDK do Dispatcher](https://video.tv.adobe.com/v/30601) para entender como instalar o SDK do Dispatcher</li><li>Observar [Configurar o SDK do Dispatcher](https://video.tv.adobe.com/v/30602) para entender como configurar o SDK do Dispatcher</li><li>Revisão [Configuração de desenvolvimento local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) documentação para saber mais</li><li>Configuração do acesso ao Experience Manager [caminhada](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Princípios básicos de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[Noções básicas sobre a estrutura do projeto do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[Sobreposições](/help/implementing/developing/introduction/overlays.md)</li><li>[Referência da API do Experience Manager as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Consulte tutorial sobre como [Desenvolver e implantar o WKND no SDK do Experience Manager local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)

### Implantação

Os desenvolvedores criam o código e o testam localmente, e depois o enviam para ambientes remotos do AEM as a Cloud Service.

O uso do Cloud Manager, que era uma ferramenta opcional de entrega de conteúdo do Managed Services, é obrigatório. Ele agora é o único mecanismo para implantar código nos ambientes do AEM as a Cloud Service.

Consulte os recursos de autoajuda sobre como configurar e implantar em ambientes AEM as a Cloud Service.

1. [Configurar pipeline CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * Pipeline de produção
   * Pipelines somente para não-produção e qualidade de código
2. [Implantar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [Noções básicas dos resultados de teste](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **Acessar logs**
   * [via interface do usuário do CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [por cli de e/s do Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operações e manutenção](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [Configuração do OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [Backup e restauração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> Consulte tutorial sobre como [Implantar WKND no Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)

### Ajuda e recursos

1. [Dicas e truques para depuração](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (Disponível somente em ambientes locais de SDK e Experience Manager Cloud Dev)
4. [Logs e registro](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Logs do CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (teste de unidade de compilação, verificação de código, compilação de imagem, implantação)
   * [Logs de Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Logs locais do SDK (em host:port/crx-quickstart/logs)

>[!NOTE]
> Para obter ajuda adicional, talvez você queira:
>1. [Entre em contato com a equipe de suporte do Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explorar [Experience Manager Communities e fóruns](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Migração para o Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Migração para o Adobe Experience Manager as a Cloud Service"
>abstract="Esse único pager descreve a abordagem de fases recomendada para clientes de transição de várias implantações de Experience Manager para o Experience Manager as a Cloud Service e ajuda os clientes existentes a fornecer experiências contínuas e conectadas nessa plataforma moderna e criada especificamente para o gerenciamento de experiências."

**O Experience Manager as a Cloud Service oferece uma base de tecnologia escalável, segura e ágil para Experience Manager Sites e Assets, permitindo que os profissionais de marketing e TI se concentrem em fornecer experiências impactantes em escala.**

Com o Experience Manager as a Cloud Service, suas equipes podem se concentrar em inovar em vez de planejar atualizações de produtos. Os novos recursos do produto são totalmente testados e entregues às suas equipes, sem interrupção, para que elas sempre tenham acesso ao aplicativo mais avançado.

A jornada de transição para o Cloud Service envolve três fases - Planejamento, Execução e Pós ativação.
Para uma transição tranquila e bem-sucedida, você deve garantir um planejamento adequado e seguir as melhores práticas descritas neste Guia.

A figura abaixo mostra uma representação de alto nível da jornada de transição recomendada para o Cloud Service.

![imagem](/help/journey-migration/assets/home-img1.png)

<br>

### Planejamento

Antes de iniciar a jornada de transição para o Cloud Service, você deve se familiarizar com o Experience Manager as a Cloud Service e revisar as alterações notáveis que foram feitas nele, além de revisar os recursos que foram substituídos ou obsoletos.

<table>
<tr>
<td>Detecção e avaliação de projetos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=pt-BR">Alterações importantes no Experience Manager as a Cloud Service</a> para compreender as diferenças importantes entre o Adobe Experience Manager as a Cloud Service e o Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">Recursos obsoletos</a> para saber mais sobre os recursos e funcionalidades que foram marcados como obsoletos.</li><li>[Somente para migrações Cloud Service] Avaliação da prontidão do Cloud Service : Execute o <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">BPA (Best Practices Analyzer)</a> no ambiente de origem </li><li>Conclua uma avaliação contra alterações notáveis e recursos obsoletos no Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Análise</td>
<td><ul><li>Com base na descoberta, faça exercícios de estimativa de esforço e recursos</li></ul></td>
</tr>
<tr>
<td>Medição</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Estabelecer KPIs de Projeto</a>, critérios de sucesso e prazos do projeto</li></ul></td>
</tr>
</table>

>[!NOTE]
>O Relatório do Analisador de Práticas Recomendadas acelera o processo de estimativa do tempo e custo necessários para a transição para o AEM as a Cloud Service, fornecendo informações que de outra forma precisariam ser coletadas e avaliadas manualmente.


<br>

### Execução

Antes de iniciar a fase de execução de um projeto, você deve estar integrado ao Cloud Service. Você também precisa se familiarizar com o Cloud Manager. Esse é o mecanismo para implantar o código do projeto em uma instância do Experience Manager Cloud Service.

O Cloud Manager permite que as organizações autogerenciem o Experience Manager na nuvem. Inclui integração contínua e entrega contínua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en)) estrutura que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações sem comprometer o desempenho ou a segurança.

#### Migração de conteúdo

1. [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) : usado para mover o conteúdo existente de uma instância de AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.
2. [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) : usado para importar e exportar conteúdo mutável do repositório.


#### Refatorar/Otimizar

| Introdução | Código de Revisão e Refatoração | Revisão do Dispatcher |
|---|---|---|
| <ul><li>[Configuração de Desenvolvimento Local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Configuração local do Dispatcher](https://video.tv.adobe.com/v/30602/)</li><li>[Compile seu código usando o jar da API do SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Revisar AEM diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>Tarefas em Segundo Plano e Trabalhos de Longa Execução</li><li>Agendadores Sling</li><li>Uso do fluxo de entrada e muito mais</li></ul></li></ul> | <ul><li>Execute o [BPA (Best Practices Analyzer)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) no ambiente de origem.[**Somente migração**]<ul><li>Considerações sobre a estrutura do projeto (com base em [Arquétipo da nuvem](https://github.com/adobe/aem-project-archetype))<ul><li>Separação de código e conteúdo (variável vs imutável)</li><li>[Definições de índice personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[Modos de execução personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>Revisar e executar as alterações necessárias</li><li>[Implantar](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) no SDK local</li><li>Realizar teste de fumaça via SDK AEM</li></ul> | <ul><li>Revisão [Configurações do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) para refatoração</li><li>Use [Conversor do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) ferramenta, se necessário. [**Somente migração**]</li><li>Os testes podem ser realizados usando [SDK do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clientes de ativos : Fluxos de trabalho de revisão e redefinição de ativos usando [Migração da Asset Cloud](https://github.com/adobe/aem-cloud-migration) ferramentas


#### Implantação/ativação

1. [Implantar no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. Execute o código do cliente por meio da [Pipeline de qualidade do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [Implantar no ambiente de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Somente migração**] Transferência de conteúdo através de pacotes ou [Ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(TPC)
5. Executar ciclos de teste recomendados (fumaça, QA e muito mais)
6. Promover para o pipeline de produção do Cloud Manager
7. Validação do ensaio de fumo
8. Publicação

<br>

### Pós-ativação

Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

>[!TIP]
> As ferramentas estão disponíveis para solucionar problemas AEM ambiente as a Cloud Service
>1. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [Gerenciamento de logs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)


<br>

### Ferramentas e recursos

| Avaliação | Refatoração | Modernização Experience Manager | Migração de conteúdo |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Plug-in de experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[Modelos estáticos em modelos editáveis](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Configurações de design em políticas](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componentes de base para Componentes principais](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[IU Clássica em IU ativada por toque](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR)</li><li>[Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Para obter ajuda adicional, talvez você queira:
>1. [Entre em contato com a equipe de suporte do Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explorar [Experience Manager Communities e fóruns](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

