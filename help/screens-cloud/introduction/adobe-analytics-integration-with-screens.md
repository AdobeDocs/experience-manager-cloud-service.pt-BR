---
title: Integração do Adobe Analytics com a AEM Screens Cloud
seo-title: Adobe Analytics Integration with AEM Screens
description: Siga esta página para saber mais sobre a integração imediata do AEM Screens com o Adobe Analytics e fornecer uma prova de reprodução.
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
exl-id: e22242ce-e5ce-4486-bba4-e6a89ac4fb5e
source-git-commit: 75d147886c8151f8b8ac41af907e17b5deff5a9c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Integração do Adobe Analytics com a AEM Screens Cloud {#adobe-analytics-integration-with-aem-screens}

Esta seção abrange os seguintes tópicos:

* **Visão geral**
* **Detalhes da arquitetura**

## Visão geral {#overview}

***AEM Screens*** A utiliza o Adobe Analytics e, com isso, você pode alcançar algo único no mercado: o cross-channel analytics, que ajuda a correlacionar o conteúdo mostrado no local com outras fontes de dados.

O AEM Screens fornece uma integração imediata com o Adobe Analytics e uma prova de atividade.

Esta seção descreve a seguinte funcionalidade envolvida na conexão de um projeto do AEM Screens com o Adobe Analytics:

* Permite o relatório de prova de reprodução por dispositivo
* Permite relatórios de prova de reprodução por ativo
* Garante que todos os eventos do player sejam capturados e carimbados com data e hora
* Garante que todos os eventos do player sejam armazenados localmente se a reprodução não estiver conectada a uma rede
* Permite a criação de loops de comentários que rastreiam eventos de reprodução ao longo do tempo
* Permite que o sistema modifique o conteúdo e os layouts com base nos critérios de sucesso definidos pelo autor de conteúdo

A integração do Adobe Analytics com o AEM Screens impõe o seguinte *metas*:

* Habilitar o ROI de implementações de sinalização digital
* Integre o Analytics como base para viabilização futura da coleta e análise de informações de uso

## Detalhes da arquitetura {#architectural-details}

Um cliente do AEM Screens deseja entender qual conteúdo foi mostrado, em que momento e por quanto tempo (agregado). Esse é um recurso comum da solução de sinalização. Em vez de criar nossa própria análise, o AEM Screens aproveitará o Adobe Analytics e, com isso, poderemos alcançar algo exclusivo no mercado: a análise entre canais, que ajuda a correlacionar o conteúdo mostrado no local com outras fontes de dados.

O diagrama de arquitetura a seguir explica a integração do Adobe Analytics com o AEM Screens:

![Integração com o Adobe Analytics](/help/screens-cloud/assets/analytics-architecture.png)

## Habilitar o Adobe Analytics na AEM Screens Cloud {#enabling-adobe-analytics-in-aem-screens-cloud}

Entre em contato com o Gerente de relacionamento de Adobe para ativar a análise de Adobe no Screens Cloud.

## Utilização do serviço Adobe Analytics na AEM Screens Cloud {#using-adobe-analytics-service-in-aem-screens}

Esse cenário invoca a API do Analytics por meio de chamadas REST de um serviço de análise nos componentes principais do firmware e da tela do instrumento para criar e enviar eventos específicos para um caso de uso específico e, ao mesmo tempo, permitir a extensibilidade, em que qualquer mensagem personalizada pode ser enviada para o Analytics a partir de um canal desenvolvido personalizado.

Os eventos do Analytics são armazenados offline no indexedDB e, posteriormente, fragmentados e enviados para a nuvem.

>[!NOTE]
>Para saber mais sobre o Sequenciamento e o Modelo de dados padrão para eventos, consulte [Configuração do Adobe Analytics para AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/administering/analytics-integration/configuring-adobe-analytics-aem-screens.html) para obter detalhes.
