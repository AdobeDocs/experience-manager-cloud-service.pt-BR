---
title: 'Considerações de permissão para conteúdo sem periféricos '
description: Saiba mais sobre as diferentes permissões e considerações de ACL para uma implementação sem cabeçalho com o Adobe Experience Manager. Entenda as diferentes personas e os possíveis níveis de permissão necessários para os ambientes Autor e Publicação.
feature: Content Fragments,GraphQL API
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Considerações de permissão para conteúdo sem periféricos

Com uma implementação sem cabeçalho, há várias áreas de segurança e permissões que devem ser abordadas. As permissões e as pessoas podem ser amplamente consideradas com base no ambiente de AEM **Autor** ou **Publicar**. Cada ambiente contém personas diferentes e com necessidades diferentes.

## Considerações sobre o serviço de criação

O serviço Autor é onde os usuários internos criam, gerenciam e publicam conteúdo. As permissões giram em torno de diferentes personas que gerenciam conteúdo.

### Gerenciar permissões no nível do Grupo

Como prática recomendada, as permissões devem ser definidas em Grupos no AEM. Também conhecidos como grupos locais, esses grupos podem ser gerenciados no ambiente de criação de AEM.

A maneira mais fácil de gerenciar a associação de grupo é usar grupos do Adobe Identity Management System (IMS) e atribuir [Grupos IMS para grupos de AEM locais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem).

![Fluxo de permissão do Admin Console](assets/admin-console-aem-group-permissions.png)

Em um alto nível, o processo é:

1. Adicionar usuários do IMS a um grupo de usuários do IMS novo ou existente usando o [Admin Console](https://adminconsole.adobe.com/)
1. Os grupos IMS são sincronizados com AEM quando os usuários fazem logon.
1. Atribuir grupos IMS a grupos de AEM.
1. Defina permissões em Grupos de AEM.
1. Quando os usuários fazem logon no AEM e são autenticados por meio do IMS, eles herdam as permissões do grupo AEM.

>[!TIP]
>
> Uma apresentação detalhada em vídeo do gerenciamento de usuários e grupos do IMS e AEM pode ser encontrada [here](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html).

Para gerenciar **grupos** no AEM, navegue até **Ferramentas** > **Segurança** > **Grupos**.

Para gerenciar permissões de grupos no AEM, navegue até **Ferramentas** > **Segurança** > **Permissões**.

### Usuários de DAM

&quot;DAM&quot;, nesse contexto, significa Gerenciamento de ativos digitais. O **Usuários de DAM** O é um grupo pronto para uso no AEM que pode ser usado para usuários &quot;diários&quot; que gerenciam ativos digitais e Fragmentos de conteúdo. Esse grupo fornece permissões para **exibir**, **adicionar**, **atualizar**, **excluir** e **publicar** Fragmentos de conteúdo e todos os outros arquivos no AEM Assets.

Se estiver usando o IMS para associação de grupo, adicione os Grupos IMS apropriados como membros do **Usuários de DAM** grupo. Os membros do grupo IMS herdam as permissões do grupo Usuários do DAM ao fazer logon no ambiente AEM.

#### Personalizar grupo de usuários do DAM

É melhor não modificar diretamente as permissões de um grupo pronto para uso. Em vez disso, você também pode criar seus próprios grupos modelados após a variável **Usuários de DAM** permissões de grupo e restringir ainda mais o acesso a diferentes **pastas** no AEM Assets.

Para obter permissões mais granulares, use o **Permissões** no AEM e atualize o caminho de `/content/dam` para um caminho mais específico, ou seja, `/content/dam/mycontentfragments`.

Pode ser desejável conceder a esse grupo de usuários permissões para criar e editar fragmentos de conteúdo, mas não excluir. Para revisar e atribuir permissões para edição, mas não excluir, consulte [Fragmentos de conteúdo - excluir considerações](/help/assets/content-fragments/content-fragments-delete.md).

### Editores de modelo

A capacidade de modificar **Modelos de fragmentos do conteúdo** deve ser deixada para administradores ou um **grupo pequeno** de usuários com permissões elevadas. A modificação do modelo do fragmento de conteúdo tem muitos efeitos de downstream.

>[!CAUTION]
>
>As modificações nos Modelos de fragmento de conteúdo alteram a API GraphQL subjacente à qual os aplicativos sem periféricos dependem.

Se quiser criar um grupo que gerencia os Modelos de fragmentos de conteúdo, mas não o acesso completo do administrador, é possível criar um grupo com as seguintes entradas de controle de acesso:

| Caminho | Permissão | Privilégios |
|-----| -------------| ---------|
| `/conf` | **permitir** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **permitir** | `rep:write`, `crx:replicate` |

## Publicar permissões de serviço

O serviço de Publicação é considerado o ambiente &quot;live&quot; e normalmente é com o que os consumidores de API GraphQL interagem. O conteúdo, depois de ser editado e aprovado no serviço Autor, é publicado no serviço de Publicação. O aplicativo sem cabeçalho consome o conteúdo aprovado do serviço de Publicação por meio de APIs GraphQL.

Por padrão, o conteúdo exposto por meio dos pontos de extremidade GraphQL do serviço de Publicação AEM é acessível a todos, incluindo usuários não autenticados.

### Permissões de conteúdo

O conteúdo exposto por meio AEM APIs GraphQL pode ser restrito usando [Grupos de usuários fechados (CUGs)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) definido nas pastas de ativos, que especificam quais AEM Grupos de usuários (e seus membros) podem acessar o conteúdo das pastas Ativos.

Os CUGs do Assets trabalham por:

* Primeiro, negando todo o acesso à pasta e às subpastas
* Em seguida, permitindo o acesso de leitura à pasta e às subpastas para todos os Grupos de Usuários AEM listados na lista de CUGs

Os CUGs podem ser configurados em pastas de ativos que contêm conteúdo exposto por meio de APIs GraphQL. O acesso às pastas de ativos na publicação do AEM deve ser controlado por grupos de usuários, em vez de pelo usuário diretamente. Crie (ou reutilize) um grupo de usuários AEM que conceda acesso a pastas de ativos que contenham conteúdo exposto por APIs GraphQL.

#### Selecione o esquema de autenticação{#publish-permissions-users}

O [SDK sem cabeçalho AEM](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) O suporta dois tipos de autenticação:

* [Autenticação por token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) usando credenciais de serviço vinculadas a uma única conta técnica.
* Autenticação básica usando usuários AEM.

### Acesse a API GraphQL

Solicitações HTTP que fornecem a variável [credenciais de autenticação apropriadas](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) para os pontos de extremidade da API GraphQL do serviço de publicação do AEM, inclua o conteúdo para o qual as credenciais estão autorizadas a ler e o conteúdo acessível anonimamente. Outros consumidores da API GraphQL não podem ler o conteúdo nas pastas protegidas por CUGs.

