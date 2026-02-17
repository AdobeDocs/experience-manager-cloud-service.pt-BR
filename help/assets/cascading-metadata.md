---
title: Metadados em cascata
description: Este artigo descreve como definir metadados em cascata para ativos.
feature: Metadata
role: Admin, User
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: 8d1744ca10ecce8637d9f9ff37eba05d2ca09ca4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 7%

---

# Metadados em cascata {#cascading-metadata}

Ao capturar as informações de metadados de um ativo, os usuários fornecem informações nos vários campos disponíveis. É possível exibir campos de metadados específicos ou valores de campo que dependem das opções selecionadas em outros campos. Essa exibição condicional de metadados é chamada de metadados em cascata. Em outras palavras, você pode criar uma dependência entre um campo/valor de metadados específico e um ou mais campos e/ou seus valores.

Use esquemas de metadados para definir regras para exibir metadados em cascata. Por exemplo, se o esquema de metadados incluir um campo de tipo de ativo, será possível definir um conjunto pertinente de campos a serem exibidos com base no tipo de ativo selecionado pelo usuário.

Estes são alguns casos de uso para os quais você pode definir metadados em cascata:

* Quando a localização do usuário for necessária, exibir nomes de cidades relevantes com base na escolha de país e estado do usuário.
* Carregue os nomes de marca pertinentes em uma lista de acordo com a escolha da categoria do produto feita pelo usuário.
* Alterne a visibilidade de um campo específico com base no valor especificado em outro campo. Por exemplo, exiba campos de endereço de entrega separados se o usuário quiser que a entrega seja distribuída em um endereço diferente.
* Designe um campo como obrigatório com base no valor especificado em outro campo.
* Altere as opções exibidas para um campo específico com base no valor especificado em outro campo.
* Defina o valor de metadados padrão em um campo específico com base no valor especificado em outro campo.

## Configurar metadados em cascata em [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Considere um cenário em que você deseja exibir metadados em cascata com base no tipo de ativo selecionado. Alguns exemplos

* Para um vídeo, exiba campos aplicáveis como formato, codec, duração e assim por diante.
* Para um documento do Word ou PDF, exiba campos como contagem de páginas, autor, etc.

Independentemente do tipo de ativo escolhido, exiba as informações de direitos autorais como um campo obrigatório.

1. Selecione o logotipo [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.
1. Na página **[!UICONTROL Forms de Esquema]**, selecione um formulário de esquema e, em seguida, selecione **[!UICONTROL Editar]** na barra de ferramentas para editar o esquema.

   ![selecionar_formulário](assets/select_form.png)

1. (Opcional) No editor de esquema de metadados, crie um campo para condicionar. Especifique um nome e um caminho de propriedade na guia **[!UICONTROL Configurações]**.

   Para criar uma guia, selecione `+` para adicionar uma guia e, em seguida, adicione um campo de metadados.

   ![add_tab](assets/add_tab.png)

1. Adicione um campo suspenso para o tipo de ativo. Especifique um nome e um caminho de propriedade na guia **[!UICONTROL Configurações]**. Adicione uma descrição opcional.

   ![campo_tipo_de_ativo](assets/asset_type_field.png)

1. Pares de valores-chave são as opções fornecidas a um usuário de formulário. Você pode fornecer os pares de valor-chave manualmente ou a partir de um arquivo JSON.

   * Para especificar os valores manualmente, selecione **[!UICONTROL Adicionar manualmente]**, **[!UICONTROL Adicionar opção]** e especifique o texto e o valor da opção. Por exemplo, especifique os tipos de ativos de Vídeo, PDF, Word e Imagem.

   * Para buscar os valores de um arquivo JSON dinamicamente, selecione **[!UICONTROL Adicionar por meio do caminho JSON]** e forneça o caminho do arquivo JSON. [!DNL Experience Manager] busca os pares chave-valor em tempo real quando o formulário é apresentado ao usuário.

   Ambas as opções se excluem mutuamente. Não é possível importar as opções de um arquivo JSON e editar manualmente.

   ![adicionar_escolha](assets/add_choice.png)

   >[!NOTE]
   >
   >Ao adicionar um arquivo JSON, os pares de valores chave não são exibidos no editor de esquema de metadados, mas estão disponíveis no formulário publicado.

   >[!NOTE]
   >
   >Ao adicionar opções, se clicar no campo pop-up, a interface é distorcida e o ícone excluir das opções para de funcionar. Não clique na lista suspensa até salvar as alterações. Se você enfrentar esse problema, salve o esquema e abra-o novamente para continuar editando.

1. (Opcional) Adicione os outros campos obrigatórios. Por exemplo, formato, codec e duração do vídeo do tipo de ativo.

   Da mesma forma, adicione campos dependentes para outros tipos de ativos. Por exemplo, adicione campos contagem de páginas e autor para ativos de documento, como arquivos do PDF e do Word.

   ![campos_dependentes_do_vídeo](assets/video_dependent_fields.png)

1. Para criar uma dependência entre o campo de tipo de ativo e outros campos, escolha o campo dependente e abra a guia **[!UICONTROL Regras]**.

   ![select_dependentfield](assets/select_dependentfield.png)

1. Em **[!UICONTROL Requisito]**, escolha a opção **[!UICONTROL Obrigatório, com base na nova regra]**.
1. Selecione **[!UICONTROL Adicionar regra]** e escolha o campo **[!UICONTROL Tipo de ativo]** para criar uma dependência. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Selecione **[!UICONTROL Concluído]** para salvar as alterações.

   ![definir_regra](assets/define_rule.png)

   >[!NOTE]
   >
   >Uma lista suspensa com valores predefinidos manualmente pode ser usada com regras. Menus suspensos com caminho JSON configurado não podem ser usados com regras que usam valores predefinidos para aplicar condições. Se os valores forem carregados do JSON no tempo de execução, não será possível aplicar uma regra predefinida.

1. Em **[!UICONTROL Visibilidade]**, escolha **[!UICONTROL Visível, com base na nova opção de regra]**.

1. Selecione **[!UICONTROL Adicionar regra]** e escolha o campo **[!UICONTROL Tipo de ativo]** para criar uma dependência. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Selecione **[!UICONTROL Concluído]** para salvar as alterações.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >Para redefinir os valores, selecione qualquer lugar na interface que não seja o valor. Se os valores forem redefinidos, selecione-os novamente.

   >[!NOTE]
   >
   >É possível aplicar as condições de **[!UICONTROL Requisito]** e **[!UICONTROL Visibilidade]** independentemente umas das outras.

1. Da mesma forma, crie uma dependência entre o valor Vídeo no campo Tipo de ativo e outros campos, como Codec e Duração.
1. Repita as etapas para criar dependência entre ativos de documento (PDF e Word) no campo [!UICONTROL Tipo de ativo] e em campos como [!UICONTROL Contagem de páginas] e [!UICONTROL Autor].
1. Clique em **[!UICONTROL Salvar]**. Aplicar o esquema de metadados a uma pasta.

1. Navegue até a pasta à qual você aplicou o esquema de metadados e abra a página de propriedades de um ativo. Dependendo da sua escolha no campo Tipo de ativo, os campos de metadados em cascata pertinentes são exibidos.

   ![Metadados em cascata para Ativo de vídeo](assets/video_asset.png)
   *Figura: metadados em cascata para ativo de vídeo*

   ![Metadados em cascata para o ativo de documento](assets/doc_type_fields.png)
   *Figura: metadados em cascata para o ativo de documento*

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
