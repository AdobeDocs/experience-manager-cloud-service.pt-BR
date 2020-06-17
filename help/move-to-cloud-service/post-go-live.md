---
title: Fase de ativação da postagem
description: Fase de ativação da postagem
translation-type: tm+mt
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Publicar ao vivo {#post-go-live}

Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar as práticas recomendadas para o desenvolvimento contínuo e gerenciar registros.

As seguintes ferramentas estão disponíveis para solucionar problemas do AEM como ambientes de Cloud Service:

* **Developer Console**
* **CRX/DE Lite**
* **Gerenciamento de registros**


## Developer Console {#developer-console}

A depuração do AEM como ambientes para desenvolvedores de Cloud Service está disponível no Developer Console para ambientes de desenvolvimento, estágio e produção.

Consulte [Implementação do AEM como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) para saber mais sobre as ferramentas de desenvolvimento.

## CRX/DE Lite {#crxde-lite}

Como usuário, você pode acessar o CRX/DE Lite no ambiente de desenvolvimento, mas não no estágio ou na produção.

>[IMPORTANTE]
>A gravação em repositórios imutáveis, como `/libs` e `/apps` no tempo de execução, resultará em erros. Além disso, como cliente, você não terá acesso às ferramentas do desenvolvedor para ambientes de preparo e produção.

Consulte [Desenvolvimento com CRX/DE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) para saber como desenvolver seu aplicativo AEM usando o CRX/DE Lite.

## Gerenciamento de registros {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessar e gerenciar registros](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para saber como acessar e gerenciar registros por meio da interface do usuário ou da API por meio do Cloud Manager.

### Suporte adicional {#additional-support}

Se tiver dúvidas sobre o acesso ao Cloud Service, entre em contato com seu representante da Adobe ou com o Portal de suporte do Adobe AEM CQ.
