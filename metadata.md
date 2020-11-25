---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.pt-BR
index: y
type: Documentation
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html
getting-started-title: Introdução
getting-started-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/home.html
tutorials-title: Tutoriais
tutorials-url: https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 8832307a96160a3d45cc85942473a5ada288a74f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 10%

---


# Metadados para uso interno

Os metadados no sistema de criação do GitHub são hierárquicos e são definidos como os seguintes níveis crescentes de precedência.

1. metadata.md
1. ToC
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o acordo de recompra, mas podem ser substituídos nos níveis ToC e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

Os metadados no depósito experience-manager-cloud-service.en são o mínimo necessário.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

Artigo

* `title`
* `description`
* `contentOwner` (somente no conteúdo dos ativos principais em `/help/assets`)
