---
title: Como atualizar seu conteúdo por meio das APIs do AEM Assets
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho AEM, saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 0c47dec1e96fc3137d17fc3033f05bf1ae278141
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 3%

---

# Como atualizar seu conteúdo por meio das APIs do AEM Assets {#update-your-content}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada do desenvolvedor sem cabeçalho,](overview.md) saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como acessar o conteúdo por meio AEM APIs de entrega](access-your-content.md) você aprendeu a acessar o conteúdo sem periféricos no AEM por meio da API GraphQL AEM e agora deve:

* Ter um alto nível de compreensão do GraphQL.
* Entenda como a API GraphQL AEM funciona.
* Entenda algumas consultas práticas de amostra.

Este artigo se baseia nesses fundamentos para que você entenda como atualizar o conteúdo headless existente no AEM por meio da REST API.

## Objetivo {#objective}

* **Público-alvo**: Avançado
* **Objetivo**: Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo:
   * Apresente a API HTTP do AEM Assets.
   * Apresente e discuta o suporte ao Fragmento de conteúdo na API.
   * Ilustre detalhes da API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Por que você precisa da API HTTP de ativos para o Fragmento de conteúdo {#why-http-api}

No estágio anterior da Jornada Sem cabeçalho, você aprendeu a usar a API GraphQL da AEM para recuperar o conteúdo usando consultas.

Então, por que outra API é necessária?

A API HTTP do Assets permite **Ler** o seu conteúdo, mas também permite **Criar**, **Atualizar** e **Eliminar** conteúdo - ações que não são possíveis com a API GraphQL.

## API HTTP de ativos {#assets-http-api}

A [API HTTP de ativos](/help/assets/mac-api-assets.md) abrange:

* API REST de ativos
* incluindo suporte para Fragmentos de conteúdo

A implementação atual da API HTTP de ativos é baseada no estilo arquitetônico **REST**.

A API REST de ativos permite que os desenvolvedores do Adobe Experience Manager as a Cloud Service acessem o conteúdo (armazenado em AEM) diretamente sobre a API HTTP, por meio de operações **CRUD** (Criar, Ler, Atualizar, Excluir).

A API permite operar o Adobe Experience Manager as a Cloud Service como um CMS (Content Management System) sem periféricos fornecendo serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON.

Por exemplo, Aplicativos de página única (SPA), baseados em estrutura ou personalizados, exigem conteúdo fornecido por meio de uma API, geralmente no formato JSON.

Embora AEM os Componentes principais forneçam uma API muito abrangente, flexível e personalizável que possa servir as operações de Leitura necessárias para essa finalidade e cuja saída JSON possa ser personalizada, eles exigem AEM know-how WCM (Gerenciamento de conteúdo da Web) para implementação, pois devem ser hospedados em páginas baseadas em modelos de AEM dedicados. Nem todas as organizações SPA de desenvolvimento têm acesso direto a esses conhecimentos.

É quando a API REST do Assets pode ser usada. Ela permite que os desenvolvedores acessem ativos (por exemplo, imagens e fragmentos de conteúdo) diretamente, sem a necessidade de primeiro incorporá-los a uma página e entregar seu conteúdo em formato JSON serializado.

>[!NOTE]
>
>Não é possível personalizar a saída JSON da API REST de ativos.

A API REST de ativos também permite que os desenvolvedores modifiquem o conteúdo, criando ativos novos, atualizados ou excluindo ativos, fragmentos de conteúdo e pastas existentes.

A API REST de ativos:

* segue o princípio HATEOAS
* implementa o formato SIREN

## Pré-requisitos {#prerequisites}

A API REST de ativos está disponível em cada instalação pronta para uso de uma versão recente do Adobe Experience Manager as a Cloud Service.

## Principais conceitos {#key-concepts}

A API REST de ativos oferece acesso ao estilo REST a ativos armazenados em uma instância de AEM.

Ele usa o terminal `/api/assets` e requer o caminho do ativo para acessá-lo (sem o `/content/dam` à esquerda).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Você precisa solicitar:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acesso ao:
>
>* `/api/assets` **não** precisa do uso do  `.model` seletor.
>* `/content/path/to/page` **** Não requer o uso do  `.model` seletor.


O método HTTP determina a operação a ser executada:

* **GET**  - para recuperar uma representação JSON de um ativo ou uma pasta
* **POST**  - para criar novos ativos ou pastas
* **PUT**  - para atualizar as propriedades de um ativo ou pasta
* **DELETE**  - para excluir um ativo ou uma pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, defina que uma pasta ou um ativo deve ser criado por uma solicitação **POST**.

O formato exato das solicitações compatíveis é definido na documentação de Referência da API.

### Comportamento transacional {#transactional-behavior}

Todas as solicitações são atômicas.

Isso significa que as solicitações subsequentes (`write`) não podem ser combinadas em uma única transação que pode ter êxito ou falhar como uma única entidade.

### AEM (Ativos) REST API versus AEM Componentes {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API REST de ativos<br/> </td>
   <td>Componente AEM<br/> (componentes que usam Modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso suportados</td>
   <td>Finalidade geral.</td>
   <td><p>Otimizado para consumo em um Aplicativo de página única (SPA), ou qualquer outro contexto (que consome conteúdo).</p> <p>Também pode conter informações de layout.</p> </td>
  </tr>
  <tr>
   <td>Operações suportadas</td>
   <td><p>Criar, Ler, Atualizar, Excluir.</p> <p>Com operações adicionais, dependendo do tipo de entidade.</p> </td>
   <td>Somente leitura.</td>
  </tr>
  <tr>
   <td>Acesso</td>
   <td><p>Pode ser acessado diretamente.</p> <p>Usa o ponto de extremidade <code>/api/assets </code>mapeado para <code>/content/dam</code> (no repositório).</p> 
   <p>Um caminho de exemplo seria: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Precisa ser referenciado por meio de um componente de AEM em uma página de AEM.</p> <p>Usa o seletor <code>.model</code> para criar a representação JSON.</p> <p>Um caminho de exemplo seria:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Segurança</td>
   <td><p>Várias opções são possíveis.</p> <p>O OAuth é proposto; pode ser configurado separadamente da configuração padrão.</p> </td>
   <td>Usa AEM configuração padrão.</td>
  </tr>
  <tr>
   <td>Observações arquitetônicas</td>
   <td><p>O acesso de gravação normalmente endereçará uma instância de autor.</p> <p>A leitura também pode ser direcionada a uma instância de publicação.</p> </td>
   <td>Como essa abordagem é somente leitura, ela normalmente será usada para instâncias de publicação.</td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Saída SIREN baseada em JSON: verboso, mas poderoso. Permite navegar dentro do conteúdo.</td>
   <td>Saída proprietária baseada em JSON; configurável por meio de Modelos do Sling. É difícil implementar a navegação na estrutura de conteúdo (mas não é necessariamente impossível).</td>
  </tr>
 </tbody>
</table>

### Segurança {#security}

Se a API REST do Assets for usada em um ambiente sem requisitos de autenticação específicos, AEM filtro CORS precisará ser configurado corretamente.

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Explicação do CORS/AEM
>* Vídeo - Desenvolvimento do CORS com AEM

>



Em ambientes com requisitos de autenticação específicos, o OAuth é recomendado.

## Recursos disponíveis {#available-features}

Fragmentos de conteúdo são um tipo específico de ativo, consulte Trabalhar com fragmentos de conteúdo .

Para obter mais informações sobre recursos disponíveis por meio da API, consulte:

* A API REST do Assets
* Tipos de entidade, onde os recursos específicos para cada tipo suportado (conforme relevante para Fragmentos de conteúdo) são explicados

### Paginação {#paging}

A API REST de ativos suporta paginação (para solicitações do GET) por meio dos parâmetros de URL:

* `offset` - o número da primeira entidade (filho) a recuperar
* `limit` - o número máximo de entidades devolvidas

A resposta conterá informações de paginação como parte da seção `properties` da saída SIREN. Esta propriedade `srn:paging` contém o número total de entidades (filho) ( `total`), o deslocamento e o limite ( `offset`, `limit`) conforme especificado na solicitação.

>[!NOTE]
>
>A paginação normalmente é aplicada em entidades de contêiner (ou seja, pastas ou ativos com representações), pois está relacionada aos filhos da entidade solicitada.

#### Exemplo: Paginação {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipos de entidade {#entity-types}

### Pastas {#folders}

As pastas atuam como contêineres para ativos e outras pastas. Eles refletem a estrutura do repositório de conteúdo AEM.

A API REST do Assets expõe o acesso às propriedades de uma pasta; por exemplo, seu nome, título etc. Os ativos são expostos como entidades filhas de pastas e subpastas.

>[!NOTE]
>
>Dependendo do tipo de ativo dos ativos e pastas filhos, a lista de entidades filhas já pode conter o conjunto completo de propriedades que define a respectiva entidade filho. Como alternativa, apenas um conjunto reduzido de propriedades pode ser exposto para uma entidade nesta lista de entidades-filho.

### Assets {#assets}

Se um ativo for solicitado, a resposta retornará seus metadados; como título, nome e outras informações conforme definido pelo respectivo schema de ativos.

Os dados binários de um ativo são expostos como um link SIREN do tipo `content`.

Os ativos podem ter várias representações. Normalmente, elas são expostas como entidades secundárias, sendo uma exceção uma representação em miniatura, que é exposta como um link do tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de conteúdo {#content-fragments}

Um Fragmento de conteúdo é um tipo especial de ativo. Eles podem ser usados para acessar dados estruturados, como textos, números, datas, entre outros.

Como há várias diferenças nos ativos *padrão* (como imagens ou áudio), algumas regras adicionais se aplicam ao seu manuseio.

#### Representação {#representation}

Fragmentos de conteúdo:

* Não exponha quaisquer dados binários.
* Estão completamente contidos na saída JSON (dentro da propriedade `properties` ).

* Também são considerados atômicos, ou seja, os elementos e as variações são expostos como parte das propriedades do fragmento vs. como links ou entidades filhas. Isso permite acesso eficiente à carga de um fragmento.

#### Modelos de conteúdo e fragmentos de conteúdo {#content-models-and-content-fragments}

Atualmente, os modelos que definem a estrutura de um fragmento de conteúdo não são expostos por meio de uma API HTTP. Portanto, o *consumidor* precisa saber sobre o modelo de um fragmento (pelo menos um mínimo) - embora a maioria das informações possa ser inferida da carga; como tipos de dados, etc. fazem parte da definição.

Para criar um novo fragmento de conteúdo, o caminho (repositório interno) do modelo deve ser fornecido.

#### Conteúdo associado {#associated-content}

O conteúdo associado não está exposto no momento.

## Uso da API REST do Assets {#using-aem-assets-rest-api}

Para obter detalhes sobre como usar a API REST do AEM Assets, é possível fazer referência a:

* API HTTP do Adobe Experience Manager Assets
* Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets

## O que vem a seguir {#whats-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda a API HTTP do AEM Assets.
* Entenda como os Fragmentos de conteúdo são compatíveis com essa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

Você deve continuar sua jornada sem periféricos de AEM ao revisar o documento [Como colocar tudo junto - Seu aplicativo e seu conteúdo em AEM sem periféricos](put-it-all-together.md), onde você aprenderá a executar seu projeto sem periféricos de AEM e prepará-lo para entrar ao vivo.

## Recursos adicionais {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [Princípio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)
* [Formato SIREN](https://github.com/kevinswiber/siren)
* [API HTTP de ativos](/help/assets/mac-api-assets.md)
* [API REST de fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [Referência da API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
* [AEM Core Components](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)
* [Explicação do CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Vídeo - Desenvolvimento do CORS com AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

