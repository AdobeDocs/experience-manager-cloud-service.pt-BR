---
title: Convenções de nomenclatura
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 17%

---

# Convenções de nomenclatura{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository. No entanto, AEM impõe mais convenções para o nome dos nós da página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a AEM da aplicação do [Utilitários JCR](#jcr-utilities).
* PageManager: o [Gerenciador de página](#page-manager) O fornece métodos para operações no nível da página.
* Na interface do usuário do AEM {#ui-behavior}

### Utilitários JCR {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) é a AEM implementação dos utilitários JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`
   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.
* `createValidName`
   * Isso cria um rótulo válido de uma cadeia de caracteres arbitrária.
   * Ele pode ser usado para criar um nome a partir de um título.

### Gerenciador de página {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) O fornece métodos para operações de nível de página, com base em [JCRUtil](#jcr-utilities).

### Comportamento da interface do usuário do AEM {#ui-behavior}

Ao gerenciar conteúdo, a interface do usuário do AEM:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:
   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido
