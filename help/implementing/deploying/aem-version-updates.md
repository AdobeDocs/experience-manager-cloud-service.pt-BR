---
title: Atualizações da versão AEM
description: 'Atualizações da versão AEM '
translation-type: tm+mt
source-git-commit: 3d9ed5ea31344bf4e25c37368cca01856cdbbd01
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Atualizações da versão AEM {#aem-version-updates}

## Introdução {#introduction}

AEM como Cloud Service agora usa a Integração contínua e o Delivery contínuo (CI/CD) para garantir que seus projetos estejam na versão mais recente do AEM. Isso significa que todas as operações de atualização são totalmente automatizadas, portanto, não é necessário interromper o serviço para os usuários.

>[!NOTE]
>Se a atualização do ambiente de produção falhar, o Cloud Manager reverterá automaticamente o ambiente stage. Isso é feito automaticamente para garantir que, após a conclusão de uma atualização, os ambientes de estágio e de produção estejam na mesma versão AEM.

AEM atualizações de versão são de dois tipos:

* **Atualizações de envio de AEM**

   * Pode ser lançado diariamente.

   * A maioria da manutenção, incluindo as últimas correções de erros e atualizações de segurança.

      Como as mudanças são aplicadas regularmente, o impacto é incremental, reduzindo o impacto sobre seu serviço.

* **Atualizações de novos recursos**

   * Lançado por meio de uma programação mensal previsível.

AEM atualizações passam por um pipeline de validação de produto intenso e totalmente automatizado, que envolve várias etapas, garantindo que o serviço não seja interrompido em nenhum sistema em produção. Os controlos de saúde são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante um AEM como uma atualização de Cloud Service, o lançamento não prosseguirá e o Adobe investigará por que a atualização causou esse comportamento inesperado.

[Os testes do produto e os testes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) funcionais do Cliente, que impedem que upgrades de produtos e empurramentos de código do cliente quebrem a produção, também são validados durante uma atualização da versão AEM.

>[!NOTE]
>
>Se o código personalizado foi enviado para o armazenamento temporário e depois rejeitado por você, a próxima atualização AEM removerá essas alterações para refletir a tag git da última versão do cliente bem-sucedido para produção.

## Armazenamento de nós composto {#composite-node-store}

Como mencionado acima, as atualizações na maioria dos casos resultarão em tempo de inatividade zero, inclusive para o autor, que é um cluster de nós. As atualizações contínuas são possíveis devido ao recurso de armazenamento *de nós* compostos no Oak.

Esse recurso permite que AEM faça referência a vários repositórios simultaneamente. Em uma implantação contínua, a nova versão do AEM Verde contém seu próprio repositório (o repositório executável baseado no TarMK), distinto da versão mais antiga do AEM Azul, embora ambos referenciem um repositório mutável baseado no DocumentMK compartilhado que contém áreas como `/libs` , `/content` , `/conf` `/etc` e outras. Como o Azul e o Verde têm suas próprias versões do `/libs`, ambos podem estar ativos durante a atualização do acumulado, ambos assumindo o tráfego até que o azul seja totalmente substituído pelo verde.

