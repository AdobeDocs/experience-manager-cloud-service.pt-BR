---
title: Perfis de metadados
description: Saiba mais sobre perfis de metadados para ativos. Saiba como criar um perfil de metadados e aplicá-lo aos ativos da pasta.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 23%

---


# Perfis de metadados {#metadata-profiles}

Um Perfil de Metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um Perfil de Metadados e aplique-o a uma pasta. Qualquer ativo carregado posteriormente para a pasta herda os metadados padrão configurados no Perfil Metadados.

<!-- See [Profiles for Processing Metadata, Images, and Videos](processing-profiles.md).

See also [Best Practices for Organizing your Digital Assets for using Processing Profiles](/help/assets/best-practices-for-file-management.md).

-->

## Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis]** de metadados e, em seguida, toque em **[!UICONTROL Criar]**.
1. Digite um título para o Perfil de Metadados, por exemplo Metadados de amostra, e toque em **[!UICONTROL Enviar]**. O formulário Editar para o Perfil de Metadados é exibido.
1. Clique em um componente e configure suas propriedades na guia **[!UICONTROL Configurações]** . Por exemplo, clique no componente **[!UICONTROL Descrição]** e edite suas propriedades.
Edite as seguintes propriedades para o componente **[!UICONTROL Descrição]** :

   * **[!UICONTROL Rótulo]** do campo - o nome de exibição da propriedade de metadados. É apenas para a referência do usuário.
   * **[!UICONTROL Mapear para propriedade]** - o valor dessa propriedade fornece o caminho/nome relativo para o nó do ativo no qual ele é salvo no repositório. O valor deve sempre ser start `./` porque indica que o caminho está sob o nó do ativo.

      The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Por exemplo, se você especificar . `/jcr:content/metadata/dc:desc` como o nome do **[!UICONTROL Mapa para a propriedade]**, os ativos AEM armazenam o valor `dc:desc` no nó de metadados do ativo.

   * **[!UICONTROL Valor]** padrão - Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

      >[!NOTE]
      >
      >Adicionando um valor padrão a uma nova propriedade de metadados (que ainda não existe no . `/jcr:content/metadata` nó) não exibe a propriedade e seu valor na página Propriedades do ativo por padrão. Para visualização da nova propriedade na página Propriedades dos ativos, modifique o formulário de schema correspondente.

1. (Opcional) Adicione mais componentes ao Formulário de edição na guia **[!UICONTROL Criar formulário]** e configure as propriedades na guia **[!UICONTROL Configurações]**. As seguintes propriedades estão disponíveis na guia **[!UICONTROL Criar formulário]**:

| Componente | Propriedades |
|------------------|----------------------------------------------------|
| Título da seção | Rótulo do campo, Descrição |
| Texto em linha única | Rótulo do campo, Mapear para propriedade, Valor padrão |
| Texto multivalor | Rótulo do campo, Mapear para propriedade, Valor padrão |
| Número | Rótulo do campo, Mapear para propriedade, Valor padrão |
| Data | Rótulo do campo, Mapear para propriedade, Valor padrão |
| Tags padrão | Rótulo do campo, Mapear para propriedade, Valor padrão, Descrição |

1. Toque em **[!UICONTROL Concluído]**. O Perfil Metadados é adicionado à lista de perfis na página Perfis **** Metadados.

## Copiar um perfil de metadados {#copying-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um Perfil de metadados para fazer uma cópia dele.
1. Toque em **[!UICONTROL Copiar]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Copiar Perfil]** de Metadados, digite um título para a nova cópia do Perfil de Metadados.
1. Toque em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

## Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um perfil a ser excluído.
1. Toque em **[!UICONTROL Excluir Perfis]** de metadados na barra de ferramentas.
1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

## Aplicar um perfil de metadados a pastas {#applying-a-metadata-profile-to-folders}

Quando você atribui um perfil de metadados a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir apenas um perfil de metadados a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você carrega, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de metadados diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos adicionados posteriormente à pasta.

As pastas que têm um perfil atribuído a ele são indicadas na interface do usuário pelo nome do perfil que aparece no nome do cartão.

Você pode aplicar perfis de metadados a pastas específicas ou globalmente a todos os ativos.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Aplicar perfis de metadados a pastas específicas {#applying-metadata-profiles-to-specific-folders}

Aplique um perfil de metadados a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de metadados a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

You can reprocess assets in a folder that already has an existing video profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Aplicar perfis de metadados a pastas da interface do usuário do Perfis {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Selecione o perfil de metadados que deseja aplicar a uma pasta ou várias pastas.
1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de metadados a pastas a partir de Propriedades {#applying-metadata-profiles-to-folders-from-properties}

1. No painel esquerdo, toque em **[!UICONTROL Ativos]** e navegue até a pasta à qual deseja aplicar um perfil de metadados.
1. Na pasta, toque ou clique na marca de seleção para selecioná-la e, em seguida, toque ou clique em **Propriedades**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione o perfil no menu suspenso e toque em **Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

### Aplicar um perfil de metadados globalmente {#applying-a-metadata-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado em ativos AEM em qualquer pasta tenha o perfil selecionado aplicado.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Para aplicar um perfil de metadados globalmente, execute um dos procedimentos a seguir**

* Navegue até `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e toque em **Salvar**.

* Navegue até CRXDE Lite até o seguinte nó: `/content/dam/jcr:content`. Adicione a propriedade `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` e toque em **Salvar tudo**.

## Remoção de um perfil de metadados de pastas {#removing-a-metadata-profile-from-folders}

Quando você remove um perfil de metadados de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, qualquer processamento de arquivos que tenha ocorrido dentro das pastas permanece intacto.

Remova um perfil de metadados a uma pasta do menu **Ferramentas** ou, se estiver na pasta, nas **Propriedades**. Esta seção descreve como remover perfis de metadados de pastas de ambas as maneiras.

### Remoção de perfis de metadados de pastas por meio da interface do usuário de Perfis {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Toque ou clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis]** de metadados.
1. Selecione o perfil de metadados que deseja remover de uma pasta ou de várias pastas.
1. Toque em **[!UICONTROL Remover perfil de metadados das pastas]**, selecione uma ou várias pastas que deseja usar para remover um perfil e toque em **[!UICONTROL Concluído]**.

   Você pode confirmar que o perfil de metadados não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remoção de perfis de metadados de pastas por meio de Propriedades {#removing-metadata-profiles-from-folders-via-properties}

1. Toque no logotipo do AEM e navegue **[!UICONTROL pelos Ativos]** e, em seguida, até a pasta da qual você deseja remover um perfil de metadados.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
