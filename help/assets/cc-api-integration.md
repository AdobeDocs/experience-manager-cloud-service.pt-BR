---
title: Automação de conteúdo para integração com o Creative Cloud
description: Gerar variações de ativos usando a integração do Creative Cloud
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 4%

---

# Gerar variações de ativos usando a integração do [!DNL Adobe Creative Cloud] {#content-automation}

O complemento de automação de conteúdo integra o [!DNL Adobe Experience Manager Assets] como APIs do [!DNL Cloud Service] e do [!DNL Adobe Creative Cloud] para processar seus ativos de forma criativa e em escala. O [!DNL Experience Manager] usa os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) baseados na nuvem para usar os recursos do [!DNL Adobe Creative Cloud] e automatizar a criação de ativos e o manuseio de mídia.

Para editar ativos em [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], não é necessário baixar ativos de [!DNL Experience Manager Assets], editá-los e carregá-los novamente. Você cria e configura um perfil de processamento no [!DNL Experience Manager], aplica o perfil a uma pasta e carrega os ativos na pasta. Os ativos carregados são reprocessados com base nos perfis de processamento e você obtém variações desses ativos. O processamento em massa consistente e sem esforços economiza esforços manuais e aumenta a velocidade do conteúdo, também sem a necessidade de habilidades criativas excepcionais. Além disso, os desenvolvedores e os parceiros podem estender os microsserviços de ativos com acesso direto a essas APIs e incluir lógica personalizada.

Os usuários podem criar perfis de processamento para automatizar as seguintes operações criativas em seus ativos:

* **AutoTom**: usa a inteligência artificial para analisar o conteúdo da imagem e, de forma inteligente, faz correções de luz e cores com base nos atributos exclusivos da imagem.

* **Vertical automática**: usa a inteligência artificial para analisar o conteúdo da imagem e corrigir a perspectiva inclinada em imagens. Por exemplo, para criar horizontes de nível.

  ![tom automático](/help/assets/assets/content-automation-autotone.png)

  *Figura: o ajuste e o ajuste automáticos podem ajudar a melhorar imagens distorcidas.*

* **Predefinições do Lightroom**: aplica uma aparência definida pelo usuário a imagens para obter uma aparência consistente usando predefinições personalizadas.

  ![Predefinição do Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Figura: predefinição do Adobe Lightroom para melhorar a qualidade da imagem de forma consistente para muitas imagens.*

* **Recorte de imagem**: usa a inteligência artificial para criar seleção em torno de objetos principais e remover o plano de fundo com um único comando.

  ![Remover plano de fundo e recortar uma imagem de uma foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de Imagem**: usa inteligência artificial para criar máscaras em torno de objetos importantes com um único comando.

  ![Mascarar uma imagem usando IA](/help/assets/assets/content-automation-mask.png)

* **Ações do Photoshop**: aplica uma série de tarefas [!DNL Adobe Photoshop] a um arquivo ou lote de arquivos.

  ![Ações do Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Substituição de Objeto Inteligente**: faz personalização em escala permitindo que você troque imagens enquanto mantém todos os efeitos e ajustes aplicados em um arquivo PSD.

  ![Substituir objetos com inteligência](/help/assets/assets/content-automation-objectreplace.png)

## Habilitar a automação de conteúdo para o programa AEM as a Cloud Service {#enable-content-automation}

Para ativar o complemento de Automatização de Conteúdo para o programa AEM as a Cloud Service usando o Cloud Manager:

1. Entre em contato com seu representante de conta para obter licença do complemento de Automatização de conteúdo.
1. Acesse o Cloud Manager e alterne para sua organização usando o seletor de organização.
1. Clique em **[!UICONTROL Adicionar programa]** e especifique um nome de programa.
1. Clique em **[!UICONTROL Continuar]**.
1. Expanda **[!UICONTROL Assets]** e selecione **[!UICONTROL Automação de Conteúdo]**.
1. Clique em **[!UICONTROL Criar]**.
1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se você precisar adicionar um complemento de Automação de conteúdo a um programa existente do AEM as a Cloud Service no Cloud Manager:

1. Clique em ... no cartão do programa.

1. Selecione **[!UICONTROL Editar programa]** e depois selecione a guia **[!UICONTROL Soluções e complementos]**.

1. Expanda **[!UICONTROL Assets]** e selecione **[!UICONTROL Automação de Conteúdo]**.
1. Clique em **[!UICONTROL Atualizar]**.
1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Use um perfil de processamento para editar seus ativos criativos em massa {#process-assets}

Para usar perfis de processamento para criar variações automaticamente, siga estas etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Processando Perfis]**.

1. Selecione **[!UICONTROL Criar]** e especifique um **[!UICONTROL Nome]**.

1. Selecione a guia **[!UICONTROL Creative]**, especifique a pasta de saída e selecione **[!UICONTROL Adicionar novo]** para adicionar uma configuração criativa.

1. Forneça o **[!UICONTROL Nome da Representação]** (ou o nome de saída), a **[!UICONTROL Extensão]** (ou o tipo de arquivo), selecione a **[!UICONTROL Qualidade]** (ou os parâmetros de saída), selecione as listas de tipos MIME **[!UICONTROL Inclusões]** e **[!UICONTROL Exclusões]** (ou o filtro de ativos de entrada) e selecione a operação de criação necessária.

   Guia ![[!UICONTROL Creative] em [!UICONTROL Processando Perfil]](assets/creative-processing-profile.png)

1. Algumas operações exigem parâmetros extras (ativo). Forneça valores para esses parâmetros adicionais, se necessário.

1. Adicione mais operações criativas como parte do mesmo perfil de processamento ou Salve o perfil.

1. Aplicar o perfil de processamento a uma pasta. Na página **[!UICONTROL Propriedades]** de uma pasta, selecione **[!UICONTROL Processamento de ativos]** e selecione o perfil de processamento a ser aplicado.

Depois de aplicar o perfil de processamento a uma pasta do DAM, todos os ativos carregados ou atualizados nessa pasta executam as operações definidas, além do processamento padrão. As subpastas herdam os mesmos perfis que os aplicados às pastas principais. Os usuários podem substituir essa herança.

Para processar os ativos existentes, selecione os ativos, selecione a opção **[!UICONTROL Reprocessar]** e selecione o perfil de processamento necessário.

## Dicas e limitações {#limitations-best-practices}

* [!DNL Experience Manager] limita o processamento de ativos a 300 solicitações por minuto por ambiente e 700 solicitações por minuto por organização.
* O tamanho do arquivo é limitado a 4 GB para operações de API [!DNL Adobe Photoshop] e 1 GB para operações [!DNL Adobe Lightroom].
* As representações PDF de documentos do Microsoft Office (&quot;.docx&quot;, &quot;.doc&quot;, &quot;.ppt&quot;, &quot;.pptx&quot;, &quot;.xls&quot;, &quot;.xlsx&quot;) estão limitadas a arquivos de 100 MB ou menos.
* A transcodificação de vídeo é limitada a arquivos de entrada de 15 GB ou menos.

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
>* [Configurar e usar microsserviços de ativos por meio de perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrar [!DNL Experience Manager] a [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Assimilação e processamento de ativos com microsserviços de ativos: uma visão geral](/help/assets/asset-microservices-overview.md).
