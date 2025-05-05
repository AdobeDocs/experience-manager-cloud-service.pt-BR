---
title: Exemplos de tipos de módulo da interface do usuário do ContextHub
description: O ContextHub fornece vários módulos de interface do usuário de amostra que você pode usar em suas soluções
exl-id: 31ff4444-8d96-4817-9676-ea5ad36dcda5
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# Exemplos de tipos de módulo da interface do usuário do ContextHub {#sample-contexthub-ui-module-types}

O ContextHub fornece vários módulos de interface do usuário de amostra que você pode usar em suas soluções. As seguintes informações são fornecidas:

* Os principais recursos do módulo de interface do usuário.
* Onde encontrar o código-fonte para poder abri-lo para fins de aprendizado.
* Como configurar o módulo da interface do usuário.

Para obter informações sobre como adicionar módulos de interface do usuário ao ContextHub, consulte [Adicionando um Módulo de Interface do Usuário](configuring-contexthub.md#adding-a-ui-module). Para obter informações sobre como desenvolver módulos de interface, consulte [Criação de tipos de módulo de interface do usuário do ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

## Tipo de módulo da interface do usuário contexthub.base {#contexthub-base-ui-module-type}

O tipo de módulo contexthub.base UI é o tipo base para todos os outros tipos de módulo UI. Dessa forma, ele fornece recursos genéricos para renderizar dados do armazenamento.

Os seguintes recursos estão disponíveis:

* **Título e ícone:** especifique um título para o módulo de interface do usuário e um ícone. O ícone pode ser referenciado usando um URL ou na biblioteca de ícones da interface do Coral.
* **Dados de armazenamento:** Identifique um ou mais armazenamentos dos quais recuperar dados.
* **Conteúdo:** especifique o conteúdo que aparece no módulo de interface do usuário como ele aparece na barra de ferramentas do ContextHub.
* **Popover:** especifique o conteúdo que aparece em um popover quando o módulo de interface do usuário é clicado ou tocado.
* **Modo de tela cheia:** controla se o modo de tela cheia é permitido.

O código-fonte está localizado em `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.

### Configuração {#configuration}

Configure o módulo de interface contexthub.base usando um objeto JavaScript no formato JSON. Inclua qualquer uma das seguintes propriedades para configurar os recursos do módulo da interface do usuário:

* **imagem:** uma URL para uma imagem a ser exibida como ícone.
* **Ícone:** O nome de uma classe [Ícone de interface do usuário do Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html). Se você especificar um valor para as propriedades icon e image, a imagem será usada.
* **título:** um título para o módulo de interface do usuário. O título é exibido quando o ponteiro é pausado sobre o ícone do módulo da interface do usuário.
* **tela cheia:** um valor booliano que indica se o módulo de interface do usuário dá suporte ao modo de tela cheia. Use `true` para oferecer suporte à tela cheia e `false` para impedir o modo de tela cheia.
* **modelo:** um modelo [Handlebars](https://handlebarsjs.com/) que especifica o conteúdo a ser renderizado na barra de ferramentas do ContextHub. Use no máximo duas `<p>` tags.
* **storeMapping:** um mapeamento de chave/repositório. Use a chave nos modelos de Handlebar para acessar os dados de armazenamento do ContextHub associados.
* **lista:** uma matriz de itens para exibir como uma lista em um popover quando o módulo de interface do usuário for clicado. Se você incluir esse item, não inclua popoverTemplate. O valor é uma matriz de objetos com as seguintes chaves:
   * título: o texto a ser exibido para este item
   * image: (opcional) um URL para uma imagem que deve ser exibida à esquerda
   * ícone: (opcional) uma classe de ícone CUI que deve ser exibida à esquerda; ignorado se uma imagem for especificada
   * selecionado: (opcional) um valor booleano que especifica se esse item deve ser exibido como selecionado (true=seleted). Por padrão, os itens selecionados aparecem usando uma fonte em negrito. Use uma propriedade `listType` para configurar outras aparências (veja abaixo).
* **listType:** o estilo a ser usado para itens de lista de popover. Use um dos seguintes valores:
   * marca de seleção
   * caixa de seleção
   * rádio
* **popoverTemplate:** um modelo Handlebars que especifica o conteúdo a ser renderizado no popover quando o módulo de interface do usuário for clicado. Se você incluir este item, não inclua o item `list`.

### Exemplo {#example}

O exemplo a seguir configura um módulo de interface do usuário c`ontexthub.base` para exibir informações de um armazenamento [contexthub.emulators](sample-stores.md#granite-emulators-sample-store-candidate). O item `template` demonstra como obter dados do repositório usando a chave estabelecida pelo item `storeMapping`.

```javascript
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![módulo contexthub.base](assets/base-module.png)

## Tipo de módulo da interface do usuário contexthub.browserinfo {#contexthub-browserinfo-ui-module-type}

O módulo de interface do usuário `contexthub.browserinfo` exibe informações sobre o navegador da Web cliente e o sistema operacional. As informações são obtidas do repositório surferinfo, com base no [candidato do repositório &lbrace;contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate).

![módulo contexthub.browserinfo](assets/browserinfo-module.png)

O código-fonte do módulo de interface do usuário está localizado em `/libs/granite/contexthub/components/modules/browserinfo`. Embora `contexthub.browserinfo` estenda o módulo de interface do usuário `contexthub.base`, ele não substitui nem fornece funções adicionais. A implementação fornece uma configuração padrão para renderizar informações do navegador.

### Configuração {#configuration-1}

As instâncias do módulo de interface do usuário contexthub.browserinfo não exigem um valor para a Configuração de detalhes. O texto JSON a seguir representa a configuração padrão do módulo.

```javascript
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## Tipo de módulo da interface do usuário contexthub.datetime {#contexthub-datetime-ui-module-type}

O módulo de interface do usuário `contexthub.datetime` exibe a data e a hora armazenadas em um armazenamento chamado datetime que se baseia no candidato a armazenamento `contexthub.datetime`.

![módulo contexthub.datetime](assets/datetime-module.png)

O módulo fornece um formulário popover que permite alterar a data e a hora na loja.

A origem do módulo de interface do usuário `contexthub.datetime` está localizada em `/libs/granite/contexthub/components/modules/datetime`.

### Configuração {#configuration-2}

As instâncias do módulo de interface do usuário contexthub.datetime não exigem um valor para a Configuração detalhada. O texto JSON a seguir representa a configuração padrão do módulo.

```javascript
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## Tipo de módulo da interface do usuário contexthub.location {#contexthub-location-ui-module-type}

O módulo de interface do usuário `contexthub.location` exibe a longitude e a latitude do cliente. O módulo fornece um popover que exibe um mapa de Google no qual você pode clicar para alterar a localização atual. O módulo obtém informações de um armazenamento do ContextHub chamado geolocalização baseado no [candidato de armazenamento contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate).

![módulo contexthub.location](assets/location-module.png)

A origem do módulo de interface do usuário está localizada em `/etc/cloudsettings/default/contexthub/geolocation`.

### Configuração {#configuration-4}

As instâncias do módulo de interface do usuário contexthub.location não exigem um valor para a Configuração de detalhes. O texto JSON a seguir representa a configuração padrão do módulo.

```javascript
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## Tipo de módulo da interface do usuário contexthub.screen-orientation {#contexthub-screen-orientation-ui-module-type}

O módulo de interface do usuário `contexthub.screen-orientation` exibe a orientação de tela atual do cliente. Embora desativado por padrão, o módulo fornece um popover que permite selecionar uma orientação. O módulo obtém informações de um armazenamento do ContextHub chamado emuladores que é baseado no candidato de armazenamento [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate).

![módulo contexthub.screen-orientation](assets/screen-orientation-module.png)

A origem do módulo de interface do usuário está localizada em `/libs/granite/contexthub/components/modules/screen-orientation`.

### Configuração {#configuration-5}

As instâncias do módulo de interface do usuário `contexthub.screen-orientation` não exigem um valor para a Configuração Detalhada. O texto JSON a seguir representa a configuração padrão do módulo. A propriedade `clickable` é `false` por padrão. Se você substituir a configuração padrão para definir `clickable` como `true`, clicar no módulo revela um pop-up onde você pode selecionar a orientação.

```javascript
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## Tipo de módulo da interface do usuário do contexthub.tagcloud {#contexthub-tagcloud-ui-module-type}

O módulo de interface do usuário `contexthub.tagcloud` exibe informações sobre marcas. Na barra de ferramentas, o módulo da interface mostra o número de tags. O pop-up revela uma nuvem de tag e uma caixa de texto para adicionar novas tags. O módulo de interface do usuário obtém informações de um armazenamento do ContextHub chamado tagcloud que é baseado no candidato a armazenamento `contexthub.tagcloud`.

![módulo contexthub.tagcloud](assets/tagcloud-module.png)

A origem do módulo de interface do usuário está localizada em `/libs/granite/contexthub/components/modules/tagcloud`.

### Configuração {#configuration-6}

As instâncias do módulo de interface do usuário `contexthub.tagcloud` não exigem um valor para a Configuração Detalhada. O texto JSON a seguir representa a configuração padrão do módulo.

```javascript
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## Tipo de módulo de interface do usuário do granite.profile {#granite-profile-ui-module-type}

O módulo da interface do usuário do ContextHub `granite.profile` exibe o nome de exibição do usuário atual. A janela pop-up revela o nome de logon do usuário e permite alterar o valor do nome de exibição. O módulo de interface do usuário obtém informações de um armazenamento do ContextHub chamado perfil, que é baseado no candidato de armazenamento [granite.profile](sample-stores.md#granite-profile-sample-store-candidate).

![módulo granite.profile](assets/profile-module.png)

A origem do módulo de interface do usuário está em `/libs/granite/contexthub/components/modules/profile`.

### Configuração {#configuration-7}

As instâncias do módulo de interface do usuário `granite.profile` não exigem um valor para a Configuração Detalhada. O texto JSON a seguir representa a configuração padrão do módulo.

```javascript
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
