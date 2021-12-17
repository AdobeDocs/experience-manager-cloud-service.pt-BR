---
title: Pós-ativação
description: Saiba como monitorar problemas e melhorar o desempenho
source-git-commit: c9143d77e70476beb7f7dd162c36aeda8d1be506
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 21%

---


# Pós-ativação {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solução de problemas de AEM"
>abstract="Revise as práticas recomendadas para o desenvolvimento contínuo e gerencie logs juntamente com ferramentas como o console do desenvolvedor e o CRXDE Lite para ajudar a solucionar problemas com o AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Acesso e gerenciamento de registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM ferramentas de desenvolvimento as a Cloud Service"

Esta é a última parte da jornada, portanto, você aprenderá a monitorar os problemas e a melhorar o desempenho após a conclusão da migração. Você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

## A História Até Agora {#story-so-far}

Na etapa anterior da jornada, você aprendeu a executar a migração e [Ao vivo](/help/journey-migration/go-live.md) assim que o código e o conteúdo estavam prontos para serem movidos para AEM as a Cloud Service.

## Objetivo {#objective}

Este documento descreve as ferramentas disponíveis para solucionar problemas AEM ambientes as a Cloud Service:

* **Console do desenvolvedor**
* **CRXDE Lite**
* **Gerenciamento de logs**

## Console do desenvolvedor {#developer-console}

A depuração AEM ambientes as a Cloud Service de desenvolvedor está disponível no Console do desenvolvedor para ambientes de desenvolvimento, preparo e produção.

Consulte [Implementação do AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) para saber mais sobre ferramentas de desenvolvimento.

## CRXDE Lite {#crxde-lite}

Como usuário, você pode acessar o CRXDE Lite no ambiente de desenvolvimento, mas não no ambiente de preparo ou produção.

>[!IMPORTANT]
>Gravação em repositórios imutáveis, como `/libs` e `/apps` em tempo de execução resulta em erros. Além disso, você não tem acesso a ferramentas de desenvolvedor para ambientes de preparo e produção.

Consulte [Desenvolvimento com o CRXDE Lite](/help/implementing/developing/tools/crxde.md) para saber como desenvolver seu aplicativo do AEM usando o CRXDE Lite.

## Gerenciamento de logs {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessar e gerenciar logs](/help/implementing/cloud-manager/manage-logs.md) para saber como acessar e gerenciar logs por meio da interface do usuário ou da API via Cloud Manager.

## Entrar em contato com o suporte {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ajuda e suporte"
>abstract="Entre em contato com a equipe de suporte AEM para obter esclarecimentos ou solucionar problemas."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Suporte para Experience Cloud"

Em caso de dúvidas sobre o acesso ao Cloud Service, entre em contato com o representante do Adobe ou [Suporte para Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes.

## Aprendizados de documentos {#document-learnings}

Quando a migração estiver concluída, você deverá documentar o conhecimento adquirido durante esse processo. Algumas perguntas que podem ajudar no processo de documentação são:

* O que funcionou bem e o que não funcionou?
* Quais foram os principais pontos problemáticos?
* Recommendations no caso de uma migração futura.

Em seguida, você deve compartilhar esses aprendizados pós-migração com as partes interessadas e equipes em sua organização.

## A Jornada Termina - Ou Será? {#journey-ends}

Parabéns! Você concluiu a Jornada de migração AEM as a Cloud Service! Você deve conhecer como:

* Comece já a mudar para AEM as a Cloud Service
* Determine se sua implantação está pronta para ser movida para AEM as a Cloud Service
* Prepare seu código e a nuvem de conteúdo
* Executar a migração
* Monitore problemas e melhore o desempenho
