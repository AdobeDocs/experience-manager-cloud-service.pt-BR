---
title: Fase de implementação
description: Certifique-se de que seu código e conteúdo estejam prontos para a migração para a nuvem
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2416'
ht-degree: 9%

---

# Fase de implementação {#implementation-phase}

Na fase de implementação da jornada, você explorará as ferramentas através das quais você pode preparar o código e o conteúdo para serem transferidos para AEM as a Cloud Service.

## A história até agora {#story-so-far}

Nas partes anteriores da jornada, você passou [familiarizar-se com as mudanças no AEM as a Cloud Service](/help/journey-migration/getting-started.md), bem como determinar se sua implantação está pronta para ser movida para a nuvem com o [fase de preparação](/help/journey-migration/readiness.md).

Este artigo continua com recomendações sobre como usar as ferramentas fornecidas pelo Adobe para garantir que seu código e conteúdo estejam prontos para serem movidos para a nuvem.

## Objetivo {#objective}

O presente documento tem por objetivo:

* Apresente você ao Cloud Manager, AEM integração contínua e estrutura de entrega usada para implantar código AEM as a Cloud Service
* Atualize-o com a ferramenta de transferência de conteúdo
* Descreva as ferramentas de refatoração de código que você precisa usar para modernizar o código para AEM as a Cloud Service

## Uso do Cloud Manager {#using-cloud-manager}

Antes de começar, você deve se familiarizar com o Cloud Manager, pois ele é o único mecanismo para implantar código AEM as a Cloud Service.

O Cloud Manager permite que as organizações gerenciem automaticamente o AEM na Nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança.

Familiarize-se com o uso do Cloud Manager, consultando os recursos abaixo:

* [Jornada de integração](/help/journey-onboarding/overview.md) para entender os recursos de autoajuda sobre integração com o Experience Manager as a Cloud Service.

* [Integração do Git com o Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) para saber mais sobre o uso de um único repositório Git para implantar código.

* [Configuração do Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) para saber mais sobre como gerenciar produtos e o acesso dos usuários no Admin Console.

## Use as ferramentas fornecidas pelo Adobe para preparar o conteúdo e o código para a nuvem {#use-tools-to-make-code-and-content-cloud-ready}

As etapas exatas da sua transição para o Cloud Service dependem dos sistemas adquiridos e das práticas de ciclo de vida de desenvolvimento de software seguidas.

A figura a seguir mostra as principais etapas envolvidas na fase que envolve a conversão do código e do conteúdo para uso com AEM as a Cloud Service:

![imagem](/help/journey-migration/assets/exec-image1.png)

Começaremos a detalhar as ferramentas que você precisa usar para conseguir isso nos capítulos abaixo.

## Migração de conteúdo {#content-migration}

Para migrar o conteúdo da instância de AEM atual para a instância de Cloud Service, você pode usar a ferramenta Transferência de conteúdo do Adobe.

Com essa ferramenta, você pode especificar o subconjunto de conteúdo desejado que deseja transferir da instância de origem do AEM para a instância do AEM Cloud Service.

A Migração de conteúdo é um processo em várias etapas que requer planejamento, rastreamento e colaboração entre diferentes equipes.

Para obter um detalhe completo sobre como a ferramenta funciona e como recomendamos que você a use, consulte o [Documentação da ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refatoração do código {#code-refactor}

### Configurar para desenvolvimento {#set-up-for-development}

É hora de começar a refatorar os recursos existentes para serem compatíveis com o Cloud Services.

Para fazer isso, você precisa consultar a documentação detalhando as ferramentas básicas necessárias para iniciar a refatoração do código:


* Durante o planejamento, é boa ideia ter uma lista de áreas que precisam ser refatoradas para serem compatíveis com AEM as a Cloud Service. Você pode revisar [Diretrizes de desenvolvimento](/help/implementing/developing/introduction/development-guidelines.md) para obter mais detalhes sobre como refatorar e otimizar o código para o Cloud Service.
* Leia sobre como [Gerenciar configurações](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) em AEM as a Cloud Service.
* Saiba como configurar um Ambiente de desenvolvimento local baixando o [AEM SDK as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* Por fim, familiarize-se com o [AEM API Java as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Além disso, também é possível:

* Assista a este vídeo para entender como instalar o SDK do Dispatcher localmente:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Assista a este vídeo para entender como configurar o SDK do Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Uma alteração no conjunto de indicadores {#a-change-in-mindset}

O desenvolvimento e a execução de código AEM as a Cloud Service requer uma mudança de mentalidade. Vale lembrar que o código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento. O código em execução no Cloud Service deve reconhecer o fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução.

Determinadas alterações são necessárias para que AEM projetos Maven sejam compatíveis com a nuvem. AEM as a Cloud Service exige a separação de *conteúdo* e *código* em pacotes distintos para implantação no AEM:

* `/apps` e `/libs` são consideradas áreas imutáveis de AEM, pois não podem ser alteradas após AEM início (ou seja, no tempo de execução). Isso inclui operações de criação, atualização ou exclusão. Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

* Todo o restante no repositório (por exemplo, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) são áreas mutáveis, o que significa que podem ser alteradas em tempo de execução.

Você pode obter mais informações consultando o [Estrutura de pacote recomendada](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) documentação.


### Ferramentas de migração na nuvem {#cloud-migration-tools}

O Adobe fornece várias ferramentas para ajudar a acelerar algumas de suas tarefas de refatoração de código. Compreender essas ferramentas e os problemas que elas resolverem reduzirá a complexidade e o tempo da migração.

* [Migração de fluxo de trabalho de ativos](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), uma ferramenta usada para migrar automaticamente os fluxos de trabalho de processamento de ativos
* [Conversor do Dispatcher](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), uma ferramenta que converte as configurações existentes do Dispatcher em um formato pronto para AEM as a Cloud Service.
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en), uma ferramenta que utiliza um projeto Multimode AEM como entrada e o converte em um AEM as a Cloud Service
* [Conversor de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en), uma ferramenta que converte índices em um formulário compatível com AEM as a Cloud Service
* [Ferramentas de Modernização](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), um conjunto de utilitários que pode ser usado para converter recursos AEM herdados em recursos modernos e compatíveis AEM as a Cloud Service.

Depois de configurar o ambiente de desenvolvimento local, familiarize-se com o SDK as a Cloud Service AEM consultando o [documentação](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Programar um congelamento de código {#schedule-a-code-freeze}

Para gerenciar o desenvolvimento contínuo do código no AEM ativo, juntamente com as tarefas de refatoração de código como parte da jornada de transição, recomendamos que você programe um período de congelamento do código até concluir a reestruturação do projeto Maven para ser compatível com AEM as a Cloud Service.

Quando a reestruturação do projeto estiver concluída, você poderá retomar o desenvolvimento de novo código com base nessa nova estrutura. Isso reduz as falhas de pipeline do Cloud Manager durante a implantação e os testes do código.

>[!NOTE]
>As tarefas Transferência de conteúdo e Refatoração do código não precisam ser realizadas sequencialmente. Elas podem ser realizadas independentemente uma da outra. No entanto, é necessário ter a estrutura correta do projeto para garantir que o conteúdo seja renderizado com êxito no seu ambiente do Cloud Service.

## Práticas recomendadas para testes e implantação do código {#best-practices}

O pipeline do Cloud Manager oferece suporte à execução de testes que são executados no ambiente de preparo.

Siga as práticas recomendadas dos documentos abaixo com relação ao teste de qualidade do código:

* [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md), um documento que descreve o processo de escrita de scripts de teste e explica o conceito de cobertura recomendada de pelo menos 50%.
* [Noções básicas sobre regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) que tem como objetivo descrever as regras de qualidade de código personalizadas executadas pelo Cloud Manager e criadas com base nas práticas recomendadas da AEM Engineering.

## Preparando para ativação {#preparing-for-go-live}

A preparação do sistema de origem para migração envolve tarefas de nível de sistema e administrador AEM. Você pode começar verificando se o repositório de conteúdo está em um estado bem mantido, verificando o [limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e [coleta de lixo do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) status da tarefa. Se você estiver executando AEM versão 6.3 (já que a ferramenta Transferência de conteúdo é compatível a partir da versão 6.3), é recomendável executar a compactação offline, seguida pela coleta de lixo do Data Store.

[Verificação da consistência dos dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) é recomendado em todas as versões AEM para garantir que o repositório de conteúdo esteja em bom estado para iniciar atividades de migração.

O acesso de nível de administrador do sistema é necessário para instalar e configurar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

Também é recomendável revisar quaisquer Ativos, Páginas, Projetos AEM, Usuários e Grupos não utilizados para economizar tempo na migração. Consulte a [Integridade do repositório de conteúdo](#repository-health) seção.

### Integridade do repositório de conteúdo {#repository-health}

Ao acessar uma [clone de produção](#proof-of-migration) for estabelecido, continue a verificar a integridade do repositório. Como mencionado na seção anterior, o objetivo é limpar e compactar o repositório na origem antes de iniciar a migração. Essa etapa poderá economizar muito tempo, caso contrário, gastará na solução de problemas assim que a migração começar.

| Item de ação | Takeaways de chave |
|---------|----------|
| Usuários, grupos e permissões | Você precisa entender o volume de usuários, grupos e a complexidade em torno das associações. Procure oportunidades para limpar usuários e grupos não utilizados na origem antes da migração. |
| Processamento incompleto de ativos | Tente concluir o processamento de ativos no sistema de origem antes de iniciar a migração para evitar possíveis problemas AEM pós migração as a Cloud Service. |
| Integridade do conteúdo | É recomendável consultar se há conteúdo incorreto e limpá-lo antes de iniciar a migração. Por exemplo, procure por ativos ou páginas que não têm representações originais ou que estão travadas no processamento do fluxo de trabalho. Consulte também [Integridade do ativo](#asset-health). |

## Coletando dados {#gathering-data}

>[!NOTE]
> O [Estratégia e cronograma da migração de conteúdo](#content-strategy-and-timeline) seção mais detalhes sobre como extrapolar os dados coletados e criar um plano de migração.

A coleta de dados pode ajudar você a planejar as atividades de migração e tarefas associadas. Os tempos de extração e ingestão são particularmente úteis porque os pontos de dados podem ser associados a um tamanho específico do conjunto de migração. Assim, esses pontos de dados podem ser extrapolados para se elaborar um plano:

* Tempo total necessário [extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Tempo total necessário [ingestão](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Tempo total necessário para o reforço [extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Tempo total necessário para o reforço [ingestão](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

Um ponto de dados mais importante é a quantidade de tempo necessária para concluir a [mapeamento de usuário](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), se isso estiver combinado com a migração do conteúdo. Você pode considerar esse ponto de dados para estimativas mais realistas, pois ele será adicionado à linha do tempo geral de extração e pode não ser necessário executá-lo durante as atualizações complementares.

Esses pontos de dados também podem ajudar você [Estabeleça KPIs](/help/journey-migration/readiness.md#establish-kpis) e outras tarefas relacionadas com a migração.

### Plano de migração {#migration-plan}

Com base nos pontos de dados coletados (veja acima), você pode criar um plano de migração que pode ser integrado a um plano de projeto de macro. Esta etapa permitirá que todos os principais participantes visualizem e planejem as atividades de migração.

A tabela a seguir ilustra um plano de migração típico:

| Iteração da migração | Data inicial | Data final estimada | Dependências | Duração estimada (em dias) | Detalhes adicionais / Itens de ação |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

Como você pode ver na tabela acima, é útil seguir um formato de nomenclatura específico para identificar as iterações de migração, por exemplo: **PRDCLONE** para o ambiente AEM de origem , **AUTOR/PUBLICAÇÃO** para o ambiente AEM as a Cloud Service, **AUTOR DO CSSTAGE** para a instância AEM as a Cloud Service e assim por diante.

Alguns detalhes importantes que influenciam seu plano de migração:

**O número total de extrações necessárias**

* As extrações Autor e Publicação em ambientes específicos são consideradas duas extrações paralelas, pois são independentes umas das outras.
* Número de extrações principais com base no crescimento do repositório em períodos específicos.

**Número total de sugestões necessárias**

* É importante capturar esse item no plano, pois um conjunto extraído pode ser assimilado em vários ambientes de Cloud Service.
* Número de ingestões de Topo.
* Migrar o conteúdo do Autor de origem para a instância do Autor do serviço de nuvem e da Publicação de origem para publicação do Cloud Service é a prática recomendada para evitar assimilar todo o conteúdo do Autor na publicação do Cloud Service.

### Rastreador de migração {#migration-tracker}

Você pode usar o rastreador de migração para anotar os tempos das execuções inicial e superior. Esses pontos de dados ajudarão você a formular requisitos realistas de congelamento de conteúdo antes do complemento final.

O rastreador também ajudará você a:

* Identificar quaisquer desvios em relação ao planejador que necessitem de ajustes no plano ou nas linhas do tempo de ativação
* Fornecer um status realista que possa ser usado em todas as comunicações necessárias
* Plano de migração inicial ou futura do complemento

A tabela a seguir ilustra um rastreador de migração funcional:

| Fonte (Ambiente / Instância / URL) | Destino (Ambiente / Instância / URL) | Nome, tipo do conjunto de migração (inicial ou superior) | Tamanho do Conjunto de Migração (MB) | Mapeamento de usuários (Sim / Não) | Duração da extração (Início, Término, Tempo gasto) | Duração da assimilação (início, fim, tempo gasto) | Problemas/resoluções/detalhes |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## Estratégia e cronograma da migração de conteúdo {#content-strategyand-timeline}

A seção a seguir mostra as etapas importantes e as tarefas associadas que podem ser usadas para formular uma estratégia de migração de conteúdo e uma linha do tempo.

![imagem](/help/journey-migration/assets/content-migration2.png)

### Compromisso {#fitment}

* Execute limpeza de revisão, coleta de lixo do armazenamento de dados e verificações de consistência de dados. Consulte também [Preparando para ativação](#preparing-for-go-live)
* [Coletar estatísticas](#gathering-data) sobre o repositório de origem AEM:
   * Tamanho do armazenamento do segmento
   * Tamanho da loja de índice
   * Número de páginas
   * Número de ativos
   * Número de usuários e grupos
* Saiba se os seguintes recursos estão ativados na fonte de AEM (também necessários em AEM as a Cloud Service):
   * Marcação inteligente
   * Pesquisa de semelhança
   * Pesquisar por conter texto em documentos do word e pdf
* Colete o Analisador de práticas recomendadas [relatório](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importe para o [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Revise a recomendação de autoanálise para garantir que AEM as a Cloud Service possa lidar com os requisitos de armazenamento.
* Crie um tíquete de suporte ao Adobe para obter quaisquer esclarecimentos antes de continuar com o plano de migração.

### Prova de migração {#proof-of-migration}

* Solicite um clone de produção que:
   * Está na mesma zona de rede
   * Fornecerá conteúdo de produção como usuários e grupos
   * Clona criar e publicar - um nó cada no caso de um cluster ou farm de publicação
* Escolha um subconjunto do conteúdo que será migrado para que:
   * É uma combinação de todos os tipos de conteúdo disponíveis
   * Contém todos os usuários e grupos no caso [mapeamento de usuário](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) é obrigatório
* Inclui 25% do conteúdo ou até 1 TB de conteúdo, o que for menor.
* Executar pelo menos um completo e [top-up](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) migração, do clone de produção para o ambiente de não produção AEM as a Cloud Service
* Resolva possíveis problemas como:
   * Espaço em disco na origem AEM
   * Conectividade entre a fonte de AEM e a AEM as a Cloud Service
   * Qualquer [limitações relacionadas à ingestão](go-live.md#known-limitations).
* Registrar o tempo necessário para [extração e ingestão](#gathering-data):
   * Saiba quanto conteúdo é adicionado por semana
   * Extrapolar os tempos medidos a partir da prova de migração para criar um [plano de migração](#migration-plan).

## O que vem a seguir {#what-is-next}

Assim que você tiver compreendido completamente como avaliar se sua instalação do AEM está pronta para ser movida para a nuvem, já que nós, enquanto aprendemos a usar as ferramentas necessárias para prepará-la, é hora de ir para a [fase de ativação](/help/journey-migration/go-live.md).
