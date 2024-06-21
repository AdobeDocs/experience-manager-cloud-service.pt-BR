---
title: Atualizações de versão do AEM
description: Saiba como o Adobe Experience Manager (AEM) as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Atualizações de versão do AEM {#aem-version-updates}

Saiba como o Adobe Experience Manager (AEM) as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.

## CI/CD {#ci-cd}

O AEM as a Cloud Service usa integração contínua e entrega contínua (CI/CD) para garantir que seus projetos estejam na versão AEM mais atual. Esse processo atualiza com facilidade suas instâncias de produção, preparo e desenvolvimento sem causar interrupções para os usuários.

>[!NOTE]
> Como as instâncias de desenvolvimento já são atualizadas automaticamente, as atualizações manuais das instâncias de desenvolvimento podem não estar disponíveis para _alguns_ de seus programas. Este recurso está sendo transferido para atualizações automáticas.

Antes que suas instâncias sejam atualizadas automaticamente, uma nova versão de manutenção do AEM é publicada com 3 a 5 dias de antecedência. Durante esse período, sua instância de desenvolvimento pode ser atualizada automaticamente ou, caso esteja disponível, você pode optar por [acionar a atualização das instâncias de desenvolvimento](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). As atualizações de versão são aplicadas automaticamente primeiro aos ambientes de desenvolvimento. Se a atualização for bem-sucedida, o processo de atualização continuará nas instâncias de estágio e produção. As instâncias de desenvolvimento e de preparo atuam como um quality gate (portal de qualidade) automatizado, em que os testes personalizados são executados antes que a atualização seja aplicada no ambiente de produção.

### NIMU (Atualizações de manutenção não invasivas) {#nimu}

As Atualizações de manutenção não invasivas são atualizações automáticas aplicadas sem envolver os pipelines do cliente.
Por meio do NIMU, o cliente pode usar o pipeline a qualquer momento, mesmo se uma atualização de versão de AEM estiver programada ou em andamento e as atualizações de manutenção não aparecerão mais no histórico de execução do pipeline do cliente, facilitando o acompanhamento do histórico de implantações de código.

#### Atualizar atividades

A versão atual do AEM ainda pode ser verificada para cada ambiente, como antes, usando o painel Ambientes de interface do usuário do Cloud Manager. Os mesmos quality gates (portais de qualidade) usados no pipeline são usados pelas atualizações de manutenção não invasivas, incluindo os testes escritos pelo cliente.
Uma notificação da interface do usuário do Cloud Manager será enviada sempre que uma Atualização de manutenção não invasiva for aplicada aos ambientes do seu programa. Você pode configurá-lo para que também seja enviado ao seu email.

>[!NOTE]
>
> Observação: as atualizações de manutenção não invasivas serão progressivamente habilitadas para todos os clientes em 2024.


## Tipo de atualizações {#update-types}

Há dois tipos de atualizações de versão do AEM:

* [**Atualizações de manutenção do AEM**](/help/release-notes/maintenance/latest.md)

   * Eles são usados principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * O impacto é mínimo, pois as alterações são aplicadas regularmente.

* [**Ativação do recurso AEM**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * Elas são lançadas em um cronograma mensal previsível.

>[!NOTE]
>
> Verifique as datas principais dos lançamentos mensais na [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR#aem-as-cloud-service) e marque em seu calendário para se preparar para as atividades principais e assim estar pronto para o lançamento.

## Falha ao atualizar {#update-failure}

As atualizações do AEM passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que não haja interrupção do serviço para nenhum sistema em produção. As verificações de integridade são usadas para monitorar a integridade do aplicativo. Se essas verificações falharem durante uma atualização as a Cloud Service do AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

Ao implantar uma nova versão de código personalizado em seu ambiente, [Testes funcionais de produto e personalizados](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) desempenhar um papel crucial. Eles garantem que os sistemas de produção permaneçam estáveis e funcionais mesmo após uma alteração ser aplicada. Esses testes também são aplicados no processo de atualização da versão do AEM.

Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.
Da mesma forma, se uma atualização automatizada de um ambiente de desenvolvimento falhar, os ambientes de preparo e produção não serão atualizados.

>[!NOTE]
>
>Se o código personalizado foi enviado para preparo e não para produção, a próxima atualização do AEM remove essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção. Portanto, o código personalizado que estava disponível somente no preparo deve ser implantado novamente.

## Práticas recomendadas {#best-practices}

* **Uso do ambiente de preparo**
   * Use um ambiente diferente (não Preparo) para ciclos longos de QA/UAT.
   * Após a conclusão do teste de sanidade no preparo, mova para verificar na produção.

* **Pipeline de produção**
   * Pause antes de implantar na produção.
   * Cancelar o pipeline após uma implantação de preparo indica que o código é &quot;um descartável&quot; e não um candidato válido para Produção, consulte [Configuração de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **Pipeline de não produção**
   * Configurar um [Pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * Acelerar a velocidade/frequência de entrega para falhas de pipeline de produção. Identifique problemas em pipelines de não produção ativando o Teste funcional do produto, o Teste funcional personalizado e o Teste de interface do usuário personalizada.

* **Cópia de conteúdo**
   * Uso [Cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) para mover conjuntos de conteúdo semelhantes para um ambiente de não produção.

* **Teste funcional automatizado**
   * Inclua testes automatizados em seu pipeline para que você possa testar a funcionalidade crítica.
   * [Teste funcional do cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) e [Testes de interface do usuário personalizados](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) estão bloqueando, se falharem, a liberação do AEM não é distribuída.

## Regressão {#regression}

Se você encontrar um problema relacionado à regressão, envie um caso de suporte por meio do Admin Console. Se o problema for um bloqueador e estiver afetando a Produção, um P1 deverá ser gerado. Forneça todos os detalhes necessários para reproduzir o problema de regressão.

## Armazenamento de nó composto {#composite-node-store}

Geralmente, as atualizações incorrem em tempo de inatividade zero, inclusive para a instância de criação, que é um cluster de nós. As atualizações contínuas são possíveis devido a [o recurso de armazenamento de nós compostos no Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em um [implantação contínua](/help/implementing/deploying/overview.md#how-rolling-deployments-work), a nova versão do AEM contém sua própria `/libs` (o repositório imutável baseado em TarMK). É diferente da versão mais antiga do AEM, embora ambos façam referência a um repositório mutável compartilhado baseado em DocumentMK que contém áreas como `/content` , `/conf` , `/etc` e outros.

Como a versão antiga e a nova têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua. E ambos podem assumir o tráfego até que o antigo seja totalmente substituído pelo novo.
