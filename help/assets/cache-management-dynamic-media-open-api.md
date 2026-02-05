---
title: Gerenciamento de cache no Dynamic Media com APIs abertas
description: Gerenciamento de cache no Dynamic Media com APIs abertas
role: User
source-git-commit: 89f21f96a741acbd6458c3777227548fbc89e525
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Gerenciamento de cache no Dynamic Media com APIs abertas {#cache-management-dynamic-media-open-apis}

O gerenciamento eficiente do cache é essencial para o fornecimento de ativos digitais de alto desempenho, dimensionáveis e atualizados. No Dynamic Media com APIs abertas, o gerenciamento de cache define como o conteúdo é armazenado, atualizado e entregue nas várias camadas do pipeline de entrega. As respostas da entrega de ativos são armazenadas em cache em várias camadas para garantir o desempenho ideal e a entrega rápida de conteúdo.

O cache prolongado no Dynamic Media com APIs abertas consiste em [Cache de Camada CDN](#cdn-layer-caching) e [Controle de Cache Externo (BYOCDN e Cache de Navegador)](#byocdn-browser-caching).

## Armazenamento em cache da camada CDN {#cdn-layer-caching}

As respostas da entrega de ativos são armazenadas em cache na [CDN Gerenciada pela Adobe](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn) por um período estendido para maximizar o desempenho e minimizar a carga na origem. Esse armazenamento em cache é totalmente gerenciado pela Adobe para garantir uma experiência de alta qualidade consistente para os usuários finais. A duração do cache é intencionalmente otimizada para desempenho e não pode ser personalizada pelos usuários para manter a confiabilidade e a entrega eficiente do conteúdo em todos os clientes.

Todos os URLs de entrega são armazenados em cache na borda do (Fastly) por um período estendido para garantir o desempenho ideal. Os objetos do delivery em cache incluem representações estáticas, vídeos, binários de imagem original e imagens transformadas dinamicamente, como ativos redimensionados ou reformatados gerados por meio de parâmetros de URL. <!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## Controle de cache externo (BYOCDN e cache do navegador) {#byocdn-browser-caching}

As respostas de entrega de ativos incluem um cabeçalho `Cache-Control` com um padrão de `max-age` de **10 minutos** para camadas de cache downstream. Isso se aplica às *configurações personalizadas BYOCDN (Bring-Your-Own-CDN)*, *navegadores de usuário final* e qualquer *proxy de cache intermediário*, garantindo um controle de cache consistente em todo o caminho de entrega.

### Personalizando Cabeçalhos de Controle de Cache {#customizing-cache-control-headers}

Aumentar o tempo de cache para valores ativos além da configuração padrão aumenta a probabilidade de veicular conteúdo obsoleto, o que pode atrasar a visibilidade das atualizações de conteúdo na experiência do usuário final. Se você precisar modificar o comportamento do controle de cache para seu caso de uso específico, poderá configurar regras de CDN personalizadas para ajustar cabeçalhos de resposta. Isso permite que você defina diferentes durações de cache com base em seus requisitos. Consulte [Regras personalizadas de CDN da AEM para cabeçalhos de resposta](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic).

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

Para obter assistência adicional ou fazer perguntas sobre o gerenciamento de cache, entre em contato com o [Suporte da Adobe](https://helpx.adobe.com/in/contact.html).

## Invalidação de cache ativo {#active-cache-invalidation}

Sempre que um ativo é atualizado, excluído ou modificado (qualquer alteração nos metadados), o Dynamic Media com APIs abertas invalida automaticamente cada URL de entrega associado no Adobe Managed CDN. Isso se aplica a URLs que usam IDs personalizadas ou aliases, juntamente com quaisquer URLs que incluam parâmetros de transformação, como largura, formato ou qualidade. Essa invalidação orientada por eventos garante que seus usuários sempre recebam a versão mais recente de seus ativos sem intervenção manual.

### Limpeza manual de cache {#manual-cache-purging}

Quando houver necessidade de limpar manualmente o conteúdo em cache, você poderá fazer isso usando os recursos de invalidação de cache do AEM. Para obter instruções detalhadas sobre como limpar URLs de cache específicos, consulte [Invalidação de cache do AEM CDN](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge).

## Perguntas frequentes{#faq-cache-management}

+++**Como o gerenciamento de cache afeta as integrações existentes?**

As URLs de ativos permanecem inalteradas, e o cabeçalho de controle de cache enviado aos navegadores (e a outros intermediários downstream) da CDN gerenciada pela Adobe continua sendo de 10 minutos com um [`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean), garantindo que os sistemas downstream continuem aproveitando seus caches de maneira ideal.

+++

+++**O que aciona uma limpeza de cache?**

A limpeza do cache é acionada automaticamente quando um ativo é atualizado, modificado, arquivado ou excluído.

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **Quais tipos de ativos são suportados para o armazenamento em cache de longa duração?**

O armazenamento em cache prolongado com invalidação de cache ativo orientada por evento se aplica a todos os tipos de ativos no Dynamic Media com APIs abertas, independentemente do tipo ou formato do ativo.

+++

+++ **Posso recusar o armazenamento em cache de longa duração do meu repositório?**

Você pode entrar em contato com o [Suporte da Adobe](https://helpx.adobe.com/in/contact.html) explicando a lógica, e a Adobe entrará em contato com você para discussão.

+++


>[!MORELIKETHIS]
>
>- [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>- [URLs personalizados](/help/assets/vanity-urls.md)
