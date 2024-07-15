---
title: Mapeamento de recursos
description: Saiba como definir redirecionamentos, URLs personalizados e hosts virtuais para AEM usando o mapeamento de recursos.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Mapeamento de recursos{#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizados e hosts virtuais para AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixe todas as solicitações com `/content` para que a estrutura interna fique oculta dos visitantes do seu site.
* Defina um redirecionamento para que todas as solicitações para a página `/content/en/gateway` do seu site sejam redirecionadas para `https://gbiv.com/`.

Um mapeamento HTTP possível prefixa todas as solicitações a `localhost:4503` com `/content`. Um mapeamento como esse pode ser usado para ocultar a estrutura interna dos visitantes do site, pois permite:

`localhost:4503/content/we-retail/en/products.html`

Para ser acessado usando:

`localhost:4503/we-retail/en/products.html`

Como o mapeamento adiciona automaticamente o prefixo `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>URLs personalizados não são compatíveis com padrões regex.

>[!NOTE]
>
>Consulte a documentação do Sling e os [Mapeamentos para Resolução de Recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) e [Recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para obter mais informações.

## Exibição de Definições de Mapeamento {#viewing-mapping-definitions}

Os mapeamentos formam duas listas que o JCR Resource Resolver avalia (de cima para baixo) para encontrar uma correspondência.

Essas listas podem ser exibidas (juntamente com informações de configuração) na opção **JCR ResourceResolver** do console Felix; por exemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuração
Mostra a configuração atual (conforme definido para o [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map)).

* Teste de configuração
Isso permite inserir um URL ou um caminho de recurso. Clique em **Resolver** ou **Mapear** para confirmar como o sistema transforma a entrada.

* **Entradas do Mapa de Resolução**
A lista de entradas usadas pelos métodos ResourceResolver.resolve para mapear URLs para Recursos.

* **Mapeando Entradas do Mapa**
A lista de entradas usadas pelos métodos ResourceResolver.map para mapear Caminhos de Recursos para URLs.

As duas listas mostram várias entradas, incluindo aquelas definidas como padrão pelas aplicações. Essas entradas geralmente têm como objetivo simplificar URLs para o usuário.

As listas emparelham um **Padrão**, uma expressão regular que corresponde à solicitação, com uma **Substituição** que define o redirecionamento a ser imposto.

Por exemplo, o:

**Padrão** `^[^/]+/[^/]+/welcome$`

Aciona o:

**Substituição** `/libs/cq/core/content/welcome.html`.

Para redirecionar uma solicitação:

`https://localhost:4503/welcome`

Para:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Novas definições de mapeamento são criadas no repositório.

>[!NOTE]
>
>Há muitos recursos disponíveis que ajudam a explicar como definir expressões regulares. Por exemplo, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Criação de definições de mapeamento no AEM {#creating-mapping-definitions-in-aem}

Em uma instalação padrão do AEM, você pode encontrar a pasta:

`/etc/map/http`

Essa pasta é a estrutura usada ao definir mapeamentos para o protocolo HTTP. Outras pastas ( `sling:Folder`) podem ser criadas em `/etc/map` para qualquer outro protocolo que você queira mapear.

#### Configuração de um redirecionamento interno para /content {#configuring-an-internal-redirect-to-content}

Para criar o mapeamento que prefixa qualquer solicitação para https://localhost:4503/ com `/content`:

1. Usando o CRXDE, navegue até `/etc/map/http`.

1. Criar um nó:

   * **Tipo** `sling:Mapping`
Esse tipo de nó se destina a esses mapeamentos, embora seu uso não seja obrigatório.

   * **Nome** `localhost_any`

1. Clique em **Salvar tudo**.
1. **Adicione** as seguintes propriedades a este nó:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`

   * **Nome** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor** `/content/`

1. Clique em **Salvar tudo**.

Esse mapeamento lida com uma solicitação como:
`localhost:4503/geometrixx/en/products.html`
como se:
`localhost:4503/content/geometrixx/en/products.html`
foi solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) na Documentação do Sling para obter mais informações sobre as propriedades do sling disponíveis e como elas podem ser configuradas.
>Por exemplo, a [Interpolação de cadeia de caracteres](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) é útil porque permite configurar um mapeamento que obtém valores por ambiente por meio de variáveis de ambiente.

>[!NOTE]
>
>Você pode usar `/etc/map.publish` para manter as configurações para o ambiente de publicação. Essas configurações devem ser replicadas e o novo local ( `/etc/map.publish`) configurado para o **Local de Mapeamento** do [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) do ambiente de publicação.
