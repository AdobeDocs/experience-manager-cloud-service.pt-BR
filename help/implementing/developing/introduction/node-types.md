---
title: Tipos de nó AEM
description: AEM é baseado no Sling e usa um repositório JCR com tipos de nó oferecidos por ambos, mas AEM também fornece um intervalo de seus próprios tipos de nó.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Tipos de nó AEM {#aem-node-types}

Como o AEM é baseado no Sling e usa um repositório JCR, os tipos de nó oferecidos por ambos os padrões estão disponíveis para uso no AEM:

* [Tipos de nó JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de Nó Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Além disso. AEM fornece um intervalo de tipos de nó personalizados. Para a lista mais atual com todas as propriedades associadas, [use o CRXDE](/help/implementing/developing/tools/crxde.md) para navegar pelo seguinte caminho no repositório AEM:

`/jcr:system/jcr:nodeTypes`
