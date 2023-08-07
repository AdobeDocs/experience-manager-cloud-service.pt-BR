---
title: Atualizações de versão do AEM
description: Saiba como o AEM as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: dd567c484d71e25de1808f784c455cfb9b124fbf
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 11%

---


# Atualizações de versão do AEM {#aem-version-updates}

Saiba como o AEM as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.

## CI/CD {#ci-cd}

O AEM as a Cloud Service usa integração contínua e entrega contínua (CI/CD) para garantir que seus projetos estejam na versão AEM mais atual. Esse processo atualiza com facilidade suas instâncias de produção, preparo e desenvolvimento sem causar interrupções para os usuários.

Antes que suas instâncias sejam atualizadas automaticamente, uma nova versão de manutenção do AEM é publicada com 3 a 5 dias de antecedência. Durante esse período, é possível optar por
[acionar atualizações manuais para suas instâncias de desenvolvimento](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).
Depois que esse tempo transcorrer, as atualizações de versão serão aplicadas automaticamente aos ambientes de desenvolvimento primeiro. Se a atualização for bem-sucedida, o processo de atualização continuará nas instâncias de estágio e produção. As instâncias de desenvolvimento e preparo atuam como um quality gate (portal de qualidade) automatizado, em que seus testes personalizados são executados antes que a atualização seja aplicada em seu ambiente de produção.

>[!NOTE]
>
> Observação: as atualizações automáticas para ambientes de desenvolvimento serão progressivamente habilitadas em 2023 para todos os clientes. Se seus ambientes de desenvolvimento não forem atualizados automaticamente, você poderá usar atualizações manuais para mantê-los sincronizados com seus ambientes de preparo e produção.


## Tipo de atualizações {#update-types}

Há dois tipos de atualizações de versão do AEM:

* **Atualizações de manutenção do AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Têm um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * São lançados em um [cronograma mensal previsível.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR)

## Falha ao atualizar {#update-failure}

As atualizações do AEM passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que não haja interrupção do serviço para nenhum sistema em produção.
As verificações de integridade são usadas para monitorar a integridade do aplicativo.
Se essas verificações falharem durante uma atualização as a Cloud Service do AEM, a liberação não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

Ao implantar uma nova versão de um código personalizado de em seus ambientes,
[Testes funcionais de produto e personalizados](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)
desempenhar um papel crucial para assegurar que os sistemas de produção se mantêm estáveis e funcionais mesmo após a aplicação de uma alteração. Esses testes também são aproveitados no processo de atualização da versão do AEM.

Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.
Da mesma forma, se uma atualização automatizada de um ambiente de desenvolvimento falhar, os ambientes de preparo e produção não serão atualizados.

>[!NOTE]
>
>Se o código personalizado foi enviado para preparo e não para produção, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção. Portanto, o código personalizado que estava disponível somente no preparo terá que ser implantado novamente.

## Armazenamento de nó composto {#composite-node-store}

Na maioria dos casos, as atualizações não terão tempo de inatividade, inclusive para a instância de criação, que é um cluster de nós. As atualizações contínuas são possíveis devido a [o recurso de armazenamento de nós compostos no Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em um [implantação contínua,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) a nova versão do AEM contém sua própria `/libs` (o repositório imutável baseado em TarMK), distinto da versão mais antiga do AEM, embora ambos façam referência a um repositório mutável compartilhado baseado em DocumentMK que contém áreas como `/content` , `/conf` , `/etc` e outros.

Como a versão antiga e a nova têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua e ambos podem assumir o tráfego até que o antigo seja totalmente substituído pelo novo.
