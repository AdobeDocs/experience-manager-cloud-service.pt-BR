---
title: Publicação rápida no AEM e no Dynamic Media
description: A Publicação rápida na exibição do Assets permite publicar ativos no AEM e Dynamic Media simultaneamente ou separadamente. Você pode selecionar ativos e pastas e optar por publicar no Dynamic Media ou no AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Publicar o Assets no AEM e no Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

O Experience Manager Assets permite publicar ativos rapidamente no Experience Manager e no Dynamic Media usando a visualização Assets. Isso garante que você gerencie seus ativos e publique-os usando a [exibição do Assets sem alternar para a exibição do Administrador](/help/assets/overview.md##persona-based-experiences).

A visualização do Experience Manager Assets oferece a flexibilidade de publicar ativos no AEM, Dynamic Media ou ambos ao mesmo tempo. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos. Todas essas opções para publicar ativos são explicadas neste artigo em detalhes.

## Antes de começar {#before-you-begin}

Defina essas configurações para exibir as opções de publicação para o AEM e Dynamic Media:

* Para exibir as opções de publicação do Dynamic Media, defina as seguintes configurações usando a exibição de Administrador:

   * [Criar uma configuração de Nuvem do Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Defina o modo de publicação do Dynamic Media no nível da pasta. Você também pode definir essas configurações ao criar a configuração do Dynamic Media Cloud. Para substituir essas configurações no nível da pasta, consulte [Configurar publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Para exibir as opções de publicação do AEM, você deve configurar o endpoint de publicação do AEM para o seu ambiente.

## Publicar o Assets durante o upload {#piblish-assets-during-upload}

Você pode publicar ativos no AEM e no Dynamic Media ao fazer upload de ativos para uma pasta. As opções de publicação exibidas dependem das configurações de modo de publicação do Dynamic Media da pasta onde os ativos estão sendo carregados. O modo de publicação do Dynamic Media pode ser definido como:

* **Na ativação:** quando os ativos forem carregados para esta pasta, você deverá publicar explicitamente o ativo primeiro, antes de fornecer um link de URL/Incorporação.

* **Imediato:** quando os ativos são carregados para esta pasta, o sistema assimila os ativos na Experience Manager e fornece a URL/Incorporar instantaneamente.
* **Publicação seletiva:** os Assets são publicados à sua escolha no Experience Manager ou no Dynamic Media para entrega no domínio público.

### Modo de publicação do Dynamic Media definido como Na ativação {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar ativos ao carregá-los em uma pasta cujo Modo de publicação do Dynamic Media esteja definido como **Na ativação**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção **Opções de Publicação** exibe o **Modo de Publicação DM** como **Na Ativação**.
   ![Carregar imagem na ativação](/help/assets/assets/upload-uactivation.svg)
2. Selecione **Publicar no AEM e Dynamic Media** e clique em **Carregar**. Os ativos são publicados no AEM e no Dynamic Media ao mesmo tempo. Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### Modo de publicação do Dynamic Media definido como Imediato {#dynamic-media-publish-mode-set-to-immediate}

Para publicar ativos ao carregá-los em uma pasta cujo Modo de publicação do Dynamic Media esteja definido como **Imediato**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção **Opções de Publicação** exibe o **Modo de Publicação DM** como **Imediato**.
   ![imagem de carregamento de arquivo - modo imediato](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Como o modo de publicação do Dynamic Media é **imediato**, os ativos carregados são publicados automaticamente no Dynamic Media quando você clica em **Carregar**.

2. Selecione **Publicar no AEM** para publicar os ativos carregados no AEM e clique em Carregar.

   Se você selecionar **Publicar no AEM**, os ativos serão publicados no AEM e no Dynamic Media, caso contrário, serão publicados no Dynamic Media.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

### Modo de publicação do Dynamic Media definido como Publicação seletiva {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar ativos durante o carregamento em uma pasta com o Modo de publicação do Dynamic Media definido como **Publicação seletiva**:

1. Clique em **Adicionar Assets** > **Procurar** > **Procurar Arquivos** para navegar até a pasta apropriada para carregar ativos. A seção **Opções de Publicação** exibe o **Modo de Publicação DM** como **Publicação Seletiva**.
   ![modo de publicação seletiva de imagem de carregamento](/help/assets/assets/upload-selective.svg)

2. Selecione **Publicar no AEM**, **Publicar no Dynamic Media**, ou ambos, de acordo com seus requisitos, e clique em **Carregar**.

   Os ativos são publicados no AEM e no Dynamic Media com base em sua seleção.

   Para ver o status de publicação atualizado desses ativos, consulte [Verificar status de publicação](#check-publish-status).

## Publicar ativos usando a página de navegação de ativos {#publish-assets-using-asset-browse-page}

Para publicar ativos usando a página de navegação de ativos:

1. Clique em **Assets** na seção **Assets Management** disponível no painel esquerdo.
2. Selecione um ou mais ativos ou pastas que você precisa publicar e clique em **Publicar**.
3. Selecione **AEM** e clique em **Publicar** para publicar ativos no AEM e no Dynamic Media.
   ![navegação de ativos](/help/assets/assets/browse-uactivation-immediate.svg)
Não é possível publicar uma pasta que tenha o Modo de publicação do Dynamic Media definido como **Publicação seletiva.** Todas as outras pastas ou ativos selecionados são publicados no AEM e no Dynamic Media depois de selecionar AEM.
   ![navegação de ativos](/help/assets/assets/browse-selective123.svg)

## Publicar ativos usando a página de resultados da pesquisa {#publish-assets-using-search-results-page}

Para publicar ativos usando a página de resultados da pesquisa de ativos:

1. Especifique os critérios na barra de pesquisa e clique no ícone de pesquisa para exibir os resultados.
2. Selecione os ativos que você precisa publicar e clique em **Publicar.**
3. Selecione AEM, Dynamic Media ou ambos conforme seus requisitos e clique em **Publicar.**
   ![pesquisar imagem](/help/assets/assets/search-mode.svg)
A opção de publicar no Dynamic Media na página de resultados da pesquisa depende do Modo de publicação do Dynamic Media definido na pasta em que o ativo está disponível no repositório.

   >[!NOTE]
   >
   >Se você selecionar uma pasta e clicar em **Publicar** na página de resultados da pesquisa, o Experience Manager Assets exibirá uma opção para publicar ativos no AEM, e não no Dynamic Media, independentemente das configurações de Modo de publicação do Dynamic Media da pasta.

## Verificar status de publicação {#check-publish-status}

Para verificar o status publicado de um ativo ou de uma pasta:

1. Clique em **[!UICONTROL Assets]** na seção **[!UICONTROL Assets Management]** disponível no painel esquerdo.
2. Alterne para a exibição em Lista usando o Alternador de exibição. É possível visualizar as propriedades do ativo, como publicação no AEM, publicação no Dynamic Media, título, tamanho, dimensões e assim por diante.\
   Se um ativo ou pasta não for publicado, o status das colunas **Publicação do AEM** e **Publicação do Dynamic Media** será exibido como **N/D.**
   ![verificar status da publicação1](/help/assets/assets/check-publish-status1.png)
Se não conseguir exibir as colunas Publicação do AEM e Publicação do Dynamic Media na exibição em Lista:
   1. Clique em ![configurações](/help/assets/assets/settings-icon.svg) e selecione as colunas **Publicação do AEM** e **Publicação do Dynamic Media** na caixa de diálogo **Colunas Configuráveis**.
   2. Clique em **Confirmar.** O Experience Manager Assets adiciona as colunas selecionadas ao modo de exibição de Lista.

      ![verificar status da publicação2](/help/assets/assets/check-publish-status2.png)

Você também pode verificar o status de publicação de um ativo selecionando um ativo e clicando em **Detalhes.** Os detalhes estão disponíveis na seção **Publicar**, disponível no painel direito. A seção **Publicar** lista a data em que os ativos são publicados no Dynamic Media e no AEM. Se precisar exibir a hora em que os ativos são publicados, navegue até a Exibição de lista e visualize esses detalhes.

![verificar status de publicação 3](/help/assets/assets/check-publish-status3.png)

## Limitações {#limitations}

Por enquanto, os seguintes recursos estão fora do escopo durante a publicação de ativos no AEM e no Dynamic Media:

* Publicar ativos no AEM e Dynamic Media a partir da página de detalhes do ativo.
* Visualize os endpoints em que os ativos são publicados usando o assistente de Publicação rápida.
* Adicione ou exclua mais ativos no Assistente de publicação rápida.
* Uma página para exibir ativos publicados.
* Uma capacidade de copiar ou colar o URL do Dynamic Media no nível do ativo (se os ativos forem publicados no Dynamic Media).
* Capacidade de publicar referências (ativos, tags e assim por diante) ao publicar no AEM.
* Capacidade de substituir o status de sincronização do Dynamic Media no nível da pasta.
* Capacidade de substituir o modo de publicação do Dynamic Media no nível da pasta
* Ainda não há suporte para Gerenciar publicação.
