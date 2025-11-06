---
title: Propriedades do Seletor de ativos para personalização
description: Use o Seletor de ativos para pesquisar, localizar e recuperar metadados e representações de ativos no aplicativo.
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 36%

---

# Propriedades do Seletor de ativos {#asset-selector-properties}

Você pode usar as propriedades do Seletor de ativos para personalizar a forma como o Seletor de ativos é renderizado. A tabela a seguir lista as propriedades que você pode usar para personalizar e usar o Seletor de ativos.

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| *painel* | Booleano | Não | Falso | Se marcado como `true`, o Seletor de ativos será renderizado em um modo de exibição de painel esquerdo. Se estiver marcado como `false`, o Seletor de ativos será renderizado na exibição modal. |
| *imsOrg* | String | Sim | | A ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A chave `imsOrg` é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | String | Não | | Token de portador IMS usado para autenticação. `imsToken` é necessário se você estiver usando um aplicativo [!DNL Adobe] para a integração. |
| *apiKey* | String | Não | | Chave de API usada para acessar o serviço de Descoberta do AEM. `apiKey` é necessário se você estiver usando uma integração de aplicativos [!DNL Adobe]. |
| *filterSchema* | Matriz | Não | | Modelo usado para configurar propriedades de filtro. Isso é útil quando quiser limitar determinadas opções de filtro no Seletor de ativos. |
| *Propriedades de Formulário de Filtro* | Objeto | Não | | Especifique as propriedades de filtro que precisam ser usadas para refinar sua pesquisa. Para! exemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | Não |                 | Especifique os ativos selecionados quando o Seletor de ativos for renderizado. É necessária uma matriz de objetos que contenha uma propriedade de id dos ativos. Por exemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Um ativo deve estar disponível no diretório atual. Se precisar usar um diretório diferente, forneça um valor para a propriedade `path` também. |
| *acvConfig* | Objeto | Não | | A propriedade Exibição da coleção do ativo que contém o objeto com a configuração personalizada para substituir os padrões. Além disso, essa propriedade é usada com a propriedade `rail` para habilitar a exibição do painel do visualizador de ativos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |                 | Se as traduções OOTB forem insuficientes para as necessidades do aplicativo, você poderá expor uma interface pela qual poderá passar seus próprios valores localizados e personalizados pela prop `i18nSymbols`. Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e, em vez disso, usa suas próprias traduções. Para executar a substituição, deverá transmitir um objeto [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que deseja substituir. |
| *intl* | Objeto | Não | | O Seletor de ativos fornece traduções OOTB padrão. Você pode selecionar o idioma de tradução fornecendo uma string de localidade válida por meio da propriedade `intl.locale`. Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As strings de idioma com suporte seguem os padrões [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação de nomes de idiomas. </br></br> Lista de localidades compatíveis: Inglês - “en-us” (padrão) Espanhol - “es-es” Alemão - “de-de” Francês - “fr-fr” Italiano - “it-it” Japonês - “ja-jp” Coreano - “ko-kr” Português - “pt-br” Chinês (Tradicional) - “zh-cn” Chinês (Taiwan) - “zh-tw” |
| *repositoryId* | String | Não | &#39;&#39; | Repositório de onde o Seletor de ativos carrega o conteúdo. |
| *additionalAemSolutions* | `Array<string>` | Não | [ ] | Ele permite adicionar uma lista de repositórios AEM adicionais. Se nenhuma informação for fornecida nessa propriedade, somente a biblioteca de mídia ou os repositórios do AEM Assets serão considerados. |
| *hideTreeNav* | Booleano | Não |  | Especifica se deve mostrar ou ocultar a barra lateral de navegação da árvore de ativos. Usada apenas na exibição modal e, portanto, não há efeito dessa propriedade na exibição de painel. |
| *onDrop* | Função | Não | | A funcionalidade ao soltar é usada para arrastar um ativo e soltar em uma área designada para soltar. Ela permite interfaces de usuário interativas, nas quais os ativos podem ser movidos e processados sem interrupções. |
| *dropOptions* | `{allowList?: Object}` | Não | | Configura as opções de soltar usando “allowList”. |
| *colorScheme* | String | Não | | Configure o tema (`light` ou `dark`) do Seletor de ativos. |
| *Tema* | String | Não | Padrão | Aplique o tema ao aplicativo Seletor de Ativos entre `default` e `express`. Também aceita `@react-spectrum/theme-express`. |
| *handleSelection* | Função | Não | | Chamado com a matriz de itens do ativo quando os ativos são selecionados e o botão `Select` no modal é clicado. Essa função só é invocada na exibição modal. Para exibição do painel, use as funções `handleAssetSelection` ou `onDrop`. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [seleção de ativos](/help/assets/asset-selector-customization.md#selection-of-assets) para obter detalhes. |
| *handleAssetSelection* | Função | Não | | Invocado com uma matriz de itens enquanto os ativos estão sendo selecionados ou desmarcados. É útil quando você deseja acompanhar os ativos à medida que o usuário os seleciona. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [seleção de ativos](/help/assets/asset-selector-customization.md#selection-of-assets) para obter detalhes. |
| *onClose* | Função | Não | | Invocado quando o botão `Close` na exibição modal é pressionado. Somente é chamado na exibição `modal` e desconsiderado na exibição `rail`. |
| *onFilterSubmit* | Função | Não | | Invocado com itens de filtro à medida que o usuário altera critérios de filtro diferentes. |
| *selectionType* | String | Não | Solteiro | Configuração para a seleção `single` ou `multiple` de ativos de cada vez. |
| *arrastarOpções.incluir na lista de permissões* | booleano | Não | | A propriedade é usada para permitir ou negar a ação de arrastar ativos que não podem ser selecionados. Consulte [Propriedade dragOptions](/help/assets/asset-selector-customization.md#drag-options-property) |
| *aemTierType* | String | Não |  | Ela permite selecionar se você deseja mostrar ativos do nível de entrega, do nível de criação ou de ambos. Sintaxe de <br><br>: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Por exemplo, se ambos `["author","delivery"]` forem usados, o alternador de repositório exibirá opções para o autor e para a entrega. |
| *handleNavigateToAsset* | Função | Não | | É uma função de Retorno de chamada para lidar com a seleção de um ativo. |
| *noWrap* | Booleano | Não | | A propriedade *noWrap* ajuda a renderizar o Seletor de ativos no painel lateral. Se essa propriedade não for mencionada, ela renderizará a *Exibição da caixa de diálogo* por padrão. |
| *tamanhoDaCaixaDeDiálogo* | controle pequeno, médio, grande, tela cheia ou tela cheia | String | Opcional | Você pode controlar o layout especificando seu tamanho com as opções fornecidas. |
| *colorScheme* | Claro ou escuro | Não | | Essa propriedade é usada para definir o tema de um aplicativo Seletor de ativos. Você pode escolher entre um tema claro ou escuro. |
| *filterRepoList* | Função | Não |  | Você pode usar a função de retorno de chamada `filterRepoList` que chama o repositório do Experience Manager e retorna uma lista filtrada de repositórios. |
| *OpçõesDeExpiração* | Função | | | Você pode usar entre as duas propriedades a seguir: **getExpiryStatus** que fornece o status de um ativo expirado. A função retorna `EXPIRED`, `EXPIRING_SOON` ou `NOT_EXPIRED` com base na data de expiração de um ativo fornecido. Consulte [personalizar ativos expirados](/help/assets/asset-selector-customization.md#customize-expired-assets). Além disso, você pode usar **allowSelectionAndDrag**, no qual o valor da função pode ser `true` ou `false`. Quando o valor é definido como `false`, o ativo expirado não pode ser selecionado ou arrastado na tela. |
| *mostrarNotificação* | | Não | | Ele permite que o Seletor de ativos mostre uma mensagem em caixa de informações personalizada para o ativo expirado. |
| *uploadConfig* | Objeto | | | É um objeto que contém a configuração personalizada para o upload. Consulte [configuração de carregamento](#asset-selector-customization.md#upload-config) para ver a usabilidade. |
| *metadataSchema* | Matriz | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. Adicione uma matriz de campos fornecida para coletar metadados do usuário. Usando essa propriedade, também é possível usar metadados ocultos que são atribuídos a um ativo automaticamente, mas que não estão visíveis para o usuário. |
| *onMetadataFormChange* | Função de retorno de chamada | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. Consiste em `property` e `value`. `Property` é igual a *mapToProperty* do campo passado de *metadataSchema* cujo valor está sendo atualizado. Por outro lado, `value` é igual ao novo valor fornecido como uma entrada. |
| *targetUploadPath* | String |  | `"/content/dam"` | Esta propriedade está aninhada sob a propriedade `uploadConfig`. O caminho de upload de destino para os arquivos cujo padrão é a raiz do repositório de ativos. |
| *hideUploadButton* | Booleano | | Falso | Ele garante se o botão de upload interno deve estar oculto ou não. Esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *onUploadStart* | Função | Não |  | É uma função de retorno de chamada usada para transmitir a origem do upload entre o Dropbox, o OneDrive ou o local. Sintaxe `(uploadInfo: UploadInfo) => void`. Esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *importSettings* | Função | | | Ela permite o suporte para importar ativos de origem de terceiros. `sourceTypes` usa uma matriz das fontes de importação que você deseja habilitar. As fontes compatíveis são Onedrive e Dropbox. Sintaxe `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`. Além disso, esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *onUploadComplete* | Função | Não | | É uma função de retorno de chamada usada para passar o status de upload de arquivo entre com êxito, com falha ou duplicado. Sintaxe `(uploadStats: UploadStats) => void`. Além disso, esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *onFilesChange* | Função | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. É uma função de retorno de chamada usada para mostrar o comportamento de upload quando um arquivo é alterado. Ele passa a nova matriz de arquivos pendentes para upload e o tipo de origem do upload. O tipo de Source pode ser nulo em caso de erro. A sintaxe é `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | String | | | É uma imagem de espaço reservado que substitui o formulário de metadados quando um upload do ativo é iniciado. A sintaxe é `{ href: string; alt: string; }`. Além disso, essa propriedade está aninhada na propriedade `uploadConfig`. |
| *featureSet* | Matriz | String | | A propriedade `featureSet:[ ]` é usada para habilitar ou desabilitar uma funcionalidade específica no aplicativo Seletor de ativos. Para ativar o componente ou um recurso, passe um valor de string na matriz ou deixe a matriz vazia para desativar esse componente.  Por exemplo, se você deseja habilitar a funcionalidade de carregamento no Seletor de ativos, use a sintaxe `featureSet:[0:"upload"]`. Da mesma forma, você pode usar `featureSet:[0:"collections"]` para habilitar coleções no Seletor de ativos. Além disso, use o `featureSet:[0:"detail-panel"]` para habilitar o [painel de detalhes](overview-asset-selector.md#asset-details-and-metadata) de um ativo. Para usar esses recursos juntos, a sintaxe é `featureSet:["upload", "collections", "detail-panel"]`. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

>[!MORELIKETHIS]
>
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Integrar o Seletor de ativos a aplicativos de terceiros](/help/assets/integrate-asset-selector-non-adobe-app.md)
