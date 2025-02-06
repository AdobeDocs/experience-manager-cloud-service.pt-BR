---
title: Internacionalizar componentes
description: Internacionalizar seus componentes e caixas de diálogo para que suas cadeias de caracteres da interface do usuário possam ser apresentadas em diferentes idiomas
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Internacionalizar componentes{#internationalizing-components}

Internacionalize seus componentes e caixas de diálogo para que suas cadeias de caracteres da interface do usuário possam ser apresentadas em idiomas diferentes. Os componentes projetados para internacionalização permitem que as sequências de caracteres da interface sejam externalizadas, traduzidas e, em seguida, importadas para o repositório. No tempo de execução, as preferências de idioma do usuário ou o local da página determinam qual idioma é exibido na interface do usuário.

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

Use o processo a seguir para internacionalizar seus componentes e fornecer a interface do usuário em diferentes idiomas:

1. [Implemente seus componentes usando o código que internacionaliza as cadeias de caracteres](/help/implementing/developing/extending/i18n/dev.md). O código identifica as cadeias de caracteres a serem traduzidas e seleciona o idioma a ser apresentado no tempo de execução.
1. Crie dicionários e adicione as cadeias de caracteres em inglês para traduzir.
1. Exporte o dicionário para o formato XLIFF, traduza as cadeias de caracteres e importe os arquivos XLIFF de volta para o AEM.
1. Incorpore o dicionário no processo de gerenciamento de versões do seu aplicativo.

>[!NOTE]
>
>Os métodos descritos aqui para internacionalizar componentes destinam-se a traduzir strings estáticas. Quando espera-se que as cadeias de caracteres do componente mudem, você deve usar fluxos de trabalho de tradução convencionais. Por exemplo, quando os autores podem editar uma sequência de caracteres da interface usando propriedades na caixa de diálogo Editar de um componente, você não deve usar um dicionário de idioma para internacionalizar a sequência.

## Dicionários de idiomas {#language-dictionaries}

A estrutura de internacionalização do AEM usa dicionários no repositório para armazenar strings em inglês e suas traduções em outros idiomas. A estrutura usa inglês como idioma padrão. As cadeias de caracteres são identificadas usando a versão em inglês. Normalmente, as estruturas de internacionalização usam IDs alfanuméricas para strings de interface. O uso da versão em inglês da string como ID tem várias vantagens:

* O código é fácil de ler.
* O idioma padrão está sempre disponível.

As alterações na tradução precisam vir do Git por meio do [pipeline de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) no AEM as a cloud service.

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)


### Sobreposição de strings em dicionários do sistema {#overlaying-strings-in-system-dictionaries}

Se os componentes usarem strings incluídas nos dicionários do sistema AEM, duplique a string no seu próprio dicionário. Todos os componentes usarão as strings do seu dicionário.

Observe que você não pode prever qual tradução é usada quando as cadeias de caracteres são duplicadas em dicionários localizados abaixo do nó `/apps`.
