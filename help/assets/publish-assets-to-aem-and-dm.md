---
title: Publicação Rápida em  [!DNL AEM and Dynamic Media]
description: A Publicação Rápida no  [!DNL Assets view] permite que você publique ativos no [!DNL AEM and Dynamic Media] simultaneamente ou separadamente. Você pode selecionar ativos e pastas e optar por publicar em [!DNL Dynamic Media] ou [!DNL AEM].
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Publicar Assets em [!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

O [!DNL Experience Manager Assets] permite que você publique ativos rapidamente no [!DNL Experience Manager] e [!DNL Dynamic Media] usando o [!DNL Assets view]. Isso garante que você gerencie seus ativos e publique-os usando o [[!DNL Assets view] sem alternar para o [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences).

O [!DNL Experience Manager Assets view] oferece a flexibilidade para publicar ativos no [!DNL AEM] ou [!DNL Dynamic Media], ou ambos ao mesmo tempo. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos. Todas essas opções para publicar ativos são explicadas neste artigo em detalhes.

## Antes de começar {#before-you-begin}

Defina estas configurações para exibir as opções de publicação para [!DNL AEM and Dynamic Media]:

* Para exibir as opções de publicação para [!DNL Dynamic Media], defina as seguintes configurações usando o modo de exibição de Administrador:

   * [Criar uma [!DNL Dynamic Media] Configuração na nuvem](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Defina o Modo de publicação [!DNL Dynamic Media] no nível da pasta. Você também pode definir essas configurações ao criar a configuração na nuvem do [!DNL Dynamic Media]. Para substituir essas configurações no nível da pasta, consulte [Configurar Publicação Seletiva no nível da pasta em [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md).

* Para exibir as opções de publicação para [!DNL AEM], você deve configurar o ponto de extremidade de publicação [!DNL AEM] para o seu ambiente.

## Publicar o Assets durante o upload {#piblish-assets-during-upload}

Você pode publicar ativos no [!DNL AEM and Dynamic Media] enquanto carrega ativos para uma pasta. As opções de publicação exibidas dependem das configurações de modo de publicação do [!DNL Dynamic Media] da pasta para onde os ativos estão sendo carregados. O modo de publicação [!DNL Dynamic Media] pode ser definido como:

* **[!UICONTROL Na ativação]:** quando os ativos são carregados para esta pasta, você deve publicar explicitamente o ativo primeiro, antes de fornecer um link de URL/Incorporação.

* **[!UICONTROL Imediato]:** quando os ativos são carregados para esta pasta, o sistema assimila os ativos na Experience Manager e fornece instantaneamente a URL/Incorporação.
* **[!UICONTROL Publicação seletiva]:** os Assets foram publicados à sua escolha entre [!DNL Experience Manager] ou [!DNL Dynamic Media] para entrega no domínio público.

### [!UICONTROL Modo de publicação do Dynamic Media] definido como [!UICONTROL Na ativação] {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar ativos ao carregá-los em uma pasta cujo [!DNL Dynamic Media Publish Mode] esteja definido como **[!UICONTROL Na ativação]**:

1. Clique em **[!UICONTROL Adicionar Assets]** > **[!UICONTROL Procurar]** > **[!UICONTROL Procurar Arquivos]** para navegar até a pasta apropriada para carregar ativos. A seção **[!UICONTROL Opções de Publicação]** exibe o **[!UICONTROL Modo de Publicação DM]** como **[!UICONTROL Na Ativação]**.

   ![Carregar imagem na ativação](/help/assets/assets/upload-uactivation.svg)

1. Selecione **[!UICONTROL Publicar no AEM e Dynamic Media]** e clique em **[!UICONTROL Carregar]**. Os ativos são publicados em [!DNL AEM and Dynamic Media] ao mesmo tempo. Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### [!UICONTROL Modo de publicação do Dynamic Media] definido como [!UICONTROL Imediato] {#dynamic-media-publish-mode-set-to-immediate}

Para publicar ativos ao carregá-los em uma pasta cujo [!UICONTROL Modo de publicação do Dynamic Media] esteja definido como **[!UICONTROL Imediato]**:

1. Clique em **[!UICONTROL Adicionar Assets]** > **[!UICONTROL Procurar]** > **[!UICONTROL Procurar Arquivos]** para navegar até a pasta apropriada para carregar ativos. A seção **[!UICONTROL Opções de Publicação]** exibe o **[!UICONTROL Modo de Publicação DM]** como **[!UICONTROL Imediato]**.

   ![imagem de carregamento de arquivo - modo imediato](/help/assets/assets/resized-image-pdf-svg-new.svg)

   Como o [!UICONTROL Modo de publicação do Dynamic Media] é **[!UICONTROL Imediato]**, os ativos carregados são publicados automaticamente no [!DNL Dynamic Media] quando você clica em **[!UICONTROL Carregar]**.

1. Selecione **Publicar no AEM** para publicar os ativos carregados em [!DNL AEM] e clique em **[!UICONTROL Carregar]**.

   Se você selecionar **Publicar no AEM**, os ativos serão publicados em [!DNL AEM and Dynamic Media], caso contrário, serão publicados em [!DNL Dynamic Media].

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### [!UICONTROL Modo de publicação do Dynamic Media] definido como [!UICONTROL Publicação seletiva] {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar ativos durante o carregamento em uma pasta com [!UICONTROL Modo de publicação do Dynamic Media] definido como **[!UICONTROL Publicação seletiva]**:

1. Clique em **[!UICONTROL Adicionar Assets]** > **[!UICONTROL Procurar]** > **[!UICONTROL Procurar Arquivos]** para navegar até a pasta apropriada para carregar ativos. A seção **[!UICONTROL Opções de Publicação]** exibe o **[!UICONTROL Modo de Publicação DM]** como **[!UICONTROL Publicação Seletiva]**.

![modo de publicação seletiva de imagem de carregamento](/help/assets/assets/upload-selective.svg)

1. Selecione **[!UICONTROL Publicar no AEM]**, **[!UICONTROL Publicar no Dynamic Media]**, ou ambos, de acordo com seus requisitos, e clique em **Carregar**.

   Os ativos são publicados em [!DNL AEM and Dynamic Media] com base na sua seleção.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

## Publicar ativos usando a página de navegação de ativos {#publish-assets-using-asset-browse-page}

Para publicar ativos usando a página de navegação de ativos:

1. Clique em **[!UICONTROL Assets]** na seção **[!UICONTROL Assets Management]** disponível no painel esquerdo.
1. Selecione um ou mais ativos ou pastas que você precisa publicar e clique em **[!UICONTROL Publicar]**.
1. Selecione **[!UICONTROL AEM]** e clique em **[!UICONTROL Publicar]** para publicar ativos em [!DNL AEM and Dynamic Media].

   ![navegação de ativos](/help/assets/assets/browse-uactivation-immediate.svg)

   Não é possível publicar uma pasta que tenha o Modo de Publicação [!DNL Dynamic Media] definido como **[!UICONTROL Publicação Seletiva]**. Todas as outras pastas ou ativos selecionados são publicados em [!DNL AEM and Dynamic Media] depois de selecionar [!DNL AEM].

   ![navegação de ativos](/help/assets/assets/browse-selective123.svg)

## Publicar ativos usando a página de resultados da pesquisa {#publish-assets-using-search-results-page}

Para publicar ativos usando a página de resultados da pesquisa de ativos:

1. Especifique os critérios na barra de pesquisa e clique no ícone de pesquisa para exibir os resultados.
1. Selecione os ativos que você precisa publicar e clique em **[!UICONTROL Publicar].**
1. Selecione [!DNL AEM, Dynamic Media] ou ambos de acordo com seus requisitos e clique em **[!UICONTROL Publicar]**.

   ![pesquisar imagem](/help/assets/assets/search-mode.svg)

   A opção de publicar em [!DNL Dynamic Media] na página de resultados da pesquisa depende do Modo de publicação [!DNL Dynamic Media] definido na pasta em que o ativo está disponível no repositório.

   >[!NOTE]
   >
   >Se você selecionar uma pasta e clicar em **[!UICONTROL Publicar]** na página de resultados da pesquisa, [!DNL Experience Manager Assets] exibirá uma opção para publicar ativos em [!DNL AEM] e não em [!DNL Dynamic Media], independentemente das [!DNL Dynamic Media] configurações de Modo de Publicação da pasta.

## Verificar status de publicação {#check-publish-status}

Para verificar o status publicado de um ativo ou de uma pasta:

1. Clique em **[!UICONTROL Assets]** na seção **[!UICONTROL Assets Management]** disponível no painel esquerdo.
1. Alterne para a exibição em Lista usando o Alternador de exibição. Você pode exibir propriedades de ativos, como [!UICONTROL publicação do AEM], [!UICONTROL Publicação do Dynamic Media], [!UICONTROL título], [!UICONTROL tamanho], [!UICONTROL dimensões] e assim por diante.

   Se um ativo ou pasta não for publicado, o status das colunas **[!UICONTROL Publicação do AEM]** e **[!UICONTROL Publicação do Dynamic Media]** será exibido como **[!UICONTROL N/D]**.

   ![verificar status da publicação1](/help/assets/assets/check-publish-status1.png)

   Se você não conseguir exibir as colunas Publicar [!DNL AEM] e Publicar [!DNL Dynamic Media] no modo de exibição de Lista:

   1. Clique em ![configurações](/help/assets/assets/settings-icon.svg) e selecione as colunas **[!UICONTROL Publicação do AEM]** e **[!UICONTROL Publicação do Dynamic Media]** na caixa de diálogo **[!UICONTROL Colunas Configuráveis]**.
   1. Clique em **[!UICONTROL Confirmar]**. [!DNL Experience Manager Assets] adiciona as colunas selecionadas à exibição de Lista.

      ![verificar status da publicação2](/help/assets/assets/check-publish-status2.png)

Você também pode verificar o status de publicação de um ativo selecionando um ativo e clicando em **[!UICONTROL Detalhes]**. Os detalhes estão disponíveis na seção **[!UICONTROL Publicar]**, disponível no painel direito. A seção **[!UICONTROL Publicar]** lista a data em que os ativos são publicados em [!DNL Dynamic Media] e [!DNL AEM]. Se precisar exibir a hora em que os ativos são publicados, navegue até a Exibição de lista e visualize esses detalhes.

![verificar status de publicação 3](/help/assets/assets/check-publish-status3.png)

## Limitações {#limitations}

Os seguintes recursos estão fora do escopo por enquanto ao publicar ativos em [!DNL AEM and Dynamic Media]:

* Publicar ativos em [!DNL AEM and Dynamic Media] a partir de [!DNL Asset details page].
* Visualize os endpoints em que os ativos são publicados usando o assistente de Publicação rápida.
* Adicione ou exclua mais ativos no Assistente de publicação rápida.
* Uma página para exibir ativos publicados.
* Uma capacidade de copiar ou colar a URL [!DNL Dynamic Media] em um nível de ativo (se os ativos forem publicados em [!DNL Dynamic Media]).
* Capacidade de publicar referências (ativos, marcas, etc.) ao publicar em [!DNL AEM].
* Capacidade de substituir o status de sincronização [!DNL Dynamic Media] no nível da pasta.
* Capacidade de substituir o Modo de publicação [!DNL Dynamic Media] no nível da pasta
* Ainda não há suporte para Gerenciar publicação.
