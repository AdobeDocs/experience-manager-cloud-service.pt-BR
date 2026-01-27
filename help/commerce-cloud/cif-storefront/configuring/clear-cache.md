---
title: Component & GraphQL Clear Cache
description: Saiba como ativar e verificar o recurso de cache limpo no AEM CIF.
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
index: false
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---


# Component &amp; GraphQL Clear Cache {#clear-cache}

Este documento fornece um guia abrangente sobre como ativar e verificar o recurso de cache limpo no AEM CIF.

>[!NOTE]
>
> Este recurso é experimental.

## Ativação do recurso Limpar cache na configuração do CIF {#enable-clear-cache}

Por padrão, o recurso de cache limpo é desativado na configuração do CIF. Para ativá-lo, é necessário adicionar o seguinte aos projetos correspondentes:

* Habilite o servlet `/bin/cif/invalidate-cache` que ajuda a acionar a API clear-cache com suas solicitações correspondentes adicionando a configuração `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` no projeto, como mostrado [aqui.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)

  >[!NOTE]
  >
  > A configuração precisa ser ativada somente para as instâncias do autor.

* Habilite o ouvinte a limpar o cache de cada instância do AEM (publicar e criar) adicionando a configuração `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` no seu projeto, como mostrado [aqui.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)
   * A configuração deve ser ativada para as instâncias do autor e de publicação.
   * Habilitar o cache do Dispatcher (Opcional): é possível habilitar a configuração limpar cache do dispatcher definindo a propriedade `enableDispatcherCacheInvalidation` como true na configuração acima. Isso fornece funcionalidade para limpar o cache do dispatcher.

     >[!NOTE]
     >
     > Isso só funciona com instâncias de publicação.

   * Além disso, certifique-se de fornecer o padrão correspondente que se adapta às necessidades de produto, categoria e página do CMS ao arquivo de configuração acima para removê-lo do cache do dispatcher.

* Para melhorar o desempenho das consultas SQL para encontrar a página correspondente relacionada ao produto e à categoria, adicione o índice correspondente em seu projeto (recomendado). Para obter mais informações, consulte [cifCacheInvalidationSupport.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml)

## Verificando o Recurso Limpar Cache {#verify-clear-cache}

Para verificar se tudo está configurado corretamente:

* Acione o servlet correspondente para a Instância de Autor do AEM, por exemplo [http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache), e você deve obter uma resposta HTTP 200.
* Verifique se um nó foi criado no seguinte caminho nas instâncias do autor: `/var/cif/cacheinvalidation`. O nome do nó segue este padrão: `cmd_{{timestamp}}`.
* Verifique se o mesmo nó foi criado em cada instância de publicação.

Agora, para verificar se os caches estão sendo limpos corretamente:

1. Navegue até as páginas PLP e PDP correspondentes.
2. Atualize um nome de produto ou categoria no mecanismo de comércio. As alterações não são refletidas no AEM imediatamente com base nas configurações de cache.
3. Acione a API do servlet conforme mostrado aqui:

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ******' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

Se tudo correr bem, as novas mudanças serão refletidas em todas as instâncias. Se as alterações não estiverem visíveis na instância de publicação, tente acessar as páginas PLP e PDP relevantes em uma janela do navegador privada/incógnita.

>[!NOTE]
>
> As instâncias de publicação podem ter vários níveis de camadas de cache. O recurso é responsável apenas pela limpeza do cache da memória interna e do Dispatcher do AEM.

## Limpar API de invalidação de cache {#clear-cache-api}

Essa é a API que você precisa acionar sempre que quiser limpar o cache de dados relacionados ao comércio do AEM.

Tipo de Solicitação: `POST`

### Cabeçalhos {#headers}

| Parâmetro | Valor | Obrigatório/obrigatório | Comentar |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | Obrigatório |  |
| `Authorization` | Credenciais de usuário do autor correspondente (Tipo de autenticação: autenticação básica) | Obrigatório | Adicione o nome de usuário e a senha correspondentes. |


### Conteúdo {#payload}

A tabela a seguir mostra os atributos existentes que o recurso está fornecendo prontos para uso. Essas propriedades `InvalidateType` precisam ser fornecidas em combinação com o atributo obrigatório (como `storePath`).

| `invalidateType` | Valor | Tipo (Matriz/String/Booleano) | Isso limpará o cache do dispatcher? | Comentar |
|------------------------------|-------------------|---|---|---|
| `productSkus` | SKU do produto - que precisa ser invalidado do cache. | Matriz | Sim | Limpar o cache da memória interna usando o seguinte padrão:<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>Limpar o cache de página PDP dos SKUs correspondentes</li><li>Limpar o cache da página de categorias correspondente na qual eles existem (com base na resposta do graphql do comércio)</li><li>Limpar cache com base na seguinte consulta:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | UID da categoria - que precisa ser invalidada do cache. | Matriz | Sim | Limpar o cache da memória interna usando o seguinte padrão:<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>Limpar o cache de páginas de categoria para os dados correspondentes (incluindo sua página de categoria secundária)</li><li>Limpar todas as páginas PDP que têm as categorias correspondentes</li><li>Limpar cache com base na seguinte consulta:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | Se você precisar limpar os dados de resposta do GraphQL com base no padrão regex, use isso. | Matriz | Não | |
| `cacheNames` | Esses valores são definidos na correspondente fábrica de configuração de cliente do CIF GraphQL >> Configuração de GraphQL do StorePath correspondente >> Configurações de cache do GraphQL | Matriz | Não | |
| `invalidateAll` | Verdadeiro ou falso | Booleano | Sim | |

Esta tabela mostra a propriedade obrigatória que precisa ser passada em cada chamada de API:

| Propriedade | Valor | Tipo (Matriz/String/Booleano) | Isso limpará o cache do dispatcher? | Comentar |
|------------------------------|-------------------|---|---|---|
| `storePath` | Valor correspondente do caminho do site de onde o cache precisa ser removido (Exemplo: `/content/venia/us/en` como referência com o projeto venia). | String | Sim | Isto precisa ser fornecido com a combinação de `invalidateType.` |

### Solicitação de API de exemplo {#sample-request}

```text
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ******' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## Extensibilidade {#clear-cache-extensibility}

Esse recurso não só fornece sua funcionalidade principal, como também oferece extensibilidade, permitindo que os desenvolvedores criem e personalizem ainda mais, conforme necessário.

### Extensão do atributo existente {#existing-attribute}

Nos casos em que o cache precisa ser limpo e que não estão cobertos atualmente pela funcionalidade baseada em atributos existente (como `categoryUids`), você pode consultar [este arquivo de referência](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java) para adicionar novos padrões e definir `invalidatePaths` adicionais que devem ser limpos do cache além do que a implementação atual lida.

### Adicionar novo atributo personalizado {#new-custom-attribute}

Se, por exemplo, você não quiser usar o atributo existente para limpar o cache, terá a flexibilidade de criar seu próprio atributo e definir sua funcionalidade correspondente.

* Se você precisar apenas limpar o cache da memória interna do AEM (a resposta graphql), será necessário seguir [esta referência.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java)
* Se você precisar limpar o cache da memória interna e do cache do Dispatcher, siga [esta referência.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java)

  >[!NOTE]
  >
  > Você pode ignorar a limpeza interna do cache retornando `null` para o método `getPatterns()`.
