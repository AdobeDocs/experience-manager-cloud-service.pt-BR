---
title: Gerenciar ativos digitais
description: Saiba mais sobre vários métodos de edição e gerenciamento de ativos.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 61e3f77b7d503b252a00178cebe654038ac6df83
workflow-type: tm+mt
source-wordcount: '4336'
ht-degree: 12%

---


# Gerenciar ativos {#manage-assets}

Este artigo descreve como gerenciar e editar ativos no Adobe Experience Manager Assets. Para gerenciar fragmentos de conteúdo, consulte [Fragmentos de conteúdo](content-fragments/content-fragments.md) ativos.

## Criar pastas {#creating-folders}

Ao organizar uma coleção de ativos, por exemplo, todas as imagens `Nature`, você pode criar pastas para mantê-las juntas. Você pode usar pastas para categorizar e organizar seus ativos. [!DNL Experience Manager Assets] não requer que você organize ativos em pastas para trabalhar melhor.

>[!NOTE]
>
>* O compartilhamento de uma pasta Assets do tipo `sling:OrderedFolder` não é suportado ao compartilhar com o Marketing Cloud. Se quiser compartilhar uma pasta, não selecione [!UICONTROL Solicitado] ao criar uma pasta.
>* O Experience Manager não permite o uso da palavra `subassets` como o nome de uma pasta. É uma palavra-chave reservada para nós que contêm subativos para ativos compostos


1. Navegue até o local na pasta de ativos digitais onde deseja criar uma nova pasta. No menu, clique em **[!UICONTROL Criar]**. Selecione **[!UICONTROL Nova pasta]**.
1. No campo **[!UICONTROL Title]**, forneça um nome de pasta. Por padrão, o DAM usa o título fornecido como o nome da pasta. Depois que a pasta for criada, você poderá substituir o padrão e especificar outro nome de pasta.
1. Clique em **[!UICONTROL Criar]**. Sua pasta é exibida na pasta de ativos digitais.

Os seguintes caracteres (lista separada por espaços de) não são suportados:

* Um nome de arquivo de ativo não pode conter nenhum destes caracteres: `* / : [ \\ ] | # % { } ? &`
* O nome da pasta de ativos não pode conter nenhum destes caracteres: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carregar ativos {#uploading-assets}

Consulte [adicionar ativos digitais a Experience Manager](add-assets.md).

## Detectar ativos de duplicado {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Se um usuário do DAM fizer upload de um ou mais ativos que já existem no repositório, [!DNL Experience Manager] detectará a duplicação e notificará o usuário. A detecção de duplicados é desativada por padrão, pois pode ter impacto no desempenho dependendo do tamanho do repositório e do número de ativos carregados. Para habilitar o recurso, configure [!UICONTROL AEM Detector de Duplicação de Ativos da Nuvem]. Consulte [como fazer configurações OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html). A detecção de duplicação é baseada no valor exclusivo `dam:sha1` armazenado em `jcr:content/metadata/dam:sha1`. Isso significa que os ativos do duplicado são detectados mesmo se os nomes dos arquivos forem diferentes.

![Detectar a configuração OSGi do ativo do duplicado](assets/duplicate-detection.png)

Você pode adicionar o arquivo de configuração `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` no código personalizado e o arquivo pode conter o seguinte:

```json
{
  "enabled":true,
  "detectMetadataField":"dam:sha1"
}
```

Depois de habilitado, o Experience Manager envia notificações de ativos do duplicado para a caixa de entrada. É um resultado agregado para vários duplicados. Os usuários podem optar por remover os ativos com base nos resultados.

![Notificação de caixa de entrada para ativos de duplicado](assets/duplicate-detect-inbox-notification.png)

## ativos de pré-visualização {#previewing-assets}

Para pré-visualização de um ativo, siga estas etapas.

1. Na interface do usuário Ativos, navegue até o local do ativo que deseja pré-visualização.
1. Toque no ativo desejado para abri-lo.

1. No modo de pré-visualização, as opções de zoom estão disponíveis para [tipos de imagem suportados](/help/assets/file-format-support.md) (com edição interativa).

   Para aplicar zoom em um ativo, toque/clique em `+` (ou toque/clique na lupa do ativo). Para diminuir o zoom, toque/clique em `-`. Ao ampliar, você pode observar cuidadosamente qualquer área da imagem ao deslocar o panorama. A seta de redefinição de zoom leva você de volta à visualização original.

   Toque em **[!UICONTROL Redefinir]** para redefinir a visualização para o tamanho original.

## Editar propriedades {#editing-properties}

1. Navegue até o local do ativo cujos metadados você deseja editar.

1. Selecione o ativo e toque/clique em **[!UICONTROL Propriedades]** na barra de ferramentas para visualização das propriedades do ativo. Como alternativa, escolha a ação rápida **[!UICONTROL Propriedades]** no cartão de ativos.

   ![properties_quickaction](assets/properties_quickaction.png)

1. Na página [!UICONTROL Propriedades], edite as propriedades de metadados em várias guias. Por exemplo, na guia **[!UICONTROL Basic]**, edite o título, a descrição e assim por diante.

   >[!NOTE]
   >
   >O layout da página [!UICONTROL Propriedades] e as propriedades de metadados disponíveis dependem do schema de metadados subjacente. Para saber como modificar o layout da página [!UICONTROL Propriedades], consulte [Schemas de metadados](/help/assets/metadata-schemas.md).

1. Para programar uma data/hora específica para a ativação do ativo, use o seletor de datas ao lado do campo **[!UICONTROL No horário]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Para desativar o ativo após uma duração específica, escolha a data/hora de desativação no seletor de datas ao lado do campo **[!UICONTROL Tempo de desligamento]**. A data de desativação deve ser posterior à data de ativação de um ativo. Depois do [!UICONTROL Tempo desligado], um ativo e suas representações não estão disponíveis por meio da interface da Web Ativos ou por meio da API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. No campo **[!UICONTROL Tags]**, selecione uma ou mais tags. Para adicionar uma tag personalizada, digite o nome da tag na caixa e selecione a tecla `Enter`. A nova tag é salva em [!DNL Experience Manager].

   O YouTube requer Tags para publicar e ter um link para o YouTube (se for possível encontrar um link adequado).

   >[!NOTE]
   >
   >Para criar tags, é necessário ter permissão de gravação no caminho `/content/cq:tags/default` no repositório CRX.

1. Toque/clique em **[!UICONTROL Salvar e fechar]**.

1. Navegue até a interface do usuário Ativos. As propriedades de metadados editadas, incluindo título, descrição e tags, são exibidas no cartão de ativos na visualização do cartão e em colunas relevantes na visualização da Lista.

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Asset Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## Copiar ativos {#copying-assets}

Quando você copia um ativo ou uma pasta, o ativo inteiro ou a pasta é copiado, juntamente com sua estrutura de conteúdo. Um ativo copiado ou uma pasta é duplicado no local do público alvo. O ativo no local de origem não é alterado.

Alguns atributos exclusivos a uma cópia específica de um ativo não são transmitidos. Alguns exemplos são:

* ID do ativo, data e hora de criação e versões e histórico de versões. Algumas dessas propriedades são indicadas pelas propriedades `jcr:uuid`, `jcr:created` e `cq:name`.

* O tempo de criação e os caminhos referenciados são exclusivos para cada ativo e cada uma de suas execuções.

As outras propriedades e informações de metadados são mantidas. Uma cópia parcial não é criada ao copiar um ativo.

1. Na interface do usuário do Assets, selecione um ou mais ativos e toque/clique no ícone **[!UICONTROL Copiar]** na barra de ferramentas. Como alternativa, selecione a ação rápida **[!UICONTROL Copy]** ![copy_icon](assets/copy_icon.png) do cartão de ativos.

   >[!NOTE]
   >
   >Se você usar a ação rápida [!UICONTROL Copiar], poderá copiar apenas um ativo por vez.

1. Navegue até o local onde deseja copiar os ativos.

   >[!NOTE]
   >
   >Se você copiar um ativo no mesmo local, [!DNL Experience Manager] gera automaticamente uma variação do nome. Por exemplo, se você copiar um ativo chamado `Square`, [!DNL Experience Manager] gera automaticamente o título para sua cópia como `Square1`.

1. Clique no ícone de ativo **[!UICONTROL Colar]** na barra de ferramentas. Os ativos são copiados para este local.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >O ícone **[!UICONTROL Colar]** está disponível na barra de ferramentas até que a operação de colagem seja concluída.

### Mover ou renomear ativos {#moving-or-renaming-assets}

1. Navegue até o local do ativo que deseja mover.

1. Selecione o ativo e toque/clique no ícone **[!UICONTROL Mover]** ![move_icon](assets/move_icon.png) da barra de ferramentas.

1. No assistente de Ativos de Movimentação, execute um dos procedimentos a seguir:

   * Especifique o nome do ativo depois de movê-lo. Em seguida, toque/clique em **[!UICONTROL Próximo]** para continuar.

   * Toque/clique em **[!UICONTROL Cancelar]** para parar o processo.
   >[!NOTE]
   >
   >* Você pode especificar o mesmo nome para o ativo se não houver um ativo com esse nome no novo local. No entanto, você deve usar um nome diferente se mover o ativo para um local onde um ativo com o mesmo nome exista. Se você usar o mesmo nome, o sistema gera automaticamente uma variação do nome. Por exemplo, se seu ativo tiver o nome Quadrado, o sistema gera o nome Quadrado1 para sua cópia.
   >* Ao renomear, o espaço em branco não é permitido no nome do arquivo.


1. Na caixa de diálogo **[!UICONTROL Selecionar destino]**, siga um destes procedimentos:

   * Navegue até o novo local dos ativos e toque/clique em **[!UICONTROL Próximo]** para prosseguir.

   * Toque/clique em **[!UICONTROL Voltar]** para retornar à tela **[!UICONTROL Renomear]**.

1. Se os ativos que estão sendo movidos tiverem páginas, ativos ou coleções de referência, a guia **[!UICONTROL Ajustar referências]** aparecerá ao lado da guia **[!UICONTROL Selecionar destino]**.

   Execute um dos procedimentos a seguir na tela **[!UICONTROL Ajustar referências]**:

   * Especifique as referências a serem ajustadas com base nos novos detalhes e toque/clique em **[!UICONTROL Mover]** para continuar.

   * Na coluna **[!UICONTROL Ajustar]**, selecione/cancele a seleção das referências aos ativos.
   * Toque/clique em **[!UICONTROL Voltar]** para retornar à tela **[!UICONTROL Selecionar destino]**.

   * Toque/clique em **[!UICONTROL Cancelar]** para parar a operação de movimentação.

   Se você não atualizar referências, elas continuarão apontando para o caminho anterior do ativo. Se você ajustar as referências, elas serão atualizadas para o novo caminho do ativo.

### Gerenciar execuções {#managing-renditions}

1. Você pode adicionar ou remover representações de um ativo, exceto o original. Navegue até o local do ativo para o qual você deseja adicionar ou remover representações.

1. Toque/clique no ativo para abrir sua página de ativos.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Toque/clique no ícone GlobalNav e selecione **[!UICONTROL Representações]** na lista.

   ![renditions_menu](assets/renditions_menu.png)

1. No painel **[!UICONTROL Representações]**, visualização a lista de representações geradas para o ativo.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Por padrão, [!DNL Experience Manager Assets] não exibe a representação original do ativo no modo de pré-visualização. Se você for um administrador, poderá usar sobreposições para configurar [!DNL Assets] para exibir as representações originais no modo de pré-visualização.

1. Selecione uma representação para visualização ou exclua a representação.

   **Excluindo uma representação**

   Selecione uma representação no painel **[!UICONTROL Representações]** e toque/clique no ícone **[!UICONTROL Excluir representação]** da barra de ferramentas. As execuções não podem ser excluídas em massa após a conclusão do processamento do ativo. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir execuções específicas ou excluir os ativos e fazer upload novamente dos ativos excluídos.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Carregar uma nova execução**

   Navegue até a página de detalhes do ativo e toque/clique no ícone **[!UICONTROL Adicionar representação]** na barra de ferramentas para fazer upload de uma nova representação do ativo.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Se você selecionar uma representação no painel **[!UICONTROL Representações]**, a barra de ferramentas alterará o contexto e exibirá somente as ações relevantes para a representação. As opções, como o ícone Fazer upload da representação, não são exibidas. Para exibir essas opções na barra de ferramentas, navegue até a página de detalhes do ativo.

   Você pode configurar as dimensões para a representação que deseja exibir na página de detalhes de um ativo de imagem ou vídeo. Com base nas dimensões especificadas, os Ativos exibem a representação com as dimensões exatas ou mais próximas.

   Para configurar as dimensões de representação de uma imagem no nível de detalhes do ativo, sobreponha o nó `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configure o valor da propriedade largura. Configure o **[!UICONTROL tamanho (Longo) em KB]** da propriedade no lugar da largura para personalizar a representação na página Detalhes do ativo com base no tamanho da imagem. Para personalização baseada em tamanho, a propriedade `preferOriginal` atribui preferência ao original se o tamanho da representação correspondente for maior que o original.

   Da mesma forma, você pode personalizar a imagem da página Anotar sobrepondo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Para configurar dimensões de representação para um ativo de vídeo, navegue até o nó `videopicker` no repositório CRX no local `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sobreponha o nó e edite a propriedade apropriada.

   >[!NOTE]
   >
   >As anotações em vídeo são compatíveis apenas em navegadores com formatos de vídeo compatíveis com HTML5. Além disso, dependendo do navegador, diferentes formatos de vídeo são suportados.

## Excluir ativos {#delete-assets}

Para resolver ou remover as referências recebidas de outras páginas, atualize as referências relevantes antes de excluir um ativo.

Além disso, desative o botão forçar exclusão usando uma sobreposição para impedir que os usuários excluam ativos referenciados e deixem links quebrados.

1. Vá ao local do(s) ativo(s) que deseja excluir.

1. Selecione o ativo e toque/clique no ícone **[!UICONTROL Excluir]** na barra de ferramentas.

   ![delete_icon](assets/delete_icon.png)

1. Na caixa de diálogo de confirmação, clique em:

   * **** Cancelar para interromper a ação
   * **[!UICONTROL Excluir]** para confirmar a ação:

      * Se o ativo não tiver referências, ele será excluído.
      * Se o ativo tiver referências, uma mensagem de erro informará que **Um ou mais ativos são referenciados.** Você pode selecionar **[!UICONTROL Forçar exclusão]** ou **[!UICONTROL Cancelar]**.

   >[!NOTE]
   >
   >Você precisa de permissões de exclusão no dam/asset para poder excluir um ativo. Se você tiver apenas permissões de modificação, poderá apenas editar os metadados do ativo e adicionar anotações ao ativo. No entanto, não é possível excluir o ativo ou seus metadados.

   >[!NOTE]
   >
   >Para resolver ou remover as referências recebidas de outras páginas, atualize as referências relevantes antes de excluir um ativo.
   >
   >
   >Além disso, desative o botão forçar exclusão usando uma sobreposição para impedir que os usuários excluam ativos referenciados e deixem links quebrados.

## Baixar ativos {#download-assets}

Consulte [Baixar ativos de [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Publicar ativos {#publish-assets}

<!--
>[!NOTE]
>
>For more information specific to Dynamic Media, see [Publishing Dynamic Media Assets.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
-->

1. Navegue até o local dos ativos/pastas que deseja publicar.

1. Selecione a ação rápida **[!UICONTROL Publicar]** no cartão de ativos ou selecione o ativo e toque/clique no ícone **[!UICONTROL Publicação rápida]** na barra de ferramentas.
1. Se o ativo fizer referência a outros ativos, suas referências serão listadas no assistente. Somente as referências que não foram publicadas ou modificadas desde a última vez que foram publicadas/não foram publicadas são exibidas. Escolha as referências que deseja publicar.

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Se a pasta que você deseja publicar incluir uma pasta vazia, a pasta vazia não será publicada.

1. Toque/clique em **[!UICONTROL Publicar]** para confirmar a ativação dos ativos.

>[!CAUTION]
>
>Se você publicar um ativo que está sendo processado, somente o conteúdo original será publicado. As execuções estão faltando. Aguarde a conclusão do processamento e publique ou republique o ativo quando o processamento for concluído.

## Cancelar a publicação de ativos {#unpublishing-assets}

1. Navegue até o local da pasta de ativos/ativos que deseja remover do ambiente de publicação (cancelar publicação).

1. Selecione o ativo/pasta para cancelar a publicação e toque/clique no ícone **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![manage_publication](assets/manage_publication.png)

1. Selecione a ação **[!UICONTROL Cancelar a publicação]** da lista.

   ![unpublish_action](assets/unpublish_action.png)

1. Para cancelar a publicação do ativo mais tarde, selecione **[!UICONTROL Cancelar a publicação mais tarde]** e selecione uma data para cancelar a publicação do ativo.
1. Agende uma data para o ativo ficar indisponível a partir do ambiente de publicação.
1. Se o ativo fizer referência a outros ativos, escolha as referências que deseja cancelar a publicação. Toque/clique em **[!UICONTROL Cancelar a publicação]**.
1. Na caixa de diálogo de confirmação, toque/clique em:

   * **** Cancelar para interromper a ação
   * **[!UICONTROL Cancele a]** publicação para confirmar que os ativos não foram publicados (não estão mais disponíveis no ambiente de publicação) na data especificada.

   >[!NOTE]
   >
   >Ao cancelar a publicação de um ativo complexo, cancele a publicação somente do ativo. Evite cancelar a publicação das referências, pois elas podem ser referenciadas por outros ativos publicados.

## Grupo de usuários fechado {#closed-user-group}

Um grupo de usuários fechado (CUG) é usado para limitar o acesso a pastas de ativos específicas publicadas de [!DNL Experience Manager]. Se você criar um CUG para uma pasta, o acesso à pasta (incluindo os ativos e as subpastas da pasta) será restrito somente aos membros ou grupos atribuídos. Para acessar a pasta, eles devem fazer logon usando suas credenciais de segurança.

Os CUGs são uma maneira extra de restringir o acesso aos seus ativos. Você também pode configurar uma página de logon para a pasta.

1. Selecione uma pasta na interface do usuário do Assets e toque/clique no ícone Propriedades na barra de ferramentas para exibir a página de propriedades.
1. Na guia **[!UICONTROL Permissões]**, adicione membros ou grupos em **[!UICONTROL Grupo de usuários fechado]**.

   ![add_user](assets/add_user.png)

1. Para exibir uma tela de logon quando os usuários acessarem a pasta, selecione a opção **[!UICONTROL Ativar]**. Em seguida, selecione o caminho para uma página de logon em [!DNL Experience Manager] e salve as alterações.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Se você não especificar o caminho para uma página de logon, [!DNL Experience Manager] exibirá a página de logon padrão na instância de publicação.

1. Publique a pasta e tente acessá-la da instância de publicação. Uma tela de login é exibida.
1. Se você for um membro do CUG, insira suas credenciais de segurança. A pasta é exibida depois que [!DNL Experience Manager] o autentica.

## Pesquisar ativos {#search-assets}

Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte de profissionais de criação, para o gerenciamento robusto de ativos por parte de usuários e comerciantes, ou para administração por administradores de DAM.

Para pesquisas simples, avançadas e personalizadas para descobrir e usar os ativos mais apropriados, consulte [ativos de pesquisa em [!DNL Experience Manager]](/help/assets/search-assets.md).

## Ações rápidas {#quick-actions}

Os ícones de ação rápida estão disponíveis para um único ativo por vez. Dependendo do seu dispositivo, execute as seguintes ações para exibir os ícones de ação rápida:

* Dispositivos de toque: Toque e segure. Por exemplo, em um iPad, é possível tocar e segurar um ativo para que as ações rápidas sejam exibidas.
* Dispositivos não sensíveis ao toque: Passe o ponteiro do mouse. Por exemplo, em um dispositivo de desktop, a barra de ação rápida é exibida se você passar o ponteiro do mouse sobre a miniatura do ativo.

## Editar imagens {#editing-images}

As ferramentas de edição na interface [!DNL Experience Manager Assets] permitem executar pequenos trabalhos de edição em ativos de imagem. É possível recortar, girar, virar e executar outras tarefas de edição em imagens. Também é possível adicionar mapas de imagem a ativos.

>[!NOTE]
>
>Para alguns componentes, o modo Tela cheia tem opções adicionais disponíveis.

1. Execute um dos procedimentos a seguir para abrir um ativo no modo de edição:

   * Selecione o ativo e clique/toque no ícone **[!UICONTROL Editar]** na barra de ferramentas.
   * Toque/clique no ícone **[!UICONTROL Editar]** que aparece em um ativo na visualização de cartão.
   * Na página de ativos, toque/clique no ícone **[!UICONTROL Editar]** na barra de ferramentas.

   ![edit_icon](assets/edit_icon.png)

1. Para recortar a imagem, toque/clique no ícone **Recortar**.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Selecione a opção desejada na lista. A área de corte aparece na imagem com base na opção escolhida. A opção **Mão livre** permite cortar a imagem sem restrições de proporção.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Selecione a área a ser cortada e redimensione ou reposicione-a na imagem.
1. Use o ícone **Concluir** (canto superior direito) para cortar a imagem. Clicar no ícone **Concluir** também aciona a regeneração de execuções.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use os ícones **Desfazer** e **Refazer** na parte superior direita para reverter para a imagem não cortada ou manter a imagem cortada, respectivamente.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Toque/clique no ícone Girar apropriado para girar a imagem no sentido horário ou anti-horário.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Toque/clique no ícone Virar apropriado para virar a imagem na horizontal ou na vertical.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Toque/clique no ícone **Concluir** para salvar as alterações.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>A edição de imagens é compatível com os formatos de arquivos BMP, GIF, PNG e JPEG.

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>Para editar um arquivo TXT, defina **Externalizador de links Day CQ** do Configuration Manager.

## Linha do tempo {#timeline}

A linha do tempo permite que você visualização vários eventos para um item selecionado, como workflows ativos para um ativo, comentários/anotações, registros de atividades e versões.

![Classificar entradas de linha do tempo de um ](assets/sort_timeline.gif)
*assetFigura: Classificar entradas de linha do tempo de um ativo*

>[!NOTE]
>
>No console [Coleções](/help/assets/manage-collections.md#navigate-the-collections-console), a lista **[!UICONTROL Mostrar tudo]** fornece opções para visualização somente de comentários e workflows. Além disso, a linha do tempo é exibida somente para coleções de nível superior listadas no console. Ela não será exibida se você navegar dentro de qualquer uma das coleções.

>[!NOTE]
>
>A linha do tempo contém várias [opções específicas para fragmentos de conteúdo](content-fragments/content-fragments.md).

## Anotar {#annotating}

Anotações são comentários ou notas explicativas adicionadas a imagens ou vídeos. As anotações fornecem aos comerciantes a capacidade de colaborar e deixar feedback sobre os ativos.

As anotações de vídeo são compatíveis apenas em navegadores com formatos de vídeo compatíveis com HTML5. Os formatos de vídeo compatíveis com o Assets dependem do navegador.

>[!NOTE]
>
>Para Fragmentos de conteúdo, as anotações [são criadas no editor de fragmentos](content-fragments/content-fragments.md).

1. Navegue até o local do ativo ao qual você deseja adicionar anotações.
1. Toque/clique no ícone **[!UICONTROL Anotar]** de um dos seguintes:

   * [Ações rápidas](#quick-actions)
   * Na barra de ferramentas depois de selecionar o ativo ou navegar até a página do ativo

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Adicione um comentário na caixa **[!UICONTROL Comentário]** na parte inferior da linha do tempo. Como alternativa, marque uma área na imagem e adicione uma anotação na caixa de diálogo **[!UICONTROL Adicionar anotação]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Para um usuário que não seja administrador, as sugestões serão exibidas somente se o usuário tiver permissões de Leitura em `/home` no CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Depois de adicionar a anotação, clique em **[!UICONTROL Adicionar]** para salvá-la. Uma notificação para a anotação é enviada para Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >É possível adicionar várias anotações antes de salvá-las.

1. Toque/clique em **[!UICONTROL Fechar]** para sair do modo Anotar.
1. Para visualização da notificação, faça logon nos Ativos com as credenciais do Aaron MacDonald e clique no ícone **[!UICONTROL Notificações]** para visualização da notificação.

   >[!NOTE]
   >
   >As anotações também podem ser adicionadas aos ativos de vídeo. Ao anotar vídeos, o player pausa para permitir que você anote em um quadro. Para obter detalhes, consulte [gerenciar ativos de vídeo](manage-video-assets.md).

1. Para escolher uma cor diferente para diferenciar os usuários, clique/toque no ícone de Perfil e clique/toque em **[!UICONTROL Minhas preferências]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Especifique a cor desejada na caixa **[!UICONTROL Cor da anotação]** e clique/toque em **[!UICONTROL Aceitar]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>Também é possível adicionar anotações a uma coleção. No entanto, se uma coleção contiver coleções-filho, você poderá adicionar anotações/comentários somente à coleção-pai. A opção Anotar não está disponível para coleções filhas.

### Visualização de anotações salvas {#viewing-saved-annotations}

1. Para visualização de anotações salvas para um ativo, navegue até o local do ativo e abra a página do ativo para o ativo.

1. Toque/clique no ícone GlobalNav e escolha **[!UICONTROL Linha do tempo]** na lista.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. Na lista **[!UICONTROL Exibir todos]** na linha do tempo, selecione **[!UICONTROL Comentários]** para filtrar os resultados com base em anotações.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Toque/clique em um comentário no painel **[!UICONTROL Linha do tempo]** para visualização da anotação correspondente na imagem.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Toque/clique em **[!UICONTROL Excluir]** para excluir um comentário específico.

### Imprimir anotações {#printing-annotations}

Se um ativo tiver anotações ou tiver sido submetido a um fluxo de trabalho de revisão, você poderá imprimir o ativo junto com anotações e revisar o status como um arquivo PDF para revisão offline.

Você também pode imprimir somente as anotações ou o status da revisão.

Para imprimir as anotações e revisar o status, toque/clique no ícone **[!UICONTROL Imprimir]** e siga as instruções do assistente. O ícone **[!UICONTROL Imprimir]** aparece na barra de ferramentas somente quando o ativo tem pelo menos um status de anotação ou revisão atribuído a ele.

1. Na interface do usuário Ativos, abra a página pré-visualização de um ativo.
1. Faça uma das seguintes opções:

   * Para imprimir todas as anotações e o status da revisão, pule a etapa 3 e vá diretamente para a etapa 4.
   * Para imprimir anotações específicas e revisar o status, abra a [linha do tempo](/help/assets/manage-digital-assets.md#timeline) e vá para a etapa 3.

1. Para imprimir anotações específicas, selecione as anotações na linha do tempo.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Para imprimir somente o status da revisão, selecione-o na linha do tempo.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Toque/clique no ícone **[!UICONTROL Imprimir]** na barra de ferramentas.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Na caixa de diálogo Imprimir, escolha a posição em que deseja que o status de anotações/revisão seja exibido no PDF. Por exemplo, se desejar que as anotações/status sejam impressas na parte superior direita da página que contém a imagem impressa, use a configuração **Parte superior esquerda**. Está selecionado por padrão.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   É possível escolher outras configurações, dependendo da posição em que deseja que as anotações/status apareçam no PDF impresso. Se desejar que as anotações/status apareçam em uma página separada do ativo impresso, escolha **[!UICONTROL Próxima página]**.

1. Clique em **[!UICONTROL Imprimir]**. Dependendo da opção escolhida na etapa 2, o PDF gerado exibirá as anotações/os status na posição especificada. Por exemplo, se optar por imprimir as anotações e o status da revisão usando a configuração **Superior esquerdo**, o resultado será semelhante ao arquivo PDF mostrado aqui.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Baixe ou imprima o PDF usando as opções na parte superior direita.

   ![chlimage_1-248](assets/chlimage_1-247.png)

   Para modificar a aparência do arquivo PDF renderizado, por exemplo, a cor, o tamanho e o estilo da fonte, a cor de plano de fundo dos comentários e status, abra a **[!UICONTROL Configuração do PDF de anotação]** no Configuration Manager e modifique as opções desejadas. Por exemplo, para alterar a cor de exibição do status aprovado, modifique o código de cor no campo correspondente. Para obter informações sobre como alterar a cor da fonte das anotações, consulte [Anotar](/help/assets/manage-digital-assets.md#annotating).

   ![chlimage_1-247](assets/chlimage_1-248.png)

   Retorne ao arquivo PDF renderizado e atualize-o. O PDF atualizado reflete as alterações feitas.

## Controle de versão do ativo {#asset-versioning}

O controle de versão cria um instantâneo de ativos digitais em um ponto específico do tempo. O controle de versão ajuda a restaurar ativos para um estado anterior posteriormente. Por exemplo, se você deseja desfazer uma alteração feita em um ativo, restaure a versão não editada do ativo.

A seguir estão os cenários nos quais você cria versões:

* Você modifica uma imagem em um aplicativo diferente e faz upload para Ativos. Uma versão da imagem é criada para que sua imagem original não seja substituída.
* Edite os metadados de um ativo.
* Use [!DNL Experience Manager] aplicativo desktop para fazer check-out de um ativo existente e salvar suas alterações. Uma nova versão é criada sempre que o ativo é salvo.

Você também pode ativar o controle automático de versão por meio de um fluxo de trabalho. Quando você cria uma versão para um ativo, os metadados e as execuções são salvos junto com a versão. As execuções são alternativas renderizadas das mesmas imagens, por exemplo, uma execução PNG de um arquivo JPEG carregado.

A funcionalidade de controle de versão permite fazer o seguinte:

* Criar uma versão de um ativo.
* Visualização da revisão atual de um ativo.
* Restaure o ativo para uma versão anterior.

1. Navegue até o local do ativo para o qual deseja criar uma versão e toque/clique nele para abrir sua página de ativo.

1. Toque/clique no ícone GlobalNav e escolha **[!UICONTROL Linha do tempo]** no menu.

   ![linha do tempo](assets/timeline.png)

1. Toque/clique no ícone **[!UICONTROL Ações]** (seta) na parte inferior para visualização das ações disponíveis que você pode executar no ativo.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Toque/clique em **[!UICONTROL Salvar como versão]** para criar uma versão para o ativo.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Adicione um rótulo e um comentário e clique em **[!UICONTROL Criar]** para criar uma versão. Como alternativa, toque/clique em **Cancelar** para sair da operação.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Para exibir a nova versão, abra a lista **[!UICONTROL Mostrar tudo]** na linha do tempo da página Detalhes do ativo ou na interface do usuário do Assets e escolha **[!UICONTROL Versões]**. Todas as versões criadas para um ativo são listadas na guia Linha do tempo. Filtre a lista para mostrar Versões ao clicar na seta suspensa e selecionar **[!UICONTROL Versões]** na lista.

   ![version_option](assets/versions_option.png)

1. Selecione uma versão específica para o ativo a ser pré-visualização ou permita que ele apareça na interface do usuário do Assets.

   ![select_version](assets/select_version.png)

1. Adicione um rótulo e um comentário para a versão para reverter para a versão específica na interface do usuário do Assets.

   ![save_version](assets/save_version.png)

1. Para gerar uma visualização da versão, toque/clique em **[!UICONTROL Visualizar versão]**.
1. Para exibir essa versão na interface do usuário do Assets, selecione **[!UICONTROL Reverter para esta versão]**.
1. Para comparar entre duas versões, vá para a página de ativos do ativo e toque/clique na versão a ser comparada com a versão atual.

   ![select_version_to-compare](assets/select_version_tocompare.png)

1. Na linha do tempo, selecione a versão que deseja comparar e arraste o controle deslizante para a esquerda para sobrepor essa versão à versão atual e compare.

   ![compare_Versões](assets/compare_versions.png)

### Iniciar um fluxo de trabalho em um ativo {#starting-a-workflow-on-an-asset}

1. Navegue até o local do ativo para o qual você deseja start um fluxo de trabalho e toque/clique no ativo para abrir a página do ativo.
1. Toque/clique no ícone GlobalNav e escolha **[!UICONTROL Linha do tempo]** no menu para exibir a linha do tempo.

   ![linha do tempo 1](assets/timeline-1.png)

1. Toque/clique no ícone **[!UICONTROL Ações]** (seta) na parte inferior para abrir a lista de ações disponíveis para o ativo.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Toque/clique em **[!UICONTROL Fluxo de trabalho do Start]** na lista.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. Na caixa de diálogo **[!UICONTROL Fluxo de trabalho do Start]**, selecione um modelo de fluxo de trabalho na lista.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Opcional) Especifique um título para o fluxo de trabalho, que pode ser usado para fazer referência à instância do fluxo de trabalho.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Toque/clique em **[!UICONTROL Iniciar]** e em **[!UICONTROL Prosseguir]** na caixa de diálogo para confirmar. Cada etapa do fluxo de trabalho é exibida na linha do tempo como um evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Coleções {#collections}

Uma coleção é um conjunto ordenado de ativos. Use coleções para compartilhar ativos entre usuários.

* Uma coleção pode incluir ativos de diferentes locais, pois eles só contêm referências a esses ativos. Cada coleção mantém a integridade referencial dos ativos.
* Você pode compartilhar coleções com vários usuários com diferentes níveis de privilégio, incluindo edição, visualização e assim por diante.

Consulte [Gerenciar coleções](/help/assets/manage-collections.md) para obter detalhes sobre o gerenciamento de coleções.
