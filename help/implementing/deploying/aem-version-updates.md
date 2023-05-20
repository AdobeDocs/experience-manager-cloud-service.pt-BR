---
title: Atualizações de versão do AEM
description: Saiba como o AEM as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 7cdc7bb56565cccc04a2dcb74a6c8088ed4e7847
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# Atualizações de versão do AEM {#aem-version-updates}

Saiba como o AEM as a Cloud Service usa integração e entrega contínuas (CI/CD) para manter seus projetos na versão mais recente.

## CI/CD {#ci-cd}

O AEM as a Cloud Service usa integração contínua e entrega contínua (CI/CD) para garantir que seus projetos estejam na versão AEM mais atual. Isso significa que as instâncias de produção e preparação são atualizadas para a versão mais recente do AEM sem a interrupção do serviço dos usuários.

As atualizações de versão são aplicadas automaticamente somente a instâncias de produção e de preparo. [As atualizações do AEM devem ser aplicadas manualmente a todas as outras instâncias.](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## Tipo de atualizações {#update-types}

Há dois tipos de atualizações de versão do AEM:

* **Atualizações de manutenção do AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Têm um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * São lançados em um [cronograma mensal previsível.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR)

## Falha ao atualizar {#update-failure}

As atualizações do AEM passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que não haja interrupção do serviço para nenhum sistema em produção. As verificações de integridade são usadas para monitorar a integridade do aplicativo. Se essas verificações falharem durante uma atualização as a Cloud Service do AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Testes do produto e testes funcionais do cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) que impedem que atualizações de produtos e envios por push de código do cliente interrompam os sistemas de produção, também são validados durante uma atualização de versão do AEM.

Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para preparo e não para produção, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção. Portanto, o código personalizado que estava disponível somente no preparo terá que ser implantado novamente.

## Armazenamento de nó composto {#composite-node-store}

As atualizações na maioria dos casos não terão tempo de inatividade, inclusive para a instância de criação, que é um cluster de nós. As atualizações contínuas são possíveis devido a [o recurso de armazenamento de nós compostos no Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em um intervalo [implantação azul-verde,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) a nova versão verde do AEM contém sua própria `/libs` (o repositório imutável baseado em TarMK), distinto da versão mais antiga do AEM azul, embora ambos façam referência a um repositório mutável compartilhado baseado em DocumentMK que contém áreas como `/content` , `/conf` , `/etc` e outros.

Porque tanto o azul quanto o verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos assumindo o tráfego até que o azul seja totalmente substituído pelo verde.
