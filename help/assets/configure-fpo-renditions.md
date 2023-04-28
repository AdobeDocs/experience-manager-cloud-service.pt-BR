---
title: Gerar para representações somente posicionamento para o Adobe InDesign
description: Gere representações FPO de ativos novos e existentes usando o fluxo de trabalho do Experience Manager Assets e o ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Gerar para representações somente posicionamento para o Adobe InDesign {#fpo-renditions}

Ao colocar ativos de grande porte do Experience Manager em documentos do Adobe InDesign, um profissional criativo deve aguardar por um tempo substancial depois que eles [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está bloqueado de usar o InDesign. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos InDesign para começar. Quando a saída final é necessária, digamos, para fluxos de trabalho de impressão e publicação, os ativos originais de resolução completa substituem a representação temporária em segundo plano. Essa atualização assíncrona em segundo plano acelera o processo de design para melhorar a produtividade e não dificulta o processo criativo.

Os ativos fornecem representações que são usadas somente para posicionamento (FPO). Essas renderizações de FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção. Se uma representação FPO não estiver disponível para um ativo, o Adobe InDesign usará o ativo original. Esse mecanismo de fallback garante que o fluxo de trabalho criativo continue sem interrupções.

O Experience Manager as a Cloud Service oferece recursos de processamento de ativos nativos em nuvem para gerar as representações FPO. Use microsserviços de ativos para geração de representação. Você pode configurar a geração de representação de ativos recém-carregados e dos ativos que existem no Experience Manager.

A seguir estão as etapas para gerar representações de FPO:

1. [Criar um perfil de processamento](#create-processing-profile).

1. Configure o Experience Manager para usar este perfil para [processar novos ativos](#generate-renditions-of-new-assets).
1. Use os perfis para [processar ativos existentes](#generate-renditions-of-existing-assets).

## Criar um perfil de processamento {#create-processing-profile}

Para gerar representações FPO, crie um **[!UICONTROL Perfil de processamento]**. Os perfis usam microsserviços de ativos nativos em nuvem para processamento. Para obter instruções, consulte [criar perfis de processamento para microsserviços de ativos](asset-microservices-configure-and-use.md).

Selecionar **[!UICONTROL Criar representação FPO]** para gerar a representação FPO. Opcionalmente, clique em **[!UICONTROL Adicionar novo]** para adicionar outras configurações de representação ao mesmo perfil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Gerar representações de novos ativos {#generate-renditions-of-new-assets}

Para gerar representações FPO de novos ativos, aplique a variável **[!UICONTROL Perfil de processamento]** para a pasta nas propriedades da pasta. Na página Propriedades de uma pasta, clique em **[!UICONTROL Processamento de ativos]** selecione a guia **[!UICONTROL Perfil FPO]** como **[!UICONTROL Perfil de processamento]** e salve as alterações. Todos os novos ativos carregados na pasta são processados usando este perfil.

![representação suplementar](assets/add-fpo-rendition.png)


## Gerar representações de ativos existentes {#generate-renditions-of-existing-assets}

Para gerar representações, selecione os ativos e siga essas etapas.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Exibir representações de FPO {#view-fpo-renditions}

Você pode verificar as renderizações de FPO geradas após a conclusão do workflow. Na interface do usuário do Experience Manager Assets, clique no ativo para abrir uma visualização grande. Abra o painel à esquerda e selecione **[!UICONTROL Representações]**. Como alternativa, use o atalho de teclado `Alt + 3` quando a visualização estiver aberta.

Clique em **[!UICONTROL Representação de FPO]** para carregar a visualização. Como opção, você pode clicar com o botão direito do mouse na representação e salvá-la em seu sistema de arquivos. Verifique se há representações disponíveis no painel esquerdo.

![rendition_list](assets/list-renditions.png)

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
