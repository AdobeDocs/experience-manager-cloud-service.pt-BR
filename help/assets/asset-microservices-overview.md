---
title: Processar ativos usando microsserviços de ativos
description: Processe seus ativos digitais usando microsserviços de processamento de ativos escaláveis e nativos em nuvem.
contentOwner: AG
feature: Microserviços do Asset compute, Fluxo de trabalho, Informações da versão, Processamento de ativos
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 2%

---

# Visão geral da assimilação e do processamento de ativos com microsserviços de ativos {#asset-microservices-overview}

O Adobe Experience Manager as a [!DNL Cloud Service] fornece um método nativo em nuvem para aproveitar os aplicativos e os recursos do Experience Manager. Um dos principais elementos dessa nova arquitetura é a assimilação e o processamento de ativos, alimentados por microsserviços de ativos. Os microsserviços de ativos fornecem um processamento escalável e resiliente de ativos usando serviços em nuvem. O Adobe gerencia os serviços em nuvem para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento. Os principais benefícios dos microsserviços de ativos nativos em nuvem são:

* Arquitetura escalável que permite um processamento contínuo para operações com uso intenso de recursos.
* Indexação eficiente e extrações de texto que não afetam o desempenho de seus ambientes Experience Manager.
* Minimize a necessidade de fluxos de trabalho para lidar com o processamento de ativos no ambiente Experience Manager. Isso libera recursos, minimiza a carga no Experience Manager e fornece escalabilidade.
* Maior resiliência do processamento de ativos. Possíveis problemas ao manipular arquivos atípicos, como arquivos corrompidos ou arquivos extremamente grandes, não afetam mais o desempenho da implantação.
* Configuração simplificada do processamento de ativos para os administradores.
* A configuração de processamento de ativos é gerenciada e mantida pelo Adobe para fornecer a configuração mais conhecida para lidar com representações, metadados e extração de texto para vários tipos de arquivos
* Os serviços de processamento de arquivos Adobe nativos são usados, quando aplicável, fornecendo saída de alta fidelidade e [manuseio eficiente de formatos proprietários de Adobe](file-format-support.md).
* Capacidade de configurar o fluxo de trabalho de pós-processamento para adicionar ações e integrações específicas do usuário.

Os microsserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como [!DNL ImageMagick] e transcodificação FFmpeg) e simplificam as configurações, além de fornecer a funcionalidade básica para os formatos de arquivo comuns por padrão.

## Arquitetura de alto nível {#asset-microservices-architecture}

Um diagrama de arquitetura de alto nível descreve os principais elementos de assimilação de ativos, processamento e fluxo de ativos no sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Assimilação e processamento de ativos com ](assets/asset-microservices-overview.png "microsserviços de ativosAssimilação e processamento de ativos com microsserviços de ativos")

As principais etapas da assimilação e do processamento usando microsserviços de ativos são:

* Os clientes, como navegadores da Web ou Adobe Asset Link, enviam uma solicitação de upload para [!DNL Experience Manager] e começam a fazer upload do binário diretamente no armazenamento da nuvem binária.
* Quando o upload binário direto é concluído, o cliente notifica [!DNL Experience Manager].
* [!DNL Experience Manager] envia uma solicitação de processamento para microsserviços de ativos. O conteúdo da solicitação depende da configuração dos perfis de processamento em [!DNL Experience Manager] que especifica, quais renderizações serão geradas.
* O back-end dos microsserviços de ativos recebe a solicitação, a despacha para um ou mais microsserviços com base na solicitação. Cada microsserviço acessa o binário original diretamente da loja de nuvem binária.
* Os resultados do processamento, como representações, são armazenados no armazenamento binário em nuvem.
* O Experience Manager é notificado de que o processamento está concluído, juntamente com ponteiros diretos para os binários gerados (execuções). As representações geradas estão disponíveis em [!DNL Experience Manager] para o ativo carregado.

Esse é o fluxo básico de assimilação e processamento de ativos. Se configurado, o Experience Manager também pode iniciar o modelo de fluxo de trabalho personalizado para fazer o pós-processamento do ativo. Por exemplo, execute etapas personalizadas específicas para seu ambiente, como buscar informações de um sistema empresarial e adicionar às propriedades do ativo.

O fluxo de assimilação e processamento são conceitos-chave da arquitetura de microsserviços de ativos para o Experience Manager.

* **Acesso** binário direto: Os ativos são transportados (e carregados) para a Loja Binária da Nuvem depois de configurados para ambientes do Experience Manager e, em seguida,  [!DNL Experience Manager], microsserviços de ativos e, finalmente, os clientes obtêm acesso direto a eles para realizar seu trabalho. Isso minimiza a carga em redes e a duplicação de binários armazenados
* **Processamento** externo: O processamento de ativos é feito fora do  [!DNL Experience Manager] ambiente e salva seus recursos (CPU, memória) para fornecer as principais funcionalidades do Gerenciamento de ativos digitais (DAM) e suportar o trabalho interativo com o sistema para usuários finais

## Upload de ativo com acesso binário direto {#asset-upload-with-direct-binary-access}

Os clientes do Experience Manager, que fazem parte da oferta de produtos, todos suportam upload com acesso binário direto por padrão. Isso inclui upload usando a interface da Web, o Adobe Asset Link e o [!DNL Experience Manager] aplicativo de desktop.

Você pode usar ferramentas de upload personalizadas, que funcionam diretamente com [!DNL Experience Manager] APIs HTTP. Você pode usar essas APIs diretamente ou usar e estender os seguintes projetos de código aberto que implementam o protocolo de upload:

* [Biblioteca de upload de código aberto](https://github.com/adobe/aem-upload)
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem)

Para obter mais informações, consulte [fazer upload de ativos](add-assets.md).

## Adicionar pós-processamento de ativo personalizado {#add-custom-asset-post-processing}

Embora a maioria dos clientes deva obter todas as suas necessidades de processamento de ativos dos microsserviços de ativos configuráveis, alguns podem precisar de processamento de ativos adicional. Isso é especialmente verdadeiro se os ativos precisarem ser processados com base nas informações provenientes de outros sistemas por meio de integrações. Em casos como esse, fluxos de trabalho personalizados de pós-processamento podem ser usados.

Os workflows de pós-processamento são modelos de workflow regulares [!DNL Experience Manager], criados e gerenciados no [!DNL Experience Manager] Editor de workflow. Os clientes podem configurar os fluxos de trabalho para realizar etapas de processamento adicionais em um ativo, incluindo o uso de etapas de fluxo de trabalho prontas para uso e fluxos de trabalho personalizados disponíveis.

O Adobe Experience Manager pode ser configurado para acionar automaticamente os fluxos de trabalho de pós-processamento após a conclusão do processamento de ativos.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introdução ao uso dos microsserviços de ativos](asset-microservices-configure-and-use.md)
* [Formatos de arquivo não suportados](file-format-support.md)
* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
* Aplicativo de desktop do [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
* [Documentação do Apache Oak sobre acesso binário direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

