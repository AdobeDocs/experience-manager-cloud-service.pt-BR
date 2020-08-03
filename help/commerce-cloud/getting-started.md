---
title: Introdução ao AEM Commerce como Cloud Service
description: Introdução ao AEM Commerce como Cloud Service
translation-type: tm+mt
source-git-commit: 170a6f4f3aa07b9aa917014b7a682ead9ed595c1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 3%

---


# Introdução ao AEM Commerce como Cloud Service {#start}

Para começar a usar AEM Commerce como Cloud Service, seu Experience Manager Cloud Service precisa ser provisionado com o complemento Commerce Integration Framework (CIF). O add-on CIF é um módulo adicional sobre [AEM Sites como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/home.html).

## Integração {#onboarding}

A integração do AEM Commerce como Cloud Service é um processo de duas etapas:

1. Obter comércio AEM como Cloud Service e o complemento CIF provisionado
2. Conecte o AEM Commerce como um Cloud Service com seu ambiente Magento

O primeiro passo é feito pela Adobe. Você precisará fornecer informações como a organização IMS, o URL do ponto de extremidade GraphQL do ambiente Magento etc. como parte do processo de provisionamento. Para obter mais detalhes sobre preços e provisionamento, é necessário entrar em contato com seu representante de vendas.

Depois que você tiver sido provisionado com o suplemento CIF, ele será aplicado a qualquer programa existente do Cloud Manager. Caso não tenha um Programa do Gerenciador de nuvem, será necessário criar um novo. Para obter mais detalhes, consulte [Configurar seu Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

A segunda etapa é o autoatendimento para cada AEM como um ambiente Cloud Service. Há algumas configurações adicionais que você precisará fazer após o provisionamento inicial do complemento CIF.

## Conexão AEM Comércio com o Magento {#magento}

Para conectar o suplemento CIF e os componentes [principais CIF](https://github.com/adobe/aem-core-cif-components) AEM com o ambiente Magento, é necessário fornecer o URL do terminal Magento GraphQL por meio de uma variável de ambiente do Cloud Manager. O nome da variável é `COMMERCE_ENDPOINT`. Uma conexão segura via HTTPS deve ser configurada.
Um URL de ponto de extremidade Magento GraphQL diferente pode ser usado para cada AEM como um ambiente. Dessa forma, os projetos podem conectar AEM ambientes de preparo com sistemas de preparo de Magento e AEM ambiente de produção a um sistema de produção de Magento. Esse ponto de extremidade Magento GraphQL deve estar disponível publicamente, VPN privada ou conexões locais não são suportadas.

Para conectar AEM Commerce ao Magento, siga estas etapas:

1. Obtenha a CLI de E/S do Adobe com o plug-in do Cloud Manager

   Consulte a documentação [do Gerenciador da](https://docs.adobe.com/content/help/br/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) Adobe Cloud sobre como baixar, configurar e usar a CLI [de E/S do](https://github.com/adobe/aio-cli) Adobe com o plug-in [da CLI do](https://github.com/adobe/aio-cli-plugin-cloudmanager)Cloud Manager.

2. Autentique a CLI com o AEM como programa Cloud Service

3. Definir a `COMMERCE_ENDPOINT` variável no Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte documentos [CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obter detalhes.

   O URL do ponto de extremidade Magento GraphQL deve apontar para o serviço GraphQl e usar uma conexão HTTPS segura. Por exemplo: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Você pode lista todas as variáveis do Gerenciador de nuvem usando o seguinte comando para verificar o duplo: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Nnota]
>
>Como alternativa, você pode usar a API [do Gerenciador de](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) nuvem para configurar as variáveis do Gerenciador de nuvem também.

Com isso, você está pronto para usar o AEM Commerce como Cloud Service e pode implantar seu projeto por meio do Cloud Manager.

## Integrações de comércio de terceiros {#integrations}

Para integrações de comércio de terceiros, é necessária uma camada [de mapeamento de](architecture/third-party.md) API para conectar AEM Commerce como Cloud Service e CIF Core Components ao seu sistema de comércio. Normalmente, essa camada de mapeamento da API é implantada no Adobe I/O Runtime. Entre em contato com seu representante de vendas para obter integrações disponíveis e acesso à Adobe I/O Runtime.
