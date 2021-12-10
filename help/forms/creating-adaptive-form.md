---
title: Como criar um formulário adaptável?
description: 'Saiba como criar um formulário adaptável usando [!DNL Experience Manager Forms]. O Adaptive Forms são formulários HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um formulário adaptável com base em um Modelo de dados de formulário e esquema XML ou JSON. '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 0%

---

# Criar um formulário adaptável {#creating-an-adaptive-form}

O Adaptive Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. [!DNL AEM Forms] O oferece uma interface de usuário intuitiva e componentes prontos para uso para criar e trabalhar com o Adaptive Forms. É possível optar por criar um formulário adaptável com base em um modelo ou esquema de formulário ou sem um modelo de formulário. É importante escolher cuidadosamente o modelo de formulário que atende não apenas às suas necessidades, mas estende os investimentos e ativos existentes em infraestrutura. Você pode escolher entre as seguintes opções para criar um formulário adaptável:

* **Uso de um modelo de dados de formulário**
   [Integração de dados](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados em um Modelo de dados de formulário que pode ser usado para criar o Adaptive Forms. Escolha Modelo de dados de formulário se o Formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **Usando uma Definição de Esquema XML (XSD) ou um Esquema JSON**
Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. Você pode associar o esquema a um Formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao Formulário adaptável. Os elementos do esquema estarão disponíveis para uso na guia Objetos do modelo de dados do navegador Conteúdo ao criar o Adaptive Forms.

* **Uso de um modelo de formulário nenhum ou sem**
O Adaptive Forms criado com essa opção não usa nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.

## Pré-requisitos

Você precisa do seguinte para criar um formulário adaptável:

* Um modelo de formulário adaptável. Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados contendo determinadas propriedades e estrutura de conteúdo É possível [criar um novo modelo](template-editor.md), importar um modelo existente ou baixar e importar alguns [modelos de exemplo](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52).
* Um tema Adaptive Form. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes. Você pode [criar um novo tema](themes.md), [importar um tema existente](import-export-forms-templates.md#uploading-a-theme)ou baixe e importe alguns [temas de exemplo](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25).
* Adicione seus usuários a [!DNL forms-users] para fornecer permissões para criar um formulário adaptável. Para obter uma lista detalhada dos grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

## Criar um formulário adaptável {#strong-create-an-adaptive-form-strong}

Siga estas etapas para criar um formulário adaptável.

1. Acesso [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância do Cloud ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Selecione um modelo e toque em **[!UICONTROL Próximo]**.
1. Uma opção para **[!UICONTROL Adicionar propriedades]** é exibido. Especifique os valores para os seguintes campos de propriedade. Os campos Título e Nome são obrigatórios:

   * **[!UICONTROL Título:]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário no [!DNL Experience Manager Forms] interface do usuário.
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. À medida que você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Descrição:]** Especifica as informações detalhadas sobre o formulário.
   * **[!UICONTROL Tags:]** Especifica tags para identificar exclusivamente o formulário adaptável. As tags ajudam a pesquisar o formulário. Para criar tags, digite novos nomes de tag no **[!UICONTROL Tags]** caixa.

1. É possível criar um formulário adaptável com base em um dos seguintes modelos de formulário:

   * [Modelo de dados do formulário](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [Esquema XML ou JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nenhum ou sem qualquer modelo de formulário

   Você pode configurá-los no **[!UICONTROL Modelo de formulário]** na guia **[!UICONTROL Adicionar propriedades]** página. Por padrão, o modelo de formulário selecionado é **[!UICONTROL Nenhum]**.

1. Toque **[!UICONTROL Criar]**. Um formulário adaptável é criado, e uma caixa de diálogo para abrir o formulário para edição é exibida.

1. Toque **[!UICONTROL Abrir]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição e exibe o conteúdo disponível no modelo. Também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de formulário adaptável, os elementos de formulário presentes no <!--XFA form template, -->O esquema XML ou JSON são exibidos na variável **[!UICONTROL Objetos do modelo de dados]** da guia **[!UICONTROL Navegador de conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar o Formulário adaptável.

## Criar um formulário adaptável com base em um modelo de dados de formulário {#fdm}

[Integração de dados](data-integration.md) O permite integrar várias fontes de dados e unir suas entidades e serviços para criar um modelo de dados de formulário. É uma extensão do esquema JSON. Você pode usar um Modelo de dados de formulário para criar um Formulário adaptável. As entidades ou objetos de modelo de dados configurados em um Modelo de dados de formulário estão disponíveis como objetos de modelo de dados para a criação de formulário. Eles são vinculados às respectivas fontes de dados e usados para preencher previamente um formulário e gravar os dados enviados de volta nas respectivas fontes de dados. Você também pode chamar os serviços configurados em um Modelo de dados de formulário usando as regras do Formulário adaptável.

Para usar um Modelo de dados de formulário para criar um Formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades , selecione **[!UICONTROL Modelo de dados do formulário]** no **[!UICONTROL Selecionar de]** lista suspensa.

   ![Criar um formulário adaptável](assets/create-af-1-1.png)

1. Toque para expandir **[!UICONTROL Selecionar Modelo de Dados de Formulário]**. Todos os modelos de dados de formulário disponíveis são listados.Selecione um modelo de dados de formulário.

>[!NOTE]
>
>Também é possível alterar o Modelo de dados de formulário para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar as propriedades do Modelo de formulário de um formulário adaptável](#edit-form-model).

## Criar um formulário adaptável com base no esquema XML ou JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. Você pode associar um esquema a um Formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao Formulário adaptável. Os elementos do esquema estão disponíveis na guia Objeto do modelo de dados do navegador de conteúdo para a criação do Adaptive Forms. Você pode arrastar e soltar os elementos do esquema para criar o formulário.

Consulte os seguintes documentos para entender como projetar o esquema XML ou JSON para criar o Adaptive Forms.

* [Criando Forms adaptável usando esquema XML](adaptive-form-xml-schema-form-model.md)
* [Criação de Forms adaptável usando esquema JSON](adaptive-form-json-schema-form-model.md)

Faça o seguinte para usar o esquema XML ou JSON como modelo de formulário para um Formulário adaptável:

1. No **[!UICONTROL Adicionar propriedades]** etapa da página de criação do formulário adaptável, toque em **[!UICONTROL Modelo de formulário]** guia .
1. Na guia Modelo de formulário , selecione **[!UICONTROL Esquema]** do **[!UICONTROL Selecionar de]** campo suspenso .

1. Toque **[!UICONTROL Selecionar esquema]** e siga um destes procedimentos:

   * **[!UICONTROL Fazer upload do disco]** - Selecione esta opção e toque em Fazer upload da definição de esquema para procurar e fazer upload de um esquema XML ou JSON do seu sistema de arquivos. O arquivo de esquema carregado reside no formulário e não pode ser acessado por outro Adaptive Forms.
   * **[!UICONTROL Pesquisar no repositório]** - Selecione essa opção para selecionar na lista de arquivos de definição de esquema disponíveis no repositório. Selecione o arquivo de esquema XML ou JSON como modelo de formulário. O schema selecionado é associado ao formulário por referência e pode ser usado em outro Adaptive Forms.

      Certifique-se de que o nome de arquivo do esquema JSON termine com **.schema.json**. Por exemplo: mySchema.schema.json
   ![Seleção do esquema XML ou JSON](assets/upload-schema.png)
   **Figura:** *Seleção do esquema XML ou JSON*

1. (Somente para esquema XML) Após selecionar ou carregar um esquema XML, especifique um elemento raiz do arquivo XSD selecionado a ser mapeado com o formulário adaptável.

   ![Selecionar elemento raiz XSD](assets/xsd-root-element.png)
   **Figura:** *Selecionar elemento raiz XSD*

>[!NOTE]
>
>Também é possível alterar o esquema de um Formulário adaptável. Para obter etapas detalhadas, consulte [Editar as propriedades do Modelo de formulário de um formulário adaptável](#edit-form-model).

## Editar as propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

Os Forms adaptáveis são criados sem um modelo de formulário (usando a opção Nenhum para o modelo de formulário) ou usando um modelo de formulário, como um <!-- form template, --> Esquema XML, esquema JSON ou modelo de dados de formulário. É possível alterar o modelo de formulário para um formulário adaptável de Nenhum para outro modelo de formulário. Para o formulário adaptável baseado em um modelo de formulário, você pode escolher outro <!-- form template,--> Esquema XML, esquema JSON ou Modelo de dados de formulário para o mesmo modelo de formulário. No entanto, não é possível alterar de um modelo de formulário para outro.

1. Selecione o formulário adaptável e toque no **Propriedades** ícone .
1. Abra o **[!UICONTROL Modelo de formulário]** e faça o seguinte.

   * Se o formulário adaptável não tiver um modelo de formulário, é possível escolher outro modelo de formulário e, consequentemente, selecionar <!-- a form template, --> Esquema XML ou JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro <!-- form template, --> Esquema XML ou JSON ou Modelo de dados de formulário para o mesmo modelo de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.
