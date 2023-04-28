---
title: Automação de conteúdo para integração com o Creative Cloud
description: Gerar variações de ativos usando a integração do Creative Cloud
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Gerar variações de ativos usando [!DNL Adobe Creative Cloud] integração {#content-automation}

Integra o complemento de automação de conteúdo [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service] e [!DNL Adobe Creative Cloud] As APIs para processar criativamente seus ativos em escala. [!DNL Experience Manager] O usa a nuvem [microsserviços de ativos](/help/assets/asset-microservices-overview.md) para usar o [!DNL Adobe Creative Cloud] e automatizam a criação de ativos e o manuseio de mídia.

Para editar ativos em [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], não é necessário baixar ativos do [!DNL Experience Manager Assets], edite-as e faça upload delas novamente. Você cria e configura um perfil de processamento no [!DNL Experience Manager], aplique o perfil a uma pasta e faça upload dos ativos para a pasta . Os ativos carregados são reprocessados com base nos perfis de processamento e você obtém variações desses ativos. O processamento em massa consistente e sem esforço salva esforços e aumenta a velocidade do conteúdo, também sem a necessidade de habilidades criativas ótimas. Além disso, os desenvolvedores e os parceiros podem estender os microsserviços de ativos com acesso direto a essas APIs e incluir a lógica personalizada.

Os usuários podem criar perfis de processamento para automatizar as seguintes operações criativas em seus ativos:

* **Toque automático**: Usa inteligência artificial para analisar o conteúdo da imagem e faz correções de luz e cor de forma inteligente com base nos atributos únicos da imagem.

* **Elevação automática**: Usa inteligência artificial para analisar o conteúdo da imagem e corrigir a perspectiva distorcida nas imagens. Por exemplo, para criar horizontes de nível.

   ![tom automático](/help/assets/assets/content-automation-autotone.png)

   *Figura: O tom automático e a correção automática podem ajudar a melhorar imagens distorcidas.*

* **Predefinições de Lightroom**: Aplica uma aparência definida pelo usuário a imagens para obter uma aparência consistente usando predefinições personalizadas.

   ![Predefinição de Lightroom](/help/assets/assets/content-automation-lrpresets.png)

   *Figura: Predefinição do Adobe Lightroom para melhorar a qualidade da imagem de forma consistente para muitas imagens.*

* **Recorte de imagem**: Usa inteligência artificial para criar seleção em torno de objetos salientes e remover o plano de fundo com um único comando.

   ![Remover o plano de fundo e recortar uma imagem de uma foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de imagem**: Usa inteligência artificial para criar máscara em torno de objetos salientes com um único comando.

   ![Mascarar uma imagem usando AI](/help/assets/assets/content-automation-mask.png)

* **Ações do Photoshop**: Aplica uma série de [!DNL Adobe Photoshop] tarefas em um arquivo ou lote de arquivos.

   ![Ações do Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Substituição de objeto inteligente**: A personalização em escala permite trocar imagens enquanto mantém todos os efeitos e ajustes aplicados em um arquivo PSD.

   ![Substituir objetos de maneira inteligente](/help/assets/assets/content-automation-objectreplace.png)

## Habilitar Automação de conteúdo para AEM programa as a Cloud Service {#enable-content-automation}

Para ativar o complemento de Automação de conteúdo para AEM programa as a Cloud Service usando o Cloud Manager:

1. Entre em contato com seu representante de conta para licenciar o complemento Content Automation .
1. Acesse o Cloud Manager e alterne para sua organização usando o seletor de organização.
1. Clique em **[!UICONTROL Adicionar programa]** e especifique um nome de programa.
1. Clique em **[!UICONTROL Continuar]**.
1. Expandir **[!UICONTROL Ativos]** e selecione **[!UICONTROL Automação de conteúdo]**.
1. Clique em **[!UICONTROL Criar]**.
1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se você precisar adicionar o complemento Content Automation a um programa AEM as a Cloud Service existente no Cloud Manager:

1. Clique em ... no cartão do programa.

1. Selecionar **[!UICONTROL Editar programa]** e depois selecione **[!UICONTROL Soluções e complementos]** guia .

1. Expandir **[!UICONTROL Ativos]** e selecione **[!UICONTROL Automação de conteúdo]**.
1. Clique em **[!UICONTROL Atualizar]**.
1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Use um perfil de processamento para editar seus ativos de criação em massa {#process-assets}

Para usar perfis de processamento para criar variações automaticamente, siga estas etapas:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Processando perfis]**.

1. Selecionar **[!UICONTROL Criar]** e especifique um **[!UICONTROL Nome]**.

1. Selecione o **[!UICONTROL Criativo]** , especifique a pasta de saída, selecione **[!UICONTROL Adicionar novo]** para adicionar uma configuração criativa.

1. Fornecer **[!UICONTROL Nome da representação]** (ou nome de saída), **[!UICONTROL Extensão]** (ou tipo de arquivo), selecione **[!UICONTROL Qualidade]** (ou parâmetros de saída), selecione **[!UICONTROL Inclui]** e **[!UICONTROL Exclui]** O tipo MIME lista (ou o filtro de ativo de entrada) e seleciona a operação criativa necessária.

   ![[!UICONTROL Criativo] em [!UICONTROL Perfil de processamento]](assets/creative-processing-profile.png)

1. Algumas operações exigem parâmetros extras (ativo). Forneça valores para esses parâmetros extras, se necessário.

1. Adicione mais operações criativas como parte do mesmo perfil de processamento ou Salve o perfil.

1. Aplique o perfil de processamento a uma pasta. Em uma pasta **[!UICONTROL Propriedades]** página, selecione **[!UICONTROL Processamento de ativos]** e selecione o perfil de processamento a ser aplicado.

Depois de aplicar o perfil de processamento a uma pasta DAM, todos os ativos carregados ou atualizados nessa pasta executam as operações definidas além do processamento padrão. As subpastas herdam os mesmos perfis que foram aplicados nas pastas pai. Os usuários podem substituir essa herança.

Para processar os ativos existentes, selecione os ativos, selecione **[!UICONTROL Reprocessar]** e selecione o perfil de processamento necessário.

## Dicas e limitações {#limitations-best-practices}

* [!DNL Experience Manager] limita o processamento de ativos a 300 solicitações por minuto e por ambiente e 700 solicitações por minuto por organização.
* O tamanho do arquivo é limitado a 4 GB para [!DNL Adobe Photoshop] Operações de API e 1 GB para [!DNL Adobe Lightroom] operações.

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

>[!MORELIKETHIS]
>
>* [Configurar e usar microsserviços de ativos por meio de perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).
>* [ [!DNL Experience Manager] Integrar com a [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Assimilação e processamento de ativos com microsserviços de ativos: Uma visão geral](/help/assets/asset-microservices-overview.md).

