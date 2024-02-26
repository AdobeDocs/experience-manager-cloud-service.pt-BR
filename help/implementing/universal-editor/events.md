---
title: Eventos Universais do Editor
description: Saiba mais sobre os diferentes eventos que o Editor universal envia que você pode usar para reagir a alterações de conteúdo ou na interface do usuário no aplicativo remoto.
source-git-commit: e92a0be2213e3d5793fd077bd1968852336cc98b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Eventos Universais do Editor {#events}

Saiba mais sobre os diferentes eventos que o Editor universal envia que você pode usar para reagir a alterações de conteúdo ou na interface do usuário no aplicativo remoto.

## Introdução {#introduction}

Os aplicativos podem ter requisitos diferentes para atualizações de páginas ou componentes. Portanto, o Editor universal envia eventos definidos para aplicativos remotos. Caso a aplicação remota não tenha um ouvinte de evento personalizado para o evento enviado, uma [ouvinte de eventos de fallback](#fallback-listeners) fornecido pelo `universal-editor-cors` o pacote é executado.

Todos os eventos são chamados no elemento DOM afetado da página remota. Bolha de eventos para o `BODY` elemento em que o ouvinte de eventos default fornecido pelo `universal-editor-cors` o pacote está registrado. Há eventos para o conteúdo e eventos para a interface do usuário.

Todos os eventos seguem uma convenção de nomenclatura.

* `aue:<content-or-ui>-<event-name>`

Por exemplo, `aue:content-update` e `aue:ui-select`

Os eventos incluem a carga da solicitação e da resposta e são acionados assim que a chamada correspondente é bem-sucedida. Para obter mais detalhes sobre chamadas e exemplos de suas cargas, consulte o documento [Chamadas do editor universal.](/help/implementing/universal-editor/calls.md)

## Eventos de atualização de conteúdo {#content-events}

### aue:adição de conteúdo {#content-add}

A variável `aue:content-add` evento é acionado quando um novo componente é adicionado a um contêiner.

A carga é o conteúdo do serviço do Universal Editor, com conteúdo de fallback da definição do componente.

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

A variável `aue:content-details` o evento é acionado quando um componente é carregado no painel de propriedades.

A carga é o conteúdo do componente e, opcionalmente, seu schema.

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:movimentação de conteúdo {#content-move}

A variável `aue:content-move` o evento é acionado quando um componente é movido.

A carga é o componente, contêiner de origem e contêiner de destino.

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-patch {#content-patch}

A variável `aue:content-patch` o evento é acionado quando os dados de um componente são atualizados no painel de propriedades.

A carga é uma correção JSON das propriedades atualizadas.

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:remoção de conteúdo {#content-remove}

A variável `aue:content-remove` evento é acionado quando um componente é removido de um container.

A carga é a ID do item do componente removido.

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:atualização de conteúdo {#content-update}

A variável `aue:content-update` O evento é acionado quando as propriedades de um componente são atualizadas no contexto.

O payload é o valor atualizado.

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### Envio de cargas {#passing-payloads}

Para todos os eventos de atualização de conteúdo, a carga solicitada, bem como a carga de resposta, são passadas para o evento. Por exemplo, para uma chamada de atualização:

Carga da solicitação:

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

Carga de resposta

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## Eventos da interface do usuário {#ui-events}

### aue:ui-publish {#ui-publish}

A variável `aue:ui-publish` evento é acionado quando o conteúdo é publicado (com invocação no `BODY` nível da UE).

A carga é uma lista de IDs de item e seus status de publicação.

### aue:ui-select {#ui-select}

A variável `aue:ui-select` evento é acionado quando um componente é selecionado.

A carga é a ID do item, as propriedades do item e o tipo do componente selecionado.

```json
{
    details: {
        resource: string;       // resource of the selected
        prop: string;           // prop of the selected
        type: string;           // type of the selected
        selected: boolean;      // was selected or unselected
    }
}
```

### aue:ui-preview {#ui-preview}

A variável `aue:ui-preview` evento é acionado quando o modo de edição da página é alterado para **Visualizar**.

A carga está vazia para este evento.

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

A variável `aue:ui-edit` evento é acionado quando o modo de edição da página é alterado para **Editar**.

A carga está vazia para este evento.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

A variável `aue:ui-viewport-change` O evento é acionado quando o tamanho do visor é alterado.

A carga são as dimensões da janela de visualização.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:inicializado {#initialized}

A variável `aue:initialized` O evento é acionado para informar à página remota que ele foi carregado com êxito no Editor universal.

A carga está vazia para este evento.

```json
{
    details: {}
}
```

## Ouvintes de Eventos de Fallback {#fallback-listeners}

### Atualizações de conteúdo {#content-update-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:content-add` | Recarregamento de página |
| `aue:content-details` | Não fazer nada |
| `aue:content-move` | Mover o conteúdo/estrutura do componente para a área de destino |
| `aue:content-patch` | Recarregamento de página |
| `aue:content-remove` | Remover o elemento DOM |
| `aue:content-update` | Atualize o `innerHTML` com a carga útil |

### Eventos da interface do usuário {#ui-event-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:ui-publish` | Não fazer nada |
| `aue:ui-select` | Rolar até o elemento selecionado |
| `aue:ui-preview` | Adicionar `class="adobe-ue-preview"` para tag HTML |
| `aue:ui-edit` | Adicionar `class=adobe-ue-edit"` para tag HTML |
| `aue:ui-viewport-change` | Não fazer nada |
| `aue:initialized` | Não fazer nada |

## Recursos adicionais {#additional-resources}

* [Chamadas do editor universal](/help/implementing/universal-editor/calls.md)
