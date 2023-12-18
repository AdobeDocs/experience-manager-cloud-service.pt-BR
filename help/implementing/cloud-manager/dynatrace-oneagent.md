---
title: Dynatrace OneAgent
description: Saiba como usar o OneAgent do Dynatrace com AEM as a Cloud Service
source-git-commit: 2e70c8be73915bea860b98e02c08772bb4f5dcd2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

O Adobe oferece a capacidade de usar o OneAgent do Dynatrace para monitorar o AEM as a Cloud Service como parte de uma implantação corporativa, identificar a causa de possíveis problemas e tomar medidas para corrigi-los conforme necessário. <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## Integração do OneAgent ao AEM as a Cloud Service {#integrating-oneagent-with-aem-as-a-cloud-service}

Os clientes do Dynatrace OneAgent podem monitorar o uso do AEM solicitando conectividade por meio de um tíquete de suporte ao cliente.

Os detalhes necessários para solicitações de conectividade são descritos abaixo:

| **Campo** | **Descrição** |
|---|---|
| URL de ambiente do Dynatrace | O URL do ambiente do Dynatrace.<br><br>Para clientes SaaS do Dynatrace, o formato é `https://<environment>.live.dynatrace.com`.<br><br>Para clientes do Dynatrace Managed, o formato é `https://<your-managed-url>/e/<environmentId>` |
| ID de ambiente do Dynatrace | Sua ID de ambiente do Dynatrace, que pode ser encontrada no URL do ambiente |
| Token de ambiente do Dynatrace | Seu token de ambiente do OneAgent. Consulte a documentação do Dynatrace para saber como criar isso.<br><br>Isso deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, que o tíquete de suporte ao cliente pode mencionar, junto com a senha. |
| Token de acesso da API do Dynatrace | O token de acesso à API do seu ambiente Dynatrace. Consulte a documentação do Dynatrace para saber como criar isso.<br><br>Isso deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, que o tíquete de suporte ao cliente pode mencionar, junto com a senha.<br><br>Observação: isso só é necessário para o Dynatrace Managed. |
| Porta de destino do Dynatrace | A porta de destino do Dynamic Track.<br><br>Observação: isso só é necessário para o Dynatrace Managed. |
| ID(s) de ambiente do AEM | As IDs de ambiente do AEM que o Dynatrace deve monitorar. |


