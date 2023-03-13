---
title: Atualizações de versão do AEM
description: Atualizações de versão do AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: f977c6d8fa3ebd4b082e48da8b248178f9a2f34b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 30%

---


# Atualizações de versão do AEM {#aem-version-updates}

## Introdução {#introduction}

O AEM as a Cloud Service agora usa a integração/entrega contínua (CI/CD) para garantir que seus projetos estejam sempre na versão do AEM mais recente. Isso significa que as instâncias de produção e de preparo são atualizadas para a versão mais recente do AEM sem interrupção do serviço para os usuários.

>[!NOTE]
>
>Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.

Há dois tipos de atualizações de versão do AEM:

* **Atualizações de manutenção do AEM**

   * Pode ser lançado diariamente.
   * Elas são utilizadas principalmente para fins de manutenção, incluindo as correções de erros e atualizações de segurança mais recentes.
   * Têm um impacto mínimo, uma vez que as alterações são aplicadas regularmente.

* **Novas atualizações de recursos**

   * Elas são liberadas em um cronograma mensal previsível.

As atualizações do AEM passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que não haja interrupção do serviço para nenhum sistema em produção. As verificações de integridade são usadas para monitorar a integridade do aplicativo. Se essas verificações falharem durante uma atualização as a Cloud Service do AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Testes do produto e testes funcionais do cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) que impedem que atualizações de produtos e envios por push de código do cliente interrompam os sistemas de produção, também são validados durante uma atualização de versão do AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para preparo e não para produção, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção. Portanto, o código personalizado que estava disponível somente no preparo terá que ser implantado novamente.

## Armazenamento de nó composto {#composite-node-store}

As atualizações na maioria dos casos não terão tempo de inatividade, inclusive para a instância de criação, que é um cluster de nós. As atualizações contínuas são possíveis devido ao recurso de armazenamento de nó composto no Oak.

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em uma implantação contínua, a nova versão verde do AEM contém sua própria `/libs` (o repositório imutável baseado em TarMK), distinto da versão mais antiga do AEM azul, embora ambos façam referência a um repositório mutável compartilhado baseado em DocumentMK que contém áreas como `/content` , `/conf` , `/etc` e outros. Porque tanto o azul quanto o verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos assumindo o tráfego até que o azul seja totalmente substituído pelo verde.
