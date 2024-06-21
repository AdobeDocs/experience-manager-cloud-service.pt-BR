---
title: Reutilizar fragmentos de conteúdo usando MSM e Live Copies
description: Saiba mais sobre como usar a funcionalidade de Live Copy do MSM para usar o mesmo conteúdo de fragmento de conteúdo, ou similar, em vários locais, enquanto sincroniza com o conteúdo original.
exl-id: f050b2d1-856c-4cdb-ac74-bc78016f144a
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# Reutilizar fragmentos de conteúdo usando o MSM {#reuse-content-fragments-using-msm}

O Gerenciador de vários sites (MSM) e a funcionalidade de Live Copy permitem usar o mesmo conteúdo em vários locais, ao mesmo tempo em que são sincronizados com o conteúdo original.

* Com as Live Copies do MSM é possível:
   * Criar um conteúdo uma vez e
   * Reutilizar esse conteúdo em outras áreas do mesmo site ou de outros sites ou aplicativos.
* O MSM mantém os relacionamentos dinâmicos entre o conteúdo original e suas Live Copies, de modo que:
   * Quando você altera o conteúdo original, ele e as Live Copies são sincronizados.
   * É possível fazer ajustes somente no conteúdo das Live Copies, desconectando o relacionamento dinâmico de subpáginas e/ou componentes individuais.

Para obter uma visão geral detalhada dos conceitos do MSM, consulte [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[Gerenciador de vários sites (MSM)](/help/sites-cloud/administering/msm/overview.md) A funcionalidade no Adobe Experience Manager permite que os usuários reutilizem o conteúdo criado uma vez e depois reutilizado em vários locais da Web.

Ao usar o MSM para fragmentos de conteúdo, você pode:

* Crie fragmentos de conteúdo uma vez e faça cópias (vinculadas) desses fragmentos para reutilizar em outras áreas do site ou aplicativo.
* Manter várias cópias sincronizadas atualizando a cópia de origem uma vez e, em seguida, enviando as alterações para as cópias (ativas).
* Fazer alterações locais temporariamente ou permanentemente, suspendendo o vínculo entre fragmentos pai e filho; completamente ou para suas variações ou campos.

O MSM para fragmentos de conteúdo, combinado com a funcionalidade no Editor de fragmento de conteúdo, permite quebrar e restaurar a herança no nível do campo.

>[!CAUTION]
>
>O MSM para fragmentos de conteúdo só está disponível ao usar fragmentos de conteúdo por meio do **Assets** console.
>
>A funcionalidade do MSM é *não* disponível ao usar o **Fragmentos de conteúdo** console.

## Como {#how-to}

Consulte a documentação a seguir para obter detalhes sobre o uso do MSM para fragmentos de conteúdo (também aplicável a ativos):

* Como usar [MSM para fragmentos de conteúdo (e ativos)](/help/assets/reuse-assets-using-msm.md)

* [Criar uma Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Se você quiser usar o MSM para criar cópias de Fragmentos de conteúdo), qualquer **Exclusivo** restrições devem ser removidas de qualquer Tipo de dados usado nos respectivos [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md).

* [Exibir propriedades e status da origem e da Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Propagar modificações da origem para a Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Cancelar e restaurar a herança de:
   * campos e variações no [Editor de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadados de ativos relacionados](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Suspender e retomar a relação](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Remover o relacionamento dinâmico](/help/assets/reuse-assets-using-msm.md#detach)
* [Comparar o MSM para fragmentos de conteúdo (e ativos) com o MSM para sites](/help/assets/reuse-assets-using-msm.md#comparison)

## Limitações {#limitations}

* Os acionadores durante a modificação e a configuração de implantação associada não existem para Fragmentos de conteúdo.
