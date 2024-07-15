---
title: Conversor de índice
description: Saiba como migrar as Definições de índice em preparação para a migração para o AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Conversor de índice {#index-converter}

O Conversor de índice é um utilitário desenvolvido para migrar as Definições de índice de um cliente, em preparação para a migração para o AEM as a Cloud Service.

## Introdução {#introduction}

O Conversor de índice permite que os desenvolvedores do AEM migrem as definições de índice Oak personalizadas existentes para definições de índice Oak personalizadas compatíveis com o AEM as a Cloud Service.

>[!NOTE]
>O Conversor de Índice transforma apenas as Definições de Índice Oak Personalizado do tipo *lucene* presentes em `/apps` ou `/oak:index`. Ele não transforma índices do tipo *lucene* que são criados para `nt:base`.

Há duas maneiras de criar Definições de índice Oak personalizadas:

* `under /apps` (por meio de qualquer pacote de conteúdo personalizado)
* diretamente no caminho `/oak:index`

Se [Verificar se o Índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) foi usado, verificar se não há suporte para Definições no AEM as a Cloud Service. Dessa forma, eles devem ser convertidos primeiro para Definições de índice do Oak e depois migrados para Definições de índice do Oak personalizadas compatíveis com o AEM as a Cloud Service, de acordo com as diretrizes abaixo:

* Se a propriedade ignore estiver definida como `true`, ignore ou ignore a Definição de Verificação
* Atualizar o `jcr:primaryType` para `oak:QueryIndexDefinition`
* Remova todas as propriedades que devem ser ignoradas, conforme mencionado nas configurações do OSGi
* Remover subárvore `/facets/jcr:content` de Assegurar Definição

## Uso do Conversor de índice {#using-index-converter}

* Por meio da CLI do Adobe I/O : o Adobe recomenda o uso do Conversor de índice por meio do `aio-cli-plugin-aem-cloud-service-migration` (plug-in de refatoração de código AEM as a Cloud Service para a CLI do Adobe I/O).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : o Conversor de índice também pode ser executado como um utilitário independente.

  Consulte **[Recurso do Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para saber como usar esta ferramenta.
