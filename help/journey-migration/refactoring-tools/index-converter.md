---
title: Conversor de índice
description: Conversor de índice
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Conversor de índice {#index-converter}

O Index Converter é um utilitário desenvolvido para migrar as Definições de Índice de um cliente em preparação para a mudança para AEM as a Cloud Service.

## Introdução {#introduction}

O Conversor de Índice permite AEM desenvolvedores migrarem Definições de Índice Oak Personalizado existentes para AEM Definições de Índice Oak Personalizado e as a Cloud Service compatíveis.

>[!NOTE]
>O Conversor de índice só transforma *lucene* digite Definições do Índice Oak personalizado que estão presentes em `/apps` ou `/oak:index`. Não transforma *lucene* índices do tipo criados para `nt:base`.

Há duas maneiras de criar Definições de Índice Oak Personalizado:

* `under /apps` (por meio de qualquer pacote de conteúdo personalizado)
* diretamente em `/oak:index` caminho

If [Assegure o índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) foi usado, observe que as Definições de garantir que não sejam suportadas em AEM as a Cloud Service e, portanto, elas precisam ser convertidas em Definições de Índice Oak primeiro e, em seguida, precisam ser migradas para Definições de Índice Oak Personalizado que sejam compatíveis com AEM as a Cloud Service de acordo com as diretrizes abaixo:

* Se a propriedade ignore estiver definida como `true`, ignore ou ignore a definição de garantir
* Atualize o `jcr:primaryType` para `oak:QueryIndexDefinition`
* Remova quaisquer propriedades que devam ser ignoradas, conforme mencionado nas configurações OSGi
* Remover subárvore `/facets/jcr:content` em Garantir definição

## Uso do Conversor de índice {#using-index-converter}

* Via Adobe I/O CLI : É recomendável usar o Conversor de índice por meio de `aio-cli-plugin-aem-cloud-service-migration` (AEM plug-in de refatoração de código as a Cloud Service para o Adobe I/O CLI).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : O Conversor de índice também pode ser executado como um utilitário independente.

   Consulte **[Recurso Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para saber como usar essa ferramenta.
