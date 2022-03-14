---
title: Atualizações de versão do AEM
description: 'Atualizações de versão do AEM '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 36%

---

# Atualizações de versão do AEM {#aem-version-updates}

## Introdução {#introduction}

O AEM as a Cloud Service agora usa a Integração contínua e o Delivery contínuo (CI/CD) para garantir que seus projetos estejam na versão do AEM mais recente. Isso significa que as instâncias de Produção e Preparo são atualizadas para a versão mais recente do AEM sem interrupção do serviço para os usuários.

>[!NOTE]
>Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de preparo e de produção estejam na mesma versão do AEM.

As atualizações de versão do AEM são de dois tipos:

* **Atualizações de push do AEM**

   * Pode ser lançado diariamente.

   * Geralmente manutenção, incluindo as últimas correções de erros e atualizações de segurança.

      Como as alterações são aplicadas regularmente, o impacto é incremental, reduzindo o impacto no serviço.

* **Novas atualizações de recursos**

   * Liberado em um cronograma mensal previsível.

AEM atualizações passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que o serviço não seja interrompido em nenhum sistema em produção. Os controlos sanitários são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante uma atualização as a Cloud Service AEM, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Testes do produto e testes funcionais do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) que impedem que as atualizações de produtos e os envios de código do cliente quebrem a produção também são validados durante uma atualização de versão AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para o armazenamento temporário e depois rejeitado por você, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção.

## Loja de nós composta {#composite-node-store}

Como mencionado acima, as atualizações na maioria dos casos terão tempo de inatividade zero, incluindo para o autor, que é um cluster de nós. As atualizações em andamento são possíveis devido à variável *armazenamento de nó composto* no Oak.

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em uma implantação contínua, a nova versão do AEM verde contém seu próprio `/libs` (o repositório imutável baseado em TarMK), distinto da versão mais antiga do AEM Azul, embora ambos referenciem um repositório mutável baseado em DocumentMK compartilhado que contém áreas como `/content` , `/conf` , `/etc` e outros. Porque tanto o Azul quanto o Verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos gerando tráfego até que o azul seja totalmente substituído pelo verde.
