---
title: Conversor de índice
description: Conversor de índice
translation-type: tm+mt
source-git-commit: 21bd9392d913369a5e8e0ebd9badbbe30fd4bba3
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Conversor de índice {#index-converter}

Index Converter é um utilitário desenvolvido para migrar a definição de índice de um cliente em preparação para a mudança para AEM como Cloud Service.

## Introdução {#introduction}

O Index Converter permite que AEM desenvolvedores migrem as Definições de Índice de Oak Personalizado para AEM como Definições de Índice de Oak Personalizado compatíveis com Cloud Service.

>[!NOTE]
>O Conversor de índice só transforma *lucene* tipo Definições de índice de Oak personalizado que estão presentes em `/apps` ou `/oak:index`. Ele não transforma índices de tipo *lucene* que são criados para `nt:base`.

## Usando o Conversor de índice {#using-index-converter}

Consulte **[Recurso Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

