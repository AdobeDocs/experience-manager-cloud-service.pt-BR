---
title: Mapeamento de recursos
description: Saiba como definir redirecionamentos, URLs personalizadas e hosts virtuais para AEM usando o mapeamento de recursos.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---

# Mapeamento de recursos{#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizadas e hosts virtuais para AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixar todas as solicitações com `/content` para que a estrutura interna fique oculta dos visitantes do seu site.
* Defina um redirecionamento para que todas as solicitações da variável `/content/en/gateway` página do seu site são redirecionadas para `https://gbiv.com/`.

Um possível mapeamento HTTP prefixa todas as solicitações para `localhost:4503` com `/content`. Um mapeamento como esse pode ser usado para ocultar a estrutura interna dos visitantes do site, conforme permite:

`localhost:4503/content/we-retail/en/products.html`

a ser acessado usando:

`localhost:4503/we-retail/en/products.html`

como o mapeamento adicionará automaticamente o prefixo `/content` para `/we-retail/en/products.html`.

>[!CAUTION]
>
>URLs personalizadas não suportam padrões regex.

>[!NOTE]
>
>Consulte a documentação do Sling e [Mapeamentos para Resolução de Recursos](https://sling.apache.org/site/resources.html) e [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) para obter mais informações.

## Exibindo Definições de Mapeamento {#viewing-mapping-definitions}

Os mapeamentos de duas listas que o Resolvedor de Recursos do JCR avalia (de cima para baixo) para encontrar uma correspondência.

Essas listas podem ser visualizadas (junto com informações de configuração) no **JCR ResourceResolver** opção do console Felix; por exemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuração Mostra a configuração atual (conforme definido para a variável [Resolvedor de Recursos do Apache Sling](/help/overview/seo-and-url-management.md#etc-map)).

* Teste de configuração Permite inserir um URL ou caminho de recurso. Clique em **Resolver** ou **Mapa** para confirmar como o sistema transformará a entrada.

* **Entradas do Mapa do Resolvedor**
A lista de entradas usadas pelos métodos ResourceResolver.resolve para mapear URLs para Recursos.

* **Mapeamento de entradas do mapa**
A lista de entradas usadas pelos métodos ResourceResolver.map para mapear Caminhos de Recursos para URLs.

As duas listas mostram várias entradas, incluindo as definidas como padrões pelo(s) aplicativo(s). Geralmente, o objetivo é simplificar os URLs para o usuário.

As listas emparelham um **Padrão**, uma expressão regular correspondente à solicitação, com um **Substituição** que define o redirecionamento a ser imposto.

Por exemplo, o:

**Padrão** `^[^/]+/[^/]+/welcome$`

acionará o:

**Substituição** `/libs/cq/core/content/welcome.html`.

para redirecionar uma solicitação:

`https://localhost:4503/welcome` ``

para:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Novas definições de mapeamento são criadas no repositório.

>[!NOTE]
>
>Há muitos recursos disponíveis que ajudam a explicar como definir expressões regulares; por exemplo [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Criando definições de mapeamento no AEM {#creating-mapping-definitions-in-aem}

Em uma instalação padrão de AEM, você pode encontrar a pasta:

`/etc/map/http`

Essa é a estrutura usada ao definir mapeamentos para o protocolo HTTP. Outras pastas ( `sling:Folder`) pode ser criada em `/etc/map` para quaisquer outros protocolos que você queira mapear.

#### Configurar um redirecionamento interno para /content {#configuring-an-internal-redirect-to-content}

Para criar o mapeamento que prefixa qualquer solicitação para https://localhost:4503/ com `/content`:

1. Usando o CRXDE, navegue até `/etc/map/http`.

1. Crie um novo nó:

   * **Tipo** `sling:Mapping`
Esse tipo de nó é destinado a esses mapeamentos, embora seu uso não seja obrigatório.

   * **Nome** `localhost_any`

1. Clique em **Salvar tudo**.
1. **Adicionar** as seguintes propriedades desse nó:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`
   * **Nome** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor** `/content/`


1. Clique em **Salvar tudo**.

Isso lidará com uma solicitação como:
`localhost:4503/geometrixx/en/products.html`
como se:
`localhost:4503/content/geometrixx/en/products.html`
tinham sido solicitados.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) na Documentação do Sling para obter mais informações sobre as propriedades do sling disponíveis e como elas podem ser configuradas.
>Por exemplo, [Interpolação de cadeia de caracteres](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) é muito útil, pois permite configurar um mapeamento que obtém valores por ambiente por meio de variáveis de ambiente.

>[!NOTE]
>
>Você pode usar `/etc/map.publish` para manter as configurações do ambiente de publicação. Eles devem então ser replicados e o novo local ( `/etc/map.publish`) configurado para o **Localização do mapeamento** do [Resolvedor de Recursos do Apache Sling](/help/overview/seo-and-url-management.md#etc-map) do ambiente de publicação.
