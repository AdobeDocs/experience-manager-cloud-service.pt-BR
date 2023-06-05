---
title: Seletor de destino para AEM as a Cloud Service
description: Use o Seletor de destino do AEM para mostrar e selecionar ativos que você pode usar como uma cópia do ativo original.
contentOwner: Adobe
role: Admin,User
source-git-commit: d6ea74834f73ad90f5df929a2806cd1ed53af0aa
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 3%

---


# Seletor de destino de micro front-end {#Overview}

O Seletor de destino de micro front-end fornece uma interface do usuário em seu aplicativo que se integra facilmente ao [!DNL Experience Manager Assets as a Cloud Service] repositório. Você pode pesquisar ou navegar até a pasta apropriada no [!DNL Experience Manager Assets as a Cloud Service] repositório e upload de ativos do seu aplicativo.

A interface de usuário de MicroFront-End é disponibilizada em sua experiência de aplicativo usando o pacote do Seletor de destino. Quaisquer atualizações no pacote são automaticamente importadas e o Seletor de destino implantado mais recente é carregado automaticamente no aplicativo.

![Visão geral](assets/overview-destination-selector.png)

O Seletor de destino oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos Adobe ou não-Adobe usando a biblioteca JavaScript Vanilla.
* Fácil de manter, pois as atualizações do pacote do Seletor de destino são implantadas automaticamente no Seletor de destino disponível para seu aplicativo. Não há atualizações necessárias no aplicativo para carregar as modificações mais recentes.
* Facilidade de personalização, pois há propriedades disponíveis que controlam a exibição do Seletor de destino no aplicativo.
* Pesquisa de texto completo para navegar rapidamente até pastas para fazer upload de ativos do seu aplicativo.
* Capacidade de criar pastas, classificar pastas em ordem crescente ou decrescente e exibi-las na exibição de Lista, Grade, Galeria ou Cascata.

O escopo deste artigo é demonstrar como usar o Seletor de destino com uma [!DNL Adobe] aplicativo no Unified Shell ou quando você já tiver um imsToken gerado para autenticação. Esses workflows são chamados de fluxo não SUSI neste artigo.

Execute as seguintes tarefas para integrar e usar o Seletor de destino com seu [!DNL Experience Manager Assets as a Cloud Service] repositório:

* [Integrar seletor de destino usando o Vanilla JS](#integration-with-vanilla-js)
* [Definir propriedades de exibição do Seletor de destino](#destination-selector-properties)
* [Usar seletor de destino](#using-destination-selector)

## Integrar seletor de destino usando o Vanilla JS {#integration-with-vanilla-js}

É possível integrar qualquer [!DNL Adobe] ou aplicativo não-Adobe com [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repositório e selecione os ativos no aplicativo.

A integração é feita importando o pacote do Seletor de destino e se conectando aos Ativos as a Cloud Service por meio da biblioteca JavaScript do Vanilla. É necessário editar um `index.html` ou qualquer arquivo apropriado em seu aplicativo para -
* Definir os detalhes de autenticação
* Acessar o repositório as a Cloud Service do Assets
* Configurar as propriedades de exibição do Seletor de destino

É possível executar a autenticação sem definir algumas das propriedades do IMS, se:

* Você está integrando um [!DNL Adobe] aplicativo ativado [Shell unificado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* Você já tem um token IMS gerado para autenticação.

## Pré-requisitos {#prerequisites}

Defina os pré-requisitos no `index.html` arquivo ou um arquivo semelhante na implementação do aplicativo para definir os detalhes de autenticação para acessar o [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repositório. Os pré-requisitos incluem:
* imsOrg
* imsToken
* apikey

## Instalação {#installation}

O Seletor de destino está disponível por meio da CDN do ESM (por exemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e [UMD](https://github.com/umdjs/umd) versão.

Nos navegadores usando **Versão do UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderDestinationSelector } = PureJSSelectors;
</script>
```

Em navegadores com `import maps` suporte usando **Versão do ESM CDN**:

```
<script type="module">
  import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

Na Federação do módulo Deno/Webpack usando o **Versão do ESM CDN**:

```
import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### Destino selecionado {#selected-destination}

O Seletor de destino recebe uma chamada de retorno de `onItemSelect`, `onTreeToggleItem`ou `onTreeSelectionChange` com o diretório selecionado que contém o objeto (diretório, imagem e assim por diante).

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
| *repositório:repositoryId* | string | Identificador exclusivo do repositório onde o ativo está armazenado. |
| *repositório:id* | string | Identificador exclusivo do ativo. |
| *repo:assetClass* | string | A classificação do ativo (por exemplo, imagem ou vídeo, documento). |
| *repositório:nome* | string | O nome do ativo, incluindo a extensão de arquivo. |
| *repositório:tamanho* | número | O tamanho do ativo em bytes. |
| *repositório:caminho* | string | O local do ativo no repositório. |
| *repositório:antecessores* | `Array<string>` | Uma matriz de itens ancestrais para o ativo no repositório. |
| *repositório:estado* | string | Estado atual do ativo no repositório (Por exemplo, ativo, excluído etc.). |
| *repositório:createdBy* | string | O usuário ou sistema que criou o ativo. |
| *repo:createDate* | string | A data e a hora em que o ativo foi criado. |
| *repositório:modifiedBy* | string | O usuário ou sistema que modificou o ativo pela última vez. |
| *repo:modifyDate* | string | A data e a hora em que o ativo foi modificado pela última vez. |
| *dc:format* | string | O formato do ativo. |
| *_página* | orderBy: string; count: número; | Inclui o número de página do documento. |

Para obter uma lista completa das propriedades e um exemplo detalhado, visite [Exemplo de código do seletor de destino](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### Exemplo para o fluxo não-SUSI {#non-ims-vanilla}

Este exemplo demonstra como usar o Seletor de destino com um fluxo não SUSI ao executar um [!DNL Adobe] aplicativo no Unified Shell ou quando você já tiver `imsToken` gerado para autenticação.

Inclua o pacote do Seletor de destino no código usando o `script` tag, conforme mostrado em _linhas 6 a 15_ do exemplo abaixo. Depois que o script for carregado, a variável `PureJSSelectors` A variável global está disponível para uso. Definir o seletor de destino [propriedades](#destination-selector-properties) conforme mostrado em _linhas 16 a 23_. A variável `imsOrg` e `imsToken` As propriedades são necessárias para autenticação em um fluxo não-SUSI. A variável `handleSelection` propriedade é usada para manipular os ativos selecionados. Para renderizar o Seletor de destino, chame o `renderDestinationSelector` como mencionado no _linha 17_. O Seletor de destino é exibido no `<div>` elemento de contêiner, conforme mostrado em _linhas 21 e 22_.

Ao seguir essas etapas, é possível usar o Seletor de destino com um fluxo não SUSI no [!DNL Adobe] aplicação.

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
| *imsOrg* | string | Sim |  | ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A variável `imsOrg` A chave é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | string | Não |  | Token de portador IMS usado para autenticação. `imsToken` não é necessário se você estiver usando o fluxo SUSI. No entanto, é obrigatório se você estiver usando o fluxo não-SUSI. |
| *apiKey* | string | Não |  | Chave de API usada para acessar o serviço de Descoberta do AEM. `apiKey` não é necessário se você estiver usando o fluxo SUSI. No entanto, é obrigatório no fluxo não-SUSI. |
| *rootPath* | string | Não | /content/dam/ | Caminho da pasta onde o Seletor de destino exibe seus ativos. `rootPath` também podem ser usados na forma de encapsulamento. Por exemplo, dado o seguinte caminho, `/content/dam/marketing/subfolder/`, o Seletor de destino não permite que você percorra qualquer pasta pai, mas exibe apenas as pastas filho. |
| *hasMore* | booleano | Não |  | Quando o aplicativo tiver mais conteúdo para exibir, você poderá usar essa propriedade para adicionar um carregador que carregue o conteúdo e torná-lo visível no aplicativo. É um indicador que indica que o carregamento do conteúdo está em andamento. |
| *orgName* | booleano | Não |  | É o nome da organização (provavelmente orgID) associada ao AEM |
| *initRepoID* | string | Não |  | É o caminho do repositório de ativos que você deseja usar em uma visualização inicial padrão |
| *onCreateFolder* | string | Não |  | A variável `onCreateFolder` permite adicionar um ícone que adiciona uma nova pasta no aplicativo. |
| *onConfirm* | string | Não |  | É um retorno de chamada quando você clica no botão confirmar. |
| *confirmDisabled* | string | Não |  | Esta propriedade controla a alternância do botão de confirmação. |
| *viewType* | string | Não |  | A variável `viewType` A propriedade é usada para especificar as exibições usadas para exibir ativos. |
| *viewTypeOptions* | string | Não |  | Esta propriedade está relacionada com `viewType` propriedade. é possível especificar uma ou mais exibições para exibir ativos. As opções de tipo de exibição disponíveis são: Exibição em lista, Exibição em grade, Exibição em galeria, Exibição em cascata e Exibição em árvore. |
| *itemNameFormatter* | string | Não |  | Essa propriedade permite formatar o nome do item |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |  | Se as traduções OOTB forem insuficientes para as necessidades do aplicativo, você poderá expor uma interface pela qual poderá passar seus próprios valores localizados personalizados pela `i18nSymbols` prop Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e, em vez disso, usa suas próprias traduções.  Para executar a substituição, você deve passar um [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que você deseja substituir. |
| *inlineAlertSetup* | string | Não |  | Ele adiciona uma mensagem de alerta que você deseja passar no aplicativo. Por exemplo, adicionar uma mensagem de alerta de que Você não tem permissão para acessar essa pasta. |
| *intl* | Objeto | Não |  | O Seletor de destino fornece traduções OOTB padrão. Você pode selecionar o idioma de tradução fornecendo uma cadeia de caracteres de localidade válida por meio da `intl.locale` prop Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As cadeias de caracteres de local com suporte seguem o [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação dos nomes das normas linguísticas. </br></br> Lista de locais com suporte: Inglês - &#39;en-us&#39; (padrão) Espanhol - &#39;es-es&#39; Alemão - &#39;de-de&#39; Francês - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonês - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Português - &#39;pt-br&#39; Chinês (Tradicional) - &#39;zh-cn&#39; Chinês (Taiwan) - &#39;zh-tw&#39; |

## Exemplos para o uso de propriedades do Seletor de destino {#usage-examples}

É possível definir o Seletor de destino [propriedades](#destination-selector-properties) no `index.html` arquivo para personalizar a exibição do Seletor de destino no aplicativo.

### Exemplo 1: criar uma pasta no Seletor de destino

O Seletor de destino permite criar uma nova pasta para fazer upload, mover ou copiar ativos no local específico.

![create-folder-destination-seletor](assets/create-folder-destination-selector.png)

### Exemplo 2: especificar o tipo de exibição do Seletor de destino

O Seletor de destino exibe uma grande variedade de ativos em quatro exibições diferentes, incluindo a Exibição em lista, a Exibição em grade, a Exibição de galeria e a Exibição em cascata. Para especificar o tipo de exibição padrão, é possível usar `viewType` propriedade. A variável `viewTypeOptions` propriedade é usada junto com `viewType` propriedade para estipular outros tipos de exibição para que outras opções de tipo de exibição possam ser exibidas em uma lista suspensa. Um único argumento pode ser usado caso você queira que apenas uma opção seja exibida.

![viewtype-destination-seletor](assets/viewtype-destination-selector.png)

### Exemplo 3: inicializar o caminho da pasta de ativos

Use o `path` para definir o nome da pasta que é exibido automaticamente quando o Seletor de destino é renderizado.

![initialize-folder-path](assets/initialize-folder-path.png)

## Utilização do seletor de destino {#using-destination-selector}

Depois que o Seletor de destino estiver configurado e você estiver autenticado para usar o Seletor de destino com sua [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] , você pode selecionar ativos ou executar várias outras operações para pesquisar seus ativos no repositório.

![using-destination-seletor](assets/using-destination-selector.png)

* **A**: [Barra de pesquisa](#search-bar)
* **B**: [Classificação](#sorting)
* **C**: [Assets](#assets-repo)
* **D**: [Adicionar sufixo ou prefixo](#add-suffix-or-prefix)
* **E**: [Criar nova pasta](#create-new-folder)
* **F**: [Exibir](#types-of-view)
* **G**: [Informações](#info)
* **H**: [Selecionar pasta](#select-folder)

### Barra de pesquisa {#search-bar}

O Seletor de destino permite executar uma pesquisa de texto completo dos ativos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os ativos com a variável `wave` a palavra-chave mencionada em qualquer uma das propriedades de metadados é exibida.

### Classificação {#sorting}

Você pode classificar ativos no Seletor de destino por nome, dimensão ou tamanho de um ativo. Também é possível classificar os ativos em ordem crescente ou decrescente.

### Repositório de ativos {#assets-repo}

O Seletor de destino também permite visualizar os dados do repositório de sua escolha disponível no aplicativo AEM. Você pode usar `repositoryID` propriedade para inicializar o caminho da pasta de destino que você deseja visualizar na primeira instância do Seletor de destino.

### Adicionar sufixo ou prefixo {#add-suffix-or-prefix}

É um exemplo da `optionsFormSetup` propriedade. Você pode usar isso para confirmar a seleção, ela será transmitida ao `onConfirm` evento.

### Crie uma nova pasta {#create-new-folder}

Ele permite criar uma nova pasta na pasta de destino do seu [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].

### Tipos de visualização {#types-of-view}

O Seletor de destino permite exibir o ativo em quatro exibições diferentes:

* **![exibição de lista](assets/do-not-localize/list-view.png) [!UICONTROL Exibição de lista]**: a exibição de lista exibe arquivos e pastas roláveis em uma única coluna.
* **![exibição de grade](assets/do-not-localize/grid-view.png) [!UICONTROL Exibição em grade]**: a exibição de grade exibe arquivos e pastas roláveis em uma grade de linhas e colunas.
* **![exibição de galeria](assets/do-not-localize/gallery-view.png) [!UICONTROL Exibição da Galeria]**: a exibição de galeria exibe arquivos ou pastas em uma lista horizontal com bloqueio central.
* **![exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Exibição em cascata]**: a exibição em cascata exibe arquivos ou pastas no formato de um Bridge.

### Informações {#info}

O ícone de informações ou informações permite visualizar metadados do ativo selecionado. Ele inclui vários detalhes, como dimensões, tamanho, descrição, caminho, data de modificação e data de criação. As informações de metadados são fornecidas ao fazer upload, copiar ou criar um novo ativo.

### Selecionar pasta {#select-folder}

O botão Selecionar pasta permite selecionar ativos para executar várias operações associadas a [propriedades](#destination-selector-properties) no seletor de destino.