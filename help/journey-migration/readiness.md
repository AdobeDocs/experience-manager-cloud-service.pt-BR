---
title: Fase de preparação
description: Saiba mais sobre as etapas necessárias para garantir que a instalação do AEM esteja pronta para ser movida para a nuvem.
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
feature: Migration
role: Admin
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 6%

---

# Fase de preparação {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planejamento da transição"
>abstract="Antes de iniciar sua jornada de transição para o Cloud Service, acostume-se com o AEM as a Cloud Service. Analise as alterações notáveis feitas e os recursos que foram substituídos ou descontinuados."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=pt-BR" text="Analisador de práticas recomendadas"

Nesta fase da Jornada de migração do AEM as a Cloud Service, você se familiariza com o AEM as a Cloud Service. Você pode analisar as alterações notáveis introduzidas e entender o que é necessário para planejar uma migração bem-sucedida para a nuvem.

## A história até agora {#story-so-far}

O documento anterior, [Introdução à migração para o AEM as a Cloud Service](/help/journey-migration/getting-started.md), descreve uma lista de fases que devem ser realizadas para que você possa migrar para o AEM as a Cloud Service. Ele também descreve os benefícios de fazer a migração.

## Objetivo {#objective}

Este documento ajuda você a entender quais fatores devem ser considerados para garantir que a instalação do AEM esteja pronta para ser movida para a nuvem:

* Saiba mais sobre alterações notáveis e recursos obsoletos
* Entenda como planejar a migração para o AEM as a Cloud Service

## Revise as alterações importantes na arquitetura do AEM as a Cloud Service {#notable-changes-in-aem-cloud-service-architecture}

O AEM as a Cloud Service traz muitos novos recursos e possibilidades para gerenciar seus projetos AEM.

Juntamente com essas melhorias, foram introduzidas várias diferenças entre as instalações locais do AEM e do Adobe Managed Services, em comparação com o AEM as a Cloud Service.

A lista de itens na tabela abaixo é o subconjunto das alterações mais relevantes para uma migração para o AEM as a Cloud Service. Você pode consultar a lista completa de [Alterações importantes no Adobe Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>O que mudou?</th>
    <th>Referência</th>
    <th>Principais pontos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separe filtros mutáveis e imutáveis em pacotes correspondentes</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=pt-BR">Alterações importantes do AEM as a Cloud Service</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR#mutable-vs-immutable">Estrutura de projeto AEM para AEM as a Cloud Service</a></td>
    <td>Um único pacote que pode ser implantado no AEM as a Cloud Service pode ter pacotes secundários, principalmente para conter conteúdo mutável e imutável separado em seus próprios pacotes.</td>
  </tr>
  <tr>
    <td>Inicialização do repositório</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentação do Apache Sling RepoInit</a></td>
    <td>Os scripts de repoinit são a prática recomendada para criar qualquer estrutura de nó inicial, usuário, grupo ou usuário de serviço. Como esses scripts podem ser direcionados pelo modo de execução e gerenciados por meio da implantação de pacotes de códigos, eles fornecem muita flexibilidade para realizar tarefas de inicialização de repositório.</td>
  </tr>
  <tr>
    <td>Modos de execução personalizados não são permitidos</td>
    <td></td>
    <td>Somente os modos de execução fornecidos com o AEM as a Cloud Service são compatíveis.<br>Quando outros ambientes de desenvolvimento são adicionados, todos eles se vinculam ao modo de execução "dev".</td>
  </tr>
  <tr>
    <td>A execução do pipeline Cloud Manager é a única maneira de implantar</td>
    <td></td>
    <td>No AEM as a Cloud Service, o acesso a /system/console não é permitido, portanto, todas as configurações de OSGi devem fazer parte do código e devem ser implantadas como código.<br>As configurações de OSGi estão disponíveis no modo somente leitura para visualização no Developer Console por meio do Cloud Manager</td>
  </tr>
  <tr>
    <td>Os agentes de replicação são substituídos pelo Sling Content Distribution</td>
    <td></td>
    <td>O conceito do agente de replicação é substituído por Sing Content Distribution. Se houver personalizações que usam agentes de replicação, elas deverão ser reprojetadas.<br>Não há suporte para replicação inversa</td>
  </tr>
  <tr>
    <td>CRX/DE e Gerenciador de pacotes</td>
    <td></td>
    <td>CRX/DE é permitido somente no ambiente de desenvolvimento.<br>O Gerenciador de Pacotes pode ser acessado em todas as instâncias do autor, mas os pacotes que serão implantados devem conter apenas conteúdo mutável ( por exemplo: /content ou /conf)</td>
  </tr>
  <tr>
    <td>CDN integrada e Obter seu próprio CDN</td>
    <td></td>
    <td>O AEM as a Cloud Service inclui a CDN para todos os ambientes, que é otimizada para a maioria dos casos de uso.<br>Se quiser configurar seu próprio CDN, envie uma solicitação ao Suporte do Adobe para que ele seja aprovado.<br>Se aprovada, a CDN aponta para o Fastly e não para instâncias do AEM em nenhum ambiente.</td>
  </tr>
  <tr>
    <td>Trabalhos de Longa Execução</td>
    <td></td>
    <td>Evite tarefas de longa execução, como Sling Schedulers ou trabalhos Cron, já que as instâncias do AEM em execução nos contêineres podem vir e ir a qualquer momento.<br>Repense essas funcionalidades para descarregá-las no Adobe Developer.</td>
  </tr>
  <tr>
    <td>Alternar para operações assíncronas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html?lang=pt-BR#configuring-asynchronous-msm-operations">Configurar operações assíncronas</a></td>
    <td>Para melhorar o desempenho geral de seus ambientes, determinadas operações são executadas no modo assíncrono. Os trabalhos assíncronos são enfileirados e executados quando os recursos do sistema estão disponíveis.</td>
  </tr>
  <tr>
    <td>Estratégias de autenticação e integração baseadas em token</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=pt-BR#the-server-to-server-flow">Gerando tokens de acesso para APIs do lado do servidor</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=pt-BR#authentication">Tutorial de autenticação baseado em token</a></td>
    <td>É comum que sistemas externos ao AEM estejam tentando executar operações HTTP dentro do AEM.<br>A abordagem recomendada é implementar as estratégias descritas aqui em vez de depender da criação de nomes de usuários locais com senhas no AEM.</td>
  </tr>
  <tr>
    <td>Uso de E/S de arquivo/disco</td>
    <td></td>
    <td>Não há garantia de quanto espaço em disco é alocado, e as instâncias em contêineres vêm e vão. Portanto, não é aconselhável usar operações de E/S de arquivo para gravar ou ler o disco anexado à instância do AEM.</td>
  </tr>
  <tr>
    <td>Fluxo de trabalho do Ativo de atualização DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=pt-BR">Serviço Asset Compute</a></td>
    <td>As etapas de processamento de mídia que fazem parte do fluxo de trabalho Atualizar ativo do DAM agora são substituídas pelo Serviço do Asset Compute</td>
  </tr>
  <tr>
    <td>Métodos de upload de ativos e etapas do processo de fluxo de trabalho compatíveis no AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html?lang=pt-BR#post-processing-workflows-steps">Fazer upload de comparações de API e etapas do processo WF compatíveis</a></td>
    <td>No AEM as a Cloud Service, durante o upload ou download de um ativo, o ativo flui diretamente para dentro ou para fora do armazenamento binário. <br>Nem todas as etapas do processo de fluxo de trabalho são suportadas no AEMaaCS.</td>
  </tr>
  <tr>
    <td>Inicializadores do fluxo de trabalho</td>
    <td></td>
    <td>Remova todos os Iniciadores de fluxo de trabalho que estão acionando o fluxo de trabalho de ativos de atualização do DAM pronto para uso ou personalizado do seu código. <br>Todos os ativos carregados na AEM as a Cloud Service serão processados pelo Serviço de Processamento de Ativos. Para ver etapas personalizadas, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=pt-BR#post-processing-workflows"> Fluxos de Trabalho de Pós-Processamento</a> sobre como configurar fluxos de trabalho de pós-processamento.</td>
  </tr>
  <tr>
    <td>Etapas de representação personalizadas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=pt-BR">Processando perfis</a></td>
    <td>Qualquer geração de representação personalizada, conversões de imagem ou codificações de vídeo devem ser descarregadas no Serviço de processamento de ativos, criando perfis de processamento correspondentes.</td>
  </tr>
  <tr>
    <td>Pesquisa e indexação de conteúdo</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=pt-BR">Alterações de pesquisa e indexação de conteúdo</a></td>
    <td>Há alterações consideráveis no processamento subjacente de índices e no momento em que ele é iniciado.<br>Compreenda e refatore completamente os índices do Oak antes de gerenciá-los no código que você implantou.</td>
  </tr>
  <tr>
    <td>Nem todas as tarefas de manutenção são configuráveis</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html?lang=pt-BR">Tarefas de manutenção do AEM as a Cloud Service</a></td>
    <td>Você pode configurar apenas determinadas tarefas de manutenção com o AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>Alterações no repositório do Publish</td>
    <td></td>
    <td>Não são permitidas alterações diretas no repositório do Publish, exceto aquelas alterações em /home. É sempre recomendável que qualquer alteração feita no autor seja distribuída. Todas as alterações de código e configuração devem ser implantadas por meio do pipeline correspondente do Cloud Manager.</td>
  </tr>
  <tr>
    <td>Configurações e armazenamento em cache do Dispatcher</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=pt-BR">Dispatcher na nuvem</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html?lang=pt-BR#other-content">Gerenciamento de cache<br></td>
    <td>As configurações do Dispatcher devem seguir uma estrutura específica.<br>As configurações devem ser gerenciadas como parte do código e implantadas por meio do pipeline do Cloud Manager.</td>
  </tr>
  <tr>
    <td>Backup e restauração</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=pt-BR">Backup e restauração do AEM as a Cloud Service</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Alterações na autenticação</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR">Suporte IMS do AEM as a Cloud Service</td>
    <td>Se você estava usando anteriormente a integração SAML 2.0 no autor e na publicação antes de migrar para o Cloud Service, a principal alteração é que o AEM as a Cloud Service Author só se integra ao Adobe IMS. No entanto, o nível do AEM as a Cloud Service Publish ainda pode usar o SAML ou outras integrações de autenticação. O AEM as a Cloud Service oferece suporte à autenticação IMS somente para os usuários Autor, Administrador e Desenvolvedor. A autenticação IMS não oferece suporte para usuários finais externos de sites do cliente, como visitantes do site.</td>
  </tr>
</tbody>
</table>

## Recursos obsoletos {#deprecated-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

A Adobe recomenda que você consulte [Recursos obsoletos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=pt-BR#deprecated-features) para se familiarizar com os recursos e funcionalidades marcados como obsoletos no Experience Manager as a Cloud Service. Veja qual é o impacto da sua implementação do AEM.

## Plano para uma revisão da instalação do AEM {#review-planning}

Depois de se familiarizar com as alterações introduzidas no AEM as a Cloud Service, é hora de começar a planejar uma revisão de sua instalação existente. Isso ajuda a medir o nível de alterações necessárias para movê-lo para a nuvem.

A figura a seguir mostra as principais etapas envolvidas durante a fase de revisão:

![Etapas principais envolvidas durante a fase de revisão](/help/journey-migration/assets/planning-phaseimg1.png)

Em seguida, explore detalhadamente o que cada uma dessas etapas significa.

### Avaliação da prontidão do Cloud Service {#assess-cloud-readiness}

O primeiro passo é avaliar sua prontidão para migrar da versão existente do AEM para o Cloud Service e determinar as áreas que exigem que a refatoração seja compatível com o AEM as a Cloud Service.

Faça uma avaliação abrangente do código-fonte AEM atual em relação às alterações notáveis e aos recursos obsoletos para determinar o nível de esforço esperado na jornada de transição.

O número de descobertas pode influenciar diretamente as linhas do tempo e o sucesso geral do projeto. Portanto, a Adobe recomenda que você descubra o máximo possível para que possa planejar o delivery. Ou inicie as conversas para reprojetar as personalizações necessárias para estar em conformidade com as práticas recomendadas da AEM as a Cloud Service.

**Analisador de práticas recomendadas**

Você pode acelerar a avaliação executando o Analisador de práticas recomendadas na versão atual do AEM. Ter uma boa compreensão de como funciona é fundamental para acelerar seu planejamento de avaliação.

Você pode ler como funciona consultando a documentação do [Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

**Criar um Relatório de Avaliação de Disponibilidade para a Nuvem**

A próxima etapa é criar um relatório com base em todo o conhecimento adquirido até o momento. Crie o relatório gerando relatórios do Analisador de práticas recomendadas das instâncias de Preparo e Produção, [carregue-os no Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) para obter um relatório digerível de itens acionáveis.

Um relatório típico deve conter estas entradas:

* Documentação detalhando o conjunto de recursos da sua instalação de AEM específica
* Detalhes sobre suas configurações personalizadas e código AEM
* Configurações do Dispatcher de produção
* Mapeamentos de domínio (configurações de CDN) (se houver)

**Socializar o relatório**

Depois que os relatórios do Analisador de práticas recomendadas forem concluídos, compartilhe-os com as equipes relevantes para que você possa confirmar suas conclusões e planejar as próximas etapas. Dependendo da preferência, você também pode distribuir uma versão impressa do relatório usando a [Visualização de Impressão](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Revisão do planejamento de recursos {#review-resource-planning}

Depois de estimar o nível de esforço necessário para migrar para o Cloud Service, você deve identificar recursos, criar uma equipe e mapear funções e responsabilidades para o processo de transição.

### Estabelecimento de KPIs {#establish-kpis}

Se você não tiver estabelecido Indicadores-chave de desempenho (KPIs) anteriormente, é recomendável estabelecer KPIs para a implementação do AEM para ajudar sua equipe a se concentrar naquilo que é mais importante.

Consulte [Desenvolvendo KPIs](https://experienceleague.adobe.com/welcome/aem/part6.html?lang=pt-BR) para que você possa aprender a escolher os KPIs certos para seus objetivos comerciais.

## O que vem a seguir {#what-is-next}

Depois de entender o escopo das alterações necessárias para migrar para o AEM as a Cloud Service, é hora de [Preparar seu código e sua nuvem de conteúdo](/help/journey-migration/implementation.md) antes de realmente executar a migração.

## Recursos adicionais {#additional-resources}

* [Introdução ao Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Um guia abrangente sobre como usar o Cloud Acceleration Manager para acelerar sua migração para a nuvem.
* [AEM as a Cloud Service: Introdução, Arquitetura e Reflexão Diferentes](https://experienceleague.adobe.com/pt-br?launch=ExperienceManager-D-1-2021.1.migration&recommended=ExperienceManager-D-1-2021.1.migration&lang=en#dashboard/learning)
* [AEM a Cloud Service Home](/help/overview/introduction.md) - Para obter uma visão geral da documentação as a Cloud Service de Experience Manager, comece por aqui.
* [Visão geral do AEM as a Cloud Service](/help/overview/introduction.md) - Este guia fornece uma visão geral do Experience Manager as a Cloud Service, incluindo uma introdução, terminologia e arquitetura.
* [Jornada de integração](/help/journey-onboarding/overview.md)- Este guia fornece um resumo de como começar a usar o Experience Manager as a Cloud Service, incluindo como obter acesso e configurar sua equipe.
