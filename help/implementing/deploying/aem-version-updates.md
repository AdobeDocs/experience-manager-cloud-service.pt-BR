---
title: Atualizações de versão do AEM
description: Saiba como o AEM as a Cloud Service usa a integração e o delivery contínuos (CI/CD) para manter seus projetos na versão mais recente.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 58ad2e4dec1c55426846f16918b3de13846ac03d
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# Atualizações de versão do AEM {#aem-version-updates}

Saiba como o AEM as a Cloud Service usa a integração e o delivery contínuos (CI/CD) para manter seus projetos na versão mais recente.

## CI/CD {#ci-cd}

AEM as a Cloud Service usa integração contínua e entrega contínua (CI/CD) para garantir que seus projetos estejam na versão de AEM mais recente. Isso significa que as instâncias de produção e preparação são atualizadas para a versão mais recente do AEM sem a interrupção do serviço dos usuários.

As atualizações de versão são aplicadas automaticamente somente às instâncias de produção e de preparo. [AEM atualizações devem ser aplicadas manualmente a todas as outras instâncias.](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## Tipo de atualizações {#update-types}

Há dois tipos de atualizações de versão do AEM:

* **Atualizações de manutenção do AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Têm um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * São liberados em um [programação mensal previsível.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR)

## Falha de atualização {#update-failure}

AEM atualizações passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que o serviço não seja interrompido em nenhum sistema em produção. Os controlos sanitários são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante uma atualização as a Cloud Service AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Testes do produto e testes funcionais do cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) que impedem que atualizações de produtos e códigos de clientes quebrem sistemas de produção, também são validados durante uma atualização de versão AEM.

Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para o armazenamento temporário e não para a produção, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção. Portanto, o código personalizado que estava disponível somente no armazenamento temporário terá que ser implantado novamente.

## Loja de nós composta {#composite-node-store}

As atualizações na maioria dos casos terão zero tempo de inatividade, incluindo para a instância de criação, que é um cluster de nós. As atualizações em andamento são possíveis devido a [o recurso de armazenamento do nó composto no Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em um rolamento [implantação azul-verde,](/help/operations/indexing.md#what-is-blue-green-deployment) a nova versão AEM verde contém a sua própria `/libs` (o repositório imutável baseado em TarMK), distinto da versão azul mais antiga do AEM, embora ambos referenciem um repositório mutável baseado em DocumentMK compartilhado que contém áreas como `/content` , `/conf` , `/etc` e outros.

Porque tanto o azul quanto o verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos gerando tráfego até que o azul seja totalmente substituído pelo verde.
