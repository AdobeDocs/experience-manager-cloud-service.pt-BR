---
title: Personalizar o aplicativo Seletor de ativos
description: Use funções para personalizar o Seletor de ativos no aplicativo.
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 21%

---

# Personalizações do Seletor de ativos {#asset-selector-customization}

O Seletor de ativos permite personalizar vários componentes de acordo com preferências, requisitos ou necessidades funcionais. Você pode personalizar os seguintes componentes [Seletor de ativos de microfront-end](#overview-asset-selector.md):

* [Personalizar painel de filtro](#customize-filter-panel)
* [Personalizar informações na exibição modal](#customize-info-in-modal-view)
* [Ativar ou desativar o modo arrastar e soltar](#enable-disable-drag-and-drop)
* [Seleção do Assets](#selection-of-assets)
* [Personalizar ativos expirados](#customize-expired-assets)
* [Filtro de invocação contextual](#contextual-invocation-filter)
* [propriedade dragOptions](#drag-options-property)

Você precisa definir os pré-requisitos no arquivo **index.html** ou em um arquivo semelhante na implementação do aplicativo para definir os detalhes de autenticação para acessar o repositório [!DNL Experience Manager Assets]. Depois de concluído, você pode adicionar trechos de código de acordo com sua exigência.

## Personalizar painel de filtro {#customize-filter-panel}

Você pode adicionar o seguinte trecho de código no objeto `assetSelectorProps` para personalizar o painel de filtro:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

## Personalizar informações na exibição modal {#customize-info-in-modal-view}

Você pode personalizar a exibição detalhada de um ativo ao clicar no ícone ![informações](assets/info-icon.svg). Execute o código abaixo:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## Ativar ou desativar o modo arrastar e soltar {#enable-disable-drag-and-drop}

Adicione as seguintes propriedades a `assetSelectorProp` para habilitar o modo arrastar e soltar. Para desabilitar arrastar e soltar, substitua o parâmetro `true` por `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

## Seleção do Assets {#selection-of-assets}

O Tipo de ativo selecionado é uma matriz de objetos que contém as informações do ativo ao usar as funções `handleSelection`, `handleAssetSelection`, e `onDrop`.

Execute as seguintes etapas para configurar a seleção de um ou vários ativos:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Sintaxe do esquema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

A tabela a seguir descreve algumas das propriedades importantes do objeto de ativo selecionado.

| Propriedade | Tipo | Descrição |
|---|---|---|
| *repositório:repositoryId* | string | Identificador exclusivo do repositório onde o ativo está armazenado. |
| *repositório:id* | string | Identificador exclusivo do ativo. |
| *repositório:assetClass* | string | A classificação do ativo (por exemplo, imagem, vídeo ou documento). |
| *repositório:name* | string | O nome do ativo, incluindo a extensão de arquivo. |
| *repositório:size* | número | O tamanho do ativo em bytes. |
| *repositório:path* | string | O local do ativo no repositório. |
| *repositório:ancestors* | `Array<string>` | Uma matriz de itens ancestrais do ativo no repositório. |
| *repositório:state* | string | Estado atual do ativo no repositório (Por exemplo, ativo, excluído etc.). |
| *repositório:createdBy* | string | O usuário ou sistema que criou o ativo. |
| *repositório:createDate* | string | A data e a hora em que o ativo foi criado. |
| *repositório:modifiedBy* | string | O usuário ou sistema que modificou o ativo pela última vez. |
| *repositório:modifyDate* | string | A data e a hora em que o ativo foi modificado pela última vez. |
| *dc:format* | string | O formato do ativo, como o tipo de arquivo (por exemplo, JPEG, PNG etc.). |
| *tiff:imageWidth* | número | A largura de um ativo. |
| *tiff:imageLength* | número | A altura de um ativo. |
| *computedMetadata* | `Record<string, any>` | Um objeto que representa um compartimento para todos os metadados do ativo de todos os tipos (repositório, aplicativo ou metadados incorporados). |
| *_links* | `Record<string, any>` | Links de hipermídia do ativo associado. Inclui links para recursos como metadados e representações. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | Matriz de objetos que contém informações sobre representações do ativo. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | string | O URI da representação. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | string | O tipo MIME da representação. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | número | O tamanho da representação em bytes. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | número | A largura da representação. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | número | A altura da representação. |

### Lidar com a seleção de ativos usando o esquema de objeto {#handling-selection}

A propriedade `handleSelection` é usada para lidar com seleções únicas ou múltiplas de ativos no Seletor de ativos. O exemplo abaixo declara a sintaxe de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

### Desabilitação da seleção de Assets {#disable-selection}

Desativar seleção é usado para ocultar ou desativar a seleção de ativos ou pastas. Ela oculta a caixa de seleção de seleção do cartão ou ativo, impedindo-o de ser selecionado. Para usar esse recurso, você pode declarar a posição de um ativo ou pasta que deseja desativar em uma matriz. Por exemplo, se você quiser desativar a seleção de uma pasta que aparece na primeira posição, poderá adicionar o seguinte código:
`disableSelection: [0]:folder`

Você pode fornecer à matriz uma lista de tipos MIME (como imagem, pasta, arquivo ou outros tipos MIME, por exemplo, image/jpeg) que deseja desativar. Os tipos MIME declarados são mapeados em `data-card-type` e `data-card-mimetype` atributos de um ativo.

Além disso, o Assets com seleção desativada é arrastável. Para desabilitar a ação de arrastar e soltar um tipo de ativo específico, você pode usar a propriedade `dragOptions.allowList`.

A sintaxe de desabilitar seleção é a seguinte:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> No caso de um ativo, a caixa de seleção Selecionar fica oculta, enquanto no caso de uma pasta, a pasta não pode ser selecionada, mas a navegação da pasta mencionada ainda é exibida.

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## Personalizar ativos expirados {#customize-expired-assets}

O Seletor de ativos permite controlar o uso de um ativo expirado. Você pode personalizar o ativo expirado com um selo **Expirando em breve** que pode ajudá-lo a saber com antecedência sobre os ativos que expirarão em 30 dias a partir da data atual. Além disso, isso pode ser personalizado de acordo com a exigência. Você também pode permitir a seleção de um ativo expirado na tela ou vice-versa. A personalização de um ativo expirado pode ser feita usando alguns snippets de código de várias maneiras:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

### Seleção de um ativo expirado {#selection-of-expired-asset}

Você pode personalizar o uso de um ativo expirado para torná-lo selecionável ou não selecionável. É possível personalizar se deseja permitir ou não o arrastar e soltar de um ativo expirado na tela Seletor de ativos. Para fazer isso, use os seguintes parâmetros para tornar um ativo não selecionável na tela:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```

<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### Configuração da duração de um ativo expirado {#set-duration-of-expired-asset}

O trecho de código a seguir ajuda a definir o selo **Expirando em Breve** para os ativos que expiram nos próximos cinco dias: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Consulte o exemplo a seguir para entender como a propriedade funciona para buscar a data e hora atuais:

```
const currentData = new Date();
currentData.getTime(),
```

retorna `1718779013959` que é o formato de data 2024-06-19T06:36:53.959Z.

### Personalizar mensagem em caixa de informações de um ativo expirado {#customize-toast-message}

A propriedade `showToast` é usada para personalizar a mensagem do sistema que você deseja mostrar em um ativo expirado.

Sintaxe:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

O tempo limite padrão é de 500 milissegundos. Ao passo que, você pode modificá-lo de acordo com o requisito. Além disso, passar o valor `timeout: 0` mantém a janela aberta até que você clique no botão cruzado.

Veja abaixo um exemplo para mostrar uma mensagem em caixa de informações quando é necessário proibir a seleção de uma pasta e mostrar uma mensagem correspondente:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Use o seguinte trecho de código para mostrar uma mensagem do sistema para o uso de um ativo expirado:

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## Filtro de invocação contextual{#contextual-invocation-filter}

O Seletor de ativos permite adicionar um filtro seletor de tags. Ela é compatível com um grupo de tags que combina todas as tags relevantes a um grupo de tags específico. Além disso, permite selecionar tags adicionais correspondentes ao ativo que você está procurando. Além disso, você também pode definir os grupos de tags padrão no filtro de chamada contextual que são usados principalmente por você para que sejam acessíveis a você em qualquer lugar.

>[!NOTE]
>
> * É necessário adicionar um trecho de código de invocação contextual para ativar o filtro de marcação na pesquisa.
> * É obrigatório usar a propriedade de nome correspondente ao tipo de grupo de marcas `(property=xcm:keywords.id=)`.

Sintaxe:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Para adicionar grupos de tags no painel Filtros, é obrigatório adicionar pelo menos um grupo de tags como padrão. Além disso, use o trecho de código abaixo para adicionar as tags padrão pré-selecionadas do grupo de tags.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![filtro de grupo de marcas](assets/tag-group.gif)

## Carregar no Seletor de ativos {#upload-in-asset-selector}

Você pode fazer upload de arquivos ou pastas para o Seletor de ativos no seu sistema de arquivos local. Para carregar arquivos usando o sistema de arquivos local, geralmente é necessário usar um recurso de upload fornecido por um aplicativo de micro front-end do Seletor de ativos. Os `upload` Vários trechos de código necessários para invocar o upload no seletor de ativos envolvem:

* [Trecho básico do código do formulário para upload](#basic-upload)
* [Fazer upload da configuração](#upload-config)
* [Carregar com metadados](#upload-with-metadata)
* [Upload personalizado](#customized-upload)
* [Fazer upload usando fontes de terceiros](#upload-using-third-party-source)

### Formulário básico de upload {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### Fazer upload da configuração {#upload-config}

```
uploadConfig: {
        onUploadStart: action('onUploadStart'),
        onUploadComplete: action('onUploadComplete'),
        metadataSchema: [
            {
                mapToProperty: 'dam:assetStatus',
                value: 'approved',
                element: 'hidden',
            },
        ],
        ... more properties
     }, 
```

*Mais propriedades incluem `metadataSchema`, `onMetadataFormChange`, `targetUploadPath`, `hideUploadButton`, `onUploadStart`, `importSettings` `onUploadComplete`, `onFilesChange`,`uploadingPlaceholder`*. Consulte [Propriedades do Seletor de ativos](#asset-selector-properties.md) para obter mais informações.

### Carregar com metadados {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### Upload personalizado {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### Fazer upload usando fontes de terceiros {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

### Propriedade dragOptions {#drag-options-property}

```
dragOptions: {
            allowList: {
                '*': true,          // allow all types to be dragged
                'folder': false,    // except those explicitly set to disallow
                'image/jpeg': false // or those with specific mimeTypes
            },
         }
```

>[!MORELIKETHIS]
>
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
