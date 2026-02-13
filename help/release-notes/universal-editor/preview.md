---
title: Notas de versão de visualização do Universal Editor
description: Estas são as notas de versão da versão de pré-visualização do Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Notas de versão de visualização do Universal Editor {#preview}

Estas são as notas de versão da **versão de visualização** do Editor Universal. Estes recursos estão disponíveis atualmente no **ambiente de visualização** do Editor Universal. Esses recursos estão programados para serem lançados para disponibilização geral em 19 de fevereiro de 2026.

Estas notas de versão do **preview** são fornecidas como conveniência, para que você saiba quais alterações do Universal Editor estão por vir e possa testá-las [alternando para a versão de visualização.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Para as **notas de versão atuais** do Universal Editor, consulte as [Notas de Versão do Universal Editor.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>O conteúdo da versão real, bem como a data de lançamento, estão sujeitos a alterações.

## Novos recursos futuros {#what-is-new}

* Foram feitos aprimoramentos no RTE.
   * Ocultar itens da barra de ferramentas no RTE em contexto agora é compatível.
   * A quebra de texto entre tabelas com parágrafos agora é suportada.
   * Tags de RTE não compatíveis agora são preservadas.
   * A lógica do RTE agora é disponibilizada a partir de um arquivo separado.
   * Agora, as tabelas podem ser criadas e editadas usando o RTE.
* Se nenhum rótulo for definido, o título do componente da definição do componente será usado.
* `setEditorMode` agora está disponível por meio de extensões.

## Aprimoramentos futuros {#other-improvements}

* A funcionalidade de copiar e colar entre páginas foi corrigida.
* `universal-editor-extensibility` foi deslocado para `universal-editor`.
* O número de solicitações para o endpoint de extensões foi reduzido.
* As desmontagens do RemoteApp foram reduzidas de três para um.
* Os endpoints de RTE agora são fornecidos para o editor local.
* A edição de campos aninhados não resulta mais na substituição de entradas de mesmo nível dessas estruturas.
* Os campos obrigatórios de RTE não podem mais ser salvos como vazios.
* A formatação no local não é mais aplicada incorretamente ao adicionar links após a formatação.
