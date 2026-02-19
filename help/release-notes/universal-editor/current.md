---
title: Notas de versão do Universal Editor 2026.02.19
description: Estas são as notas de versão do Universal Editor de 2026.02.19.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2026.02.19 {#release-notes}

Estas são as notas de versão da versão de 19 de fevereiro de 2026 do Editor universal.

>[!TIP]
>
>Se você deseja testar os recursos do Universal Editor **futuros** antes de eles serem lançados, consulte as [Notas de Versão de Visualização do Universal Editor.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* Foram feitos aprimoramentos no RTE.
   * [Ocultar itens da barra de ferramentas no RTE de contexto](/help/implementing/universal-editor/configure-rte.md#common-action-options) agora é suportado.
   * [Quebra de texto dentro de tabelas com parágrafos](/help/implementing/universal-editor/configure-rte.md#table-actions) agora é suportado.
   * [Marcas do HTML sem suporte](/help/implementing/universal-editor/configure-rte.md#unsupported-html) agora podem ser preservadas pelo RTE.
   * A lógica do RTE agora é disponibilizada a partir de um arquivo separado.
   * [As tabelas agora podem ser criadas](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options) e editadas usando o RTE.
* Se nenhum rótulo for definido, o título do componente da definição do componente será usado.
* `setEditorMode` agora está disponível por meio de extensões.

## Recursos da adoção antecipada {#early-adopter}

Se você estiver interessado em testar os recursos futuros listados abaixo e compartilhar seu feedback, envie um email para o seu Gerente de sucesso do cliente da Adobe a partir do endereço de email associado à sua Adobe ID.

* A cópia superficial foi implementada para Fragmentos de conteúdo.

## Outras melhorias {#other-improvements}

* Os endpoints de RTE agora são fornecidos para o editor local.
* A edição de campos aninhados não resulta mais na substituição de entradas de mesmo nível dessas estruturas.
* Os campos obrigatórios de RTE não podem mais ser salvos como vazios.
* A formatação no local não é mais aplicada incorretamente ao adicionar links após a formatação.
