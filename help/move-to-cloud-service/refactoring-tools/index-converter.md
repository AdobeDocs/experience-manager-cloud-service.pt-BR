---
title: Conversor de índice
description: Conversor de índice
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Conversor de índice {#index-converter}

Index Converter é um utilitário desenvolvido para migrar a definição de índice de um cliente em preparação para a mudança para AEM como Cloud Service.

## Introdução {#introduction}

O Index Converter permite que AEM desenvolvedores migrem as Definições de Índice de Oak Personalizado para AEM como Definições de Índice de Oak Personalizado compatíveis com Cloud Service.

>[!NOTE]
>O Conversor de índice só transforma *lucene* tipo Definições de índice de Oak personalizado que estão presentes em `/apps` ou `/oak:index`. Ele não transforma índices de tipo *lucene* que são criados para `nt:base`.

Há duas maneiras de criar Definições de índice de Oak personalizado:

* `under /apps` (por meio de qualquer pacote de conteúdo personalizado)
* diretamente sob o caminho `/oak:index`

>[!NOTE]
>Consulte [Verifique o índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) para saber como definir e criar definições Oak

## Usando o Conversor de índice {#using-index-converter}

>[!NOTE]
>Embora seja recomendável usar a ferramenta Conversor de índice por meio do [plug-in AIO CLI para migração de origem](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration), também é possível executá-la separadamente.

Consulte **[Recurso Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para saber como instalar e usar o plug-in.

