---
title: Notas de versão do Universal Editor 2026.03.19
description: Estas são as notas de versão do Universal Editor de 2026.3.19.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Notas de versão do Universal Editor 2026.03.19 {#release-notes}

Estas são as notas de versão da versão de 19 de março de 2026 do Editor universal.

>[!TIP]
>
>Se você deseja testar os recursos do Universal Editor **futuros** antes de eles serem lançados, consulte as [Notas de Versão de Visualização do Universal Editor.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* Os itens nas propriedades agora são recolhidos ao navegar de volta para [a tela inicial.](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [O seletor de ativos](/help/implementing/universal-editor/configure-assets-selector.md) agora dá suporte a [definições de filtro.](/help/implementing/universal-editor/filtering.md)
* Se não houver ações disponíveis para o item selecionado, [o menu de contexto](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu) não mostrará mais uma divisa para acessar ações.

## Outras melhorias {#other-improvements}

* Se houver uma definição de modelo/filtro/componente, ela será buscada novamente ao alternar de um aplicativo para outro no editor.
* A remoção de uma imagem não deixa mais tags de imagem vazias ao usar o DA como back-end.
* As classes em blocos agora são manipuladas adequadamente ao usar o DA como back-end.
* A API aberta agora salva ativos remotos adequadamente como objetos.

## Quebra de alteração {#breaking-change}

* Todas as extensões devem ser atualizadas para `@adobe/uix-guest` >= `1.1.7` para melhorar a estabilidade.
