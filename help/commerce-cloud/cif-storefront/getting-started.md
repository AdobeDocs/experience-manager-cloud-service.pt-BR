---
title: Introdução ao AEM Commerce as a Cloud Service
description: Saiba como implantar um projeto de comércio do Adobe Experience Manager (AEM) usando o Adobe Cloud Manager, um pipeline de CI/CD e a loja de referência Venia.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 9%

---


# Introdução ao AEM Commerce as a Cloud Service {#start}

Para começar a usar o Adobe Experience Manager (AEM) Commerce as a Cloud Service, o Experience Manager Cloud Service deve ser provisionado com o complemento Commerce integration framework (CIF). O complemento CIF é um módulo extra sobre o [AEM Sites as a Cloud Service.](/help/sites-cloud/sites-cloud-changes.md)

>[!TIP]
>
>**Você já considerou o Edge Delivery Services?**
>
>O Edge Delivery Services é a solução preferida pela Adobe para criar uma loja. Consulte o documento [Introdução e visão geral](/help/commerce-cloud/introduction.md) para obter mais informações.

## Integração {#onboarding}

A integração do AEM Commerce as a Cloud Service é um processo de duas etapas:

1. Habilitação do AEM Commerce as a Cloud Service e provisionamento do complemento CIF
1. Conectar o AEM Commerce as a Cloud Service com sua solução comercial

A primeira etapa de integração é realizada pela Adobe. Para obter mais detalhes sobre preços e provisionamento, entre em contato com seu representante de vendas.

Depois de provisionado com o complemento CIF, ele é aplicado a todos os programas Cloud Manager existentes. Caso não tenha um Programa Cloud Manager, é necessário criar um. Para obter mais detalhes, consulte [Configurar o programa.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html?lang=pt-BR)

A segunda etapa é o autoatendimento para cada ambiente do AEM as a Cloud Service. Há algumas configurações adicionais que você deve fazer após o provisionamento inicial do complemento CIF.

## Conectar o AEM com uma solução da Commerce {#solution}

Para conectar o complemento CIF e os [Componentes principais do AEM CIF](https://github.com/adobe/aem-core-cif-components) com uma solução comercial, você deve fornecer a URL do ponto de extremidade do GraphQL por meio de uma variável de ambiente do Cloud Manager. O nome da variável é `COMMERCE_ENDPOINT`. Deve ser configurada uma conexão segura por meio de HTTPS.

Essa variável de ambiente é usada em dois lugares:

* Chamadas de GraphQL do AEM para o back-end de comércio, por meio de algum cliente GraphQl compartilhável comum, usado pelos Componentes principais do AEM CIF e componentes do projeto do cliente.
* Configure uma URL de proxy GraphQL em cada ambiente AEM para o qual a variável esteja disponível em `/api/graphql`. Esse URL é usado pelas ferramentas de criação do AEM Commerce (complemento do CIF) e pelos componentes do cliente do CIF.

Um URL de endpoint do GraphQL diferente pode ser usado para cada ambiente AEM as a Cloud Service. Dessa forma, os projetos podem conectar ambientes de preparo do AEM a sistemas de preparo de comércio e o ambiente de produção do AEM a um sistema de produção de comércio. Esse endpoint do GraphQL deve estar disponível publicamente. Não há suporte para VPN privada ou conexões locais. Opcionalmente, um cabeçalho de autenticação pode ser fornecido para usar recursos adicionais do CIF que exigem autenticação.

Opcionalmente e somente para o Adobe Commerce Enterprise/Cloud, o complemento CIF é compatível com o uso de dados de catálogo preparados para autores do AEM. Esses dados exigem a configuração de um cabeçalho de autorização. Esse cabeçalho só está disponível e é usado em instâncias do AEM Author por motivos de segurança. As instâncias de Publicação do AEM não podem mostrar dados preparados.

Há duas opções para configurar o endpoint:

### Por meio da interface do usuário do Cloud Manager (padrão) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Essa configuração pode ser feita usando uma caixa de diálogo na página Detalhes do ambiente. Ao visualizar esta página para um programa habilitado para Commerce, um botão será exibido se o endpoint não estiver configurado no momento:

![Informações de Ambiente de CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

Clicar nesse botão abre uma caixa de diálogo:

![Ponto de Extremidade do Commerce](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png) CM

Depois que o ponto de extremidade e, opcionalmente, um cabeçalho de autorização para suporte ao catálogo em etapas forem definidos, o ponto de extremidade será exibido na página de detalhes. Clicar no ícone Editar para abrir a mesma caixa de diálogo, na qual você pode editar o endpoint, se necessário.

![Informações de Ambiente de CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### Por meio da CLI do Adobe I/O  {#adobe-cli}

Para conectar o AEM a uma solução comercial por meio da CLI do Adobe I/O, siga estas etapas:

1. Obtenha a CLI do Adobe I/O com o plug-in do Cloud Manager.

   * Verifique a [documentação do Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/introduction.html?lang=pt-BR) sobre como baixar, configurar e usar a [CLI do Adobe I/O](https://github.com/adobe/aio-cli) com o [plug-in do Cloud Manager CLI.](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. Autentique a Adobe I/O CLI com o programa AEM as a Cloud Service.

1. Defina a variável `COMMERCE_ENDPOINT` no Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * Consulte [documentos da CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para saber mais.

   * O URL do ponto de extremidade de GraphQL de comércio deve apontar para o serviço GraphQl do comércio e usar uma conexão HTTPS segura. Por exemplo: `https://<yourcommercesystem>/graphql`.

1. Habilitar recursos de catálogo em etapas que exigem autenticação (Opcional).

   >[!NOTE]
   >
   >Esse recurso só está disponível com o Adobe Commerce Enterprise ou Cloud Edition. Consulte [Autenticação baseada em token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obter detalhes.

   * Defina a variável secreta `COMMERCE_AUTH_HEADER` no Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Você pode listar todas as variáveis do Cloud Manager usando o seguinte comando para verificar: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Você está pronto para usar o AEM Commerce as a Cloud Service e pode implantar seu projeto por meio do Cloud Manager.

## Configuração de lojas e catálogos {#catalog}

O complemento CIF e os [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components) podem ser usados em várias estruturas de site do AEM conectadas a diferentes lojas de comércio (ou exibições de loja e assim por diante). Por padrão, o complemento CIF é implantado com uma configuração padrão conectada à loja e ao catálogo padrão da Adobe Commerce.

Essa configuração pode ser ajustada para o projeto por meio da configuração do CIF Cloud Service seguindo estas etapas:

1. No AEM, acesse Ferramentas > Serviços da nuvem > Configuração do CIF.

1. Selecione a configuração de comércio que deseja alterar.

1. Abra as propriedades de configuração por meio da barra de ações.

![Configuração do CIF Cloud Services](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

As seguintes propriedades podem ser configuradas:

* Cliente GraphQL - selecione o cliente GraphQL configurado para comunicação de back-end de comércio. Normalmente, esse cliente deve permanecer no padrão.
* Exibição de loja - o identificador de exibição de loja. Se estiver vazia, a exibição de loja padrão será usada.
* Caminho de proxy do GraphQL - o caminho de URL que o Proxy da GraphQL no AEM usa para solicitações de proxy para o endpoint do GraphQL de back-end de comércio.

  >[!NOTE]
  >
  > Na maioria das configurações, o valor padrão `/api/graphql` não deve ser alterado. Somente a configuração avançada que não usa o proxy do GraphQL fornecido deve alterar essa configuração.

* Habilitar suporte ao UID do catálogo - habilite o suporte para o UID em vez da ID nas chamadas de GraphQL de back-end de comércio.

  >[!NOTE]
  >
  > O suporte para UIDs foi introduzido no Adobe Commerce 2.4.2. Habilite os UIDs somente se o back-end de comércio suportar um esquema do GraphQL versão 2.4.2 ou posterior.

* Identificador de categoria raiz do catálogo - o identificador (UID ou ID) da raiz do catálogo de armazenamento

  >[!CAUTION]
  >
  > A partir da versão 2.0.0 dos Componentes Principais do CIF, o suporte para `id` foi removido e substituído por `uid`. Se o seu projeto usar os Componentes principais do CIF versão 2.0.0, você deverá ativar o Suporte ao UID do catálogo e usar uma categoria válida do UID como &quot;Identificador de categoria raiz do catálogo&quot;.

A configuração mostrada acima serve como referência. Os projetos devem fornecer suas próprias configurações.

Para configurações mais complexas, usando várias estruturas de site do AEM combinadas com diferentes catálogos de comércio, consulte o tutorial [Configuração de várias lojas do Commerce](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md).

## Recursos adicionais {#additional-resources}

* [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Configuração de várias lojas do Commerce](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [Várias configurações de sistemas Commerce](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
