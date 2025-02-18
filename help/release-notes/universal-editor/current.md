---
title: Notas de versão do Universal Editor 2025.02.17
description: Estas são as notas de versão do Universal Editor de 2025.02.17.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c88aa13c6bc75c8f9cd624d00ef768290981c840
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Notas de versão do Universal Editor 2025.02.17 {#release-notes}

Estas são as notas de versão da versão de 17 de fevereiro de 2025 do Universal Editor.

>[!TIP]
>
>Para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service, consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novidades {#what-is-new}

* **Publicar para visualização** - [Ao publicar (ou desfazer a publicação) seu conteúdo](/help/sites-cloud/authoring/universal-editor/publishing.md) usando o Universal Editor, agora você pode escolher se deseja publicar no seu [ambiente de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md), além do ambiente de publicação
   * Isso permite a análise do seu conteúdo antes da publicação pública.
* **Modelo e filtro podem ser definidos na definição de componente** - Agora é possível definir qual modelo e filtro um componente usa [na definição de componente.](/help/implementing/universal-editor/component-definition.md#template)
   * Essas informações podem ser mantidas centralmente na definição e não precisam ser especificadas na instrumentação.
   * Isso permite mover componentes entre contêineres.
* **Elementos filho de contêineres são considerados implicitamente componentes** - Se [um item com `data-aue-resource`](/help/implementing/universal-editor/attributes-types.md#data-properties) for colocado como filho direto em um contêiner, ele será considerado um componente e poderá ser movido sem precisar especificar `data-aue-behavior="component"`.

## Outras melhorias {#other-improvements}

* **Seletor de ativos do AEM 6.5** - O seletor de ativos do 6.5 agora abre corretamente ao [executar o Editor universal com o AEM 6.5.](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
