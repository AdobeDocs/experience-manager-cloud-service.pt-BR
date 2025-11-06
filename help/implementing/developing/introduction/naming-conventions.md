---
title: Convenções de nomenclatura
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Repositório de conteúdo Java
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Convenções de nomenclatura{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura do Repositório de conteúdo Java. No entanto, o AEM impõe mais convenções para o nome dos nós de página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a implementação do AEM dos [utilitários JCR](#jcr-utilities).
* PageManager: o [Gerenciador de páginas](#page-manager) fornece métodos para operações em nível de página.
* Na interface do AEM {#ui-behavior}

### Utilitários JCR {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) é a implementação do AEM dos utilitários JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`
   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.
* `createValidName`
   * Isso cria um rótulo válido de uma sequência arbitrária.
   * Ela pode ser usada para criar um nome a partir de um título.

### Gerenciador de páginas {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) fornece métodos para operações no nível da página, com base em [JCRUtil](#jcr-utilities).

### Comportamento da interface do usuário do AEM {#ui-behavior}

Ao gerenciar conteúdo, a interface do usuário do AEM:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:
   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido
