---
title: Como atualizar seu conteúdo por meio das APIs do AEM Assets
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho AEM, saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 787af0d4994bf1871c48aadab74d85bd7c3c94fb
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 2%

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

A API REST de ativos está disponível em cada instalação pronta para uso de uma versão recente do Adobe Experience Manager as a Cloud Service.

## API HTTP de ativos {#assets-http-api}

A [API HTTP de ativos](/help/assets/mac-api-assets.md) abrange:

* API REST de ativos
* incluindo suporte para Fragmentos de conteúdo

A implementação atual da API HTTP de ativos é baseada no estilo arquitetônico **REST**.

A API REST de ativos permite que os desenvolvedores do Adobe Experience Manager as a Cloud Service acessem o conteúdo (armazenado em AEM) diretamente sobre a API HTTP, por meio de operações **CRUD** (Criar, Ler, Atualizar, Excluir).

Com essa operação, a API permite operar o Adobe Experience Manager como um Cloud Service como um CMS (Content Management System) sem periféricos fornecendo serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON. Por exemplo, Aplicativos de página única (SPA), baseados em estrutura ou personalizados, exigem conteúdo fornecido por meio de uma API, geralmente no formato JSON.

>[!NOTE]
>
>Não é possível personalizar a saída JSON da API REST de ativos.

A API REST de ativos:

* segue o princípio HATEOAS
* implementa o formato SIREN

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

### Segurança {#security}

Se a API REST do Assets for usada em um ambiente sem requisitos de autenticação específicos, AEM filtro CORS precisará ser configurado corretamente.

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Explicação do CORS/AEM
>* Vídeo - Desenvolvimento do CORS com AEM


Em ambientes com requisitos de autenticação específicos, o OAuth é recomendado.

## Recursos disponíveis {#available-features}

Fragmentos de conteúdo são um tipo específico de ativo, consulte Trabalhar com fragmentos de conteúdo .

Para obter mais informações sobre recursos disponíveis por meio da API, consulte:

* A API REST de ativos (recursos adicionais)
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

O uso pode ser diferente dependendo se você está usando um autor ou um ambiente de publicação AEM, juntamente com seu caso de uso específico.

* É altamente recomendável que a criação seja vinculada a uma instância do autor ([e atualmente não há como replicar um fragmento para publicar usando essa API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* A entrega é possível de ambos, pois AEM serve o conteúdo solicitado somente no formato JSON.

   * O armazenamento e o delivery de uma instância de autor de AEM devem ser suficientes para aplicativos de biblioteca de mídia por trás do firewall.

   * Para entrega na Web ao vivo, recomenda-se uma instância de publicação de AEM.

>[!CAUTION]
>
>A configuração do dispatcher em instâncias AEM nuvem pode bloquear o acesso a `/api`.

>[!NOTE]
>
>Para obter mais detalhes, consulte a [Referência da API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). Especificamente, [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html).

### Leitura/entrega {#read-delivery}

O uso é via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

A resposta é JSON serializado com o conteúdo estruturado como no fragmento de conteúdo. As referências são fornecidas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, a representação JSON do fragmento de conteúdo é retornada.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: isso retorna as representações JSON de todos os fragmentos de conteúdo dentro da pasta.

### Criar {#create}

O uso é via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a propriedade `cq:model` e deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, haverá um erro. Também é necessário adicionar um cabeçalho `Content-Type` que está definido como `application/json`.

### Atualizar {#update}

O uso é via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do que deve ser atualizado para o fragmento de conteúdo especificado.

Pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores e/ou metadados do elemento.

### Exclua {#delete}

O uso é via:

`DELETE /{cfParentPath}/{cfName}`

Para obter mais detalhes sobre o uso da API REST do AEM Assets, consulte:

* API HTTP do Adobe Experience Manager Assets (Recursos adicionais)
* Suporte a fragmentos de conteúdo na API HTTP do AEM Assets (Recursos adicionais)

## O que vem a seguir {#whats-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda as noções básicas da API HTTP do AEM Assets.
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

