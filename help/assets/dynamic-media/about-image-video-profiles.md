---
title: Sobre perfis de imagem e perfis de vídeo do Dynamic Media
description: Um Perfil de imagem ou um Perfil de vídeo é uma receita para quais opções se aplicam a ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media você faz upload. Ou, qual Perfil de imagem aplicar aos ativos de imagem da Dynamic Media para cortá-los corretamente.
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: f2f805043ab3037cb8dcc8636ab162c9d0f80e19
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Sobre perfis de imagem e perfis de vídeo do Dynamic Media{#about-dm-image-video-profiles}

Um Perfil de imagem ou Perfil de vídeo é uma receita para quais opções se aplicam a ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media você faz upload. Ou, qual Perfil de imagem aplicar aos ativos de imagem da Dynamic Media para cortá-los corretamente.

No Dynamic Media, você pode criar dois tipos de perfis, que são abordados detalhadamente nos seguintes links:

* [Perfis de imagem do Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Perfis de vídeo do Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte também [Perfis de metadados](/help/assets/metadata-profiles.md).

Você deve ter direitos de Administrador para criar, editar e excluir Perfis de imagem do Dynamic Media ou Perfis de vídeo do Dynamic Media.

Depois de criar o Perfil de imagem ou o Perfil de vídeo, atribua-o a uma ou mais pastas que usa para os ativos recém-carregados do Dynamic Media.

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).


>[!NOTE]
>
>Os ativos que você move de uma pasta para outra não são reprocessados. Por exemplo, suponha que você tenha a Pasta 1 que tem o perfil A atribuído a ela e a Pasta 2 que tem o perfil B atribuído a ela. Se você mover ativos da Pasta 1 para a Pasta 2, os ativos movidos manterão o processamento original da Pasta 1.
>
>O mesmo é verdadeiro mesmo quando você move ativos entre duas pastas que têm o mesmo perfil atribuído a ele.

## Reprocessar ativos do Dynamic Media em uma pasta {#reprocessing-assets}

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem do Dynamic Media ou um Perfil de vídeo do Dynamic Media que você alterou posteriormente.

Por exemplo, suponha que você criou um Perfil de imagem do Dynamic Media e o atribuiu a uma pasta. Qualquer ativo de imagem carregado na pasta tinha automaticamente o Perfil de imagem aplicado aos ativos. No entanto, posteriormente você decide adicionar uma nova proporção de recorte inteligente ao Perfil de imagem. Agora, em vez de ter selecionado e refazer o upload dos ativos para a pasta novamente, basta executar o *Scene7: Reprocessar ativos* fluxo de trabalho.

Você pode executar o fluxo de trabalho de reprocessamento em um ativo para o qual o processamento falhou na primeira vez. Mesmo que você não tenha editado um perfil de imagem ou de vídeo ou já tenha aplicado um perfil de imagem ou de vídeo, ainda poderá executar o fluxo de trabalho de reprocessamento em uma pasta de ativos a qualquer momento.

Opcionalmente, é possível ajustar o tamanho do lote do workflow de reprocessamento a partir de um padrão de 50 ativos até 1000 ativos. Ao executar o _Scene7: Reprocessar ativos_ em uma pasta, os ativos são agrupados em lotes e enviados ao servidor da Dynamic Media para processamento. Após o processamento, os metadados de cada ativo em todo o conjunto de lotes são atualizados em [!DNL Adobe Experience Manager]. Se o tamanho do lote for grande, você pode experimentar um atraso no processamento. Ou, se o tamanho do lote for muito pequeno, pode causar muitas viagens de ida e volta para o servidor do Dynamic Media.

Consulte [Ajuste o tamanho do lote do workflow de reprocessamento](#adjusting-load).

>[!NOTE]
>
>Se você estiver executando uma migração em massa de ativos do Dynamic Media Classic para o [!DNL Experience Manager], ative o agente de replicação Migration no servidor do Dynamic Media. Quando a migração estiver concluída, desative o agente.
>
>O agente de publicação de Migração deve estar desabilitado no servidor do Dynamic Media para que o fluxo de trabalho de Reprocessamento funcione como esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para reprocessar ativos Dynamic Media em uma pasta:**

1. Em [!DNL Experience Manager], na página Ativos , navegue até uma pasta de ativos que tenha um Perfil de imagem ou um Perfil de vídeo atribuído a ela e para a qual deseja aplicar a variável **Scene7: Reprocessar ativo** fluxo de trabalho.

   As pastas que têm um Perfil de imagem ou Perfil de vídeo atribuído a elas têm o nome do perfil exibido logo abaixo do nome da pasta na Exibição de cartão.

1. Selecione uma pasta.

   * O workflow considera todos os arquivos na pasta selecionada, de forma recursiva.
   * Se houver uma ou mais subpastas com ativos na pasta selecionada principal, o workflow reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, evite executar esse workflow em uma hierarquia de pastas que tenha mais de 1000 ativos.

1. Próximo ao canto superior esquerdo da página, na lista suspensa, selecione **[!UICONTROL Linha do tempo]**.
1. Próximo ao canto inferior esquerdo da página, à direita do [!UICONTROL Comentário] selecione o ícone do carrinho ( **^** ).

   ![Reprocessar fluxo de trabalho de ativos 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Selecionar **[!UICONTROL Iniciar fluxo de trabalho]**.
1. No **[!UICONTROL Iniciar fluxo de trabalho]** lista suspensa, escolha **[!UICONTROL Scene7: Reprocessar ativos]**.
1. (Opcional) Na seção **Inserir o título do fluxo de trabalho** , digite um nome para o workflow. Você pode usar o nome para fazer referência à instância do workflow, se necessário.

   ![Reprocessar ativos 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Selecionar **[!UICONTROL Iniciar]**, em seguida selecione **[!UICONTROL Confirmar]**.

   Para monitorar ou verificar o progresso do workflow, no [!DNL Experience Manager] página principal do console, selecione **[!UICONTROL Ferramentas > Fluxo de trabalho]**. Na página Instâncias de fluxo de trabalho , selecione um fluxo de trabalho. Na barra de menus, selecione **[!UICONTROL Abrir Histórico]**. Você também pode encerrar, suspender ou renomear um fluxo de trabalho selecionado na mesma página Instâncias de fluxo de trabalho .

### Ajuste o tamanho do lote do workflow de reprocessamento (opcional) {#adjusting-load}

(Opcional) O tamanho padrão do lote no fluxo de trabalho de reprocessamento é de 50 ativos por trabalho. Esse tamanho ideal do lote é regulado pelo tamanho médio do ativo e pelos tipos MIME de ativos em que o reprocessamento é executado. Um valor maior significa que você tem muitos arquivos em um único trabalho de reprocessamento. Assim, o banner de processamento permanece ativo [!DNL Experience Manager] ativos por um tempo maior. No entanto, se o tamanho médio do arquivo for de 1 MB ou menos Adobe, a recomenda que você aumente o valor para vários 100, mas nunca mais que 1000. Se o tamanho médio do arquivo for de centenas de megabytes, o Adobe recomenda diminuir o tamanho do lote para até 10.

**Para ajustar opcionalmente o tamanho do lote do workflow de reprocessamento:**

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global, selecione o **[!UICONTROL Ferramentas]** Ícone (martelo) > **[!UICONTROL Fluxo de trabalho > Modelos]**.
1. Na página Modelos de fluxo de trabalho , na Exibição de cartão ou na Exibição de lista, selecione **[!UICONTROL Scene7: Reprocessar ativos]**.

   ![Página Modelos de fluxo de trabalho com o Scene7: Fluxo de trabalho Reprocessar ativos selecionado na Exibição de cartão](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**. Uma nova guia do navegador abre o Scene7: Página de modelo de fluxo de trabalho Reprocessar ativos .
1. Na Scene7: Reprocessar ativos na página de fluxo de trabalho, próximo ao canto superior direito, selecione **[!UICONTROL Editar]** para &quot;desbloquear&quot; o workflow.
1. No fluxo de trabalho, selecione o componente Upload em lote do Scene7 para abrir a barra de ferramentas e selecione **[!UICONTROL Configurar]** na barra de ferramentas.

   ![Componente de upload em lote do Scene7](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. No **[!UICONTROL Upload em lote para o Scene7 — Propriedades da etapa]** , defina o seguinte:
   * No **[!UICONTROL Título]** e **[!UICONTROL Descrição]** campos de texto, insira um novo título e descrição para a tarefa, se desejado.
   * Selecionar **[!UICONTROL Avanço do Manipulador]** se o manipulador avançar para a próxima etapa.
   * No **[!UICONTROL Tempo limite]** , insira o tempo limite do processo externo (segundos).
   * No **[!UICONTROL Período]** , insira um intervalo de polling (segundos) para testar a conclusão do processo externo.
   * No **[!UICONTROL Campo em lote]**, insira o número máximo de ativos (50-1000) a serem processados em um trabalho de upload de processamento em lote do servidor Dynamic Media.
   * Selecionar **[!UICONTROL Avanço no tempo limite]** se desejar avançar quando o tempo limite for atingido. Desmarque se deseja continuar com a caixa de entrada quando o tempo limite for atingido.

   ![Caixa de diálogo Propriedades](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. No canto superior direito do **[!UICONTROL Upload em lote para o Scene7 - Propriedades da etapa]** caixa de diálogo, selecione **[!UICONTROL Concluído]**.

1. No canto superior direito da Scene7: Reprocessar página de modelo do fluxo de trabalho Ativos , selecione **[!UICONTROL Sincronizar]**. Quando você vê **[!UICONTROL Sincronizado]**, o modelo de tempo de execução do workflow é sincronizado e pronto para reprocessar ativos em uma pasta.

   ![Sincronizar o modelo de fluxo de trabalho](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Feche a guia do navegador que mostra a Scene7: Reprocessar modelo de fluxo de trabalho do Assets.

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
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
