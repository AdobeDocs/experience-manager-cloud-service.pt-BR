---
title: Gerenciar ativos digitais
description: Saiba mais sobre vários métodos de edição e gerenciamento de ativos
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: c49352926c67587096b8c60840e00bf379b92075
workflow-type: tm+mt
source-wordcount: '4063'
ht-degree: 11%

---

# Gerenciar ativos {#manage-assets}

Este artigo descreve como gerenciar e editar ativos no [!DNL Adobe Experience Manager Assets]. Para gerenciar [!DNL Content Fragments], consulte [[!DNL Content Fragments]](content-fragments/content-fragments.md) ativos.

## Criar pastas {#creating-folders}

Ao organizar uma coleção de ativos, por exemplo, todos `Nature` , é possível criar pastas para mantê-las juntas. Você pode usar pastas para categorizar e organizar seus ativos. [!DNL Experience Manager Assets] não exige que você organize ativos em pastas para funcionar melhor.

>[!NOTE]
>
>* Compartilhamento de uma pasta de Ativos do tipo `sling:OrderedFolder`, não é compatível ao compartilhar com o Marketing Cloud. Se deseja compartilhar uma pasta, não selecione [!UICONTROL Solicitado] ao criar uma pasta.
>* Experience Manager não permite usar `subassets` palavra como o nome de uma pasta. É uma palavra-chave reservada para nós que contêm subativos para ativos compostos


1. Navegue até o local na pasta de ativos digitais onde deseja criar uma nova pasta. No menu, clique em **[!UICONTROL Criar]**. Selecionar **[!UICONTROL Nova pasta]**.
1. No **[!UICONTROL Título]** , forneça um nome de pasta. Por padrão, o DAM usa o título fornecido como o nome da pasta. Depois que a pasta for criada, é possível substituir o padrão e especificar outro nome de pasta.
1. Clique em **[!UICONTROL Criar]**. Sua pasta é exibida na pasta de ativos digitais.

Os seguintes caracteres (lista separada por espaços de) não são suportados:

* Um nome de arquivo de ativo não pode conter nenhum destes caracteres: `* / : [ \\ ] | # % { } ? &`
* Um nome de pasta de ativos não pode conter nenhum destes caracteres: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Fazer upload de ativos {#uploading-assets}

Consulte [adicionar ativos digitais ao Experience Manager](add-assets.md).

## Detectar ativos duplicados {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Se um usuário do DAM fizer upload de um ou mais ativos que já existem no repositório, [!DNL Experience Manager] detecta a duplicação e notifica o usuário. A detecção de duplicatas é desativada por padrão, pois pode ter impacto no desempenho dependendo do tamanho do repositório e do número de ativos carregados. Para ativar o recurso, configure [!UICONTROL Detector de duplicação de ativos na nuvem do Adobe AEM]. Consulte [como fazer configurações do OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html). A detecção de duplicação é baseada no `dam:sha1` valor armazenado em `jcr:content/metadata/dam:sha1`. Isso significa que os ativos duplicados são detectados, mesmo se os nomes de arquivo forem diferentes.

Você pode adicionar o arquivo de configuração `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` no código personalizado e o arquivo pode conter o seguinte:

```json
{
  "enabled":true,
  "detectMetadataField":"dam:sha1"
}
```

Depois de habilitado, o Experience Manager envia notificações de ativos duplicados para a Caixa de entrada do Experience Manager. É um resultado agregado para várias duplicatas. Os usuários podem optar por remover os ativos com base nos resultados.

![Notificação da caixa de entrada para ativos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Ao fazer upload de ativos no repositório, o Experience Manager detecta a duplicação e notifica sobre os primeiros 100 ativos duplicados.

## Visualizar ativos {#previewing-assets}

Para visualizar um ativo, siga estas etapas.

1. Na interface do usuário do Assets, navegue até o local do ativo que deseja visualizar.
1. Toque no ativo desejado para abri-lo.

1. No modo de visualização, as opções de zoom estão disponíveis para [tipos de imagem suportados](/help/assets/file-format-support.md) (com edição interativa).

   Para ampliar um ativo, toque/clique `+` (ou toque/clique na lupa do ativo). Para diminuir o zoom, toque/clique `-`. Ao ampliar, você pode observar cuidadosamente qualquer área da imagem ao fazer o panorama. A seta de redefinição do zoom o traz de volta à exibição original.

   Toque **[!UICONTROL Redefinir]** para redefinir a exibição para o tamanho original.

## Editar propriedades {#editing-properties}

1. Navegue até o local do ativo cujos metadados você deseja editar.

1. Selecione o ativo e toque/clique **[!UICONTROL Propriedades]** na barra de ferramentas para exibir as propriedades do ativo. Como alternativa, escolha a **[!UICONTROL Propriedades]** ação rápida no cartão de ativos.

   ![properties_quickaction](assets/properties_quickaction.png)

1. No [!UICONTROL Propriedades] edite as propriedades dos metadados em várias guias. Por exemplo, em **[!UICONTROL Básico]** , edite o título, a descrição e assim por diante.

   >[!NOTE]
   >
   >O layout da [!UICONTROL Propriedades] As propriedades de metadados disponíveis dependem do esquema de metadados subjacente. Para saber como modificar o layout do [!UICONTROL Propriedades] página, consulte [Esquemas de metadados](/help/assets/metadata-schemas.md).

1. Para programar uma data/hora específica para a ativação do ativo, use o seletor de datas ao lado do campo **[!UICONTROL No horário]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Para desativar o ativo após uma duração específica, escolha a data/hora de desativação do seletor de datas ao lado do **[!UICONTROL Hora de desligar]** campo. A data de desativação deve ser posterior à data de ativação de um ativo. Depois que a variável [!UICONTROL Hora de desligar], um ativo e suas representações não estão disponíveis por meio da interface da Web do Assets ou por meio da API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. No **[!UICONTROL Tags]** selecione uma ou mais tags. Para adicionar uma tag personalizada, digite o nome da tag na caixa e selecione o `Enter` chave. A nova tag é salva em [!DNL Experience Manager].

   O YouTube requer Tags para publicar e ter um link para o YouTube (se um link adequado puder ser encontrado).

   >[!NOTE]
   >
   >Para criar tags, você deve ter permissão de gravação em `/content/cq:tags/default` no repositório CRX.

1. Toque/clique **[!UICONTROL Salvar e fechar]**.

1. Navegue até a interface do usuário do Assets. As propriedades de metadados editadas, incluindo título, descrição e tags, são exibidas no cartão de ativo na exibição Cartão e em colunas relevantes na exibição Lista.

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## Copiar ativos {#copying-assets}

Ao copiar um ativo ou uma pasta, todo o ativo ou a pasta é copiada, juntamente com sua estrutura de conteúdo. Um ativo copiado ou uma pasta é duplicado no local de destino. O ativo no local de origem não é alterado.

Alguns atributos exclusivos a uma cópia específica de um ativo não são transportados. Alguns exemplos:

* ID do ativo, data e hora de criação e versões e histórico da versão. Algumas dessas propriedades são indicadas pelas propriedades `jcr:uuid`, `jcr:created`e `cq:name`.

* O tempo de criação e os caminhos referenciados são exclusivos para cada ativo e sua representação.

As outras propriedades e informações de metadados são retidas. Uma cópia parcial não é criada ao copiar um ativo.

1. Na interface do usuário do Assets, selecione um ou mais ativos e toque/clique no botão **[!UICONTROL Copiar]** ícone na barra de ferramentas. Como alternativa, selecione o **[!UICONTROL Copiar]** ![copy_icon](assets/copy_icon.png) ação rápida do cartão de ativos.

   >[!NOTE]
   >
   >Se você usar a variável [!UICONTROL Copiar] ação rápida, você só pode copiar um ativo de cada vez.

1. Navegue até o local onde deseja copiar os ativos.

   >[!NOTE]
   >
   >Se você copiar um ativo no mesmo local, [!DNL Experience Manager] gera automaticamente uma variação do nome. Por exemplo, se você copiar um ativo intitulado `Square`, [!DNL Experience Manager] gera automaticamente o título para sua cópia como `Square1`.

1. Clique no botão **[!UICONTROL Colar]** ícone de ativo na barra de ferramentas. Os ativos são copiados para este local.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >O **[!UICONTROL Colar]** ícone está disponível na barra de ferramentas até que a operação de colar seja concluída.

### Mover ou renomear ativos {#moving-or-renaming-assets}

1. Navegue até o local do ativo que deseja mover.

1. Selecione o ativo e toque/clique no **[!UICONTROL Mover]** ícone ![move_icon](assets/move_icon.png) na barra de ferramentas.

1. No assistente Mover ativos , execute um dos seguintes procedimentos:

   * Especifique o nome do ativo após movê-lo. Em seguida, toque/clique **[!UICONTROL Próximo]** para continuar.

   * Toque/clique **[!UICONTROL Cancelar]** para interromper o processo.
   >[!NOTE]
   >
   >* Você pode especificar o mesmo nome para o ativo se não houver um ativo com esse nome no novo local. No entanto, você deve usar um nome diferente se mover o ativo para um local onde um ativo com o mesmo nome existe. Se você usar o mesmo nome, o sistema gera automaticamente uma variação do nome. Por exemplo, se o ativo tiver o nome Quadrado, o sistema gera o nome Quadrado1 para a cópia.
   >* Ao renomear, o espaço em branco não é permitido no nome do arquivo.


1. No **[!UICONTROL Selecionar destino]** , siga um destes procedimentos:

   * Navegue até o novo local dos ativos e toque/clique em **[!UICONTROL Próximo]** para continuar.

   * Toque/clique **[!UICONTROL Voltar]** para retornar ao **[!UICONTROL Renomear]** tela.

1. Se os ativos que estão sendo movidos tiverem páginas, ativos ou coleções de referência, a variável **[!UICONTROL Ajustar referências]** aparece ao lado da guia **[!UICONTROL Selecionar destino]** guia .

   Siga um destes procedimentos em **[!UICONTROL Ajustar referências]** tela:

   * Especifique as referências a serem ajustadas com base nos novos detalhes e toque/clique **[!UICONTROL Mover]** para continuar.

   * No **[!UICONTROL Ajustar]** selecione/desmarque referências aos ativos.
   * Toque/clique **[!UICONTROL Voltar]** para retornar ao **[!UICONTROL Selecionar destino]** tela.

   * Toque/clique **[!UICONTROL Cancelar]** para interromper a operação de movimentação.

   Se você não atualizar referências, elas continuarão apontando para o caminho anterior do ativo. Se você ajustar as referências, elas serão atualizadas para o novo caminho do ativo.

### Gerenciar representações {#managing-renditions}

1. Você pode adicionar ou remover representações de um ativo, exceto o original. Navegue até o local do ativo para o qual deseja adicionar ou remover representações.

1. Toque/clique no ativo para abrir a página de ativos.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Toque/clique no ícone de Navegação global e selecione **[!UICONTROL Representações]** na lista.

   ![renditions_menu](assets/renditions_menu.png)

1. No **[!UICONTROL Representações]** , exibir a lista de representações geradas para o ativo.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Por padrão, [!DNL Experience Manager Assets] não exibe a representação original do ativo no modo de visualização. Se você for um administrador, poderá usar as sobreposições para configurar [!DNL Assets] para exibir representações originais no modo de visualização.

1. Selecione uma representação para exibir ou excluir a representação.

   **Exclusão de uma representação**

   Selecione uma representação do **[!UICONTROL Representações]** e toque/clique no painel **[!UICONTROL Excluir representação]** ícone na barra de ferramentas. As representações não podem ser excluídas em massa após a conclusão do processamento do ativo. Para ativos individuais, você pode remover as renderizações manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e fazer upload novamente dos ativos excluídos.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Upload de uma nova representação**

   Navegue até a página de detalhes do ativo e toque/clique no ícone **[!UICONTROL Adicionar representação]** na barra de ferramentas para fazer upload de uma nova representação do ativo.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Se você selecionar uma representação no painel **[!UICONTROL Representações]**, a barra de ferramentas alterará o contexto e exibirá somente as ações relevantes para a representação. As opções, como o ícone Fazer upload da representação, não são exibidas. Para exibir essas opções na barra de ferramentas, navegue até a página de detalhes do ativo.

   Você pode configurar as dimensões para a representação que deseja exibir na página de detalhes de um ativo de imagem ou vídeo. Com base nas dimensões especificadas, os Ativos exibem a representação com as dimensões exatas ou mais próximas.

   Para configurar as dimensões de representação de uma imagem no nível de detalhes do ativo, sobreponha o nó `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configure o valor da propriedade largura. Configure o **[!UICONTROL tamanho (Longo) em KB]** da propriedade no lugar da largura para personalizar a representação na página Detalhes do ativo com base no tamanho da imagem. Para personalização baseada em tamanho, a propriedade `preferOriginal` atribui preferência ao original se o tamanho da representação correspondente for maior que o original.

   Da mesma forma, é possível personalizar a imagem da página de Anotação ao sobrepor `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Para configurar dimensões de representação para um ativo de vídeo, navegue até o `videopicker` nó no repositório CRX no local `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sobreponha o nó e edite a propriedade apropriada.

   >[!NOTE]
   >
   >As anotações de vídeo são suportadas somente em navegadores com formatos de vídeo compatíveis com HTML5. Além disso, dependendo do navegador, diferentes formatos de vídeo são compatíveis. No entanto, o formato de vídeo MXF ainda não é compatível com anotações de vídeo.

## Excluir ativos {#delete-assets}

Para resolver ou remover as referências recebidas de outras páginas, atualize as referências relevantes antes de excluir um ativo.

Além disso, desative o botão forçar exclusão usando uma sobreposição para impedir que os usuários excluam ativos referenciados e deixem links quebrados.

1. Vá ao local do(s) ativo(s) que deseja excluir.

1. Selecione o ativo e clique em **[!UICONTROL Excluir]** ![delete_icon](assets/do-not-localize/delete-icon.png) na barra de ferramentas.

1. Na caixa de diálogo de confirmação, clique em:

   * **[!UICONTROL Cancelar]** para interromper a ação
   * **[!UICONTROL Excluir]** para confirmar a ação:

      * Se o ativo não tiver referências, o ativo será excluído.
      * Se o ativo tiver referências, uma mensagem de erro informará que **[!UICONTROL Um ou mais ativos são referenciados]**. Você pode selecionar **[!UICONTROL Forçar exclusão]** ou **[!UICONTROL Cancelar]**.

   >[!NOTE]
   >
   >Você precisa de permissões de exclusão no dam/asset para excluir um ativo. Se você só tiver permissões de modificação, poderá editar os metadados do ativo e adicionar anotações ao ativo. No entanto, não é possível excluir o ativo ou seus metadados.

   >[!NOTE]
   >
   >Para resolver ou remover as referências recebidas de outras páginas, atualize as referências relevantes antes de excluir um ativo. É possível não permitir a exclusão de ativos referenciados, pois isso causa links quebrados. Desative o botão forçar exclusão usando uma sobreposição.

## Baixar ativos {#download-assets}

Consulte [baixar ativos de [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Publicar ou desfazer a publicação de ativos {#publish-assets}

Você pode publicar ativos e pastas contendo ativos da instância de criação para o [!DNL Experience Manager Assets], [!DNL Dynamic Media]e [!DNL Brand Portal]. Você pode publicar ou cancelar a publicação de ativos no nível do ativo ou da pasta, usando **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]** disponível na [!DNL Experience Manager Assets] interface.

Consulte [gerenciar publicação a partir de [!DNL Experience Manager]](/help/assets/manage-publication.md)

<!--

1. Navigate to the location of the asset or the asset folder that you want to publish or that you want to remove from the publish environment (unpublish).

1. Select the asset or the folder to publish or unpublish and select **[!UICONTROL Manage Publication]** ![manage publication option](assets/do-not-localize/globe-publication.png) option from the toolbar. Alternatively, to publish quickly, select the **[!UICONTROL Quick Publish]** option from the toolbar. If the folder you want to publish includes an empty folder, the empty folder is not published.

1. Select the **[!UICONTROL Publish]** or **[!UICONTROL Unpublish]** option as required.

   ![Unpublish action](assets/unpublish_action.png)
   *Figure: Publish and unpublish options and the scheduling option.*

1. Select **[!UICONTROL Now]** to act on the asset right away or select **[!UICONTROL Later]** to schedule the action. Select a date and time if you choose the **[!UICONTROL Later]** option. Click **[!UICONTROL Next]**.

1. When publishing, if an asset references other assets, its references are listed in the wizard. Only those references are displayed, that are either unpublished or modified since last publish. Choose the references that you want to publish.

1. When unpublishing, if an asset references other assets, choose the references that you want to unpublish. Click **[!UICONTROL Unpublish]**. In the confirmation dialog, click **[!UICONTROL Cancel]** to stop the action or click **[!UICONTROL Unpublish]** to confirm that the assets are to be unpublished at the specified date.

Understand the following limitations and tips related to publishing or unpublishing assets or folders:

* The option to [!UICONTROL Manage Publication] is available only to the user accounts that have replication permissions.
* While unpublishing a complex asset, unpublish the asset only. Avoid unpublishing the references because those may be referenced by other published assets.
* Empty folders are not published.
* If you publish an assets that is being processed, only the original content is published. The renditions are missing. Either wait for processing to complete and then publish or re-publish the asset once the processing completes.

-->

## Grupo de usuários fechado {#closed-user-group}

Um grupo de usuários fechado (CUG) é usado para limitar o acesso a pastas específicas de ativos publicadas a partir de [!DNL Experience Manager]. Se você criar um CUG para uma pasta, o acesso a ela (incluindo ativos e subpastas de pastas) será restrito somente a membros ou grupos atribuídos. Para acessar a pasta, eles devem fazer logon usando suas credenciais de segurança.

Os CUGs são uma maneira extra de restringir o acesso aos seus ativos. Você também pode configurar uma página de logon para a pasta .

1. Selecione uma pasta na interface do usuário do Assets e toque/clique no ícone Propriedades na barra de ferramentas para exibir a página de propriedades.
1. No **[!UICONTROL Permissões]** , adicionar membros ou grupos em **[!UICONTROL Grupo de usuários fechado]**.

   ![add_user](assets/add_user.png)

1. Para exibir uma tela de logon quando os usuários acessarem a pasta, selecione o **[!UICONTROL Habilitar]** opção. Em seguida, selecione o caminho para uma página de logon em [!DNL Experience Manager]e salve as alterações.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Se você não especificar o caminho para uma página de logon, [!DNL Experience Manager] exibe a página de logon padrão na instância de publicação.

1. Publique a pasta e tente acessá-la da instância de publicação. Uma tela de logon é exibida.
1. Se você for um membro CUG, informe suas credenciais de segurança. A pasta é exibida após [!DNL Experience Manager] autentica você.

## Pesquisar ativos {#search-assets}

Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte dos criadores, para o gerenciamento robusto de ativos pelos usuários e profissionais de marketing ou para administração por administradores de DAM.

Para pesquisas simples, avançadas e personalizadas para descobrir e usar os ativos mais apropriados, consulte [pesquisar ativos em [!DNL Experience Manager]](/help/assets/search-assets.md).

## Ações rápidas {#quick-actions}

Os ícones de ação rápida estão disponíveis para um único ativo por vez. Dependendo do seu dispositivo, execute as seguintes ações para exibir os ícones de ação rápida:

* Dispositivos de toque: Toque e segure. Por exemplo, em uma iPad, é possível tocar e segurar um ativo para que as ações rápidas sejam exibidas.
* Dispositivos sem toque: Ponteiro do mouse. Por exemplo, em um dispositivo de desktop, a barra de ação rápida é exibida se você passar o ponteiro do mouse sobre a miniatura do ativo.

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then click/tap the **[!UICONTROL Edit]** icon in the toolbar.
    * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, tap/click the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Tap/click the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Tap/click the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## Linha do tempo {#timeline}

A linha do tempo permite visualizar vários eventos de um item selecionado, como fluxos de trabalho ativos de um ativo, comentários/anotações, registros de atividades e versões.

![Classificar entradas de linha do tempo de um ativo](assets/sort_timeline.gif)
*Figura: Classificar entradas de linha do tempo de um ativo*

>[!NOTE]
>
>No [Console Coleções](/help/assets/manage-collections.md#navigate-the-collections-console), o **[!UICONTROL Mostrar tudo]** list fornece opções para exibir comentários e fluxos de trabalho somente. Além disso, a linha do tempo é exibida somente para coleções de nível superior listadas no console. Ele não é exibido se você navegar dentro de qualquer uma das coleções.

>[!NOTE]
>
>A linha do tempo contém vários [opções específicas para fragmentos de conteúdo](content-fragments/content-fragments.md).

## Anotar ativos {#annotating}

Anotações são comentários ou notas explicativas adicionadas a imagens ou vídeos. As anotações oferecem aos profissionais de marketing a capacidade de colaborar e deixar comentários sobre ativos.

As anotações de vídeo são suportadas apenas em navegadores com formatos de vídeo compatíveis com HTML5. Os formatos de vídeo compatíveis com o Assets dependem do navegador. No entanto, o formato de vídeo MXF ainda não é compatível com anotações de vídeo.

>[!NOTE]
>
>Para Fragmentos De Conteúdo, [anotações são criadas no editor de fragmentos](content-fragments/content-fragments.md).

1. Navegue até o local do ativo ao qual deseja adicionar anotações.
1. Toque/clique no botão **[!UICONTROL Anotar]** ícone de um dos seguintes:

   * [Ações rápidas](#quick-actions)
   * Na barra de ferramentas, depois de selecionar o ativo ou navegar até a página de ativos

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Adicione um comentário na caixa **[!UICONTROL Comentário]** na parte inferior da linha do tempo. Como alternativa, marque uma área na imagem e adicione uma anotação na caixa de diálogo **[!UICONTROL Adicionar anotação]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Para um usuário não administrador, as sugestões serão exibidas somente se o usuário tiver permissões de Leitura em `/home` no CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Depois de adicionar a anotação, clique em **[!UICONTROL Adicionar]** para salvá-lo. Uma notificação para a anotação é enviada para Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >É possível adicionar várias anotações antes de salvá-las.

1. Toque/clique **[!UICONTROL Fechar]** para sair do modo Anotar.
1. Para exibir a notificação, faça logon no Assets com as credenciais do Aaron MacDonald e clique no link **[!UICONTROL Notificações]** para exibir a notificação.

   >[!NOTE]
   >
   >As anotações também podem ser adicionadas aos ativos de vídeo. Ao anotar vídeos, o reprodutor pausa para permitir que você anote em um quadro. Para obter detalhes, consulte [gerenciamento de ativos de vídeo](manage-video-assets.md). No entanto, o formato de vídeo MXF ainda não é compatível com anotações de vídeo.

1. Para escolher uma cor diferente para diferenciar os usuários, clique/toque no ícone Perfil e clique/toque em **[!UICONTROL Minhas preferências]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Especifique a cor desejada na caixa **[!UICONTROL Cor da anotação]** e clique/toque em **[!UICONTROL Aceitar]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>Também é possível adicionar anotações a uma coleção. No entanto, se uma coleção contiver coleções secundárias, você poderá adicionar anotações/comentários somente à coleção principal. A opção Anotar não está disponível para coleções secundárias.

### Exibir anotações salvas {#viewing-saved-annotations}

É possível exibir apenas uma anotação por vez.

>[!NOTE]
>
>Se estiver selecionando várias anotações, a anotação mais recente ficará visível na interface do usuário.
>
>A seleção múltipla é suportada apenas para imprimir o ativo anotado como PDF.

1. Para exibir anotações salvas de um ativo, navegue até o local do ativo e abra a página do ativo.

1. Toque/clique no ícone de Navegação global e escolha **[!UICONTROL Linha do tempo]** na lista.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. Na lista **[!UICONTROL Exibir todos]** na linha do tempo, selecione **[!UICONTROL Comentários]** para filtrar os resultados com base em anotações.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Toque/clique em um comentário na **[!UICONTROL Linha do tempo]** painel para exibir a anotação correspondente na imagem.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Toque/clique **[!UICONTROL Excluir]**, para excluir um comentário específico.

### Imprimir anotações {#printing-annotations}

Se um ativo tiver anotações ou tiver sido sujeito a um fluxo de trabalho de revisão, é possível imprimir o ativo junto com anotações e revisar o status como um arquivo PDF para revisão offline.

Você também pode optar por imprimir somente as anotações ou o status da revisão.

>[!NOTE]
>
>É possível selecionar várias anotações ao imprimir o ativo anotado como PDF.

Para imprimir as anotações e o status da revisão, toque/clique no botão **[!UICONTROL Imprimir]** e siga as instruções no assistente. O **[!UICONTROL Imprimir]** aparece na barra de ferramentas somente quando o ativo tem pelo menos um status de anotação ou revisão atribuído a ele.

1. Na interface do usuário do Assets, abra a página de visualização de um ativo.
1. Faça uma das seguintes opções:

   * Para imprimir todas as anotações e o status da revisão, pule a etapa 3 e vá diretamente para a etapa 4.
   * Para imprimir anotações específicas e revisar o status, abra o [linha do tempo](/help/assets/manage-digital-assets.md#timeline) e então vá para a etapa 3.

1. Para imprimir anotações específicas, selecione as anotações na linha do tempo.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Para imprimir somente o status da revisão, selecione-o na linha do tempo.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Toque/clique no botão **[!UICONTROL Imprimir]** ícone na barra de ferramentas.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Na caixa de diálogo Imprimir, escolha a posição em que deseja que o status das anotações/revisões seja exibido no PDF. Por exemplo, se você quiser que as anotações/status sejam impressas na parte superior direita da página que contém a imagem impressa, use a variável **Superior esquerdo** configuração. Ele é selecionado por padrão.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   É possível escolher outras configurações, dependendo da posição em que deseja que as anotações/status apareçam no PDF impresso. Se desejar que as anotações/status apareçam em uma página separada do ativo impresso, escolha **[!UICONTROL Próxima página]**.

1. Clique em **[!UICONTROL Imprimir]**. Dependendo da opção escolhida na etapa 2, o PDF gerado exibirá as anotações/os status na posição especificada. Por exemplo, se optar por imprimir as anotações e o status da revisão usando a configuração **Superior esquerdo**, o resultado será semelhante ao arquivo PDF mostrado aqui.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Baixe ou imprima o PDF usando as opções na parte superior direita.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   Para modificar a aparência do arquivo PDF renderizado, por exemplo, a cor da fonte, o tamanho e o estilo, a cor de fundo dos comentários e status, abra o **[!UICONTROL Configuração do PDF de anotação]** no Configuration Manager e modifique as opções desejadas. Por exemplo, para alterar a cor de exibição do status aprovado, modifique o código de cor no campo correspondente. Para obter informações sobre como alterar a cor da fonte das anotações, consulte [Anotar](/help/assets/manage-digital-assets.md#annotating).

   Retorne ao arquivo PDF renderizado e atualize-o. O PDF atualizado reflete as alterações feitas.

## Controle de versão de ativos {#asset-versioning}

O controle de versão cria um instantâneo de ativos digitais em um ponto específico do tempo. O controle de versão ajuda a restaurar ativos para um estado anterior posteriormente. Por exemplo, se você deseja desfazer uma alteração feita em um ativo, restaure a versão não editada do ativo.

A seguir estão os cenários em que você cria versões:

* Você modifica uma imagem em um aplicativo diferente e faz upload para os Ativos. Uma versão da imagem é criada para que sua imagem original não seja substituída.
* Você edita os metadados de um ativo.
* Você usa [!DNL Experience Manager] aplicativo de desktop para fazer check-out de um ativo existente e salvar as alterações. Uma nova versão é criada sempre que o ativo é salvo.

Você também pode ativar o controle de versão automático por meio de um fluxo de trabalho. Ao criar uma versão para um ativo, os metadados e as representações são salvos junto com a versão. As representações são alternativas renderizadas das mesmas imagens, por exemplo, uma representação PNG de um arquivo JPEG carregado.

A funcionalidade de controle de versão permite fazer o seguinte:

* Crie uma versão de um ativo.
* Exibir a revisão atual de um ativo.
* Restaure o ativo para uma versão anterior.

1. Navegue até o local do ativo para o qual deseja criar uma versão e toque/clique nele para abrir a página de ativos.

1. Toque/clique no ícone de Navegação global e escolha **[!UICONTROL Linha do tempo]** no menu .

   ![linha do tempo](assets/timeline.png)

1. Toque/clique no botão **[!UICONTROL Ações]** (seta) na parte inferior para exibir as ações disponíveis que podem ser executadas no ativo.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Toque/clique **[!UICONTROL Salvar como versão]** para criar uma versão para o ativo.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Adicione um rótulo, um comentário e, em seguida, clique em **[!UICONTROL Criar]** para criar uma versão. Como alternativa, toque/clique **Cancelar** para sair da operação.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Para exibir a nova versão, abra a lista **[!UICONTROL Mostrar tudo]** na linha do tempo da página Detalhes do ativo ou na interface do usuário do Assets e escolha **[!UICONTROL Versões]**. Todas as versões criadas para um ativo são listadas na guia Linha do tempo. Filtre a lista para mostrar Versões ao clicar na seta suspensa e selecionar **[!UICONTROL Versões]** na lista.

   ![version_option](assets/versions_option.png)

1. Selecione uma versão específica para o ativo visualizar ou permitir que ele apareça na interface do usuário do Assets.

   ![select_version](assets/select_version.png)

1. Adicione um rótulo e um comentário para a versão para reverter para a versão específica na interface do usuário do Assets.

   ![save_version](assets/save_version.png)

1. Para gerar uma visualização da versão, toque/clique em **[!UICONTROL Visualizar versão]**.
1. Para exibir essa versão na interface do usuário do Assets, selecione **[!UICONTROL Reverter para esta versão]**.
1. Para comparar duas versões, vá para a página de ativos do ativo e toque/clique na versão a ser comparada com a versão atual.

   ![select_version_to compare](assets/select_version_tocompare.png)

1. Na linha do tempo, selecione a versão que deseja comparar e arraste o controle deslizante para a esquerda para sobrepor essa versão à versão atual e compare.

   ![compare_Versões](assets/compare_versions.png)

### Iniciar um fluxo de trabalho em um ativo {#starting-a-workflow-on-an-asset}

1. Navegue até o local do ativo para o qual deseja iniciar um fluxo de trabalho e toque/clique no ativo para abrir a página de ativo.
1. Toque/clique no ícone de Navegação global e escolha **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![linha do tempo-1](assets/timeline-1.png)

1. Toque/clique no botão **[!UICONTROL Ações]** (seta) ícone na parte inferior para abrir a lista de ações disponíveis para o ativo.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Toque/clique **[!UICONTROL Iniciar fluxo de trabalho]** na lista.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. No **[!UICONTROL Iniciar fluxo de trabalho]** selecione um modelo de fluxo de trabalho na lista.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Opcional) Especifique um título para o fluxo de trabalho, que pode ser usado para fazer referência à instância do fluxo de trabalho.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Toque/clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Prosseguir]** na caixa de diálogo para confirmar. Cada etapa do fluxo de trabalho é exibida na linha do tempo como um evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Coleções {#collections}

Uma coleção é um conjunto ordenado de ativos. Use coleções para compartilhar ativos entre usuários.

* Uma coleção pode incluir ativos de locais diferentes, pois eles contêm apenas referências a esses ativos. Cada coleção mantém a integridade referencial dos ativos.
* Você pode compartilhar coleções com vários usuários com diferentes níveis de privilégio, incluindo edição, visualização e assim por diante.

Para saber detalhes do gerenciamento de Coleção, consulte [gerenciar coleções](/help/assets/manage-collections.md).

## Ocultar ativos expirados ao visualizar ativos no aplicativo de desktop ou no Adobe Asset Link {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] o aplicativo de desktop permite acesso ao repositório DAM do desktop do Windows ou Mac. O Adobe Asset Link permite acesso a ativos no [!DNL Creative Cloud] aplicativos de desktop.

Ao navegar pelos ativos no [!DNL Experience Manager] interface do usuário, os ativos expirados não são exibidos. Para evitar visualizar, pesquisar e buscar ativos expirados ao navegar por ativos do aplicativo de desktop e do Asset Link, os administradores podem fazer a seguinte configuração. A configuração funciona para todos os usuários, independentemente do privilégio de administrador.

Execute o seguinte comando CURL. Garantir o acesso de leitura em `/conf/global/settings/dam/acpapi/` para os usuários que acessam ativos. Usuários que fazem parte de `dam-user` têm a permissão por padrão.

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

Para saber mais, consulte como [navegue pelos ativos do DAM usando o aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) e [como usar o Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).
