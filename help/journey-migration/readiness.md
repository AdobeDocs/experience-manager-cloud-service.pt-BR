---
title: Fase de preparação
description: Saiba mais sobre as etapas necessárias para garantir que sua instalação do AEM esteja pronta para ser movida para a nuvem
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 8%

---

# Fase de preparação {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planejamento da transição"
>abstract="Antes de iniciar sua jornada de transição para o Cloud Service, você deve se familiarizar com o AEM as a Cloud Service e rever as alterações notáveis que foram feitas nele, além de revisar os recursos que foram substituídos ou preteridos."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Analisador de práticas recomendadas"

Nesta fase da Jornada de Migração AEM as a Cloud Service, você se familiarizará com AEM as a Cloud Service, analisará as alterações notáveis que introduziu e compreenderá o que é necessário para planejar uma migração bem-sucedida para a nuvem.

## A história até agora {#story-so-far}

O documento anterior, [Introdução à migração para AEM as a Cloud Service](/help/journey-migration/getting-started.md), descreve uma lista de fases que precisam ser seguidas para migrar para AEM as a Cloud Service, bem como os benefícios de fazê-lo.

## Objetivo {#objective}

Este documento ajuda você a entender quais fatores devem ser considerados para garantir que sua instalação do AEM esteja pronta para ser movida para a nuvem:

* Saiba mais sobre alterações notáveis e recursos obsoletos
* Entenda como planejar a migração para AEM as a Cloud Service

## Revise as alterações importantes na arquitetura AEM as a Cloud Service {#notable-changes-in-aem-cloud-service-architecture}

O AEM as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar seus projetos do AEM.

Junto com essas melhorias, várias diferenças foram introduzidas entre as instalações locais do AEM e o Adobe Managed Services, em comparação a AEM as a Cloud Service.

A lista de itens na tabela abaixo é o subconjunto das alterações mais relevantes para uma migração para AEM as a Cloud Service. Você pode consultar a lista completa de alterações importantes [here](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>O que mudou?</th>
    <th>Referência</th>
    <th>Takeaways de chave</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separe os filtros mutáveis e imutáveis em pacotes correspondentes</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEM alterações importantes as a Cloud Service</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM Estrutura de Projeto para AEM as a Cloud Service</a></td>
    <td>Um único pacote que pode ser implantado em AEM as a Cloud Service pode ter subpacotes, principalmente para conter conteúdo mutável e imutável separado em seus próprios pacotes.</td>
  </tr>
  <tr>
    <td>Repo Init</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentação do Apache Sling RepoInit</a></td>
    <td>Os scripts de realocação são a prática recomendada para criar estruturas de nó iniciais, usuários, grupos ou usuários de serviços. Como esses scripts podem ser direcionados pelo modo de execução e gerenciáveis por meio da implantação do pacote de código, eles fornecem muita flexibilidade para realizar tarefas de inicialização do repositório.</td>
  </tr>
  <tr>
    <td>Não são permitidos modos de Execução Personalizados</td>
    <td></td>
    <td>Somente os modos de execução fornecidos prontos para uso com AEM as a Cloud Service são compatíveis.<br>Quando ambientes de desenvolvimento adicionais são adicionados, todos se vinculam ao modo de execução "dev".</td>
  </tr>
  <tr>
    <td>A execução de pipeline do Cloud Manager é a única maneira de implantar</td>
    <td></td>
    <td>Em AEM as a Cloud Service, o acesso ao /system/console não é permitido, portanto, todas as configurações do OSGi devem fazer parte do código e devem ser implantadas como código.<br>As configurações OSGi estão disponíveis no modo somente leitura para visualização no Console do desenvolvedor por meio do Cloud Manager</td>
  </tr>
  <tr>
    <td>Os agentes de replicação são substituídos pela Distribuição de conteúdo de sling</td>
    <td></td>
    <td>O conceito do agente de replicação é substituído por Sing Content Distribution. Se houver personalizações aproveitando agentes de replicação, elas deverão ser reprojetadas.<br>Não há suporte para replicação inversa</td>
  </tr>
  <tr>
    <td>CRX/DE e Gerenciador de pacotes</td>
    <td></td>
    <td>O CRX/DE é permitido somente no ambiente de desenvolvimento.<br>O Gerenciador de Pacotes está acessível em todas as instâncias do autor, mas os pacotes que serão implantados devem conter apenas conteúdo mutável ( por exemplo: /content ou /conf)</td>
  </tr>
  <tr>
    <td>Incorporado no CDN e Obtenha seu próprio CDN</td>
    <td></td>
    <td>AEM as a Cloud Service inclui a CDN para todos os ambientes, o que é otimizado para a maioria dos casos de uso.<br>Se quiser configurar seu próprio CDN, envie uma solicitação para o Adobe Support para que ele seja aprovado.<br>Se for aprovado, o CDN apontará para Fastly e não para AEM instâncias em nenhum ambiente.</td>
  </tr>
  <tr>
    <td>Trabalhos de longa execução</td>
    <td></td>
    <td>Evite executar trabalhos de longa execução, como agendadores do Sling ou trabalhos do Cron, pois as instâncias de AEM executadas nos contêineres podem vir e ir a qualquer momento.<br>Repense essas funcionalidades para descarregá-las no Adobe I/O.</td>
  </tr>
  <tr>
    <td>Alternar para operações assíncronas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">Configuração de operações assíncronas</a></td>
    <td>Para melhorar o desempenho geral de seus ambientes, determinadas operações são executadas no modo assíncrono. Os trabalhos assíncronos serão enfileirados e executados quando os recursos do sistema estiverem disponíveis.</td>
  </tr>
  <tr>
    <td>Estratégias de integração e autenticação baseadas em token</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">Gerar tokens de acesso para APIs do lado do servidor</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Tutorial de autenticação baseado em token</a></td>
    <td>É comum que sistemas externos ao AEM estejam tentando executar operações HTTP dentro do AEM.<br>A abordagem recomendada é implementar as estratégias descritas aqui, em vez de depender da criação de nomes de usuário locais com senhas no AEM.</td>
  </tr>
  <tr>
    <td>E/S de arquivo/Uso de disco</td>
    <td></td>
    <td>Como não há garantia de quanto espaço em disco é alocado e as instâncias em contêineres vêm e vão, não é aconselhável usar operações de E/S de arquivo para gravar ou ler do disco anexado à instância de AEM.</td>
  </tr>
  <tr>
    <td>Fluxo de trabalho do ativo de atualização DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Serviço Asset compute</a></td>
    <td>As etapas de processamento de mídia que fazem parte do fluxo de trabalho do Ativo de atualização do DAM agora são substituídas pelo Serviço do Asset compute</td>
  </tr>
  <tr>
    <td>Métodos de upload de ativos e etapas do processo de fluxo de trabalho compatíveis em AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">Fazer upload de comparações de API e etapas do processo WF suportadas</a></td>
    <td>Em AEM as a Cloud Service, durante o upload ou o download de um ativo, o ativo é transmitido diretamente para dentro ou para fora do armazenamento binário.</br>Nem todas as etapas do processo de fluxo de trabalho são compatíveis com o AEMaaCS.</td>
  </tr>
  <tr>
    <td>Inicializadores do fluxo de trabalho</td>
    <td></td>
    <td>Remova todos os Iniciadores de fluxo de trabalho que estão acionando o fluxo de trabalho de ativos de atualização do OOTB ou DAM personalizado de seu código.</br>Todos os ativos carregados AEM as a Cloud Service serão processados pelo Serviço de processamento de ativos. Para obter etapas personalizadas, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> Fluxos de trabalho de pós-processamento</a> sobre como configurar e configurar workflows de pós-processamento.</td>
  </tr>
  <tr>
    <td>Etapas da representação personalizada</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">Processando perfis</a></td>
    <td>Qualquer geração de representação personalizada, conversões de imagem ou codificações de vídeo devem ser descarregadas no Serviço de processamento de ativos criando perfis de processamento correspondentes.</td>
  </tr>
  <tr>
    <td>Pesquisa e indexação de conteúdo</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">Alterações na pesquisa e indexação de conteúdo</a></td>
    <td>Há mudanças consideráveis no processamento subjacente de índices e no momento em que ele começa.<br>Entenda e refatere completamente os índices do Oak antes de gerenciá-los no código que você implantará.</td>
  </tr>
  <tr>
    <td>Nem todas as tarefas de manutenção podem ser configuradas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEM tarefas de manutenção as a Cloud Service</a></td>
    <td>Você pode configurar apenas determinadas tarefas de manutenção com AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>Alterações no repositório de publicação</td>
    <td></td>
    <td>Alterações diretas no repositório de Publicação não são permitidas, exceto aquelas em /home. É sempre recomendável fazer as alterações no autor e distribuí-las. Todas as alterações de código e configuração devem ser implantadas por meio do pipeline do Cloud Manager correspondente.</td>
  </tr>
  <tr>
    <td>Configurações e armazenamento em cache do Dispatcher</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">Dispatcher na nuvem</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">Gerenciamento de cache<br></td>
    <td>As configurações do Dispatcher devem seguir uma estrutura específica.<br>As configurações devem ser gerenciadas como parte do código e implantadas por meio do pipeline do Cloud Manager .</td>
  </tr>
  <tr>
    <td>Backup e restauração</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEM backup e restauração as a Cloud Service</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Alterações na autenticação</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=pt-BR">Suporte IMS do AEM as a Cloud Service</td>
    <td>Se você estava usando anteriormente a integração do SAML 2.0 no autor e na publicação antes de migrar para o Cloud Service, a principal mudança é que AEM autor as a Cloud Service só se integra ao Adobe IMS. No entanto, AEM camada de publicação as a Cloud Service ainda pode aproveitar o SAML ou outras integrações de autenticação. O AEM as a Cloud Service oferece suporte à autenticação do IMS somente para os usuários Autor, Administrador e Desenvolvimento. A autenticação IMS não oferece suporte para usuários finais externos de sites do cliente como visitantes do site.</td>
  </tr>
</tbody>
</table>

## Recursos obsoletos {#deprecated-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

Recomendamos que você consulte o [Recursos obsoletos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) para se familiarizar com os recursos e funcionalidades marcados como obsoletos no Experience Manager as a Cloud Service e ver qual é o impacto da sua implantação de AEM.

## Plano de revisão da instalação AEM {#review-planning}

Depois de se acostumar com as alterações introduzidas com AEM as a Cloud Service, é hora de começar a planejar uma revisão da instalação existente, para medir o nível de alterações necessárias para movê-la para a nuvem.

A figura a seguir mostra as principais etapas envolvidas durante a fase de revisão:

![imagem](/help/journey-migration/assets/planning-phaseimg1.png)

Em seguida, exploraremos detalhadamente o significado de cada uma dessas etapas.

### Avaliação da prontidão do Cloud Service {#assess-cloud-readiness}

O primeiro passo é avaliar sua disponibilidade para migrar da versão AEM existente para o Cloud Service e determinar as áreas que exigirão refatoração para serem compatíveis com AEM as a Cloud Service.

Você precisará fazer uma avaliação abrangente do código-fonte AEM atual em relação às alterações notáveis e aos recursos obsoletos para determinar o nível de esforço esperado na jornada de transição.

O número de descobertas influenciará diretamente os prazos e o sucesso geral do projeto. Portanto, é recomendável descobrir o máximo possível para planejar o delivery ou iniciar as conversas necessárias para reprojetar qualquer personalização necessária para estar em conformidade com AEM prática recomendada as a Cloud Service.

**Analisador de práticas recomendadas**

Você pode acelerar a avaliação executando o Analisador de práticas recomendadas em relação à versão atual do AEM. Ter um bom entendimento de como funciona é fundamental para acelerar seu planejamento de avaliação.

Leia como funciona consultando o [Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) documentação.

**Criar um relatório de avaliação de disponibilidade da nuvem**

O passo seguinte é criar um relatório baseado em todos os conhecimentos adquiridos até agora. Você pode fazer isso gerando relatórios do Analisador de práticas recomendadas das instâncias de Preparo e Produção, [em seguida, faça o upload delas no Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) para um relatório digestível de itens acionáveis.

Um relatório típico deve conter essas entradas:

* Documentação que detalha o conjunto de recursos de sua instalação AEM específica
* Detalhes sobre as configurações e o código personalizados do AEM
* Configurações do Dispatcher de Produção
* Configurações de CDN (se houver)

**Socializar o relatório**

Depois que os relatórios do Analisador de práticas recomendadas forem concluídos, compartilhe-os com as equipes relevantes para confirmar suas conclusões e planejar suas próximas etapas. Dependendo da preferência, você também pode distribuir uma versão impressa do relatório usando [Visualização de impressão](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Revisão do planejamento de recursos {#review-resource-planning}

Depois de estimar o nível de esforço necessário para migrar para o Cloud Service, você deve identificar recursos, criar uma equipe e mapear funções e responsabilidades para o processo de transição.

### Estabelecimento de KPIs {#establish-kpis}

Se você não tiver estabelecido Indicadores-chave de desempenho (KPIs) anteriormente, é recomendável estabelecer KPIs para sua implementação de AEM para ajudar sua equipe a se concentrar naquilo que é mais importante.

Consulte [Desenvolvimento de KPIs](https://guided.adobe.com/welcome/aem/part6.html) para saber como escolher os KPIs certos para seus objetivos de negócios.

## O que vem a seguir {#what-is-next}

Assim que você entender o escopo das alterações necessárias para mudar para AEM as a Cloud Service, é hora de [Prepare seu código e a nuvem de conteúdo](/help/journey-migration/implementation.md) antes de realmente executar a migração.

## Recursos adicionais {#additional-resources}

* [Introdução ao Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Um guia abrangente sobre como usar o Cloud Acceleration Manager para acelerar sua migração para a nuvem
* [AEM as a Cloud Service: Introdução, arquitetura e pensamento de forma diferente](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM um Cloud Service Home](/help/overview/home.md) - Para obter uma visão geral da documentação do Experience Manager as a Cloud Service, comece aqui.
* [Visão geral as a Cloud Service do AEM](/help/overview/home.md) - Este guia fornece uma visão geral do Experience Manager as a Cloud Service, incluindo uma introdução, terminologia e arquitetura.
* [Jornada de integração](/help/journey-onboarding/overview.md)- Este guia fornece um resumo de como começar a usar o Experience Manager as a Cloud Service, incluindo como obter acesso e configurar sua equipe
