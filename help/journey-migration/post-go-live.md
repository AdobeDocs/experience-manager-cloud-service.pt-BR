---
title: Pós-ativação
description: Saiba como monitorar problemas e melhorar o desempenho
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 39%

---

# Pós-ativação {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solução de problemas do AEM"
>abstract="Revise as práticas recomendadas para o desenvolvimento contínuo e gerencie logs juntamente com ferramentas como o console do desenvolvedor e o CRXDE Lite para ajudar a solucionar problemas do AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Acesso e gerenciamento de registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="Ferramentas de desenvolvimento do AEM as a Cloud Service"

Esta é a última parte da jornada; portanto, você aprenderá a monitorar problemas e melhorar o desempenho após a conclusão da migração. Você deve garantir a limpeza de arquivos temporários, analisar práticas recomendadas para desenvolvimento contínuo e gerenciar logs.

## A história até agora {#story-so-far}

Na etapa anterior da jornada, você aprendeu a executar a migração e [Ativação](/help/journey-migration/go-live.md) quando o código e o conteúdo estavam prontos para serem transferidos para o AEM as a Cloud Service.

## Objetivo {#objective}

Este documento descreve as ferramentas disponíveis para solucionar problemas de ambientes as a Cloud Service AEM:

* **Console do desenvolvedor**
* **CRXDE Lite**
* **Gerenciamento de logs**

## Console do desenvolvedor {#developer-console}

A depuração de ambientes de desenvolvedor do AEM as a Cloud Service está disponível no Console do desenvolvedor para ambientes de desenvolvimento, preparo e produção.

Consulte [Implementação do AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) para saber mais sobre ferramentas de desenvolvimento.

## CRXDE Lite {#crxde-lite}

Como usuário, você pode acessar o CRXDE Lite no ambiente de desenvolvimento, mas não no ambiente de preparo ou produção.

>[!IMPORTANT]
>Gravação em repositórios imutáveis, como `/libs` e `/apps` no tempo de execução resulta em erros. Além disso, você não tem acesso a ferramentas de desenvolvedor para ambientes de preparo e produção.

Consulte [Desenvolvimento com o CRXDE Lite](/help/implementing/developing/tools/crxde.md) para saber como desenvolver seu aplicativo do AEM usando o CRXDE Lite.

## Gerenciamento de logs {#managing-logs}

Os usuários podem acessar uma lista de arquivos de log disponíveis para o ambiente selecionado.

Consulte [Acessar e gerenciar logs](/help/implementing/cloud-manager/manage-logs.md) para saber como acessar e gerenciar logs por meio da interface do usuário ou da API via Cloud Manager.

## Entrando em contato com o suporte {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ajuda e suporte"
>abstract="Entre em contato com a Equipe de suporte do AEM para tirar dúvidas ou enviar preocupações."
>additional-url="https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html" text="Suporte para a Experience Cloud"

Em caso de dúvidas sobre o acesso ao Cloud Service, entre em contato com o representante da Adobe ou [Suporte para Experience Cloud](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para obter mais detalhes.

## Aprendizados de documento {#document-learnings}

Quando a migração estiver concluída, você deverá documentar o conhecimento adquirido durante esse processo. Algumas perguntas que podem ajudar no processo de documentação do são:

* O que funcionou bem e o que não?
* Quais eram os principais pontos problemáticos?
* Recommendations no caso de uma migração futura.

Em seguida, você deve compartilhar esses aprendizados pós-migração com as partes interessadas e as equipes dentro da organização.

## A jornada termina - Será? {#journey-ends}

Parabéns! Você concluiu a Jornada de migração as a Cloud Service do AEM! Você deve entender como:

* Introdução à migração para o AEM as a Cloud Service
* Determine se sua implantação está pronta para ser movida para o AEM as a Cloud Service
* Prepare o código e a nuvem de conteúdo
* Executar a migração
* Monitore problemas e melhore o desempenho
