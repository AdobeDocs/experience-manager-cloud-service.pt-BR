---
title: Esquema de metadados de pasta
description: Saiba como criar schemas de metadados para pastas de ativos no AEM Assets
contentOwner: AG
translation-type: tm+mt
source-git-commit: dc5cec192a70413e0ebcc27eb5e58577079ae93b
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 10%

---


# Esquema de metadados de pasta {#folder-metadata-schema}

Os ativos Adobe Experience Manager (AEM) permitem que você crie schemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta.

## Adicionar um formulário de schema de metadados de pasta {#add-a-folder-metadata-schema-form}

Use o editor do Forms Schema de Metadados da Pasta para criar e editar schemas de metadados para pastas.

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados de pasta]**.
1. Na página do Forms Schema de metadados da pasta, toque/clique em **[!UICONTROL Criar]**.
1. Especifique um nome para o formulário e toque/clique em **[!UICONTROL Criar]**. O novo formulário de schema é listado na página Forms do Schema.

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

É possível editar um formulário de schema de metadados recém-adicionado ou existente, que inclui o seguinte:

* Guias
* Itens de formulário em guias.

Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar novas guias ou itens de formulário ao formulário de schema de metadados.

1. Na página Forms do Schema, selecione o formulário criado e, em seguida, toque/clique no ícone **[!UICONTROL Editar]** na barra de ferramentas.
1. Na página Editor de Schemas de Metadados de Pastas, toque/clique no ícone **[!UICONTROL +]** para adicionar uma guia ao formulário. Para renomear a guia, toque/clique no nome padrão e especifique o novo nome em **[!UICONTROL Configurações]**.

   ![custom_tab](assets/custom_tab.png)

   Para adicionar mais guias, toque/clique no ícone **[!UICONTROL +]** . Toque/clique em **[!UICONTROL X]** para excluir uma guia.

1. Na guia ativa, adicione um ou mais componentes da guia **[!UICONTROL Criar formulário]** .

   ![add_components](assets/adding_components.png)

   Se você criar várias guias, toque/clique em uma guia específica para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Configurações]** .

   Se necessário, exclua um componente da guia **[!UICONTROL Configurações]** .

   ![configure_properties](assets/configure_properties.png)

1. Toque/clique em **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações.

### Componentes para criar formulários {#components-to-build-forms}

A guia **[!UICONTROL Criar formulário]** lista itens de formulário que você usa no formulário de schema de metadados da pasta. A guia **[!UICONTROL Configurações]** exibe os atributos para cada item selecionado na guia **[!UICONTROL Criar formulário]** . Esta é uma lista dos itens de formulário disponíveis na guia **[!UICONTROL Criar formulário]** :

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome do componente</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Título da seção</p> </td>
   <td><p> Adicione um cabeçalho de seção para uma lista de componentes comuns.</p> </td>
  </tr>
  <tr>
   <td><p>Texto em linha única</p> </td>
   <td><p> Adicione uma propriedade de texto de linha única. É armazenado como uma string.</p> </td>
  </tr>
  <tr>
   <td><p>Texto multivalor</p> </td>
   <td><p> Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de string.</p> </td>
  </tr>
  <tr>
   <td><p>Número</p> </td>
   <td><p> Adicione um componente de número.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p> Adicione um componente de data.</p> </td>
  </tr>
  <tr>
   <td><p>Lista suspensa</p> </td>
   <td><p> Adicione uma lista suspensa.</p> </td>
  </tr>
  <tr>
   <td><p>Tags padrão</p> </td>
   <td><p> Adicionar uma tag. </p> </td>
  </tr>
  <tr>
   <td><p>Campo oculto</p> </td>
   <td><p> Adicionar um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo.</p> </td>
  </tr>
 </tbody>
</table>

### Editar itens de formulário {#editing-form-items}

Para editar as propriedades dos itens de formulário, toque/clique no componente e edite todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Configurações]** .

**[!UICONTROL Rótulo]** do campo: O nome da propriedade de metadados que é exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para propriedade]**: Essa propriedade especifica o caminho relativo do nó de pasta no repositório CRX onde ele é salvo. Ele start com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

Estes são os valores válidos para esta propriedade:

* `./jcr:content/metadata/dc:title`: Armazena o valor no nó de metadados da pasta como a propriedade `dc:title`.

* `./jcr:created`: Armazena a data e a hora de criação de um ativo. É uma propriedade protegida. Se você configurar essas propriedades, o Adobe recomenda marcá-las como [!UICONTROL Desativar edição].

Para garantir que o componente seja exibido corretamente no formulário de schema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho]** JSON: Use-o para especificar o caminho do arquivo JSON no qual você especifica pares de valores chave para opções.

**[!UICONTROL Espaço reservado]**: Use essa propriedade para especificar o texto relevante do espaço reservado para a propriedade metadata.

**[!UICONTROL Opções]**: Use essa propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: Use essa propriedade para adicionar uma breve descrição para o componente de metadados.

**[!UICONTROL Classe]**: Classe de objeto à qual a propriedade está associada.

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

Você pode excluir formulários de schema de metadados de pasta da página Forms do Schema Metadados de pasta. Para excluir um formulário, selecione-o e toque/clique no ícone Excluir da barra de ferramentas.

![delete_form](assets/delete_form.png)

## Atribuir um schema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um schema de metadados de pasta a uma pasta na página Forms do Schema Metadados de pasta ou ao criar uma pasta.

Se você configurar um schema de metadados para uma pasta, o caminho para o formulário de schema será armazenado na propriedade `folderMetadataSchema` do nó de pasta em .*/jcr:content*.

### Atribuir a um schema da página Schema Metadados da pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**> **[!UICONTROL Esquemas de metadados de pasta]**.
1. Na página do Forms Schema de metadados da pasta, selecione o formulário de schema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Aplicar às pastas]**.

1. Selecione a pasta na qual aplicar o schema e clique/toque em **[!UICONTROL Aplicar]**. Se um schema de metadados já estiver aplicado na pasta, uma mensagem de aviso informará que você está prestes a substituir o schema de metadados existente. Toque/clique em **[!UICONTROL Substituir]**.
1. Abra as propriedades de metadados da pasta na qual você aplicou o schema de metadados.

   ![folder_properties](assets/folder_properties.png)

   Para exibir os campos de metadados da pasta, toque/clique na guia **[!UICONTROL Metadados da pasta]**.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Atribuir um schema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um schema de metadados de pasta ao criar uma pasta. Se pelo menos um schema de metadados de pasta existir no sistema, uma lista extra será exibida na caixa de diálogo **[!UICONTROL Criar pasta]** . Você pode selecionar o schema desejado. Por padrão, nenhum schema é selecionado.

1. Na interface do usuário do AEM Assets, toque/clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Schema Metadados da pasta, selecione o schema desejado. Then, tap/click **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades de metadados da pasta na qual você aplicou o schema de metadados.
1. Para exibir os campos de metadados da pasta, toque/clique na guia **[!UICONTROL Metadados da pasta]**.

## Usar o schema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. Uma guia **[!UICONTROL Metadados da pasta]** é exibida na página Propriedades da pasta. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira valores de metadados nos vários campos e toque/clique em **[!UICONTROL Salvar]** para armazenar os valores. Os valores especificados são armazenados no nó da pasta no repositório CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
