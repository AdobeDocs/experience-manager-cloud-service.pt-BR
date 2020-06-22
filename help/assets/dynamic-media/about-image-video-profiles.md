---
title: Sobre Perfis de imagem Dynamic Media e Perfis de vídeo
description: Um Perfil de imagem ou um Perfil de vídeo é uma receita para quais opções se aplicam aos ativos que você carrega em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media você carrega. Ou qual Perfil de imagem aplicar aos ativos de imagem do Dynamic Media para que eles sejam cortados corretamente.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 2%

---


# Sobre Perfis de imagem Dynamic Media e Perfis de vídeo{#about-dm-image-video-profiles}

Um Perfil de imagem ou um Perfil de vídeo é uma receita para quais opções se aplicam aos ativos que você carrega em uma pasta. Por exemplo, você pode especificar qual codificação de vídeo aplicar aos ativos de vídeo do Dynamic Media você carrega. Ou qual Perfil de imagem aplicar aos ativos de imagem do Dynamic Media para que eles sejam cortados corretamente.

No Dynamic Media, você pode criar dois tipos de perfis, que são abordados detalhadamente nos seguintes links:

* [perfis de imagem Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [perfis de vídeo Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte também perfis [de metadados](/help/assets/metadata-profiles.md).

Você deve ter direitos de Administrador para criar, editar e excluir Perfis de imagem Dynamic Media ou Perfis de vídeo Dynamic Media.

Depois de criar o Perfil de imagem ou o Perfil de vídeo, atribua-o a uma ou mais pastas usadas como destino para os ativos do Dynamic Media carregados recentemente.

Consulte também Práticas [recomendadas para organizar seus ativos digitais para usar Perfis de imagem ou Perfis](/help/assets/dynamic-media/best-practices-for-file-management.md)de vídeo.

>[!NOTE]
>
>Os ativos movidos de uma pasta para outra não são reprocessados. Por exemplo, suponha que você tenha a Pasta 1 com o perfil A atribuído a ela e a Pasta 2 com o perfil B atribuído a ela. Se você mover ativos da Pasta 1 para a Pasta 2, os ativos movidos manterão seu processamento original da Pasta 1.
>
>O mesmo ocorre mesmo quando você move ativos entre duas pastas que têm o mesmo perfil atribuído a ele.

## Reprocessamento de ativos Dynamic Media em uma pasta {#reprocessing-assets}

Você pode reprocessar ativos em uma pasta que já tenha um Perfil Dynamic Media Image ou um Perfil Dynamic Media Video que você tenha alterado posteriormente.

Por exemplo, suponha que você tenha criado um Perfil de imagem Dynamic Media e o atribuiu a uma pasta. Todos os ativos de imagem carregados na pasta tinham automaticamente o Perfil de imagem aplicado aos ativos. No entanto, depois você decide adicionar uma nova proporção de recorte inteligente ao Perfil de imagem. Agora, em vez de ter selecionado e carregado novamente os ativos para a pasta, basta executar o *Scene7: Reprocessar fluxo de trabalho de Ativos* .

Você pode executar o fluxo de trabalho de reprocessamento em um ativo cujo processamento falhou na primeira vez. Assim, mesmo se você não tiver editado um Perfil de imagem ou um perfil de vídeo, ou se já tiver aplicado um Perfil de imagem ou um Perfil de vídeo, ainda poderá executar o fluxo de trabalho de reprocessamento em uma pasta de ativos a qualquer momento.

Como opção, você pode ajustar o tamanho do lote do fluxo de trabalho de reprocessamento a partir de um padrão de 50 ativos até 1000 ativos. Ao executar o _Scene7: Processar novamente o fluxo de trabalho dos Ativos_ em uma pasta, os ativos são agrupados em lotes e enviados ao servidor Dynamic Media para processamento. Após o processamento, os metadados de cada ativo em todo o conjunto de lotes são atualizados no AEM. Se o tamanho do lote for muito grande, pode ocorrer um atraso no processamento. Ou, se o tamanho do lote for muito pequeno, pode causar muitas viagens de ida e volta ao servidor Dynamic Media.

Consulte [Ajustar o tamanho do lote do fluxo de trabalho](#adjusting-load)de reprocessamento.

>[!NOTE]
>
>Se você estiver realizando uma migração em massa de ativos do Dynamic Media Classic para o AEM, deverá ativar o agente de replicação de Migração no servidor Dynamic Media. Quando a migração estiver concluída, desative o agente.
O agente de publicação de Migração deve estar desabilitado no servidor Dynamic Media para que o fluxo de trabalho de Reprocessamento funcione como esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para reprocessar ativos Dynamic Media em uma pasta**:
1. No AEM, na página Ativos, navegue até uma pasta de ativos do Dynamic Media que tenha um Perfil de imagem ou um Perfil de vídeo atribuído a ele e para o qual você deseja aplicar o **Scene7: Reprocessar fluxo de trabalho de ativos** ,

   As pastas que tiverem um Perfil de imagem ou um Perfil de vídeo já atribuídos a ele serão indicadas pela exibição do nome do perfil logo abaixo do nome da pasta na Visualização de placa.

1. Selecione uma pasta.

   * O fluxo de trabalho considera todos os arquivos na pasta selecionada, recursivamente.
   * Se houver uma ou mais subpastas com ativos na pasta selecionada principal, o fluxo de trabalho reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, você deve evitar executar esse fluxo de trabalho em uma hierarquia de pastas que tenha mais de 1000 ativos.

1. Próximo ao canto superior esquerdo da página, na lista suspensa, clique em **[!UICONTROL Linha do tempo]**.
1. Perto do canto inferior esquerdo da página, à direita do campo Comentário, clique no ícone de carrinho ( **^** ) .

   ![Reprocessar fluxo de trabalho de ativos 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Clique em Fluxo de trabalho do **[!UICONTROL Start]**.
1. Na lista suspensa Fluxo de trabalho **[!UICONTROL do]** Start, escolha **[!UICONTROL Scene7: Reprocessar ativos]**.
1. (Opcional) No campo **Inserir título do campo de texto do fluxo de trabalho** , insira um nome para o fluxo de trabalho. Você pode usar o nome para fazer referência à instância do fluxo de trabalho, se necessário.

   ![Reprocessar ativos 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Clique em **[!UICONTROL Start]** e, em seguida, clique em **[!UICONTROL Confirmar]**.

   Para monitorar o fluxo de trabalho ou verificar seu progresso, na página principal do console do AEM, clique em **[!UICONTROL Ferramentas > Fluxo de trabalho]**. Na página Instâncias do fluxo de trabalho, selecione um fluxo de trabalho. Na barra de menus, clique em **[!UICONTROL Abrir histórico]**. Você também pode encerrar, suspender ou renomear um fluxo de trabalho selecionado na mesma página Instâncias de fluxo de trabalho.

### Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento {#adjusting-load}

(Opcional) O tamanho padrão do lote no fluxo de trabalho de reprocessamento é de 50 ativos por tarefa. O tamanho ideal do lote é regido pelo tamanho médio do ativo e pelos tipos MIME de ativos nos quais o reprocessamento é executado. Um valor mais alto significa que você terá muitos arquivos em um único trabalho de reprocessamento. Dessa forma, o banner de processamento permanece nos ativos AEM por mais tempo. No entanto, se o tamanho médio do arquivo for pequeno a 1 MB ou menos, a Adobe recomenda que você aumente o valor para várias centenas, mas nunca mais que 1000. Se o tamanho médio do arquivo for grande - centenas de megabytes - a Adobe recomenda que você reduza o tamanho do lote para até 10.

**Como opção, ajuste o tamanho do lote do fluxo de trabalho de reprocessamento**

1. No Experience Manager, toque em **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global e, em seguida, toque no ícone **[!UICONTROL Ferramentas]** (martelo) > **[!UICONTROL Fluxo de trabalho > Modelos]**.
1. Na página Modelos de fluxo de trabalho, em Visualização de cartão ou Visualização de Lista, selecione **[!UICONTROL Scene7: Reprocessar ativos]**.

   ![Página Modelos de fluxo de trabalho com o Scene7: Reprocessar fluxo de trabalho de Ativos selecionado na Visualização de Cartão](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Editar]**. Uma nova guia do navegador abre o Scene7: Reprocessar página de modelo de fluxo de trabalho dos Ativos.
1. No Scene7: Reprocessar a página de fluxo de trabalho Ativos, próximo ao canto superior direito, toque em **[!UICONTROL Editar]** para &quot;desbloquear&quot; o fluxo de trabalho.
1. No fluxo de trabalho, selecione o componente de Upload em lote do Scene7 para abrir a barra de ferramentas e, em seguida, toque em **[!UICONTROL Configurar]** na barra de ferramentas.

   ![Componente de Upload em lote do Scene7](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. Na caixa de diálogo Carregamento em **[!UICONTROL lote para o Scene7—Step Properties]** , defina o seguinte:
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * Selecione **[!UICONTROL Manipulador avançado]** se o seu manipulador avançar para a próxima etapa.
   * No campo **[!UICONTROL Tempo limite]** , informe o tempo limite do processo externo (segundos).
   * No campo **[!UICONTROL Período]** , informe um intervalo de polling (segundos) para testar a conclusão do processo externo.
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * Selecione **[!UICONTROL Avançar no tempo limite]** se desejar avançar quando o tempo limite for atingido. Desmarque se deseja continuar com a caixa de entrada quando o tempo limite for atingido.

   ![Caixa de diálogo Propriedades](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. No canto superior direito da caixa de diálogo Carregamento em **[!UICONTROL lote para o Scene7 - Propriedades]** da etapa, toque em **[!UICONTROL Concluído]**.

1. No canto superior direito do Scene7: Reprocessar a página de modelo de fluxo de trabalho do Assets, toque em **[!UICONTROL Sincronizar]**. Quando você vê **[!UICONTROL Sincronizado]**, o modelo de tempo de execução do fluxo de trabalho é sincronizado e pronto para reprocessar ativos em uma pasta.

   ![Sincronizar o modelo de fluxo de trabalho](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Feche a guia do navegador que mostra o Scene7: Reprocessar modelo de fluxo de trabalho de Ativos.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
