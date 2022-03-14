---
title: Metadados em cascata
description: Este artigo descreve como definir metadados em cascata para ativos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 12%

---

# Metadados em cascata {#cascading-metadata}

Ao capturar as informações de metadados de um ativo, os usuários fornecem informações nos vários campos disponíveis. É possível exibir campos de metadados específicos ou valores de campo que dependem das opções selecionadas nos outros campos. Essa exibição condicional de metadados é chamada de metadados em cascata. Em outras palavras, é possível criar uma dependência entre um campo/valor de metadados específico e um ou mais campos e/ou seus valores.

Use esquemas de metadados para definir regras para exibir metadados em cascata. Por exemplo, se o esquema de metadados incluir um campo de tipo de ativo, você poderá definir um conjunto pertinente de campos a serem exibidos com base no tipo de ativo selecionado pelo usuário.

Estes são alguns casos de uso para os quais você pode definir metadados em cascata:

* Sempre que a localização do usuário for necessária, exiba nomes de cidades relevantes com base na escolha do país e do estado pelo usuário.
* Carregue nomes de marcas pertinentes em uma lista com base na escolha de categoria de produto pelo usuário.
* Alternar a visibilidade de um campo específico com base no valor especificado em outro campo. Por exemplo, exiba campos de endereço de entrega separados se o usuário desejar que a entrega seja entregue em um endereço diferente.
* Atribua um campo como obrigatório com base no valor especificado em outro campo.
* Altere as opções exibidas para um campo específico com base no valor especificado em outro campo.
* Defina o valor dos metadados padrão em um campo específico com base no valor especificado em outro campo.

## Configurar metadados em cascata em [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Considere um cenário em que deseja exibir metadados em cascata com base no tipo de ativo selecionado. Alguns exemplos

* Para um vídeo, exiba campos aplicáveis, como formato, codec, duração e assim por diante.
* Para um documento do Word ou PDF, exiba campos, como contagem de páginas, autor e assim por diante.

Independentemente do tipo de ativo escolhido, exiba as informações de direitos autorais como um campo obrigatório.

1. Toque/clique no botão [!DNL Experience Manager] logotipo e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.
1. Na página **[!UICONTROL Formulários de esquema]**, selecione um formulário de esquema e toque/clique em **[!UICONTROL Editar]** na barra de ferramentas para editar o esquema.

   ![select_form](assets/select_form.png)

1. (Opcional) No editor de esquema de metadados, crie um novo campo para condicionar. Especifique um nome e um caminho de propriedade no **[!UICONTROL Configurações]** guia .

   Para criar uma nova guia, toque/clique em `+` para adicionar uma guia e, em seguida, adicionar um campo de metadados.

   ![add_tab](assets/add_tab.png)

1. Adicione um campo suspenso para o tipo de ativo. Especifique um nome e um caminho de propriedade no **[!UICONTROL Configurações]** guia . Adicione uma descrição opcional.

   ![asset_type_field](assets/asset_type_field.png)

1. Os pares de valores-chave são as opções fornecidas a um usuário do formulário. Você pode fornecer os pares de valores chave manualmente ou de um arquivo JSON.

   * Para especificar os valores manualmente, selecione **[!UICONTROL Adicionar manualmente]** e toque/clique **[!UICONTROL Adicionar escolha]** e especifique o texto e o valor da opção. Por exemplo, especifique os tipos de ativos Vídeo, PDF, Palavra e Imagem .

   * Para buscar os valores de um arquivo JSON dinamicamente, selecione **[!UICONTROL Adicionar por meio do caminho JSON]** e forneça o caminho do arquivo JSON. [!DNL Experience Manager] busca os pares de valor chave em tempo real, quando o formulário é apresentado ao usuário.

   Ambas as opções são mutuamente exclusivas. Não é possível importar as opções de um arquivo JSON e editar manualmente.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Ao adicionar um arquivo JSON, os pares de valor chave não são exibidos no editor de esquema de metadados, mas estão disponíveis no formulário publicado.

   >[!NOTE]
   >
   >Ao adicionar opções, se você clicar no campo pop-up, a interface fica distorcida e o ícone de exclusão das opções para de funcionar. Não clique na lista suspensa até salvar as alterações. Se você enfrentar esse problema, salve o schema e abra-o novamente para continuar a edição.

1. (Opcional) Adicione os outros campos obrigatórios. Por exemplo, formato, codec e duração do vídeo de tipo de ativo.

   Da mesma forma, adicione campos dependentes para outros tipos de ativos. Por exemplo, adicione campos contagem de páginas e autor para ativos de documento, como arquivos PDF e Word.

   ![campos_dependentes_do_vídeo](assets/video_dependent_fields.png)

1. Para criar uma dependência entre o campo do tipo de ativo e outros campos, escolha o campo dependente e abra o **[!UICONTROL Regras]** guia .

   ![select_depenentfield](assets/select_dependentfield.png)

1. Em **[!UICONTROL Requisito]**, escolha o **[!UICONTROL Obrigatório, com base na nova regra]** opção.
1. Toque/clique em **[!UICONTROL Adicionar regra]** e escolha o campo **[!UICONTROL Tipo de ativo]** para criar uma dependência. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Toque/clique em **[!UICONTROL Concluído]** para salvar as alterações.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >A lista suspensa com valores predefinidos manualmente pode ser usada com regras. Menus suspensos com caminho JSON configurado não podem ser usados com regras que usam valores predefinidos para aplicar condições. Se os valores forem carregados do JSON no tempo de execução, não será possível aplicar uma regra predefinida.

1. Em **[!UICONTROL Visibilidade]**, escolha **[!UICONTROL Visível, com base na nova opção de regra]**.

1. Toque/clique em **[!UICONTROL Adicionar regra]** e escolha o campo **[!UICONTROL Tipo de ativo]** para criar uma dependência. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Toque/clique em **[!UICONTROL Concluído]** para salvar as alterações.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >Para redefinir os valores, clique ou toque em espaço em branco ou em qualquer lugar na interface diferente dos valores. Se os valores forem redefinidos, selecione os valores novamente.

   >[!NOTE]
   >
   >É possível aplicar as condições de **[!UICONTROL Requisito]** e **[!UICONTROL Visibilidade]** independentemente umas das outras.

1. Da mesma forma, crie uma dependência entre o valor Vídeo no campo Tipo de ativo e outros campos, como Codec e Duration.
1. Repita as etapas para criar dependência entre ativos de documento (PDF e Word) na [!UICONTROL Tipo de ativo] e campos como [!UICONTROL Contagem de Página] e [!UICONTROL Autor].
1. Clique em **[!UICONTROL Salvar]**. Aplique o esquema de metadados a uma pasta.

1. Navegue até a pasta na qual você aplicou o Esquema de metadados e abra a página de propriedades de um ativo. Dependendo de sua escolha no campo Tipo de ativo , os campos de metadados em cascata pertinentes são exibidos.

   ![Metadados em cascata para o ativo de Vídeo](assets/video_asset.png)
   *Figura: Metadados em cascata para o ativo de Vídeo*

   ![Metadados em cascata para o ativo de documento](assets/doc_type_fields.png)
   *Figura: Metadados em cascata para o ativo de documento*
