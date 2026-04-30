---
title: Propriedades do Supervisor de Conteúdo
description: Use as propriedades para personalizar como o Supervisor de Conteúdo é renderizado ao integrá-lo ao seu aplicativo.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Aplicável ao AEM Assets)."
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: c92611e4b815e49887e175943b81177e60623067
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 17%

---

# Instalação e propriedades do Supervisor de conteúdo {#content-advisor-installation-properties}

O Content Advisor também está disponível para integração com aplicativos que não sejam da Adobe (de terceiros), ampliando a detecção inteligente de ativos para além dos aplicativos da Adobe. O mesmo conjunto de recursos avançados, incluindo pesquisa alimentada por IA, recomendações de reconhecimento de contexto, descoberta baseada em resumo da campanha, acesso a representações do Dynamic Media, descoberta de fragmentos de conteúdo, filtros e metadados de ativos, é compatível com integrações de terceiros.

## Pré-requisitos{#prereqs}

Você deve garantir os seguintes métodos de comunicação:

* O aplicativo host está sendo executado em HTTPS.
* Você não pode executar o aplicativo em `localhost`. Para integrar o Supervisor de Conteúdo ao computador local, é necessário criar um domínio personalizado, por exemplo `[https://<your_campany>.localhost.com:<port_number>]`, e adicionar esse domínio personalizado ao `redirectUrl list`.
* Você pode configurar e adicionar clientID na variável de ambiente do AEM Cloud Service com o respectivo `imsClientId`.
<!--
* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)
-->
* A lista de escopos IMS precisa ser definida na configuração de ambiente.
* O URL do aplicativo está na lista de permissões de URLs de redirecionamento do cliente IMS.
* O fluxo de logon do IMS é configurado e renderizado usando um pop-up no navegador da Web. Portanto, os pop-ups devem ser ativados ou permitidos no navegador de destino.

Use os pré-requisitos acima se você precisar do fluxo de trabalho de autenticação IMS do Supervisor de conteúdo. Como alternativa, se você já estiver autenticado com o fluxo de trabalho do IMS, é possível adicionar as informações do IMS.

>[!IMPORTANT]
>
> Esse repositório deve servir como uma documentação complementar que descreve as APIs disponíveis e exemplos de uso para integração do Supervisor de conteúdo. Antes de tentar instalar ou usar o Supervisor de Conteúdo, verifique se sua organização recebeu o acesso ao Supervisor de Conteúdo como parte do perfil do Experience Manager Assets as a Cloud Service. Se não tiver sido provisionado, você não poderá integrar ou usar esses componentes. Para solicitar o provisionamento, o administrador do programa deve levantar um tíquete de suporte marcado como P2 do Admin Console e incluir as seguintes informações:
>
>* Nomes de domínio em que o aplicativo de integração está hospedado.
>* Após o provisionamento, sua organização receberá `imsClientId`, `imsScope` e um `redirectUrl` correspondentes aos ambientes solicitados que são essenciais para a configuração do Supervisor de conteúdo. Sem essas propriedades válidas, não é possível executar as etapas de instalação.

## Instalação {#content-advisor-installation}

O Supervisor de Conteúdo está disponível por meio da CDN do ESM (por exemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e da versão [UMD](https://github.com/umdjs/umd).

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

## Propriedades do Supervisor de Conteúdo {#content-advisor-propertiess}

Você pode usar as propriedades do Supervisor de Conteúdo para personalizar a forma como o Supervisor de Conteúdo é renderizado. A tabela a seguir lista as propriedades que você pode usar para personalizar e usar o Supervisor de Conteúdo.

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| *painel* | Booleano | Não | Falso | Se marcado como `true`, o Supervisor de Conteúdo é renderizado em um modo de exibição do painel esquerdo. Se estiver marcado como `false`, o Supervisor de Conteúdo será renderizado na exibição modal. |
| *imsOrg* | String | Sim | | A ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A chave `imsOrg` é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | String | Não | | Token de portador IMS usado para autenticação. `imsToken` é necessário se você estiver usando um aplicativo [!DNL Adobe] para a integração. |
| *apiKey* | String | Não | | Chave de API usada para acessar o serviço de Descoberta do AEM. `apiKey` é necessário se você estiver usando uma integração de aplicativos [!DNL Adobe]. |
| *externalBrief* | String | Não | | Permite fazer upload de um documento de resumo da campanha para descobrir ativos relevantes sem inserir manualmente palavras-chave de pesquisa. O Supervisor de Conteúdo analisa as informações no resumo da campanha para entender a intenção da campanha e recomenda ativos relevantes disponíveis no AEM Assets. |
| *filterSchema* | Matriz | Não | | Modelo usado para configurar propriedades de filtro. Isso é útil quando você deseja limitar determinadas opções de filtro no Supervisor de conteúdo. |
| *filterFormProps* | Objeto | Não | | Especifique as propriedades de filtro que precisam ser usadas para refinar sua pesquisa. Para! exemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | Não |                 | Especifique o Assets selecionado quando o Supervisor de Conteúdo for renderizado. É necessária uma matriz de objetos que contenha uma propriedade de id dos ativos. Por exemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Um ativo deve estar disponível no diretório atual. Se precisar usar um diretório diferente, forneça um valor para a propriedade `path` também. |
| *acvConfig* | Objeto | Não | | A propriedade Exibição da coleção do ativo que contém o objeto com a configuração personalizada para substituir os padrões. Além disso, essa propriedade é usada com a propriedade `rail` para habilitar a exibição do painel do visualizador de ativos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |                 | Se as traduções OOTB forem insuficientes para as necessidades do aplicativo, você poderá expor uma interface pela qual poderá passar seus próprios valores localizados e personalizados pela prop `i18nSymbols`. Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e usará suas próprias traduções. Para executar a substituição, deverá transmitir um objeto [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que deseja substituir. |
| *intl* | Objeto | Não | | O Supervisor de conteúdo fornece traduções OOTB padrão. Você pode selecionar o idioma de tradução fornecendo uma string de localidade válida por meio da propriedade `intl.locale`. Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As cadeias de caracteres de localidade com suporte seguem a [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação de nomes de padrões de idiomas. </br></br> Lista de locais com suporte: Inglês - &#39;en-us&#39; (padrão) Espanhol - &#39;es-es&#39; Alemão - &#39;de-de&#39; Francês - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonês - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Português - &#39;pt-br&#39; Chinês (Tradicional) - &#39;zh-cn&#39; Chinês (Taiwan) - &#39;zh-tw&#39; |
| *repositoryId* | String | Não | &#39;&#39; | Repositório de onde o Supervisor de conteúdo carrega o conteúdo. |
| *additionalAemSolutions* | `Array<string>` | Não | [ ] | Ele permite adicionar uma lista de repositórios AEM adicionais. Se nenhuma informação for fornecida nessa propriedade, somente a biblioteca de mídia ou os repositórios do AEM Assets serão considerados. |
| *hideTreeNav* | Booleano | Não |  | Especifica se deve mostrar ou ocultar a barra lateral de navegação da árvore de ativos. Usada apenas na exibição modal e, portanto, não há efeito dessa propriedade na exibição de painel. |
| *onDrop* | Função | Não | | A funcionalidade ao soltar é usada para arrastar um ativo e soltar em uma área designada para soltar. Ela permite interfaces de usuário interativas, nas quais os ativos podem ser movidos e processados sem interrupções. |
| *dropOptions* | `{allowList?: Object}` | Não | | Configura as opções de soltar usando “allowList”. |
| *tema* | String | Não | Padrão | Aplicar tema ao aplicativo Supervisor de Conteúdo entre `default` e `express`. Também aceita `@react-spectrum/theme-express`. |
| *handleSelection* | Função | Não | | Chamado com a matriz de itens do ativo quando os ativos são selecionados e o botão `Select` no modal é clicado. Essa função só é invocada na exibição modal. Para exibição do painel, use as funções `handleAssetSelection` ou `onDrop`. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [seleção de ativos](/help/assets/content-advisor-customization.md#selection-of-assets) para obter detalhes. |
| *handleAssetSelection* | Função | Não | | Invocado com uma matriz de itens enquanto os ativos estão sendo selecionados ou desmarcados. É útil quando você deseja acompanhar os ativos à medida que o usuário os seleciona. Exemplo: <pre>handleAssetSelection=(ativos: Ativo[])=> {...}</pre> Consulte [seleção de ativos](/help/assets/content-advisor-customization.md#selection-of-assets) para obter detalhes. |
| *onClose* | Função | Não | | Invocado quando o botão `Close` na exibição modal é pressionado. Somente é chamado na exibição `modal` e desconsiderado na exibição `rail`. |
| *onFilterSubmit* | Função | Não | | Invocado com itens de filtro à medida que o usuário altera critérios de filtro diferentes. |
| *selectionType* | String | Não | Solteiro | Configuração para a seleção `single` ou `multiple` de ativos de cada vez. |
| *arrastarOpções.incluir na lista de permissões* | booleano | Não | | A propriedade é usada para permitir ou negar a ação de arrastar ativos que não podem ser selecionados. Consulte [Propriedade dragOptions](/help/assets/content-advisor-customization.md#drag-options-property) |
| *aemTierType* | String | Não |  | Ela permite selecionar se você deseja mostrar ativos do nível de entrega, do nível de criação ou de ambos. <br><br> Sintaxe: `aemTierType: "author"  "delivery"` <br><br> Por exemplo, se ambos `["author","delivery"]` forem usados, o alternador de repositório exibirá opções para o autor e para a entrega. |
| *handleNavigateToAsset* | Função | Não | | É uma função de Retorno de chamada para lidar com a seleção de um ativo. |
| *noWrap* | Booleano | Não | | A propriedade *noWrap* impede que o Supervisor de Conteúdo seja colocado em uma caixa de diálogo. Se essa propriedade não for mencionada, ela renderizará a *Exibição da caixa de diálogo* por padrão. |
| *tamanhoDaCaixaDeDiálogo* | S, M, L, tela cheia, fullscreenTakeover | String | Opcional | Você pode controlar o layout especificando seu tamanho com as opções fornecidas. |
| *colorScheme* | Sequência de caracteres (claro, escuro) | Não | | Esta propriedade é usada para definir o tema de um aplicativo do Supervisor de Conteúdo. Você pode escolher entre um tema claro ou escuro. |
| *filterRepoList* | Função | Não | | Uma função que recebe a lista de repositórios e retorna uma lista filtrada. |
| *OpçõesDeExpiração* | Função | | | Você pode usar entre as duas propriedades a seguir: **getExpiryStatus** que fornece o status de um ativo expirado. A função retorna `EXPIRED`, `EXPIRING_SOON` ou `NOT_EXPIRED` com base na data de expiração de um ativo fornecido. Consulte [personalizar ativos expirados](/help/assets/content-advisor-customization.md#customize-expired-assets). Além disso, você pode usar **allowSelectionAndDrag**, no qual o valor da função pode ser `true` ou `false`. Quando o valor é definido como `false`, o ativo expirado não pode ser selecionado ou arrastado na tela. |
| *mostrarNotificação* | | Não | | Ele permite que o Supervisor de conteúdo mostre uma mensagem em caixa de informações personalizada para o ativo expirado. |
| *uploadConfig* | Objeto | | | É um objeto que contém a configuração personalizada para o upload. Consulte [configuração de carregamento](#content-advisor-customization.md#upload-config) para ver a usabilidade. |
| *uploadConfig* > *metadataSchema* | Matriz | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. Adicione uma matriz de campos fornecida para coletar metadados do usuário. Usando essa propriedade, também é possível usar metadados ocultos que são atribuídos a um ativo automaticamente, mas que não estão visíveis para o usuário. |
| *uploadConfig* > *onMetadataFormChange* | Função de retorno de chamada | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. Consiste em `property` e `value`. `Property` é igual a *mapToProperty* do campo passado de *metadataSchema* cujo valor está sendo atualizado. Por outro lado, `value` é igual ao novo valor fornecido como uma entrada. |
| *uploadConfig* > *targetUploadPath* | String |  | `"/content/dam"` | Esta propriedade está aninhada sob a propriedade `uploadConfig`. O caminho de upload de destino para os arquivos cujo padrão é a raiz do repositório de ativos. |
| *uploadConfig* > *hideUploadButton* | Booleano | | Falso | Ele garante se o botão de upload interno deve estar oculto ou não. Esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *uploadConfig* > *onUploadStart* | Função | Não |  | É uma função de retorno de chamada usada para transmitir a origem do upload entre o Dropbox, o OneDrive ou o local. Sintaxe `(uploadInfo: UploadInfo) => void`. Esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *uploadConfig* > *importSettings* | Função | | | Ela permite o suporte para importar ativos de origem de terceiros. `sourceTypes` usa uma matriz das fontes de importação que você deseja habilitar. As fontes compatíveis são Onedrive e Dropbox. Sintaxe `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`. Além disso, esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *uploadConfig* > *onUploadComplete* | Função | Não | | É uma função de retorno de chamada usada para passar o status de upload de arquivo entre com êxito, com falha ou duplicado. Sintaxe `(uploadStats: UploadStats) => void`. Além disso, esta propriedade está aninhada sob a propriedade `uploadConfig`. |
| *uploadConfig* > *onFilesChange* | Função | Não | | Esta propriedade está aninhada sob a propriedade `uploadConfig`. É uma função de retorno de chamada usada para mostrar o comportamento de upload quando um arquivo é alterado. Ele passa a nova matriz de arquivos pendentes para upload e o tipo de origem do upload. O tipo de Source pode ser nulo em caso de erro. A sintaxe é `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadConfig* > *uploadingPlaceholder* | String | | | É uma imagem de espaço reservado que substitui o formulário de metadados quando um upload do ativo é iniciado. A sintaxe é `{ href: string; alt: string; }`. Além disso, essa propriedade está aninhada na propriedade `uploadConfig`. |
| *featureSet* | Matriz | String | | A propriedade `featureSet:[ ]` é usada para habilitar ou desabilitar uma funcionalidade específica no aplicativo Supervisor de Conteúdo. Para ativar o componente ou um recurso, você pode passar um valor de string na matriz ou deixar a matriz vazia para desativar recursos adicionados e apenas ter a funcionalidade base. Por exemplo, se você deseja habilitar a funcionalidade de carregamento no Supervisor de Conteúdo, use a sintaxe `featureSet:["upload"]`. Da mesma forma, você pode usar `featureSet:["content-fragments"]` para habilitar Fragmentos de conteúdo no Supervisor de conteúdo. Para usar vários recursos juntos, a sintaxe é featureSet:[&quot;upload&quot;, &quot;content-fragments&quot;]. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

### ImsAuthProps {#ims-auth-props}

As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Supervisor de Conteúdo usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação deve se comportar e registrar ouvintes para vários eventos de autenticação.

| Nome de propriedade | Descrição |
|---|---|
| `imsClientId` | Um valor de string que representa a ID do cliente IMS usada para fins de autenticação. Esse valor é fornecido pela Adobe e é específico para a sua organização do Adobe AEM CS. |
| `imsScope` | Descreve os escopos usados na autenticação. Os escopos determinam o nível de acesso que o aplicativo tem aos recursos da organização. Vários escopos podem ser separados por vírgulas. |
| `redirectUrl` | Representa o URL para o qual o usuário é redirecionado após a autenticação. Normalmente, esse valor é definido como o URL atual do aplicativo. Se um `redirectUrl` não for fornecido, `ImsAuthService` usará o redirectUrl usado para registrar o `imsClientId` |
| `modalMode` | Um booleano que indica se o fluxo de autenticação deve ser exibido em um modal (pop-up) ou não. Se definido como `true`, o fluxo de autenticação será exibido em um pop-up. Se definido como `false`, o fluxo de autenticação será exibido em um recarregamento de página completo. _Observação :_para melhor UX, você pode controlar dinamicamente esse valor se o usuário tiver o pop-up do navegador desabilitado. |
| `onImsServiceInitialized` | Uma função de retorno de chamada que é chamada quando o serviço de autenticação do Adobe IMS é inicializado. Essa função recebe um parâmetro, `service`, que é um objeto que representa o serviço Adobe IMS. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obter mais detalhes. |
| `onAccessTokenReceived` | Uma função de retorno de chamada que é chamada quando um `imsToken` é recebido do serviço de autenticação do Adobe IMS. Esta função recebe um parâmetro, `imsToken`, que é uma cadeia de caracteres que representa o token de acesso. |
| `onAccessTokenExpired` | Uma função de retorno de chamada chamada chamada quando um token de acesso expira. Normalmente, essa função é usada para acionar um novo fluxo de autenticação para obter um novo token de acesso. |
| `onErrorReceived` | Uma função de retorno de chamada que é chamada quando ocorre um erro durante a autenticação. Essa função usa dois parâmetros: o tipo de erro e a mensagem de erro. O tipo de erro é uma cadeia de caracteres que representa o tipo de erro, e a mensagem de erro é uma cadeia de caracteres que representa a mensagem de erro. |

### ImsAuthService {#ims-auth-service}

A classe `ImsAuthService` manipula o fluxo de autenticação para o Supervisor de Conteúdo. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao [!DNL Adobe Experience Manager] como um repositório do Assets [!DNL Cloud Service]. O ImsAuthService usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a conveniente função [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar a instância _ImsAuthService_ com o Supervisor de Conteúdo. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função _registerAssetsSelectorsAuthService_, não será necessário chamar essas funções diretamente.

| Nome da função | Descrição |
|---|---|
| `isSignedInUser` | Determina se o usuário está conectado ao serviço no momento e retorna um valor booleano correspondente. |
| `getImsToken` | Recupera a autenticação `imsToken` para o usuário conectado no momento, que pode ser usada para autenticar solicitações para outros serviços, como a geração de _representação de ativos. |
| `signIn` | Inicia o processo de entrada do usuário. Esta função usa o `ImsAuthProps` para mostrar autenticação em um pop-up ou em um recarregamento de página completo |
| `signOut` | Desconecta o usuário do serviço, invalidando seu token de autenticação e exigindo que ele entre novamente para acessar recursos protegidos. Chamar essa função recarregará a página atual. |
| `refreshToken` | Atualiza o token de autenticação do usuário conectado no momento, evitando a expiração e garantindo acesso ininterrupto aos recursos protegidos. Retorna um novo token de autenticação que pode ser usado para solicitações subsequentes. |

### contentFragmentSelectorProps {#content-fragment-selector-properties}

`contentFragmentSelectorProps` permite configurar como os fragmentos de conteúdo são acessados e exibidos no Supervisor de conteúdo. Ao ativar o recurso de fragmentos de conteúdo no `featureSet` e fornecer a configuração necessária, você pode integrar facilmente a seleção de Fragmento de conteúdo com os ativos. Isso permite que os usuários naveguem, pesquisem e selecionem fragmentos de conteúdo na mesma interface unificada, garantindo uma experiência consistente de seleção de conteúdo em ativos e conteúdo estruturado.

```
const assetSelectorProps = {
     featureSet: [
       'upload',            /* Include upload or other featureSet values to ensure no missing functionality */
       'content-fragments', /* Content Fragments pill will be shown */
     ],
     contentFragmentSelectorProps: {
       /* Configures the Content Fragments Pill experience */
       /* ...props @aem-sites/content-fragment-selector MFE supports */
    }
}

<AssetSelector {...assetSelectorProps} />
```

Em `contentFragmentSelectorProps`, você pode mencionar qualquer uma das propriedades disponíveis em [Propriedades do Seletor de Fragmento de Conteúdo](/help/headless/content-fragment-selector/properties.md).

Para obter informações sobre como integrar o Supervisor de Conteúdo aos aplicativos do Angular, React e JavaScript, consulte [exemplos de integração do Supervisor de Conteúdo](https://github.com/adobe/aem-assets-selectors-mfe-examples/tree/consolidate-docs-to-experience-league/examples).


