---
title: Integrar o Edge Delivery Services com a CDN gerenciada pela Adobe no Cloud Manager
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Integrar o Edge Delivery Services com a CDN gerenciada pela Adobe no Cloud Manager {#integrate-adbe-cdn-with-edservices-in-cm}

A CDN gerenciada pela Adobe (AMC-D) integra-se nativamente ao Edge Delivery Services para fornecer experiências globalmente distribuídas e com bom desempenho para o Adobe Experience Manager (AEM) Sites.

Juntos, eles oferecem os seguintes benefícios:

* Uma CDN de nível empresarial, pronta para uso, gerenciada pela Adobe.
* Uma camada moderna de entrega de borda que acelera as solicitações, otimiza o armazenamento em cache e protege contra ataques comuns.
* Um fluxo de trabalho unificado do Cloud Manager para gerenciamento de domínio, certificados SSL e implantações orientadas por pipeline.

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Opções de implantação do Edge Delivery Services na CDN gerenciada pela Adobe no Cloud Manager {#deployment-options}

Este tópico explica as duas maneiras de implantar o Edge Delivery Services no Adobe Managed CDN na Cloud Manager e, igualmente importante, ajuda a decidir qual opção é a melhor para o seu caso de uso.

O Edge Delivery Services pode ser configurado usando uma das duas opções a seguir. Cada um tem diferentes recursos.

|  | Opção de implantação | Documento principal | Recurso | Melhor para |
| --- | --- | --- | --- | --- |
| Opção 1 | *Com* um ambiente AEM as a Cloud Service (AEMaaCS) existente | [Configurar um proxy de um ambiente existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | O Pipeline de configuração está disponível, em geral, para ambientes AEMaaCS | Equipes que já executam o Sites no Cloud Manager e desejam um aumento rápido no desempenho de baixo risco. |
| Opção 2 | *Sem* um ambiente AEMaaCS existente; conhecido como &quot;ambiente Edge&quot; independente. | [Configurar um site do Edge Delivery sem um ambiente existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | No momento, o Pipeline de configuração está disponível apenas para ambientes Edge por meio do programa limitado Beta.<br>Consulte [Adicionar Pipeline De Configuração Do Edge Delivery](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline). | Novos builds ou migrações que desejam adotar a arquitetura completa da Edge Delivery e o roteamento granular. |

<!-- Ultimately this URL above will need to be updated on GA -->

| Opção | Resumo | Melhor para | Documentos principais |
| --- | --- | --- | --- |
| Proxy da CDN gerenciada pela Adobe | O Adobe Managed CDN encaminha um ambiente AEM Sites existente. Seu pipeline do Sites atual permanece a &quot;origem&quot;, enquanto o AMC-D lida com armazenamento em cache de borda e encerramento de TLS. | Equipes que já executam o Sites no Cloud Manager e desejam um aumento rápido no desempenho de baixo risco. | Configurar um proxy AMC-D |
| Configuração do pipeline com originSelectors | Um pipeline de configuração do Edge Delivery dedicado publica conteúdo estático e dinâmico diretamente na borda. `originSelectors` rotear o tráfego entre a AMC-D e seus níveis de autor/publicação do AEM. | Novos builds ou migrações que desejam adotar a arquitetura completa da Edge Delivery e o roteamento granular. | Configurar o pipeline do Edge Delivery |

>[!TIP]
>
>Não sabe qual caminho escolher? Consulte [Escolher um modelo de implantação](#choose-deployment-model) abaixo para obter diretrizes de decisão.

## Escolha um modelo de implantação {#choose-deployment-model}

Ambos os modelos podem coexistir no mesmo programa Cloud Manager, permitindo migrações em fases.

| Se você... | Depois use... |
| :--- | :--- |
| Precisam de uma implantação rápida, com alterações mínimas, e já hospedam o Sites na Cloud Manager | Proxy AMC-D |
| Planeje reestruturar o conteúdo do Edge Delivery ou deseje um roteamento refinado entre várias origens | Configurar o pipeline de entrega do Edge + `originSelectors` |

## Pré-requisitos {#prerequisites}

1. Integração do site no Cloud Manager - Obrigatório para ambos os modelos de implantação. Siga Integrar um site do AEM.

2. Traga seu próprio Git (BYOG) (opcional) - se você armazenar o código do site fora do Adobe Git, conclua a integração do BYOG.

3. Licença do Edge Delivery - Verifique se o programa está licenciado para o Edge Delivery Services.


