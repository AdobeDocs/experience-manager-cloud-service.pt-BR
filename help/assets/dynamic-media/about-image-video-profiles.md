---
title: Sobre perfis de imagem e perfis de vídeo do Dynamic Media
description: Um Perfil de imagem ou um Perfil de vídeo é uma fórmula para quais opções aplicar aos ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media que você carrega. Ou qual perfil de imagem aplicar aos ativos de imagem do Dynamic Media para cortá-los corretamente.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 0%

---

# Sobre perfis de imagem e perfis de vídeo do Dynamic Media{#about-dm-image-video-profiles}

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

Um Perfil de imagem ou Perfil de vídeo é uma fórmula para quais opções aplicar aos ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media que você carrega. Ou qual perfil de imagem aplicar aos ativos de imagem do Dynamic Media para cortá-los corretamente.

No Dynamic Media, você pode criar dois tipos de perfis, que são abordados em detalhes nos seguintes links:

* [Perfis de imagem do Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Perfis de vídeo do Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte também [Perfis de metadados](/help/assets/metadata-profiles.md).

Você deve ter direitos de administrador para criar, editar e excluir Perfis de imagem do Dynamic Media ou Perfis de vídeo do Dynamic Media.

Depois de criar o Perfil de imagem ou o Perfil de vídeo, você o atribui a uma ou mais pastas que usa para ativos do Dynamic Media recém-carregados.

Consulte também [Práticas recomendadas para organizar sua Assets digital para usar Perfis de processamento](/help/assets/organize-assets.md).


>[!NOTE]
>
>O Assets que você move de uma pasta para outra não é reprocessado. Por exemplo, suponha que você tenha uma Pasta 1 com o perfil A atribuído a ela e uma Pasta 2 com o perfil B atribuído a ela. Se você mover ativos da Pasta 1 para a Pasta 2, os ativos movidos manterão o processamento original da Pasta 1.
>
>O mesmo é verdadeiro mesmo quando você move ativos entre duas pastas que têm o mesmo perfil atribuído a elas.

## Reprocessamento de ativos do Dynamic Media em uma pasta {#reprocessing-assets}

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem do Dynamic Media ou um Perfil de vídeo do Dynamic Media que você alterou posteriormente.

Por exemplo, suponha que você tenha criado um Perfil de imagem de mídia dinâmica e o atribuído a uma pasta. Todos os ativos de imagem carregados na pasta automaticamente tinham o Perfil de imagem aplicado aos ativos. No entanto, mais tarde, você decide adicionar uma nova taxa de corte inteligente ao Perfil de imagem. Agora, em vez de precisar selecionar e recarregar os ativos na pasta novamente, basta executar o fluxo de trabalho *Reprocessamento do Dynamic Media*.

Você pode executar o fluxo de trabalho de reprocessamento em um ativo cujo processamento falhou pela primeira vez. Mesmo que você não tenha editado um Perfil de imagem ou Perfil de vídeo, ou já tenha aplicado um Perfil de imagem ou Perfil de vídeo, ainda será possível executar o fluxo de trabalho de reprocessamento em uma pasta de ativos a qualquer momento.

Como opção, é possível ajustar o tamanho do lote do fluxo de trabalho de reprocessamento de um padrão de 50 ativos até 1000 ativos. Ao executar o fluxo de trabalho _Reprocessamento do Dynamic Media_ em uma pasta, os ativos são agrupados em lotes e depois enviados ao servidor do Dynamic Media para processamento. Após o processamento, os metadados de cada ativo em todo o conjunto de lotes são atualizados em [!DNL Adobe Experience Manager]. Se o tamanho do lote for grande, você pode enfrentar um atraso no processamento. Ou, se o tamanho do lote for muito pequeno, isso poderá causar muitas viagens de ida e volta para o servidor do Dynamic Media.

Consulte [Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento](#adjusting-load).

>[!NOTE]
>
>Se você estiver executando uma migração em massa de ativos do Dynamic Media Classic para o [!DNL Experience Manager], habilite o agente de replicação de migração no servidor do Dynamic Media. Quando a migração for concluída, desative o agente.
>
>O agente de publicação de migração deve ser desativado no servidor do Dynamic Media para que o fluxo de trabalho de reprocessamento funcione conforme esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para reprocessar ativos do Dynamic Media em uma pasta:**

1. No [!DNL Experience Manager], na página do Assets, navegue até uma pasta de ativos que tenha um Perfil de Imagem ou um Perfil de Vídeo atribuído a ele e para o qual você deseja aplicar o fluxo de trabalho **Reprocessamento de Dynamic Media**.

   As pastas que têm um Perfil de imagem ou Perfil de vídeo atribuído a elas têm o nome do perfil exibido logo abaixo do nome da pasta na Exibição de cartão.

1. Selecione uma pasta.

   * O fluxo de trabalho considera todos os arquivos na pasta selecionada de forma recursiva.
   * Se houver uma ou mais subpastas com ativos na pasta principal selecionada, o fluxo de trabalho reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, evite executar esse fluxo de trabalho em uma hierarquia de pastas com mais de 1000 ativos.

1. Próximo ao canto superior esquerdo da página, na lista suspensa, selecione **[!UICONTROL Linha do tempo]**.
1. Próximo ao canto inferior esquerdo da página, à direita do campo [!UICONTROL Comentário], selecione o ícone de quilate ( **^** ).

   ![Captura de tela do Assets no Experience Manager mostrando uma pasta selecionada de ativos, a lista suspensa Linha do tempo destacada, o botão Iniciar fluxo de trabalho destacado e o ícone de carrinho à direita do campo Comentário também destacado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Selecione **[!UICONTROL Iniciar Fluxo de Trabalho]**.
1. Na lista suspensa **[!UICONTROL Iniciar Fluxo de Trabalho]**, escolha **[!UICONTROL Reprocessamento do Dynamic Media]**.
1. (Opcional) No campo de texto **Inserir título do fluxo de trabalho**, digite um nome para o fluxo de trabalho. Você pode usar o nome para fazer referência à instância do workflow, se necessário.

   ![Captura de tela da interface de usuário da Linha do Tempo com a opção &quot;Reprocessamento do Dynamic Media&quot; selecionada na lista suspensa Iniciar Fluxo de Trabalho e o botão Iniciar realçado](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. Selecione **[!UICONTROL Iniciar]** e **[!UICONTROL Confirmar]**.

   Para monitorar o fluxo de trabalho ou verificar seu progresso, na página de console principal [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas > Fluxo de trabalho]**. Na página Instâncias do fluxo de trabalho, selecione um fluxo de trabalho. Na barra de menus, selecione **[!UICONTROL Abrir Histórico]**. Você também pode encerrar, suspender ou renomear um workflow selecionado na mesma página Instâncias do workflow.

### Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento (opcional) {#adjusting-load}

(Opcional) O tamanho de lote padrão no fluxo de trabalho de reprocessamento é de 50 ativos por trabalho. Esse tamanho ideal do lote é determinado pelo tamanho médio do ativo e pelos tipos MIME de ativos nos quais o reprocessamento é executado. Um valor mais alto significa que você tem muitos arquivos em um único trabalho de reprocessamento. Portanto, o banner de processamento permanece nos ativos [!DNL Experience Manager] por mais tempo. No entanto, se o tamanho médio do arquivo for pequeno - 1 MB ou menos - a Adobe recomenda aumentar o valor para vários 100, mas nunca mais do que 1000. Se o tamanho médio do arquivo for de centenas de megabytes, a Adobe recomenda que você reduza o tamanho do lote para 10.

**Para ajustar opcionalmente o tamanho do lote do fluxo de trabalho de reprocessamento:**

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global e, em seguida, selecione o ícone **[!UICONTROL Ferramentas]** (martelo) > **[!UICONTROL Fluxo de trabalho > Modelos]**.
1. Na página Modelos de fluxo de trabalho, no Modo de exibição de cartão ou no Modo de exibição de lista, selecione **[!UICONTROL Reprocessamento do Dynamic Media]**.

   ![Captura de tela da página Modelos de Fluxo de Trabalho com o fluxo de trabalho &quot;Reprocessamento de Dynamic Media&quot; selecionado na exibição Cartão do Experience Manager](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**. Uma nova guia do navegador abre a página de modelo de fluxo de trabalho de Reprocessamento do Dynamic Media.
1. Na página de fluxo de trabalho Reprocessamento de Dynamic Media, próximo ao canto superior direito, selecione **[!UICONTROL Editar]** para &quot;desbloquear&quot; o fluxo de trabalho.
1. No fluxo de trabalho, selecione o componente de Carregamento em lote do Scene7 para abrir a barra de ferramentas e selecione **[!UICONTROL Configurar]** na barra de ferramentas.

   ![Captura de tela do componente &quot;Carregamento em lote do Scene7&quot; na página &quot;Reprocessamento do Dynamic Media&quot; com o ponteiro do mouse sobre o ícone &quot;Configurar&quot;](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. Na caixa de diálogo **[!UICONTROL Carregar em Lote para o Scene7—Propriedades da Etapa]**, defina o seguinte:
   * Nos campos de texto **[!UICONTROL Título]** e **[!UICONTROL Descrição]**, insira um novo título e descrição para o trabalho, se desejado.
   * Selecione **[!UICONTROL Avanço do manipulador]** se o seu manipulador avançar para a próxima etapa.
   * No campo **[!UICONTROL Tempo limite]**, insira o tempo limite do processo externo (segundos).
   * No campo **[!UICONTROL Período]**, insira um intervalo de sondagem (segundos) para testar a conclusão do processo externo.
   * No **[!UICONTROL Campo de lote]**, insira o número máximo de ativos (50-1000) a serem processados em um trabalho de carregamento de processamento em massa do servidor Dynamic Media.
   * Selecione **[!UICONTROL Avançar no tempo limite]** se desejar avançar quando o tempo limite for atingido. Desmarque se deseja continuar na caixa de entrada quando o tempo limite for atingido.

   ![Captura de tela da página &quot;Carregamento em lote para o Scene7 - Propriedades da etapa&quot;](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. No canto superior direito da caixa de diálogo **[!UICONTROL Carregamento em lote para o Scene7 - Propriedades da etapa]**, selecione **[!UICONTROL Concluído]**.

1. No canto superior direito da página do modelo de fluxo de trabalho de Reprocessamento do Dynamic Media, selecione **[!UICONTROL Sincronizar]**. Quando você vê **[!UICONTROL Sincronizado]**, o modelo de tempo de execução de fluxo de trabalho foi sincronizado com êxito e está pronto para reprocessar ativos em uma pasta.

   ![Captura de tela do Assets no Experience Manager mostrando uma pasta selecionada de ativos, a lista suspensa Linha do tempo destacada, o botão Iniciar fluxo de trabalho destacado e o ícone de carrinho à direita do campo Comentário também destacado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Feche a guia do navegador que mostra o modelo de fluxo de trabalho de Reprocessamento do Dynamic Media.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
