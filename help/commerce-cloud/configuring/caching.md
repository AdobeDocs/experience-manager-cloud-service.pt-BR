---
title: Armazenamento em cache e desempenho
description: Saiba mais sobre as diferentes configurações disponíveis para habilitar o GraphQL e o armazenamento em cache de conteúdo para otimizar o desempenho da sua implementação comercial.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 40%

---

# Armazenamento em cache e desempenho {#caching}

## Armazenamento em cache de respostas do Component e GraphQL {#graphql}

Os Componentes principais da CIF do AEM já contam com suporte integrado para o armazenamento em cache de respostas GraphQL para componentes individuais. Esse recurso pode ser usado para reduzir consideravelmente o número de chamadas GraphQL de back-end. Um armazenamento em cache eficaz pode ser obtido especialmente para consultas repetitivas, como recuperar a árvore de categoria de um componente de navegação ou buscar todos os valores de agregações/facetas disponíveis, exibidos nas páginas de pesquisa e categoria do produto.

Para os Componentes principais da CIF do AEM, o armazenamento em cache é configurado de acordo com os componentes, portanto é possível controlar se (e por quanto tempo) as solicitações/respostas de GraphQL estão sendo armazenadas em cache para cada componente. Também é possível definir o comportamento do armazenamento em cache de serviços OSGi usando o cliente GraphQL.

### Configuração {#configuration}

Depois de configurado para um determinado componente, o cache começa a armazenar consultas e respostas GraphQL conforme definido por cada entrada de configuração do cache. O tamanho do cache e a duração do armazenamento em cache de cada entrada são definidos de acordo com o projeto, dependendo, por exemplo, do seguinte:

* A frequência com que os dados do catálogo podem mudar.
* É crítico que um componente sempre exiba os dados mais recentes possíveis e assim por diante.

Não há nenhuma invalidação de cache, portanto, tenha cuidado ao definir a duração do cache.

Ao configurar o armazenamento em cache de componentes, o nome do cache deve ser o nome dos componentes **proxy** definidos no projeto.

Antes de enviar uma solicitação GraphQL, o cliente verifica se **exato** a mesma solicitação do GraphQL já está armazenada em cache e possivelmente retorna a resposta em cache. Para corresponder, a solicitação GraphQL _deve_ corresponde exatamente. Ou seja, a consulta, o nome da operação (se houver), as variáveis (se houver) _deve_ todos devem ser iguais à solicitação em cache. E, todos os cabeçalhos HTTP personalizados que podem ser definidos _deve_ ser o mesmo. Por exemplo, o Adobe Commerce `Store` cabeçalho _deve_ corresponde.

### Exemplos {#examples}

A Adobe recomenda que você configure algum armazenamento em cache para o serviço de pesquisa que busca todos os valores de agregações/facetas disponíveis exibidos nas páginas de pesquisa e categoria do produto. Normalmente, esses valores só mudam quando um novo atributo é adicionado aos produtos, por exemplo. Portanto, a duração dessa entrada de cache pode ser &quot;grande&quot; se o conjunto de atributos do produto não for alterado com frequência. Embora essa entrada seja específica do projeto, o Adobe recomenda valores de alguns minutos em fases de desenvolvimento do projeto e de algumas horas em sistemas de produção estáveis.

Normalmente, essa configuração é definida com a seguinte entrada de cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Outro exemplo de cenário em que o recurso de armazenamento em cache GraphQl é recomendado para uso é o componente de navegação. O motivo é que ele envia a mesma consulta do GraphQL em todas as páginas. Nesse caso, a entrada do cache normalmente seria definida como:

```
venia/components/structure/navigation:true:10:600
```

Tendo em conta que a [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) é usada. Observe o uso do nome proxy do componente `venia/components/structure/navigation`, e **não** o nome do componente de navegação na CIF (`core/cif/components/structure/navigation/v1/navigation`).

O armazenamento em cache para outros componentes deve ser definido de acordo com o projeto, geralmente junto com o armazenamento em cache configurado no Dispatcher. Lembre-se de que não há nenhuma invalidação ativa desses caches, portanto a duração do armazenamento em cache deve ser cuidadosamente definida. Não há valores de &quot;tamanho único&quot; que correspondam a todos os projetos e casos de uso possíveis. Defina a melhor estratégia de armazenamento em cache segundo as exigências do seu projeto.

## Cache do Dispatcher {#dispatcher}

O armazenamento em cache de páginas ou fragmentos do AEM no [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma prática recomendada para qualquer projeto do AEM. Normalmente, ele depende de técnicas de invalidação que garantem que qualquer conteúdo alterado no AEM seja atualizado corretamente no Dispatcher. Esse recurso é essencial para a estratégia de armazenamento em cache do AEM Dispatcher.

Além da CIF de conteúdo puro gerenciado pelo AEM, a página pode exibir dados comerciais que são buscados dinamicamente no Adobe Commerce via GraphQL. Embora a estrutura da página em si nunca mude, o conteúdo comercial pode mudar. Por exemplo, se os dados do produto, como nome e preço, forem alterados no Adobe Commerce.

Para garantir que as páginas da CIF sejam armazenadas em cache por um tempo limitado no AEM Dispatcher, a Adobe recomenda usar [Invalidação de cache com base no tempo](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (conhecido como armazenamento em cache com base em TTL) ao armazenar páginas da CIF no AEM Dispatcher. Esse recurso pode ser configurado no AEM com o uso do pacote adicional [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/).

Com o armazenamento em cache com base em TTL, o desenvolvedor normalmente define uma ou várias durações de armazenamento em cache para determinadas páginas do AEM. Essa duração garante que as páginas da CIF sejam armazenadas em cache somente no AEM Dispatcher pela duração configurada e que o conteúdo seja atualizado com frequência.

>[!NOTE]
>
>Embora os dados do lado do servidor possam ser armazenados em cache pelo AEM Dispatcher, alguns componentes da CIF, como o `product`, `productlist`, e `searchresults` normalmente, os componentes sempre buscam novamente os preços do produto em uma solicitação do navegador do lado do cliente quando a página é carregada. Isso garante que o conteúdo dinâmico essencial seja sempre buscado no carregamento da página.

## Recursos adicionais {#additional}

* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Configuração de armazenamento em cache GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR)
