---
title: Modelos de fragmentos do conteúdo
description: Modelos de fragmento de conteúdo são usados para criar fragmentos de conteúdo com conteúdo estruturado.
translation-type: tm+mt
source-git-commit: 287e2cec425c2fd7e80618d247dc658ae1280066
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 10%

---


# Modelos de fragmentos do conteúdo {#content-fragment-models}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

>[!CAUTION]
>
>A API AEM GraphQL, para o Delivery de fragmento de conteúdo, será lançada no início de 2021.
>
>A documentação relacionada já está disponível para fins de pré-visualização.

Os Modelos de fragmento de conteúdo definem a estrutura do conteúdo para seus [fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md).

Para usar os Modelos de fragmento de conteúdo, faça o seguinte:

1. [Ativar a funcionalidade do Modelo de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Crie](#creating-a-content-fragment-model) e  [configure](#defining-your-content-fragment-model) seus Modelos de fragmento de conteúdo
1. [Ative seus ](#enabling-disabling-a-content-fragment-model) Modelos de fragmento de conteúdo para uso ao criar Fragmentos de conteúdo para uso ao criar Fragmentos de conteúdo

## Criação de um modelo de fragmento de conteúdo {#creating-a-content-fragment-model}

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.
1. Navegue até a pasta apropriada para sua [configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Use **Criar** para abrir o assistente.

   >[!CAUTION]
   >
   >Se o [uso de modelos de fragmento de conteúdo não tiver sido ativado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

1. Especifique o **título do modelo**. Você também pode adicionar **Tags** e **Descrição**, se necessário.

   ![título e descrição](assets/cfm-models-02.png)

1. Use **Create** para salvar o modelo vazio. Uma mensagem indicará o sucesso da ação. Você pode selecionar **Abrir** para editar imediatamente o modelo ou **Concluído** para retornar ao console.

## Definição do modelo de fragmento de conteúdo {#defining-your-content-fragment-model}

O modelo de fragmento de conteúdo define efetivamente a estrutura dos fragmentos de conteúdo resultantes usando uma seleção de **[Tipos de dados](#data-types)**. Usando o editor de modelo, você pode adicionar instâncias dos tipos de dados e configurá-las para criar os campos necessários:

>[!CAUTION]
>
>Editar um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes.

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Abra o modelo necessário para **Editar**; use a ação rápida ou selecione o modelo e a ação na barra de ferramentas.

   Depois de abrir o editor de modelo, é mostrado:

   * esquerda: campos já definidos
   * direito: **Tipos de dados** disponíveis para criar campos (e **Propriedades** para uso depois que os campos forem criados)

   >[!NOTE]
   >
   >Quando um campo é **Obrigatório**, o **Rótulo** indicado no painel à esquerda é marcado com um asterisco (*****).

1. **Para adicionar um campo**

   * Arraste um tipo de dados necessário para o local desejado para um campo.

   * Depois que um campo for adicionado ao modelo, o painel direito mostrará as **Propriedades** que podem ser definidas para esse tipo de dados específico. Aqui você pode definir o que é necessário para esse campo.
Muitas propriedades são autoexplicativas, para obter detalhes adicionais, consulte [Propriedades](#properties).

1. **Como remover um campo**

   Selecione o campo desejado e clique/toque no ícone lixeira. Você receberá uma solicitação para confirmar a ação.

1. Adicione todos os campos obrigatórios e defina as propriedades relacionadas, conforme necessário.

1. Selecione **Salvar** para persistir na definição.

<!--
## Defining your Content Fragment Model {#defining-your-content-fragment-model}

The content fragment model effectively defines the structure of the resulting content fragments using a selection of **[Data Types](#data-types)**. Using the model editor you can add instances of the data types, then configure them to create the required fields:

>[!CAUTION]
>
>Editing an existing content fragment model can impact dependent fragments.

1. Navigate to **Tools**, **Assets**, then open **Content Fragment Models**.

1. Navigate to the folder holding your content fragment model.
1. Open the required model for **Edit**; use either the quick action, or select the model and then the action from the toolbar.

   Once open the model editor shows:

    * left: fields already defined
    * right: **Data Types** available for creating fields (and **Properties** for use once fields have been created)

   >[!NOTE]
   >
   >When a field as **Required**, the **Label** indicated in the left pane will be marked with an asterix (**&#42;**).

   ![properties](assets/cfm-models-03.png)

1. **To Add a Field**

    * Drag a required data type to the required location for a field:

      ![data type to field](assets/cfm-models-04.png)

    * Once a field has been added to the model, the right panel will show the **Properties** that can be defined for that particular data type. Here you can define what is required for that field. 
      Many properties are self-explanatory, for additional details see [Properties](#properties).
      For example:

      ![field properties](assets/cfm-models-05.png)

1. **To Remove a Field**

   Select the required field, then click/tap the trash-can icon. You will be asked to confirm the action.

   ![remove](assets/cfm-models-06.png)

1. Add all required fields, and define the related properties, as required. For example:

   ![save](assets/cfm-models-07.png)

1. Select **Save** to persist the definition.
-->

## Tipos de dados {#data-types}

Uma seleção de tipos de dados está disponível para definir seu modelo:

* **Texto em linha única**
   * Adicione um ou mais campos de uma única linha de texto; o comprimento máximo pode ser definido
* **Texto multilinha**
   * Uma área de texto que pode ser Rich Text, Plain Text ou Markdown
* **Número**
   * Adicionar um ou mais campos numéricos
* **Booleano**
   * Adicionar uma caixa de seleção booleana
* **Data e hora**
   * Adicionar uma data e/ou hora
* **Enumeração**
   * Adicionar um conjunto de caixas de seleção, botões de opção ou campos suspensos
* **Tags**
   * Permite que os autores de fragmentos acessem e selecionem áreas de tags
* **Referência de conteúdo**
   * Referências a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)

<!--
* **Fragment Reference**
  * References other content fragments; can be used to [create nested content](#using-references-to-form-nested-content)
  * The data type can be configured to allow fragment authors to:
    * Edit the referenced fragment directly.
    * Create a new content fragment, based on the appropriate model  
* **JSON Object**
  * Allows the content fragment author to enter JSON syntax into the corresponding elements of a fragment. 
    * To allow AEM to store direct JSON that you have copy/pasted from another service.
    * The JSON will be passed through, and output as JSON in GraphQL.
    * Includes JSON syntax-highlighting, auto-complete and error-highlighting in the content fragment editor.
-->

## Propriedades {#properties}

Muitas propriedades são autoexplicativas, para certas propriedades, mais detalhes são os seguintes:

* **Renderizar**
comoAs várias opções para realizar/renderizar o campo em um fragmento. Geralmente, isso permite definir se o autor verá uma única instância do campo ou poderá criar várias instâncias.

* **Rótulo**
do campoInserir um 
**O** Rótulo de campo gerará automaticamente um Nome **de** propriedade, que pode ser atualizado manualmente se necessário.

* **A validação**
ValidationBasic está disponível por mecanismos como a propriedade  **** Requirements. Alguns tipos de dados têm campos de validação de adição. Consulte [Validação](#validation) para obter mais detalhes.

* No tipo de dados **Texto de várias linhas**, é possível definir o **Tipo padrão** como:

   * **Texto formatado**
   * **Markdown**
   * **Texto sem formatação**

   Se não for especificado, o valor padrão **Rich Text** será usado para esse campo.

   Alterar o **Tipo padrão** em um modelo de fragmento de conteúdo só terá efeito em um fragmento de conteúdo existente relacionado depois que esse fragmento for aberto no editor e salvo.

<!--
* **Translatable**
  Checking the "Translatable" checkbox on a field in CF model editor will

  * Ensure the field's property name is added in translation config, context `/content/dam/<tenant>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.

* See **[Fragment Reference (Nested Fragments)](#fragment-reference-nested-fragments)** for more details about that specific data type and its properties.
-->

## Validação {#validation}

Vários tipos de dados agora incluem a possibilidade de definir requisitos de validação para quando o conteúdo é inserido no fragmento resultante:

* **Texto em linha única**
   * Compare com um regex predefinido.
* **Número**
   * Verifique valores específicos.

<!--
* **Content Reference**
  * Test for specific types of content.
  * Only images within a predefined range of width and height (in pixels) can be referenced. 
  * Only assets of specified file size or smaller can be referenced. 
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
* **Fragment Reference**
  * Test for a specific content fragment model.
-->

<!--
## Using References to form Nested Content {#using-references-to-form-nested-content}

Content Fragments can form nested content, using either of the following data types:

* **[Content Reference](#content-reference)**
  * Provides a simple reference to other content; of any type.
  * Can be configured for a one or multiple references (in the resulting fragment).

* **[Fragment Reference](#fragment-reference-nested-fragments)** (Nested Fragments)
  * References other fragments, dependent on the specific models specified.
  * Allows you to include/retrieve structured data.
    >[!NOTE]
    >
    >This method is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
  * Can be configured for one or multiple references (in the resulting fragment)..

>[!NOTE]
>
>AEM has a recurrence protection for:
>
>* Content References
>  This prevents the user from adding a reference to the current fragment. This may lead to an empty Fragment Reference picker dialog.
>
>* Fragment References in GraphQL 
>  If you create a deep query that returns multiple Content Fragments referenced by each another, it will return null at first occurence.

### Content Reference {#content-reference}

The Content Reference allows you to render content from another source; for example, image or content fragment.

In addition to standard properties you can specify:

* The **Root Path** for any referenced content.
* The content types that can be referenced.
* Limitations for file sizes.
* Image restraints.
-->

<!-- Check screenshot - might need update

   ![Content Reference](assets/cfm-content-reference.png)
-->

<!--
### Fragment Reference (Nested Fragments) {#fragment-reference-nested-fragments}

The Fragment Reference references one, or more, content fragments. This feature of particular interest when retrieving content for use in your app, as it allows you to retrieve structured data with multiple layers.

For example:

* A model defining details for an employee; these include:
  * A reference to the model that defines the employer (company)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>This is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

In addition to standard properties you can define:

* **Render As**:

  * **multifield** - the fragment author can create multiple, individual, references

  * **fragmentreference** - allows the fragment author to select a single reference to a fragment

* **Model Type**
  Multiple models can be selected. When authoring the Content Fragment any referenced fragments must have been created using these models.

* **Root Path**
  This specifies a root path for any fragments referenced.

* **Allow Fragment Creation**

  This will allow the fragment author to create a new fragment based on the appropriate model.
-->

<!--
  * **fragmentreferencecomposite** - allows the fragment author to build a composite, by selecting multiple fragments
-->

<!-- Check screenshot - might need update

   ![Fragment Reference](assets/cfm-fragment-reference.png)
-->

<!--
>[!NOTE]
>
>A recurrence protection mechanism is in place. It prohibits the user from selecting the current Content Fragment in the Fragment Reference. This may lead to an empty Fragment Reference picker dialog.
>
>There is also a recurrence protection for Fragment References in GraphQL. If you create a deep query across two Content Fragments that reference each other, it will return null.
-->

## Ativar ou desativar um modelo de fragmento de conteúdo {#enabling-disabling-a-content-fragment-model}

Para ter total controle sobre o uso dos Modelos de fragmento de conteúdo, eles têm um status que pode ser definido.

### Habilitar um modelo de fragmento de conteúdo {#enabling-a-content-fragment-model}

Depois que um modelo é criado, ele precisa ser habilitado para que:

* Está disponível para seleção ao criar um novo Fragmento de conteúdo.
* Pode ser referenciado em um Modelo de fragmento de conteúdo.
* Está disponível para GraphQL; então o schema é gerado.

Para habilitar um Modelo sinalizado como:

* **Rascunho** : mew (nunca ativado).
* **Desativado** : foi especificamente desativado.

Use a opção **Ativar** de:

* A barra de ferramentas superior, quando o Modelo necessário for selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Ativar um rascunho ou modelo desativado](assets/cfm-status-enable.png)

### Desabilitando um Modelo de Fragmento de Conteúdo {#disabling-a-content-fragment-model}

Um modelo também pode ser desativado para que:

* O modelo não está mais disponível como base para a criação de *novos* Fragmentos de conteúdo.
* No entanto:
   * O schema GraphQL continua sendo gerado e ainda pode ser consultado (para evitar o impacto da API JSON).
   * Todos os Fragmentos de conteúdo baseados no modelo ainda podem ser consultados e retornados do ponto de extremidade GraphQL.
* O modelo não pode mais ser referenciado, mas as referências existentes são mantidas intocadas e ainda podem ser consultadas e retornadas do ponto final GraphQL.

Para desativar um Modelo sinalizado como **Ativado**, use a opção **Desativar** de:

* A barra de ferramentas superior, quando o Modelo necessário for selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Desativar um modelo ativado](assets/cfm-status-disable.png)

## Excluindo um modelo de fragmento de conteúdo {#deleting-a-content-fragment-model}

>[!CAUTION]
A exclusão de um modelo de fragmento de conteúdo pode afetar fragmentos dependentes.

Para excluir um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Excluir** na barra de ferramentas.

   >[!NOTE]
   Se o modelo for referenciado, um aviso será dado. Agir adequadamente.

## Publicar um modelo de fragmento de conteúdo {#publishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo precisam ser publicados quando/antes que qualquer fragmento de conteúdo dependente seja publicado.

Para publicar um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Publicar** na barra de ferramentas.
O status publicado será indicado no console.

   >[!NOTE]
   Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

## Cancelamento de publicação de um modelo de fragmento de conteúdo {#unpublishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo podem ser despublicados se não forem referenciados por nenhum fragmento.

Para cancelar a publicação de um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento do conteúdo.
1. Selecione seu modelo, seguido por **Cancelar a publicação** na barra de ferramentas.
O status publicado será indicado no console.
