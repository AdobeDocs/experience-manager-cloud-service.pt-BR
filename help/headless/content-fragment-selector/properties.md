---
title: Propriedades do seletor de fragmentos de conteúdo de front-end micro para Adobe Experience Manager as a Cloud Service
description: Propriedades para configurar o Seletor de fragmento de conteúdo de micro front-end para pesquisar, localizar e recuperar fragmentos de conteúdo do aplicativo.
role: Admin, User, Developer
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 86be8e53b77e8c7771f5a60b711a045128899acd
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 3%

---

# Seletor de fragmento de conteúdo — Propriedades relacionadas {#content-fragment-selector-related-properties}

O Seletor de fragmento de conteúdo de micro front-end permite navegar ou pesquisar fragmentos de conteúdo no repositório e usá-los no aplicativo.

Você pode usar as seguintes propriedades para personalizar como o Seletor de fragmento de conteúdo é renderizado e como ele pode ser usado:

## Propriedades do seletor de fragmentos de conteúdo {#content-fragment-selector-properties}

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|--- |--- |--- |--- |--- |
| `ref` | RefSeletorFragmento | Não | | Referência à instância `ContentFragmentSelector`, permitindo acesso à funcionalidade fornecida, como `reload`. |
| `imsToken` | string | Não | | Token IMS usado para autenticação. Se não for fornecido, o fluxo de logon do IMS será iniciado. |
| `repoId` | string | Não | | ID do repositório usada para o Seletor de fragmentos. Quando fornecido, o seletor se conecta automaticamente ao repositório especificado e a lista suspensa de repositórios fica oculta. Se não for fornecido, o usuário poderá selecionar um repositório na lista de repositórios disponíveis aos quais tem acesso. |
| `allowedRepositoryIds` | cadeia de caracteres[] | Não | | Lista de IDs de repositório para filtrar repositórios e fragmentos de conteúdo no Seletor de fragmento de conteúdo. Quando forem fornecidas com as IDs do repositório, somente esses repositórios estarão visíveis no seletor de repositórios. Se não for fornecida uma matriz ou se a matriz estiver vazia, todos os repositórios aos quais o usuário tiver acesso estarão disponíveis. |
| `defaultRepoId` | string | Não | | ID do repositório que será selecionado por padrão quando o seletor de repositório for exibido. Usado apenas quando `repoId` não é fornecido. Se `repoId` estiver definido, o seletor de repositório ficará oculto e esse valor será ignorado. |
| `orgId` | string | Não | | ID da organização usada para autenticação. Se não for fornecido, o usuário poderá selecionar um repositório de diferentes organizações às quais tem acesso. Se o usuário não tiver acesso a nenhum repositório ou organização, o conteúdo não será carregado. |
| `locale` | string | Não | &quot;en-US&quot; | Localidade. |
| `env` | string | Não | | Ambiente de implantação. Consulte o tipo `Env` para obter os nomes de ambiente permitidos. |
| `filters` | FiltroDeFragmentos | Não | `{ folder: "/content/dam" }` | Filtros a serem aplicados à lista de fragmentos de conteúdo. Por padrão, os fragmentos em `/content/dam` serão exibidos. |
| `isOpen` | booleano | Não | `false` | Sinalizador para controlar se o seletor está aberto ou fechado. |
| `noWrap` | booleano | Não | `false` | Determina se o Seletor de fragmentos é renderizado sem uma caixa de diálogo de encapsulamento. Quando definido como `true`, o Seletor de fragmento é inserido diretamente no contêiner pai. Útil para integrar o seletor em layouts ou fluxos de trabalho personalizados. |
| `onSelectionChange` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | Não | | A função de retorno de chamada é acionada sempre que a seleção de fragmentos de conteúdo é alterada. Fornece os fragmentos selecionados no momento, o nome do domínio, as informações do locatário, a ID do repositório e os repositórios de entrega. |
| `onDismiss` | () => void | Não | | Função de retorno de chamada acionada quando a ação de descarte é executada (por exemplo, fechar o seletor). |
| `onSubmit` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | Não | | A função de retorno de chamada é acionada quando o usuário confirma sua seleção. Recebe os fragmentos de conteúdo selecionados, o nome do domínio, as informações do locatário, a ID do repositório e os repositórios de entrega. |
| `theme` | &quot;claro&quot; ou &quot;escuro&quot; | Não | | Tema para o Seletor de fragmentos. Por padrão, é definido como o tema de ambiente unifiedShell. |
| `selectionType` | &quot;único&quot; ou &quot;múltiplo&quot; | Não | `single` | O tipo de seleção pode ser usado para restringir a seleção do Seletor de fragmentos. |
| `dialogSize` | &quot;fullscreen&quot; ou &quot;fullscreenTakeover&quot; | Não | `fullscreen` | Prop opcional para controlar o tamanho do diálogo. |
| `runningInUnifiedShell` | booleano | Não | | Se DestinationSelector está em execução no UnifiedShell ou autônomo. |
| `readonlyFilters` | CampoFiltrosSomenteLeituraRecurso[] | Não | | Filtros somente leitura aplicados à lista de fragmentos de conteúdo. Esses filtros não podem ser removidos pelo usuário. |
| `selectedFragments` | IdentificadorFragmentoConteúdo[] | Não | `[]` | Seleção inicial de fragmentos de conteúdo a serem pré-selecionados quando o seletor é aberto. |
| `hipaaEnabled` | booleano | Não | `false` | Indica se a conformidade com a HIPAA está habilitada. |
| `inventoryView` | TipodeVisualizaçãodeInventário | Não | `table` | Tipo de exibição padrão de estoque a ser usado no seletor. |
| `inventoryViewToggleEnabled` | booleano | Não | `false` | Indica se a opção de exibição de estoque está habilitada, permitindo que o usuário alterne entre as exibições de tabela e grade. |

## Propriedades de ImsAuthProps {#imsauthprops-properties}

As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Seletor de fragmento de conteúdo usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação deve se comportar e registrar ouvintes para vários eventos de autenticação.

| Nome de propriedade | Descrição |
|--- |--- |
| `imsClientId` | Um valor de string que representa a ID do cliente IMS usada para fins de autenticação. Esse valor é fornecido pela Adobe e é específico para a sua organização do Adobe AEM CS. |
| `imsScope` | Descreve os escopos usados na autenticação. Os escopos determinam o nível de acesso que o aplicativo tem aos recursos da organização. Vários escopos podem ser separados por vírgulas. |
| `redirectUrl` | Representa o URL para o qual o usuário é redirecionado após a autenticação. Normalmente, esse valor é definido como o URL atual do aplicativo. Se um `redirectUrl` não for fornecido, `ImsAuthService` usará o redirectUrl usado para registrar o `imsClientId` |
| `modalMode` | Um booleano que indica se o fluxo de autenticação deve ser exibido em um modal (pop-up) ou não. Se definido como `true`, o fluxo de autenticação será exibido em um pop-up. Se definido como `false`, o fluxo de autenticação será exibido em um recarregamento de página completo. _Observação :_para melhor UX, você pode controlar dinamicamente esse valor se o usuário tiver o pop-up do navegador desabilitado. |
| `onImsServiceInitialized` | Uma função de retorno de chamada que é chamada quando o serviço de autenticação do Adobe IMS é inicializado. Essa função recebe um parâmetro, `service`, que é um objeto que representa o serviço Adobe IMS. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obter mais detalhes. |
| `onAccessTokenReceived` | Uma função de retorno de chamada que é chamada quando um `imsToken` é recebido do serviço de autenticação do Adobe IMS. Esta função recebe um parâmetro, `imsToken`, que é uma cadeia de caracteres que representa o token de acesso. |
| `onAccessTokenExpired` | Uma função de retorno de chamada chamada chamada quando um token de acesso expira. Normalmente, essa função é usada para acionar um novo fluxo de autenticação para obter um novo token de acesso. |
| `onErrorReceived` | Uma função de retorno de chamada que é chamada quando ocorre um erro durante a autenticação. Essa função usa dois parâmetros: o tipo de erro e a mensagem de erro. O tipo de erro é uma cadeia de caracteres que representa o tipo de erro, e a mensagem de erro é uma cadeia de caracteres que representa a mensagem de erro. |

## Propriedades de ImsAuthService {#imsauthservice-properties}

A classe `ImsAuthService` manipula o fluxo de autenticação para o Seletor de fragmento de conteúdo. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao repositório do Adobe Experience Manager (AEM) CS. O ImsAuthService usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a conveniente função `registerContentFragmentSelectorAuthService` para registrar a instância `ImsAuthService` com o Seletor de fragmentos de conteúdo. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função `registerContentFragmentSelectorAuthService`, não será necessário chamar essas funções diretamente.

| Nome da função | Descrição |
|--- |--- |
| `isSignedInUser` | Determina se o usuário está conectado ao serviço no momento e retorna um valor booleano correspondente. |
| `getImsToken` | Recupera a autenticação `imsToken` para o usuário conectado no momento, que pode ser usada para autenticar solicitações para outros serviços, como geração de representação de ativos. |
| `signIn` | Inicia o processo de entrada do usuário. Esta função usa o `ImsAuthProps` para mostrar autenticação em um pop-up ou em um recarregamento de página completo. |
| `signOut` | Desconecta o usuário do serviço, invalidando seu token de autenticação e exigindo que ele entre novamente para acessar recursos protegidos. Chamar essa função recarregará a página atual. |
| `refreshToken` | Atualiza o token de autenticação do usuário conectado no momento, evitando a expiração e garantindo acesso ininterrupto aos recursos protegidos. Retorna um novo token de autenticação que pode ser usado para solicitações subsequentes. |
