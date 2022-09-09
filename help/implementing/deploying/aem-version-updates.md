---
title: Atualizações de versão do AEM
description: Atualizações de versão do AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 4%

---


# Atualizações de versão do AEM {#aem-version-updates}

## Introdução {#introduction}

AEM as a Cloud Service agora usa integração contínua e entrega contínua (CI/CD) para garantir que seus projetos estejam na versão de AEM mais recente. Isso significa que as instâncias de produção e de preparo são atualizadas para a versão de AEM mais recente, sem interrupção do serviço para os usuários.

>[!NOTE]
>
>Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e produção estejam na mesma versão AEM.

Há dois tipos de atualizações de versão AEM:

* **Atualizações de manutenção de AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Ter um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * São liberados por meio de uma programação mensal previsível.

AEM atualizações passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que o serviço não seja interrompido em nenhum sistema em produção. Os controlos sanitários são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante uma atualização as a Cloud Service AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Testes do produto e testes funcionais do cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) que impedem que atualizações de produtos e códigos de clientes quebrem sistemas de produção, também são validados durante uma atualização de versão AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para o armazenamento temporário e depois rejeitado por você, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção.

## Loja de nós composta {#composite-node-store}

As atualizações na maioria dos casos terão zero tempo de inatividade, incluindo para a instância de criação, que é um cluster de nós. As atualizações contínuas são possíveis devido ao recurso de armazenamento de nó composto no Oak.

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em uma implantação contínua, a nova versão AEM verde contém a sua própria `/libs` (o repositório imutável baseado em TarMK), distinto da versão azul mais antiga do AEM, embora ambos referenciem um repositório mutável baseado em DocumentMK compartilhado que contém áreas como `/content` , `/conf` , `/etc` e outros. Porque tanto o azul quanto o verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos gerando tráfego até que o azul seja totalmente substituído pelo verde.
