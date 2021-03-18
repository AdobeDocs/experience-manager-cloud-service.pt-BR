---
title: Convenções de nomenclatura
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 15%

---


# Convenções de nomenclatura{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository. No entanto, AEM impõe mais convenções para o nome dos nós da página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a implementação AEM dos [utilitários JCR](#jcr-utilities).
* PageManager: o [Gerenciador de páginas](#page-manager) fornece métodos para operações no nível da página.
* Na interface do usuário do AEM {#ui-behavior}

### Utilitários JCR {#jcr-utilities}

[](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis a implementação AEM dos utilitários JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`
   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.
* `createValidName`
   * Isso cria um rótulo válido de uma cadeia de caracteres arbitrária.
   * Ele pode ser usado para criar um nome a partir de um título.

### Gerenciador de página {#page-manager}

[](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) O PageManager fornece métodos para operações no nível da página, com base no  [JCRUtil](#jcr-utilities).

### Comportamento da interface do usuário de AEM {#ui-behavior}

Ao gerenciar conteúdo, a interface do usuário do AEM:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:
   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido
