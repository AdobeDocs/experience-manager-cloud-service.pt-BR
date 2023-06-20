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
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 15%

---

# Configurações avançadas de URL {#url}

>[!NOTE]
>
> A Otimização do mecanismo de pesquisa (SEO) se tornou uma preocupação principal para muitos comerciantes. Como resultado, as preocupações com a SEO precisam ser abordadas em muitos projetos do Adobe Experience Manager (AEM) as a Cloud Service. Leia [Práticas recomendadas de gerenciamento de SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) para obter informações adicionais.

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem configurações avançadas para personalizar os URLs das páginas de produto e categoria. Muitas implementações personalizam esses URLs para fins de otimização de mecanismo de pesquisa (SEO). O vídeo a seguir mostra detalhes sobre como configurar o serviço `UrlProvider` e os recursos do [Mapeamento do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o `UrlProvider` de acordo com os requisitos e necessidades de SEO, um projeto deve fornecer uma configuração OSGI para o _Configuração do provedor de URL da CIF_.

>[!NOTE]
>
> Desde a versão 2.0.0 dos Componentes principais da CIF do AEM, a configuração do Provedor de URL fornece apenas formatos de URL predefinidos, em vez dos formatos configuráveis de texto livre conhecidos das versões 1.x. Além disso, o uso de seletores para transmitir dados em URLs foi substituído por sufixos.

### Formato do URL da página do produto {#product}

O modelo configura os URLs das páginas de produto e oferece suporte às seguintes opções:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (default)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

No caso do [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` é substituída por `/content/venia/us/en/products/product-page`
* `{{sku}}` é substituído pelo SKU do produto, por exemplo, `VP09`
* `{{url_key}}` é substituído pelo nome do produto `url_key` propriedade, por exemplo, `lenora-crochet-shorts`
* `{{url_path}}` é substituído pelo nome do produto `url_path`, por exemplo, `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` é substituída pela variante selecionada no momento, por exemplo, `VP09-KH-S`

Uma vez que a `url_path` foi descontinuado, os formatos de URL de produto predefinidos usam o `url_rewrites` e escolha aquele com mais segmentos de caminho como alternativa se a variável `url_path` não está disponível.

Com os dados de exemplo acima, um URL de variante de produto formatado usando o formato de URL padrão será semelhante a `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato do URL da página de categoria {#product-list}

O modelo configura os URLs das páginas de categoria ou lista de produtos e oferece suporte às seguintes opções:

* `{{page}}.html/{{url_path}}.html` (default)
* `{{page}}.html/{{url_key}}.html`

No caso do [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` é substituída por `/content/venia/us/en/products/category-page`
* `{{url_key}}` é substituído pelo nome da `url_key` propriedade
* `{{url_path}}` é substituído pelo nome da `url_path`

Com os dados de exemplo acima, uma URL de página de categoria formatada usando o formato de URL padrão será semelhante a `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> A variável `url_path` é uma concatenação da variável `url_keys` dos ancestrais de um produto ou categoria e do produto ou categoria do `url_key` separado por `/` barra. Each `url_key` é considerado exclusivo em um determinado armazenamento.

### Configuração específica da loja {#store-specific-urlformats}

A categoria do sistema e os formatos de URL da página do produto definidos pelo _Configuração do provedor de URL da CIF_ pode ser alterado para cada armazenamento.

Na configuração da CIF, um editor pode selecionar um produto alternativo ou um formato de URL de página de categoria. Se nada for selecionado, a implementação fallback para a configuração do sistema.

A alteração do formato de URL de um site ativo pode ter um impacto negativo no tráfego orgânico do site. Consulte a [Práticas recomendadas](#best-practices) abaixo e planeje com antecedência a alteração do formato do URL.

![Formatos de URL na configuração da CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> A configuração específica da loja dos formatos de URL exige [Componentes principais da CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-CIF-components-reator-2.6.0) e a versão mais recente do complemento Adobe Experience Manager Content and Commerce.

## URLs da página do produto com reconhecimento de categoria {#context-aware-pdps}

Como é possível codificar informações de categoria em um URL de produto, os produtos que estão em várias categorias também podem ser endereçados com vários URLs de produto.

Os formatos de URL padrão selecionarão uma das alternativas possíveis usando o seguinte esquema:

* se a variável `url_path` é definido pelo back-end de comércio eletrônico usá-lo (desaprovado)
* do `url_rewrites` usar os URLs que terminam com o do produto `url_key` como alternativas
* a partir dessas alternativas, use aquele com mais segmentos de caminho
* se houver vários, use o primeiro na ordem fornecida pelo back-end de comércio eletrônico

Este esquema selecionará o `url_path` com a maioria dos antecessores, com base na suposição de que uma categoria filho é mais específica do que sua categoria pai. O selecionado dessa forma `url_path` é considerado _canônico_ e sempre serão usados como link canônico nas páginas do produto ou no mapa de site do produto.

No entanto, quando um comprador navega de uma página de categoria para uma página de produto ou de uma página de produto para outra página de produto relacionada na mesma categoria, vale a pena manter o contexto de categoria atual. Neste caso, o `url_path` a seleção deve preferir alternativas, que estão dentro do contexto da categoria atual, _canônico_ seleção descrita acima.

Esse recurso deve ser ativado na variável _Configuração do provedor de URL da CIF_. Se ativada, a seleção pontuará as alternativas como maiores, quando

* elas correspondem a partes de uma determinada categoria `url_path` do início (correspondência de prefixos difusos)
* ou eles correspondem a uma determinada categoria `url_key` em qualquer lugar (correspondência parcial exata)

Por exemplo, considere a resposta de um [consulta de produtos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) abaixo. Considerando que o usuário está na página de categoria &quot;Novos produtos / Novo no verão de 2022&quot; e a loja usa o formato de URL da página de categoria padrão, a alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corresponderia a dois segmentos de caminho do contexto desde o início: &quot;novos produtos&quot; e &quot;novo no verão de 2022&quot;. Se a loja usar um formato de URL de página de categoria que contenha apenas a categoria `url_key`, a mesma alternativa ainda seria selecionada, pois corresponde à variável de contexto `url_key` em qualquer lugar. Em ambos os casos, o URL da página do produto seria criado para o &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

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

É possível criar [várias páginas de categoria e produto](../authoring/multi-template-usage.md) apenas para um subconjunto específico de categorias ou produtos de um catálogo.

### Critérios de seleção {#specific-pages-selection}

A seleção de uma página de categoria específica é direta, com base na `url_path` ou `url_key`. Subcategorias correspondentes são suportadas apenas para formatos de URL que contenham a categoria completa `url_path`. Caso contrário, apenas uma correspondência exata do `url_key` é possível.

Páginas de produto específicas são selecionadas pelo SKU ou pela categoria do produto. Posteriormente, exige que algumas informações de categoria sejam codificadas no URL do produto. Isso só está disponível para alguns dos formatos de URL padrão. Consulte a tabela abaixo para obter uma comparação sobre qual formato de URL suporta a seleção de página específica por sku ou categoria.


| Formato de URL | por sku | por categoria |
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
> A seleção de páginas de produtos específicas por categoria requer [Componentes principais da CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) ou mais recente.

### Vinculação profunda {#specific-pages-deep-linking}

A variável `UrlProvider` O é pré-configurado para gerar deep links para páginas de categoria e produto específicas nas instâncias do nível do autor. Isso é útil para editores que navegam em um site usando o modo de Visualização, navegam até uma página de produto ou categoria específica e voltam ao modo de Edição para editar a página.

Por outro lado, em instâncias do nível de publicação, os URLs de página de catálogo devem ser mantidos estáveis para não perder ganhos nas classificações do mecanismo de pesquisa, por exemplo. Por causa disso, as instâncias de nível de publicação não renderizarão deep links para páginas de catálogo específicas por padrão. Para alterar esse comportamento, a variável _Estratégia de página específica do provedor de URL da CIF_ O pode ser configurado para sempre gerar URLs de página específicos.

### Várias páginas do catálogo {#multiple-product-pages}

Quando os editores desejam ter controle total da navegação de nível superior de um site, usar uma única página de catálogo para renderizar as categorias de nível superior de um catálogo pode não ser desejado. Em vez disso, os editores podem criar várias páginas de catálogo, uma para cada categoria do catálogo que desejam incluir na navegação de nível superior.

Para esse caso de uso, cada uma das páginas do catálogo pode ter uma referência a uma página de produto e categoria específica para a categoria configurada para a página do catálogo. A variável `UrlProvider` O os usará para criar links para as páginas e categorias na categoria configurada. No entanto, por motivos de desempenho, somente os filhos de página de catálogo direto da raiz de navegação/página de aterrissagem de um site são considerados.

É recomendável que as páginas de produto e categoria de uma página de catálogo sejam descendentes dessa página de catálogo, caso contrário, componentes como Navegação ou Navegação estrutural podem não funcionar corretamente.

>[!NOTE]
>
> O suporte completo para várias páginas de catálogo requer [Componentes principais da CIF 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) ou mais recente.

## Personalizações {#customization}

### Formatos personalizados de URL {#custom-url-format}

Para fornecer um formato de URL personalizado, um projeto pode implementar o [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) ou o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registre a implementação como um serviço OSGI. Essas implementações, se disponíveis, substituirão o formato pré-definido configurado. Se houver várias implementações registradas, aquela com a classificação de serviço mais alta substituirá aquela(s) com a classificação de serviço mais baixa.

As implementações de formato de URL personalizado devem implementar um par de métodos para criar um URL a partir de determinados parâmetros e para analisar um URL para retornar os mesmos parâmetros, respectivamente.

### Combinar com Mapeamentos do Sling {#sling-mapping}

Além do `UrlProvider`, também é possível configurar [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para substituir e processar URLs. O Arquétipo do AEM também fornece [um exemplo de configuração](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para definir alguns Mapeamentos do Sling para as portas 4503 (Publish) e 80 (Dispatcher).

### Combinar com o AEM Dispatcher {#dispatcher}

As substituições de URL também podem ser obtidas usando o servidor HTTP do AEM Dispatcher com `mod_rewrite` módulo. O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) fornece uma configuração de referência do AEM Dispatcher que já inclui [regras de substituição](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para o tamanho gerado.

## Práticas recomendadas     {#best-practices}

### Escolher o melhor formato de URL {#choose-url-format}

Como mencionado antes de selecionar um dos formatos padrão disponíveis, ou mesmo implementar um formato personalizado, depende muito das necessidades e dos requisitos de uma loja. As sugestões a seguir podem ajudar a tomar uma decisão instruída.

_**Use um formato de URL da página do produto que contenha a SKU.**_

Os Componentes principais da CIF usam a SKU como o identificador principal de todos os componentes. Se o formato do URL da página do produto não contiver o SKU, uma consulta do GraphQL será necessária para resolvê-lo. Isso pode afetar o tempo até o primeiro byte. Além disso, pode ser desejável que os compradores possam encontrar produtos por sku usando mecanismos de pesquisa.

_**Use um formato de URL da página do produto que contenha o contexto da categoria.**_

Alguns recursos do Provedor de URL da CIF só estão disponíveis ao usar formatos de URL de produto, que codificam o contexto da categoria, como a categoria `url_key` ou a categoria `url_path`. Mesmo que esses recursos não sejam necessários para uma nova loja, usar um desses formatos de URL no início ajuda a reduzir os esforços de migração no futuro.

_**Equilíbrio entre comprimento do URL e informações codificadas.**_

Dependendo do tamanho do catálogo, em particular o tamanho e a profundidade da árvore de categoria, pode não ser razoável codificar o inteiro `url_path` de categorias no URL. Nesse caso, o comprimento do URL poderia ser reduzido incluindo somente o da categoria. `url_key` em vez disso. Isso suportará a maioria dos recursos que estão disponíveis ao usar a categoria `url_path`.

Além disso, utilize [Mapeamentos do Sling](#sling-mapping) para combinar o SKU com o produto `url_key`. Na maioria dos sistemas de comércio eletrônico, o SKU segue um formato específico e separa o SKU do `url_key` para solicitações recebidas devem ser facilmente possíveis. Com isso em mente, deve ser possível reescrever o URL de uma página de produto para `/p/{{category}}/{{sku}}-{{url_key}}.html`e um URL de categoria para `/c/{{url_key}}.html` respectivamente. A variável `/p` e `/c` Os prefixos ainda são necessários para distinguir as páginas de produto e categoria de outras páginas de conteúdo.

### Migração para um novo formato de URL {#migrate-url-formats}

Muitos dos formatos de URL padrão são de alguma forma compatíveis entre si, o que significa que os URLs formatados por um podem ser analisados por outro. Isso ajuda a migrar entre formatos de URL.

Por outro lado, os mecanismos de pesquisa precisarão de algum tempo para rastrear novamente todas as páginas do catálogo com o novo formato de URL. Para dar suporte a esse processo e também melhorar a experiência do usuário final, é recomendável fornecer redirecionamentos que encaminham o usuário dos URLs antigos para os novos.

Uma abordagem para isso pode ser, conectar um ambiente de preparo ao back-end de comércio eletrônico de produção e configurá-lo para usar o novo formato de URL. Posteriormente, obtenha a [mapa de site de produto gerado pelo gerador de mapa de site de produtos da CIF](../../overview/seo-and-url-management.md) para o ambiente de preparo e produção, e usá-los para criar uma [Mapa de reescrita do Apache httpd](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Esse mapa de regravação pode ser implantado no dispatcher junto com a implantação do novo formato de URL.

## Exemplo {#example}

O projeto da [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) inclui configurações de exemplo para demonstrar o uso de URLs personalizados para páginas de produto e categoria. Isso permite que cada projeto configure padrões de URL individuais para páginas de produto e categoria de acordo com suas necessidades de SEO. Usa-se uma combinação do `UrlProvider` da CIF e os Mapeamentos do Sling conforme descrito acima.

>[!NOTE]
>
>Essa configuração deve ser ajustada com o domínio externo usado pelo projeto. Os Mapeamentos do Sling estão funcionando com base no nome do host e no domínio. Portanto, essa configuração é desativada por padrão e deve ser ativada antes da implantação. Para fazer isso, renomeie a pasta `hostname.adobeaemcloud.com` do Mapeamento do Sling em `ui.content/src/main/content/jcr_root/etc/map.publish/https` de acordo com o nome de domínio usado e ative essa configuração adicionando `resource.resolver.map.location="/etc/map.publish"` à configuração `JcrResourceResolver` do projeto.

## Recursos adicionais {#additional}

* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mapeamento de recursos do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
