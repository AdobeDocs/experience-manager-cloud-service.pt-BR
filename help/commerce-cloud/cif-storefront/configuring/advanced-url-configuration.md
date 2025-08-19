---
title: Configurações avançadas de URL
description: Saiba como personalizar os URLs das páginas de produto e categoria. A personalização permite que as implementações otimizem URLs para mecanismos de pesquisa e promovam a descoberta.
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 9%

---


# Configurações avançadas de URL {#url}

>[!NOTE]
>
> A Otimização do mecanismo de pesquisa (SEO) se tornou uma preocupação principal para muitos comerciantes. Como resultado, as preocupações com a SEO devem ser abordadas em muitos projetos no Adobe Experience Manager (AEM) as a Cloud Service. Consulte [Práticas recomendadas de gerenciamento de SEO e URL](/help/overview/seo-and-url-management.md) para obter mais informações.

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem configurações avançadas para personalizar os URLs das páginas de produto e categoria. Muitas implementações personalizam esses URLs para fins de otimização de mecanismo de pesquisa (SEO). O vídeo a seguir mostra detalhes sobre como configurar o serviço `UrlProvider` e os recursos do [Mapeamento do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o serviço `UrlProvider` de acordo com os requisitos e necessidades de SEO, um projeto deve fornecer uma configuração OSGi para a _configuração do Provedor de URL da CIF_.

>[!NOTE]
>
> Desde a versão 2.0.0 dos Componentes principais do AEM CIF, a configuração do Provedor de URL fornece apenas formatos de URL predefinidos, em vez dos formatos configuráveis de texto livre conhecidos das versões 1.x. Além disso, o uso de seletores para transmitir dados em URLs foi substituído por sufixos.

### Formato do URL da página do produto {#product}

Configura os URLs das páginas de produtos e oferece suporte às seguintes opções:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (default)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Se houver a [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` foi substituído por `/content/venia/us/en/products/product-page`
* `{{sku}}` é substituído pelo SKU do produto, por exemplo, `VP09`
* `{{url_key}}` é substituído pela propriedade `url_key` do produto, por exemplo, `lenora-crochet-shorts`
* `{{url_path}}` é substituído pelo `url_path` do produto, por exemplo, `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` foi substituída pela variante selecionada no momento, por exemplo, `VP09-KH-S`

Como o `url_path` foi descontinuado, os formatos predefinidos de URL de produto usam o `url_rewrites` de um produto e escolhem aquele com mais segmentos de caminho como alternativa se o `url_path` não estiver disponível.

Com os dados de exemplo acima, uma URL de variante de produto formatada usando o formato de URL padrão se parece com `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato do URL da página de categoria {#product-list}

Configura os URLs das páginas de categoria ou lista de produtos e oferece suporte às seguintes opções:

* `{{page}}.html/{{url_path}}.html` (default)
* `{{page}}.html/{{url_key}}.html`

Se houver a [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` foi substituído por `/content/venia/us/en/products/category-page`
* `{{url_key}}` é substituído pela propriedade `url_key` da categoria
* `{{url_path}}` é substituído pelo `url_path` da categoria

Com os dados de exemplo acima, uma URL de página de categoria formatada usando o formato de URL padrão se parece com `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> O `url_path` é uma concatenação do `url_keys` dos ancestrais de um produto ou categoria e o `url_key` do produto ou categoria separado por uma barra `/`. Cada `url_key` é considerado único em um determinado armazenamento.

### Configuração específica do armazenamento {#store-specific-urlformats}

Os formatos de categoria e de URL de página de produto em todo o sistema definidos pela _configuração do Provedor de URL da CIF_ podem ser alterados para cada loja.

Na Configuração do CIF, um editor pode selecionar um formato alternativo de URL da página do produto ou da categoria. Se nada for selecionado lá, a implementação voltará para a configuração do sistema geral.

A alteração do formato de URL de um site ativo pode ter um impacto negativo no tráfego orgânico do site. Consulte as [Práticas recomendadas](#best-practices) abaixo e planeje cuidadosamente a alteração do formato de URL com antecedência.

![Formatos de URL na Configuração do CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> A configuração específica do armazenamento dos formatos de URL requer o [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) e a versão mais recente do complemento Adobe Experience Manager Content and Commerce.

## URLs da página do produto com reconhecimento de categoria {#context-aware-pdps}

Como é possível codificar informações de categoria em um URL de produto, os produtos que estão em várias categorias também podem ser endereçados com vários URLs de produto.

Os formatos de URL padrão selecionam uma das alternativas possíveis usando o seguinte esquema:

* se o `url_path` estiver definido pelo back-end de comércio eletrônico, use-o (desaprovado)
* do `url_rewrites` use as URLs que terminam com o `url_key` do produto como alternativas
* a partir dessas alternativas, use aquele com mais segmentos de caminho
* se houver vários, use o primeiro na ordem fornecida pelo back-end de comércio eletrônico

Este esquema seleciona o `url_path` com mais ancestrais, baseado na suposição de que uma categoria filho é mais específica do que sua categoria pai. O `url_path` selecionado é considerado _canônico_ e é sempre usado como o link canônico nas páginas do produto ou no mapa de site do produto.

No entanto, quando um comprador navega de uma página de categoria para uma página de produto ou de uma página de produto para outra página de produto relacionada na mesma categoria, vale a pena manter o contexto de categoria atual. Nesse caso, a seleção `url_path` deve preferir alternativas que estejam dentro do contexto da categoria atual em vez da seleção _canônica_ descrita acima.

Este recurso deve ser habilitado na _configuração do Provedor de URL do CIF_. Se ativada, a seleção pontua as alternativas como maiores, quando

* eles correspondem a partes de um determinado `url_path` de categoria desde o início (correspondência de prefixo difuso)
* ou eles correspondem a `url_key` de determinada categoria em qualquer lugar (correspondência parcial exata)

Por exemplo, considere a resposta para uma [consulta de produtos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) abaixo. Considerando o seguinte:

* o usuário está na página de categoria &quot;Novos produtos / Novo no verão de 2022&quot;
* a loja usa o formato de URL da página de categoria padrão

A alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corresponde a dois segmentos de caminho do contexto desde o início. Ou seja, &quot;novos produtos&quot; e &quot;novo no verão de 2022&quot;. Se o armazenamento usar um formato de URL de página de categoria que contenha apenas a categoria `url_key`, a mesma alternativa ainda será selecionada, pois ele corresponde ao `url_key` do contexto em qualquer lugar. Em ambos os casos, a URL da página do produto é criada para o &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> As URLs de produtos com reconhecimento de categoria exigem o [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) ou mais recente.

## Categoria específica e páginas de produto {#specific-pages}

É possível criar [páginas de várias categorias e produtos](/help/commerce-cloud/cif-storefront/authoring/multi-template-usage.md) somente para um subconjunto específico de categorias ou produtos de um catálogo.

### Critérios de seleção {#specific-pages-selection}

A seleção de uma página de categoria específica é direta, com base no `url_path` ou `url_key` da categoria. Subcategorias correspondentes só têm suporte para formatos de URL que contenham a categoria completa `url_path`. Caso contrário, somente uma correspondência exata de `url_key` será possível.

Páginas de produto específicas são selecionadas pelo SKU ou pela categoria do produto. Este último requer que algumas informações de categoria sejam codificadas no URL do produto. Essa funcionalidade só está disponível para alguns dos formatos de URL padrão. Consulte a tabela a seguir para obter uma comparação sobre qual formato de URL suporta uma seleção de página específica por SKU ou categoria.


| Formato de URL | por SKU | por categoria |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | não | não |
| `{{page}}.html/{{category}}/{{url_key}}.html` | não | somente correspondência exata |
| `{{page}}.html/{{url_path}}.html` | não | sim |
| `{{page}}.html/{{sku}}.html` | sim | não |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | sim | não |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | sim | somente correspondência exata |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | sim | sim |

{style="table-layout:auto"}

>[!NOTE]
>
> A seleção de páginas de produto específicas por categoria requer o [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) ou mais recente.

### Vinculação profunda {#specific-pages-deep-linking}

O `UrlProvider` é pré-configurado para gerar deep links para páginas de categoria e produto específicas em instâncias do nível do autor. Essa capacidade é útil para editores que navegam em um site usando o modo de Visualização, navegam até uma página de produto ou categoria específica e voltam ao modo de Edição para editar a página.

Por outro lado, em instâncias do nível de publicação, os URLs de página de catálogo devem ser mantidos estáveis para não perder ganhos nas classificações do mecanismo de pesquisa, por exemplo. Devido a esse nível de publicação, as instâncias não renderizam deep links para páginas de catálogo específicas por padrão. Para alterar esse comportamento, a _Estratégia de página específica do provedor de URL da CIF_ pode ser configurada para sempre gerar URLs de página específicas.

### Várias páginas do catálogo {#multiple-product-pages}

Quando os editores desejam ter controle total da navegação de nível superior de um site, usar uma única página de catálogo para renderizar as categorias de nível superior de um catálogo pode não ser desejado. Em vez disso, os editores podem criar várias páginas de catálogo, uma para cada categoria do catálogo que desejam incluir na navegação de nível superior.

Para esse caso de uso, cada uma das páginas do catálogo pode ter uma referência a uma página de produto e categoria específica para a categoria configurada para a página do catálogo. O `UrlProvider` usa essas conexões para criar links para as páginas e categorias na categoria configurada. No entanto, por motivos de desempenho, somente os filhos de página de catálogo direto da raiz de navegação/página de aterrissagem de um site são considerados.

É recomendável que as páginas de produto e categoria de uma página de catálogo sejam descendentes dessa página de catálogo, caso contrário, componentes como Navegação ou Navegação estrutural podem não funcionar corretamente.

>[!NOTE]
>
> O suporte completo para várias páginas de catálogo requer o [CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) ou mais recente.

## Personalizações {#customization}

### Formatos personalizados de URL {#custom-url-format}

Para fornecer um formato de URL personalizado, um projeto pode implementar a interface de serviço [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) ou [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registrar a implementação como serviço OSGI. Essas implementações, se disponíveis, substituem o formato pré-definido configurado. Se houver várias implementações registradas, aquela com a classificação de serviço mais alta substituirá aquelas com a classificação de serviço mais baixa.

As implementações de formato de URL personalizado devem implementar um par de métodos para criar um URL a partir de determinados parâmetros e para analisar um URL para retornar os mesmos parâmetros, respectivamente.

### Combinar com Mapeamentos do Sling {#sling-mapping}

Além do `UrlProvider`, também é possível configurar os [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para substituir e processar URLs. O Arquétipo do AEM também fornece [um exemplo de configuração](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para definir alguns Mapeamentos do Sling para as portas 4503 (Publish) e 80 (Dispatcher).

### Combinar com o AEM Dispatcher {#dispatcher}

As substituições de URL também podem ser obtidas usando o servidor HTTP do AEM Dispatcher com o módulo `mod_rewrite`. O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) fornece uma configuração de referência do AEM Dispatcher que já inclui [regras de substituição](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para o tamanho gerado.

## Práticas recomendadas {#best-practices}

### Escolher o melhor formato de URL {#choose-url-format}

Como mencionado antes de selecionar um dos formatos padrão disponíveis, ou mesmo implementar um formato personalizado, depende muito das necessidades e dos requisitos de uma loja. As sugestões a seguir podem ajudar a tomar uma decisão instruída.

#### Use um formato de URL da página do produto que contenha o SKU. {#use-sku}

Os Componentes principais do CIF usam o SKU como identificador principal em todos os componentes. Se o formato do URL da página do produto não contiver o SKU, uma consulta do GraphQL será necessária para resolvê-lo. Essa resolução pode afetar o tempo até o primeiro byte. Além disso, pode ser desejável que os compradores possam encontrar produtos por SKU usando mecanismos de pesquisa.

#### Use um formato de URL da página do produto que contenha o contexto da categoria. {#use-url}

Alguns recursos do Provedor de URL da CIF só estão disponíveis ao usar formatos de URL de produto, que codificam o contexto da categoria, como a categoria `url_key` ou a categoria `url_path`. Mesmo que esses recursos não sejam necessários para uma nova loja, usar um desses formatos de URL no início ajuda a reduzir os esforços de migração no futuro.

#### Equilíbrio entre comprimento do URL e informações codificadas. {#balance-url}

Dependendo do tamanho do catálogo, em particular o tamanho e a profundidade da árvore de categorias, pode não ser razoável codificar o `url_path` completo das categorias na URL. Nesse caso, o comprimento do URL poderia ser reduzido incluindo apenas o `url_key` da categoria. Este método dá suporte à maioria dos recursos disponíveis ao usar a categoria `url_path`.

Além disso, use os [Mapeamentos do Sling](#sling-mapping) para combinar o SKU com o produto `url_key`. Na maioria dos sistemas de comércio eletrônico, o SKU segue um formato específico e separar o SKU do `url_key` para solicitações recebidas deve ser facilmente possível. Com isso em mente, deve ser possível reescrever uma URL de página de produto para `/p/{{category}}/{{sku}}-{{url_key}}.html`, e uma URL de categoria para `/c/{{url_key}}.html`, respectivamente. Os prefixos `/p` e `/c` ainda são necessários para distinguir páginas de produto e categoria de outras páginas de conteúdo.

### Migração para um novo formato de URL {#migrate-url-formats}

Muitos dos formatos de URL padrão são de alguma forma compatíveis entre si, o que significa que os URLs formatados por um podem ser analisados por outro. Isso ajuda a migrar entre formatos de URL.

Por outro lado, os mecanismos de pesquisa precisam de tempo para rastrear novamente todas as páginas do catálogo com o novo formato de URL. Para dar suporte a esse processo e também melhorar a experiência do usuário final, é recomendável fornecer redirecionamentos que encaminham o usuário dos URLs antigos para os novos.

Uma abordagem para isso pode ser, conectar um ambiente de preparo ao back-end de comércio eletrônico de produção e configurá-lo para usar o novo formato de URL. Posteriormente, obtenha o [mapa de site do produto gerado pelo gerador de mapa de site de produtos da CIF](/help/overview/seo-and-url-management.md) para o ambiente de preparo e produção, e use-o para criar um [mapa de regravação httpd do Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Esse mapa de regravação pode ser implantado na Dispatcher junto com a implantação do novo formato de URL.

## Exemplo {#example}

O projeto da [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) inclui configurações de exemplo para demonstrar o uso de URLs personalizados para páginas de produto e categoria. Essa configuração permite que cada projeto defina padrões de URL individuais para páginas de produto e categoria de acordo com suas necessidades de SEO. Usa-se uma combinação do `UrlProvider` da CIF e os Mapeamentos do Sling conforme descrito acima.

>[!NOTE]
>
>Essa configuração deve ser ajustada com o domínio externo usado pelo projeto. Os Mapeamentos do Sling estão funcionando com base no nome do host e no domínio. Portanto, essa configuração é desativada por padrão e deve ser ativada antes da implantação. Para fazer isso, renomeie a pasta `hostname.adobeaemcloud.com` do Mapeamento do Sling em `ui.content/src/main/content/jcr_root/etc/map.publish/https` de acordo com o nome de domínio usado e habilite essa configuração adicionando `resource.resolver.map.location="/etc/map.publish"` à configuração `JcrResourceResolver` do projeto.

## Recursos adicionais {#additional}

* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mapeamento de recursos do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/implementing/deploying/configuring/resource-mapping)
* [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
