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
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 30%

---

# Introdução ao AEM Commerce as a Cloud Service {#start}

Para começar a usar o AEM Commerce as a Cloud Service, o Experience Manager Cloud Service deve ser fornecido com o complemento Commerce Integration Framework (CIF). O complemento CIF é um módulo adicional do [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Integração {#onboarding}

A integração do AEM Commerce as a Cloud Service é um processo de duas etapas:

1. Ativação do AEM Commerce as a Cloud Service e provisionamento do complemento CIF
2. Conecte o AEM Commerce as a Cloud Service com sua solução comercial

A primeira etapa de integração é feita pelo Adobe. Para obter mais detalhes sobre preços e provisionamento, entre em contato com seu representante de vendas.

Com o provisionamento do complemento CIF, ele será aplicado a todos os programas existentes do Cloud Manager. Caso não tenha um programa do Cloud Manager, será necessário criar um novo. Para obter mais detalhes, consulte [Configurar o programa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

A segunda etapa é o autoatendimento para cada ambiente do AEM as a Cloud Service. Há algumas configurações adicionais a serem feitas após o provisionamento inicial do complemento CIF.

## Conexão de AEM com uma solução comercial {#magento}

Para conectar o complemento CIF e o [AEM Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) a uma solução comercial, é necessário fornecer o URL do ponto de extremidade GraphQL por meio de uma variável de ambiente do Cloud Manager. O nome da variável é `COMMERCE_ENDPOINT`. Deve ser configurada uma conexão segura via HTTPS.

Essa variável de ambiente é usada em dois lugares:

- Chamadas GraphQL de AEM para o backend comercial, por meio de um cliente GraphQl compartilhável comum, usado pelos Componentes principais da CIF AEM e componentes do projeto do cliente.
- Configure um URL proxy GraphQL em cada ambiente de AEM em que a variável está definida e está disponível em `/api/graphql`. Isso é usado pelas ferramentas de criação comercial do AEM (complemento CIF) e pelos componentes do lado do cliente da CIF.

Pode ser usado um URL de ponto de extremidade GraphQL da diferente para cada ambiente do AEM as a Cloud Service. Dessa forma, os projetos podem conectar AEM ambientes de preparo com sistemas de preparo comercial e AEM ambiente de produção a um sistema de produção comercial. Esse ponto de extremidade GraphQL da deve estar disponível publicamente. Não há suporte para VPN privada ou conexões locais. Como opção, é possível fornecer um cabeçalho de autenticação para usar recursos adicionais da CIF que exigem autenticação.

Opcional e somente para o Adobe Commerce Enterprise / Cloud, o complemento CIF oferece suporte ao uso de dados de catálogo preparados para AEM autores. Isso requer a configuração de um token de autorização. O token de autorização configurado só está disponível e é usado em instâncias AEM autor por motivos de segurança. AEM instâncias de publicação não podem mostrar dados preparados.

Há duas opções para configurar o ponto de extremidade:

### Por meio da interface do usuário do Cloud Manager (padrão) {#cm-ui}

Isso pode ser feito usando uma caixa de diálogo na página Detalhes do ambiente . Ao visualizar esta página para um programa habilitado para comércio, um botão será exibido se o terminal não estiver configurado no momento:

![Informações do ambiente CM](/help/commerce-cloud/assets/commerce-cmui.png)

Clicar nesse botão abre uma caixa de diálogo:

![Endpoint de comércio CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Depois que o endpoint (como opção, um token de autenticação para suporte ao catálogo preparado) é definido, o endpoint é exibido na página de detalhes. Clicar no ícone Editar abrirá a mesma caixa de diálogo em que o endpoint pode ser modificado, se necessário.

![Informações do ambiente CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Via Adobe I/O CLI {#adobe-cli}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Para conectar AEM com uma solução comercial via Adobe I/O CLI, siga estas etapas:

1. Obtenha a CLI do Adobe I/O com o plug-in do Cloud Manager

   Verifique a [documentação do Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=pt-BR) sobre como baixar, configurar e usar o [Adobe I/O CLI](https://github.com/adobe/aio-cli) com o [plug-in da CLI do Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique a CLI do Adobe I/O com o AEM como um programa Cloud Service

3. Defina a variável `COMMERCE_ENDPOINT` no Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [documentos da CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para saber mais.

   O URL do ponto de extremidade GraphQL de comércio deve apontar para o serviço GraphQl do Commerce e usar uma conexão HTTPS segura. Por exemplo: `https://demo.magentosite.cloud/graphql`.

4. Habilitar recursos do catálogo de preparo que exigem autenticação (opcional)

   >[!NOTE]
   >
   >Esse recurso só está disponível com o Adobe Commerce Enterprise ou Cloud Edition. Consulte [Autenticação baseada em token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obter detalhes.

   Defina a variável `COMMERCE_AUTH_HEADER` secreta no Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Você pode listar todas as variáveis do Cloud Manager usando o seguinte comando para verificar: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Agora você está pronto para usar o AEM Commerce as a Cloud Service e implantar seu projeto por meio do Cloud Manager.

## Configuração de lojas e catálogos {#catalog}

O complemento CIF e os [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) podem ser usados em várias estruturas de site AEM conectadas a diferentes lojas de comércio (ou visualizações de loja, etc.). Por padrão, o complemento CIF é implantado com uma configuração padrão conectando-se à loja e ao catálogo padrão do Adobe Commerce (Magento).

Essa configuração pode ser ajustada para o projeto por meio da configuração do Cloud Service da CIF, seguindo estas etapas:

1. AEM acesse Ferramentas -> Cloud Services -> Configuração da CIF

2. Selecione a configuração de comércio que deseja alterar

3. Abra as propriedades de configuração na barra de ações

![Configuração do CIF Cloud Services](/help/commerce-cloud/assets/cif-cloud-service-config.png)

As seguintes propriedades podem ser configuradas:

- Cliente GraphQL - selecione o cliente GraphQL configurado para comunicação de back-end de comércio. Normalmente, isso deve permanecer no padrão.
- Exibição de armazenamento - o identificador de exibição de loja (Magento). Se estiver vazia, a exibição de loja padrão será usada.
- Caminho do proxy GraphQL - o caminho do URL Proxy GraphQL no AEM usado para solicitações de proxy no ponto de extremidade GraphQL de back-end do comércio.
   >[!NOTE]
   >
   > Na maioria das configurações, o valor padrão `/api/graphql` não deve ser alterado. Somente a configuração avançada que não usa o proxy GraphQL fornecido deve alterar essa configuração.
- Ativar o suporte à UID do catálogo - ative o suporte para UID em vez da ID nas chamadas GraphQL de back-end de comércio.
   >[!NOTE]
   >
   > O suporte para UIDs foi introduzido no Adobe Commerce (Magento) 2.4.2. Habilite-o somente se o back-end comercial suportar um esquema GraphQL da versão 2.4.2 ou posterior.
- Identificador de categoria raiz do catálogo - o identificador (UID ou ID) da raiz do catálogo de loja

A configuração mostrada acima é para referência. Os projetos devem fornecer suas próprias configurações.

Para configurações mais complexas usando várias estruturas de site de AEM combinadas com diferentes catálogos de comércio, consulte o tutorial [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md).

## Recursos adicionais {#additional-resources}

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md)
