---
product: adobe experience manager
description: Documentação do Adobe Experience Manager as a Cloud Service.
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.pt-BR
index: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 49%

---


# Metadados para uso interno

Os metadados no sistema de criação do GitHub são hierárquicos e definidos nos seguintes níveis crescentes de precedentes.

1. metadata.md
1. Índice
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o repositório, mas podem ser substituídos nos níveis de índice e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

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

Índices

* `sub-product`
* `user-guide-title`

Artigo

* `title`
* `description`
* `contentOwner` (somente no conteúdo do ativo principal em `/help/assets`)
