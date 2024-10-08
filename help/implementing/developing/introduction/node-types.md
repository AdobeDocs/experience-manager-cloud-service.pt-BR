---
title: Tipos de nós do AEM
description: O AEM é baseado no Sling e usa um repositório JCR com tipos de nó oferecidos por ambos, mas o AEM também fornece uma variedade de seus próprios tipos de nó.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 6%

---

# Tipos de nós do AEM {#aem-node-types}

Como o AEM é baseado no Sling e usa um repositório JCR, os tipos de nó oferecidos por esses dois padrões estão disponíveis para uso no AEM:

* [Tipos de nós JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de Nó do Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Além desses. O AEM fornece uma variedade de tipos de nós personalizados. Para a lista mais atual com todas as propriedades associadas, [use o CRXDE](/help/implementing/developing/tools/crxde.md) para procurar o seguinte caminho no repositório AEM:

`/jcr:system/jcr:nodeTypes`
