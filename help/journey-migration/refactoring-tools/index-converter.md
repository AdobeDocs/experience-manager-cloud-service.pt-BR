---
title: Conversor de índice
description: Saiba como migrar as Definições de índice em preparação para a mudança para o AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Conversor de índice {#index-converter}

O Conversor de índice é um utilitário desenvolvido para migrar as Definições de índice de um cliente em preparação para a mudança para o AEM as a Cloud Service.

## Introdução {#introduction}

O Conversor de índice permite que os desenvolvedores do AEM migrem as definições de índice Oak personalizado existentes para definições de índice Oak personalizado compatíveis com AEM as a Cloud Service.

>[!NOTE]
>Somente o Conversor de índice transforma *lucene* Definições de índice Oak personalizado do tipo presentes em `/apps` ou `/oak:index`. Não transforma *lucene* índices do tipo criados para `nt:base`.

Há duas maneiras de criar definições de índice Oak personalizadas:

* `under /apps` (por meio de qualquer pacote de conteúdo personalizado)
* diretamente em `/oak:index` caminho

Se [Garantir índice do Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) foi usada, Verifique se as definições não são compatíveis com o AEM as a Cloud Service. Dessa forma, eles devem ser convertidos primeiro para Definições de índice Oak e, em seguida, migrados para Definições de índice Oak personalizadas compatíveis com o AEM as a Cloud Service, de acordo com as diretrizes abaixo:

* Se a propriedade ignorar estiver definida como `true`, ignorar ou ignorar a Definição de Garantia
* Atualize o `jcr:primaryType` para `oak:QueryIndexDefinition`
* Remova todas as propriedades que devem ser ignoradas, conforme mencionado nas configurações do OSGi
* Remover subárvore `/facets/jcr:content` em Garantir definição

## Uso do Conversor de índice {#using-index-converter}

* Por meio da CLI do Adobe I/O : é recomendável usar o Conversor de Índice por meio de `aio-cli-plugin-aem-cloud-service-migration` (Plug-in de refatoração de código as a Cloud Service AEM para a CLI do Adobe I/O).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : o Conversor de índice também pode ser executado como um utilitário independente.

  Consulte **[Recurso do Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para saber como usar esta ferramenta.
