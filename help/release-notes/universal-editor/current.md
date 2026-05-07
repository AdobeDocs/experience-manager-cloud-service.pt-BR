---
title: Notas de versão do Universal Editor 2026.05.07
description: Estas são as notas de versão do Universal Editor de 2026.05.07.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 4f66cd6048d7a78bea33c0f9c21017983b9032d5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Notas de versão do Universal Editor 2026.05.07 {#release-notes}

Estas são as notas de versão da versão de 7 de maio de 2026 do Universal Editor.

>[!TIP]
>
>Se você deseja testar os recursos do Universal Editor **futuros** antes de eles serem lançados, consulte as [Notas de Versão de Visualização do Universal Editor.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* Agora você pode [arrastar e soltar componentes no editor para movê-los.](/help/sites-cloud/authoring/universal-editor/authoring.md#drag-and-drop-move)
* Um service worker foi introduzido para reduzir a latência entre a interface do usuário do Editor universal e os sistemas de back-end.
* Todos os adaptadores para fragmentos de conteúdo (AEM 6.5, OpenAPI e GraphQL) agora incluem os filtros para o seletor de ativos a fim de garantir consistência e que os usuários possam selecionar somente ativos permitidos.
* `content:patch` intenção foi fornecida.
* Para ajudar na acessibilidade, o fluxo do autor e os pontos de referência foram definidos.

## Outras melhorias futuras {#other-improvements}

* Declarações de tipo desnecessárias em `assignImageDimensionFields` foram removidas.
* Correção de um problema em que o tratamento do lado do servidor da operação `add` iterava o valor da cadeia de caracteres, tratando-o como um objeto em vez de um patch.
