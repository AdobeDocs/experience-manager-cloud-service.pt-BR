---
title: Buscar conteúdo JSON com JavaScript
description: Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo CodePen e o AEM Headless Client para JavaScript.
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Buscar conteúdo JSON com JavaScript {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Buscar conteúdo JSON com JavaScript"
>abstract="Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo CodePen e o AEM Headless Client para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Inicie o aplicativo CodePen de amostra"
>abstract="Criamos um aplicativo CodePen mínimo para introduzir a busca de dados JSON do ambiente de avaliação usando consultas persistentes do GraphQL.<br><br>Inicie o exemplo da CodePen clicando abaixo e siga este guia para saber mais."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="Neste módulo, você aprendeu a usar o AEM Headless Client for JavaScript para buscar dados JSON de seu ambiente de avaliação usando consultas persistentes do GraphQL.<br><br>Agora você sabe como usar esse cliente para consumir dados de dentro de seu próprio aplicativo web."
>abstract=""

## Introdução {#intro}

Você começa no aplicativo CodePen, que serve como um exemplo mínimo de busca de dados JSON usando a variável [Cliente autônomo do AEM para JavaScript](https://github.com/adobe/aem-headless-client-js). O aplicativo de amostra foi projetado para renderizar qualquer conteúdo JSON que seja retornado, independentemente da estrutura do modelo de fragmento de conteúdo subjacente. O aplicativo CodePen tenta ser detalhado com todos os erros encontrados e, portanto, você pode ver a seguinte mensagem de erro impressa no painel inferior do aplicativo:

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

Esse erro é esperado, pois o aplicativo ainda não está configurado para usar a consulta persistente que você salvou e publicou em um módulo anterior. Você configurará o aplicativo para buscar dados de seu query específico nas etapas a seguir.

## Apresentação do CodePen {#code-walkthrough}

O painel JS (Javascript) na CodePen contém os cérebros do aplicativo de exemplo. A partir da linha 2, importamos o Cliente sem cabeçalho AEM para JavaScript do CDN do Skypack. O Skypack é usado para facilitar o desenvolvimento sem uma etapa de compilação, mas você também pode usar o Cliente Sem Cabeça AEM com NPM ou Yarn em seus próprios projetos. Confira as instruções de uso no [LEITURA](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obter mais detalhes.

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Na linha 6, lemos os detalhes do host de publicação no `publishHost` parâmetro de consulta. Este é o host do qual o Cliente Sem Cabeça do AEM buscará dados. Normalmente, isso seria codificado no aplicativo, mas estamos usando um parâmetro de consulta para facilitar o trabalho do aplicativo CodePen com ambientes diferentes.

Configuramos o Cliente Sem Cabeçalho do AEM na linha 12 para usar uma função proxy Adobe Runtime para evitar problemas de CORS. Isso não é necessário para seus próprios projetos, mas é necessário para que o aplicativo CodePen funcione com seu ambiente de avaliação. A função de proxy está configurada para usar a variável `publishHost` valor que foi fornecido no parâmetro de consulta.

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

Finalmente, a função `fetchJsonFromGraphQL()` é usado para executar a solicitação de busca usando o Cliente Sem Cabeça do AEM. Ele é chamado sempre que o código é alterado, ou pode ser acionado pressionando o link &quot;Refetch&quot;. O `aemHeadlessClient.runPersistedQuery(..)` ocorre na linha 34. Um pouco mais tarde, faremos uma alteração na forma como esses dados JSON são renderizados, mas por enquanto vamos imprimi-los no `#output` div usando o `resultToPreTag(queryResult)` .

## Buscar dados da consulta mantida {#use-persisted-query}

Na linha 25, indicamos qual consulta persistente do GraphQL o aplicativo deve buscar dados. O nome da consulta persistente é uma combinação do nome do projeto (ou seja, `your-project`), seguido por uma barra e, em seguida, o nome do query.

Atualize o `persistedQueryName` para usar a consulta persistente criada no módulo anterior. Se você seguisse a sugestão de nomenclatura exatamente você teria criado uma consulta persistente chamada `adventures` no `your-project` e você definiria a variável `persistedQueryName` para `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

Depois que essa alteração for feita, o aplicativo deverá atualizar automaticamente e imprimir a resposta JSON bruta da sua consulta persistente para o `#output` div. Se aparecer uma mensagem de erro, verifique o console para obter mais detalhes.

Esse JSON contém as propriedades exatas de que seu aplicativo precisa? Caso contrário, retorne ao ambiente de criação do AEM, às Ferramentas, ao Editor de consultas do GraphQL (ou navegue até o `/aem/graphiql.html` caminho) e faça alterações na sua consulta persistente. Não se esqueça de salvar e publicar a query depois que terminar.

## Alterar a renderização JSON {#change-rendering}

Atualmente, o JSON está sendo renderizado como está em um `pre` tag, que não é muito criativa. Podemos mudar nossa Caneta de código para usar o `resultToDom()` em vez disso, para ilustrar como a resposta JSON pode ser repetida para criar um resultado mais interessante.

Para fazer essa alteração, comente a linha 37 e remova o comentário da linha 40:

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

Essa função também renderizará quaisquer imagens incluídas na resposta JSON como uma `img` . Se os fragmentos de conteúdo &quot;Aventura&quot; criados não incluírem imagens, tente mudar para utilizar a variável `aem-demo-assets/adventures-all` consulta persistente modificando a linha 25:

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

Essa consulta produzirá uma resposta JSON que inclui imagens e a variável `resultToDom()` os renderizará em linha.

![Resultado da consulta de aventuras-tudo e da função de renderização resultToDom](assets/do-not-localize/adventures-all-query-result.png)
