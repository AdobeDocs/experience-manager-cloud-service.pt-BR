---
title: Pós-ativação
description: Saiba como monitorar problemas e melhorar o desempenho.
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 14%

---

# Pós-ativação {#post-go-live}

<!-- Alexandru: contextual help links are broken, temporarily comminting this out until they,re fixed.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Troubleshooting AEM"
>abstract="Review best practices for continuous development and management of logs. Learn about tools like Developer Console and CRXDE Lite to help with troubleshooting issues with AEM."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs" text="Accessing and Managing Logs"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service Development tools"

-->

Esta jornada é a última parte, para que você saiba como monitorar problemas e melhorar o desempenho após a conclusão da migração. Garanta a limpeza de arquivos temporários, analise as práticas recomendadas para desenvolvimento contínuo e gerencie logs.

## A história até agora {#story-so-far}

Na etapa anterior da jornada, você aprendeu a executar a migração e a [ativação](/help/journey-migration/go-live.md) depois que o código e o conteúdo estivessem prontos para serem transferidos para o AEM as a Cloud Service.

## Objetivo {#objective}

Este documento descreve as ferramentas disponíveis para solucionar problemas em ambientes do AEM as a Cloud Service:

* **Console do desenvolvedor**
* **CRXDE Lite**
* **Gerenciamento de logs**

## Console do desenvolvedor {#developer-console}

A depuração de ambientes de desenvolvedor do AEM as a Cloud Service está disponível na Developer Console para ambientes de desenvolvimento, preparo e produção.

Consulte [Implementação do AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) para saber mais sobre ferramentas de desenvolvimento.

## CRXDE Lite {#crxde-lite}

Como usuário, você pode acessar o CRXDE Lite no ambiente de desenvolvimento, mas não no ambiente de preparo ou produção.

>[!IMPORTANT]
>A gravação em repositórios imutáveis, como `/libs` e `/apps` em tempo de execução, resulta em erros. Além disso, você não tem acesso a ferramentas de desenvolvedor para ambientes de preparo e produção.

Consulte [Desenvolvimento com o CRXDE Lite](/help/implementing/developing/tools/crxde.md) para obter mais informações sobre como desenvolver seu aplicativo do AEM usando o CRXDE Lite.

## Gerenciamento de logs {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessando e Gerenciando Logs](/help/implementing/cloud-manager/manage-logs.md) para saber como acessar e gerenciar logs por meio da interface do usuário ou da API por meio da Cloud Manager.

## Contato com o suporte {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ajuda e suporte"
>abstract="Entre em contato com a equipe de suporte do Adobe AEM para obter esclarecimentos ou tirar dúvidas."
>additional-url="https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html" text="Suporte para a Experience Cloud"

Em caso de dúvidas sobre o acesso ao Cloud Service, entre em contato com o representante da Adobe ou com o [Suporte do Experience Cloud](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes.

## Aprendizados de documento {#document-learnings}

Quando a migração estiver concluída, documente o conhecimento adquirido durante esse processo. Algumas perguntas que podem ajudar no processo de documentação do são:

* O que funcionou bem e o que não?
* Quais eram os principais pontos problemáticos?
* Recomendações se houver uma migração futura.

Compartilhe esses aprendizados pós-migração com as partes interessadas e as equipes da sua organização.

## A jornada termina - Será? {#journey-ends}

Parabéns! Você concluiu a Jornada de migração do AEM as a Cloud Service. Você deve entender como:

* Introdução à migração para o AEM as a Cloud Service
* Determine se sua implantação está pronta para ser movida para o AEM as a Cloud Service
* Prepare o código e a nuvem de conteúdo
* Executar a migração
* Monitore problemas e melhore o desempenho
