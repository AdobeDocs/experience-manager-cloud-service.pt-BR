---
title: Configurações avançadas de URL
description: Saiba como personalizar os URLs das páginas de produto e categoria. Isso permite que as implementações otimizem URLs para mecanismos de pesquisa e promovam a descoberta.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 17%

---

# Configurações avançadas de URL {#url}

>[!NOTE]
>
> A Otimização do mecanismo de pesquisa (SEO) se tornou uma preocupação principal para muitos comerciantes. Como resultado, as preocupações com a SEO precisam ser abordadas em muitos projetos do Adobe Experience Manager (AEM) as a Cloud Service. Leia [Práticas recomendadas de gerenciamento de SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) para obter mais informações.

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem configurações avançadas para personalizar os URLs das páginas de produto e categoria. Muitas implementações personalizam esses URLs para fins de otimização de mecanismo de pesquisa (SEO). O vídeo a seguir mostra detalhes sobre como configurar o serviço `UrlProvider` e os recursos do [Mapeamento do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o `UrlProvider` de acordo com os requisitos e necessidades de SEO, um projeto deve fornecer uma configuração de OSGI para o _Configuração do provedor de URL da CIF_.

>[!NOTE]
>
> Desde a versão 2.0.0 dos Componentes principais da CIF do AEM, a configuração do Provedor de URL fornece apenas formatos de URL predefinidos, em vez dos formatos configuráveis de texto livre conhecidos das versões 1.x. Além disso, o uso de seletores para transmitir dados em URLs foi substituído por sufixos.

### Formato de URL da página do produto {#product}

Isso configura os URLs das páginas do produto e oferece suporte às seguintes opções:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (default)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

No caso de [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` será substituída por `/content/venia/us/en/products/product-page`
* `{{sku}}` será substituído pelo SKU do produto, por exemplo `VP09`
* `{{url_key}}` será substituído pelo `url_key` propriedade, por exemplo `lenora-crochet-shorts`
* `{{url_path}}` será substituído pelo `url_path`, por exemplo `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` será substituída pela variante selecionada no momento, por exemplo, `VP09-KH-S`

Como a variável `url_path` Se for descontinuado, os formatos de URL de produto predefinidos usarão `url_rewrites` e escolha aquele com os segmentos de caminho mais alternativos se a variável `url_path` não está disponível.

Com os dados de exemplo acima, um URL de variante de produto formatado usando o formato de URL padrão será semelhante `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato de URL da página de categoria {#product-list}

Isso configura os URLs das páginas de categoria ou lista de produtos e oferece suporte às seguintes opções:

* `{{page}}.html/{{url_path}}.html` (padrão)
* `{{page}}.html/{{url_key}}.html`

No caso de [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` será substituída por `/content/venia/us/en/products/category-page`
* `{{url_key}}` será substituído por `url_key` propriedade
* `{{url_path}}` será substituído por `url_path`

Com os dados de exemplo acima, um URL de página de categoria formatado usando o formato de URL padrão terá a aparência `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> O `url_path` é uma concatenação do `url_keys` dos ancestrais de um produto ou categoria e do produto ou categoria `url_key` separados por `/` barra. Cada `url_key` é considerada exclusiva em uma determinada loja.

### Configuração específica da loja {#store-specific-urlformats}

Os formatos de URL de página de produto e categoria do sistema definidos pela variável _Configuração do provedor de URL da CIF_ pode ser alterado para cada loja.

Na Configuração da CIF, um editor pode selecionar um formato alternativo de URL de página de produto ou categoria. Se nada for selecionado, a implementação falará para a configuração do sistema inteiro.

Alterar o formato do URL de um site ativo pode ter um impacto negativo no tráfego orgânico do site. Consulte a [Práticas recomendadas](#best-practices) abaixo e planeje com cuidado a alteração do formato do URL antecipadamente.

![Formatos de URL na configuração da CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> A configuração específica do armazenamento dos formatos de URL requer [Componentes principais da CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-CIF-components-reator-2.6.0) e a versão mais recente do complemento Adobe Experience Manager Content and Commerce.

## URLs de página de produto com reconhecimento de categoria {#context-aware-pdps}

Como é possível codificar informações de categoria em um URL de produto, os produtos que estão em várias categorias também podem ser endereçados com vários URLs de produto.

Os formatos padrão de URL selecionarão uma das alternativas possíveis usando o seguinte esquema:

* se a variável `url_path` é definido pelo back-end de comércio eletrônico usá-lo (obsoleto)
* do `url_rewrites` use os URLs que terminam com o `url_key` como alternativas
* Essas alternativas usam o que tem mais segmentos de caminho
* se houver vários, tome o primeiro na ordem dada pelo backend de comércio eletrônico

Este esquema selecionará a variável `url_path` com mais ancestrais, baseado na suposição de que uma categoria filho é mais específica do que a categoria pai. Os selecionados `url_path` é considerado _canônico_ e sempre serão usados como o link canônico nas páginas de produto ou no mapa do site do produto.

No entanto, quando um comprador navega de uma página de categoria para uma página de produto, ou de uma página de produto para outra página de produto relacionada na mesma categoria, vale a pena manter o contexto de categoria atual. Nesse caso, a variável `url_path` a seleção deve preferir alternativas que estejam no contexto da categoria atual em vez da _canônico_ seleção descrita acima.

Esse recurso deve ser ativado no _Configuração do provedor de URL da CIF_. Se ativada, a seleção pontuará as alternativas mais altas, quando

* correspondem a partes de uma determinada categoria `url_path` desde o início (correspondência de prefixo difusa)
* ou correspondem a uma categoria específica `url_key` em qualquer lugar (correspondência parcial exata)

Por exemplo, considere a resposta de uma [consulta de produtos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) abaixo. Considerando que o usuário está na página da categoria &quot;Novos produtos / Novos no verão de 2022&quot; e que a loja usa o formato de URL da página da categoria padrão, a alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corresponderia a 2 dos segmentos de caminho do contexto desde o início: &quot;novos produtos&quot; e &quot;novo no verão de 2022&quot;. Se a loja usar um formato de URL de página de categoria que contenha apenas a categoria `url_key`, a mesma alternativa ainda seria selecionada, pois corresponde ao contexto `url_key` em qualquer lugar. Em ambos os casos, o URL da página do produto seria criado para o &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

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
> Os URLs de produtos com reconhecimento de categoria exigem [Componentes principais da CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) ou mais recente.

## Categoria específica e páginas de produto {#specific-pages}

É possível criar [várias páginas de categoria e produto](../authoring/multi-template-usage.md) para apenas um subconjunto específico de categorias ou produtos de um catálogo.

### Critérios de seleção {#specific-pages-selection}

A seleção de uma página de categoria específica é direta, com base no `url_path` ou `url_key`. A correspondência de subcategorias é compatível somente com formatos de URL que contêm a categoria completa `url_path`. Caso contrário, somente uma correspondência exata da variável `url_key` é possível.

Páginas específicas do produto são selecionadas pelo SKU ou categoria do produto. A versão mais recente requer que algumas informações de categoria sejam codificadas no URL do produto. Isso só está disponível para alguns dos formatos de URL padrão. Consulte a tabela abaixo para obter uma comparação sobre qual formato de URL suporta a seleção de página específica por sku ou categoria.


| Formato de URL | por sku | por categoria |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | não | não |
| `{{page}}.html/{{category}}/{{url_key}}.html` | não | somente correspondência exata |
| `{{page}}.html/{{url_path}}.html` | não | sim |
| `{{page}}.html/{{sku}}.html` | sim | não |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | sim | não |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | sim | somente correspondência exata |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | sim | sim |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> A seleção de páginas de produto específicas por categoria requer [Componentes principais da CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) ou mais recente.

### Vinculação profunda {#specific-pages-deep-linking}

O `UrlProvider` O é pré-configurado para gerar deep links para páginas de categoria e produto específicas em instâncias da camada do autor. Isso é útil para editores que navegam em um site usando o modo de Visualização, navegam até uma página de produto ou categoria específica e alternam de volta para o modo de Edição para editar a página.

Por outro lado, ao publicar instâncias de nível, os URLs de página de catálogo devem ser mantidos estáveis para não perder ganhos nas classificações do mecanismo de pesquisa, por exemplo. Devido a essa situação, as instâncias de camada de publicação não renderizarão deep links para páginas de catálogo específicas por padrão. Para alterar esse comportamento, a variável _Estratégia da página específica do provedor de URL da CIF_ pode ser configurado para sempre gerar URLs de página específicos.

## Personalizações {#customization}

### Formatos de URL personalizados {#custom-url-format}

Para fornecer um formato de URL personalizado, um projeto pode implementar [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) ou [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registre a implementação como serviço OSGI. Essas implementações, se disponíveis, substituirão o formato configurado e predefinido. Se houver várias implementações registradas, aquela com a classificação de serviço mais alta substitui aquela(s) pela classificação de serviço mais baixa.

As implementações de formato de URL personalizado devem implementar um par de métodos para criar um URL a partir de determinados parâmetros e para analisar um URL para retornar os mesmos parâmetros, respectivamente.

### Combinar com Mapeamentos do Sling {#sling-mapping}

Além do `UrlProvider`, também é possível configurar os [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para substituir e processar URLs. O Arquétipo do AEM também fornece [um exemplo de configuração](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para definir alguns Mapeamentos do Sling para as portas 4503 (Publish) e 80 (Dispatcher).

### Combinar com o AEM Dispatcher {#dispatcher}

As substituições de URL também podem ser obtidas usando AEM servidor HTTP do Dispatcher com `mod_rewrite` módulo. O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) fornece uma configuração de referência do AEM Dispatcher que já inclui [regras de substituição](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para o tamanho gerado.

## Práticas recomendadas     {#best-practices}

### Escolha o melhor formato de URL {#choose-url-format}

Conforme mencionado antes de selecionar um dos formatos padrão disponíveis, ou até mesmo implementar um formato personalizado, depende muito das necessidades e dos requisitos de uma loja. As sugestões a seguir podem ajudar a tomar uma decisão.

_**Use o formato de URL da página do produto que contém o SKU.**_

Os Componentes principais da CIF usam o SKU como identificador principal em todos os componentes. Se o formato de URL da página do produto não contiver o SKU, será necessário um query GraphQL para resolvê-lo. Isso pode afetar o tempo para o primeiro byte. Além disso, pode ser desejável que os compradores possam encontrar produtos por sku usando mecanismos de pesquisa.

_**Use um formato de URL da página do produto que contenha o contexto da categoria.**_

Alguns recursos do provedor de URL da CIF só estão disponíveis ao usar formatos de URL do produto, que codificam o contexto da categoria, como a categoria `url_key` ou a categoria `url_path`. Mesmo que esses recursos não sejam necessários para uma nova loja, usar um desses formatos de URL no início ajuda a reduzir os esforços de migração no futuro.

_**Equilíbrio entre a duração do URL e as informações codificadas.**_

Dependendo do tamanho do catálogo, em especial do tamanho e profundidade da árvore de categoria, pode não ser razoável codificar todo o `url_path` de categorias no URL. Nesse caso, o comprimento do URL pode ser reduzido ao incluir somente o da categoria `url_key` em vez disso. Isso oferecerá suporte à maioria dos recursos disponíveis ao usar a categoria `url_path`.

Além disso, use [Mapeamentos do Sling](#sling-mapping) para combinar o SKU com o produto `url_key`. Na maioria dos sistemas de comércio eletrônico, o sku segue um formato específico e separa o sku do `url_key` para solicitações recebidas deve ser facilmente possível. Tendo isso em mente, deve ser possível reescrever um URL de página de produto para `/p/{{category}}/{{sku}}-{{url_key}}.html`e um URL de categoria para `/c/{{url_key}}.html` , respectivamente. O `/p` e `/c` ainda são necessários para distinguir as páginas de produto e categoria de outras páginas de conteúdo.

### Migrando para um novo formato de URL {#migrate-url-formats}

Muitos dos formatos de URL padrão são compatíveis entre si, o que significa que URLs formatados por um podem ser analisados por outro. Isso ajuda a migrar entre formatos de URL.

Por outro lado, os mecanismos de pesquisa precisarão de algum tempo para rastrear novamente todas as páginas de catálogo com o novo formato de URL. Para dar suporte a esse processo e também melhorar a experiência do usuário final, é recomendável fornecer redirecionamentos que encaminhem o usuário dos URLs antigos para os novos.

Uma abordagem para isso poderia ser conectar um ambiente de preparo ao back-end de produção de comércio eletrônico e configurá-lo para usar o novo formato de URL. Depois obtenha o [sitemap de produto gerado pelo gerador de mapa de site de produtos CIF](../../overview/seo-and-url-management.md) para o ambiente de preparo e produção, e use-os para criar um [Mapa de reescrita httpd do Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Esse mapa de reescrita pode ser implantado no dispatcher junto com a implantação do novo formato de URL.

## Exemplo {#example}

O projeto da [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) inclui configurações de exemplo para demonstrar o uso de URLs personalizados para páginas de produto e categoria. Isso permite que cada projeto configure padrões de URL individuais para páginas de produto e categoria de acordo com suas necessidades de SEO. Usa-se uma combinação do `UrlProvider` da CIF e os Mapeamentos do Sling conforme descrito acima.

>[!NOTE]
>
>Essa configuração deve ser ajustada com o domínio externo usado pelo projeto. Os Mapeamentos do Sling estão funcionando com base no nome do host e no domínio. Portanto, essa configuração é desativada por padrão e deve ser ativada antes da implantação. Para fazer isso, renomeie a pasta `hostname.adobeaemcloud.com` do Mapeamento do Sling em `ui.content/src/main/content/jcr_root/etc/map.publish/https` de acordo com o nome de domínio usado e ative essa configuração adicionando `resource.resolver.map.location="/etc/map.publish"` à configuração `JcrResourceResolver` do projeto.

## Recursos adicionais {#additional}

* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mapeamento de recursos do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
