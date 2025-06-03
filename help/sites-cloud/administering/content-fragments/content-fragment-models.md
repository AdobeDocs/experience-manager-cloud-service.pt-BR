---
title: Definição de Modelos de fragmentos de conteúdo
description: Saiba como os modelos de fragmento de conteúdo servem como base para os fragmentos de conteúdo no AEM, permitindo criar conteúdo estruturado para uso em entrega headless ou criação de página.
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: cf2f64dec2ff39ea237dd092b3049bf9b8cd40e7
workflow-type: tm+mt
source-wordcount: '2280'
ht-degree: 36%

---

# Definição de Modelos de fragmentos de conteúdo {#defining-content-fragment-models}

Os modelos de fragmento de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service definem a estrutura do conteúdo dos seus [fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md). Esses fragmentos podem ser usados para criação de página ou como base para o conteúdo headless.

Esta página aborda como definir o modelo de fragmento de conteúdo usando o editor dedicado. Consulte [Gerenciamento de modelos de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) para obter mais tarefas e opções disponíveis após a criação dos fragmentos, incluindo [ações disponíveis no Console de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#actions), [permissão do modelo na sua pasta](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder) e [publicação do seu modelo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model).

>[!CAUTION]
>
>Se você estiver consultando vários fragmentos referenciados, não é recomendável que os vários modelos de fragmento tenham nomes de campo com o mesmo nome, mas tipos diferentes.
>
>Para obter mais detalhes, consulte a [API do AEM GraphQL para uso com Fragmentos de conteúdo - Limitações](/help/headless/graphql-api/content-fragments.md#limitations)

## Definição do Modelo de fragmento de conteúdo {#defining-your-content-fragment-model}

O modelo de fragmento de conteúdo define efetivamente a estrutura dos fragmentos de conteúdo resultantes usando uma seleção de **[Tipos de dados](#data-types)**. Usando o editor do modelo, é possível adicionar instâncias dos tipos de dados e configurá-las para criar os campos necessários:

>[!CAUTION]
>
>A edição de um modelo que já é usado pelos Fragmentos de conteúdo existentes pode afetar esses fragmentos dependentes.

1. No Console de fragmentos de conteúdo, selecione o painel para [Modelos de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#basic-structure-handling-content-fragment-models-console) e navegue até a pasta que contém seu modelo de fragmento de conteúdo.

   >[!NOTE]
   >
   >Você também pode abrir um modelo diretamente após [criá-lo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).

1. Abra o modelo necessário para **Edição**; use a ação rápida ou selecione o modelo e depois a ação na barra de ferramentas.

   Uma vez aberto, o editor de modelo mostra:

   * à esquerda: campos já definidos
   * à direita: **Tipos de dados** disponíveis para criar campos (e **Propriedades** para uso depois que os campos forem criados)

   >[!NOTE]
   >
   >Quando um campo é definido como **Obrigatório**, o **Rótulo** indicado no painel à esquerda é marcado com um asterisco (**&#42;**).

   ![Propriedades](assets/cf-cfmodels-empty-model.png)

1. **Para adicionar um campo**

   * Arraste um tipo de dados necessário para o local exigido de um campo:

     ![Arraste o tipo de dados para criar o campo](assets/cf-cfmodels-create-field.png)

   * Depois que um campo é adicionado ao modelo, o painel direito mostra as **Propriedades** que podem ser definidas para esse tipo de dados específico. Aqui é possível definir o que é necessário para esse campo.

      * Muitas propriedades são autoexplicativas. Para obter mais detalhes, consulte [Propriedades (Tipos de Dados)](#properties).
      * Digitar um **Rótulo de Campo** preenche automaticamente o **Nome da Propriedade**, se estiver vazio, e pode ser atualizado manualmente posteriormente.

        >[!CAUTION]
        >
        >Ao atualizar manualmente a propriedade **Nome da Propriedade** para um tipo de dados, os nomes devem conter *somente* A-Z, a-z, 0-9 e um sublinhado &quot;_&quot; como caractere especial.
        >
        >Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.

     Por exemplo:

     ![Propriedades do campo](assets/cf-cfmodels-field-properties.png)

1. **Para remover um campo**

   Selecione o campo obrigatório e, em seguida, o ícone da lixeira. Você receberá uma solicitação para confirmar a ação.

   ![Remover](assets/cf-cfmodels-remove-icon.png)

1. Adicione todos os campos obrigatórios e defina as propriedades relacionadas, conforme necessário. Por exemplo:

   ![Salvar](assets/cf-cfmodels-save.png)

1. Selecione **Salvar** para salvar a definição.

## Tipos de dados {#data-types}

Uma variedade de tipos de dados está disponível para a definição do seu modelo:

* **Texto em linha única**
   * Adicionar um campo para uma única linha de texto; o comprimento máximo pode ser definido
   * O campo pode ser configurado para permitir que os autores de fragmento criem novas instâncias do campo

* **Texto multilinha**
   * Uma área de texto que pode ser Rich Text, Texto sem formatação ou Markdown
   * O campo pode ser configurado para permitir que os autores de fragmento criem novas instâncias do campo

  >[!NOTE]
  >
  >Se a área de texto é Rich Text, Texto sem formatação ou Markdown, é definida no modelo pela propriedade **Tipo padrão**.
  >
  >Este formato não pode ser alterado do [editor de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md), mas somente do Modelo.

* **Número**
   * Adicionar um campo numérico
   * O campo pode ser configurado para permitir que os autores de fragmento criem novas instâncias do campo

* **Booleano**
   * Adicionar uma caixa de seleção booleana

* **Data e hora**
   * Adicionar um campo de data e/ou hora

* **Enumeração**
   * Adicionar um conjunto de caixas de seleção, botões de opção ou campos suspensos
      * É possível especificar as opções disponíveis para o autor do fragmento

* **Tags**
   * Permite que os autores de fragmentos acessem e selecionem áreas de tags
* **Referência do fragmento**
   * Faz referência a outros fragmentos de conteúdo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * O tipo de dados pode ser configurado para permitir que os autores de fragmento:
      * Editem o fragmento referenciado diretamente.
      * Crie um novo Fragmento de conteúdo, com base no modelo apropriado
      * Criar novas instâncias do campo
   * A referência especifica o caminho para o recurso referenciado; por exemplo `/content/dam/path/to/resource`

* **Referência de fragmento (UUID)**
   * Faz referência a outros fragmentos de conteúdo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * O tipo de dados pode ser configurado para permitir que os autores de fragmento:
      * Editem o fragmento referenciado diretamente.
      * Crie um novo Fragmento de conteúdo, com base no modelo apropriado
      * Criar novas instâncias do campo
   * No editor, a referência especifica o caminho para o recurso referenciado; internamente, a referência é mantida como uma ID universalmente exclusiva (UUID) que faz referência ao recurso
      * Não é necessário conhecer a UUID; no editor de fragmentos, é possível navegar até o fragmento necessário

  >[!NOTE]
  >
  >Os UUIDs são específicos do repositório. Se você usar a [Ferramenta de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) para copiar fragmentos de conteúdo, as UUIDs serão recalculadas no ambiente de destino.

* **Referência de conteúdo**
   * Faz referência a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * Se uma imagem for referenciada, você pode optar por mostrar uma miniatura
   * O campo pode ser configurado para permitir que os autores de fragmento criem novas instâncias do campo
   * A referência especifica o caminho para o recurso referenciado; por exemplo `/content/dam/path/to/resource`

* **Referência de conteúdo (UUID)**
   * Faz referência a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * Se uma imagem for referenciada, você pode optar por mostrar uma miniatura
   * O campo pode ser configurado para permitir que os autores de fragmento criem novas instâncias do campo
   * No editor, a referência especifica o caminho para o recurso referenciado; internamente, a referência é mantida como uma ID universalmente exclusiva (UUID) que faz referência ao recurso
      * Não é necessário conhecer a UUID; no editor de fragmentos, é possível navegar até o recurso de ativo necessário

  >[!NOTE]
  >
  >Os UUIDs são específicos do repositório. Se você usar a [Ferramenta de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) para copiar fragmentos de conteúdo, as UUIDs serão recalculadas no ambiente de destino.

* **Objeto JSON**
   * Permite que o autor do Fragmento de conteúdo insira a sintaxe JSON nos elementos correspondentes de um fragmento.
      * Para permitir que o AEM armazene o JSON direto que você tenha copiado/colado de outro serviço.
      * O JSON será transmitido e emitido como JSON no GraphQL.
      * Inclui o realce da sintaxe JSON, o preenchimento automático e o realce de erros no editor de Fragmento de conteúdo.

* **Espaço reservado da guia**
   * Permite a introdução de guias para uso ao editar o conteúdo do fragmento de conteúdo.
      * Eles são mostrados como divisores no editor de modelo, separando seções da lista de tipos de dados de conteúdo. Cada instância representa o início de uma nova guia.
      * No editor de fragmentos, cada instância aparece como uma guia.

     >[!NOTE]
     >
     >Esse tipo de dados é usado apenas para formatação e é ignorado pelo esquema GraphQL do AEM.

## Propriedades (Tipos de dados) {#properties}

Muitas propriedades são autoexplicativas. Para certas propriedades, os detalhes adicionais são os seguintes:

* **Nome da Propriedade**

  Ao atualizar manualmente essa propriedade para um tipo de dados, os nomes **devem** conter *somente* A-Z, a-z, 0-9 e o sublinhado &quot;_&quot; como caractere especial.

  >[!CAUTION]
  >
  >Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.

* **Renderizar como**

  As várias opções para realizar/renderizar o campo em um fragmento. Geralmente, isso permite definir se o autor verá uma única instância do campo ou se poderá criar várias instâncias. Quando **Vários Campos** for usado, você poderá definir o número mínimo e máximo de itens - consulte [Validação](#validation) para obter mais detalhes.

* **Rótulo do campo**
Inserir um **Rótulo de Campo** gera automaticamente um **Nome de Propriedade**, que pode ser atualizado manualmente se necessário.

* **Validação**
A validação básica está disponível por meio de mecanismos como a propriedade **Obrigatório**. Alguns tipos de dados têm campos de validação de adição. Consulte [Validação](#validation) para obter mais detalhes.

* No tipo de dados **Texto multilinha**, é possível definir o **Tipo padrão** como:

   * **Rich Text**
   * **Markdown**
   * **Texto sem formatação**

  Se não for especificado, o valor padrão **Rich Text** é usado para esse campo.

  Alterar o **Tipo padrão** em um modelo de Fragmento de conteúdo só terá efeito em um Fragmento de conteúdo existente relacionado depois que esse fragmento for aberto no editor e salvo.

* **Exclusivo**
O conteúdo (para o campo específico) deve ser exclusivo em todos os fragmentos de conteúdo criados a partir do modelo atual.

  Isso é usado para garantir que os autores de conteúdo não possam repetir o conteúdo já adicionado em outro fragmento do mesmo modelo.

  Por exemplo, um campo **Texto de linha única** chamado de `Country` no modelo de fragmento de conteúdo não pode ter o valor `Japan` em dois fragmentos de conteúdo dependentes. Um aviso será emitido na tentativa da segunda instância.

  >[!NOTE]
  >
  >A exclusividade é assegurada por raiz de idioma.

  >[!NOTE]
  >
  >As variações podem ter o mesmo valor *exclusivo* como variações do mesmo fragmento, mas não o mesmo valor usado em qualquer variação de outros fragmentos.

* Consulte **[Referência de conteúdo](#content-reference)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

* Consulte **[Referência de fragmento (fragmentos aninhados)](#fragment-reference-nested-fragments)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

* **Traduzível**

  Marcar a caixa de seleção **Traduzível** em um campo no editor do modelo de fragmento de conteúdo:

   * Garantirá que o nome da propriedade do campo seja adicionado à configuração de tradução, no contexto `/content/dam/<sites-configuration>`, se ainda não estiver presente.
   * Para GraphQL: definirá uma propriedade `<translatable>` no campo Fragmento de conteúdo para `yes`, permitindo o uso do filtro de consulta GraphQL para saída de JSON somente para conteúdo traduzível.

## Validação {#validation}

Vários tipos de dados agora incluem a possibilidade de definir requisitos de validação para quando o conteúdo é inserido no fragmento resultante:

* **Texto em linha única**
   * Comparar com uma expressão regular predefinida.
* **Número**
   * Verificar valores específicos.
* **Referência de conteúdo**
   * Testar tipos específicos de conteúdo.
   * Somente ativos de tamanho de arquivo especificado ou menores podem ser referenciados.
   * Somente imagens dentro de um intervalo predefinido de largura e/ou altura (em pixels) podem ser referenciadas.
* **Referência do fragmento**
   * Testar um modelo de Fragmento de conteúdo específico.
* **Número mínimo de itens** / **Número máximo de itens**

  Os campos que foram definidos como **Vários Campos** (definidos com **Renderizar como**) têm as seguintes opções:

   * **Número mínimo de itens**
   * **Número Máximo de Itens**

  Eles são validados no [Editor de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md).

## Usar referências para formar conteúdo aninhado {#using-references-to-form-nested-content}

Os fragmentos de conteúdo podem formar conteúdo aninhado, usando um dos seguintes tipos de dados:

* [Referência de conteúdo](#content-reference)
   * Fornece uma referência simples a outro conteúdo, de qualquer tipo.
   * Fornecidos pelos tipos de dados:
      * **Referência de conteúdo** - baseada em caminho
      * **Referência de conteúdo (UUID)** - baseada em UUID
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

* [Referência de fragmento](#fragment-reference-nested-fragments) (fragmentos aninhados)
   * Faz referência a outros fragmentos, dependendo dos modelos especificados.
   * Fornecidos pelos tipos de dados:
      * **Referência de fragmento** - baseada em caminho
      * **Referência de fragmento (UUID)** - baseada em UUID
   * Permite incluir/recuperar dados estruturados.

     >[!NOTE]
     >
     >Este método é especialmente interessante quando você está usando a [Entrega de conteúdo headless usando fragmentos de conteúdo com o GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

>[!NOTE]
>
>Consulte [Atualizar os fragmentos de conteúdo para referências UUID](/help/headless/graphql-api/uuid-reference-upgrade.md) para obter mais informações sobre a referência de conteúdo/fragmento e a referência de conteúdo/fragmento (UUID), além de atualizar para os tipos de dados baseados em UUID.

>[!NOTE]
>
>O AEM tem proteção de recorrência para:
>
>* Referências de conteúdo
>Isso impede que o usuário adicione uma referência ao fragmento atual e pode levar a uma caixa de diálogo vazia do seletor de Referência de fragmento.
>
>* Referências de fragmento no GraphQL
>Se você criar uma consulta profunda que retorna vários Fragmentos de conteúdo referenciados entre si, ela retornará um valor nulo na primeira ocorrência.

>[!CAUTION]
>
>Se você estiver consultando vários fragmentos referenciados, não é recomendável que os vários modelos de fragmento tenham nomes de campo com o mesmo nome, mas tipos diferentes.
>
>Para obter mais detalhes, consulte a [API do AEM GraphQL para uso com Fragmentos de conteúdo - Limitações](/help/headless/graphql-api/content-fragments.md#limitations)

### Referência de conteúdo {#content-reference}

Os tipos de dados **Referência de Conteúdo** e **Referência de Conteúdo (UUID)** permitem renderizar o conteúdo de outra fonte; por exemplo, imagem, página ou Fragmento de Experiência.

Além das propriedades padrão, é possível especificar:

* O **Caminho Raiz**, que especifica ou representa onde armazenar qualquer conteúdo referenciado
  >[!NOTE]
  >
  >Isso é obrigatório se você quiser fazer upload diretamente e fazer referência a imagens nesse campo ao usar o editor de fragmentos de conteúdo.
  >
  >Consulte [Referenciar imagens](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images) para obter mais detalhes.

* Os tipos de conteúdo que podem ser referenciados
  >[!NOTE]
  >
  >Eles devem incluir **Imagem** se você quiser carregar e fazer referência diretamente a imagens nesse campo ao usar o editor de Fragmento de conteúdo.
  >
  >Consulte [Referenciar imagens](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images) para obter mais detalhes.

* Limitações para tamanhos de arquivo
* Se uma imagem for referenciada:
   * Mostrar miniatura
   * Restrições de altura e largura da imagem

![Referência de conteúdo](assets/cf-cfmodels-content-reference.png)

### Referência de fragmento (fragmentos aninhados) {#fragment-reference-nested-fragments}

Os tipos de dados **Referência de Fragmento** e **Referência de Fragmento (UUID)** podem fazer referência a um ou mais Fragmentos de Conteúdo. Esse recurso é especialmente interessante ao recuperar conteúdo para uso no aplicativo, pois permite recuperar dados estruturados com várias camadas.

Por exemplo:

* Um modelo que define os detalhes de um funcionário, incluindo:
   * Uma referência ao modelo que define o empregador (empresa)

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
>As Referências de fragmento são de especial interesse para [Entrega de conteúdo headless usando fragmentos de conteúdo com o GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

Além das propriedades padrão, você pode definir:

* **Renderizar como**:

   * **multifield** — o autor do fragmento pode criar várias referências individuais

   * **fragmentreference** — permite que o autor do fragmento selecione uma única referência a um fragmento

* **Tipo de modelo**
Vários modelos podem ser selecionados. Ao adicionar referências a um fragmento de conteúdo, todos os fragmentos referenciados devem ter sido criados usando esses modelos.

* **Caminho raiz**
Especifica ou representa um caminho raiz para qualquer fragmento referenciado.

* **Permitir criação de fragmentos**

  Isso permite que o autor do fragmento crie um fragmento com base no modelo apropriado.

   * **fragmentreferencecomposite** — permite que o autor do fragmento crie uma composição ao selecionar vários fragmentos

  ![Referência do fragmento](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
>Um mecanismo de proteção contra recorrências está em vigor. Ele proíbe que o usuário selecione o fragmento de conteúdo atual na referência do fragmento e pode levar a uma caixa de diálogo vazia do seletor de referência de fragmento.
>
>Também há proteção de recorrência para referências de fragmento no GraphQL. Se você criar uma consulta profunda em dois Fragmentos de conteúdo que fazem referência um ao outro, ela retornará um valor nulo.
