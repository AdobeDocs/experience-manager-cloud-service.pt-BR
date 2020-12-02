---
title: Migração para o Experience Manager como Cloud Service
description: Migração para o Experience Manager como Cloud Service
translation-type: tm+mt
source-git-commit: 3c1ff52d58f64d351507d20e4368a6aeb1bf6339
workflow-type: tm+mt
source-wordcount: '2070'
ht-degree: 8%

---


# Migração para a Adobe Experience Manager como Cloud Service {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration-overview"
>title="Migração para AEM como um serviço em nuvem"
>abstract="Descreve a abordagem em fases recomendada para clientes de transição de várias implantações de Experience Manager para Experience Manager como Cloud Service e ajuda os clientes existentes a fornecerem experiências contínuas e conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="Novidades e diferentes?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="Introdução ao AEM as a Cloud Service."

A Adobe Experience Manager (AEM) como Cloud Service oferta  é uma fundação reformulada para o Experience Manager, construída sobre uma infraestrutura baseada em container, desenvolvimento orientado por API e processo DevOps orientado, permitindo que os profissionais de marketing e desenvolvedores continuem sempre à frente das inovações do gerenciamento da experiência do cliente.

O Cloud Service reúne recursos avançados e abrangentes da Adobe Experience Manager com agilidade da arquitetura moderna nativa da nuvem, permitindo que as marcas atendam à demanda sempre crescente dos consumidores.

Este único pager descreve a abordagem por etapas recomendada para clientes de transição, desde várias implantações de Experience Manager para o Experience Manager como Cloud Service, e ajuda os clientes existentes a fornecer experiências contínuas e conectadas nessa plataforma moderna e criada especificamente para o gerenciamento de experiências.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Introdução ao Adobe Experience Manager como Cloud Service {#getting-started}

| O que é diferente? | Visão geral da arquitetura |
|--------------------------|--------------------------|
| <ul><li>[Arquitetura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Atualizações automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Microserviços de ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Binários de acesso direto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[Separação do código e do conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Replicação como um serviço](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[Admin Console, associação de grupo/usuário e ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[Introdução à arquitetura AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Pilha de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Camada do autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Publicar camada](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Gerenciador](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)  de nuvem (CI/CD)</li><li>[Gerenciamento ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) de identidade via console  [de administração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[Serviço de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - Arquitetura do tempo de execução](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - Arquitetura do tempo de execução")

<br>

## Jornada do desenvolvedor no Adobe Experience Manager como Cloud Service {#developer-journey}

### Desenvolvimento

Os fundamentos do desenvolvimento de código são semelhantes no Adobe Experience Manager como um Cloud Service em comparação às soluções Adobe Experience Manager On Premise e Managed Services.

Os desenvolvedores gravam o código e o testam localmente, que é então enviado para o Adobe Experience Manager remoto como ambientes Cloud Service.

Veja os recursos de autoajuda sobre a implementação do Experience Manager como Cloud Service para saber como personalizar seu Experience Manager como uma implantação Cloud Service.

| Configuração de desenvolvimento local | As coisas que você deve saber antes do start |
|-----------|------------|
| <ol><li>Consulte a documentação [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) para saber mais.</li><li>Assista [Instale o Dispatcher SDK](https://video.tv.adobe.com/v/30601?captions=por_br) para entender como instalar o Dispatcher SDK</li><li>Assista [Configure o Dispatcher SDK](https://video.tv.adobe.com/v/30602?captions=por_br) para entender como configurar o Dispatcher SDK</li><li>Consulte a documentação [Configuração de Desenvolvimento Local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) para saber mais</li><li>Configurando o acesso a Experience Manager [caminhada](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Princípios básicos de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Noções Gerais da Estrutura do Projeto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[Sobreposições](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Experience Manager como uma referência de API Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> Consulte o tutorial sobre como [Desenvolver e implantar o WKND no Experience Manager SDK local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### Implantação

Os desenvolvedores gravam o código e o testam localmente, que é então enviado para o AEM remoto como um ambiente Cloud Service.

O Cloud Manager, que era uma ferramenta de delivery de conteúdo opcional para Managed Services, é necessário. Esse agora é o único mecanismo para implantar código para AEM como ambientes Cloud Service.

Veja os recursos de autoajuda sobre como configurar e implantar em AEM como ambientes Cloud Service.

1. [Configurar Pipelines CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * Pipeline de produção
   * Pipelines que não são de produção e qualidade de código
2. [Implantar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [Como entender seus resultados de teste](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **Acessar registros**
   * [via interface do usuário do CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [via Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operações e Manutenção](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [Configuração de OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [Backup e restauração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> Consulte o tutorial sobre como [Implantar WKND para Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### Ajuda e recursos

1. [Dicas e truques de depuração](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (Disponível somente nos ambientes de desenvolvedores locais do SDK e da Experience Manager Cloud)
4. [Logs e registros](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)  CM (teste de unidade de compilação, digitalização de código, compilação-imagem, implantação)
   * [Experience Manager Cloud Service Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Logs SDK locais (em host:porta/crx-quickstart/logs)

>[!NOTE]
> Para obter ajuda adicional, talvez você queira:
>1. [Entre em contato com a equipe de suporte do Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explore [Comunidades e Fóruns Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Mudar para o Adobe Experience Manager como um Cloud Service {#move-to-cloud}

**O Experience Manager como Cloud Service oferece uma base tecnológica escalável, segura e ágil para os Experience Manager Sites e Assets, permitindo que os profissionais de marketing e de TI se concentrem em fornecer experiências impactantes em escala.**

Com o Experience Manager como Cloud Service, suas equipes podem se concentrar em inovar em vez de planejar atualizações de produtos. Os novos recursos do produto são exaustivamente testados e entregues às suas equipes, sem interrupção, para que elas sempre tenham acesso ao aplicativo mais moderno e atual.

A jornada de transição para o Cloud Service envolve três fases - Planejamento, Execução e Pós ativação.
Para uma transição tranquila e bem-sucedida, você deve garantir um planejamento adequado e seguir as melhores práticas descritas neste Guia.

A figura abaixo mostra uma representação visual da jornada de transição recomendada para o Cloud Service.

![imagem](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### Planejamento

Antes de iniciar sua jornada de transição, você deve se familiarizar com Experience Manager como Cloud Service, revisar as mudanças notáveis que foram feitas e também revisar os recursos que foram substituídos ou desaprovados.

<table>
<tr>
<td>Detecção e avaliação de projetos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Alterações notáveis no Experience Manager como um Cloud Service</a> para entender as diferenças importantes entre o Adobe Experience Manager como Cloud Service e Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">Recursos obsoletos</a> para saber mais sobre recursos e recursos que foram marcados como obsoletos.</li><li>[Somente para migrações Cloud Service] Avaliando a prontidão dos Cloud Service: Execute o <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer(BPA)</a> no ambiente de origem </li><li>Conclua uma avaliação contra alterações notáveis e recursos obsoletos no Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Análise</td>
<td><ul><li>Com base na descoberta, faça exercícios de estimativa de esforço e de recursos</li></ul></td>
</tr>
<tr>
<td>Medida</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Estabelecer KPIs</a> do projeto, critérios de sucesso e linhas do tempo do projeto</li></ul></td>
</tr>
</table>

>[!NOTE]
>O Relatório do Analisador de Práticas Recomendadas acelera o processo de estimativa do tempo e custo necessários para a transição, fornecendo informações que, de outra forma, precisariam ser coletadas e avaliadas manualmente.


<br>

### Execução

Antes de start da fase de execução de um projeto, você deve estar a bordo do Cloud Service. Você também precisa se familiarizar com o Cloud Manager. Este é o mecanismo para implantar o código do projeto em uma instância Experience Manager Cloud Service.

O Cloud Manager permite que as organizações gerenciem o Experience Manager na nuvem por conta própria. Ele inclui uma integração contínua e uma estrutura de delivery contínua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview)) que permite que equipes de TI e parceiros de implementação acelerem o delivery de personalizações ou atualizações sem comprometer o desempenho ou a segurança.

#### Migração de conteúdo

1. [Ferramenta](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration)  de transferência de conteúdo: usado para mover o conteúdo existente de uma instância de AEM de origem (local ou AMS) para a instância de Cloud Service de público alvo AEM.
2. [Gerenciador](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager)  de pacotes: usado para importar e exportar conteúdo mutável do repositório.


#### Refator/Otimizar

| Introdução | Revisar e Refatorar código | Revisão do Dispatcher |
|---|---|---|
| <ul><li>[Configuração Local do Dev](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Configuração local do Dispatcher](https://video.tv.adobe.com/v/30602/?captions=por_br)</li><li>[Compile seu código usando o jar da API do SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Revisar AEM diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>Tarefas em segundo plano e trabalhos de longa execução</li><li>Scheduleres Sling</li><li>Uso do fluxo de entrada e muito mais</li></ul></li></ul> | <ul><li>Execute o [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) no ambiente de origem.[**Somente migração**]<ul><li>Considerações sobre a estrutura do projeto (com base em [Cloud Archetype](https://github.com/adobe/aem-project-archetype))<ul><li>Separação de código e conteúdo (mutável vs imutável)</li><li>[Definições de índice personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[Modos de execução personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>Revisar e executar as alterações necessárias</li><li>[](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) Implantar no SDK local</li><li>Executar teste de fumaça via AEM SDK</li></ul> | <ul><li>Revisar [Configurações do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) para refatoração</li><li>Aproveite a ferramenta [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher) quando apropriado. [**Somente migração**]</li><li>O teste pode ser realizado usando [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clientes do Assets: Analisar e Refatorar Workflows de ativos usando a ferramenta [Migração do Asset Cloud](https://github.com/adobe/aem-cloud-migration)


#### Implantação/Ao Vivo

1. [Implantar no Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Manager
2. Execute o código do cliente pelo [pipeline de qualidade do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [Implantar no Ambiente de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Migração**] somenteTransferência de conteúdo usando pacotes ou Ferramenta [ de transferência de ](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)conteúdo (CTT)
5. Executar ciclos de teste recomendados (fumaça, controle de qualidade e muito mais)
6. Promover o pipeline de produção do Cloud Manager
7. Validação do ensaio de fumos
8. Go-Live

<br>

### Publicar ao vivo

Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

>[!TIP]
> As ferramentas estão disponíveis para solucionar problemas de AEM como ambientes Cloud Service
>1. [Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [Gerenciamento de logs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### Ferramentas e recursos

| Avaliação | Refatoração | Modernização Experience Manager | Migração de conteúdo |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Plug-in de experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[Modelos estáticos em modelos editáveis](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[Configurações de design em políticas](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[Componentes básicos em componentes principais](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[IU Clássica em IU ativada por toque](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Para obter ajuda adicional, talvez você queira:
>1. [Entre em contato com a equipe de suporte do Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explore [Comunidades e Fóruns Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

