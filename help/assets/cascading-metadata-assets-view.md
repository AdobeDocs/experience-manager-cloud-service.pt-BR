---
title: Metadados em cascata
description: Este artigo descreve como definir metadados em cascata para ativos na exibição de ativos.
feature: Metadata
role: Admin, User
source-git-commit: 2bb309afc372fe18ce274a2813ed25cba22eb4de
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 4%

---


# Exibição do Assets de metadados em cascata{#cascading-metadata-assets-view}

Ao capturar as informações de metadados de um ativo, os usuários fornecem informações nos vários campos disponíveis. É possível exibir campos de metadados específicos ou valores de campo que dependem das opções selecionadas em outros campos. Essa exibição condicional de metadados é chamada de metadados em cascata. Em outras palavras, você pode criar uma dependência entre um campo/valor de metadados específico e um ou mais campos e/ou seus valores.

Use o Forms de metadados para definir regras para exibir metadados em cascata. Por exemplo, se o formulário de metadados incluir um campo de tipo de ativo, será possível definir um conjunto pertinente de campos a serem exibidos com base no tipo de ativo que um usuário selecionar.

Estes são alguns casos de uso para os quais você pode definir metadados em cascata:

* Quando a localização do usuário for necessária, exibir nomes de cidades relevantes com base na escolha de país e estado do usuário.
* Carregue os nomes de marca pertinentes em uma lista de acordo com a escolha da categoria do produto feita pelo usuário.
* Alterne a visibilidade de um campo específico com base no valor especificado em outro campo. Por exemplo, exiba campos de endereço de entrega separados se o usuário quiser que a entrega seja distribuída em um endereço diferente.
* Designe um campo como obrigatório com base no valor especificado em outro campo.
* Altere as opções exibidas para um campo específico com base no valor especificado em outro campo.
* Defina o valor de metadados padrão em um campo específico com base no valor especificado em outro campo.

>[!IMPORTANT]
>
>O recurso de metadados em cascata está disponível como recursos de Disponibilidade limitada. Você pode [criar e enviar um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para habilitá-lo para sua implantação.

## Configurar metadados em cascata em [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Considere um cenário em que você deseja exibir metadados em cascata com base no tipo de ativo selecionado. Por exemplo -

* Para um vídeo, exiba campos aplicáveis como formato, codec, duração e assim por diante.
* Para um documento do Word ou PDF, exiba campos como contagem de páginas, autor, etc.

Estamos usando um campo suspenso chamado `Image` como exemplo para categorizar arquivos com base em seus tipos de imagem. A lista suspensa contém opções que representam extensões de imagem compatíveis (como JPG/JPEG, GIF etc.). Para garantir a consistência dos dados e evitar que formatos não compatíveis sejam selecionados ou processados, uma regra de validação é aplicada a esse campo. A regra avalia o valor suspenso selecionado e impõe restrições que se alinham aos formatos de imagem aceitos.

>[!IMPORTANT]
>
>Você pode criar regras com base apenas em campos suspensos.

Independentemente do tipo de ativo escolhido, exiba as informações de direitos autorais como um campo obrigatório. Você pode usar os [componentes de metadados predefinidos](metadata-assets-view.md#property-components) e [atribuir metadados a uma pasta](metadata-assets-view.md#assign-metadata-form-folder).

### Criar Forms de metadados {#build-metadata-schema-forms}

Considere as etapas abaixo para criar um novo Formulário de metadados:

1. Selecione o logotipo [!DNL Experience Manager] e vá para **[!UICONTROL Configurações]** > **[!UICONTROL Forms de Metadados]** > **[!UICONTROL Criar]**.

1. Na lista suspensa **[!UICONTROL Tipo]**, selecione o tipo de formulário apropriado: **[!UICONTROL Arquivo]**, **[!UICONTROL Pasta]** ou **[!UICONTROL Coleção]**.

1. Especifique o título do formulário de metadados no campo **[!UICONTROL Nome]**.

1. Como alternativa, escolha um modelo de formulário de metadados existente na lista suspensa **[!UICONTROL Escolher a partir do modelo de formulário existente]**.

1. Um Formulário de metadados em branco é exibido. Adicione uma nova guia.

   ![Interface do Usuário do Formulário de Metadados](assets/metadata-form-ui.png)

   * **A:** Alternar entre [!UICONTROL Editar] ou [!UICONTROL Visualizar]
   * **B:** [Componentes do Formulário de Metadados](metadata-assets-view.md#property-components)
   * **C:** Alternar para outro Formulário de Metadados
   * **D:** Adicione uma nova guia
   * **E:** Tela
   * **F:** Configurações gerais do componente selecionado
   * **G:** guia Regras
   * **H:** propriedades do componente

Assista a este vídeo para exibir a sequência de etapas, [Configurar Forms de Metadados](https://video.tv.adobe.com/v/341275).

### Modificar um formulário de metadados existente {#modify-existing-metadata-form}

Para modificar um formulário de metadados existente, siga as etapas abaixo:

1. Abra um Formulário de Metadados existente e navegue até os [componentes predefinidos](metadata-assets-view.md#property-components) que deseja adicionar ao formulário e solte os elementos na tela.

   De acordo com o caso de uso **Image**, adicione um campo suspenso para definir tipos de ativos de imagem. Especifique o nome e o caminho da propriedade em **Configurações** e, opcionalmente, configure o campo como **[!UICONTROL Somente Leitura]** ou **[!UICONTROL Várias Seleções]**.

1. Forneça as opções de valor principal para a lista suspensa, inserindo-as manualmente, especificando um caminho JSON ou importando um arquivo CSV.

   * Para especificar os valores manualmente, selecione **[!UICONTROL Adicionar manualmente]** em **[!UICONTROL Opções]**, clique em `Add` e especifique o rótulo e o valor da opção. Por exemplo, especifique os tipos de ativos de Vídeo, PDF e Imagem.

     ![Tipo de ativo de imagem](assets/image-asset-type.png)

   * Para buscar valores de um caminho JSON, selecione **[!UICONTROL Adicionar por meio do Caminho JSON]** e especifique o caminho do arquivo JSON.

     >[!NOTE]
     >
     >Armazene o arquivo JSON em um local compartilhado acessível a todos os editores e autores do DAM.

     ![Adicionar opções por meio do caminho JSON](assets/add-json-choices.png)

   * Para buscar os valores de um CSV dinamicamente, clique em **[!UICONTROL Importar CSV]** e forneça o caminho do arquivo CSV. [!DNL Experience Manager] busca os pares chave-valor em tempo real quando o formulário é apresentado ao usuário.

     ![Adicionar opções por meio do CSV](assets/import-csv-choices.png)

   >[!NOTE]
   > 
   >Não é possível importar as opções de um arquivo CSV e editá-las manualmente, pois ambas são mutuamente exclusivas.

1. Para criar uma dependência entre o campo Imagem e outros campos, selecione o campo dependente e abra a guia **[!UICONTROL Regras]**. Cada componente aceita um conjunto específico de regras. Para esse caso de uso, as opções de Tipo de ativo de imagem são usadas para definir a lógica da regra.

   <!--![Image Asset Type Rule](assets/image-asset-type-rule.png)-->

   <!--![rule tab](assets/rule-tab.png)-->

1. Em **[!UICONTROL Obrigatório]**, escolha a opção **[!UICONTROL Obrigatório com base na nova regra]**. Clique no ![ícone de adição](assets/do-not-localize/aem_assets_add_icon.png) para adicionar uma nova regra.

   ![regra](assets/image-required-rule1.png)

   No caso de uso atual, o campo Tipo de ativo é necessário quando o formato do ativo de imagem é JPG/JPEG, PNG, GIF, TIFF ou WEBP. Além disso, clique em ![ícone de edição](assets/do-not-localize/edit.svg) para redefinir a regra ou clique em ![ícone de exclusão](assets/do-not-localize/delete.svg) para excluir a regra definida.

   ![regra](assets/image-required-rule2.png)

1. Em **[!UICONTROL Visibilidade]**, escolha a opção **[!UICONTROL Visível, com base na nova regra]**. Clique no ![ícone de adição](assets/do-not-localize/aem_assets_add_icon.png) para adicionar uma nova regra.

   >[!NOTE]
   >
   >Você pode aplicar a condição de **[!UICONTROL Requisito]** e a condição de **[!UICONTROL Visibilidade]** independentemente umas das outras.

   ![regra](assets/image-visible-rule1.png)

   No caso de uso atual, o campo Tipo de ativo fica visível quando o formato do ativo de imagem é JPG/JPEG, PNG ou GIF. Além disso, clique em ![ícone de edição](assets/do-not-localize/edit.svg) para redefinir a regra ou clique em ![ícone de exclusão](assets/do-not-localize/delete.svg) para excluir a regra definida.

   ![regra](assets/image-visible-rule2.png)

1. Selecione **[!UICONTROL Opções com base na regra]** para criar uma dependência e definir a regra. Clique no ![ícone de adição](assets/do-not-localize/aem_assets_add_icon.png) para adicionar uma nova regra.

   ![regra](assets/image-choices-rule1.png)

   Para configurar opções com base em regras para a lista suspensa Tipo de ativo, crie uma regra e defina Imagem como o campo dependente. Em seguida, defina os valores de exibição para cada formato de imagem selecionando Imagem para JPG/JPEG, PNG, GIF e TIFF e selecionando Vídeo para WEBP, garantindo que apenas os valores pretendidos sejam verificados para cada formato para exibir dinamicamente opções relevantes. Além disso, clique em ![ícone de edição](assets/do-not-localize/edit.svg) para redefinir a regra ou clique em ![ícone de exclusão](assets/do-not-localize/delete.svg) para excluir a regra definida.

   ![regra](assets/image-choices-rule2.png)

1. Da mesma forma, repita as etapas para criar uma dependência entre os outros ativos, como o PDF e o Word, no campo [!UICONTROL Tipo de ativo], e em campos como [!UICONTROL Contagem de páginas] e [!UICONTROL Autor].

1. Clique em **[!UICONTROL Salvar]**. Aplicar o formulário de metadados a uma pasta.

1. Navegue até a pasta à qual você aplicou o Formulário de metadados e abra a página de propriedades de um ativo. Dependendo da sua escolha no campo Tipo de ativo, os campos de metadados em cascata pertinentes são exibidos.

   ![Saída de formulário de metadados em cascata](assets/cascading-metadata-form-output.png)

>[!NOTE]
> 
>Para obter acesso antecipado aos Metadados em Cascata na sua conta do Assets View, [crie e envie um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## Próximas etapas {#next-steps}

* [Assista a um vídeo sobre gerenciamento de formulários de metadados no modo de exibição do Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=pt-BR)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General&lang=pt-BR#support)

