---
title: Automação de conteúdo para integração com o Creative Cloud
description: Gerar variações de ativos usando a integração do Creative Cloud
contentOwner: AG
feature: Upload,Processamento de Ativos,Publicação,Microserviços do Asset compute,Fluxo de Trabalho
role: Business Practitioner,Administrator
source-git-commit: ffca94ef8d93cf95011d7e3128c49929f69cdc28
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# Gerar variações de ativos usando a integração [!DNL Adobe Creative Cloud] {#content-automation}

O complemento de automação de conteúdo integra os ativos Experience Manager como um Cloud Service e as APIs do Adobe Creative Cloud para processar seus ativos em escala de forma criativa. O Experience Manager usa os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) baseados em nuvem para aproveitar os recursos do Adobe Creative Cloud e automatizar a criação de ativos e o manuseio de mídia.

Para editar ativos em [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], não é necessário baixar de, editar e fazer upload para [!DNL Experience Manager Assets]. Basta criar e configurar um perfil de processamento, aplicar o perfil a uma pasta e fazer upload dos ativos para a pasta. Os ativos carregados na pasta são processados para criar diferentes variações desse ativo. O processamento e a edição em massa, consistente e sem esforços, de ativos economizaram esforços manuais e aumentaram a velocidade do conteúdo. Além disso, desenvolvedores e parceiros podem estender os microsserviços de ativos com acesso direto a essas APIs e incluir lógica personalizada.

Os usuários podem criar perfis de processamento para automatizar as seguintes operações criativas em seus ativos:

* **Toque** automático: Utiliza inteligência artificial para analisar o conteúdo da imagem e faz correções de luz e cor de forma inteligente com base nos atributos exclusivos da imagem.
* **Direita** automaticamente: Utiliza inteligência artificial para analisar o conteúdo da imagem e corrigir a perspectiva distorcida nas imagens. Por exemplo, para criar horizontes de nível.
* **Predefinições** do Lightroom: Aplica uma aparência definida pelo usuário a imagens para obter uma aparência consistente usando predefinições personalizadas.
* **Recorte** da imagem: Utiliza inteligência artificial para criar seleção em torno de objetos salientes e remover o plano de fundo com um único comando.
* **Máscara** de imagem: Utiliza inteligência artificial para criar máscara em torno de objetos salientes com um único comando.
* **Ações** do Photoshop: Aplica uma série de tarefas (no Photoshop) a um arquivo ou lote de arquivos.
* **Substituição** de objeto inteligente: Executa a personalização em escala permitindo trocar imagens enquanto mantém todos os efeitos e ajustes aplicados em um arquivo PSD.

## Usar um perfil de processamento para processar ativos {#process-assets}

Para usar perfis de processamento para criar variações automaticamente, siga estas etapas:

1. Entre em contato com o [Adobe Customer Care](https://experienceleague.adobe.com/#support) para receber a licença.

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]**.

1. Selecione **[!UICONTROL Criar]** e especifique um **[!UICONTROL Nome]**.

1. Selecione a guia **[!UICONTROL Creative]**, especifique a pasta de saída, selecione **[!UICONTROL Adicionar novo]** para adicionar configurações criativas.

1. Forneça **[!UICONTROL Nome da representação]** (ou nome da saída), **[!UICONTROL Extensão]** (ou tipo de arquivo), selecione **[!UICONTROL Qualidade]** (ou parâmetros de saída), selecione Inclui e Exclui listas do tipo MIME (ou filtro de ativo de entrada) e selecione a operação criativa necessária.

1. Algumas operações exigem um parâmetro adicional (ativo). Forneça valores para esses parâmetros adicionais, se necessário.

1. Adicione mais operações criativas como parte do mesmo perfil de processamento ou Salve o perfil.

1. Aplique o perfil de processamento a uma pasta. Na página **[!UICONTROL Properties]** de uma pasta, selecione **[!UICONTROL Asset Processing]** e selecione o perfil de processamento a ser aplicado.

Depois que o perfil de processamento é aplicado a uma pasta DAM, todos os ativos carregados ou atualizados nessa pasta executam as operações definidas, além do processamento padrão. As subpastas herdam os mesmos perfis aplicados nas pastas pai. Os usuários podem substituir essa herança.

Para processar os ativos existentes, selecione os ativos, selecione a opção **[!UICONTROL Reprocessar]** e selecione o perfil de processamento necessário.

## Dicas e limitações {#limitations-best-practices}

* [!DNL Experience Manager] limita o processamento de ativos a 300 solicitações por minuto e por ambiente e 700 solicitações por minuto por organização.
* O tamanho do arquivo é limitado a 4 GB para operações de API [!DNL Adobe Photoshop] e 1 GB para operações [!DNL Adobe Lightroom].

>[!MORELIKETHIS]
>
>* [Configure e use microsserviços de ativos por meio de perfis](/help/assets/asset-microservices-configure-and-use.md) de processamento.
>* [ [!DNL Experience Manager] Integrar com [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).

