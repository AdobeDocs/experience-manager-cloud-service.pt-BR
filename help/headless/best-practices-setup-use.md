---
title: Práticas recomendadas para a configuração e uso do AEM GraphQL com fragmentos de conteúdo
description: Conheça as Práticas recomendadas para a configuração e uso do AEM GraphQL com Fragmentos de conteúdo.
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 23%

---

# Práticas recomendadas para a configuração e uso do AEM GraphQL com fragmentos de conteúdo{#best-practices-setup-use-aem-graphql-content-fragments}

Estas diretrizes resumem as práticas recomendadas para instalar, configurar e usar o AEM com GraphQL e Fragmentos de conteúdo.

## Introdução {#getting-started}

Para ajudar você a se atualizar:

* [O que é Headless?](/help/headless/what-is-headless.md)
* Uma visão geral dos vários ambientes na [Arquitetura](/help/headless/deployment/architecture.md) do AEM

## Configurar {#setup}

Para configurar com segurança o AEM GraphQL para uso com Fragmentos de conteúdo e seus aplicativos, é necessário configurar vários componentes.

### Criação de endpoint do GraphQL (incluindo segurança) {#graphql-endpoint-creation}

O endpoint é o caminho usado para acessar o GraphQL no AEM. Esses endpoints precisam ser criados e publicados para que possam ser acessados com segurança.

#### Detalhes {#details-graphql-endpoint-creation}

[Gerenciar endpoints de GraphQL no AEM](/help/headless/graphql-api/graphql-endpoint.md)

#### Ambientes {#environments-graphql-endpoint-creation}

Os endpoints precisam ser configurados em:

* Autor
* Visualização
* Publicação

Para:

* Desenvolvimento
* Testes
* Produção

### Armazenamento em cache do AEM Dispatcher {#dispatcher-caching}

>[!NOTE]
>Se o cache na Dispatcher estiver habilitado, a [configuração do CORS](#cors-setup) não será necessária e, portanto, poderá ser ignorada.

O armazenamento em cache de consultas persistentes não é ativado por padrão no Dispatcher. A ativação padrão não é possível, pois os clientes que usam o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) precisam revisar e possivelmente atualizar a configuração do Dispatcher.

#### Detalhes {#details-dispatcher-caching}

[Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Ambientes {#environments-dispatcher-caching}

Normalmente, o Dispatcher é configurado para:

* Publicar: produção

### Configuração do CORS {#cors-setup}

>[!NOTE]
>Se o armazenamento em cache no [AEM Dispatcher](#dispatcher-caching) estiver habilitado, a configuração do CORS não será necessária e, portanto, esta seção poderá ser ignorada.

Para acessar o endpoint do GraphQL, uma política do CORS deve ser configurada e adicionada a um projeto do AEM que esteja implantado no AEM via Cloud Manager. Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados.

#### Detalhes {#details-cors-setup}

[Configuração do Compartilhamento de recursos entre origens (CORS)](/help/headless/deployment/cross-origin-resource-sharing.md)

#### Ambientes {#environments-cors-setup}

Normalmente, o CORS é configurado para:

* Publicar: produção

### Autenticação {#authentication}

Um caso de uso fundamental para a entrega de fragmentos de conteúdo da API do GraphQL do Adobe Experience Manager as a Cloud Service (AEM) é o de aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticado para garantir a entrega de conteúdo headless.

#### Detalhes {#details-authentication}

[Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo](/help/headless/security/authentication.md)

#### Ambientes {#environments-authentication}

Normalmente, a autenticação é configurada para:

* Visualização
* Publicação

Para:

* Desenvolvimento
* Testes
* Produção

### Permissões {#permissions}

Com uma implementação headless, há várias áreas de segurança e permissões que devem ser abordadas. As permissões e os perfis podem ser amplamente considerados com base no **Autor** ou **Publicação** de ambiente do AEM. Cada ambiente contém perfis diferentes e com necessidades diferentes.

#### Detalhes {#details-permissions}

[Considerações de permissão para conteúdo headless](/help/headless/security/permissions.md)

#### Ambientes {#environments-permissions}

As permissões geralmente são configuradas para:

* Autor
* Visualização
* Publicação

Para:

* Desenvolvimento
* Testes
* Produção

### Usar uma rede de entrega de conteúdo (CDN) {#cdn}

As consultas do GraphQL e suas respostas JSON podem ser armazenadas em cache se direcionadas como solicitações `GET` ao usar um CDN. Por outro lado, as solicitações não armazenadas em cache podem ser muito caras (recursos) e de processamento lento, com potencial para efeitos prejudiciais adicionais nos recursos da origem.

#### Detalhes {#details-cdn}

[CDN no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md)

#### Ambientes {#environments-cdn}

Uma CDN geralmente é configurada para:

* Publicar: produção

### Configurar e criar fragmentos de conteúdo {#cconfigure-create-content-fragments}

O AEM GraphQL é usado para recuperar informações dos fragmentos de conteúdo. Eles precisam ser configurados e, em seguida, uma estrutura e um local definidos para que você possa criar o conteúdo.

#### Detalhes {#details-content-fragments}

* [Criar uma configuração](/help/headless/setup/create-configuration.md)
* [Criar um modelo de fragmento de conteúdo](/help/headless/setup/create-content-model.md)
* [Criar uma pasta do Assets](/help/headless/setup/create-assets-folder.md)
* [Criar e editar os fragmentos de conteúdo](/help/headless/setup/create-content-fragment.md)

#### Ambientes {#eenvironments-content-fragments}

Os fragmentos de conteúdo são definidos, criados, testados, publicados e acessados em:

* Autor
* Visualização
* Publicação

Para:

* Desenvolvimento
* Testes
* Produção

## Utilização do AEM GraphQL {#use-aem-graphql}

### Otimizar as consultas do GraphQL {#optimize-graphql-queries}

Essas diretrizes são fornecidas para ajudar a evitar problemas de desempenho com as consultas do GraphQL.

#### Detalhes {#details-optimize-graphql-queries}

[Otimização de consultas de GraphQL](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>As diretrizes de otimização abrangem a configuração de cache, já abordada em [Configuração](#setup).

### Acessar o GraphQL pelos seus aplicativos {#access-graphql-from-your-apps}

O AEM headless CMS oferece aos desenvolvedores a liberdade de criar e fornecer experiências excepcionais usando as linguagens, estruturas e ferramentas com as quais já estão familiarizados.

#### Detalhes {#details-your-apps}

* [Instalar e usar o AEM SDK para desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=pt-BR)
* [Recursos do desenvolvedor sem periféricos do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* Exemplos, incluindo [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html), [Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html), [Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html), entre outros

#### Ambientes {#environments-your-apps}

Normalmente, os aplicativos são desenvolvidos, testados e usados em:

* Visualização
* Publicação

Para:

* Desenvolvimento
* Testes
* Produção

### Recursos adicionais

Para obter mais detalhes sobre o AEM GraphQL e os fragmentos de conteúdo, consulte o seguinte:

* [API GraphQL do AEM para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
* [Uso do GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [Recursos do desenvolvedor sem periféricos do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
