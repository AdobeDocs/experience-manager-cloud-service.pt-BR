---
title: Processar ativos usando microsserviços de ativos
description: Processe seus ativos digitais usando microsserviços de processamento de ativos escaláveis e nativos da nuvem.
contentOwner: AG
feature: Asset Compute Microservices, Asset Ingestion, Asset Processing
role: Developer, Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 99%

---

# Visão geral da ingestão e processamento de ativos com microsserviços de ativos {#asset-microservices-overview}

O Adobe Experience Manager as a [!DNL Cloud Service] fornece um método nativo da nuvem para usar os aplicativos e os recursos do Experience Manager. Um dos principais elementos dessa nova arquitetura é a ingestão e processamento de ativos, possibilitadas por microsserviços de ativos. Os microsserviços de ativos fornecem um processamento escalável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento. Os principais benefícios dos microsserviços de ativos nativos da nuvem são:

* Arquitetura escalável que permite um processamento contínuo de operações com uso intenso de recursos.
* Indexação e extrações de texto eficientes que não afetam o desempenho de seus ambientes do Experience Manager.
* Minimiza a necessidade de usar fluxos de trabalho para lidar com o processamento de ativos no ambiente do Experience Manager. Isso libera recursos, diminui a carga sobre o Experience Manager e fornece escalabilidade.
* Maior resiliência no processamento de ativos. Possíveis problemas ao manipular arquivos atípicos, como arquivos corrompidos ou extremamente grandes, não afetam mais o desempenho da implantação.
* Configuração simplificada do processamento de ativos para os administradores.
* A configuração de processamento de ativos é gerenciada e mantida pela Adobe para fornecer a configuração mais conhecida para lidar com representações, metadados e extrações de textos para vários tipos de arquivos
* Quando aplicável, os serviços nativos de processamento de arquivos da Adobe são utilizados, o que proporciona resultados de alta fidelidade e garante um [tratamento eficiente dos formatos próprios da Adobe](file-format-support.md).
* Capacidade de configurar o fluxo de trabalho de pós-processamento para adicionar ações e integrações específicas do usuário.

Os microsserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como a transcodificação do [!DNL ImageMagick] e FFmpeg) e simplificam as configurações, além de oferecer funcionalidades básicas para os formatos de arquivo comuns por padrão.

## Arquitetura de alto nível {#asset-microservices-architecture}

Um diagrama de arquitetura de alto nível descreve os principais elementos da ingestão, do processamento e do fluxo dos ativos no sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Ingestão e processamento de ativos com microsserviços de ativos](assets/asset-microservices-overview.png "Ingestão e processamento de ativos com microsserviços de ativos")

As principais etapas da ingestão e do processamento usando microsserviços de ativos são:

* Os clientes, como navegadores da web ou o Adobe Asset Link, enviam uma solicitação de upload para o [!DNL Experience Manager] e iniciam o upload do binário diretamente para o armazenamento binário na nuvem.
* Quando o upload direto do binário é concluído, o cliente notifica o [!DNL Experience Manager].
* O [!DNL Experience Manager] envia uma solicitação de processamento para os microsserviços de ativos. O conteúdo da solicitação depende da configuração dos perfis de processamento no [!DNL Experience Manager], que especifica quais representações serão geradas.
* O back-end dos microsserviços de ativos recebe a solicitação e o envia para um ou mais microsserviços, de acordo com a solicitação. Cada microsserviço acessa o binário original diretamente do armazenamento binário na nuvem.
* Os resultados do processamento, como as representações, são armazenados no armazenamento binário na nuvem.
* O Experience Manager é notificado de que o processamento foi concluído e é apontado diretamente para os binários gerados (representações). As representações geradas estão disponíveis no [!DNL Experience Manager] para o ativo carregado.

Esse é o fluxo básico de ingestão e processamento de ativos. Se configurado, o Experience Manager também pode iniciar o modelo de fluxo de trabalho personalizado para fazer o pós-processamento do ativo. Por exemplo, execute etapas personalizadas específicas para seu ambiente, como buscar informações de um sistema empresarial e adicioná-las nas propriedades do ativo.

O fluxo de ingestão e processamento são conceitos fundamentais da arquitetura dos microsserviços de ativos do Experience Manager.

* **Acesso direto ao binário**: os ativos são transportados (e carregados) para o armazenamento binário na nuvem após serem configurados para ambientes do Experience Manager; em seguida, o [!DNL Experience Manager], os microsserviços de ativos e, por fim, os clientes obtêm acesso direto a eles para realizar seu trabalho. Isso minimiza a carga em redes e a duplicação de binários armazenados
* **Processamento externo**: o processamento de ativos é feito fora do ambiente do [!DNL Experience Manager], e seus recursos são salvos (CPU, memória) para fornecer as principais funcionalidades do Gerenciamento de ativos digitais (DAM) e permitir o trabalho interativo com o sistema para usuários finais

## Upload de ativo com acesso direto ao binário {#asset-upload-with-direct-binary-access}

Os clientes do Experience Manager, que fazem parte da oferta de produtos, todos permitem o upload com acesso direto ao binário por padrão. Isso inclui o upload por meio da interface da web, do Adobe Asset Link e do aplicativo de desktop do [!DNL Experience Manager].

Você pode usar ferramentas de upload personalizadas, que funcionam diretamente com as APIs HTTP do [!DNL Experience Manager]. Você pode usar essas APIs diretamente ou utilizar e estender os seguintes projetos de código aberto que implementam o protocolo de upload:

* [Biblioteca de upload de código aberto](https://github.com/adobe/aem-upload)
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem)

Para obter mais informações, consulte [Fazer upload de ativos](add-assets.md).

## Adicionar pós-processamento de ativo personalizado {#add-custom-asset-post-processing}

Embora a maioria dos clientes deva obter todas as suas necessidades de processamento de ativos dos microsserviços de ativos configuráveis, alguns podem precisar de processamento de ativos adicional. Isso é especialmente verdadeiro se os ativos precisarem ser processados com base nas informações provenientes de outros sistemas por meio de integrações. Em casos como esse, fluxos de trabalho personalizados de pós-processamento podem ser usados.

Os workflows de pós-processamento são modelos de fluxo de trabalho regulares do [!DNL Experience Manager], criados e gerenciados no Editor de fluxo de trabalho do [!DNL Experience Manager]. Os clientes podem configurar os workflows para realizar etapas de processamento adicionais em um ativo, incluindo o uso de etapas de fluxo de trabalho prontas para uso e workflows personalizados disponíveis.

O Adobe Experience Manager pode ser configurado para acionar automaticamente os fluxos de trabalho de pós-processamento após a conclusão do processamento de ativos.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Introdução ao uso dos microsserviços de ativos](asset-microservices-configure-and-use.md)
>* [Formatos de arquivo não suportados](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* Aplicativo de desktop do [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=pt-BR)
>* [Documentação do Apache Oak sobre acesso binário direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)
