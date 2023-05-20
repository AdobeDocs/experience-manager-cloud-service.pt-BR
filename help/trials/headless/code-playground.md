---
title: Renderizar seu conteúdo em um aplicativo simples
description: Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo CodePen de exemplo e o AEM Headless Client para JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1949ee211b4f816e05aa779deb9e287347f006ad
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 48%

---


# Renderizar seu conteúdo em um aplicativo simples {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Renderize o conteúdo em um aplicativo simples"
>abstract="Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo CodePen de exemplo e o AEM Headless Client para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Inicie o aplicativo CodePen de exemplo"
>abstract="Este guia aborda a consulta de dados JSON do seu ambiente de avaliação em um aplicativo web JavaScript básico. Usaremos os fragmentos de conteúdo que você modelou e criou nos módulos de aprendizagem anteriores, portanto, conclua esses guias antes de entrar neste."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="Neste módulo, você aprendeu a usar o AEM Headless Client para JavaScript para buscar dados JSON de seu ambiente de avaliação usando consultas persistentes de GraphQL.<br><br>Agora você sabe como pode usar esse cliente para consumir dados de seu próprio aplicativo web."
>abstract=""

## CanetaCódigo {#codepen}

CodePen é um editor de código online e um playground para desenvolvimento web front-end. Ele permite que você escreva código HTML, CSS e JavaScript no seu navegador e veja os resultados do seu trabalho quase que instantaneamente. Você também pode salvar seu trabalho e compartilhá-lo com outras pessoas. Criamos um aplicativo no CodePen que você pode usar para buscar dados JSON no seu ambiente de avaliação usando o [Cliente AEM Headless para JavaScript](https://github.com/adobe/aem-headless-client-js). Você pode usar este aplicativo como está ou bifurcá-lo em sua própria conta do CodePen para personalizar ainda mais.

Clicar no **Inicie o aplicativo de amostra CodePen** botão da avaliação levará você ao aplicativo no CodePen. O aplicativo serve como um exemplo mínimo de busca de dados JSON com JavaScript. O aplicativo de amostra foi projetado para renderizar qualquer conteúdo JSON retornado, independentemente da estrutura do modelo subjacente de Fragmento de conteúdo. Pronto para uso, o aplicativo buscará dados de um `aem-demo-assets` consulta persistente que está incluída em seu ambiente de avaliação. Você deve ver uma resposta JSON semelhante ao seguinte:

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

Caso veja um erro, verifique o console do navegador para obter mais detalhes ou entre em contato com [no Slack](https://adobe-dx-support.slack.com).

Agora que você sabe um pouco sobre o CodePen, em seguida, você configurará o aplicativo para buscar dados da consulta persistente criada em um módulo anterior.

## Apresentação do código JavaScript {#code-walkthrough}

A variável **JS** O painel à direita no CodePen contém o Javascript do aplicativo de exemplo. Começando na linha 2, importaremos o AEM Headless Client para JavaScript do Skypack CDN. O Skypack é usado para facilitar o desenvolvimento sem uma etapa de criação, mas você também pode usar o AEM Headless Client com o NPM ou Yarn em seus próprios projetos. Confira as instruções de uso no arquivo [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obter mais detalhes.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Na linha 6, lemos os detalhes do host de publicação do parâmetro de consulta `publishHost`. Este é o host no qual o AEM Headless Client buscará os dados. Normalmente, isso seria programado no aplicativo, mas estamos usando um parâmetro de consulta para facilitar o trabalho do aplicativo CodePen com ambientes diferentes.

Configuramos o cliente AEM Headless na linha 12:

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>A variável **serviceURL** está definido para usar uma função proxy Adobe IO Runtime para evitar problemas com CORS. Isso não será obrigatório nos seus próprios projetos, mas é necessário para que o aplicativo CodePen funcione com seu ambiente de avaliação. A função proxy é configurada para usar a variável **publishHost** que foi fornecido no parâmetro de consulta.

Por fim, a função `fetchJsonFromGraphQL()` é usada para executar a solicitação de busca usando o AEM Headless Client. Ele é chamado sempre que o código é alterado ou pode ser acionado clicando no link **Buscar novamente** link. A chamada `aemHeadlessClient.runPersistedQuery(..)` ocorre na linha 34. Mais à frente, faremos uma alteração na forma como esses dados JSON são renderizados, mas por enquanto vamos imprimi-los no div `#output` usando a função `resultToPreTag(queryResult)`.

## Buscar dados de sua consulta persistente {#use-persisted-query}

Na linha 25, indicamos de qual consulta persistente de GraphQL o aplicativo deve buscar dados. O nome da consulta persistente é uma combinação do nome do endpoint (ou seja, `your-project` ou `aem-demo-assets`), seguido por uma barra e, em seguida, o nome da query. Se você seguiu exatamente as instruções anteriores do módulo, a consulta persistente criada estará no `your-project` terminal.

1. Atualize a variável `persistedQueryName` para usar a consulta persistente criada no módulo anterior. Se você seguisse a sugestão de nomenclatura, teria criado uma consulta persistente chamada `adventure-list` no `your-project` e você definiria a variável `persistedQueryName` variável para `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Depois que essa alteração for feita, o aplicativo deve ser atualizado automaticamente e imprimir a resposta JSON bruta da sua consulta persistente no div `#output`. Se uma mensagem de erro aparecer, verifique o console para obter mais detalhes. Alcance [no Slack](https://adobe-dx-support.slack.com) se você ainda tiver problemas com essa etapa.

1. Esse JSON contém as propriedades exatas de que seu aplicativo precisa? Caso contrário, volte para a [Extrair conteúdo usando a API do GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) guia de aprendizado para fazer alterações. Não se esqueça de salvar e publicar sua consulta depois de concluído.

## Alterar a renderização de JSON {#change-rendering}

O JSON é renderizado como está em um `pre` tag, o que não é muito criativo. Em vez disso, podemos configurar o CodePen para usar a função `resultToDom()`, para ilustrar como a resposta JSON pode ser iterada para criar um resultado mais interessante.

1. Para fazer essa alteração, comente na linha 37 e remova o comentário da linha 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Essa função também renderizará quaisquer imagens incluídas na resposta JSON como uma tag `img`. Se a variável **Aventura** fragmentos de conteúdo criados não incluem imagens, você pode tentar alternar para usar o `aem-demo-assets/adventures-all` consulta persistente modificando a linha 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Essa consulta produzirá uma resposta JSON que inclui imagens, e a função `resultToDom()` as renderizará em linha.

![Resultado da consulta adventures-all e da função de renderização resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Agora que você concluiu o trabalho para criar os modelos e consultas, sua equipe de conteúdo pode assumir o controle com facilidade. Mostraremos o fluxo do autor de conteúdo no próximo módulo.
