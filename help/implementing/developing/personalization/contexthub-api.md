---
title: Referência da API JavaScript do ContextHub
description: A API JavaScript do ContextHub estará disponível para seus scripts quando o componente ContextHub for adicionado à página
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '4602'
ht-degree: 2%

---

# Referência da API JavaScript do ContextHub {#contexthub-javascript-api-reference}

A API JavaScript do ContextHub está disponível para seus scripts quando a variável [O componente ContextHub foi adicionado à página](adding-contexthub.md).

## Constantes do ContextHub {#contexthub-constants}

Valores de constante definidos pela API JavaScript do ContextHub.

### Constantes de evento {#event-constants}

A tabela a seguir lista os eventos de nomes que ocorrem para as Lojas do ContextHub. Consulte também [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Constante | Descrição | Valor |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Namespace de evento do ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica que todos os armazenamentos necessários estão registrados, inicializados e prontos para serem consumidos | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica que nem todos os armazenamentos foram inicializados dentro de um determinado tempo limite | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Acionado quando um armazenamento é registrado | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica que o armazenamento está pronto para funcionar. É acionado imediatamente após o registro, exceto armazenamentos JSONP, em que é acionado quando os dados são buscados). | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Acionado quando um armazenamento atualiza sua persistência | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nome do container de persistência | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Armazena um nome de chave de persistência específico onde o resultado JSON bruto é armazenado | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Armazena um carimbo de data e hora específico que indica quando os dados JSON foram buscados | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Armazena o URL específico do serviço JSON usado durante a última chamada | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica se a interface do usuário do ContextHub é expandida | `/_/container-expanded` |

### Constantes de evento da interface do usuário {#ui-event-constants}

A tabela a seguir lista os nomes dos eventos que ocorrem para a interface do usuário do ContextHub.

| **Constante** | **Descrição** | **Valor** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Acionado quando um modo é registrado | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Acionado quando um modo tem registro cancelado | `ui-mode-unregistered` |
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
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Acionado quando a interface do ContextHub é recolhida | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Acionado quando uma propriedade é modificada | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Acionado sempre que a interface do usuário do ContextHub é renderizada (por exemplo, após uma alteração de propriedade) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Acionado quando o contêiner da interface do usuário é inicializado | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica o modo da interface do usuário ativa | `/_/active-ui-mode` |

## Referência da API JavaScript do ContextHub {#contexthub-javascript-api-reference-2}

O objeto ContextHub fornece acesso a todos os armazenamentos.

### Funções (ContextHub) {#functions-contexthub}

#### getAllStores () {#getallstores}

Retorna todos os armazenamentos registrados do ContextHub.

Esta função não tem parâmetros.

##### Devoluções {#returns-}

Um objeto que contém todos os armazenamentos do ContextHub. Cada armazenamento é um objeto que usa o mesmo nome do armazenamento.

##### Exemplo {#example-}

O exemplo a seguir recupera todos os armazenamentos e, em seguida, recupera o armazenamento de geolocalização:

```javascript
var allStores = ContextHub.getAllStores ();
var geoloc = allStores.geolocation
```

#### getStore(nome) {#getstore-name}

Recupera um armazenamento como um objeto JavaScript.

##### Parâmetros {#parameters-}

* **`name`:** O nome com o qual o armazenamento foi registrado.

##### Devoluções {#returns-getstore-name}

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

Retorna o caminho do repositório da definição de segmento como um valor String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornece acesso aos segmentos do ContextHub.

### Funções (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments () {#getresolvedsegments}

Retorna os segmentos resolvidos no contexto atual. Esta função não tem parâmetros.

##### Devoluções {#returns-getresolvedsegments}

Uma matriz de `ContextHub.SegmentEngine.Segment` objetos.

## ContextHub.Store.Core {#contexthub-store-core}

A classe base para armazenamentos do ContextHub.

### Propriedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) objeto. Use esse objeto para funções de vinculação para armazenar eventos. Para obter informações sobre o valor default e a inicialização, consulte [`init(name,config)`](#init-name-config).

#### name {#name}

O nome do armazenamento.

#### persistência {#persistence}

A `ContextHub.Utils.Persistence` objeto. Para obter informações sobre o valor default e a inicialização, consulte [`init(name,config)`](#init-name-config).

### Funções (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems (árvore, opções) {#addallitems-tree-options}

Mescla um objeto de dados ou uma matriz com os dados armazenados. Cada par de chave/valor no objeto ou na matriz é adicionado ao armazenamento (por meio da variável `setItem` ):

* **Objeto:** Chaves são os nomes das propriedades.
* **Matriz:** As chaves são os índices da matriz.

Os valores podem ser objetos.

##### Parâmetros {#parameters-addallitems}

* **`tree`:** (Objeto ou matriz) Os dados a serem adicionados ao armazenamento.
* **`options`:** (Object) Um objeto opcional de opções passado para a função setItem. Para obter informações, consulte a `options` parâmetro de [`setItem(key,value,options)`](#setitem-key-value-options).

##### Devoluções {#returns-addallitems}

A `boolean` valor:

* Um valor de `true` indica que o objeto de dados foi armazenado.
* Um valor de `false` indica que o armazenamento de dados não foi alterado.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Cria uma referência de uma chave para outra. Uma chave não pode fazer referência a si mesma.

##### Parâmetros {#parameters-addreference}

* **`key`:** A chave que faz referência a `anotherKey`.

* **`anotherkey`:** A chave que é referenciada pelo `key`.

##### Devoluções {#returns-addreference}

A `boolean` valor:

* Um valor de `true` indica que a referência foi adicionada.
* Um valor de `false` indica que nenhuma referência foi adicionada.

#### announcementReadiness () {#announcereadiness}

Aciona o `ready` evento para esta loja. Esta função não tem parâmetros e não retorna nenhum valor.

#### clean() {#clean}

Remove todos os dados do armazenamento. A função não tem parâmetros e nenhum valor de retorno.

#### getItem(key) {#getitem-key}

Retorna o valor associado a uma chave.

##### Parâmetros {#parameters-getitem}

* **`key`:** (String) A chave para a qual retornar o valor.

##### Devoluções {#returns-getitem}

Um Objeto que representa o valor da chave.

#### getKeys (includeInternals) {#getkeys-includeinternals}

Recupera as chaves do armazenamento. Como opção, você pode recuperar as chaves usadas internamente pela estrutura do ContextHub.

##### Parâmetros {#parameters-getkeys}

* **`includeInternals`:** Um valor de `true` inclui chaves usadas internamente nos resultados. Essas teclas começam com um sublinhado (`_`). O valor padrão é `false`.

##### Devoluções {#returns-getkeys}

Uma matriz de nomes de chave ( `string` valores).

#### getReferences () {#getreferences}

Recupera as referências do armazenamento.

##### Devoluções {#returns-getreferences}

Uma matriz que usa chaves de referência como índices para as chaves referenciadas:

* As chaves de referência correspondem à variável `key` parâmetro do `addReference` função.
* As chaves referenciadas correspondem à variável `anotherKey` parâmetro do `addReference` função.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera a árvore de dados do armazenamento. Como opção, inclua os pares chave/valor usados internamente pela estrutura do ContextHub.

##### Parâmetros {#parameters-gettree}

* `includeInternals:` Um valor de `true` inclui pares de chave/valor usados internamente nos resultados. As chaves desses dados começam com um sublinhado (`_`). O valor padrão é `false`.

##### Devoluções {#returns-gettree}

Um objeto que representa a árvore de dados. As chaves são os nomes de propriedade do objeto.

#### init(nome, configuração) {#init-name-config}

Inicializa o armazenamento.

* Define os dados de armazenamento como um objeto vazio.
* Define as referências de armazenamento para um objeto vazio.
* A variável `eventChannel` é `data:<name>`, onde `<name>` é o nome da loja.
* A variável `storeDataKey` é `/store/<name>`, onde `<name>` é o nome da loja.

##### Parâmetros {#parameters-init}

* **`name`:** O nome do armazenamento.
* **`config`:** Um objeto que contém propriedades de configuração:
   * `eventDeferring`: O valor padrão é 32.
   * `eventing`: A variável [ContextHub.Utils.Eventing](#contexthub-utils-eventing) objeto para este armazenamento. O valor padrão é o `ContextHub.eventing` o objeto usa.
   * `persistence`: A variável `ContextHub.Utils.Persistence` objeto para este armazenamento. O valor padrão é o `ContextHub.persistence` objeto.

#### isEventingPaused() {#iseventingpaused}

Determina se o evento está pausado para este armazenamento.

##### Devoluções {#returns-iseventingpaused}

Um valor booleano:

* `true`: o evento é pausado para que nenhum evento seja acionado para esse armazenamento.
* `false`: o evento não é pausado para que os eventos sejam acionados para esse armazenamento.

#### pauseEventing() {#pauseeventing}

Pausa o evento do armazenamento para que nenhum evento seja acionado. Esta função não requer parâmetros e não retorna nenhum valor.

#### removeItem(chave, opções) {#removeitem-key-options}

Remove um par de chave/valor do armazenamento.

Quando uma tecla é removida, a função aciona o `data` evento. Os dados do evento incluem o nome do armazenamento, o nome da chave que foi removida, o valor que foi removido, o novo valor para a chave (nulo) e o tipo de ação de &quot;remover&quot;.

Como opção, você pode impedir o acionamento da variável `data` evento.

##### Parâmetros {#parameters-removeitem}

* **`key`:** (String) O nome da chave a ser removida.
* **`options`:** (Object) Um objeto de opções. As seguintes propriedades de objeto são válidas:
   * silencioso: um valor de `true` impede o acionamento da `data` evento. O valor padrão é `false`.

##### Devoluções {#returns-removeitem}

A `boolean` valor:

* Um valor de `true` indica que o par chave/valor foi removido.
* Um valor de `false` indica que o armazenamento de dados não foi alterado porque a chave não foi encontrada no armazenamento.

#### removeReference(key) {#removereference-key}

Remove uma referência do armazenamento.

##### Parâmetros {#parameters-removereference}

* **`key`:** A referência de chave a ser removida. Esse parâmetro corresponde à variável `key` parâmetro do `addReference` função.

##### Devoluções {#returns-removereference}

A `boolean` valor:

* Um valor de `true` indica que a referência foi removida.
* Um valor de `false` indica que a chave não era válida e o armazenamento não foi alterado.

#### redefinir(keepRemainingData) {#reset-keepremainingdata}

Redefine os valores iniciais dos dados persistentes do armazenamento. Como opção, você pode remover todos os outros dados do armazenamento. O evento está pausado para este armazenamento enquanto o armazenamento é redefinido. Esta função não retorna nenhum valor.

Os valores iniciais são fornecidos na variável `initialValues` propriedade do objeto de configuração usado para instanciar o objeto de armazenamento.

##### Parâmetros {#parameters-reset}

* **`keepRemainingData`**: (Booleano) um valor true faz com que os dados não iniciais sejam mantidos. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera uma chave referenciada. Opcionalmente, você pode especificar o número de iterações a serem usadas para resolver a melhor correspondência.

##### Parâmetros {#parameters-resolvereference}

* **`key`:** (String) A chave para a qual resolver a referência. Este `key` O parâmetro corresponde à variável `key` parâmetro do `addReference` função.
* **`retry`:** (Número) O número de iterações a serem usadas.

##### Devoluções {#returns-resolvereference}

A `string` que representa a chave referenciada. Se nenhuma referência for resolvida, o valor de `key` é retornado.

#### resumeEventing() {#resumeeventing}

Retoma os eventos deste armazenamento para que eles sejam acionados. Esta função não define parâmetros e não retorna nenhum valor.

#### setItem(chave, valor, opções) {#setitem-key-value-options}

Adiciona um par de chave/valor ao armazenamento.

Aciona o `data` evento somente se o valor da chave for diferente do valor armazenado no momento para a chave. Como opção, é possível impedir o acionamento da variável `data` evento.

Os dados do evento incluem o nome do armazenamento, a chave, o valor anterior, o novo valor e o tipo de ação de `set`.

##### Parâmetros {#parameters-setitem}

* **`key`:** (String) O nome da chave.
* **`options`:** (Object) Um objeto de opções. As seguintes propriedades de objeto são válidas:
   * `silent`: um valor de `true` impede o acionamento da `data` evento. O valor padrão é `false`.
* **`value`:** (Objeto) O valor a ser associado à chave.

##### Devoluções {#returns-setitem}

A `boolean` valor:

* Um valor de `true` indica que o objeto de dados foi armazenado.
* Um valor de `false` indica que o armazenamento de dados não foi alterado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Um armazenamento que contém dados JSON. Os dados são recuperados de um serviço JSONP externo ou, opcionalmente, de um serviço que retorna dados JSON. Especifique os detalhes do serviço usando o [`init`](#init-name-config) quando você cria uma ocorrência dessa classe.

O armazenamento usa a persistência na memória (variável JavaScript). Os dados de armazenamento estão disponíveis somente durante o tempo de vida da página.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](#contexthub-store-core) e herda as funções dessa classe.

### Funções (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, substituição) {#configureservice-serviceconfig-override}

Configura os detalhes para a conexão com o serviço JSONP que este objeto usa. Você pode atualizar ou substituir a configuração existente. A função não retorna nenhum valor.

##### Parâmetros {#parameters-configureservice}

* **`serviceConfig`:** Um objeto que contém as seguintes propriedades:
   * `host`: (String) O nome ou endereço IP do servidor.
   * `jsonp`: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, false. Quando verdadeiro, o {callback: &quot;ContextHub.Callbacks.*Objeto.nome*} é adicionado ao objeto service.params.
   * `params`: parâmetros de URL (Objeto) representados como propriedades de objeto. Os nomes dos parâmetros são nomes de propriedades e os valores dos parâmetros são valores de propriedades.
   * `path`: (String) O caminho para o serviço.
   * `port`: (Número) O número da porta do serviço.
   * `secure`: (String ou Booleano) Determina o protocolo a ser usado para o URL do serviço:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **substituir:** (Booleano). Um valor de `true` faz com que a configuração de serviço existente seja substituída pelas propriedades de `serviceConfig`. Um valor de `false` faz com que as propriedades de configuração do serviço existentes sejam mescladas com as propriedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Retorna a resposta bruta armazenada em cache desde a última chamada para o serviço JSONP. A função não requer parâmetros.

##### Devoluções {#returns-getrawresponse}

Um objeto que representa a resposta bruta.

#### getServiceDetails () {#getservicedetails}

Recupera o objeto de serviço para este objeto ContextHub.Store.JSONPStore. O objeto de serviço contém as informações necessárias para criar a URL do serviço.

##### Devoluções {#returns-getservicedetails}

Um objeto com as seguintes propriedades:

* **`host`:** (String) O nome do servidor ou endereço IP.
* **`jsonp`:** (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, false. Quando verdadeiro, o {callback: &quot;ContextHub.Callbacks.*Objeto.nome*} é adicionado ao objeto service.params.
* **`params`:** (Objeto) Parâmetros de URL representados como propriedades de objeto. Os nomes dos parâmetros são nomes de propriedades e os valores dos parâmetros são valores de propriedades.
* **`path`:** (String) O caminho para o serviço.
* **`port`:** (Número) O número da porta do serviço.
* **`secure`:** (String ou Booleano) Determina o protocolo a ser usado para o URL do serviço:
   * `auto`: //
   * `true`: https://
   * `false`: http://

#### getServiceURL(resolver) {#getserviceurl-resolve}

Recupera o URL do serviço JSONP.

##### Parâmetros {#parameters-getserviceurl}

* **`resolve`:** (Booleano) Determina se os parâmetros resolvidos devem ser incluídos no URL. Um valor de `true` resolve parâmetros, e `false` não.

##### Devoluções {#returns-getserviceurl}

A `string` valor que representa o URL do serviço.

#### init(nome, configuração) {#init-name-config-1}

inicializa o `ContextHub.Store.JSONPStore` objeto.

##### Parâmetros {#parameters-init-1}

* **`name`:** (String) O nome do armazenamento.
* **`config`:** (Objeto) Um objeto que contém a propriedade de serviço. O objeto JSONPStore usa as propriedades do `service` objeto para construir o URL do serviço JSONP:
   * `eventDeferring`: 32.
   * `eventing`: o objeto ContextHub.Utils.Eventing para esse armazenamento. O valor padrão é o `ContextHub.eventing` objeto.
   * `persistence`: o objeto ContextHub.Utils.Persistence desse armazenamento. Por padrão, a persistência de memória é usada (objeto JavaScript).
   * `service`: (Objeto)
      * `host`: (String) O nome ou endereço IP do servidor.
      * `jsonp`: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, false. Quando verdadeiro, a variável `{callback: "ContextHub.Callbacks.*Object.name*}`objeto é adicionado a `service.params`.
      * `params`: parâmetros de URL (Objeto) representados como propriedades de objeto. Os nomes e valores de parâmetros são os nomes e valores de propriedades de objetos, respectivamente.
      * `path`: (String) O caminho para o serviço.
      * `port`: (Número) O número da porta do serviço.
      * `secure`: (String ou Booleano) Determina o protocolo a ser usado para o URL do serviço:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Número) A quantidade de tempo para aguardar a resposta do serviço JSONP antes de atingir o tempo limite, em milissegundos.
         * `ttl`: o tempo mínimo em milissegundos decorrido entre chamadas para o serviço JSONP. (Consulte a [queryService](#queryservice-reload) função).

#### queryService(reload) {#queryservice-reload}

Consulta o serviço JSONP remoto e armazena a resposta em cache. Se o tempo desde a chamada anterior para essa função for menor que o valor de `config.service.ttl`, o serviço não é chamado e a resposta em cache não é alterada. Como opção, você pode forçar a chamada do serviço. A variável `config.service.ttl`é definida ao chamar a variável [init](#init-name-config) função para inicializar o armazenamento.

Aciona o evento pronto quando a consulta é concluída. Se o URL do serviço JSONP não estiver definido, a função não fará nada.

##### Parâmetros {#parameters-queryservice}

* **`reload`:** (Booleano) Um valor true remove a resposta em cache e força o serviço JSONP a ser chamado.

#### redefinir {#reset}

Redefine os valores iniciais dos dados persistentes do armazenamento e, em seguida, chama o serviço JSONP. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para este armazenamento enquanto os valores iniciais são redefinidos. Esta função não retorna nenhum valor.

Os valores iniciais são fornecidos na propriedade initialValues do objeto de configuração usado para instanciar o objeto de armazenamento.

##### Parâmetros {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Um valor true faz com que os dados não iniciais sejam mantidos. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveParameter(f) {#resolveparameter-f}

Resolve o parâmetro fornecido.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` estende [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) então ele herda todas as funções dessa classe. No entanto, os dados recuperados do serviço JSONP são mantidos de acordo com a configuração da persistência do ContextHub. (Consulte [Modos de persistência:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` estende [ContextHub.Store.Core](#contexthub-store-core) então ele herda todas as funções dessa classe. Os dados nesse armazenamento são mantidos de acordo com a configuração da persistência do ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` estende [ContextHub.Store.Core](#contexthub-store-core) então ele herda todas as funções dessa classe. Os dados neste armazenamento são mantidos usando a persistência na memória (objeto JavaScript).

## ContextHub.UI {#contexthub-ui}

Gerencia módulos de interface do usuário e renderizadores de módulo de interface do usuário.

### Funções (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderizador, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra um renderizador de módulo de interface do usuário no ContextHub. Depois que o renderizador é registrado, ele pode ser usado para [criar módulos de interface](configuring-contexthub.md#adding-a-ui-module). Use essa função quando estiver [extensão `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) para criar um renderizador de módulo de interface personalizada.

##### Parâmetros {#parameters-registerrenderer}

* **`moduleType`:** (String) O identificador do renderizador do módulo da interface do usuário. Se um renderizador já estiver registrado usando o valor especificado, o renderizador existente terá o registro cancelado antes que esse renderizador seja registrado.
* **`renderer`:** (String) O nome da classe que renderiza o módulo de interface do usuário.
* **`dontRender`:** (Booleano) Definido como `true` para impedir que a interface do usuário do ContextHub seja renderizada depois que o renderizador é registrado. O valor padrão é `false`.

##### Exemplo {#example-registerrenderer}

O exemplo a seguir registra um renderizador como o `contexthub.browserinfo` tipo de módulo.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Uma classe de utilitário para interagir com cookies.

### Funções (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### existe (chave) {#exists-key}

Determina se um cookie existe.

##### Parâmetros {#parameters-exists}

* **`key`:** A `String` que contém a chave do cookie para o qual você está testando.

##### Devoluções {#returns-exists}

A `boolean` valor true indica que o cookie existe.

##### Exemplo {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists ("name")) {
   // conditionally-executed code
}
```

#### getAllItems (filtro) {#getallitems-filter}

Retorna todos os cookies com chaves que correspondem a um filtro.

##### Parâmetros {#parameters-getallitems}

* **`filter`:** (Opcional) Critérios para correspondência de chaves de cookie. Para retornar todos os cookies, não especifique nenhum valor. Os seguintes tipos são compatíveis:
   * String: a string é comparada com a chave do cookie.
   * Matriz: cada item na matriz é um filtro.
   * Um objeto RegExp: a função de teste do objeto é usada para corresponder chaves de cookie.
   * Uma função: uma função que testa uma correspondência em uma chave de cookie. A função deve tomar a chave do cookie como um parâmetro e retornar true se o teste confirmar uma correspondência.

##### Devoluções {#returns-getallitems}

Um objeto de cookies. As propriedades do objeto são chaves de cookie e os valores de chave são valores de cookie.

##### Exemplo {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems ([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Retorna um valor de cookie.

##### Parâmetros {#parameters-getitem-1}

* **`key`:** A chave do cookie para o qual você deseja o valor.

##### Devoluções {#returns-getitem-1}

O valor do cookie, ou `null` se nenhum cookie for encontrado para a chave.

##### Exemplo {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys (filtro) {#getkeys-filter}

Retorna uma matriz das chaves de cookies existentes que correspondem a um filtro.

##### Parâmetros {#parameters-getkeys-1}

* **`filter`:** Critérios para correspondência de chaves de cookie. Os seguintes tipos são compatíveis:
   * String: a string é comparada com a chave do cookie.
   * Matriz: cada item na matriz é um filtro.
   * Um objeto RegExp: a função de teste do objeto é usada para corresponder chaves de cookie.
   * Uma função: uma função que testa uma correspondência em uma chave de cookie. A função deve tomar a chave do cookie como um parâmetro e retornar `true` se o teste confirmar uma correspondência.

##### Devoluções {#returns-getkeys-1}

Uma matriz de strings em que cada string é a chave de um cookie que corresponde ao filtro.

##### Exemplo {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys ([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(chave, opções) {#removeitem-key-options-1}

Remove um cookie. Para remover o cookie, o valor é definido como uma string vazia e a data de expiração é definida como o dia antes da data atual.

##### Parâmetros {#parameters-removeitem-1}

* **`key`:** A `String` valor que representa a chave do cookie a ser removido.
* **`options`:** Um objeto que contém valores de propriedade para configurar os atributos do cookie. Consulte a [`setItem`](#setitem-key-value-options) função para obter informações. A variável `expires` propriedade não tem efeito.

##### Devoluções {#returns-removeitem-1}

Esta função não retorna um valor.

##### Exemplo {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(chave, valor, opções) {#setitem-key-value-options-1}

Cria um cookie com a chave e o valor fornecidos e adiciona o cookie ao documento atual. Opcionalmente, você pode especificar opções que configuram os atributos do cookie.

##### Parâmetros {#parameters-setitem-1}

* **`key`:** Uma string que contém a chave do cookie.
* **`value`:** Uma string que contém o valor do cookie.
* **`options`:** (Opcional) Um objeto que contém qualquer uma das seguintes propriedades que configuram os atributos do cookie:
   * `expires`: A `date` ou `number` valor que especifica quando o cookie expira. Um valor de data especifica o tempo absoluto de expiração. Um número (em dias) define a hora de expiração para a hora atual mais o número. O valor padrão é `undefined`.
   * `secure`: A `boolean` valor que especifica a `Secure` atributo do cookie. O valor padrão é `false`.
   * `path`: A `String` valor a ser usado como `Path` atributo do cookie. O valor padrão é `undefined`.

##### Devoluções {#returns-setitem-1}

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

#### desaparecer (filtro, opções) {#vanish-filter-options}

Remove todos os cookies que correspondem a um determinado filtro. Os cookies são correspondidos usando o `getKeys` e removida usando a variável `removeItem` função.

##### Parâmetros {#parameters-vanish}

* **`filter`:** A variável `filter` argumento a ser usado na chamada para o [`getKeys`](#getkeys-filter) função.
* **`options`:** A variável `options` argumento a ser usado na chamada para o [`removeItem`](#removeitem-key-options) função.

##### Devoluções {#returns-vanish}

Esta função não retorna um valor.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Permite vincular e desvincular funções a eventos de armazenamento do ContextHub. Access `ContextHub.Utils.Eventing` objetos para um armazenamento usando o [evento](#eventing) propriedade do armazenamento.

### Funções (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(nome, seletor) {#off-name-selector}

Desassocia uma função de um evento.

##### Parâmetros {#parameters-off}

* **`name`:** A variável [nome do evento](#contexthub-utils-eventing) para o qual você está desvinculando a função.
* **`selector`:** O seletor que identifica a associação. (Consulte a `selector` parâmetro para o [`on`](#on-name-handler-selector-triggerforpastevents) e [`once`](#once-name-handler-selector-triggerforpastevents) funções).

##### Devoluções {#returns-off}

Esta função não retorna nenhum valor.

#### on(nome, manipulador, seletor, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada sempre que o evento ocorre. Como opção, a função pode ser chamada para eventos que ocorreram no passado, antes que a vinculação seja estabelecida.

##### Parâmetros {#parameters-on}

* **`name`:** (String) A variável [nome do evento](#contexthub-utils-eventing) ao qual você está vinculando a função.
* **`handler`:** (Função) A função a ser vinculada ao evento.
* **`selector`:** (String) Um identificador exclusivo para a associação. Você precisa do seletor para identificar o vínculo se quiser usar o `off` para remover a associação.
* **`triggerForPastEvents`:** (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor de `true` chama o manipulador de eventos anteriores. Um valor de `false` chama o manipulador para eventos futuros. O valor padrão é `true`.

##### Devoluções {#returns-on}

Quando a variável `triggerForPastEvents` o argumento é `true`, esta função retorna uma `boolean` valor que indica se o evento ocorreu no passado:

* `true`: o evento ocorreu no passado e o manipulador é chamado.
* `false`: o evento não ocorreu no passado.

Se `triggerForPastEvents` é `false`, essa função não retorna nenhum valor.

##### Exemplo {#example-on}

O exemplo a seguir vincula uma função ao evento de dados do armazenamento de geolocalização. A função preenche um elemento na página com o valor do item de dados de latitude do armazenamento.

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

#### once(nome, manipulador, seletor, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada apenas uma vez, para a primeira ocorrência do evento. Como opção, a função pode ser chamada para o evento que ocorreu no passado, antes que a vinculação seja estabelecida.

##### Parâmetros {#parameters-once}

* **`name`:** (String) A variável [nome do evento](#contexthub-utils-eventing) ao qual você está vinculando a função.
* **`handler`:** (Função) A função a ser vinculada ao evento.
* **`selector`:** (String) Um identificador exclusivo para a associação. Você precisa do seletor para identificar o vínculo se quiser usar o `off` para remover a associação.
* **`triggerForPastEvents`:** (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor de `true` chama o manipulador de eventos anteriores. Um valor de `false` chama o manipulador para eventos futuros. O valor padrão é `true`.

##### Devoluções {#returns-once}

Quando a variável `triggerForPastEvents` o argumento é `true`, esta função retorna uma `boolean` valor que indica se o evento ocorreu no passado:

* `true`: o evento ocorreu no passado e o manipulador é chamado.
* `false`: o evento não ocorreu no passado.

Se `triggerForPastEvents` é `false`, essa função não retorna nenhum valor.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Uma classe de utilitário que permite que um objeto herde as propriedades e os métodos de outro objeto.

### Funções (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(filho, pai) {#inherit-child-parent}

Faz um objeto herdar as propriedades e os métodos de outro objeto.

##### Parâmetros {#parameters-inherit}

* **`child`:** (Objeto) O objeto que herda.
* **`parent`:** (Objeto) O objeto que define as propriedades e os métodos herdados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornece funções para serializar objetos no formato JSON e desserializar strings JSON em objetos.

### Funções (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analisa um valor de string como JSON e o converte em um objeto javascript.

##### Parâmetros {#parameters-parse}

* **`data`:** Um valor de string no formato JSON.

##### Devoluções {#returns-parse}

Um objeto JavaScript.

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

#### stringify(dados) {#stringify-data}

Serializa valores e objetos JavaScript em valores de string do formato JSON.

##### Parâmetros {#parameters-stringify}

* **`data`:** O valor ou objeto a ser serializado. Esta função oferece suporte a valores booleanos, de matriz, número, sequência de caracteres e data.

##### Devoluções {#returns-stringify}

O valor da string serializada. Quando `data` é um R `egExp` value, esta função retorna um objeto vazio. Quando `data` é uma função, retorna `undefined`.

##### Exemplo {#example-stringify}

O código a seguir:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Devoluções:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Essa classe facilita a manipulação de objetos de dados que serão armazenados ou recuperados dos armazenamentos do ContextHub.

### Funções (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems () {#addallitems}

Cria uma cópia de um objeto de dados e adiciona a ele a árvore de dados de um segundo objeto. A função retorna a cópia e não modifica nenhum dos objetos originais. Quando as árvores de dados dos dois objetos contêm chaves idênticas, o valor do segundo objeto substitui o valor do primeiro objeto.

##### Parâmetros {#parameters-addallitems-1}

* **`tree`:** O objeto copiado.
* **`secondTree`:** O objeto que é mesclado com a cópia do `tree` objeto.

##### Devoluções {#returns-addallitems-1}

Um objeto que contém os dados mesclados.

#### cleanup() {#cleanup}

Cria uma cópia de um objeto, localiza e remove itens na árvore de dados que não contêm valores, valores nulos ou valores indefinidos e retorna a cópia.

##### Parâmetros {#parameters-cleanup}

* **`tree`:** O objeto a ser limpo.

##### Devoluções {#returns-cleanup}

Uma cópia da árvore que é limpa.

#### getItem() {#getitem}

Recupera o valor de um objeto para a chave.

##### Parâmetros {#parameters-getitem-2}

* **`tree`:** O objeto de dados.
* **`key`:** A chave do valor que você deseja recuperar.

##### Devoluções {#returns-getitem-2}

O valor que corresponde à chave. Quando a chave tem chaves filhas, essa função retorna um objeto complexo. Quando o tipo do valor da chave é `undefined`, `null` é retornado.

##### Exemplo {#example-getitem-2}

Considere o seguinte objeto JavaScript:

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

O código de exemplo a seguir recupera o valor de uma chave que tem chaves filhas:

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

#### getKeys () {#getkeys}

Recupera todas as chaves da árvore de dados de um objeto. Como opção, você pode recuperar somente as chaves dos filhos de uma chave específica. Também é possível especificar uma ordem de classificação das chaves recuperadas.

##### Parâmetros {#parameters-getkeys-2}

* **`tree`:** O objeto do qual recuperar as chaves da árvore de dados.
* **`parent`:** (Opcional) A chave de um item na árvore de dados para o qual você deseja recuperar as chaves dos itens secundários.
* **`order`:** (Opcional) Uma função que determina a ordem de classificação das chaves retornadas. (Consulte [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) na Mozilla Developer Network.)

##### Devoluções {#returns-getkeys-2}

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

A variável `ContextHub.Utils.JSON.tree.getKeys (myObject);` O script retorna a seguinte matriz:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Cria uma cópia de um determinado objeto, remove a ramificação especificada da árvore de dados e retorna a cópia modificada.

##### Parâmetros {#parameters-removeitem-2}

* **`tree`:** Um objeto de dados.
* **`key`:** A chave a ser removida.

##### Devoluções {#returns-removeitem-2}

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

O exemplo de script a seguir remove a ramificação /um/dois/três/quatro da árvore de dados:

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

Limpa os valores da string para torná-los utilizáveis como chaves. Para limpar uma string, essa função executa as seguintes ações:

* Reduz várias barras consecutivas a uma única barra.
* Remove os espaços em branco do início e do fim da sequência de caracteres.
* Divide o resultado em uma matriz de strings demarcadas por barras.

Use a matriz resultante para criar uma chave utilizável.

##### Parâmetros {#parameters-sanitizekey}

* **`key`:** A variável `string` para limpar.

##### Devoluções {#returns-sanitizekey}

Uma matriz de `string` valores em que cada string é a parte da variável `key` que foi demarcado por barras. representa a chave limpa. Se a matriz limpa tiver um comprimento de zero, essa função retornará `null`.

##### Exemplo {#example-sanitizekey}

O código a seguir limpa uma string para produzir a matriz `["this", "is", "a", "path"]`, e gera a chave `"/this/is/a/path"` no storage:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(árvore, chave, valor) {#setitem-tree-key-value}

Adiciona um par de chave/valor à árvore de dados de uma cópia de um objeto. Para obter informações sobre árvores de dados, consulte [Persistência.](contexthub.md#persistence)

##### Parâmetros {#parameters-setitem-2}

* **`tree`:** Um objeto de dados.
* **`key`:** A chave a ser associada ao valor que você está adicionando. A chave é o caminho para o item na árvore de dados. Essa função chama `ContextHub.Utils.JSON.tree.sanitize` para limpar a chave antes de adicioná-la.
* **`value`:** O valor a ser adicionado à árvore de dados.

##### Devoluções {#returns-setitem-2}

Uma cópia do `tree` objeto que inclui o `key`/ `value` emparelhar.

##### Exemplo {#example-setitem-2}

Considere o seguinte código JavaScript:

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

Permite registrar candidatos de armazenamento e obter candidatos registrados.

### Funções (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates (storeType) {#getregisteredcandidates-storetype}

Retorna os tipos de armazenamento registrados como candidatos de armazenamento. Recupere os candidatos registrados de um tipo de armazenamento específico ou de todos os tipos de armazenamento.

##### Parâmetros {#parameters-getregisteredcandidates}

* **`storeType`:** (String) O nome do tipo de armazenamento. Consulte a `storeType` parâmetro do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) função.

##### Devoluções {#returns-getregisteredcandidates}

Um objeto de tipos de armazenamento. As propriedades do objeto são os nomes do tipo de armazenamento e os valores da propriedade são uma matriz de candidatos de armazenamento registrados.

#### getStoreFromCandidates (storeType) {#getstorefromcandidates-storetype}

Retorna um tipo de armazenamento dos candidatos registrados. Se mais de um tipo de armazenamento com o mesmo nome estiver registrado, a função retornará o tipo de armazenamento com a prioridade mais alta.

##### Parâmetros {#parameters-getstorefromcandidates}

* `storeType`: (String) O nome do candidato a armazenamento. Consulte a `storeType` parâmetro do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) função.

##### Devoluções {#returns-getstorefromcandidates}

Um objeto que representa o candidato de armazenamento registrado. Se o Tipo de armazenamento solicitado não estiver registrado, um erro será lançado.

#### getSupportedStoreTypes () {#getsupportedstoretypes}

Retorna os nomes dos tipos de armazenamento registrados como candidatos de armazenamento. Esta função não requer parâmetros.

##### Devoluções {#returns-getsupportedstoretypes}

Uma matriz de valores de string, em que cada string é o tipo de loja com o qual um candidato a armazenamento foi registrado. Consulte a `storeType` parâmetro do [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) função.

#### registerStoreCandidate(store, storeType, priority, aplica) {#registerstorecandidate-store-storetype-priority-applies}

Registra um objeto de armazenamento como um candidato de armazenamento usando um nome e uma prioridade.

A prioridade é um número que indica a importância de armazenamentos com o mesmo nome. Quando um candidato de armazenamento é registrado usando o mesmo nome de um candidato de armazenamento já registrado, o candidato com a prioridade mais alta é usado. Ao registrar um candidato de armazenamento, o armazenamento será registrado somente se a prioridade for maior que os candidatos de armazenamento registrados com o mesmo nome.

##### Parâmetros {#parameters-registerstorecandidate}

* **`store`:** (Objeto) O objeto de armazenamento a ser registrado como um candidato de armazenamento.
* **`storeType`:** (String) O nome do candidato de armazenamento. Esse valor é necessário ao criar uma instância do candidato de armazenamento.
* **`priority`:** (Número) A prioridade do candidato da loja.
* **`applies`:** (Função) A função a ser chamada que avalia a aplicabilidade do armazenamento no ambiente atual. A função deve retornar `true` se o armazenamento for aplicável, e `false` caso contrário. O valor padrão é uma função que retorna verdadeiro: `function() {return true;}`

##### Exemplo {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
