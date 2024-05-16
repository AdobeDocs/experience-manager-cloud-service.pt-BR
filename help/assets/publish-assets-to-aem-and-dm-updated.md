---
title: Publicação rápida no AEM e no Dynamic Media
description: A Publicação rápida na exibição de Ativos permite publicar ativos no AEM e no Dynamic Media, de forma simultânea ou separada. Você pode selecionar ativos e pastas e optar por publicar no Dynamic Media ou AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: cb8a5e5e8ecec2884c061d60f2519ba3e0208f81
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Publicar ativos no AEM e no Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

O Experience Manager Assets permite publicar rapidamente ativos no Experience Manager e no Dynamic Media usando a visualização Ativos. Isso garante que você gerencie seus ativos e os publique usando [Exibição de ativos sem alternar para a exibição de Administrador](/help/assets/overview.md##persona-based-experiences).

A visualização do Experience Manager Assets oferece a flexibilidade de publicar ativos no AEM, no Dynamic Media ou em ambos ao mesmo tempo. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos. Todas essas opções para publicar ativos são explicadas em detalhes neste artigo.

## Antes de começar {#before-you-begin}

Defina essas configurações para exibir as opções de publicação para AEM e Dynamic Media:

* Para exibir as opções de publicação do Dynamic Media, defina as seguintes configurações usando a Exibição de administração:

   * [Criar uma configuração de nuvem do Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Defina o modo de Publicação do Dynamic Media no nível da pasta. Você também pode definir essas configurações ao criar a configuração da nuvem do Dynamic Media. Para substituir essas configurações no nível da pasta, consulte [Configurar publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Para exibir as opções de publicação do AEM, você deve configurar o endpoint de publicação do AEM para o seu ambiente.

## Publicar ativos durante o upload {#piblish-assets-during-upload}

Você pode publicar ativos no AEM e no Dynamic Media enquanto faz upload de ativos para uma pasta. As opções de publicação exibidas dependem do modo de publicação do Dynamic Media definido na pasta para a qual os ativos estão sendo carregados. O modo de publicação do Dynamic Media pode ser definido como:

* **Na ativação:** Quando os ativos são carregados para essa pasta, você deve publicar explicitamente o ativo primeiro, antes que um link de URL/Incorporação seja fornecido.

* **Imediato:** Quando os ativos são carregados para essa pasta, o sistema assimila os ativos no Experience Manager e fornece instantaneamente o URL/Incorporar.
* **Publicação seletiva:** Os ativos são publicados à sua escolha de Experience Manager ou no Dynamic Media para entrega no domínio público.

### Modo de publicação do Dynamic Media definido como Na ativação {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar ativos durante o upload em uma pasta com o Modo de publicação do Dynamic Media definido como **Na ativação**:

1. Clique em **Adicionar ativos** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para fazer upload de ativos. A variável **Opções de publicação** exibe a variável **Modo de publicação do DM** as **Na ativação**.
   ![Carregar imagem na ativação](/help/assets/assets/upload-uactivation.svg)
2. Selecionar **Publicar no AEM e no Dynamic Media** e clique em **Carregar**. Os ativos são publicados no AEM e no Dynamic Media ao mesmo tempo. Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### Modo de publicação do Dynamic Media definido como Imediato {#dynamic-media-publish-mode-set-to-immediate}

Para publicar ativos durante o upload em uma pasta com o Modo de publicação do Dynamic Media definido como **Imediato**:

1. Clique em **Adicionar ativos** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para fazer upload de ativos. A seção Opções de publicação exibe a **Modo de publicação do DM** as **Imediato**.
   ![imagem de upload de arquivo - modo imediato](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Como o Modo de publicação do Dynamic Media é **Imediato**, os ativos carregados são publicados automaticamente no Dynamic Media ao clicar em **Carregar**.

2. Selecione Publicar em **AEM para publicar** Adicione os ativos carregados ao AEM e clique em Fazer upload.

   Se você selecionar **Publicar no AEM**, os ativos serão publicados no AEM e no Dynamic Media, ou serão publicados no Dynamic Media.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### Modo de publicação do Dynamic Media definido como Publicação seletiva {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar ativos durante o upload em uma pasta com o Modo de publicação do Dynamic Media definido como **Publicação seletiva**:

1. Clique em **Adicionar ativos** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para fazer upload de ativos. A seção Opções de publicação exibe a **Modo de publicação do DM** as **Publicação seletiva**.
   ![fazer upload do modo de publicação seletiva de imagem](/help/assets/assets/upload-selective.svg)

2. Selecionar **Publicar no AEM**, **Publicar no Dynamic Media**, ou ambos, de acordo com suas necessidades, e clique em **Carregar**.

   Os ativos são publicados no AEM e no Dynamic Media com base em sua seleção.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

## Publicar ativos usando a página de navegação de ativos {#publish-assets-using-asset-browse-page}

Para publicar ativos usando a página de navegação de ativos:

1. Clique em **Assets** no **Gerenciamento de ativos** seção disponível no painel esquerdo.
2. Selecione o(s) ativo(s) ou pasta(s) que você precisa publicar e clique em **Publish**.
3. Selecionar **AEM** e clique em **Publish** para publicar ativos no AEM e no Dynamic Media.
   ![navegação de ativos](/help/assets/assets/browse-uactivation-immediate.svg)
Não é possível publicar uma pasta que tenha o Modo de publicação do Dynamic Media definido como **Publicação seletiva.** Todas as outras pastas ou ativos selecionados são publicados no AEM e no Dynamic Media após selecionar AEM.
   ![navegação de ativos](/help/assets/assets/browse-selective123.svg)

## Publicar ativos usando a página de resultados da pesquisa {#publish-assets-using-search-results-page}

Para publicar ativos usando a página de resultados da pesquisa de ativos:

1. Especifique os critérios na barra de Pesquisa e clique no ícone Pesquisar para exibir os resultados.
2. Selecione os ativos que precisam ser publicados e clique em **Publicar.**
3. Selecione AEM, Dynamic Media ou ambos de acordo com suas necessidades e clique em **Publicar.**
   ![imagem de pesquisa](/help/assets/assets/search-mode.svg)
A opção de publicar no Dynamic Media na página de resultados da pesquisa depende do Modo de publicação do Dynamic Media definido na pasta em que o ativo está disponível no repositório.

   >[!NOTE]
   >
   >Se você selecionar uma pasta e clicar em **Publish** na página de resultados da pesquisa, o Experience Manager Assets exibe uma opção para publicar ativos no AEM e não no Dynamic Media, independentemente das configurações de Modo de publicação do Dynamic Media para a pasta.

## Verificar status de publicação {#check-publish-status}

Para verificar o status de publicação de um ativo ou de uma pasta:

1. Clique em **[!UICONTROL Assets]** no **[!UICONTROL Gerenciamento de ativos]** seção disponível no painel esquerdo.
2. Alterne para a Exibição de lista usando o Alternador de exibição. É possível visualizar as propriedades do ativo, como AEM Publish, Dynamic Media Publish, título, tamanho, dimensões e assim por diante.\
   Se um ativo ou pasta não for publicado, o status para **Publicação no AEM** e **Dynamic Media Publish** colunas é exibida como **N/D**
   ![verificar status de publicação1](/help/assets/assets/check-publish-status1.png)
Se não conseguir exibir as colunas Publicação do AEM e Publicação do Dynamic Media na exibição em Lista:
   1. Clique em ![configurações](/help/assets/assets/settings-icon.svg) e selecione **Publicação no AEM** e **Dynamic Media Publish** colunas do **Colunas configuráveis** diálogo.
   2. Clique em **Confirme.** O Experience Manager Assets adiciona as colunas selecionadas à exibição em Lista.

      ![verificar status de publicação2](/help/assets/assets/check-publish-status2.png)

Você também pode verificar o status de publicação de um ativo selecionando um ativo e clicando em **Detalhes.** Os detalhes estão disponíveis no **Publish** seção disponível no painel direito. A variável **Publish** A seção lista a data em que os ativos são publicados no Dynamic Media e AEM. Se precisar exibir a hora em que os ativos são publicados, navegue até a Exibição de lista e visualize esses detalhes.

![verificar status de publicação 3](/help/assets/assets/check-publish-status3.png)

## Limitações {#limitations}

Por enquanto, os seguintes recursos estão fora do escopo durante a publicação de ativos no AEM e no Dynamic Media:

* Publicar ativos no AEM e no Dynamic Media na página Detalhes do ativo.
* Visualize os endpoints em que os ativos estão sendo publicados usando o assistente de Publicação rápida.
* Adicione ou exclua mais ativos no Assistente de publicação rápida.
* Uma página para exibir ativos publicados.
* Uma capacidade de copiar ou colar o URL do Dynamic Media em um nível de ativo (se os ativos forem publicados no Dynamic Media).
* Capacidade de publicar referências (ativos, tags e assim por diante) ao publicar no AEM.
* Capacidade de substituir o status de sincronização do Dynamic Media no nível da pasta.
* Capacidade de substituir o modo de publicação do Dynamic Media no nível da pasta
* Ainda não há suporte para Gerenciar publicação.
