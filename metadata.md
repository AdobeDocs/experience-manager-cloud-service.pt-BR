---
product: adobe experience manager
description: esses são os metadados necessários para as páginas de documentação do AEMaaCS
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.pt-BR
index: y
type: Documentação
solution: Experience Manager
translation-type: tm+mt
source-git-commit: 80a59a02067d478713aa7dcdb436ad1345d89c1a
workflow-type: tm+mt
source-wordcount: '92'
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
