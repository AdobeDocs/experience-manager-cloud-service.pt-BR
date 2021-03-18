---
title: Fase Pós-ativação
description: Fase Pós-ativação
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 100%

---


# Pós-ativação {#post-go-live}

Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

As seguintes ferramentas estão disponíveis para solucionar problemas com ambientes do AEM as a Cloud Service:

* **Console do desenvolvedor**
* **CRX/DE Lite**
* **Gerenciamento de logs**


## Console do desenvolvedor {#developer-console}

A depuração de ambientes de desenvolvedor do AEM as a Cloud Service está disponível no Console do desenvolvedor para ambientes de desenvolvimento, preparo e produção.

Consulte [Implementação do AEM as a Cloud Service](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/development-guidelines.translate.html#aem-as-a-cloud-service-development-tools
) para saber mais sobre ferramentas de desenvolvimento.

## CRX/DE Lite {#crxde-lite}

Como usuário, você pode acessar o CRX/DE Lite no ambiente de desenvolvimento, mas não no ambiente de preparo ou produção.

>[!IMPORTANT]
>A gravação em repositórios imutáveis, como `/libs` e `/apps` em tempo de execução, resultará em erros. Além disso, como cliente, você não terá acesso a ferramentas de desenvolvedor para ambientes de preparação e produção.

Consulte [Desenvolvimento com o CRX/DE Lite](/help/implementing/developing/tools/crxde.md) para saber como desenvolver seu aplicativo do AEM usando o CRX/DE Lite.

## Gerenciamento de logs {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessar e gerenciar logs](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.translate.html) para saber como acessar e gerenciar logs por meio da interface do usuário ou da API via Cloud Manager.

### Suporte adicional {#additional-support}

Em caso de dúvidas sobre o acesso ao Cloud Service, entre em contato com seu representante da Adobe ou com o Portal de suporte do Adobe AEM CQ.
