---
title: Uso do GraphiQL IDE no AEM
description: Saiba como usar o GraphiQL IDE no Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 377747d6bbb945b1de9cf1fdcbabc077babd7aa9
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 66%

---

# Uso do GraphiQL IDE {#graphiql-ide}

Uma implementação do [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE padrão está disponível para uso com a API GraphQL do Adobe Experience Manager (AEM) as a Cloud Service.

>[!NOTE]
>
>O GraphiQL é incluído em todos os ambientes de AEM (mas só estará acessível/visível quando você configurar os pontos de extremidade).
>
>Em versões anteriores, era necessário um pacote para instalar o GraphiQL IDE. Se você tiver isso instalado, ele poderá ser removido.

>[!NOTE]
>Você deve [configurar os endpoints](/help/headless/graphql-api/graphql-endpoint.md) no [navegador de configuração](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md) antes de usar o GraphiQL IDE.


A ferramenta **GraphiQL** permite testar e depurar as consultas de GraphQL, possibilitando:
* selecionar o **endpoint** apropriado à configuração de Sites que deseja usar para as consultas
* inserir diretamente novas consultas
* criar e acessar **[consultas persistentes](/help/headless/graphql-api/persisted-queries.md)**
* executar as consultas para ver os resultados imediatamente
* gerenciar **variáveis de consulta**
* salvar e gerenciar **consultas persistentes**
* publicar ou desfazer a publicação, **Consultas Persistentes** (por exemplo, para/de `dev-publish`)
* consultar o **histórico** de consultas anteriores
* usar o **Explorador de documentação** para acessar a documentação; ajudando você a conhecer e entender quais métodos estão disponíveis.

Você pode acessar o editor de consultas por meio de:

* **Ferramentas** -> **Geral** -> **Editor de consultas GraphQL**
* Diretamente; por exemplo, `http://localhost:4502/aem/graphiql.html`

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

Você pode usar GraphiQL no sistema para que as consultas possam ser solicitadas pelo aplicativo cliente usando solicitações GET e para publicação de consultas. Para o uso da produção, é possível [mover suas consultas para o ambiente de produção](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inicialmente ao autor de produção para validação do conteúdo recém-criado com as consultas e, finalmente, à produção de publicação para consumo em tempo real.

## Seleção do endpoint {#selecting-endpoint}

Como primeira etapa, é preciso selecionar o **[endpoint](/help/headless/graphql-api/graphql-endpoint.md)** que deseja usar para as consultas. O endpoint é apropriado para a configuração dos Sites que você deseja usar para as consultas.

Isso está disponível na lista suspensa na parte superior direita.

## Criação e persistência de uma nova consulta {#creating-new-query}

Você pode inserir a nova consulta no editor, que está no painel central esquerdo, diretamente sob o logotipo do GraphiQL.

>[!NOTE]
>
>Se você tiver uma consulta persistente já selecionada que está sendo exibida no painel do editor, selecione `+` (ao lado de **Consultas persistentes**) para esvaziar o editor para sua nova consulta.

Basta começar a digitar. O editor também:

* mostra informações adicionais sobre os elementos ao passar o mouse sobre eles
* fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática

>[!NOTE]
>
>As consultas de GraphQL normalmente começam com um caractere `{`.
>
>Linhas que começam com `#` são ignoradas.

Use a opção **Salvar como** para criar uma consulta persistente.

## Atualização da consulta persistente {#updating-persisted-query}

Selecione a consulta que deseja atualizar na lista do painel **Consultas persistentes** (lado esquerdo).

A consulta será exibida no painel do editor. Faça as alterações necessárias e use a opção **Salvar** para confirmar as atualizações da consulta persistente.

## Execução de consultas {#running-queries}

Você pode executar uma nova consulta imediatamente ou pode carregar e executar uma consulta persistente. Para carregar uma consulta persistente, selecione-a na lista — a consulta será exibida no painel do editor.

Em ambos os casos, a consulta exibida no painel do editor é a que será executada quando você:

* clicar/tocar no ícone **Executar consulta**
* usar a combinação de teclado `Control-Enter`

## Variáveis de consulta {#query-variables}

<!-- more details needed here? -->

O GraphiQL IDE também permite gerenciar as [Variáveis de consulta](/help/headless/graphql-api/content-fragments.md#graphql-variables).

Por exemplo:

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

## Gerenciamento do cache para suas consultas persistentes {#managing-cache}

[Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) são recomendadas, pois podem ser armazenadas em cache nas camadas do dispatcher e CDN, melhorando o desempenho do aplicativo cliente solicitante. Por padrão, o AEM invalidará o cache da Rede de entrega de conteúdo (CDN) com base em um Time To Live (TTL) padrão.

Usando GraphQL, você pode configurar os HTTP Cache Headers para controlar esses parâmetros para sua consulta persistente individual.

1. O **Cabeçalhos** é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda):

   ![Cabeçalhos de Cache HTTP de Consulta Persistente](assets/cfm-graphqlapi-headers-01.png "Cabeçalhos de Cache HTTP de Consulta Persistente")

1. Selecionar isso abrirá o **Configuração de cache** caixa de diálogo:

   ![Configurações Persistentes do Cabeçalho HTTP do Cache](assets/cfm-graphqlapi-headers-02.png "Configurações Persistentes do Cabeçalho HTTP do Cache")

1. Selecione o parâmetro apropriado e ajuste o valor conforme necessário:

   * **controle de cache** - **max-age**
Os caches podem armazenar esse conteúdo por um número especificado de segundos. Normalmente, esse é o TTL (Time To Live) do navegador.
   * **controle de substitutos** - **s-maxage**
Igual à idade máxima, mas aplica-se especificamente a caches proxy.
   * **controle de substitutos** - **stale-while-revalidate**
Os caches podem continuar a servir uma resposta em cache depois que ela se tornar obsoleta, por até o número especificado de segundos.
   * **controle de substitutos** - **stale-if-error**
Os caches podem continuar a servir uma resposta em cache em caso de erro de origem ou de origem, por até o número especificado de segundos.

1. Selecionar **Salvar** para persistir as alterações.

## Publicação de consultas persistentes {#publishing-persisted-queries}

Depois de selecionar a consulta persistente na lista (painel esquerdo), você pode usar as ações **Publicar** e **Desfazer a publicação**. Isso os ativará no ambiente de publicação (por exemplo, `dev-publish`) para facilitar o acesso de seus aplicativos ao testar.

>[!NOTE]
>
>A definição do cache da consulta persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} tem um valor padrão de 2 horas (7200 segundos).

## Copiar o URL para acessar a consulta diretamente {#copy-url}

A opção **Copiar URL** permite simular uma consulta copiando o URL usado para acessar diretamente a consulta persistente e ver os resultados. Essa opção pode ser usada para testes; por exemplo, acessando em um navegador:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Por exemplo:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Ao usar esse URL em um navegador, é possível confirmar os resultados:

![GraphiQL - Copiar URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copiar URL")

A opção **Copiar URL** é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda):

![GraphiQL - Copiar URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copiar URL")

## Exclusão de consultas persistentes {#deleting-persisted-queries}

A opção **Excluir** também é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda).

<!-- what happens if you try to delete something that is still published? -->


## Instalação da consulta persistente na produção {#installing-persisted-query-production}

Depois de desenvolver e testar a consulta persistente com o GraphiQL, o objetivo final é [transferi-la para o ambiente de produção](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) para que os aplicativos possam usá-la.

## Atalhos de teclado {#keyboard-shortcuts}

Há uma série de atalhos de teclado que fornecem acesso direto aos ícones de ação no IDE:

* Adornar a consulta: `Shift-Control-P`
* Mesclar consulta: `Shift-Control-M`
* Executar consulta: `Control-Enter`
* Preenchimento automático: `Control-Space`

>[!NOTE]
>
>Em alguns teclados, a tecla `Control` é rotulada como `Ctrl`.
