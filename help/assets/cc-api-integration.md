---
title: Automação de conteúdo para integração com o Creative Cloud
description: Gerar variações de ativos usando a integração Creative Cloud
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 4%

---

# Gerar variações de ativos usando [!DNL Adobe Creative Cloud] integração {#content-automation}

O complemento de automação de conteúdo é integrado [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] e [!DNL Adobe Creative Cloud] APIs para processar criativamente seus ativos em escala. [!DNL Experience Manager] usa baseados em nuvem [microsserviços de ativos](/help/assets/asset-microservices-overview.md) para usar o [!DNL Adobe Creative Cloud] recursos e automatizar a criação de ativos e o manuseio de mídia.

Para editar ativos no [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], não é necessário baixar os ativos do [!DNL Experience Manager Assets], edite e faça upload deles novamente. Crie e configure um perfil de processamento no [!DNL Experience Manager], aplique o perfil a uma pasta e faça upload dos ativos para a pasta. Os ativos carregados são reprocessados com base nos perfis de processamento e você obtém variações desses ativos. O processamento em massa consistente e sem esforços economiza esforços manuais e aumenta a velocidade do conteúdo, também sem a necessidade de habilidades criativas excepcionais. Além disso, os desenvolvedores e os parceiros podem estender os microsserviços de ativos com acesso direto a essas APIs e incluir lógica personalizada.

Os usuários podem criar perfis de processamento para automatizar as seguintes operações criativas em seus ativos:

* **Tom automático**: usa inteligência artificial para analisar o conteúdo da imagem e fazer correções de luz e cores de forma inteligente com base nos atributos exclusivos da imagem.

* **Direita automática**: usa inteligência artificial para analisar o conteúdo da imagem e corrigir a perspectiva inclinada nas imagens. Por exemplo, para criar horizontes de nível.

  ![tom automático](/help/assets/assets/content-automation-autotone.png)

  *Figura: o tom e o direcionamento automáticos podem ajudar a melhorar imagens distorcidas.*

* **Predefinições do Lightroom**: aplica uma aparência definida pelo usuário às imagens para obter uma aparência consistente usando predefinições personalizadas.

  ![Predefinição do Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Figura: predefinição do Adobe Lightroom para melhorar a qualidade da imagem de forma consistente para muitas imagens.*

* **Recorte de imagem**: usa inteligência artificial para criar seleção em torno de objetos principais e remover o plano de fundo com um único comando.

  ![Remover plano de fundo e recortar uma imagem de uma foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de imagem**: usa inteligência artificial para criar máscaras em torno de objetos principais com um único comando.

  ![Mascaramento de uma imagem usando IA](/help/assets/assets/content-automation-mask.png)

* **Ações do Photoshop**: aplica uma série de [!DNL Adobe Photoshop] tarefas a um arquivo ou lote de arquivos.

  ![Ações do Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Substituição de objeto inteligente**: faz a personalização em escala, permitindo que você troque imagens e, ao mesmo tempo, retenha todos os efeitos e ajustes aplicados em um arquivo PSD.

  ![Substituir objetos com inteligência](/help/assets/assets/content-automation-objectreplace.png)

## Habilitar a automação de conteúdo para o programa as a Cloud Service AEM {#enable-content-automation}

Para ativar o complemento de Automatização de Conteúdo para o programa AEM as a Cloud Service usando o Cloud Manager:

1. Entre em contato com seu representante de conta para obter licença do complemento de Automatização de conteúdo.
1. Acesse o Cloud Manager e alterne para sua organização usando o seletor de organização.
1. Clique em **[!UICONTROL Adicionar programa]** e especifique um nome de programa.
1. Clique em **[!UICONTROL Continuar]**.
1. Expandir **[!UICONTROL Assets]** e selecione **[!UICONTROL Automação de conteúdo]**.
1. Clique em **[!UICONTROL Criar]**.
1. Executar o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se você precisar adicionar um complemento de Automação de conteúdo a um programa as a Cloud Service AEM existente no Cloud Manager:

1. Clique em ... no cartão do programa.

1. Selecionar **[!UICONTROL Editar programa]** e selecione **[!UICONTROL Soluções e complementos]** guia.

1. Expandir **[!UICONTROL Assets]** e selecione **[!UICONTROL Automação de conteúdo]**.
1. Clique em **[!UICONTROL Atualizar]**.
1. Executar o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Use um perfil de processamento para editar seus ativos criativos em massa {#process-assets}

Para usar perfis de processamento para criar variações automaticamente, siga estas etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Processamento de perfis]**.

1. Selecionar **[!UICONTROL Criar]** e especifique um **[!UICONTROL Nome]**.

1. Selecione o **[!UICONTROL Creative]** especifique a pasta de saída e selecione **[!UICONTROL Adicionar novo]** para adicionar uma configuração criativa.

1. Fornecer **[!UICONTROL Nome da representação]** (ou nome de saída), **[!UICONTROL Extensão]** (ou tipo de arquivo), selecione **[!UICONTROL Qualidade]** (ou parâmetros de saída), selecione **[!UICONTROL Inclui]** e **[!UICONTROL Exclui]** Listas de tipo MIME (ou filtro de ativo de entrada) e selecione a operação de criação necessária.

   ![[!UICONTROL Creative] guia em [!UICONTROL Processando perfil]](assets/creative-processing-profile.png)

1. Algumas operações exigem parâmetros extras (ativo). Forneça valores para esses parâmetros adicionais, se necessário.

1. Adicione mais operações criativas como parte do mesmo perfil de processamento ou Salve o perfil.

1. Aplicar o perfil de processamento a uma pasta. Em uma pasta **[!UICONTROL Propriedades]** selecione **[!UICONTROL Processamento de ativos]** e selecione o perfil de processamento a ser aplicado.

Depois de aplicar o perfil de processamento a uma pasta do DAM, todos os ativos carregados ou atualizados nessa pasta executam as operações definidas, além do processamento padrão. As subpastas herdam os mesmos perfis que os aplicados às pastas principais. Os usuários podem substituir essa herança.

Para processar os ativos existentes, selecione os ativos, selecione **[!UICONTROL Reprocessar]** e selecione o perfil de processamento necessário.

## Dicas e limitações {#limitations-best-practices}

* [!DNL Experience Manager] o limita o processamento de ativos a 300 solicitações por minuto por ambiente e 700 solicitações por minuto por organização.
* O tamanho do arquivo é limitado a 4 GB para [!DNL Adobe Photoshop] operações de API e 1 GB para [!DNL Adobe Lightroom] operações.

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
* [Publicar ativos no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Configurar e usar microsserviços de ativos por meio de perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrar [!DNL Experience Manager] com [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Assimilação e processamento de ativos com microsserviços de ativos: uma visão geral](/help/assets/asset-microservices-overview.md).
