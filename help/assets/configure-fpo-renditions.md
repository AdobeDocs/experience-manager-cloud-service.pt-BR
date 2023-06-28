---
title: Gerar para representações somente de posicionamento para o Adobe InDesign
description: Gerar representações FPO de ativos novos e existentes usando o fluxo de trabalho do Experience Manager Assets e o ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 7%

---

# Gerar para representações somente de posicionamento para o Adobe InDesign {#fpo-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Ao colocar ativos de grande porte do Experience Manager em documentos do Adobe InDesign, um profissional criativo deve aguardar um tempo considerável depois que eles [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário é impedido de usar o InDesign. Isso interrompe o fluxo de criação e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos do InDesign para começar. Quando a saída final é necessária, digamos para workflows de impressão e publicação, os ativos originais e de resolução completa substituem a representação temporária em segundo plano. Essa atualização assíncrona em segundo plano acelera o processo de design para melhorar a produtividade e não dificulta o processo criativo.

Os ativos fornecem representações usadas somente para posicionamento (FPO). Essas representações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção. Se uma representação FPO não estiver disponível para um ativo, a Adobe InDesign usará o ativo original. Esse mecanismo de fallback garante que o workflow criativo continue sem interrupções.

O Experience Manager as a Cloud Service oferece recursos de processamento de ativos nativos em nuvem para gerar as representações FPO. Use os microsserviços de ativos para geração de representação. Você pode configurar a geração de representação de ativos carregados recentemente e dos ativos que existem no Experience Manager.

Veja a seguir as etapas para gerar representações FPO:

1. [Criar um perfil de processamento](#create-processing-profile).

1. Configurar o Experience Manager para usar este perfil [processar novos ativos](#generate-renditions-of-new-assets).
1. Use os perfis para [processar ativos existentes](#generate-renditions-of-existing-assets).

## Criar um perfil de processamento {#create-processing-profile}

Para gerar representações FPO, crie uma **[!UICONTROL Processando perfil]**. Os perfis usam microsserviços de ativos nativos em nuvem para processamento. Para obter instruções, consulte [criar perfis de processamento para microsserviços de ativos](asset-microservices-configure-and-use.md).

Selecionar **[!UICONTROL Criar representação FPO]** para gerar a representação FPO. Opcionalmente, clique em **[!UICONTROL Adicionar novo]** para adicionar outras configurações de representação ao mesmo perfil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Gerar representações de novos ativos {#generate-renditions-of-new-assets}

Para gerar representações FPO de novos ativos, aplique o **[!UICONTROL Processando perfil]** à pasta nas propriedades da pasta. Na página Propriedades de uma pasta, clique em **[!UICONTROL Processamento de ativos]** , selecione a **[!UICONTROL Perfil FPO]** as a **[!UICONTROL Processando perfil]** e salve as alterações. Todos os novos ativos carregados na pasta são processados usando este perfil.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Gerar representações de ativos existentes {#generate-renditions-of-existing-assets}

Para gerar representações, selecione os ativos e siga essas etapas.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Exibir representações FPO {#view-fpo-renditions}

Você poderá verificar as representações FPO geradas após a conclusão do fluxo de trabalho. Na interface do usuário do Experience Manager Assets, clique no ativo para abrir uma visualização grande. Abra o painel esquerdo e selecione **[!UICONTROL Representações]**. Como alternativa, use o atalho de teclado `Alt + 3` quando a visualização está aberta.

Clique em **[!UICONTROL Representação FPO]** para carregar sua visualização. Como opção, você pode clicar com o botão direito do mouse na representação e salvá-la em seu sistema de arquivos. Verifique se há representações disponíveis no painel esquerdo.

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
