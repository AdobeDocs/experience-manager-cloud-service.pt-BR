---
title: Introdução ao AEM Commerce as a Cloud Service
description: Introdução ao AEM Commerce as a Cloud Service
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 100%

---


# Introdução ao AEM Commerce as a Cloud Service {#start}

Para começar a usar o AEM Commerce as a Cloud Service, o Experience Manager Cloud Service deve ser fornecido com o complemento Commerce Integration Framework (CIF). O complemento CIF é um módulo adicional do [AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/sites/home.html).

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## Integração {#onboarding}

A integração do AEM Commerce as a Cloud Service é um processo de duas etapas:

1. Ativação do AEM Commerce as a Cloud Service e provisionamento do complemento CIF
2. Conexão do AEM Commerce as a Cloud Service com seu ambiente Magento

O primeiro passo é feito pela Adobe. Você deve fornecer informações como a organização IMS, o URL do ponto de extremidade GraphQL do ambiente Magento etc., como parte do processo de provisionamento. Para obter mais detalhes sobre preços e provisionamento, entre em contato com seu representante de vendas.

Com o provisionamento do complemento CIF, ele será aplicado a todos os programas existentes do Cloud Manager. Caso não tenha um programa do Cloud Manager, será necessário criar um novo. Para obter mais detalhes, consulte [Configurar o programa](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

A segunda etapa é o autoatendimento para cada ambiente do AEM as a Cloud Service. Há algumas configurações adicionais a serem feitas após o provisionamento inicial do complemento CIF.

## Conectar o AEM Commerce com a Magento {#magento}

Para conectar o complemento CIF e os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) com o ambiente Magento, é preciso informar o URL do ponto de extremidade GraphQL da Magento por meio de uma variável de ambiente do Cloud Manager. O nome da variável é `COMMERCE_ENDPOINT`. Deve ser configurada uma conexão segura via HTTPS.
Pode ser usado um URL de ponto de extremidade GraphQL da Magento diferente para cada ambiente do AEM as a Cloud Service. Dessa forma, os projetos podem conectar ambientes de preparo do AEM a sistemas de preparo da Magento e o ambiente de produção do AEM a um sistema de produção da Magento. Esse ponto de extremidade GraphQL da Magento deve estar disponível publicamente. Não há suporte para VPN privada ou conexões locais.

Para conectar o AEM Commerce ao Magento, siga estas etapas:

1. Obtenha a CLI do Adobe I/O com o plug-in do Cloud Manager

   Consulte a [documentação do Adobe Cloud Manager](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) sobre como baixar, configurar e usar a [CLI do Adobe I/O](https://github.com/adobe/aio-cli) com o [plug-in da CLI do Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique a CLI com o programa do AEM as a Cloud Service

3. Defina a variável `COMMERCE_ENDPOINT` no Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [documentos da CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para saber mais.

   O URL do ponto de extremidade GraphQL da Magento deve apontar para o serviço GraphQl da Magento e usar uma conexão HTTPS segura. Por exemplo: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Você pode listar todas as variáveis do Cloud Manager usando o seguinte comando para verificar: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>Como alternativa, você pode usar a [API do Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) para configurar também as variáveis do Cloud Manager.

Agora você está pronto para usar o AEM Commerce as a Cloud Service e implantar seu projeto por meio do Cloud Manager.

## Integrações de comércio de terceiros {#integrations}

Para integrações de comércio de terceiros, é preciso ter uma [camada de mapeamento de API](architecture/third-party.md) para conectar o AEM Commerce as a Cloud Service e os Componentes principais da CIF ao seu sistema de comércio. Normalmente, essa camada de mapeamento de API é implantada na Adobe I/O Runtime. Entre em contato com seu representante de vendas para obter integrações disponíveis e acesso à Adobe I/O Runtime.
