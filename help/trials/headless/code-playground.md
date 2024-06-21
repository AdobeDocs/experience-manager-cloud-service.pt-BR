---
title: Renderize o conteúdo em um aplicativo simples
description: Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo de exemplo CodePen e o AEM Headless Client para JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 96%

---


# Renderize o conteúdo em um aplicativo simples {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Renderize o conteúdo em um aplicativo simples"
>abstract="Explore a busca de conteúdo JSON do seu ambiente de avaliação com um aplicativo de exemplo CodePen e o AEM Headless Client para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Inicie o aplicativo CodePen de exemplo"
>abstract="Este guia aborda a consulta de dados JSON do seu ambiente de avaliação em um aplicativo web JavaScript básico. Você usa os Fragmentos de conteúdo modelados e criados nos módulos de aprendizado anteriores. Se necessário, analise primeiro esses guias antes de pular para este."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="Neste módulo, você aprendeu a usar o AEM Headless Client para JavaScript para buscar dados JSON de seu ambiente de avaliação usando consultas persistentes de GraphQL.<br><br>Agora você sabe como pode usar esse cliente para consumir dados de seu próprio aplicativo web."
>abstract=""

## CodePen {#codepen}

O CodePen é um editor de código online e um playground para desenvolvimento web de front-end. Ele permite gerar códigos HTML, CSS e JavaScript em seu navegador e ver os resultados de seu trabalho quase que instantaneamente. Também é possível salvar seu trabalho e compartilhá-lo com outras pessoas. Criamos um aplicativo no CodePen que você pode usar para buscar dados JSON de seu ambiente de avaliação usando o [AEM Headless Client para JavaScript](https://github.com/adobe/aem-headless-client-js). É possível usar este aplicativo como está ou copiá-lo para sua própria conta do CodePen para personalizá-lo ainda mais.

Ao clicar no botão **Iniciar o aplicativo CodePen de exemplo** na versão de avaliação, você será direcionado(a) para o aplicativo no CodePen. O aplicativo é um exemplo mínimo de busca de dados JSON com JavaScript. O aplicativo de exemplo foi desenvolvido para renderizar qualquer conteúdo JSON que seja retornado, independentemente da estrutura do modelo de fragmento de conteúdo subjacente. O aplicativo busca imediatamente os dados de uma consulta persistente `aem-demo-assets` incluída no seu ambiente de avaliação. Você deve ver uma resposta JSON semelhante ao seguinte:

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

Caso veja um erro, verifique o console do navegador para obter mais detalhes ou entre em contato com [por e-mail](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request).

Agora que você sabe um pouco sobre o CodePen, você configurará o aplicativo para buscar dados da consulta persistente criada em um módulo anterior.

## Passo a passo do código JavaScript {#code-walkthrough}

O painel **JS** à direita no CodePen contém o Javascript do aplicativo de exemplo. Começando na linha 2, você importa o AEM Headless Client para JavaScript da CDN do Skypack. O Skypack é usado para facilitar o desenvolvimento sem uma etapa de criação, mas você também pode usar o AEM Headless Client com o NPM ou Yarn em seus próprios projetos. Confira as instruções de uso no arquivo [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obter mais detalhes.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Na linha 6, os detalhes do host de publicação foram lidos no parâmetro de consulta `publishHost`. Esse parâmetro é o host do qual o AEM Headless Client busca os dados. Normalmente, a funcionalidade seria codificada no aplicativo, mas você está usando um parâmetro de consulta para facilitar o trabalho do aplicativo CodePen com ambientes diferentes.

Você configura o AEM Headless Client na linha 12:

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
>O **serviceURL** está definido para usar uma função proxy do Adobe I/O Runtime para evitar problemas de CORS. Esse proxy não é obrigatório nos seus próprios projetos, mas é necessário para que o aplicativo CodePen funcione no ambiente de avaliação. A função de proxy está configurada para usar o valor **publishHost** que foi fornecido no parâmetro de consulta.

Por fim, a função `fetchJsonFromGraphQL()` é usada para executar a solicitação de busca usando o AEM Headless Client. Ela é chamada sempre que o código é alterado, ou pode ser acionada utilizando a opção **Buscar novamente**. A chamada `aemHeadlessClient.runPersistedQuery(..)` ocorre na linha 34. Mais à frente, faremos uma alteração na forma como esses dados JSON são renderizados, mas por enquanto vamos registrá-los no div `#output` usando a função `resultToPreTag(queryResult)`.

## Buscar dados da sua consulta persistente {#use-persisted-query}

Na linha 25, indicamos de qual consulta persistente de GraphQL o aplicativo deve buscar dados. O nome da consulta persistente é uma combinação do nome do ponto de acesso (ou seja, `your-project` ou `aem-demo-assets`) seguido por uma barra e o nome da consulta. Se você seguiu exatamente as instruções do módulo anterior, a consulta persistente criada estará no ponto de acesso `your-project`.

1. Atualize a variável `persistedQueryName` para que use a consulta persistente criada no módulo anterior. Se você seguiu a sugestão de nomenclatura, uma consulta persistente chamada `adventure-list` deve ter sido criada no ponto de acesso `your-project` e agora você deve definir a variável `persistedQueryName` como `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Depois que essa alteração for feita, o aplicativo deve ser atualizado automaticamente e imprimir a resposta JSON bruta da sua consulta persistente no div `#output`. Se uma mensagem de erro aparecer, verifique o console para obter mais detalhes. Alcance [por e-mail](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request) se você ainda tiver problemas com essa etapa.

1. Esse JSON contém as propriedades exatas de que seu aplicativo precisa? Caso contrário, volte para o guia de aprendizagem [Extrair conteúdo usando a API GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) para fazer alterações. Não se esqueça de salvar e publicar a consulta depois que terminar.

## Alterar a renderização JSON {#change-rendering}

O JSON é renderizado como está em uma tag `pre`, o que não é muito criativo. Podemos também alternar o CodePen para usar a função `resultToDom()` para ilustrar como a resposta JSON pode ser iterada, a fim de criar um resultado mais interessante.

1. Para fazer essa alteração, comente na linha 37 e remova o comentário da linha 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Essa função renderizará quaisquer imagens incluídas na resposta JSON como uma tag `img`. Se os fragmentos de conteúdo de **Aventura** criados não incluírem imagens, tente alternar para o uso da consulta persistente `aem-demo-assets/adventures-all`, modificando a linha 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Essa consulta produzirá uma resposta JSON que inclui imagens, e a função `resultToDom()` as renderizará em linha.

![Resultado da consulta adventures-all e da função de renderização resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Agora que você criou os modelos e consultas, sua equipe de conteúdo pode assumir o controle com facilidade. No próximo módulo, haverá a exibição do fluxo de criação de conteúdo.
