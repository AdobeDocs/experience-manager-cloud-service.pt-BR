---
title: Identificação de conteúdo a ser traduzido
description: Saiba como as regras de tradução identificam o conteúdo que precisa ser traduzido.
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: 0c75a367861c9e4c77ee537322fa49330c70db85
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 1%

---

# Identificação de conteúdo a ser traduzido {#identifying-content-to-translate}

As regras de tradução identificam o conteúdo a ser traduzido para páginas, componentes e ativos que estão incluídos ou excluídos de projetos de tradução. Quando uma página ou ativo está sendo traduzido, o AEM extrai esse conteúdo para que ele possa ser enviado ao serviço de tradução.

>[!TIP]
>
>Se você é novo em traduzir conteúdo, consulte nosso [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência de AEM ou tradução.

## Fragmentos de conteúdo e regras de tradução {#content-fragments}

As regras de tradução descritas neste documento se aplicam aos Fragmentos de conteúdo somente se a variável **Ativar campos do modelo de conteúdo para tradução** não foi ativada na [nível de configuração da estrutura de integração de tradução.](integration-framework.md#assets-configuration-properties)

Se a variável **Ativar campos do modelo de conteúdo para tradução** estiver ativa, AEM usará a variável **Traduzível** no campo [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md#properties) para determinar se o campo deve ser traduzido e cria automaticamente regras de tradução de acordo. Essa opção substitui qualquer regra de tradução criada e não requer nenhuma intervenção ou etapas adicionais.

Se você quiser usar regras de tradução para traduzir os Fragmentos de conteúdo, a variável **Ativar campos do modelo de conteúdo para tradução** a opção na configuração da estrutura de integração de tradução deve estar desativada e você precisa seguir as etapas descritas abaixo para criar suas regras.

## Visão geral {#overview}

As páginas e os ativos são representados como nós no repositório JCR. O conteúdo extraído é um ou mais valores de propriedade dos nós. As regras de tradução identificam as propriedades que contêm o conteúdo a ser extraído.

As regras de tradução são expressas em formato XML e armazenadas nesses locais possíveis:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

O arquivo se aplica a todos os projetos de tradução.

As regras incluem as seguintes informações:

* O caminho do nó ao qual a regra se aplica
   * A regra também se aplica aos descendentes do nó.
* Os nomes das propriedades do nó que contêm o conteúdo a ser traduzido
   * A propriedade pode ser específica para um tipo de recurso específico ou para todos os tipos de recurso.

Por exemplo, você pode criar uma regra que traduza o conteúdo que os autores adicionam a todos os componentes de texto nas suas páginas. A regra pode identificar a variável `/content` e o `text` para a `core/wcm/components/text/v2/text` componente.

Existe um [console](#translation-rules-ui) que foi adicionado para configurar regras de tradução. As definições na interface do usuário preencherão o arquivo para você.

Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](overview.md).

>[!NOTE]
>
>O AEM suporta o mapeamento de um para um entre os tipos de recursos e atributos de referência para a tradução do conteúdo referenciado em uma página.

## Sintaxe de regra para páginas, componentes e ativos {#rule-syntax-for-pages-components-and-assets}

Uma regra é `node` elemento com um ou mais filhos `property` elementos e zero ou mais filhos `node` elementos:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Cada um desses `node` Os elementos têm as seguintes características:

* O `path` contém o caminho para o nó raiz da ramificação à qual as regras se aplicam.
* Filho `property` Os elementos identificam as propriedades do nó a serem traduzidas para todos os tipos de recursos:
   * O `name` contém o nome da propriedade.
   * O `translate` atributo igual `false` se a propriedade não for traduzida. Por padrão, o valor é `true`. Esse atributo é útil ao substituir regras anteriores.
* Filho `node` Os elementos identificam as propriedades do nó a serem traduzidas para tipos de recursos específicos:
   * O `resourceType` contém o caminho que é resolvido para o componente que implementa o tipo de recurso.
   * Filho `property` Os elementos identificam a propriedade do nó a ser traduzida. Usar este nó da mesma forma que o filho `property` elementos para regras de nó.

A seguinte regra de exemplo causa o conteúdo de todos `text` propriedades a serem traduzidas para todas as páginas abaixo do `/content` nó . A regra é eficaz para qualquer componente que armazene conteúdo em um `text` , como o componente de texto.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

O exemplo a seguir traduz o conteúdo de todos `text` e também traduz outras propriedades do componente de imagem. Se outros componentes tiverem propriedades com o mesmo nome, a regra não se aplica a eles.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Sintaxe de regra para extração de ativos de páginas  {#rule-syntax-for-extracting-assets-from-pages}

Use a sintaxe de regra a seguir para incluir ativos incorporados ou referenciados de componentes:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Cada `assetNode` tem as seguintes características:

* One `resourceType` atributo que é igual ao caminho que é resolvido para o componente
* One `assetReferenceAttribute` atributo que é igual ao nome da propriedade que armazena o binário do ativo (para ativos incorporados) ou o caminho para o ativo referenciado

O exemplo a seguir extrai imagens do componente de imagem:

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## Substituição de regras {#overriding-rules}

O `translation_rules.xml` O arquivo consiste em um `nodelist` elemento com vários filhos `node` elementos. AEM lê a lista de nós de cima para baixo. Quando várias regras têm como alvo o mesmo nó, a regra que está menor no arquivo é usada. Por exemplo, as seguintes regras causam todo o conteúdo em `text` propriedades a serem traduzidas, exceto para `/content/mysite/en` ramificação de páginas:

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## Propriedades do filtro {#filtering-properties}

Você pode filtrar nós que têm uma propriedade específica usando um `filter` elemento.

Por exemplo, as seguintes regras causam todo o conteúdo em `text` propriedades a serem traduzidas, exceto para os nós que têm a propriedade `draft` defina como `true`.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interface das regras de tradução {#translation-rules-ui}

Um console também está disponível para configurar regras de tradução.

Para acessá-lo:

1. Navegar para **Ferramentas** e depois **Geral**.

1. Selecionar **Configuração de tradução**.

Na interface do usuário das regras de tradução, é possível:

1. **Adicionar contexto**, que permite adicionar um caminho.

   ![Adicionar contexto de tradução](../assets/add-translation-context.png)

1. Use o navegador de caminho para selecionar o contexto necessário e toque ou clique no **Confirmar** para salvar.

   ![Selecionar contexto](../assets/select-context.png)

1. Em seguida, é necessário selecionar o contexto e clicar em **Editar**. Isso abrirá o Editor de regras de tradução.

   ![Editor de regras de tradução](../assets/translation-rules-editor.png)

Há quatro atributos que você pode alterar por meio da interface do usuário:

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  é aplicável em filtros de nó e é verdadeiro por padrão. Verifica se o nó (ou seus ancestrais) contém essa propriedade com o valor da propriedade especificado no filtro. Se falso, ele só verifica o nó atual.

Por exemplo, nós filho são adicionados a um trabalho de tradução mesmo quando o nó pai tem a propriedade `draftOnly` definido como true para sinalizar o conteúdo de rascunho. Aqui `isDeep` entra em reprodução e verifica se os nós pai têm propriedade `draftOnly` como true e exclui esses nós filho.

No editor, você pode marcar/desmarcar **É Profundo** no **Filtros** guia .

![Regras de filtro](../assets/translation-rules-editor-filters.png)

Este é um exemplo do XML resultante quando **É Profundo** está desmarcada na interface do usuário:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### herdar {#inherit}

**`inherit`** é aplicável às propriedades. Por padrão, cada propriedade é herdada, mas se você quiser que alguma propriedade não seja herdada pelo filho, poderá marcar essa propriedade como false para que seja aplicada somente a esse nó específico.

Na interface do usuário, você pode marcar/desmarcar **Herdar** no **Propriedades** guia .

### traduzir {#translate}

**`translate`** é usada apenas para especificar se uma propriedade deve ser traduzida ou não.

Na interface do usuário, você pode marcar/desmarcar **Traduzir** no **Propriedades** guia .

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** é usado para propriedades que não têm texto, mas códigos de idioma, por exemplo `jcr:language`. O usuário não está traduzindo o texto, mas o idioma local da origem para o destino. Essas propriedades não são enviadas para tradução.

Na interface do usuário, você pode marcar/desmarcar **Traduzir** no **Propriedades** para modificar esse valor, mas para as propriedades específicas que têm códigos de idioma como valor.

Para ajudar a esclarecer a diferença entre `updateDestinationLanguage` e `translate`, este é um exemplo simples de um contexto com apenas duas regras:

![exemplo updateDestinationLanguage](../assets/translation-rules-updatedestinationlanguage.png)

O resultado no xml terá esta aparência:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Editar o arquivo de regras manualmente {#editing-the-rules-file-manually}

O `translation_rules.xml` O arquivo instalado com AEM contém um conjunto padrão de regras de tradução. Você pode editar o arquivo para atender aos requisitos dos seus projetos de tradução. Por exemplo, você pode adicionar regras para que o conteúdo dos componentes personalizados seja traduzido.

Se você editar o `translation_rules.xml` mantenha uma cópia de backup em um pacote de conteúdo. A reinstalação de determinados pacotes de AEM pode substituir o pacote atual `translation_rules.xml` com o original. Para restaurar as regras nessa situação, você pode instalar o pacote que contém sua cópia de backup.

>[!NOTE]
>
>Após criar o pacote de conteúdo, recrie-o sempre que editar o arquivo.

## Exemplo de arquivo de regras de tradução {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
