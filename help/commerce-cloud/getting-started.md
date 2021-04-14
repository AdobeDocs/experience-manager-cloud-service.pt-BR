---
title: Introdução ao AEM Commerce as a Cloud Service
description: Saiba como implantar um projeto de AEM habilitado para o comércio em um AEM em execução no as a Cloud Service. Use os recursos do Adobe Cloud Manager e um pipeline de CI/CD para criar a loja de referência Venia em um ambiente em execução.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
translation-type: tm+mt
source-git-commit: e34592d24c8f6c17e6959db1d5c513feaf6381c8
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 52%

---

# Introdução ao AEM Commerce as a Cloud Service {#start}

Para começar a usar o AEM Commerce as a Cloud Service, o Experience Manager Cloud Service deve ser fornecido com o complemento Commerce Integration Framework (CIF). O complemento CIF é um módulo adicional do [AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/sites/home.html).

## Integração {#onboarding}

A integração do AEM Commerce as a Cloud Service é um processo de duas etapas:

1. Ativação do AEM Commerce as a Cloud Service e provisionamento do complemento CIF
2. Conecte o AEM Commerce as a Cloud Service com sua solução comercial

A primeira etapa de integração é feita pelo Adobe. Para obter mais detalhes sobre preços e provisionamento, entre em contato com seu representante de vendas.

Com o provisionamento do complemento CIF, ele será aplicado a todos os programas existentes do Cloud Manager. Caso não tenha um programa do Cloud Manager, será necessário criar um novo. Para obter mais detalhes, consulte [Configurar o programa](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

A segunda etapa é o autoatendimento para cada ambiente do AEM as a Cloud Service. Há algumas configurações adicionais a serem feitas após o provisionamento inicial do complemento CIF.

## Conectar AEM com uma solução comercial {#magento}

Para conectar o complemento CIF e o [AEM Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) a uma solução comercial, é necessário fornecer o URL do ponto de extremidade GraphQL por meio de uma variável de ambiente do Cloud Manager. O nome da variável é `COMMERCE_ENDPOINT`. Deve ser configurada uma conexão segura via HTTPS.
Pode ser usado um URL de ponto de extremidade GraphQL da diferente para cada ambiente do AEM as a Cloud Service. Dessa forma, os projetos podem conectar AEM ambientes de preparo com sistemas de preparo comercial e AEM ambiente de produção a um sistema de produção comercial. Esse ponto de extremidade GraphQL da deve estar disponível publicamente. Não há suporte para VPN privada ou conexões locais. Como opção, é possível fornecer um cabeçalho de autenticação para usar recursos adicionais da CIF que exigem autenticação.

Há duas opções para configurar o ponto de extremidade:

### 1) Por meio da interface do usuário do Cloud Manager (padrão)

Isso pode ser feito usando uma caixa de diálogo na página Detalhes do ambiente . Ao visualizar esta página para um programa habilitado para comércio, um botão será exibido se o terminal não estiver configurado no momento:

![Implementação Final do Símbolo Ecológico](/help/commerce-cloud/assets/commerce-cmui.png)

Clicar nesse botão abre uma caixa de diálogo:

![Implementação Final do Símbolo Ecológico](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Depois que o endpoint (e, opcionalmente, o token) for definido, o endpoint será exibido na página de detalhes. Clicar no ícone Editar abrirá a mesma caixa de diálogo em que o endpoint pode ser modificado, se necessário.

![Implementação Final do Símbolo Ecológico](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 2) Via Adobe I/O CLI

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Para conectar AEM com uma solução comercial via Adobe I/O CLI, siga estas etapas:

1. Obtenha a CLI do Adobe I/O com o plug-in do Cloud Manager

   Consulte a [documentação do Adobe Cloud Manager](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) sobre como baixar, configurar e usar a [CLI do Adobe I/O](https://github.com/adobe/aio-cli) com o [plug-in da CLI do Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique a CLI do Adobe I/O com o AEM como um programa Cloud Service

3. Defina a variável `COMMERCE_ENDPOINT` no Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [documentos da CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para saber mais.

   O URL do ponto de extremidade GraphQL de comércio deve apontar para o serviço GraphQl do Commerce e usar uma conexão HTTPS segura. Por exemplo: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Você pode listar todas as variáveis do Cloud Manager usando o seguinte comando para verificar: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Agora você está pronto para usar o AEM Commerce as a Cloud Service e implantar seu projeto por meio do Cloud Manager.

## Ativar recursos que exigem autenticação (Opcional) {#staging}

>[!NOTE]
>
>Este recurso só está disponível com o Magento Enterprise Edition ou o Magento Cloud.

1. Faça logon no Magento e crie um token de integração. Consulte [Autenticação baseada em token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obter detalhes. Certifique-se de que o token de integração tenha *somente* acesso aos recursos `Content -> Staging`. Copie o valor `Access Token`.

1. Defina a variável `COMMERCE_AUTH_HEADER` secreta no Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

   Consulte [Conectando AEM Commerce com Magento](#magento) sobre como configurar a CLI do Adobe I/O para o Cloud Manager.

## Integrações de comércio de terceiros {#integrations}

Para integrações de comércio de terceiros, é preciso ter uma [camada de mapeamento de API](architecture/third-party.md) para conectar o AEM Commerce as a Cloud Service e os Componentes principais da CIF ao seu sistema de comércio. Normalmente, essa camada de mapeamento de API é implantada na Adobe I/O Runtime. Entre em contato com seu representante de vendas para obter integrações disponíveis e acesso à Adobe I/O Runtime.
