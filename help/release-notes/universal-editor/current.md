---
title: Notas de versão do Universal Editor 2024.09.3
description: Estas são as notas de versão do Universal Editor 2024.09.3.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b70acef8dc259fff3041617abe0a89f7eb73dfab
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# Notas de versão do Universal Editor 2024.09.3 {#release-notes}

Estas são as notas de versão da versão de 3 de setembro de 2024 do Universal Editor.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novidades {#what-is-new}

* **`rootPath`agora disponível para o seletor de conteúdo**: o seletor de conteúdo agora pode ser fornecido com um `rootPath` para apresentar ao usuário uma seleção de conteúdo direcionada ao usar os tipos de campo [Conteúdo AEM,](/help/implementing/universal-editor/field-types.md#aem-content) [Fragmento de Conteúdo,](/help/implementing/universal-editor/field-types.md#content-fragment) e [Fragmento de Experiência](/help/implementing/universal-editor/field-types.md#experience-fragment).
   * A seleção de conteúdo é, portanto, limitada ao conteúdo no caminho especificado e em quaisquer subdiretórios.

## Programa de adoção antecipada para suporte ao 6.5 {#early-adoption}

O Editor universal agora está disponível para casos de uso headless ao usar o AEM 6.5 como parte de um programa de adoção antecipada.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para o representante da Adobe pelo endereço de email associado à sua Adobe ID.

## Correções de erros {#bug-fixes}

* **Arrastar e soltar entre contêineres**: [Mover componentes entre diferentes contêineres por meio do recurso de arrastar e soltar](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) agora respeita os [filtros de componentes](/help/implementing/universal-editor/customizing.md#filtering-components) tanto na origem quanto no destino.
