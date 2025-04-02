---
title: Propriedades que podem ser usadas com o Seletor de fragmento de conteúdo de micro front-end para Adobe Experience Manager as a Cloud Service
description: Propriedades para configurar o Seletor de fragmento de conteúdo de micro front-end para pesquisar, localizar e recuperar fragmentos de conteúdo do aplicativo.
role: Admin, User
source-git-commit: 4d401213b34f8202efedc177387876d188a39d02
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---


# Seletor de fragmento de conteúdo — Propriedades relacionadas {#content-fragment-selector-related-properties}

O Seletor de fragmento de conteúdo de micro front-end permite navegar ou pesquisar fragmentos de conteúdo no repositório e usá-los no aplicativo.

Você pode usar as seguintes propriedades para personalizar como o Seletor de fragmento de conteúdo é renderizado e como ele pode ser usado:

## Propriedades do seletor de fragmentos de conteúdo {#content-fragment-selector-properties}

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|--- |--- |--- |--- |--- |
| `imsToken` | string | Não | | Token IMS usado para autenticação. |
| `repoId` | string | Não | | ID do repositório usada para autenticação. |
| `orgId` | string | Sim | | ID da organização usada para autenticação. |
| `locale` | string | Não | | Dados da localidade. |
| `env` | Ambiente | Não | | Ambiente de implantação do Seletor de fragmento de conteúdo. |
| `filters` | FiltroDeFragmentos | Não | | Filtros a serem aplicados na lista de fragmentos de conteúdo. Por padrão, os fragmentos em `/content/dam` serão exibidos. Valor padrão: `{ folder: "/content/dam" }` |
| `isOpen` | booleano | Sim | `false` | Sinalizador para acionar a abertura ou o fechamento do seletor. |
| `onDismiss` | () => void | Sim | | Função a ser chamada quando **Dispensar** for selecionado. |
| `onSubmit` | ({ contentFragments: `{id: string, path: string}[]`, domainNames: `string[]` }) => void | Função a ser chamada quando **Select** for usado após selecionar um ou mais Fragmentos de Conteúdo. <br><br>A função receberá:<br><ul><li> os fragmentos de conteúdo selecionados com campos `id` e `path`</li><li>e nomes de domínio relacionados à ID de programa e à ID de ambiente do repositório, que têm o status `ready` e a Publicação `tier`</li></ul><br>Se não houver nomes de domínio, ele usará a instância de Publicação como um domínio de fallback. |
| `theme` | &quot;light&quot; | &quot;escuro&quot; | Não | | Tema do Seletor de fragmentos de conteúdo. O tema padrão é definido como o tema do ambiente UnifiedShell. |
| `selectionType` | &quot;individual&quot; | &quot;multiple&quot; | Não | `single` | Tipo de seleção que pode ser usado para restringir a seleção do Seletor de fragmentos. |
| `dialogSize` | &quot;tela cheia&quot; | &quot;fullscreenTakeover&quot; | Não | `fullscreen` | Propriedade opcional para controlar o tamanho do diálogo. |
| `waitForImsToken` | booleano | Não | `false` | Indica se o Seletor de Fragmento de Conteúdo é renderizado no contexto do fluxo SUSI e precisa aguardar o `imsToken` estar pronto. |
| `imsAuthInfo` | ImsAuthInfo | Não | | Objeto que contém as informações de autenticação IMS do usuário conectado. |
| `runningInUnifiedShell` | booleano | Não | | Indica se o Seletor de fragmento de conteúdo está em execução no UnifiedShell ou independente. |
| `readonlyFilters` | CampoFiltrosSomenteLeituraRecurso | Não | | Filtros somente leitura que podem ser aplicados à lista de conteúdo - e não podem ser removidos. |

## Propriedades de ImsAuthProps {#imsauthprops-properties}

As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Seletor de fragmento de conteúdo usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação deve se comportar e registrar ouvintes para vários eventos de autenticação.

| Nome de propriedade | Descrição |
|--- |--- |
| `imsClientId` | Um valor de string que representa a ID do cliente IMS usada para fins de autenticação. Esse valor é fornecido pela Adobe e é específico para a sua organização do Adobe AEM CS. |
| `imsScope` | Descreve os escopos usados na autenticação. Os escopos determinam o nível de acesso que o aplicativo tem aos recursos da organização. Vários escopos podem ser separados por vírgulas. |
| `redirectUrl` | Representa o URL para o qual o usuário é redirecionado após a autenticação. Normalmente, esse valor é definido como o URL atual do aplicativo. Se um `redirectUrl` não for fornecido, `ImsAuthService` usará o redirectUrl usado para registrar o `imsClientId` |
| `modalMode` | Um booleano que indica se o fluxo de autenticação deve ser exibido em um modal (pop-up) ou não. Se definido como `true`, o fluxo de autenticação será exibido em um pop-up. Se definido como `false`, o fluxo de autenticação será exibido em um recarregamento de página completo.<br>**Observação:** para obter um UX melhor, você pode controlar este valor dinamicamente se o usuário tiver o pop-up do navegador desabilitado. |
| `onImsServiceInitialized` | Uma função de retorno de chamada que é chamada quando o serviço de autenticação do Adobe IMS é inicializado. Essa função recebe um parâmetro, `service`, que é um objeto que representa o serviço Adobe IMS. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obter mais detalhes. |
| `onAccessTokenReceived` | Uma função de retorno de chamada que é chamada quando um `imsToken` é recebido do serviço de autenticação do Adobe IMS. Esta função recebe um parâmetro, `imsToken`, que é uma cadeia de caracteres que representa o token de acesso. |
| `onAccessTokenExpired` | Uma função de retorno de chamada chamada chamada quando um token de acesso expira. Normalmente, essa função é usada para acionar um novo fluxo de autenticação para obter um novo token de acesso. |
| `onErrorReceived` | Uma função de retorno de chamada que é chamada quando ocorre um erro durante a autenticação. Essa função usa dois parâmetros: o tipo de erro e a mensagem de erro. O tipo de erro é uma cadeia de caracteres que representa o tipo de erro, e a mensagem de erro é uma cadeia de caracteres que representa a mensagem de erro. |

## Propriedades de ImsAuthService {#imsauthservice-properties}

A classe `ImsAuthService` manipula o fluxo de autenticação para o Seletor de fragmento de conteúdo. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao repositório do Adobe Experience Manager (AEM) CS. O ImsAuthService usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a conveniente função `registerContentFragmentSelectorAuthService` para registrar a instância `ImsAuthService` com o Seletor de fragmentos de conteúdo. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função `registerContentFragmentSelectorAuthService`, não será necessário chamar essas funções diretamente.

| Nome da função | Descrição |
|--- |--- |
| `isSignedInUser` | Determina se o usuário está conectado ao serviço no momento e retorna um valor booleano correspondente. |
| `getImsToken` | Recupera a autenticação `imsToken` para o usuário conectado no momento, que pode ser usada para autenticar solicitações para outros serviços, como gerar a representação _do ativo._ |
| `signIn` | Inicia o processo de entrada do usuário. Esta função usa o `ImsAuthProps` para mostrar autenticação em um pop-up ou em um recarregamento de página completo. |
| `signOut` | Desconecta o usuário do serviço, invalidando seu token de autenticação e exigindo que ele entre novamente para acessar recursos protegidos. Chamar essa função recarregará a página atual. |
| `refreshToken` | Atualiza o token de autenticação do usuário conectado no momento, evitando a expiração e garantindo acesso ininterrupto aos recursos protegidos. Retorna um novo token de autenticação que pode ser usado para solicitações subsequentes. |