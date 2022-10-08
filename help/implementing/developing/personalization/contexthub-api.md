---
title: Referência de API do Javascript do ContextHub
description: A API Javascript do ContextHub está disponível para seus scripts quando o componente ContextHub foi adicionado à página
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '4622'
ht-degree: 3%

---

# Referência de API do Javascript do ContextHub {#contexthub-javascript-api-reference}

A API Javascript do ContextHub está disponível para seus scripts quando a variável [O componente ContextHub foi adicionado à página](adding-contexthub.md).

## Constantes do ContextHub {#contexthub-constants}

Valores constantes que a API Javascript do ContextHub define.

### Constantes do evento {#event-constants}

A tabela a seguir lista os nomes dos eventos que ocorrem para as lojas do ContextHub. Consulte também [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Constante | Descrição | Valor |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Namespace do evento do ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica que todas as lojas necessárias estão registradas, inicializadas e prontas para serem consumidas | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica que nem todos os armazenamentos foram inicializados dentro de um determinado tempo limite | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Disparado quando uma loja é registrada | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica que as lojas estão prontas para funcionar. É acionado imediatamente após o registro, exceto armazenamentos JSONP, onde é acionado quando os dados são buscados). | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Disparado quando um armazenamento atualiza sua persistência | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nome do contêiner de persistência | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Armazena o nome da chave de persistência específica onde o resultado JSON bruto é armazenado | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Armazena um carimbo de data e hora específico que indica quando os dados JSON foram obtidos | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Armazena url específico do serviço JSON usado durante a última chamada | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica se a interface do usuário do ContextHub foi expandida | `/_/container-expanded` |

### Constantes de evento da interface do usuário {#ui-event-constants}

A tabela a seguir lista os nomes dos eventos que ocorrem para a interface do usuário do ContextHub.

| **Constante** | **Descrição** | **Valor** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Disparado quando um modo é registrado | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Acionado quando um modo não está registrado | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Acionado quando um renderizador de modo é registrado | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Acionado quando um renderizador de modo não está registrado | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Acionado quando um novo modo é adicionado | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Acionado quando um modo é removido | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Acionado quando um modo é selecionado pelo usuário | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Acionado quando um novo módulo é registrado | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Acionado quando um módulo não está registrado | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Acionado quando um renderizador de módulo é registrado | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Acionado quando um renderizador de módulo não está registrado | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Acionado quando um novo módulo é adicionado | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Acionado quando um módulo é removido | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Acionado quando o contêiner da interface do usuário é adicionado à página | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Acionado quando a interface do usuário do ContextHub é aberta | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Acionado quando a interface do usuário do ContextHub é recolhida | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Acionado quando uma propriedade é modificada | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Acionada sempre que a interface do usuário do ContextHub é renderizada (por exemplo, após uma alteração de propriedade) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Disparado quando o contêiner da interface do usuário é inicializado | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica o modo de interface do usuário ativo | `/_/active-ui-mode` |

## Referência de API do Javascript do ContextHub {#contexthub-javascript-api-reference-2}

O objeto ContextHub fornece acesso a todos os armazenamentos.

### Funções (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Retorna todos os armazenamentos registrados do ContextHub.

Essa função não tem parâmetros.

##### Retorna {#returns-}

Um objeto que contém todos os armazenamentos do ContextHub. Cada loja é um objeto que usa o mesmo nome da loja.

##### Exemplo {#example-}

O exemplo a seguir recupera todos os armazenamentos e recupera o armazenamento de geolocalização:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera uma loja como um objeto Javascript.

##### Parâmetros {#parameters-}

* **`name`:** O nome com o qual a loja foi registrada.

##### Retorna {#returns-getstore-name}

Um objeto que representa o armazenamento.

##### Exemplo {#example-getstore-name}

O exemplo a seguir recupera o armazenamento de geolocalização:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Representa um segmento do ContextHub. Use o `ContextHub.SegmentEngine.SegmentManager` para obter segmentos.

### Funções (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Retorna o nome do segmento como um valor de String.

#### getPath() {#getpath}

Retorna o caminho do repositório da definição do segmento como um valor de String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornece acesso aos segmentos do ContextHub.

### Funções (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Retorna os segmentos que são resolvidos no contexto atual. Essa função não tem parâmetros.

##### Retorna {#returns-getresolvedsegments}

Uma matriz de `ContextHub.SegmentEngine.Segment` objetos.

## ContextHub.Store.Core {#contexthub-store-core}

A classe base dos armazenamentos do ContextHub.

### Propriedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) objeto. Use esse objeto para vincular funções a fim de armazenar eventos. Para obter informações sobre o valor padrão e a inicialização, consulte [`init(name,config)`](#init-name-config).

#### name {#name}

O nome da loja.

#### persistência {#persistence}

A `ContextHub.Utils.Persistence` objeto. Para obter informações sobre o valor padrão e a inicialização, consulte [`init(name,config)`](#init-name-config).

### Funções (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Une um objeto de dados ou uma matriz aos dados da loja. Cada par de chave/valor no objeto ou na matriz é adicionado ao armazenamento (por meio do `setItem` função):

* **Objeto:** Chaves são os nomes de propriedade.
* **Matriz:** Chaves são os índices de matriz.

Observe que os valores podem ser objetos.

##### Parâmetros {#parameters-addallitems}

* **`tree`:** (Objeto ou matriz) Os dados a serem adicionados ao armazenamento.
* **`options`:** (Objeto) Um objeto opcional de opções passado para a função setItem . Para obter informações, consulte o `options` parâmetro de [`setItem(key,value,options)`](#setitem-key-value-options).

##### Retorna {#returns-addallitems}

A `boolean` valor:

* Um valor de `true` indica que o objeto de dados foi armazenado.
* Um valor de `false` indica que o armazenamento de dados permanece inalterado.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Cria uma referência de uma chave para outra chave. Uma chave não pode fazer referência a si mesma.

##### Parâmetros {#parameters-addreference}

* **`key`:** A chave que faz referência a `anotherKey`.

* **`anotherkey`:** A chave referenciada por `key`.

##### Retorna {#returns-addreference}

A `boolean` valor:

* Um valor de `true` indica que a referência foi adicionada.
* Um valor de `false` indica que nenhuma referência foi adicionada.

#### advertisingReadiness() {#announcereadiness}

Dispara o `ready` para esta loja. Essa função não tem parâmetros e não retorna valor.

#### clean() {#clean}

Remove todos os dados do armazenamento. A função não tem parâmetros e nenhum valor de retorno.

#### getItem(key) {#getitem-key}

Retorna o valor associado a uma chave.

##### Parâmetros {#parameters-getitem}

* **`key`:** (String) A chave para a qual retornar o valor.

##### Retorna {#returns-getitem}

Um Objeto que representa o valor da chave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera as chaves da loja. Opcionalmente, é possível recuperar as chaves usadas internamente pela estrutura do ContextHub.

##### Parâmetros {#parameters-getkeys}

* **`includeInternals`:** Um valor de `true` inclui chaves usadas internamente nos resultados. Essas chaves começam com o sublinhado (`_`). O valor padrão é `false`.

##### Retorna {#returns-getkeys}

Uma matriz de nomes de chaves ( `string` valores).

#### getReferences() {#getreferences}

Recupera as referências da loja.

##### Retorna {#returns-getreferences}

Uma matriz que usa chaves de referência como índices para as chaves referenciadas:

* As teclas de referência correspondem à variável `key` do `addReference` .
* As chaves referenciadas correspondem à função `anotherKey` do `addReference` .

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera a árvore de dados do armazenamento. Opcionalmente, é possível incluir os pares chave/valor usados internamente pela estrutura do ContextHub.

##### Parâmetros {#parameters-gettree}

* `includeInternals:` Um valor de `true` O inclui pares de chave/valor usados internamente nos resultados. As chaves desses dados começam com o sublinhado (`_`). O valor padrão é `false`.

##### Retorna {#returns-gettree}

Um objeto que representa a árvore de dados. As chaves são os nomes de propriedade do objeto.

#### init(name, config) {#init-name-config}

Inicializa o armazenamento.

* Define os dados do armazenamento para um objeto vazio.
* Define as referências de armazenamento para um objeto vazio.
* O `eventChannel` é `data:<name>`, onde `<name>` é o nome da loja.
* O `storeDataKey` é `/store/<name>`, onde `<name>` é o nome da loja.

##### Parâmetros {#parameters-init}

* **`name`:** O nome da loja.
* **`config`:** Um objeto que contém propriedades de configuração:
   * `eventDeferring`: O valor padrão é 32.
   * `eventing`: O [ContextHub.Utils.Eventing](#contexthub-utils-eventing) para esta loja. O valor padrão é o `ContextHub.eventing` O objeto usa.
   * `persistence`: O `ContextHub.Utils.Persistence` para esta loja. O valor padrão é o `ContextHub.persistence` objeto.

#### isEventingPaused() {#iseventingpaused}

Determina se o evento está pausado para esta loja.

##### Retorna {#returns-iseventingpaused}

Um valor booleano:

* `true`: O evento é pausado para que nenhum evento seja acionado para esta loja.
* `false`: Os eventos não são pausados para que sejam acionados para esta loja.

#### pauseEventing() {#pauseeventing}

Pausa o evento para a loja para que nenhum evento seja acionado. Essa função não requer parâmetros e não retorna valor.

#### removeItem(key, options) {#removeitem-key-options}

Remove um par de chave/valor do armazenamento.

Quando uma chave é removida, a função aciona a variável `data` evento. Os dados do evento incluem o nome do armazenamento, o nome da chave que foi removida, o valor que foi removido, o novo valor para a chave (nulo) e o tipo de ação &quot;remover&quot;.

Como opção, você pode impedir o acionamento da variável `data` evento.

##### Parâmetros {#parameters-removeitem}

* **`key`:** (String) O nome da chave a ser removida.
* **`options`:** (Objeto) Um objeto de opções. As seguintes propriedades de objeto são válidas:
   * silencioso: Um valor de `true` impede o acionamento da variável `data` evento. O valor padrão é `false`.

##### Retorna {#returns-removeitem}

A `boolean` valor:

* Um valor de `true` indica que o par chave/valor foi removido.
* Um valor de `false` indica que o armazenamento de dados permanece inalterado, pois a chave não foi encontrada no armazenamento.

#### removeReference(key) {#removereference-key}

Remove uma referência da loja.

##### Parâmetros {#parameters-removereference}

* **`key`:** A referência de chave a ser removida. Esse parâmetro corresponde à variável `key` do `addReference` .

##### Retorna {#returns-removereference}

A `boolean` valor:

* Um valor de `true` indica que a referência foi removida.
* Um valor de `false` indica que a chave não era válida e que a loja permanece inalterada.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Redefine os valores iniciais dos dados persistentes do armazenamento. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para esta loja enquanto ela é redefinida. Essa função não retorna valor.

Os valores iniciais são fornecidos na variável `initialValues` propriedade do objeto config usado para instanciar o objeto store.

##### Parâmetros {#parameters-reset}

* **`keepRemainingData`**: (Booleano) Um valor true faz com que os dados não iniciais sejam persistentes. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera uma chave referenciada. Como opção, você pode especificar o número de iterações a serem usadas para resolver a melhor correspondência.

##### Parâmetros {#parameters-resolvereference}

* **`key`:** (String) A chave para a qual resolver a referência. Essa `key` corresponde ao parâmetro `key` do `addReference` .
* **`retry`:** (Número) O número de iterações a serem usadas.

##### Retorna {#returns-resolvereference}

A `string` que representa a chave referenciada. Se nenhuma referência for resolvida, o valor da variável `key` é retornado.

#### resumeEventing() {#resumeeventing}

Retoma o evento para esta loja para que os eventos sejam acionados. Essa função não define parâmetros e não retorna valor.

#### setItem(key, value, options) {#setitem-key-value-options}

Adiciona um par de chave/valor à loja.

Dispara o `data` somente se o valor da chave for diferente do valor armazenado para a chave no momento. Opcionalmente, é possível impedir o acionamento da variável `data` evento.

Os dados do evento incluem o nome da loja, a chave, o valor anterior, o novo valor e o tipo de ação de `set`.

##### Parâmetros {#parameters-setitem}

* **`key`:** (String) O nome da chave.
* **`options`:** (Objeto) Um objeto de opções. As seguintes propriedades de objeto são válidas:
   * `silent`: Um valor de `true` impede o acionamento da variável `data` evento. O valor padrão é `false`.
* **`value`:** (Objeto) O valor a ser associado à chave.

##### Retorna {#returns-setitem}

A `boolean` valor:

* Um valor de `true` indica que o objeto de dados foi armazenado.
* Um valor de `false` indica que o armazenamento de dados permanece inalterado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Um armazenamento que contém dados JSON. Os dados são recuperados de um serviço JSONP externo ou, opcionalmente, de um serviço que retorna dados JSON. Especifique os detalhes do serviço usando o [`init`](#init-name-config) ao criar uma instância dessa classe.

O armazenamento usa persistência na memória (variável Javascript). Os dados de armazenamento estão disponíveis somente durante a vida útil da página.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](#contexthub-store-core) e herda as funções dessa classe.

### Funções (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura os detalhes para conexão com o serviço JSONP que este objeto usa. Você pode atualizar ou substituir a configuração existente. A função não retorna valor.

##### Parâmetros {#parameters-configureservice}

* **`serviceConfig`:** Um objeto que contém as seguintes propriedades:
   * `host`: (String) O nome do servidor ou endereço IP.
   * `jsonp`: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, o {retorno de chamada: &quot;ContextHub.Callbacks.*Object.name* O objeto } é adicionado ao objeto service.params .
   * `params`: (Objeto) Parâmetros de URL representados como propriedades de objetos. Os nomes de parâmetros são nomes de propriedades e os valores de parâmetros são valores de propriedades.
   * `path`: (String) O caminho para o serviço.
   * `port`: (Número) O número da porta do serviço.
   * `secure`: (String ou Boolean) Determina o protocolo a ser usado para o URL do serviço:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **substituição:** (Booleano). Um valor de `true` faz com que a configuração de serviço existente seja substituída pelas propriedades de `serviceConfig`. Um valor de `false` faz com que as propriedades de configuração do serviço existentes sejam mescladas com as propriedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Retorna a resposta bruta armazenada em cache desde a última chamada para o serviço JSONP. A função não requer parâmetros.

##### Retorna {#returns-getrawresponse}

Um objeto que representa a resposta bruta.

#### getServiceDetails() {#getservicedetails}

Recupera o objeto de serviço para este objeto ContextHub.Store.JSONPStore. O objeto de serviço contém todas as informações necessárias para criar o URL de serviço.

##### Retorna {#returns-getservicedetails}

Um objeto com as seguintes propriedades:

* **`host`:** (String) O nome do servidor ou endereço IP.
* **`jsonp`:** (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, o {retorno de chamada: &quot;ContextHub.Callbacks.*Object.name* O objeto } é adicionado ao objeto service.params .
* **`params`:** (Objeto) Parâmetros de URL representados como propriedades de objetos. Os nomes de parâmetros são nomes de propriedades e os valores de parâmetros são valores de propriedades.
* **`path`:** (String) O caminho para o serviço.
* **`port`:** (Número) O número da porta do serviço.
* **`secure`:** (String ou Boolean) Determina o protocolo a ser usado para o URL do serviço:
   * `auto`: //
   * `true`: https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera o URL do serviço JSONP.

##### Parâmetros {#parameters-getserviceurl}

* **`resolve`:** (Booleano) Determina se os parâmetros resolvidos devem ser incluídos no URL. Um valor de `true` resolve parâmetros e `false` não.

##### Retorna {#returns-getserviceurl}

A `string` que representa o URL do serviço.

#### init(name, config) {#init-name-config-1}

inicializa o `ContextHub.Store.JSONPStore` objeto.

##### Parâmetros {#parameters-init-1}

* **`name`:** (String) O nome do armazenamento.
* **`config`:** (Objeto) Um objeto que contém a propriedade de serviço. O objeto JSONPStore usa as propriedades da variável `service` para construir o URL do serviço JSONP:
   * `eventDeferring`: 32.
   * `eventing`: O objeto ContextHub.Utils.Eventing para esta loja. O valor padrão é o `ContextHub.eventing` objeto.
   * `persistence`: O objeto ContextHub.Utils.Persistence para esta loja. Por padrão, a persistência de memória é usada (objeto Javascript).
   * `service`: (Objeto)
      * `host`: (String) O nome do servidor ou endereço IP.
      * `jsonp`: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, a variável `{callback: "ContextHub.Callbacks.*Object.name*}`objeto é adicionado a `service.params`.
      * `params`: (Objeto) Parâmetros de URL representados como propriedades de objetos. Nomes e valores de parâmetros são os nomes e valores da propriedade de objeto, respectivamente.
      * `path`: (String) O caminho para o serviço.
      * `port`: (Número) O número da porta do serviço.
      * `secure`: (String ou Boolean) Determina o protocolo a ser usado para o URL do serviço:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Número) A quantidade de tempo para aguardar a resposta do serviço JSONP antes de atingir o tempo limite, em milissegundos.
         * `ttl`: O tempo mínimo, em milissegundos, que passa entre as chamadas para o serviço JSONP. (Consulte o [queryService](#queryservice-reload) ).

#### queryService(reload) {#queryservice-reload}

Consulta o serviço JSONP remoto e armazena em cache a resposta. Se a quantidade de tempo desde a chamada anterior para essa função for menor que o valor de `config.service.ttl`, o serviço não é chamado e a resposta em cache não é alterada. Como opção, você pode forçar a chamada do serviço. O `config.service.ttl`é definida ao chamar a variável [init](#init-name-config) para inicializar o armazenamento.

Aciona o evento ready quando o query for concluído. Se o URL do serviço JSONP não estiver definido, a função não fará nada.

##### Parâmetros {#parameters-queryservice}

* **`reload`:** (Booleano) Um valor true remove a resposta em cache e força o serviço JSONP a ser chamado.

#### reset {#reset}

Redefine os valores iniciais dos dados persistentes do armazenamento e, em seguida, chama o serviço JSONP. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para esta loja enquanto os valores iniciais são redefinidos. Essa função não retorna valor.

Os valores iniciais são fornecidos na propriedade initialValues do objeto de configuração que é usado para instanciar o objeto de armazenamento.

##### Parâmetros {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Um valor true faz com que os dados não iniciais sejam persistentes. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveParameter(f) {#resolveparameter-f}

Resolve o parâmetro especificado.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` estende [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) portanto, ela herda todas as funções dessa classe. No entanto, os dados recuperados do serviço JSONP são mantidos de acordo com a configuração de persistência do ContextHub. (Consulte [Modos de persistência:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` estende [ContextHub.Store.Core](#contexthub-store-core) portanto, ela herda todas as funções dessa classe. Os dados nesse armazenamento são mantidos de acordo com a configuração da persistência do ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` estende [ContextHub.Store.Core](#contexthub-store-core) portanto, ela herda todas as funções dessa classe. Os dados nesse armazenamento são mantidos com persistência na memória (objeto Javascript).

## ContextHub.UI {#contexthub-ui}

Gerencia módulos de interface e renderizadores de módulo de interface do usuário.

### Funções (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra um renderizador de módulo de interface do usuário com o ContextHub. Depois que o renderizador é registrado, ele pode ser usado para [criar módulos de interface](configuring-contexthub.md#adding-a-ui-module). Use esta função quando você [extensão `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) para criar um renderizador de Módulo de interface do usuário personalizado.

##### Parâmetros {#parameters-registerrenderer}

* **`moduleType`:** (String) O identificador do renderizador do módulo da interface do usuário. Se um renderizador já estiver registrado usando o valor especificado, o renderizador existente não será registrado antes que esse renderizador seja registrado.
* **`renderer`:** (String) O nome da classe que renderiza o módulo da interface do usuário.
* **`dontRender`:** (Booleano) Defina como `true` para impedir que a interface do usuário do ContextHub seja renderizada depois que o renderizador for registrado. O valor padrão é `false`.

##### Exemplo {#example-registerrenderer}

O exemplo a seguir registra um renderizador como `contexthub.browserinfo` tipo de módulo.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Uma classe de utilitário para interagir com cookies.

### Funções (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se um cookie existe.

##### Parâmetros {#parameters-exists}

* **`key`:** A `String` que contém a chave do cookie para o qual você está testando.

##### Retorna {#returns-exists}

A `boolean` valor true indica que o cookie existe.

##### Exemplo {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Retorna todos os cookies que têm chaves que correspondem a um filtro.

##### Parâmetros {#parameters-getallitems}

* **`filter`:** (Opcional) Critérios para corresponder a chaves de cookie. Para retornar todos os cookies, não especifique nenhum valor. Os seguintes tipos são suportados:
   * Sequência de caracteres: A string é comparada à chave do cookie.
   * Matriz: Cada item na matriz é um filtro.
   * Um objeto RegExp: A função de teste do objeto é usada para corresponder às chaves do cookie.
   * Uma função: Uma função que testa uma chave de cookie para obter uma correspondência. A função deve assumir a chave do cookie como parâmetro e retornar true se o teste confirmar uma correspondência.

##### Retorna {#returns-getallitems}

Um objeto de cookies. As propriedades do objeto são chaves de cookie e os valores-chave são valores de cookie.

##### Exemplo {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Retorna um valor de cookie.

##### Parâmetros {#parameters-getitem-1}

* **`key`:** A chave do cookie para o qual você deseja obter o valor.

##### Retorna {#returns-getitem-1}

O valor do cookie ou `null` se nenhum cookie foi encontrado para a chave.

##### Exemplo {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Retorna uma matriz das chaves dos cookies existentes que correspondem a um filtro.

##### Parâmetros {#parameters-getkeys-1}

* **`filter`:** Critérios para corresponder chaves de cookie. Os seguintes tipos são suportados:
   * Sequência de caracteres: A string é comparada à chave do cookie.
   * Matriz: Cada item na matriz é um filtro.
   * Um objeto RegExp: A função de teste do objeto é usada para corresponder às chaves do cookie.
   * Uma função: Uma função que testa uma chave de cookie para obter uma correspondência. A função deve assumir a chave do cookie como parâmetro e retornar `true` se o teste confirmar uma correspondência.

##### Retorna {#returns-getkeys-1}

Uma matriz de strings na qual cada string é a chave de um cookie que corresponde ao filtro.

##### Exemplo {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Remove um cookie. Para remover o cookie, o valor é definido como uma string vazia e a data de expiração é definida como o dia antes da data atual.

##### Parâmetros {#parameters-removeitem-1}

* **`key`:** A `String` que representa a chave do cookie a ser removido.
* **`options`:** Um objeto que contém valores de propriedade para configurar os atributos do cookie. Consulte a [`setItem`](#setitem-key-value-options) para obter mais informações. O `expires` não tem efeito.

##### Retorna {#returns-removeitem-1}

Essa função não retorna um valor.

##### Exemplo {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Cria um cookie da chave e valor fornecidos e adiciona o cookie ao documento atual. Como opção, você pode especificar opções que configuram os atributos do cookie.

##### Parâmetros {#parameters-setitem-1}

* **`key`:** Uma String que contém a chave do cookie.
* **`value`:** Uma String que contém o valor do cookie.
* **`options`:** (Opcional) Um objeto que contém qualquer uma das seguintes propriedades que configuram os atributos do cookie:
   * `expires`: A `date` ou `number` que especifica quando o cookie expira. Um valor de data especifica o tempo absoluto de expiração. Um número (em dias) define o tempo de expiração para a hora atual mais o número. O valor padrão é `undefined`.
   * `secure`: A `boolean` que especifica a variável `Secure` do cookie. O valor padrão é `false`.
   * `path`: A `String` valor a ser usado como o `Path` do cookie. O valor padrão é `undefined`.

##### Retorna {#returns-setitem-1}

O cookie com o valor definido.

##### Exemplo {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Remove todos os cookies que correspondem a um determinado filtro. Os cookies são correspondidos usando a variável `getKeys` e removidas usando a função `removeItem` .

##### Parâmetros {#parameters-vanish}

* **`filter`:** O `filter` argumento a ser usado na chamada para o [`getKeys`](#getkeys-filter) .
* **`options`:** O `options` argumento a ser usado na chamada para o [`removeItem`](#removeitem-key-options) .

##### Retorna {#returns-vanish}

Essa função não retorna um valor.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Permite vincular e desvincular funções a eventos de armazenamento do ContextHub. Acesso `ContextHub.Utils.Eventing` objetos para um armazenamento usando o [evento](#eventing) da loja.

### Funções (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(nome, seletor) {#off-name-selector}

Desvincula uma função de um evento.

##### Parâmetros {#parameters-off}

* **`name`:** O [nome do evento](#contexthub-utils-eventing) para a qual você está desvinculando a função .
* **`selector`:** O seletor que identifica o vínculo. (Consulte o `selector` para o [`on`](#on-name-handler-selector-triggerforpastevents) e [`once`](#once-name-handler-selector-triggerforpastevents) funções).

##### Retorna {#returns-off}

Essa função não retorna valor.

#### on(name, handler, seletor, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada sempre que o evento ocorre. Como opção, a função pode ser chamada para eventos que ocorreram no passado, antes que o vínculo seja estabelecido.

##### Parâmetros {#parameters-on}

* **`name`:** (String) O [nome do evento](#contexthub-utils-eventing) à qual você está vinculando a função.
* **`handler`:** (Função) A função a ser vinculada ao evento.
* **`selector`:** (String) Um identificador exclusivo para o vínculo. Você precisa do seletor para identificar o vínculo se deseja usar o `off` para remover o vínculo.
* **`triggerForPastEvents`:** (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor de `true` chama o manipulador para eventos anteriores. Um valor de `false` chama o manipulador para eventos futuros. O valor padrão é `true`.

##### Retorna {#returns-on}

Quando a variável `triggerForPastEvents` argumento é `true`, essa função retorna um `boolean` que indica se o evento ocorreu no passado:

* `true`: O evento ocorreu no passado e o manipulador será chamado.
* `false`: O evento não ocorreu no passado.

If `triggerForPastEvents` é `false`, essa função não retorna valor.

##### Exemplo {#example-on}

O exemplo a seguir vincula uma função ao evento de dados do armazenamento de geolocalização. A função preenche um elemento na página com o valor do item de dados de latitude da loja.

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, seletor, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada somente uma vez, para a primeira ocorrência do evento. Como opção, a função pode ser chamada para o evento que ocorreu no passado, antes que o vínculo seja estabelecido.

##### Parâmetros {#parameters-once}

* **`name`:** (String) O [nome do evento](#contexthub-utils-eventing) à qual você está vinculando a função.
* **`handler`:** (Função) A função a ser vinculada ao evento.
* **`selector`:** (String) Um identificador exclusivo para o vínculo. Você precisa do seletor para identificar o vínculo se deseja usar o `off` para remover o vínculo.
* **`triggerForPastEvents`:** (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor de `true` chama o manipulador para eventos anteriores. Um valor de `false` chama o manipulador para eventos futuros. O valor padrão é `true`.

##### Retorna {#returns-once}

Quando a variável `triggerForPastEvents` argumento é `true`, essa função retorna um `boolean` que indica se o evento ocorreu no passado:

* `true`: O evento ocorreu no passado e o manipulador será chamado.
* `false`: O evento não ocorreu no passado.

If `triggerForPastEvents` é `false`, essa função não retorna valor.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Uma classe de utilitário que permite a um objeto herdar as propriedades e os métodos de outro objeto.

### Funções (ContextHub.Utils.hereditance) {#functions-contexthub-utils-inheritance}

#### herdar(filho, pai) {#inherit-child-parent}

Faz com que um objeto herde as propriedades e os métodos de outro objeto.

##### Parâmetros {#parameters-inherit}

* **`child`:** (Objeto) O objeto que herda.
* **`parent`:** (Objeto) O objeto que define as propriedades e os métodos herdados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornece funções para serializar objetos no formato JSON e desserializar cadeias JSON em objetos.

### Funções (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analisa um valor de string como JSON e o converte em um objeto javascript.

##### Parâmetros {#parameters-parse}

* **`data`:** Um valor de string no formato JSON.

##### Retorna {#returns-parse}

Um objeto Javascript.

##### Exemplo {#example-parse}

O código:

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

Retorna o seguinte objeto:

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializa valores e objetos Javascript em valores de string de formato JSON.

##### Parâmetros {#parameters-stringify}

* **`data`:** O valor ou objeto a ser serializado. Essa função suporta valores booleanos, de matriz, de número, de string e de data.

##### Retorna {#returns-stringify}

O valor da string serializada. When `data` é um R `egExp` , essa função retorna um objeto vazio. When `data` é uma função, retorna `undefined`.

##### Exemplo {#example-stringify}

O código a seguir:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Retorna:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Essa classe facilita a manipulação de objetos de dados que serão armazenados ou recuperados de armazenamentos do ContextHub.

### Funções (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Cria uma cópia de um objeto de dados e adiciona a ele a árvore de dados de um segundo objeto. A função retorna a cópia e não modifica nenhum dos objetos originais. Quando as árvores de dados dos dois objetos contêm chaves idênticas, o valor do segundo objeto substitui o valor do primeiro objeto.

##### Parâmetros {#parameters-addallitems-1}

* **`tree`:** O objeto que é copiado.
* **`secondTree`:** O objeto que é unido à cópia do `tree` objeto.

##### Retorna {#returns-addallitems-1}

Um objeto que contém os dados unidos.

#### cleanup() {#cleanup}

Cria uma cópia de um objeto, localiza e remove itens na árvore de dados que não contêm valores, valores nulos ou valores indefinidos e retorna a cópia.

##### Parâmetros {#parameters-cleanup}

* **`tree`:** O objeto a ser limpo.

##### Retorna {#returns-cleanup}

Uma cópia da árvore que é limpa.

#### getItem() {#getitem}

Recupera o valor de um objeto para a chave a.

##### Parâmetros {#parameters-getitem-2}

* **`tree`:** O objeto de dados.
* **`key`:** A chave do valor que você deseja recuperar.

##### Retorna {#returns-getitem-2}

O valor que corresponde à chave. Quando a chave tem chaves secundárias, essa função retorna um objeto complexo. Quando o tipo do valor da chave é `undefined`, `null` é retornado.

##### Exemplo {#example-getitem-2}

Considere o seguinte objeto Javascript:

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

O código de exemplo a seguir retorna o valor `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

O código de exemplo a seguir recupera o valor de uma chave que tenha chaves secundárias:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

A função retorna o seguinte objeto:

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera todas as chaves da árvore de dados de um objeto. Como opção, você pode recuperar apenas as chaves dos filhos de uma chave específica. Opcionalmente, também é possível especificar uma ordem de classificação das chaves recuperadas.

##### Parâmetros {#parameters-getkeys-2}

* **`tree`:** O objeto do qual recuperar as chaves da árvore de dados.
* **`parent`:** (Opcional) A chave de um item na árvore de dados para a qual você deseja recuperar as chaves dos itens filhos.
* **`order`:** (Opcional) Uma função que determina a ordem de classificação das chaves retornadas. (Consulte [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) no Mozilla Developer Network.)

##### Retorna {#returns-getkeys-2}

Uma matriz de chaves.

##### Exemplo {#example-getkeys-2}

Considere o seguinte objeto:

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

O `ContextHub.Utils.JSON.tree.getKeys(myObject);` o script retorna a seguinte matriz:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Cria uma cópia de um determinado objeto, remove a ramificação especificada da árvore de dados e retorna a cópia modificada.

##### Parâmetros {#parameters-removeitem-2}

* **`tree`:** Um objeto de dados.
* **`key`:** A chave a ser removida.

##### Retorna {#returns-removeitem-2}

Uma cópia do objeto de dados original com a chave removida.

##### Exemplo {#example-removeitem-2}

Considere o seguinte objeto:

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

O script de exemplo a seguir remove a ramificação /um/dois/três/quatro da árvore de dados:

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

A função retorna o seguinte objeto:

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Limpa os valores da sequência de caracteres para torná-los utilizáveis como chaves. Para limpar uma string, essa função executa as seguintes ações:

* Reduz várias barras consecutivas para a frente em uma única barra.
* Remove o espaço em branco do início e do fim da cadeia de caracteres.
* Divide o resultado em uma matriz de strings demarcadas por barras.

Use a matriz resultante para criar uma chave utilizável.

##### Parâmetros {#parameters-sanitizekey}

* **`key`:** O `string` para purificar.

##### Retorna {#returns-sanitizekey}

Uma matriz de `string` valores em que cada string é a parte da variável `key` que foi demarcada por barras. representa a chave sanitizada. Se a matriz sanitizada tiver um comprimento de zero, essa função retornará `null`.

##### Exemplo {#example-sanitizekey}

O código a seguir limpa uma string para produzir a matriz `["this", "is", "a", "path"]`e então gera a chave `"/this/is/a/path"` do storage:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Adiciona um par chave/valor à árvore de dados de uma cópia de um objeto. Para obter informações sobre árvores de dados, consulte [Persistência.](contexthub.md#persistence)

##### Parâmetros {#parameters-setitem-2}

* **`tree`:** Um objeto de dados.
* **`key`:** A chave para associar ao valor que você está adicionando. A chave é o caminho para o item na árvore de dados. Essa função chama `ContextHub.Utils.JSON.tree.sanitize` para limpar a chave antes de adicioná-la.
* **`value`:** O valor a ser adicionado à árvore de dados.

##### Retorna {#returns-setitem-2}

Uma cópia do `tree` que inclui a variável `key`/ `value` par.

##### Exemplo {#example-setitem-2}

Considere o seguinte código Javascript:

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Permite registrar candidatos a lojas e obter candidatos a lojas registradas.

### Funções (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Retorna os tipos de loja que são registrados como candidatos de loja. Recupere os candidatos registrados de um tipo de armazenamento específico ou de todos os tipos de armazenamento.

##### Parâmetros {#parameters-getregisteredcandidates}

* **`storeType`:** (String) O nome do tipo de armazenamento. Consulte a `storeType` do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) .

##### Retorna {#returns-getregisteredcandidates}

Um objeto de tipos de armazenamento. As propriedades do objeto são os nomes do tipo de armazenamento e os valores da propriedade são uma matriz de candidatos a armazenamento registrado.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Retorna um tipo de armazenamento dos candidatos registrados. Se mais de um tipo de armazenamento do mesmo nome for registrado, a função retornará o tipo de armazenamento com a prioridade mais alta.

##### Parâmetros {#parameters-getstorefromcandidates}

* `storeType`: (String) O nome do candidato da loja. Consulte a `storeType` do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) .

##### Retorna {#returns-getstorefromcandidates}

Um objeto que representa o candidato de armazenamento registrado. Se o Tipo de armazenamento solicitado não estiver registrado, um erro será lançado.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Retorna os nomes dos tipos de loja que estão registrados como candidatos de loja. Essa função não requer parâmetros.

##### Retorna {#returns-getsupportedstoretypes}

Uma matriz de valores da string, em que cada string é o tipo de armazenamento com o qual um candidato a loja foi registrado. Consulte a `storeType` do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) .

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra um objeto de loja como candidato de loja usando um nome e uma prioridade.

A prioridade é um número que indica a importância das lojas com mesmo nome. Quando um candidato de loja é registrado usando o mesmo nome de um candidato de loja já registrado, o candidato com prioridade mais alta é usado. Ao registrar um candidato a loja, a loja é registrada somente se a prioridade for maior que os candidatos a loja registrada com o mesmo nome.

##### Parâmetros {#parameters-registerstorecandidate}

* **`store`:** (Objeto) O objeto de armazenamento a ser registrado como candidato de loja.
* **`storeType`:** (String) O nome do candidato da loja. Esse valor é necessário ao criar uma instância do candidato de loja.
* **`priority`:** (Número) A prioridade do candidato à loja.
* **`applies`:** (Função) A função para invocar que avalia a aplicabilidade da loja no ambiente atual. A função deve retornar `true` se o armazém for aplicável, e `false` caso contrário. O valor padrão é uma função que retorna true: `function() {return true;}`

##### Exemplo {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
