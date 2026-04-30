---
title: Notas de versão de visualização do Universal Editor
description: Estas são as notas de versão da versão de pré-visualização do Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: f3ba70f276ab534e0becea47390fe58bf8a825d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Notas de versão de visualização do Universal Editor {#preview}

Estas são as notas de versão da **versão de visualização** do Editor Universal. Estes recursos estão disponíveis atualmente no **ambiente de visualização** do Editor Universal. Esses recursos estão programados para serem lançados para disponibilização geral em 7 de maio de 2026.

Estas notas de versão do **preview** são fornecidas como conveniência, para que você saiba quais alterações do Universal Editor estão por vir e possa testá-las [alternando para a versão de visualização.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Para as **notas de versão atuais** do Universal Editor, consulte as [Notas de Versão do Universal Editor.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>O conteúdo da versão real, bem como a data de lançamento, estão sujeitos a alterações.

## Recursos futuros {#upcoming-features}

* Um service worker foi introduzido para reduzir a latência entre a interface do usuário do Editor universal e os sistemas de back-end.
* Todos os adaptadores para fragmentos de conteúdo (AEM 6.5, OpenAPI e GraphQL) agora incluem os filtros para o seletor de ativos a fim de garantir consistência e que os usuários possam selecionar somente ativos permitidos.
* `content:patch` intenção foi fornecida.
* Para ajudar na acessibilidade, o fluxo do autor e os pontos de referência foram definidos.

## Outras melhorias futuras {#other-improvements}

* Declarações de tipo desnecessárias em `assignImageDimensionFields` foram removidas.
* Correção de um problema em que o tratamento do lado do servidor da operação `add` iterava o valor da cadeia de caracteres, tratando-o como um objeto em vez de um patch.
