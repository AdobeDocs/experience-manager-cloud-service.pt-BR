---
title: Problemas conhecidos
description: Problemas conhecidos com o Adobe Experience Manager as a Cloud Service
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 66%

---

# Problemas conhecidos {#known-issues}

Este artigo lista os problemas conhecidos da oferta [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. A lista é revisada e atualizada a cada versão contínua do [!DNL Experience Manager].

[Entre em contato com o suporte](https://experienceleague.adobe.com/?lang=pt-BR&amp;support-solution=Experience+Manager#support) para obter mais informações sobre os problemas conhecidos.

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

Alguns problemas conhecidos no [!DNL Sites] são:

* No GraphQL IDE é possível [gerencie o cache de suas consultas persistentes](/help/headless/graphql-api/graphiql-ide.md##managing-cache).
   * Na primeira vez em que os valores salvos para os cabeçalhos são definidos como `0` (em vez dos valores padrão) - se o usuário não tiver alterado esses valores na caixa de diálogo.
   * Nos salvamentos subsequentes, os valores são salvos corretamente.
   * Portanto, o usuário precisa salvar os cabeçalhos duas vezes.

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alguns problemas conhecidos no [!DNL Assets] são:

* **Download**: ao baixar uma pasta vazia, o [!DNL Experience Manager] transmite uma mensagem de sucesso sobre a criação de um arquivo ZIP, mas o arquivo não é criado.

* **Esquema de metadados**: o dispositivo de classificação de ativos usado para causar erro de compilação de JSP. Foi removido do esquema de metadados. <!-- CQ-4282865, CQ-4284633 -->

Além disso, consulte [alterações importantes no [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md).

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [Principais alterações no [!DNL Experience Manager]](aem-cloud-changes.md)
>* [Recursos obsoletos e removidos](deprecated-removed-features.md)
>* [Notas de versão](home.md)

