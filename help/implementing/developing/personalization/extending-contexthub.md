---
title: Extensão do ContextHub
description: Definir novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Extensão do ContextHub {#extending-contexthub}

Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução.

## Criação de candidatos à loja personalizada {#creating-custom-store-candidates}

Os armazenamentos do ContextHub são criados de candidatos de armazenamento registrados. Para criar um armazenamento personalizado, é necessário criar e registrar um candidato de armazenamento.

O arquivo javascript que inclui o código que cria e registra o candidato da loja deve ser incluído em um [pasta da biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

A variável `storeType` parte da categoria é a `storeType` com o qual o candidato da loja está registrado. (Consulte [Registrando um candidato de armazenamento do ContextHub](#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criação de um candidato de armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de armazenamento, use o [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) função para estender um dos armazenamentos base:

* [&quot;ContextHub.Store.PersistedStore&quot;](contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada armazenamento básico estende o [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) armazenamento.

O exemplo a seguir cria a extensão mais simples do `ContextHub.Store.PersistedStore` candidato a armazenamento:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Na realidade, seus candidatos de armazenamento personalizados definirão funções adicionais ou substituirão a configuração inicial do armazenamento. Vários [exemplos de candidatos à loja](sample-stores.md) estão instalados no repositório abaixo `/libs/granite/contexthub/components/stores`.

### Registrando um candidato de armazenamento do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato de armazenamento para integrá-lo à estrutura do ContextHub e permitir que os armazenamentos sejam criados a partir dele. Para registrar um candidato de armazenamento, use o [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) função da `ContextHub.Utils.storeCandidates` classe.

Ao registrar um candidato de armazenamento, forneça um nome para o tipo de armazenamento. Ao criar um armazenamento a partir do candidato, use o tipo de armazenamento para identificar o candidato no qual ele se baseia.

Ao registrar um candidato de armazenamento, você indica sua prioridade. Quando um candidato de armazenamento é registrado usando o mesmo tipo de armazenamento que um candidato de armazenamento já registrado, o candidato com a prioridade mais alta é usado. Portanto, você pode substituir candidatos de armazenamento existentes por novas implementações.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Na maioria dos casos, é necessário apenas um candidato e a prioridade pode ser definida como `0`, mas se você estiver interessado, poderá saber mais sobre [registros mais avançados,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) que permite que uma das poucas implementações de armazenamento seja escolhida com base na condição do javascript (`applies`) e a prioridade do candidato.

## Criação de tipos de módulo da interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Criar tipos de módulo de interface personalizada quando os que estão [instalado com o ContextHub](sample-modules.md) não atendem aos seus requisitos. Para criar um tipo de módulo de interface do usuário, crie um renderizador de módulo de interface do usuário estendendo o `ContextHub.UI.BaseModuleRenderer` e, em seguida, registrando-a com `ContextHub.UI`.

Para criar um renderizador de módulo de interface do usuário, crie um `Class` objeto que contém a lógica que renderiza o módulo da interface do usuário. No mínimo, sua classe deve executar as seguintes ações:

* Estenda o `ContextHub.UI.BaseModuleRenderer` classe. Essa classe é a implementação base para todos os renderizadores de módulo de interface do usuário. A variável `Class` O objeto define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.
* Forneça uma configuração padrão. Criar um `defaultConfig` propriedade. Essa propriedade é um objeto que inclui as propriedades definidas para o [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) Módulo de interface do usuário e quaisquer outras propriedades necessárias.

A fonte para `ContextHub.UI.BaseModuleRenderer` está localizado em `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Para registrar o renderizador, use o [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) método do `ContextHub.UI` classe. É necessário fornecer um nome para o tipo de módulo. Quando os administradores criam um módulo de interface do usuário com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe do renderizador em uma função anônima autoexecutável. O exemplo a seguir é baseado no código-fonte para o `contexthub.browserinfo` Módulo de interface do usuário. Esse módulo de interface do usuário é uma extensão simples do `ContextHub.UI.BaseModuleRenderer` classe.

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

A variável `[moduleType]` parte da categoria é a `moduleType` com o qual o renderizador do módulo está registrado. Por exemplo, para o `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
