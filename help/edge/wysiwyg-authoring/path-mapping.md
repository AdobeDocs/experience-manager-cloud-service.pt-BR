---
title: Mapeamento de caminho para o Edge Delivery Services
description: Saiba como mapear caminhos de página usados na instância de criação do AEM para caminhos de página públicos usados no site e controlar qual conteúdo é publicado no Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Mapeamento de caminho para o Edge Delivery Services {#path-mapping}

Saiba como mapear caminhos de página usados na instância de criação do AEM para caminhos de página públicos usados no site e controlar qual conteúdo é publicado no Edge Delivery Services.

## Visão geral {#overview}

Para criar conteúdo do WYSIWYG usando o AEM e publicá-lo no Edge Delivery Services, você deve configurar o mapeamento de caminho do projeto. Esse mapeamento tem dois propósitos.

* Ele mapeia e cria uma relação entre os caminhos de página usados na instância de criação do AEM e os caminhos de página pública usados no site.
* Ele controla qual conteúdo (páginas, planilhas, ativos, etc.) são publicados no Edge Delivery Services.

O mapeamento de caminho deve ser configurado para cada projeto individualmente e de acordo com o conteúdo do projeto e a estrutura de URL. Ele é usado pelo AEM durante a publicação de conteúdo e durante a edição de conteúdo no [Editor Universal](/help/sites-cloud/authoring/universal-editor/navigation.md).

## Formato de configuração {#configuration-format}

O formato da configuração de mapeamento de caminho contém duas seções (`mappings` e `includes`) semelhantes ao exemplo a seguir.

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### mapeamentos {#mappings}

A configuração `mappings` contém uma matriz de caminhos internos (na instância de criação do AEM) e caminhos de URL externos (no site público).

O formato é `<internal paths>:<external path>`. Normalmente consiste em um mínimo de duas entradas.

1. A primeira entrada do exemplo é o mapeamento de caminho das páginas do site.
1. A segunda entrada controla o mapeamento de `.helix/config.json` para a página da planilha correspondente no repositório de criação do AEM.

Neste exemplo, todas as páginas armazenadas em `/content/aem-boilerplate/...` estarão publicamente acessíveis no site do Edge Delivery Services diretamente em `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Todos os dados em tabelas gerenciados como planilhas (por exemplo, metadados, redirecionamentos e taxonomia) normalmente são publicados como URLs de API `.json` no Edge Delivery Services. Para fazer isso, eles devem ser listados individualmente na configuração de mapeamento.
>
>Consulte o documento [Usando Planilhas para Gerenciar Dados Tabulares](/help/edge/wysiwyg-authoring/tabular-data.md) para obter mais informações.

### inclui {#includes}

A configuração `includes` controla quais caminhos de conteúdo são realmente replicados para o Edge Delivery Services. Ela também pode conter qualquer matriz de caminhos e geralmente contém a página raiz de nível superior dos sites.

O Assets usado nas páginas do Edge Delivery Services normalmente é publicado junto com a página da Web. Eles serão exportados automaticamente da instância de criação do AEM para o Edge Delivery Services.

>[!TIP]
>
>Se você tiver um caso de uso em que deseja que os ativos sejam publicados diretamente no Edge Delivery Services (por exemplo, gostaria que as imagens ou os PDFs fossem diretamente acessíveis pelos URLs fora de um contexto de página), também deverá adicionar os caminhos DAM à seção `includes` da configuração.
>
>Por exemplo, se uma pasta raiz de ativo, como `/content/dam/my-site/documents`, que contém um conjunto de PDF, estiver acessível publicamente por meio de `/assets/...`, uma entrada deverá ser adicionada à seção `includes` da configuração.

## Como configurar {#how-to-configure}

Os mapeamentos de caminho podem ser configurados de uma das duas formas a seguir, dependendo da configuração do projeto.

1. Se o projeto estiver configurado para `aem.live` e usar o [serviço de configuração](https://www.aem.live/docs/config-service-setup) para configurações centralizadas, o mapeamento de caminhos para cada site será configurado por meio desse serviço de configuração.

   * Este é um exemplo de solicitação cURL para configurar mapeamentos de caminho.

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. Se o projeto não usar o serviço de configuração, o mapeamento de caminhos será configurado por meio de um arquivo `paths.json` no repositório GitHub dos projetos.

   * Veja [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) para ver um exemplo.

Em ambos os casos, depois de configurar os mapeamentos de caminho, você poderá verificar a configuração por meio da URL de configuração acessível publicamente `https://<branch>--<site>--<org>.aem.page/config.json`.
