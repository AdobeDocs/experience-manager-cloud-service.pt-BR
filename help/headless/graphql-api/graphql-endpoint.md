---
title: Gerenciar pontos de extremidade GraphQL no AEM
description: Saiba como gerenciar pontos de extremidade GraphQL no Adobe Experience Manager as a Cloud Service para entrega de conteúdo sem interface.
feature: Content Fragments,GraphQL API
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---


# Gerenciar pontos de extremidade GraphQL no AEM {#graphql-aem-endpoint}

O endpoint é o caminho usado para acessar GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acesse o esquema GraphQL,
* enviar suas consultas GraphQL,
* receba as respostas (para suas consultas GraphQL).

Há dois tipos de endpoints no AEM:

* Global
   * Disponível para uso por todos os sites.
   * Esse terminal pode usar todos os Modelos de fragmento de conteúdo de todas as configurações de Sites (definidas na variável [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Se houver Modelos de fragmento de conteúdo que devem ser compartilhados entre configurações de Sites, eles devem ser criados nas configurações globais de Sites.
* Configurações de sites:
   * Corresponde a uma configuração de Sites, conforme definido na variável [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Específico de um site/projeto especificado.
   * Um endpoint específico de configuração de Sites usará os Modelos de fragmento de conteúdo da configuração de Sites específica junto com aqueles da configuração de Sites global.

>[!CAUTION]
>
>O Editor de fragmento de conteúdo pode permitir que um Fragmento de conteúdo de uma configuração de Sites faça referência a um Fragmento de conteúdo de outra configuração de Sites (por meio de políticas).
>
>Nesse caso, nem todo o conteúdo poderá ser recuperado usando um endpoint específico da configuração de Sites .
>
>O autor de conteúdo deve controlar esse cenário; por exemplo, pode ser útil considerar colocar Modelos de fragmento de conteúdo compartilhados na configuração de Sites globais.

O caminho do repositório do GraphQL para AEM endpoint global é:

`/content/cq:graphql/global/endpoint`

Para o qual seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para ativar um terminal para GraphQL para AEM, é necessário:

* [Ativar o terminal GraphQL](#enabling-graphql-endpoint)
* [Publicar seu terminal GraphQL](#publishing-graphql-endpoint)

## Ativação do terminal GraphQL {#enabling-graphql-endpoint}

Para ativar um Endpoint GraphQL, primeiro é necessário ter uma configuração apropriada. Consulte [Fragmentos de conteúdo - Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se a variável [o uso de modelos de fragmento de conteúdo não foi ativado](/help/assets/content-fragments/content-fragments-configuration-browser.md), o **Criar** não estará disponível.

Para ativar o endpoint correspondente:

1. Navegar para **Ferramentas**, **Ativos**, em seguida selecione **GraphQL**.
1. Selecione **Criar**.
1. O **Criar novo ponto de extremidade GraphQL** será aberta. Aqui você pode especificar:
   * **Nome**: nome do ponto final; você pode inserir qualquer texto.
   * **Use o esquema GraphQL fornecido por**: use a lista suspensa para selecionar o site/projeto necessário.

   >[!NOTE]
   >
   >O seguinte aviso é mostrado na caixa de diálogo:
   >
   >* *Os pontos de extremidade do GraphQL podem causar problemas de segurança e desempenho de dados se não forem gerenciados com cuidado. Defina as permissões apropriadas após criar um ponto de extremidade.*


1. Confirme com **Criar**.
1. O **Próximas etapas** Essa caixa de diálogo fornecerá um link direto para o console Segurança para que você possa garantir que o endpoint recém-criado tenha as permissões adequadas.

   >[!CAUTION]
   >
   >O endpoint é acessível a todos. Isso pode - especialmente em instâncias de publicação - causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
   >
   >Você pode configurar ACLs, apropriadas ao seu caso de uso, no terminal.

## Publicar seu ponto de extremidade GraphQL {#publishing-graphql-endpoint}

Selecione o novo terminal e **Publicar** para disponibilizá-lo totalmente em todos os ambientes.

>[!CAUTION]
>
>O endpoint é acessível a todos.
>
>Em instâncias de publicação, isso pode causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
>
>Você deve configurar [ACLs apropriadas ao seu caso de uso](/help/headless/security/permissions.md) no terminal.