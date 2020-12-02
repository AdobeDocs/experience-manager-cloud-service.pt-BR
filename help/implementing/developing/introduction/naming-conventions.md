---
title: Convenções de nomenclatura
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 14%

---


# Nomeando Convenções{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository. No entanto, AEM impõem outras convenções para o nome dos nós de página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a implementação AEM de [utilitários JCR](#jcr-utilities).
* PageManager: o [Page Manager](#page-manager) fornece métodos para operações de nível de página.
* Na interface do usuário AEM {#ui-behavior}

### Utilitários JCR {#jcr-utilities}

[O ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis é a implementação AEM dos utilitários do JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`
   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.
* `createValidName`
   * Isso cria um rótulo válido a partir de uma string arbitrária.
   * Ele pode ser usado para criar um nome a partir de um título.

### Gerenciador de páginas {#page-manager}

[O ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager fornece métodos para operações de nível de página, com base em  [JCRUtil](#jcr-utilities).

### Comportamento da interface do usuário AEM {#ui-behavior}

Ao gerenciar conteúdo, a interface do usuário AEM:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:
   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido
