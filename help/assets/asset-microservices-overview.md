---
title: Saiba como os microserviços de ativos podem processar seus ativos digitais na nuvem
description: Processar seus ativos digitais usando microserviços de processamento de ativos escaláveis e nativos na nuvem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---


# Visão geral da assimilação e processamento de ativos com microserviços de ativos {#asset-microservices-overview}

O Adobe Experience Manager como Cloud Service fornece um método nativo de nuvem para aproveitar os aplicativos e os recursos do Experience Manager. Um dos elementos chave dessa nova arquitetura é a ingestão e o processamento de ativos, impulsionados por microserviços de ativos. Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o melhor tratamento de diferentes tipos de ativos e opções de processamento. Os principais benefícios dos microserviços de ativos nativos na nuvem são:

* Arquitetura escalável que permite um processamento ininterrupto para operações com grande quantidade de recursos.
* Indexação eficiente e extrações de texto que não afetam o desempenho dos ambientes de Experience Manager.
* Minimize a necessidade de workflows para lidar com o processamento de ativos no ambiente Experience Manager. Isso libera recursos, minimiza a carga no Experience Manager e proporciona escalabilidade.
* Maior capacidade de resistência do processamento de ativos. Os possíveis problemas ao lidar com arquivos atípicos, como arquivos corrompidos ou arquivos extremamente grandes, não afetam mais o desempenho da implantação.
* Configuração simplificada do processamento de ativos para os administradores.
* A configuração de processamento de ativos é gerenciada e mantida pela Adobe para fornecer a melhor configuração conhecida para lidar com execuções, metadados e extração de texto para vários tipos de arquivos
* Os serviços nativos de processamento de arquivos da Adobe são usados onde for aplicável, fornecendo saída de alta fidelidade e manuseio [eficiente de formatos](file-format-support.md)proprietários da Adobe.
* Capacidade de configurar o fluxo de trabalho de pós-processamento para adicionar ações e integrações específicas do usuário.

Os microserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como a transcodificação de ImageMagick e FFmpeg) e a simplificar as configurações, além de fornecer funcionalidade pronta para uso para tipos de arquivos comuns.

## Arquitetura de alto nível {#asset-microservices-architecture}

Um diagrama de arquitetura de alto nível descreve os principais elementos de assimilação de ativos, processamento e fluxo de ativos em todo o sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Inclusão e processamento de ativos com](assets/asset-microservices-overview.png "microserviços de ativosingestão e processamento de ativos com microserviços de ativos")

As etapas principais da ingestão e processamento usando microserviços de ativos são:

* Os clientes, como navegadores da Web ou o Adobe Asset Link, enviam uma solicitação de upload para o Experience Manager e o start que carregam o binário diretamente no armazenamento da nuvem binária.
* Quando o carregamento binário direto é concluído, o cliente notifica Experience Manager.
* A Experience Manager envia uma solicitação de processamento para os microserviços do ativo. O conteúdo da solicitação depende da configuração dos perfil de processamento no Experience Manager que especifica, quais execuções serão geradas.
* O back-end dos microserviços do Assets recebe a solicitação, despacha-a para um ou mais microserviços com base na solicitação. Cada microserviço acessa o binário original diretamente da loja da nuvem binária.
* Os resultados do processamento, como execuções, são armazenados no armazenamento da nuvem binária.
* Experience Manager é notificado de que o processamento está concluído, juntamente com ponteiros diretos para os binários gerados (execuções). As representações geradas estão disponíveis no Experience Manager para o ativo carregado.

Esse é o fluxo básico de assimilação e processamento de ativos. Se configurado, o Experience Manager também pode start um modelo de fluxo de trabalho personalizado para fazer o pós-processamento do ativo. Por exemplo, execute etapas personalizadas específicas ao seu ambiente, como buscar informações de um sistema empresarial e adicionar às propriedades do ativo.

O fluxo de ingestão e processamento são conceitos-chave da arquitetura de microserviços do ativo para o Experience Manager.

* **Acesso** binário direto: Os ativos são transportados (e carregados) para a loja binária da nuvem uma vez configurados para ambientes Experience Manager, e então o AEM, os microserviços de ativos e, por fim, os clientes obtêm acesso direto a eles para realizar seu trabalho. Isso minimiza a carga nas redes e a duplicação dos binários armazenados
* **Processamento** externo: O processamento de ativos é feito fora do ambiente AEM e salva seus recursos (CPU, memória) para fornecer as principais funcionalidades do Gerenciamento de ativos digitais e suportar o trabalho interativo com o sistema para usuários finais

## Carregamento de ativos com acesso binário direto {#asset-upload-with-direct-binary-access}

Os clientes Experience Manager, que fazem parte da oferta de produtos, todos suportam upload com acesso binário direto por padrão. Eles incluem carregar usando a interface da Web, o Adobe Asset Link e o aplicativo de desktop do AEM.

Você pode usar ferramentas de upload personalizadas, que funcionam diretamente com APIs HTTP AEM. Você pode usar essas APIs diretamente ou usar e estender os seguintes projetos de código aberto que implementam o protocolo de upload:

* [Biblioteca de upload de código aberto](https://github.com/adobe/aem-upload)
* [Ferramenta de linha de comando open-source](https://github.com/adobe/aio-cli-plugin-aem)

Para obter mais informações, consulte [fazer upload de ativos](add-assets.md).

## Adicionar pós-processamento de ativos personalizados {#add-custom-asset-post-processing}

Embora a maioria dos clientes deva obter todas as suas necessidades de processamento de ativos dos microserviços de ativos configuráveis, alguns podem precisar de processamento de ativos adicionais. Isso é especialmente verdadeiro se os ativos precisarem ser processados com base em informações provenientes de outros sistemas por meio de integrações. Em casos como esse, workflows de pós-processamento personalizados podem ser usados.

Os workflows de pós-processamento são modelos regulares de fluxo de trabalho do AEM, criados e gerenciados no editor de fluxo de trabalho do AEM. Os clientes podem configurar os workflows para realizar etapas de processamento adicionais em um ativo, incluindo o uso de etapas de fluxo de trabalho prontas e workflows personalizados disponíveis.

O Adobe Experience Manager pode ser configurado para acionar automaticamente os workflows de pós-processamento após a conclusão do processamento do ativo.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introdução ao uso dos microsserviços de ativos](asset-microservices-configure-and-use.md)
>* [Formatos de arquivo não suportados](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [Aplicativo de desktop do AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)
>* [Documentação do Apache Oak sobre acesso binário direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

