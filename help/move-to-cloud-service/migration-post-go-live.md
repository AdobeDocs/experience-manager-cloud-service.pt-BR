---
title: Fase Pós-ativação
description: Fase Pós-ativação
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 60%

---

# Postagem ativa {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solução de problemas de AEM"
>abstract="Revise as práticas recomendadas para o desenvolvimento contínuo e gerencie logs juntamente com ferramentas como o console do desenvolvedor e o CRXDE Lite para ajudar a solucionar problemas com o AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Acesso e gerenciamento de registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM como ferramentas de desenvolvimento de Cloud Service"


Na fase Pós-ativação, você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

As seguintes ferramentas estão disponíveis para solucionar problemas com ambientes do AEM as a Cloud Service:

* **Console do desenvolvedor**
* **CRX/DE Lite**
* **Gerenciamento de logs**


## Console do desenvolvedor {#developer-console}

A depuração de ambientes de desenvolvedor do AEM as a Cloud Service está disponível no Console do desenvolvedor para ambientes de desenvolvimento, preparo e produção.

Consulte [Implementação do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) para saber mais sobre ferramentas de desenvolvimento.

## CRX/DE Lite {#crxde-lite}

Como usuário, você pode acessar o CRX/DE Lite no ambiente de desenvolvimento, mas não no ambiente de preparo ou produção.

>[!IMPORTANT]
>A gravação em repositórios imutáveis, como `/libs` e `/apps` em tempo de execução, resultará em erros. Além disso, como cliente, você não terá acesso a ferramentas de desenvolvedor para ambientes de preparação e produção.

Consulte [Desenvolvimento com o CRX/DE Lite](/help/implementing/developing/tools/crxde.md) para saber como desenvolver seu aplicativo do AEM usando o CRX/DE Lite.

## Gerenciamento de logs {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessar e gerenciar logs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para saber como acessar e gerenciar logs por meio da interface do usuário ou da API via Cloud Manager.

### Suporte adicional {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ajuda e suporte"
>abstract="Entre em contato com a equipe de suporte AEM para obter esclarecimentos ou solucionar problemas."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Suporte para Experience Cloud"

Em caso de dúvidas sobre o acesso ao Cloud Service, entre em contato com o representante do Adobe ou com o [Suporte para Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes.
