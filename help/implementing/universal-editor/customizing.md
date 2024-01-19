---
title: Personalização da interface
description: Saiba mais sobre os diferentes pontos de extensão que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Personalização da interface {#customizing-ui}

Saiba mais sobre os diferentes pontos de extensão que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.

## Desabilitar publicação {#disable-publish}

Determinados workflows de criação exigem que o conteúdo seja revisado antes de ser publicado. Nessas situações, a opção de publicar não deve estar disponível para nenhum autor.

A variável **Publish** Portanto, o botão pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
