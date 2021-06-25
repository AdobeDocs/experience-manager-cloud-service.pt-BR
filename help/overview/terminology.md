---
title: Introdução ao Adobe Experience Manager as a Cloud Service - Terminologia
description: Introdução ao Adobe Experience Manager as a Cloud Service - Terminologia.
exl-id: a76f68f1-4f84-4844-a099-0952707cd96d
source-git-commit: 4067db2234b29e4ffbe3e76f25afd9d8642a1973
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 97%

---

# Adobe Experience Manager as a Cloud Service - Terminologia {#adobe-experience-manager-as-a-cloud-service-terminology}

Os termos a seguir são usados em relação ao Adobe Experience Manager (AEM) as a Cloud Service:

## Produtos {#products}

| Produto | Descrição |
|---|---|
| AEM as a Cloud Service | A forma nativa de nuvem de aproveitar os aplicativos do AEM |
| Ativos AEM as a Cloud Service | Recursos do Gerenciamento de ativos digitais (DAM) como uma solução escalável nativa em nuvem para assimilar, processar e gerenciar seus ativos digitais e, ao mesmo tempo, integrar ao ecossistema mais amplo da Adobe Experience Cloud e da Adobe Creative Cloud. |
| AEM Sites as a Cloud Service | Uma instância do AEM as a Cloud Service com o aplicativo do AEM Sites. |

## Instâncias e pipelines {#instances-and-pipelines}

| Instância | Descrição |
|---|---|
| Adobe Pipeline | O mecanismo de publicação de conteúdo do autor para publicação. |
| Nível de criação do AEM | Descreve o ambiente de criação do Sites e do Assets. |
| Camada de visualização do AEM | Descreve o ambiente de visualização do Sites. |
| Nível de publicação do AEM | Descreve o ambiente de publicação de Sites. |


<!-- This section of the table must be alphabetic -->

## Terminologia {#terminology}

| Termo | Descrição |
|---|---|
| Imagem do AEM | Um artefato implantável que contém o código do produto do AEM junto com o código do cliente. |
| Microsserviços de ativos | Serviços de processamento de ativos digitais em nuvem que atendem a vários casos de uso do processamento de ativos, como geração de representação, processamento de PDFs, manipulação de subativos, extração de texto e assim por diante. Consulte a [visão geral dos microsserviços de ativos](/help/assets/asset-microservices-overview.md) para obter mais informações. |
| Repositório Git do Cloud Manager | Onde os clientes armazenam os códigos e as definições de configuração. |
| Provedor de nuvem | Atualmente, o AEM as a Cloud Service oferece suporte ao Azure. O suporte para a AWS é um roteiro. |
| Rede de entrega de conteúdo (CDN) | O AEM as Cloud Service é enviado com um CDN padrão. Seu principal objetivo é reduzir a latência, fornecendo conteúdo que pode ser armazenado em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM. |
| Repositório de conteúdo | Onde o conteúdo é persistente. |
| Isolamento corporativo | Cada instância do AEM as a Cloud Service é isolada das outras instâncias. |
| Golden Master | O nível de publicação do AEM. |
| Mecanismo de orquestração | O AEM as a Cloud Service usa um mecanismo de orquestração para garantir que todos os serviços de criação e publicação estejam dimensionando como e quando necessário. |
