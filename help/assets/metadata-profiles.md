---
title: Perfis de metadados
description: Saiba mais sobre perfis de metadados para ativos. Saiba como criar um perfil de metadados e aplicá-lo a ativos de pastas.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 21%

---

# Perfis de metadados {#metadata-profiles}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Um Perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um Perfil de metadados e aplique-o a uma pasta. Qualquer ativo que você fizer upload posteriormente para a pasta herdará os metadados padrão configurados no Perfil de metadados.

Um conceito importante sobre o uso de perfis no Experience Manager Assets é que eles são atribuídos a pastas. Em um perfil são configurações na forma de perfis de metadados, juntamente com perfis de vídeo ou perfis de imagem. Essas configurações processam o conteúdo de uma pasta junto com qualquer uma de suas subpastas. Portanto, a maneira como você nomeia arquivos e pastas, organiza subpastas e lida com os arquivos dentro dessas pastas tem um impacto significativo na maneira como esses ativos são processados por um perfil.
Ao usar estratégias consistentes e apropriadas de nomenclatura de arquivos e pastas e boas práticas de metadados, você aproveita ao máximo sua coleção de ativos digitais e garante que os arquivos certos sejam processados pelo perfil correto.

## Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]** e clique em **[!UICONTROL Criar]**.
1. Insira um título para o Perfil de Metadados, por exemplo, Metadados de amostra, e selecione **[!UICONTROL Enviar]**. O formulário de edição do perfil de metadados é exibido.
1. Clique em um componente e configure suas propriedades na guia **[!UICONTROL Configurações]**. Por exemplo, clique no componente **[!UICONTROL Descrição]** e edite suas propriedades.
Edite as seguintes propriedades para o componente **[!UICONTROL Descrição]**:

   * **[!UICONTROL Rótulo do Campo]** - O nome para exibição da propriedade de metadados. É somente para referência do usuário.
   * **[!UICONTROL Mapear para a Propriedade]** - O valor dessa propriedade fornece o caminho/nome relativo para o nó do ativo onde ele é salvo no repositório. O valor deve sempre começar com `./` porque indica que o caminho está sob o nó do ativo.

     O valor especificado para **[!UICONTROL Mapear para a propriedade]** é armazenado como uma propriedade no nó de metadados do ativo. Por exemplo, se você especificar . `/jcr:content/metadata/dc:desc` como o nome de **[!UICONTROL Mapear para a propriedade]**, [!DNL Adobe Experience Manager Assets] armazena o valor `dc:desc` no nó de metadados do ativo.

   * **[!UICONTROL Valor Padrão]** - Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

     >[!NOTE]
     >
     >Adicionar um valor padrão a uma nova propriedade de metadados (que não existe no nó `/jcr:content/metadata`) não exibe a propriedade e seu valor na página Propriedades do ativo por padrão. Para exibir a nova propriedade na página [!UICONTROL Propriedades], modifique o formulário de esquema correspondente.

1. (Opcional) Adicione mais componentes ao Formulário de edição na guia **[!UICONTROL Criar formulário]** e configure as propriedades na guia **[!UICONTROL Configurações]**. As seguintes propriedades estão disponíveis na guia **[!UICONTROL Criar formulário]**:

| Componente | Propriedades |
|------------------|----------------------------------------------------|
| Cabeçalho da seção | Rótulo do campo, Descrição |
| Texto em linha única | Rótulo do campo, Mapear para a propriedade, Valor padrão |
| Texto multivalor | Rótulo do campo, Mapear para a propriedade, Valor padrão |
| Número | Rótulo do campo, Mapear para a propriedade, Valor padrão |
| Data | Rótulo do campo, Mapear para a propriedade, Valor padrão |
| Tags padrão | Rótulo do campo, Mapear para a propriedade, Valor padrão, Descrição |

1. Clique em **[!UICONTROL Concluído]**. O perfil de metadados foi adicionado à lista de perfis na página **[!UICONTROL Perfis de metadados]**.

## Copiar um perfil de metadados {#copying-a-metadata-profile}

1. Na página **[!UICONTROL Perfis de metadados]**, selecione um Perfil de metadados para fazer uma cópia dele.
1. Clique em **[!UICONTROL Copiar]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Copiar Perfil de Metadados]**, insira um título para a nova cópia do Perfil de Metadados.
1. Clique em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

## Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. Na página **[!UICONTROL Perfis de metadados]**, selecione um perfil a ser excluído.
1. Clique em **[!UICONTROL Excluir Perfis de Metadados]** na barra de ferramentas.
1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

## Aplicar um perfil de metadados a pastas {#applying-a-metadata-profile-to-folders}

Ao atribuir um perfil de metadados a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta principal. A herança é interrompida quando um perfil diferente é aplicado a uma subpasta. É possível atribuir apenas um perfil de metadados a uma pasta. Portanto, considere cuidadosamente a estrutura de pastas onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de metadados diferente a uma pasta, o novo perfil substitui o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta após a alteração. Aplique perfis de metadados a pastas específicas ou globalmente a todos os ativos.

As pastas que têm um perfil atribuído a elas são indicadas na interface pelo nome do perfil que aparece no nome do cartão.

É possível reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você alterou posteriormente. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Aplicar perfis de metadados a pastas específicas {#applying-metadata-profiles-to-specific-folders}

Aplique um perfil de metadados a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de metadados a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Aplicar perfis de metadados a pastas da interface do usuário Perfis {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Navegue até **[!UICONTROL Ferramentas > Assets > Perfis de metadados]**.
1. Selecione o perfil de metadados que deseja aplicar a uma ou várias pastas.
1. Clique em **[!UICONTROL Aplicar perfil de metadados às pastas]**, selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e clique em **[!UICONTROL Concluído]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de metadados a pastas de Propriedades {#applying-metadata-profiles-to-folders-from-properties}

1. No painel à esquerda, clique em **[!UICONTROL Assets]** e navegue até a pasta à qual deseja aplicar um perfil de metadados.
1. Na pasta, marque a marca de seleção para selecioná-la e selecione **Propriedades**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione o perfil no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

### Aplicar um perfil de metadados globalmente {#applying-a-metadata-profile-globally}

Além de aplicar um perfil a uma pasta, você também pode aplicá-lo globalmente para que qualquer conteúdo carregado em [!DNL Experience Manager Assets] em qualquer pasta tenha o perfil selecionado aplicado.

É possível reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você alterou posteriormente. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Para aplicar um perfil de metadados globalmente, siga um destes procedimentos**

* Navegue até `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam`, aplique o perfil apropriado e clique em **[!UICONTROL Salvar]**.

* Navegue até o CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`. Adicione a propriedade `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Clique em **Salvar tudo**.

## Remoção de um perfil de metadados de pastas {#removing-a-metadata-profile-from-folders}

Ao remover um perfil de metadados de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta principal. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Remova um perfil de metadados a uma pasta do menu **Ferramentas** ou, se estiver na pasta, nas **Propriedades**. Esta seção descreve como remover perfis de metadados de pastas de ambas as maneiras.

### Remover perfis de metadados de pastas por meio da interface do usuário Perfis {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Clique no logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas > Assets > Perfis de metadados]**.
1. Selecione o perfil de metadados que deseja remover de uma ou várias pastas.
1. Clique em **[!UICONTROL Remover perfil de metadados das pastas]**, selecione uma ou várias pastas que deseja usar para remover um perfil e clique em **[!UICONTROL Concluído]**.

   É possível confirmar que o perfil de metadados não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remoção de perfis de metadados de pastas por meio de Propriedades {#removing-metadata-profiles-from-folders-via-properties}

1. Clique no logotipo do Experience Manager, navegue até **[!UICONTROL Assets]** e, em seguida, acesse a pasta da qual deseja remover um perfil de metadados.
1. Na pasta, clique na marca de seleção para selecioná-la e clique em **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
