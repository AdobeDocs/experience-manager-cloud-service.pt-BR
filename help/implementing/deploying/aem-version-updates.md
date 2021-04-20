---
title: Atualizações de versão do AEM
description: 'Atualizações de versão do AEM '
feature: Deploying
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Atualizações de versão do AEM {#aem-version-updates}

## Introdução {#introduction}

O AEM as a Cloud Service agora usa a Integração contínua e o Delivery contínuo (CI/CD) para garantir que seus projetos estejam na versão mais recente do AEM. Isso significa que as instâncias de Produção e Estágio são atualizadas para a versão mais recente do AEM, sem interrupção do serviço para os usuários.

>[!NOTE]
>Se a atualização para o ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente de preparo. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de estágio e de produção estejam na mesma versão AEM.

AEM atualizações de versão são de dois tipos:

* **Atualizações de push do AEM**

   * Pode ser lançado diariamente.

   * Geralmente, manutenção, incluindo as últimas correções de erros e atualizações de segurança.

      À medida que as alterações são aplicadas regularmente, o impacto é incremental, reduzindo o impacto no serviço.

* **Novas atualizações de recursos**

   * Liberado por um agendamento mensal previsível.

AEM atualizações passam por um pipeline de validação de produto intenso e totalmente automatizado, envolvendo várias etapas, garantindo que o serviço não seja interrompido em nenhum sistema em produção. Os controlos sanitários são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante uma AEM como atualização de Cloud Service, a versão não continuará e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Os testes do produto e os ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) testes funcionais do cliente, que impedem que as atualizações do produto e os envios de código do cliente quebrem a produção, também são validados durante uma atualização da versão AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para o armazenamento temporário e depois rejeitado por você, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão bem-sucedida do cliente para produção.

## Armazenamento de nós composto {#composite-node-store}

Como mencionado acima, as atualizações na maioria dos casos terão tempo de inatividade zero, incluindo para o autor, que é um cluster de nós. As atualizações contínuas são possíveis devido ao recurso *armazenamento de nó composto* no Oak.

Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em uma implantação em andamento, a nova versão do Green AEM contém seu próprio `/libs` (o repositório imutável baseado no TarMK), distinto da versão mais antiga do Blue AEM, embora ambos referenciem um repositório mutável baseado no DocumentMK compartilhado que contém áreas como `/content` , `/conf` , `/etc` e outras. Como o Azul e o Verde têm suas próprias versões de `/libs`, ambos podem estar ativos durante a atualização contínua, ambos assumindo o tráfego até que o azul seja totalmente substituído pelo verde.

