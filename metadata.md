---
product: adobe experience manager
description: Documentação do Adobe Experience Manager as a Cloud Service.
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.pt-BR
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
cloud: Experience Cloud
translation-type: tm+mt
source-git-commit: 6908b5215dcbff0692d4e03dd1588ca5d34aeffe
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 7%

---


# Metadados para uso interno

Os metadados no sistema de criação do GitHub são hierárquicos e são definidos com os seguintes níveis crescentes de precedente.

1. metadata.md
1. ToC
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o repositório, mas podem ser substituídos nos níveis de ToC e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

Os metadados no repositório experience-manager-cloud-service.en são o mínimo necessário.

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
* `contentOwner` (somente no conteúdo dos ativos principais em  `/help/assets`)
