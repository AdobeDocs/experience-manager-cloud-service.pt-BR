---
title: Eventos Universais do Editor
description: Saiba mais sobre os diferentes eventos que o Editor universal envia que você pode usar para reagir a alterações de conteúdo ou na interface do usuário no aplicativo remoto.
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Developer
source-git-commit: 9adf2bc4f9f25ee7fc0a39b0f1a3ae9e45fce7d2
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# Eventos Universais do Editor {#events}

Saiba mais sobre os diferentes eventos que o Editor universal envia que você pode usar para reagir a alterações de conteúdo ou na interface do usuário no aplicativo remoto.

## Introdução {#introduction}

Os aplicativos podem ter requisitos diferentes para atualizações de páginas ou componentes. Portanto, o Editor universal envia eventos definidos para aplicativos remotos. Caso o aplicativo remoto não tenha um ouvinte de evento personalizado para o evento enviado, um [ouvinte de evento de fallback](#fallback-listeners) fornecido pelo pacote `universal-editor-cors` será executado.

Todos os eventos são chamados no elemento DOM afetado da página remota. Os eventos propagam para o elemento `BODY` onde o ouvinte de eventos padrão fornecido pelo pacote `universal-editor-cors` está registrado. Há eventos para o conteúdo e eventos para a interface do usuário.

Todos os eventos seguem uma convenção de nomenclatura.

* `aue:<content-or-ui>-<event-name>`

Por exemplo, `aue:content-update` e `aue:ui-select`

Os eventos incluem a carga da solicitação e da resposta e são acionados assim que a chamada correspondente é bem-sucedida. Para obter mais detalhes sobre chamadas e exemplos de cargas, consulte o documento [Chamadas do Editor Universal](/help/implementing/universal-editor/calls.md).

## Eventos de atualização de conteúdo {#content-events}

### aue&amp;dois pontos;content-add {#content-add}

O evento `aue:content-add` é disparado quando um novo componente é adicionado a um contêiner.

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

### aue&amp;dois pontos;content-details {#content-details}

O evento `aue:content-details` é disparado quando um componente é carregado no painel de propriedades.

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

### aue&amp;dois pontos;movimentação de conteúdo {#content-move}

O evento `aue:content-move` é disparado quando um componente é movido.

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

### aue&amp;dois pontos;content-patch {#content-patch}

O evento `aue:content-patch` é disparado quando os dados de um componente são atualizados no painel de propriedades.

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

### aue&amp;dois pontos;remoção de conteúdo {#content-remove}

O evento `aue:content-remove` é disparado quando um componente é removido de um contêiner.

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

### aue&amp;dois pontos;content-update {#content-update}

O evento `aue:content-update` é disparado quando as propriedades de um componente são atualizadas no contexto.

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

### aue&amp;dois pontos;ui-preview {#ui-preview}

O evento `aue:ui-preview` é disparado quando o modo de edição da página é alterado para **Visualização**.

A carga está vazia para este evento.

```json
{
    details: {}
}
```

### aue&amp;dois pontos;ui-edit {#ui-edit}

O evento `aue:ui-edit` é disparado quando o modo de edição da página é alterado para **Editar**.

A carga está vazia para este evento.

```json
{
    details: {}
}
```

### aue&amp;dois pontos;ui-viewport-change {#ui-viewport-change}

O evento `aue:ui-viewport-change` é acionado quando o tamanho do visor é alterado.

A carga são as dimensões da janela de visualização.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue&amp;dois pontos;inicializado {#initialized}

O evento `aue:initialized` é disparado para informar à página remota que ele foi carregado com êxito no Editor Universal.

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
| `aue:content-update` | Atualizar o `innerHTML` com a carga |

### Eventos da interface do usuário {#ui-event-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:ui-select` | Rolar até o elemento selecionado |
| `aue:ui-preview` | Adicionar `class="adobe-ue-preview"` à tag do HTML |
| `aue:ui-edit` | Adicionar `class=adobe-ue-edit"` à tag do HTML |
| `aue:ui-viewport-change` | Não fazer nada |
| `aue:initialized` | Não fazer nada |

## Recursos adicionais {#additional-resources}

* [Chamadas do editor universal](/help/implementing/universal-editor/calls.md)
