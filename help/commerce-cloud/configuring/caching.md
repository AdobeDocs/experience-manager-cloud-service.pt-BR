---
title: Cache e desempenho
description: Cache e desempenho
translation-type: tm+mt
source-git-commit: 2997a28e79b51e88ececbd46c81dbc6a6c443e68
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# Cache e desempenho {#caching}

## Cache de respostas do Componente e GraphQL {#graphql}

Os componentes principais CIF AEM já têm suporte integrado para o cache de respostas GraphQL para componentes individuais. Esse recurso pode ser usado para reduzir o número de chamadas de backend do GraphQL por um fator grande. Um cache eficaz pode ser obtido especialmente para query repetitivos, como recuperar a árvore de categoria de um componente de navegação ou buscar todos os valores de agregações/facetas disponíveis exibidos nas páginas de pesquisa e categoria do produto.

Para os componentes principais CIF AEM, o cache é configurado com base em componentes, de modo que é possível controlar se (e por quanto tempo) as solicitações/respostas do GraphQL estão sendo armazenadas em cache para cada componente. Também é possível definir o comportamento de cache para serviços OSGi usando o cliente GraphQL.

### Configuração

Depois de configurados para um determinado componente, os start de cache armazenam query e respostas GraphQL, conforme definido por cada entrada de configuração de cache. O tamanho do cache e a duração do armazenamento em cache de cada entrada devem ser definidos com base em projetos, dependendo, por exemplo, da frequência com que os dados do catálogo podem mudar, da importância de um componente sempre exibir os dados mais recentes possíveis etc. Observe que não há nenhuma invalidação de cache, portanto, tenha cuidado ao definir a duração do cache.

Ao configurar o cache para componentes, o nome do cache deve ser o nome dos componentes **proxy** que você define no projeto.

Antes de enviar uma solicitação GraphQL, o cliente verificará se a mesma solicitação GraphQL **exata** já está armazenada em cache e possivelmente retornará a resposta em cache. Para corresponder, a solicitação do GraphQL DEVE corresponder exatamente, ou seja, o query, o nome da operação (se houver), as variáveis (se houver) DEVEM ser iguais à solicitação em cache e também todos os cabeçalhos HTTP personalizados que podem ser definidos DEVEM ser iguais. Por exemplo, o cabeçalho Magento DEVE corresponder `Store` .

### Exemplos

Recomendamos que isso configure algum armazenamento em cache para o serviço de pesquisa que busca todos os valores de agregações/facetas disponíveis exibidos nas páginas de pesquisa e categoria do produto. Normalmente, esses valores só mudam quando um novo atributo é adicionado aos produtos, por exemplo, para que a duração dessa entrada de cache possa ser &quot;grande&quot; se o conjunto de atributos do produto não for alterado com frequência. Embora seja específico do projeto, recomendamos valores de alguns minutos em fases de desenvolvimento do projeto e algumas horas em sistemas de produção estáveis.

Normalmente, isso é configurado com a seguinte entrada de cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Outro exemplo de cenário em que o recurso de cache GraphQl é recomendado para ser usado é o componente de navegação porque envia o mesmo query GraphQL em todas as páginas. Nesse caso, a entrada do cache normalmente seria definida como:

```
venia/components/structure/navigation:true:10:600
```

quando se considera a [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia) . Observe o uso do nome proxy do componente `venia/components/structure/navigation`, e **não** o nome do componente de navegação CIF (`core/cif/components/structure/navigation/v1/navigation`).

O armazenamento em cache para outros componentes deve ser definido com base em projetos, geralmente em coordenação com o armazenamento em cache configurado no nível da Dispatcher. Lembre-se de que não há nenhuma invalidação ativa desses caches, então a duração do armazenamento em cache deve ser cuidadosamente definida. Não há valores de &quot;tamanho único&quot; que correspondam a todos os projetos possíveis e casos de uso. Certifique-se de definir uma estratégia de cache no nível do projeto que melhor corresponda às exigências do seu projeto.

## Cache Dispatcher {#dispatcher}

O armazenamento em cache AEM páginas ou fragmentos no Dispatcher [](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.translate.html) AEM é uma prática recomendada para qualquer projeto AEM. Normalmente, ele depende de técnicas de invalidação que garantem que qualquer conteúdo alterado no AEM seja atualizado corretamente no Dispatcher. Este é um recurso principal da estratégia de cache do AEM Dispatcher.

Além do conteúdo gerenciado puro, AEM uma página geralmente pode exibir dados de comércio que são obtidos dinamicamente do Magento via GraphQL. Embora a estrutura da página possa nunca mudar, o conteúdo de comércio pode mudar, por exemplo, se alguns dados do produto (nome, preço etc.) mudarem no Magento.

Para garantir que as páginas CIF possam ser armazenadas em cache por um período limitado no expedidor AEM, recomendamos o uso da Invalidação [de Cache Baseada em](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) Tempo (também conhecida como cache baseado em TTL) ao armazenar páginas CIF no Dispatcher AEM. Este recurso pode ser configurado em AEM com o uso do pacote adicional [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) .

Com o armazenamento em cache baseado em TTL, um desenvolvedor normalmente define uma ou várias durações de armazenamento em cache para páginas AEM selecionadas. Isso garante que as páginas CIF sejam armazenadas em cache somente no AEM dispatcher até a duração configurada e que o conteúdo seja atualizado com frequência.

>[!NOTE]
>
>Embora os dados do lado do servidor possam ser armazenados em cache pelo AEM dispatcher, alguns componentes CIF, como o `product`, `productlist`e `searchresults` componentes, normalmente buscam novamente os preços do produto em uma solicitação do navegador do lado do cliente quando a página é carregada. Isso garante que o conteúdo dinâmico essencial seja sempre buscado no carregamento da página.

## Recursos adicionais

- [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de cache GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [Dispatcher AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.translate.html)