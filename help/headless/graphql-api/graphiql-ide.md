---
title: Uso do GraphiQL IDE no AEM
description: Saiba como usar o GraphiQL IDE no Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: dfcad7aab9dda7341de3dc4975eaba9bdfbd9780
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 4%

---

# Uso do GraphiQL IDE {#graphiql-ide}

Uma implementação do padrão [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) O IDE está disponível para uso com a API GraphQL da Adobe Experience Manager (AEM) as a Cloud Service.

>[!NOTE]
>
>Parte da funcionalidade desse recurso está disponível no canal de pré-lançamento. Especificamente, a funcionalidade relacionada a Consultas Persistentes.
> 
>Consulte a [Documentação do Canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obter informações sobre como habilitar o recurso para seu ambiente.

>[!NOTE]
>
>O GraphiQL está incluído no AEM, mas por padrão só está ativado no `dev-authors` ambientes .

>[!NOTE]
>Você deve ter [configurou os endpoints](/help/headless/graphql-api/graphql-endpoint.md) no [navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md) antes de usar o GraphiQL IDE.


O **GraphiQL** A ferramenta permite testar e depurar as consultas GraphQL, permitindo:
* selecione o **Endpoint** apropriado à configuração de Sites que você deseja usar para suas consultas
* inserir diretamente novos queries
* criar e acessar, **[Consultas Persistentes](/help/headless/graphql-api/persisted-queries.md)**
* execute suas consultas para ver imediatamente os resultados
* gerenciar **Variáveis de consulta**
* salvar e gerenciar **Consultas Persistentes**
* publicar ou desfazer a publicação, **Consultas Persistentes** (a/de `dev-publish`)
* consulte o **Histórico** das suas consultas anteriores
* use o **Explorador de documentação** para acessar a documentação; ajudando você a saber e entender quais métodos estão disponíveis.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

Você pode usar o GraphiQL em seu sistema de criação de desenvolvimento para que ele possa ser solicitado pelo aplicativo cliente usando solicitações do GET e publicando consultas. Para o uso da produção, é necessário [mover suas consultas para o ambiente de produção](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inicialmente para autor de produção para validar conteúdo recém-criado com os queries e, por fim, para publicar em tempo real.

## Seleção do terminal {#selecting-endpoint}

Como primeira etapa, você precisa selecionar a variável **[Endpoint](/help/headless/graphql-api/graphql-endpoint.md)** que você deseja usar para os queries. O endpoint é apropriado para a configuração de Sites que você deseja usar para as consultas.

Isso está disponível na lista suspensa na parte superior direita.

## Criação e persistência de um novo query {#creating-new-query}

Você pode inserir seu novo query no editor, que é no painel do meio esquerdo, diretamente sob o logotipo GraphiQL.

>[!NOTE]
>
>Se você tiver uma consulta persistente já selecionada e exibida no painel do editor, selecione `+` (ao lado de **Consultas Persistentes**) para esvaziar o editor pronto para sua nova consulta.

Basta começar a digitar, o editor também:

* O usa o mouse sobre ele para mostrar informações adicionais sobre elementos
* fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática

>[!NOTE]
>
>As consultas GraphQL normalmente começam com um `{` caractere.
>
>Linhas que começam com um `#` são ignoradas.

Use **Salvar como** para continuar sua nova consulta.

## Atualização da consulta persistente {#updating-persisted-query}

Selecione a consulta que deseja atualizar na lista de **Consultas Persistentes** painel (extrema esquerda).

A consulta será mostrada no painel do editor. Faça as alterações necessárias e use **Salvar** para confirmar suas atualizações na consulta persistente.

## Execução de consultas {#running-queries}

Você pode executar um novo query imediatamente ou pode carregar e executar um query persistente. Para carregar uma consulta persistente, selecione-a na lista - a consulta será mostrada no painel do editor.

Em ambos os casos, a consulta exibida no painel do editor é a que será executada quando você:

* clique/toque no **Executar Consulta** ícone
* usar a combinação de teclado `Control-Enter`

## Variáveis de consulta {#query-variables}

<!-- more details needed here? -->

O GraphiQL IDE também permite gerenciar seu [Variáveis de consulta](/help/headless/graphql-api/content-fragments.md#graphql-variables).

Por exemplo:

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

## Publicação de consultas persistentes (dev-publish) {#publishing-persisted-queries}

Depois de selecionar sua consulta persistente na lista (painel esquerdo), você pode usar o **Publicar** e **Cancelar publicação** ações. Isso os ativará no ambiente de publicação de desenvolvimento (`dev-publish`) para facilitar o acesso de seus aplicativos durante os testes.

>[!NOTE]
>
>A definição do cache do query persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} tem um valor padrão de 2 horas (7200 segundos).

## Armazenamento em cache de suas consultas persistentes {#caching-persisted-queries}

AEM invalidará o cache da Rede de entrega de conteúdo (CDN) com base em um Time To Live (TTL) padrão.

Esse valor é definido como:

* 7200 segundos é o TTL padrão para o Dispatcher e o CDN; também conhecido como *caches compartilhados*
   * padrão: s-maxage=7200
* 60 é o TTL padrão para o cliente (por exemplo, um navegador)
   * padrão: máximo=60

AEM consultas GraphQL que persistiram com a interface GraphiQL usarão o TTL padrão na execução. Se você quiser alterar o TTL para sua consulta GraphLQ, a consulta deverá ser mantida usando o método da API. Isso envolve postar a consulta em AEM usando CURL na interface da linha de comando.

Para um exemplo:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

O `cache-control` pode ser definido no momento da criação (PUT) ou posteriormente (por exemplo, por meio de uma solicitação de POST, por exemplo). O controle de cache é opcional ao criar a consulta persistente, pois AEM pode fornecer o valor padrão. Consulte [Como persistir uma consulta GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), para obter um exemplo de persistência de um query usando curl.

## Copiar URL para acessar diretamente a consulta {#copy-url}

O **Copiar URL** permite simular uma consulta, copiando o URL usado para acessar diretamente a consulta mantida e ver os resultados. Pode então ser utilizado para ensaios; por exemplo, acessando em um navegador:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Por exemplo:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Ao usar esse URL em um navegador, você pode confirmar os resultados:

![GraphiQL - Copiar URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copiar URL")

O **Copiar URL** é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda):

![GraphiQL - Copiar URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copiar URL")

## Excluindo consultas persistentes {#deleting-persisted-queries}

O **Excluir** também é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda).

<!-- what happens if you try to delete something that is still published? -->


## Instalar sua consulta persistente na produção {#installing-persisted-query-production}

Depois de desenvolver e testar sua consulta persistente com GraphiQL, o objetivo final é [transfira-o para o ambiente de produção](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) para uso pelos seus aplicativos.

## Atalhos de teclado {#keyboard-shortcuts}

Há uma seleção de atalhos de teclado que fornecem acesso direto a ícones de ação no IDE:

* Pretendir Consulta:  `Shift-Control-P`
* Consulta de Mesclagem:  `Shift-Control-M`
* Executar Consulta:  `Control-Enter`
* Conclusão automática:  `Control-Space`

>[!NOTE]
>
>Em alguns teclados, o `Control` é rotulada como `Ctrl`.
