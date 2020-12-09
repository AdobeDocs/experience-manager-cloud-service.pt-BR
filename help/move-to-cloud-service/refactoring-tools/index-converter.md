---
title: Conversor de índice
description: Conversor de índice
translation-type: tm+mt
source-git-commit: 1117f03b2eff37f8b25726c3dc60d5a3fe98a5d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Conversor de índice {#index-converter}

Index Converter é um utilitário desenvolvido para migrar as Definições de índice de um cliente em preparação para a mudança para AEM como Cloud Service.

## Introdução {#introduction}

O Conversor de índice permite que os desenvolvedores AEM migrem as Definições existentes do Índice de Oak personalizado para AEM como Definições de índice de Oak personalizado compatíveis com Cloud Service.

>[!NOTE]
>O Conversor de índice só transforma *lucene* tipo Definições de índice de Oak personalizado que estão presentes em `/apps` ou `/oak:index`. Ele não transforma índices de tipo *lucene* que são criados para `nt:base`.

Há duas maneiras de criar Definições de índice de Oak personalizado:

* `under /apps` (por meio de qualquer pacote de conteúdo personalizado)
* diretamente sob o caminho `/oak:index`

Se [Certifique-se de que o índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) foi usado, observe que a opção Verificar se as Definições não são suportadas no AEM como um Cloud Service e, portanto, elas precisam ser convertidas em Definições de índice Oak e migradas para Definições de índice Oak personalizado compatíveis com AEM como Cloud Service de acordo com as diretrizes abaixo:

* Se a propriedade ignore estiver definida como `true`, ignore ou ignore a Definição de garantia
* Atualize `jcr:primaryType` para `oak:QueryIndexDefinition`
* Remova quaisquer propriedades que devem ser ignoradas como mencionado nas configurações OSGi
* Remover a subárvore `/facets/jcr:content` da Definição de Garantia

## Usando o Conversor de índice {#using-index-converter}

* Por meio do Adobe I/O CLI: É recomendável usar o Conversor de índice por `aio-cli-plugin-aem-cloud-service-migration` (AEM como um plug-in de refatoração de código de Cloud Service para a CLI do Adobe I/O).

Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente: O Conversor de índice também pode ser executado como um utilitário independente.

Consulte **[Recurso Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para saber como usar essa ferramenta.



