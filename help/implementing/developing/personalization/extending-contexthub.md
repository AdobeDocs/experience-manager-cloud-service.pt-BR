---
title: Extensão do ContextHub
description: Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Extensão do ContextHub {#extending-contexthub}

Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução.

## Criação de Candidatos de Loja Personalizada {#creating-custom-store-candidates}

As lojas ContextHub são criadas a partir de candidatos a lojas registradas. Para criar uma loja personalizada, você precisa criar e registrar um candidato de loja.

O arquivo javascript que inclui o código que cria e registra o candidato da loja deve ser incluído em um [pasta da biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

O `storeType` parte da categoria é `storeType` com o qual o candidato da loja está registrado. (Consulte [Registrando um candidato a armazenamento do ContextHub](#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criando um candidato a armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de loja, use a variável [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) para estender um dos armazenamentos base:

* [&quot;ContextHub.Store.PersistedStore&quot;](contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](contexthub-api.md#contexthub-store-persistedjsonpstore)

Observe que cada loja base estende a variável [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) armazenar.

O exemplo a seguir cria a extensão mais simples do `ContextHub.Store.PersistedStore` candidato à loja:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Realisticamente, os candidatos a loja personalizada definirão funções adicionais ou substituirão a configuração inicial da loja. Vários [candidatos à loja de amostras](sample-stores.md) são instalados no repositório abaixo `/libs/granite/contexthub/components/stores`.

### Registrando um candidato a armazenamento do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato a loja para integrá-lo à estrutura do ContextHub e permitir que as lojas sejam criadas a partir dele. Para registrar um candidato de loja, use a variável [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) da `ContextHub.Utils.storeCandidates` classe .

Ao registrar um candidato de loja, forneça um nome para o tipo de loja. Ao criar uma loja do candidato, você usa o tipo de loja para identificar o candidato em que se baseia.

Ao registrar um candidato a loja, você indica sua prioridade. Quando um candidato de loja é registrado usando o mesmo tipo de loja que um candidato de loja já registrado, o candidato com prioridade mais alta é usado. Portanto, você pode substituir candidatos de loja existentes por novas implementações.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Na maioria dos casos, só é necessário um candidato e a prioridade pode ser definida como `0`, mas se você estiver interessado, poderá saber mais sobre [registros mais avançados,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) O que permite que uma das poucas implementações da loja seja escolhida com base na condição de javascript (`applies`) e a prioridade do candidato.

## Criação de tipos de módulos da interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Criar tipos de módulo de interface de usuário personalizada quando os [instalado com o ContextHub](sample-modules.md) não atenda aos seus requisitos. Para criar um tipo de módulo de interface do usuário, crie um novo renderizador de módulo de interface do usuário estendendo o `ContextHub.UI.BaseModuleRenderer` e registrá-la com `ContextHub.UI`.

Para criar um renderizador de módulo de interface do usuário, crie um `Class` objeto que contém a lógica que renderiza o módulo da interface do usuário. No mínimo, sua classe deve executar as seguintes ações:

* Estender o `ContextHub.UI.BaseModuleRenderer` classe . Essa classe é a implementação básica para todos os renderizadores de módulo da interface do usuário. O `Class` objeto define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.
* Forneça uma configuração padrão. Crie um `defaultConfig` propriedade. Essa propriedade é um objeto que inclui as propriedades definidas para a variável [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) Módulo de interface do usuário e quaisquer outras propriedades necessárias.

A fonte para `ContextHub.UI.BaseModuleRenderer` está localizado em `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Para registrar o renderizador, use o [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) do método `ContextHub.UI` classe . É necessário fornecer um nome para o tipo de módulo. Quando os administradores criam um módulo de interface com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe renderer em uma função anônima de execução automática. O exemplo a seguir é baseado no código-fonte da variável `contexthub.browserinfo` Módulo da interface do usuário. Este módulo de interface é uma extensão simples do `ContextHub.UI.BaseModuleRenderer` classe .

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

O arquivo javascript que inclui o código que cria e registra o renderizador deve ser incluído em um [pasta da biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md). A categoria da pasta deve corresponder ao seguinte padrão:

```javascript
contexthub.module.[moduleType]
```

O `[moduleType]` parte da categoria é `moduleType` com o qual o renderizador de módulo é registrado. Por exemplo, para a variável `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
