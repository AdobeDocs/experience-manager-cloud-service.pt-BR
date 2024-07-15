---
title: Publicação
description: Saiba como executar a migração depois que o código e o conteúdo estiverem prontos para nuvem
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 3%

---

# Publicação {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparo para a ativação"
>abstract="Para garantir uma ativação tranquila e bem-sucedida do AEM as a Cloud Service, você deve planejar períodos de congelamento de código e conteúdo, iterações de teste, atualizações de conteúdo, testes de desempenho, testes de segurança e muito mais."

Nesta parte da jornada, você aprenderá a planejar e executar a migração assim que o código e o conteúdo estiverem prontos para serem transferidos para o AEM as a Cloud Service. Além disso, você aprenderá quais são as práticas recomendadas e as limitações conhecidas ao executar a migração.

## A história até agora {#story-so-far}

Nas fases anteriores da jornada:

* Você aprendeu como começar a mover para o AEM as a Cloud Service na página [Introdução](/help/journey-migration/getting-started.md).
* Determinado se a sua implantação está pronta para ser movida para a nuvem lendo a [fase de Preparação](/help/journey-migration/readiness.md)
* Familiarizou-se com as ferramentas e o processo pelos quais você pode preparar seu código e sua nuvem de conteúdo com a [fase de Implementação](/help/journey-migration/implementation.md).

## Objetivo {#objective}

Este documento ajuda você a entender como executar a migração para o AEM as a Cloud Service depois de conhecer as etapas anteriores da jornada. Você aprenderá a executar a migração de produção inicial e as práticas recomendadas a serem seguidas ao migrar para o AEM as a Cloud Service.

## Migração de produção inicial {#initial-migration}

Antes de executar a migração de produção, siga as etapas de ajuste e prova de migração descritas na seção [Estratégia de migração de conteúdo e linha do tempo](/help/journey-migration/implementation.md##strategy-timeline) da [fase de Implementação](/help/journey-migration/implementation.md).

* Inicie a migração da produção com base na experiência adquirida durante a migração de estágio do AEM as a Cloud Service executada em clones:
   * Autor-Autor
   * Publish-Publish

* Valide o conteúdo assimilado nos níveis de criação e publicação do AEM as a Cloud Service.
* Instrua a equipe de criação de conteúdo a evitar mover o conteúdo na origem e no destino até que a assimilação seja concluída
* O novo conteúdo pode ser adicionado, editado ou excluído, mas evite movê-lo. Isso se aplica tanto à origem quanto ao destino.
* Registre o [tempo gasto](/help/journey-migration/implementation.md#gathering-data) para extração e assimilação completas para ter uma estimativa para futuras linhas do tempo de migração complementares.
* Crie um [planejador de migração](/help/journey-migration/implementation.md#migration-plan) para o autor e para publicação.

## Complementos incrementais {#top-up}

Após a migração inicial da produção, você deve realizar atualizações complementares incrementais para garantir que seu conteúdo seja atualizado na instância da nuvem. Por causa disso, recomenda-se seguir estas práticas recomendadas:

* Colete dados sobre a quantidade de conteúdo. Por exemplo: por uma semana, duas semanas ou um mês.
* Certifique-se de planejar as atualizações complementares de forma a evitar mais de 48 horas de extração e assimilação de conteúdo. Isso é recomendado para que as atualizações complementares de conteúdo se encaixem em um intervalo de tempo de fim de semana.
* Planeje o número de atualizações necessárias e use essas estimativas para planejar a data de ativação.

## Identificar os cronogramas de congelamento de código e conteúdo para a migração {#code-content-freeze}

Como mencionado anteriormente, será necessário agendar um código e um período de congelamento do conteúdo. Use as seguintes perguntas para ajudá-lo a planejar o período de congelamento:

* Por quanto tempo preciso congelar as atividades de criação de conteúdo?
* Por quanto tempo devo solicitar que minha equipe de entrega pare de adicionar novos recursos?

Para responder à primeira pergunta, considere o tempo necessário para executar execuções de avaliação em ambientes não relacionados à produção. Para responder à segunda pergunta, você precisa de uma colaboração estreita entre a equipe que está adicionando novos recursos e a equipe que está refatorando o código. O objetivo é garantir que todo o código adicionado à implantação existente também seja adicionado, testado e implantado na ramificação dos serviços em nuvem. Geralmente, significa que a quantidade de congelamento do código é menor.

Além disso, é necessário planejar um congelamento do conteúdo quando a atualização final do conteúdo for agendada.

## Práticas recomendadas {#best-practices}

Ao planejar ou executar a migração, você deve considerar as seguintes diretrizes:

* Migração de Autor para Autor e Publish para Publish
* Solicite um clone de produção que possa ser usado para:
   * Capturar estatísticas do repositório
   * Prova de atividades de migração
   * Preparar o plano de migração
   * Identificar requisitos de congelamento de conteúdo
   * Identificar quaisquer necessidades de upsizing na produção ao fazer a migração da produção

**Práticas recomendadas da ferramenta Transferência de conteúdo**

Ao entrar em funcionamento, certifique-se de executar a migração de conteúdo na produção em vez de em um clone. Uma boa abordagem é usar o [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para a migração inicial e executar extrações complementares com frequência (até mesmo diariamente) para extrair partes menores e evitar qualquer carga de longo prazo no AEM de origem.

Ao executar a migração de produção, você deve evitar a execução da ferramenta Transferência de conteúdo a partir de um clone, pois:

* Se um cliente solicitar que as versões de conteúdo sejam migradas durante as migrações complementares, a execução da ferramenta Transferência de conteúdo de um clone não migrará as versões. Mesmo que o clone seja recriado frequentemente a partir de um autor ativo, cada vez que um clone é criado, os pontos de verificação usados pela ferramenta Transferência de conteúdo para calcular os deltas são redefinidos.
* Como um clone não pode ser atualizado como um todo, o pacote de Consulta ACL deve ser usado para empacotar e instalar o conteúdo que está sendo adicionado ou editado de produção para clone. O problema dessa abordagem é que qualquer conteúdo excluído na instância de origem nunca chegará ao clone, a menos que seja excluído manualmente da origem e do clone. Isso introduz a possibilidade de que o conteúdo excluído na produção não será excluído no clone e no AEM as a Cloud Service.

**Otimizando a carga na origem de AEM ao executar a migração de conteúdo**

Lembre-se, a carga na fonte AEM é maior durante a fase de extração. Esteja ciente do seguinte:

* A Ferramenta de transferência de conteúdo é um processo Java externo que usa um Heap JVM de 4 GB
* A versão que não é do AzCopy baixa binários, armazena em um espaço temporário no autor AEM de origem, consumindo E/S de disco e faz upload no contêiner do Azure que consome largura de banda de rede
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) transfere blobs diretamente do armazenamento de blobs para o contêiner do Azure, o que salva a E/S de disco e a largura de banda da rede. A versão do AzCopy ainda usa o disco e a largura de banda da rede para extrair e carregar os dados do armazenamento de segmentos no container do Azure
* O processo da ferramenta Transferência de conteúdo é mais leve nos recursos do sistema durante a fase de assimilação, pois apenas transmite logs de assimilação e não há muita carga na instância de origem no que diz respeito à E/S de disco ou à largura de banda da rede.

## Limitações conhecidas {#known-limitations}

Leve em consideração que toda a assimilação falhará se qualquer uma das seguintes limitações for encontrada como parte do conjunto de migração extraído:

* Um Nó JCR que tem um nome com mais de 150 caracteres
* Um Nó JCR com mais de 16 MB
* Qualquer usuário/grupo com `rep:AuthorizableID` sendo assimilado que já esteja presente no AEM as a Cloud Service
* Se qualquer ativo extraído e assimilado for movido para um caminho diferente na origem ou no destino antes da próxima iteração da migração.

## Integridade do ativo {#asset-health}

Comparada à seção acima, a assimilação **não** falha devido às seguintes preocupações com o ativo. No entanto, é altamente recomendável que você siga as etapas apropriadas nestes cenários:

* Qualquer ativo que tenha a representação original ausente
* Qualquer pasta que tenha um nó `jcr:content` ausente.

Ambos os itens acima são identificados e relatados no relatório do [Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

## Lista de verificação de ativação {#Go-Live-Checklist}

Para obter mais informações, consulte a documentação da [Lista de verificação da ativação](/help/journey-onboarding/go-live-checklist.md).

## O que vem a seguir {#what-is-next}

Assim que você entender como executar a migração para o AEM as a Cloud Service, poderá verificar a página [Post-Go-Live](/help/journey-migration/post-go-live.md) para manter sua instância em perfeita execução.
