---
title: Fase de implementação
description: Verificar se o código e o conteúdo estão prontos para a migração para a nuvem
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 9%

---

# Fase de implementação {#implementation-phase}

Na fase de implementação da jornada, você explorará as ferramentas através das quais pode preparar seu código e conteúdo para serem transferidos para o AEM as a Cloud Service.

## A história até agora {#story-so-far}

Nas partes anteriores da jornada, você passou por [familiarizando-se com as alterações no AEM as a Cloud Service](/help/journey-migration/getting-started.md) e determinou se a implantação está pronta para ser movida para a nuvem na [fase de preparação](/help/journey-migration/readiness.md).

Este artigo continua com conselhos sobre como usar as ferramentas fornecidas pela Adobe para garantir que seu código e conteúdo estejam prontos para serem movidos para a nuvem.

## Objetivo {#objective}

Este documento tem como objetivo:

* Apresente você ao Cloud Manager, a integração contínua da AEM e a estrutura de entrega usada para implantar código no AEM as a Cloud Service
* Atualize-se com a ferramenta de transferência de conteúdo
* Descreva as ferramentas de refatoração de código que você precisa usar para modernizar seu código para o AEM as a Cloud Service

## Utilização do Cloud Manager {#using-cloud-manager}

Antes de começar, você deve se familiarizar com o Cloud Manager, pois ele é o único mecanismo para implantar código no AEM as a Cloud Service.

O Cloud Manager permite que as organizações gerenciem automaticamente o AEM na Nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança.

Você pode se familiarizar com o uso do Cloud Manager consultando os recursos abaixo:

* [Jornada de integração](/help/journey-onboarding/overview.md) para entender os recursos de autoajuda sobre integração do Experience Manager as a Cloud Service.

* [Integração do Git com o Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) para saber mais sobre o uso de um único repositório Git para implantar código.

* [Configuração do Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) para saber mais sobre como gerenciar produtos e o acesso dos usuários no Admin Console.

## Use as ferramentas fornecidas pelo Adobe para preparar seu conteúdo e código na nuvem {#use-tools-to-make-code-and-content-cloud-ready}

As etapas exatas da sua transição para o Cloud Service dependem dos sistemas que você adquiriu e das práticas de ciclo de vida de desenvolvimento de software seguidas.

A figura a seguir mostra as principais etapas envolvidas na fase que envolve a conversão de código e conteúdo para uso com o AEM as a Cloud Service:

![Etapas de conversão](/help/journey-migration/assets/exec-image1.png)

Começaremos a detalhar as ferramentas que você deve usar para fazer isso nos capítulos abaixo.

## Migração de conteúdo {#content-migration}

Para migrar o conteúdo da sua instância atual do AEM para a sua instância do Cloud Service, use a ferramenta Transferência de conteúdo do Adobe.

Com essa ferramenta, você pode especificar o subconjunto de conteúdo desejado que deseja transferir da instância de origem do AEM para a instância do AEM Cloud Service.

A migração de conteúdo é um processo de várias etapas que requer planejamento, rastreamento e colaboração entre equipes diferentes.

Para obter detalhes completos sobre como a ferramenta funciona e como a Adobe recomenda que você a use, consulte a [documentação da Ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refatoração de código {#code-refactor}

### Configurar para desenvolvimento {#set-up-for-development}

É hora de começar a refatorar os recursos existentes para serem compatíveis com os Serviços em nuvem.

Primeiro, observe a documentação que detalha as ferramentas básicas e comece a refatorar seu código:


* Durante o planejamento, é uma boa ideia ter uma lista de áreas que devem ser refatoradas para serem compatíveis com o AEM as a Cloud Service. Você pode revisar as [Diretrizes de desenvolvimento](/help/implementing/developing/introduction/development-guidelines.md) para obter mais detalhes sobre como refatorar e otimizar o código para o Cloud Service.
* Leia sobre como [Gerenciar configurações](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html#what-is-a-configuration) no AEM as a Cloud Service.
* Saiba como configurar um Ambiente de Desenvolvimento Local baixando o [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=pt-BR)
* Por fim, familiarize-se com a [API Java do AEM as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Além disso, também é possível:

* Assista a este vídeo para saber como instalar o Dispatcher SDK localmente:

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Assista a este vídeo para entender como configurar o Dispatcher SDK:

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Uma mudança de mentalidade {#a-change-in-mindset}

O desenvolvimento e a execução de código no AEM as a Cloud Service requer uma mudança de mentalidade. Vale lembrar que o código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento. O código em execução no Cloud Service deve reconhecer o fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução.

Certas alterações são necessárias para que os projetos do AEM Maven sejam compatíveis com a nuvem. O AEM as a Cloud Service requer uma separação de *conteúdo* e *código* em pacotes distintos para implantação no AEM:

* `/apps` e `/libs` são consideradas áreas imutáveis do AEM, pois não podem ser alteradas após o AEM ser iniciado (isto é, em tempo de execução). Isso inclui operações de criação, atualização ou exclusão. Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

* Todo o restante no repositório (por exemplo, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) são áreas mutáveis, o que significa que podem ser alteradas em tempo de execução.

Você pode saber mais consultando a documentação [Estrutura de pacote recomendada](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure).


### Ferramentas de migração na nuvem {#cloud-migration-tools}

O Adobe fornece várias ferramentas para ajudar a acelerar algumas de suas tarefas de refatoração de código. Compreender essas ferramentas e os problemas que elas resolvem reduzirá a complexidade da migração e o tempo.

* [Migração de fluxo de trabalho de ativos](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), uma ferramenta usada para migrar automaticamente fluxos de trabalho de processamento de ativos
* O [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), uma ferramenta que converte as configurações existentes do Dispatcher em um formato pronto para o AEM as a Cloud Service.
* [Modernizador de repositório](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html), uma ferramenta que usa um projeto AEM Multimode como entrada e o converte em um AEM as a Cloud Service
* [Conversor de Índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html), uma ferramenta que converte índices em um formulário compatível com o AEM as a Cloud Service
* [Ferramentas de Modernização](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), um conjunto de utilitários que podem ser usados para converter recursos herdados do AEM em recursos modernos e compatíveis do AEM as a Cloud Service.

Depois de configurar o ambiente de desenvolvimento local, familiarize-se com o AEM as a Cloud Service SDK consultando a [documentação](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Programar um congelamento do código {#schedule-a-code-freeze}

Para gerenciar o desenvolvimento contínuo do código no AEM ativo, juntamente com as tarefas de refatoração de código como parte da jornada de transição, a Adobe recomenda agendar um período de congelamento do código até você concluir a reestruturação do projeto Maven para que ele seja compatível com o AEM as a Cloud Service.

Quando a reestruturação do projeto estiver concluída, você poderá retomar o desenvolvimento de novos códigos com base nessa nova estrutura. Isso reduz as falhas de pipeline do Cloud Manager durante os testes e a implantação do código.

>[!NOTE]
>As tarefas de Transferência de conteúdo e Refatoração do código não precisam ser realizadas sequencialmente. Elas podem ser realizadas independentemente uma da outra. No entanto, é necessário ter a estrutura correta do projeto para garantir que o conteúdo seja renderizado com êxito no seu ambiente do Cloud Service.

## Práticas recomendadas para testes e implantação do código {#best-practices}

O pipeline do Cloud Manager oferece suporte à execução de testes que são executados no ambiente de preparo.

Siga as práticas recomendadas nos documentos abaixo relacionados ao teste de qualidade do código:

* [Teste de Qualidade do Código](/help/implementing/cloud-manager/code-quality-testing.md), um documento que descreve o processo de gravação de scripts de teste e explica o conceito de cobertura recomendada de pelo menos 50%.
* [Noções básicas das regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md), que visa descrever as regras de qualidade do código personalizado executadas pela Cloud Manager e criadas com base nas práticas recomendadas da engenharia do AEM.

## Preparação para ativação {#preparing-for-go-live}

A preparação do sistema de origem para migração envolve tarefas de nível de administrador do sistema e do AEM. Você pode começar verificando se o repositório de conteúdo está em um estado bem mantido verificando o status da tarefa [limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=pt-BR) e a [coleta de lixo de armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=pt-BR). Se você estiver executando a versão 6.3 do AEM (já que a ferramenta Transferência de conteúdo é compatível da versão 6.3 em diante), é recomendável executar a compactação offline, seguida da coleta de Lixo do Data Store.

[A verificação de consistência de dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) é recomendada em todas as versões do AEM para garantir que o repositório de conteúdo esteja em bom estado para iniciar as atividades de migração.

É necessário acesso em nível de administrador do sistema para instalar e configurar o [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

Também é recomendável revisar qualquer Assets, Páginas, Projetos AEM, Usuários e Grupos não utilizados para economizar tempo na migração. Consulte a seção [Integridade do Repositório de Conteúdo](#repository-health).

### Integridade do repositório de conteúdo {#repository-health}

Uma vez estabelecido o acesso a um [clone de produção](#proof-of-migration), prossiga para verificar a integridade do repositório. Como mencionado na seção anterior, o objetivo é limpar e compactar o repositório na origem antes de iniciar a migração. Essa etapa possivelmente economizará muito tempo, caso contrário, gastará na solução de problemas assim que a migração começar.

| Item de Ação | Principais aprendizados |
|---------|----------|
| Usuários, grupos e permissões | Você precisa entender o volume de usuários, grupos e a complexidade em torno das associações. Procure oportunidades para limpar usuários e grupos não utilizados na origem antes da migração. |
| Processamento de ativo incompleto | Tente concluir o processamento de ativos no sistema de origem antes de iniciar a migração para evitar possíveis preocupações no AEM as a Cloud Service após a migração. |
| Integridade do conteúdo | É recomendável consultar conteúdo incorreto e removê-lo antes de iniciar a migração. Por exemplo, procure ativos ou páginas que não têm representações originais ou que estão presas no processamento de fluxo de trabalho. Consulte também [Integridade do ativo](#asset-health). |

## Coletando dados {#gathering-data}

>[!NOTE]
> A seção [Estratégia e linha do tempo de migração de conteúdo](#content-strategy-and-timeline) detalha ainda mais como extrapolar os dados coletados e criar um plano de migração.

A coleta de dados pode ajudar você a planejar as atividades de migração e as tarefas associadas. Os tempos de extração e assimilação são especialmente úteis porque os pontos de dados podem ser associados a um tamanho específico do conjunto de migração. Dessa forma, esses pontos de dados podem ser extrapolados para criar um plano:

* Tempo total necessário para [extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Total de tempo gasto para [assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Tempo total necessário para a [extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) complementar
* Quantidade total de tempo gasto para a [assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) complementar


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

Esses pontos de dados também podem ajudar você a [Estabelecer KPIs](/help/journey-migration/readiness.md#establish-kpis) e outras tarefas relacionadas à migração.

### Plano de migração {#migration-plan}

Com base nos pontos de dados coletados (veja acima), é possível criar um plano de migração que possa ser integrado a um plano de projeto de macro. Esta etapa permitirá que todas as principais partes interessadas visualizem e planejem as atividades de migração.

A tabela a seguir ilustra um plano de migração típico:

| Iteração de migração | Data inicial | Data de Término Estimada | Dependências | Duração Estimada (em dias) | Detalhes adicionais / Itens de ação |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |   |   |   |   |   |

Como você pode ver na tabela acima, é útil seguir um formato de nomenclatura específico para identificar as iterações de migração, por exemplo: **PRDCLONE** para o ambiente AEM de origem, **AUTHOR/PUBLISH** para o ambiente AEM as a Cloud Service, **CSSTAGE-AUTHOR** para a instância do AEM as a Cloud Service e assim por diante.

Alguns detalhes importantes que influenciam seu plano de migração:

**O Número Total de Extrações necessárias**

* As extrações de Autor e Publicação em ambientes específicos são consideradas como duas extrações paralelas, pois são independentes umas das outras.
* Número de extrações complementares com base no crescimento do repositório em períodos específicos.

**Número total de assimilações necessárias**

* É importante capturar esse item no plano, pois um conjunto extraído pode ser assimilado em vários ambientes do Cloud Service.
* Número de assimilações complementares.
* A migração de conteúdo do autor do Source para a instância do autor do Cloud Service e do Source Publish para o Cloud Service Publish é a prática recomendada para evitar a assimilação de todo o conteúdo do autor no Cloud Service Publish.

### Rastreador de migração {#migration-tracker}

Você pode usar o rastreador de migração para anotar os horários das execuções iniciais e complementares. Esses pontos de dados ajudarão você a formular requisitos realistas de congelamento de conteúdo antes do acréscimo final.

O rastreador também ajudará você a:

* Identificar quaisquer desvios do planejador que requeiram ajustes no plano ou nos cronogramas de ativação
* Fornecer um status realista que possa ser usado em todas as comunicações necessárias
* Planejar migrações complementares iniciais ou futuras

A tabela a seguir ilustra um rastreador de migração funcional:

| Source (Ambiente / Instância / URL) | Destino (Ambiente / Instância / URL) | Nome, tipo (inicial ou complementar) do conjunto de migrações | Tamanho do Conjunto de Migração (MB) | Mapeamento de usuários (Sim/Não) | Duração da extração (início, fim, tempo gasto) | Duração da assimilação (início, fim, tempo gasto) | Problemas/Resoluções/Detalhes |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## Estratégia e cronograma de migração de conteúdo {#content-strategyand-timeline}

A seção a seguir mostra as etapas importantes e as tarefas associadas que podem ser usadas para formular uma estratégia de migração de conteúdo e uma linha do tempo.

![Etapas para formular uma estratégia de migração](/help/journey-migration/assets/content-migration2.png)

### Ajuste {#fitment}

* Execute a limpeza de revisão, a coleta de lixo do armazenamento de dados e as verificações de consistência de dados. Consulte também [Preparação para ativação](#preparing-for-go-live)
* [Colete estatísticas](#gathering-data) sobre o repositório de origem do AEM:
   * Tamanho do armazenamento de segmentos
   * Tamanho do armazenamento de índice
   * Número de páginas
   * Número de ativos
   * Número de usuários e grupos
* Saber se os seguintes recursos estão ativados na origem do AEM (também obrigatório no AEM as a Cloud Service):
   * Marcação inteligente
   * Pesquisa de semelhança
   * Pesquisar por conter texto em documentos word e pdf
* Coletar o [relatório](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) do Analisador de Práticas Recomendadas
* Importar para o [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Revise a recomendação de autoanálise para garantir que a AEM as a Cloud Service possa lidar com os requisitos de armazenamento.
* Crie um tíquete de Suporte da Adobe para qualquer esclarecimento antes de continuar com o plano de migração.

### Prova de migração {#proof-of-migration}

* Solicite um clone de produção que:
   * Está na mesma zona de rede
   * Fornecerá conteúdo de produção como usuários e grupos
   * Clona o autor e a publicação — um nó cada no caso de um cluster ou farm de publicação
* Escolha um subconjunto do conteúdo que é migrado para que:
   * É uma combinação de todos os tipos de conteúdo disponíveis
   * Contém todos os usuários e grupos
* Inclui 25% do conteúdo ou até 1 TB, o que for menor.
* Execute pelo menos uma migração completa e [complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process), do clone de produção para o ambiente de não produção do AEM as a Cloud Service
* Resolva possíveis problemas como:
   * Espaço em disco na origem do AEM
   * Conectividade entre a origem do AEM e o AEM as a Cloud Service
   * Quaisquer [limitações relacionadas à assimilação](go-live.md#known-limitations).
* Registre o tempo gasto para [extração e assimilação](#gathering-data):
   * Saber quanto conteúdo é adicionado por semana
   * Expanda os tempos medidos na prova de migração para criar um [plano de migração](#migration-plan).

## O que vem a seguir {#what-is-next}

Depois que você entender completamente como avaliar se a sua instalação do AEM está pronta para ser movida para a nuvem, à medida que aprendemos a usar as ferramentas necessárias para torná-la pronta, é hora de seguir para a [fase de ativação](/help/journey-migration/go-live.md).
