---
title: Sobre perfis de imagem e perfis de vídeo do Dynamic Media
description: Um Perfil de imagem ou um Perfil de vídeo é uma fórmula para quais opções aplicar aos ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media que você carrega. Ou qual perfil de imagem aplicar aos ativos de imagem do Dynamic Media para cortá-los corretamente.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---

# Sobre perfis de imagem e perfis de vídeo do Dynamic Media{#about-dm-image-video-profiles}

Um Perfil de imagem ou Perfil de vídeo é uma fórmula para quais opções aplicar aos ativos que você faz upload em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media que você carrega. Ou qual perfil de imagem aplicar aos ativos de imagem do Dynamic Media para cortá-los corretamente.

No Dynamic Media, você pode criar dois tipos de perfis, que são abordados detalhadamente nos seguintes links:

* [Perfis de imagem do Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Perfis de vídeo Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte também [Perfis de metadados](/help/assets/metadata-profiles.md).

Você deve ter direitos de administrador para criar, editar e excluir Perfis de imagem do Dynamic Media ou Perfis de vídeo do Dynamic Media.

Depois de criar o Perfil de imagem ou o Perfil de vídeo, atribua-o a uma ou mais pastas que você usa para ativos do Dynamic Media recém-carregados.

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).


>[!NOTE]
>
>Os ativos que você move de uma pasta para outra não são reprocessados. Por exemplo, suponha que você tenha uma Pasta 1 com o perfil A atribuído a ela e uma Pasta 2 com o perfil B atribuído a ela. Se você mover ativos da Pasta 1 para a Pasta 2, os ativos movidos manterão o processamento original da Pasta 1.
>
>O mesmo é verdadeiro mesmo quando você move ativos entre duas pastas que têm o mesmo perfil atribuído a elas.

## Reprocessar ativos do Dynamic Media em uma pasta {#reprocessing-assets}

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem do Dynamic Media existente ou um Perfil de vídeo do Dynamic Media que você alterou posteriormente.

Por exemplo, suponha que você criou um Perfil de imagem do Dynamic Media e o atribuiu a uma pasta. Todos os ativos de imagem carregados na pasta automaticamente tinham o Perfil de imagem aplicado aos ativos. No entanto, mais tarde, você decide adicionar uma nova taxa de corte inteligente ao Perfil de imagem. Agora, em vez de precisar selecionar e fazer upload novamente dos ativos para a pasta, execute o *Scene7: Reprocessar ativos* fluxo de trabalho.

Você pode executar o fluxo de trabalho de reprocessamento em um ativo cujo processamento falhou pela primeira vez. Mesmo que você não tenha editado um Perfil de imagem ou Perfil de vídeo, ou já tenha aplicado um Perfil de imagem ou Perfil de vídeo, ainda será possível executar o fluxo de trabalho de reprocessamento em uma pasta de ativos a qualquer momento.

Como opção, é possível ajustar o tamanho do lote do fluxo de trabalho de reprocessamento de um padrão de 50 ativos até 1000 ativos. Quando você executa o _Scene7: Reprocessar ativos_ em uma pasta, os ativos são agrupados em lotes e depois enviados ao servidor do Dynamic Media para processamento. Após o processamento, os metadados de cada ativo no conjunto de lotes inteiro são atualizados em [!DNL Adobe Experience Manager]. Se o tamanho do lote for grande, você pode enfrentar um atraso no processamento. Ou, se o tamanho do lote for muito pequeno, poderá causar muitas viagens de ida e volta para o servidor do Dynamic Media.

Consulte [Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento](#adjusting-load).

>[!NOTE]
>
>Se você estiver executando uma migração em massa de ativos do Dynamic Media Classic para o [!DNL Experience Manager], habilite o Agente de replicação de migração no servidor do Dynamic Media. Quando a migração for concluída, desative o agente.
>
>O agente de publicação de migração deve ser desativado no servidor do Dynamic Media para que o fluxo de trabalho de reprocessamento funcione conforme esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para reprocessar ativos do Dynamic Media em uma pasta:**

1. Entrada [!DNL Experience Manager], na página Ativos, navegue até uma pasta de ativos que tenha um Perfil de imagem ou um Perfil de vídeo atribuído a ele e para a qual você deseja aplicar a **Scene7: Reprocessar ativo** fluxo de trabalho.

   As pastas que têm um Perfil de imagem ou Perfil de vídeo atribuído a elas têm o nome do perfil exibido logo abaixo do nome da pasta na Exibição de cartão.

1. Selecione uma pasta.

   * O fluxo de trabalho considera todos os arquivos na pasta selecionada de forma recursiva.
   * Se houver uma ou mais subpastas com ativos na pasta principal selecionada, o fluxo de trabalho reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, evite executar esse fluxo de trabalho em uma hierarquia de pastas com mais de 1000 ativos.

1. Próximo ao canto superior esquerdo da página, na lista suspensa, selecione **[!UICONTROL Linha do tempo]**.
1. Próximo ao canto inferior esquerdo da página, à direita da [!UICONTROL Comentário] , selecione o ícone de quilate ( **^** ).

   ![Captura de tela de Ativos no Experience Manager mostrando uma pasta selecionada de ativos, a lista suspensa Linha do tempo destacada, o botão Iniciar fluxo de trabalho destacado e o ícone de carrinho à direita do campo Comentário também destacado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Selecionar **[!UICONTROL Iniciar fluxo de trabalho]**.
1. No **[!UICONTROL Iniciar fluxo de trabalho]** selecione **[!UICONTROL Scene7: Reprocessar ativos]**.
1. (Opcional) Na **Inserir título do fluxo de trabalho** digite um nome para o workflow. Você pode usar o nome para fazer referência à instância do workflow, se necessário.

   ![Captura de tela da interface do usuário da Linha do tempo com a opção &quot;Scene7: Reprocessar ativos&quot; selecionada na lista suspensa Iniciar fluxo de trabalho, e o botão Iniciar realçado](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. Selecionar **[!UICONTROL Início]** e selecione **[!UICONTROL Confirmar o]**.

   Para monitorar o workflow ou verificar seu progresso, no [!DNL Experience Manager] página do console principal, selecione **[!UICONTROL Ferramentas > Fluxo de trabalho]**. Na página Instâncias do fluxo de trabalho, selecione um fluxo de trabalho. Na barra de menus, selecione **[!UICONTROL Abrir histórico]**. Você também pode encerrar, suspender ou renomear um workflow selecionado na mesma página Instâncias do workflow.

### Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento (opcional) {#adjusting-load}

(Opcional) O tamanho de lote padrão no fluxo de trabalho de reprocessamento é de 50 ativos por trabalho. Esse tamanho ideal do lote é determinado pelo tamanho médio do ativo e pelos tipos MIME de ativos nos quais o reprocessamento é executado. Um valor mais alto significa que você tem muitos arquivos em um único trabalho de reprocessamento. Assim, o banner de processamento permanece ativado [!DNL Experience Manager] ativos por mais tempo. No entanto, se o tamanho médio do arquivo for pequeno - 1 MB ou menos - o Adobe recomenda que você aumente o valor para vários 100, mas nunca mais do que um 1000. Se o tamanho médio do arquivo for centenas de megabytes, a Adobe recomenda que você reduza o tamanho do lote para 10.

**Como opção, para ajustar o tamanho do lote do workflow de reprocessamento:**

1. Entrada [!DNL Experience Manager], selecione **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global, selecione a guia **[!UICONTROL Ferramentas]** Ícone (martelo) > **[!UICONTROL Fluxo de trabalho > Modelos]**.
1. Na página Modelos de fluxo de trabalho, na Exibição de cartão ou na Exibição de lista, selecione **[!UICONTROL Scene7: Reprocessar ativos]**.

   ![Captura de tela da página Modelos de fluxo de trabalho com o fluxo de trabalho &quot;Scene7: Reprocessar ativos&quot; selecionado na exibição Cartão do Experience Manager](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**. Uma nova guia do navegador abre a página Scene7: Reprocessar ativos do modelo de fluxo de trabalho.
1. Na página de fluxo de trabalho Scene7: Reprocessar ativos, próximo ao canto superior direito, selecione **[!UICONTROL Editar]** para &quot;desbloquear&quot; o workflow.
1. No fluxo de trabalho, selecione o componente Scene7 Batch Upload para abrir a barra de ferramentas e selecione **[!UICONTROL Configurar]** na barra de ferramentas.

   ![Captura de tela do componente &quot;Upload em lote do Scene7&quot; na página &quot;Scene7: Reprocessamento de ativos&quot; com o ponteiro do mouse sobre o ícone &quot;Configurar&quot;](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. No **[!UICONTROL Upload em lote para o Scene7 — Propriedades da etapa]** defina o seguinte:
   * No **[!UICONTROL Título]** e **[!UICONTROL Descrição]** campos de texto, insira um novo título e descrição para a tarefa, se desejado.
   * Selecionar **[!UICONTROL Avanço do manipulador]** se o seu manipulador avançar para a próxima etapa.
   * No **[!UICONTROL Tempo limite]** insira o tempo limite do processo externo (segundos).
   * No **[!UICONTROL Período]** insira um intervalo de pesquisa (segundos) para testar a conclusão do processo externo.
   * No **[!UICONTROL Campo de lote]**, insira o número máximo de ativos (50-1000) a serem processados em um trabalho de upload de processamento em massa do servidor do Dynamic Media.
   * Selecionar **[!UICONTROL Avançar no tempo limite]** se desejar avançar quando o tempo limite for atingido. Desmarque se deseja continuar na caixa de entrada quando o tempo limite for atingido.

   ![Captura de tela da página &quot;Upload em lote para o Scene7 - Propriedades da etapa&quot;](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. No canto superior direito da **[!UICONTROL Upload em lote para o Scene7 - Propriedades da etapa]** caixa de diálogo, selecione **[!UICONTROL Concluído]**.

1. No canto superior direito da página do modelo de fluxo de trabalho Scene7: Reprocessar ativos, selecione **[!UICONTROL Sincronizar]**. Quando você vê **[!UICONTROL Sincronizado]**, o modelo de tempo de execução de fluxo de trabalho foi sincronizado com sucesso e está pronto para reprocessar ativos em uma pasta.

   ![Captura de tela de Ativos no Experience Manager mostrando uma pasta selecionada de ativos, a lista suspensa Linha do tempo destacada, o botão Iniciar fluxo de trabalho destacado e o ícone de carrinho à direita do campo Comentário também destacado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Feche a guia do navegador que mostra o modelo de fluxo de trabalho Scene7: Reprocessar ativos.

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
