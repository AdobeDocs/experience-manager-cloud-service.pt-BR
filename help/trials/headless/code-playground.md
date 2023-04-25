---
title: Renderizar o conteúdo em um aplicativo simples
description: Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo de exemplo CodePen e o AEM Headless Client para JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 3b64b909996674bcbe36f746bcfd15e1422a8a4b
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---


# Renderizar o conteúdo em um aplicativo simples {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Renderizar o conteúdo em um aplicativo simples"
>abstract="Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo de exemplo CodePen e o AEM Headless Client para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Inicie o aplicativo CodePen de amostra"
>abstract="Este guia aborda a consulta de dados JSON do seu ambiente de avaliação em um aplicativo Web JavaScript básico. Usaremos os Fragmentos de conteúdo que você modelou e criou nos módulos de aprendizagem anteriores, portanto, navegue primeiro por esses guias antes de entrar nesse.<br><br>Para demonstrar como o conteúdo pode ser consultado em um aplicativo da Web JavaScript, configuramos uma Caneta de código que você pode usar como está ou bifurcar em sua própria conta para personalizar ainda mais."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="Neste módulo, você aprendeu a usar o AEM Headless Client for JavaScript para buscar dados JSON de seu ambiente de avaliação usando consultas persistentes do GraphQL.<br><br>Agora você sabe como usar esse cliente para consumir dados de dentro de seu próprio aplicativo web."
>abstract=""

## CodePen {#codepen}

O CodePen é um editor de código online e um espaço de reprodução para desenvolvimento Web front-end. Ele permite que você grave o código de HTML, CSS e JavaScript em seu navegador e veja os resultados de seu trabalho quase instantaneamente. Você também pode salvar seu trabalho e compartilhá-lo com outras pessoas. Criamos um aplicativo no CodePen que você pode usar para buscar dados JSON de seu ambiente de avaliação usando o [Cliente autônomo do AEM para JavaScript](https://github.com/adobe/aem-headless-client-js). Você pode usar este aplicativo como está ou bifurcá-lo em sua própria conta do CodePen para personalizar ainda mais.

Clicar no **Inicie o aplicativo CodePen de amostra** Na versão de avaliação, você será direcionado para o aplicativo na CodePen. O aplicativo é um exemplo mínimo de busca de dados JSON com JavaScript. O aplicativo de amostra foi projetado para renderizar qualquer conteúdo JSON que seja retornado, independentemente da estrutura do modelo subjacente do Fragmento de conteúdo. Pronto para uso, o aplicativo buscará dados de um `aem-demo-assets` consulta persistente incluída no seu ambiente de avaliação. Você deve ver uma resposta JSON semelhante ao seguinte:

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

Em vez disso, se você vir um erro, verifique o console do navegador para obter mais detalhes ou entre em contato com o [no Slack](https://adobe-dx-support.slack.com).

Agora que você sabe um pouco sobre a CodePen, em seguida, configurará o aplicativo para buscar dados da consulta persistente criada em um módulo anterior.

## Apresentação do código JavaScript {#code-walkthrough}

O **JS** painel à direita em CodePen contém o Javascript do aplicativo de exemplo. A partir da linha 2, importamos o Cliente sem cabeçalho AEM para JavaScript do CDN do Skypack. O Skypack é usado para facilitar o desenvolvimento sem uma etapa de compilação, mas você também pode usar o Cliente Sem Cabeça AEM com NPM ou Yarn em seus próprios projetos. Confira as instruções de uso no [LEITURA](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obter mais detalhes.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Na linha 6, lemos os detalhes do host de publicação no `publishHost` parâmetro de consulta. Este é o host do qual o Cliente Sem Cabeça do AEM buscará dados. Normalmente, isso seria codificado no aplicativo, mas estamos usando um parâmetro de consulta para facilitar o trabalho do aplicativo CodePen com ambientes diferentes.

Configuramos o Cliente Sem Cabeçalho do AEM na linha 12 para usar uma função proxy Adobe Runtime para evitar problemas de CORS. Isso não é necessário para seus próprios projetos, mas é necessário para que o aplicativo CodePen funcione com seu ambiente de avaliação. A função de proxy está configurada para usar a variável `publishHost` valor que foi fornecido no parâmetro de consulta.

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

Finalmente, a função `fetchJsonFromGraphQL()` é usado para executar a solicitação de busca usando o Cliente Sem Cabeça do AEM. Ele é chamado sempre que o código é alterado ou pode ser acionado clicando no botão **Refetch** link . O `aemHeadlessClient.runPersistedQuery(..)` ocorre na linha 34. Um pouco mais tarde, faremos uma alteração na forma como esses dados JSON são renderizados, mas por enquanto vamos imprimi-los no `#output` div usando o `resultToPreTag(queryResult)` .

## Buscar dados da sua consulta persistente {#use-persisted-query}

Na linha 25, indicamos qual consulta persistente do GraphQL o aplicativo deve buscar dados. O nome da consulta persistente é uma combinação do nome do ponto de extremidade (ou seja, `your-project` ou `aem-demo-assets`), seguido por uma barra e, em seguida, o nome do query. Se você seguiu exatamente as instruções do módulo anterior, a consulta persistente criada estará no `your-project` endpoint .

1. Atualize o `persistedQueryName` para usar a consulta persistente criada no módulo anterior. Se você seguisse a sugestão de nomenclatura, teria criado uma consulta persistente chamada `adventure-list` no `your-project` e você definiria a variável `persistedQueryName` para `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Depois que essa alteração for feita, o aplicativo deverá atualizar automaticamente e imprimir a resposta JSON bruta da sua consulta persistente para o `#output` div. Se aparecer uma mensagem de erro, verifique o console para obter mais detalhes. Entre em contato [no Slack](https://adobe-dx-support.slack.com) se você ainda tiver problemas com essa etapa.

1. Esse JSON contém as propriedades exatas de que seu aplicativo precisa? Caso contrário, volte para a [Extrair conteúdo usando a API do GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) guia de aprendizado para fazer alterações. Não se esqueça de salvar e publicar seu query uma vez concluído.

## Alterar a renderização de JSON {#change-rendering}

O JSON é renderizado como está em um `pre` tag, que não é muito criativa. Podemos mudar nossa Caneta de código para usar o `resultToDom()` em vez disso, para ilustrar como a resposta JSON pode ser repetida para criar um resultado mais interessante.

1. Para fazer essa alteração, comente a linha 37 e remova o comentário da linha 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Essa função também renderizará quaisquer imagens incluídas na resposta JSON como uma `img` . Se a variável **Aventura** os fragmentos de conteúdo criados não incluem imagens, você pode tentar alternar para usar o `aem-demo-assets/adventures-all` consulta persistente modificando a linha 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Essa consulta produzirá uma resposta JSON que inclui imagens e a variável `resultToDom()` os renderizará em linha.

![Resultado da consulta de aventuras-tudo e da função de renderização resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Agora que você realizou o trabalho para criar os modelos e consultas, sua equipe de conteúdo pode assumir o controle com facilidade. Mostraremos o fluxo do autor de conteúdo no próximo módulo.
