---
title: Seletor de destino para AEM as a Cloud Service
description: Use o Seletor de destino do AEM para mostrar e selecionar ativos que você pode usar como uma cópia do ativo original.
contentOwner: Adobe
role: Admin, User
exl-id: 7e7bc1ee-d580-4c88-b550-273e8b0620ba
feature: Selectors
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 34%

---

# Seletor de destino de micro front-end {#Overview}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

O Seletor de Destino de MicroFront-End fornece uma interface de usuário em seu aplicativo que se integra facilmente ao repositório [!DNL Experience Manager Assets as a Cloud Service]. Pesquise ou navegue até a pasta apropriada no repositório do [!DNL Experience Manager Assets as a Cloud Service] e carregue ativos do seu aplicativo.

A interface de usuário de MicroFront-End é disponibilizada em sua experiência de aplicativo usando o pacote do Seletor de destino. Quaisquer atualizações no pacote são automaticamente importadas e o Seletor de destino implantado mais recente é carregado automaticamente no aplicativo.

![Visão geral](assets/overview-destination-selector.png)

O Seletor de destino oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos Adobe ou não-Adobe usando a biblioteca JavaScript Vanilla.
* Fácil de manter, pois as atualizações do pacote do Seletor de destino são implantadas automaticamente no Seletor de destino disponível para seu aplicativo. Não há atualizações necessárias no aplicativo para carregar as modificações mais recentes.
* Facilidade de personalização, pois há propriedades disponíveis que controlam a exibição do Seletor de destino no aplicativo.
* Pesquisa de texto completo para navegar rapidamente até pastas para fazer upload de ativos do seu aplicativo.
* Capacidade de criar pastas, classificar pastas em ordem crescente ou decrescente e exibi-las na exibição de Lista, Grade, Galeria ou Cascata.

O escopo deste artigo é demonstrar como usar o Seletor de destino com um aplicativo [!DNL Adobe] no Unified Shell ou quando você já tiver um imsToken gerado para autenticação. Esses fluxos de trabalho são chamados de fluxo não SUSI neste artigo.

Execute as seguintes tarefas para integrar e usar o Seletor de destino com seu repositório [!DNL Experience Manager Assets as a Cloud Service]:

* [Integrar seletor de destino usando o Vanilla JS](#integration-with-vanilla-js)
* [Definir propriedades de exibição do Seletor de destino](#destination-selector-properties)
* [Usar seletor de destino](#using-destination-selector)

## Integrar seletor de destino usando o Vanilla JS {#integration-with-vanilla-js}

É possível integrar qualquer [!DNL Adobe] ou aplicativo fora da Adobe com o repositório [!DNL Experience Manager Assets] as a [!DNL Cloud Service] no aplicativo.

A integração é feita importando o pacote do Seletor de destino e se conectando ao Assets as a Cloud Service por meio da biblioteca JavaScript do Vanilla. Você deve editar um `index.html` ou qualquer arquivo apropriado em seu aplicativo para -

* Definir os detalhes de autenticação
* Acessar o repositório do Assets as a Cloud Service
* Configurar as propriedades de exibição do Seletor de destino

É possível executar a autenticação sem definir algumas das propriedades do IMS, se:

* Está integrando um aplicativo [!DNL Adobe] no [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=pt-BR).
* Você já tem um token IMS gerado para autenticação.

## Pré-requisitos {#prerequisites}

Defina os pré-requisitos no arquivo `index.html` ou em um arquivo semelhante na implementação do aplicativo para definir os detalhes de autenticação e acessar o repositório do [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Os pré-requisitos incluem:

* imsOrg
* imsToken
* apikey

## Instalação {#installation}

O Seletor de Destino está disponível por meio da CDN ESM (por exemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e da versão [UMD](https://github.com/umdjs/umd).

Nos navegadores usando a **Versão UMD** (recomendado):

Nos navegadores usando a **Versão UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Em navegadores com suporte a `import maps` usando a **Versão CDN do ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

No Deno/Webpack Module Federation usando a **Versão CDN do ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

### Destino selecionado {#selected-destination}

O Seletor de Destino recebe um retorno de chamada de `onItemSelect`, `onTreeToggleItem` ou `onTreeSelectionChange` com o diretório selecionado que contém o objeto (diretório, imagem, etc.).

**Sintaxe do esquema**

```
interface SelectedDestination {
  id: string;
  children: SelectedDestination[];
  'repo:repositoryId': string;
  'dc:format': string;
  'repo:assetClass': string;
  'storage:directoryType': string;
  'storage:region': string;
  'repo:name': string;
  'repo:path': string;
  'repo:ancestors': string[];
  'repo:createDate': string;
  'storage:assignee':

  { type: string; id: string; }
  ;
  'repo:assetId': string;
  'aem:published': boolean;
  'repo:createdBy': string;
  'repo:state': string;
  'repo:id': string;
  'repo:modifyDate': string;
  _page:

  { orderBy: string; count: number; };
}
```

A tabela a seguir descreve algumas das propriedades importantes do destino selecionado.

| Propriedade | Tipo | Explicação |
|---|---|---|
| *repo:repositoryId* | string | Identificador exclusivo do repositório onde o ativo está armazenado. |
| *repo:id* | string | Identificador exclusivo do ativo. |
| *repo:assetClass* | string | A classificação do ativo (por exemplo, imagem, vídeo ou documento). |
| *repo:name* | string | O nome do ativo, incluindo a extensão de arquivo. |
| *repo:size* | número | O tamanho do ativo em bytes. |
| *repo:path* | string | O local do ativo no repositório. |
| *repo:ancestors* | `Array<string>` | Uma matriz de itens ancestrais do ativo no repositório. |
| *repo:state* | string | Estado atual do ativo no repositório (Por exemplo, ativo, excluído etc.). |
| *repo:createdBy* | string | O usuário ou sistema que criou o ativo. |
| *repo:createDate* | string | A data e a hora em que o ativo foi criado. |
| *repo:modifiedBy* | string | O usuário ou sistema que modificou o ativo pela última vez. |
| *repo:modifyDate* | string | A data e a hora em que o ativo foi modificado pela última vez. |
| *dc:format* | string | O formato do ativo. |
| *_página* | orderBy: string; count: número; | Inclui o número de página do documento. |

Para obter uma lista completa de propriedades e um exemplo detalhado, visite [Exemplo de Código do Seletor de Destino](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### Exemplo para o fluxo não SUSI {#non-ims-vanilla}

Este exemplo demonstra como usar o Seletor de Destino com um fluxo não SUSI ao executar um aplicativo [!DNL Adobe] no Unified Shell ou quando você já tem `imsToken` gerado para autenticação.

Inclua o pacote do Seletor de destino no código usando a marca `script`, como mostrado nas _linhas 6-15_ do exemplo abaixo. Depois que o script é carregado, a variável global `PureJSSelectors` fica disponível para uso. Defina o Seletor de Destino [propriedades](#destination-selector-properties) conforme mostrado em _linhas 16-23_. As propriedades `imsOrg` e `imsToken` são necessárias para autenticação em um fluxo não SUSI. A propriedade `handleSelection` é usada para manipular os ativos selecionados. Para renderizar o Seletor de Destino, chame a função `renderDestinationSelector`, conforme mencionado em _linha 17_. O Seletor de Destino é exibido no elemento de contêiner `<div>`, conforme mostrado nas _linhas 21 e 22_.

Seguindo essas etapas, você pode usar o Seletor de Destino com um fluxo não SUSI no aplicativo [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Destination Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the DestinationSelector component
        const container = document.getElementById('destination-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const destinationSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderDestinationSelector` available in PureJSSelectors globals to render DestinationSelector
        PureJSSelectors.renderDestinationSelector(container, destinationselectorprops);
    </script>
</head>

<body>
    <div id="destination-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

Para obter um exemplo detalhado, visite [Exemplo de código do seletor de destino](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Usar propriedades do Seletor de destino {#destination-selector-properties}

Você pode usar as propriedades do Seletor de destino para personalizar a forma como o Seletor de destino é renderizado. A tabela a seguir lista as propriedades que podem ser usadas para personalizar e usar o Seletor de destino:

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| *imsOrg* | string | Sim | | A ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A chave `imsOrg` é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | string | Não | | Token de portador IMS usado para autenticação. `imsToken` não é necessário se você estiver usando o fluxo SUSI. No entanto, é obrigatório se você estiver usando o fluxo não-SUSI. |
| *apiKey* | string | Não | | Chave de API usada para acessar o serviço de Descoberta do AEM. `apiKey` não é necessário se você estiver usando o fluxo SUSI. No entanto, é obrigatório no fluxo não-SUSI. |
| *rootPath* | string | Não | /content/dam/ | Caminho da pasta onde o Seletor de destino exibe seus ativos. O `rootPath` também pode ser usado na forma de encapsulamento. Por exemplo, dado o seguinte caminho, `/content/dam/marketing/subfolder/`, o Seletor de Destino não permite que você percorra qualquer pasta pai, mas exibe apenas as pastas filho. |
| *hasMore* | booleano | Não | | Quando o aplicativo tiver mais conteúdo para exibir, você poderá usar essa propriedade para adicionar um carregador que carregue o conteúdo e torná-lo visível no aplicativo. É um indicador que indica que o carregamento do conteúdo está em andamento. |
| *orgName* | booleano | Não | | É o nome da organização (provavelmente orgID) associada ao AEM |
| *initRepoID* | string | Não | | É o caminho do repositório de ativos que você deseja usar em uma visualização inicial padrão |
| *onCreateFolder* | string | Não | | A propriedade `onCreateFolder` permite adicionar um ícone que adiciona uma nova pasta no aplicativo. |
| *onConfirm* | string | Não | | É um retorno de chamada quando você clica no botão confirmar. |
| *confirmDisabled* | string | Não | | Esta propriedade controla a alternância do botão de confirmação. |
| *viewType* | string | Não | | A propriedade `viewType` é usada para especificar os modos de exibição que você usa para exibir ativos. |
| *viewTypeOptions* | string | Não | | Esta propriedade está relacionada com a propriedade `viewType`. é possível especificar uma ou mais exibições para exibir ativos. As opções de tipo de exibição disponíveis são: Exibição em lista, Exibição em grade, Exibição em galeria, Exibição em cascata e Exibição em árvore. |
| *formadordenomeItem* | string | Não | | Essa propriedade permite formatar o nome do item |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |  | Se as traduções prontas para uso forem insuficientes para as necessidades do aplicativo, é possível expor uma interface pela qual poderá passar seus próprios valores localizados personalizados pela propriedade `i18nSymbols`. Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e usará suas próprias traduções.  Para executar a substituição, deverá transmitir um objeto [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que deseja substituir. |
| *ConfiguraçãoDeAlertaEmLinha* | string | Não | | Ele adiciona uma mensagem de alerta que você deseja passar no aplicativo. Por exemplo, adicionar uma mensagem de alerta de que Você não tem permissão para acessar essa pasta. |
| *intl* | Objeto | Não | | O Seletor de destino fornece traduções OOTB padrão. Você pode selecionar o idioma de tradução fornecendo uma string de idioma válida por meio da propriedade `intl.locale`. Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As strings de idioma com suporte seguem os padrões [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação de nomes de idiomas. </br></br> Lista de idiomas com suporte: Inglês - “en-us” (padrão) Espanhol - “es-es” Alemão - “de-de” Francês - “fr-fr” Italiano - “it-it” Japonês - “ja-jp” Coreano - “ko-kr” Português - “pt-br” Chinês (Tradicional) - “zh-cn” Chinês (Taiwan) - “zh-tw” |

## Exemplos para o uso de propriedades do Seletor de destino {#usage-examples}

Você pode definir as [propriedades](#destination-selector-properties) do Seletor de Destino no arquivo `index.html` para personalizar a exibição do Seletor de Destino no aplicativo.

### Exemplo 1: criar uma pasta no Seletor de destino

O Seletor de destino permite criar uma pasta para fazer upload, mover ou copiar ativos no local específico.

![criar-pasta-seletor-destino](assets/create-folder-destination-selector.png)

### Exemplo 2: especificar o tipo de exibição do Seletor de destino

O Seletor de destino exibe uma grande variedade de ativos em quatro exibições diferentes, incluindo a Exibição em lista, a Exibição em grade, a Exibição de galeria e a Exibição em cascata. Para especificar o tipo de exibição padrão, você pode usar a propriedade `viewType`. A propriedade `viewTypeOptions` é usada com a propriedade `viewType` para estipular outros tipos de exibição para que outras opções de tipo de exibição possam ser exibidas em uma lista suspensa. Um único argumento pode ser usado caso você queira que apenas uma opção seja exibida.

![viewtype-destination-seletor](assets/viewtype-destination-selector.png)

### Exemplo 3: caminho de inicialização da pasta do Assets

Use a propriedade `path` para definir o nome da pasta que é exibido automaticamente quando o Seletor de Destino é renderizado.

![inicializar-caminho-pasta](assets/initialize-folder-path.png)

## Utilização do seletor de destino {#using-destination-selector}

Depois que o Seletor de destino estiver configurado e você estiver autenticado para usar o Seletor de destino com seu [!DNL Adobe Experience Manager] como um aplicativo do [!DNL Cloud Service], será possível selecionar ativos ou executar várias outras operações para pesquisar seus ativos no repositório.

![usando-seletor-de-destino](assets/using-destination-selector.png)

* **A**: [Barra de pesquisa](#search-bar)
* **B**: [Classificação](#sorting)
* **C**: [Ativos](#assets-repo)
* **D**: [Adicionar sufixo ou prefixo](#add-suffix-or-prefix)
* **E**: [Criar nova pasta](#create-new-folder)
* **F**: [Exibir](#types-of-view)
* **G**: [Informações](#info)
* **H**: [Selecionar pasta](#select-folder)

### Barra de pesquisa {#search-bar}

O Seletor de destino permite executar uma pesquisa de texto completo dos ativos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os ativos com a palavra-chave `wave` mencionada em qualquer uma das propriedades de metadados serão exibidos.

### Classificação {#sorting}

Você pode classificar ativos no Seletor de destino por nome, dimensão ou tamanho de um ativo. Também é possível classificar os ativos em ordem crescente ou decrescente.

### Repositório do Assets {#assets-repo}

O Seletor de destino também permite exibir os dados do repositório de sua escolha disponíveis no aplicativo AEM. Você pode usar a propriedade `repositoryID` para inicializar o caminho da pasta de destino que deseja exibir na primeira instância do Seletor de Destino.

### Adicionar sufixo ou prefixo {#add-suffix-or-prefix}

É um exemplo da propriedade `optionsFormSetup`. Você pode usar isso para confirmar a seleção, ela é passada no evento `onConfirm`.

### Criar uma pasta {#create-new-folder}

Ele permite criar uma pasta na pasta de destino do seu [!DNL Adobe Experience Manager] como [!DNL Cloud Service].

### Tipos de visualização {#types-of-view}

O Seletor de destino permite exibir o ativo em quatro exibições diferentes:

* **![exibição em lista](assets/do-not-localize/list-view.png) [!UICONTROL Exibição em lista]**: a exibição em lista exibe arquivos e pastas roláveis em uma única coluna.
* **![exibição em grade](assets/do-not-localize/grid-view.png) [!UICONTROL Exibição em grade]**: a exibição em grade exibe arquivos e pastas roláveis em uma grade de linhas e colunas.
* **![exibição em galeria](assets/do-not-localize/gallery-view.png) [!UICONTROL Exibição em galeria]**: a exibição em galeria exibe arquivos ou pastas em uma lista horizontal com bloqueio central.
* **![exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Exibição em cascata]**: a exibição em cascata exibe arquivos ou pastas no formato de uma ponte.

### Informações {#info}

O ícone de informações ou informações permite visualizar metadados do ativo selecionado. Ele inclui vários detalhes, como dimensões, tamanho, descrição, caminho, data de modificação e data de criação. As informações de metadados são fornecidas ao fazer upload, copiar ou criar um ativo.

### Selecionar pasta {#select-folder}

O botão Selecionar pasta permite selecionar ativos para executar várias operações associadas às [propriedades](#destination-selector-properties) no seletor de destino.
