---
title: Publish rápido para AEM e Dynamic Media
description: O Quick Publish na visualização do Assets permite publicar ativos no AEM e na mídia dinâmica de forma simultânea ou separada. Você pode selecionar ativos e pastas e optar por publicar no Dynamic Media ou AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: cb8a5e5e8ecec2884c061d60f2519ba3e0208f81
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Publish Assets para AEM e Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

O Experience Manager Assets permite publicar rapidamente os ativos no Experience Manager e no Dynamic Media usando a visualização do Assets. Isso garante que você gerencie seus ativos e publique-os usando a [exibição do Assets sem alternar para a exibição do Administrador](/help/assets/overview.md##persona-based-experiences).

A visualização do Experience Manager Assets oferece a flexibilidade de publicar ativos no AEM, no Dynamic Media ou em ambos ao mesmo tempo. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos. Todas essas opções para publicar ativos são explicadas em detalhes neste artigo.

## Antes de começar {#before-you-begin}

Defina essas configurações para exibir as opções de publicação para AEM e Dynamic Media:

* Para exibir as opções de publicação do Dynamic Media, defina as seguintes configurações usando a Exibição de administração:

   * [Criar uma configuração de nuvem do Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Defina o modo Dynamic Media Publish no nível da pasta. Você também pode definir essas configurações ao criar a configuração da nuvem do Dynamic Media. Para substituir essas configurações no nível da pasta, consulte [Configurar Publish Seletivo no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Para exibir as opções de publicação do AEM, você deve configurar o endpoint de publicação do AEM para o seu ambiente.

## Publish Assets durante o upload {#piblish-assets-during-upload}

Você pode publicar ativos no AEM e no Dynamic Media enquanto faz upload de ativos para uma pasta. As opções de publicação exibidas dependem do modo de publicação do Dynamic Media definido na pasta para a qual os ativos estão sendo carregados. O modo de publicação do Dynamic Media pode ser definido como:

* **Na ativação:** quando os ativos forem carregados para esta pasta, você deverá publicar explicitamente o ativo primeiro, antes de fornecer um link de URL/Incorporação.

* **Imediato:** quando os ativos são carregados para esta pasta, o sistema assimila os ativos no Experience Manager e fornece a URL/Incorporar instantaneamente.
* **Publish seletiva:** os Assets são publicados à sua escolha entre Experience Manager ou Dynamic Media para entrega no domínio público.

### Modo Dynamic Media Publish definido como Na ativação {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar ativos durante o carregamento em uma pasta com o Modo Dynamic Media Publish definido como **Na ativação**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção **Opções do Publish** exibe o **Modo DM Publish** como **Na Ativação**.
   ![Carregar imagem na ativação](/help/assets/assets/upload-uactivation.svg)
2. Selecione **Publish para AEM e Dynamic Media** e clique em **Carregar**. Os ativos são publicados no AEM e no Dynamic Media ao mesmo tempo. Para ver o status de publicação atualizado desses ativos, consulte [Verificar status do Publish](#check-publish-status).

### Modo Publish do Dynamic Media definido como Imediato {#dynamic-media-publish-mode-set-to-immediate}

Para publicar ativos durante o carregamento em uma pasta com o Modo Dynamic Media Publish definido como **Imediato**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção Opções do Publish exibe o **Modo DM Publish** como **Imediato**.
   ![imagem de carregamento de arquivo - modo imediato](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Como o Modo Publish do Dynamic Media é **Imediato**, os ativos carregados são publicados automaticamente no Dynamic Media quando você clica em **Carregar**.

2. Selecione Publish to **AEM para publicar** os ativos carregados no AEM e clique em Fazer upload.

   Se você selecionar **Publish para AEM**, os ativos serão publicados no AEM e no Dynamic Media, caso contrário, serão publicados no Dynamic Media.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status do Publish](#check-publish-status).

### Modo Publish do Dynamic Media definido como Publish seletiva {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar ativos durante o carregamento em uma pasta com o Modo Dynamic Media Publish definido como **Publish Seletiva**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção Opções do Publish exibe o **Modo DM Publish** como **Publish Seletiva**.
   ![modo de publicação seletiva de imagem de carregamento](/help/assets/assets/upload-selective.svg)

2. Selecione **Publish para AEM**, **Publish para Dynamic Media** ou ambos de acordo com suas necessidades e clique em **Carregar**.

   Os ativos são publicados no AEM e no Dynamic Media com base em sua seleção.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status do Publish](#check-publish-status).

## Ativos Publish usando a página de navegação de ativos {#publish-assets-using-asset-browse-page}

Para publicar ativos usando a página de navegação de ativos:

1. Clique em **Assets** na seção **Assets Management** disponível no painel esquerdo.
2. Selecione o(s) ativo(s) ou pasta(s) que você precisa publicar e clique em **Publish**.
3. Selecione **AEM** e clique em **Publish** para publicar ativos no AEM e no Dynamic Media.
   ![navegação de ativos](/help/assets/assets/browse-uactivation-immediate.svg)
Não é possível publicar uma pasta que tenha o Modo Publish do Dynamic Media definido como **Publicação seletiva.** Todas as outras pastas ou ativos selecionados são publicados no AEM e no Dynamic Media após selecionar AEM.
   ![navegação de ativos](/help/assets/assets/browse-selective123.svg)

## Página de resultados da pesquisa de ativos do Publish {#publish-assets-using-search-results-page}

Para publicar ativos usando a página de resultados da pesquisa de ativos:

1. Especifique os critérios na barra de Pesquisa e clique no ícone Pesquisar para exibir os resultados.
2. Selecione os ativos que você precisa publicar e clique em **Publish.**
3. Selecione AEM, Dynamic Media ou ambos conforme suas necessidades e clique em **Publish.**
   ![pesquisar imagem](/help/assets/assets/search-mode.svg)
A opção de publicar no Dynamic Media na página de resultados da pesquisa depende do Modo Publish do Dynamic Media definido na pasta em que o ativo está disponível no repositório.

   >[!NOTE]
   >
   >Se você selecionar uma pasta e clicar em **Publish** na página de resultados da pesquisa, o Experience Manager Assets exibirá uma opção para publicar ativos no AEM e não no Dynamic Media, independentemente das configurações de Modo Dynamic Media Publish da pasta.

## Verificar status do Publish {#check-publish-status}

Para verificar o status de publicação de um ativo ou de uma pasta:

1. Clique em **[!UICONTROL Assets]** na seção **[!UICONTROL Assets Management]** disponível no painel esquerdo.
2. Alterne para a Exibição de lista usando o Alternador de exibição. É possível visualizar as propriedades do ativo, como AEM Publish, Dynamic Media Publish, título, tamanho, dimensões e assim por diante.\
   Se um ativo ou pasta não for publicado, o status das colunas **AEM Publish** e **Dynamic Media Publish** será exibido como **N/D.**
   ![verificar status da publicação1](/help/assets/assets/check-publish-status1.png)
Se não conseguir exibir as colunas do Publish do AEM e do Publish do Dynamic Media na exibição em Lista:
   1. Clique em ![configurações](/help/assets/assets/settings-icon.svg) e selecione as colunas **AEM Publish** e **Dynamic Media Publish** da caixa de diálogo **Colunas Configuráveis**.
   2. Clique em **Confirmar.** O Experience Manager Assets adiciona as colunas selecionadas ao modo de exibição de Lista.

      ![verificar status da publicação2](/help/assets/assets/check-publish-status2.png)

Você também pode verificar o status de publicação de um ativo selecionando um ativo e clicando em **Detalhes.** Os detalhes estão disponíveis na seção **Publish**, disponível no painel direito. A seção **Publish** lista a data em que os ativos são publicados no Dynamic Media e no AEM. Se precisar exibir a hora em que os ativos são publicados, navegue até a Exibição de lista e visualize esses detalhes.

![verificar status de publicação 3](/help/assets/assets/check-publish-status3.png)

## Limitações {#limitations}

Por enquanto, os seguintes recursos estão fora do escopo durante a publicação de ativos no AEM e no Dynamic Media:

* Ativos do Publish para AEM e Dynamic Media na página Detalhes do ativo.
* Visualize os endpoints em que os ativos estão sendo publicados usando o assistente do Quick Publish.
* Adicionar ou excluir mais ativos no assistente do Quick Publish.
* Uma página para exibir ativos publicados.
* Uma capacidade de copiar ou colar o URL do Dynamic Media em um nível de ativo (se os ativos forem publicados no Dynamic Media).
* Capacidade de publicar referências (ativos, tags e assim por diante) ao publicar no AEM.
* Capacidade de substituir o status de sincronização do Dynamic Media no nível da pasta.
* Capacidade de substituir o modo Dynamic Media Publish no nível da pasta
* Ainda não há suporte para Gerenciar publicação.
