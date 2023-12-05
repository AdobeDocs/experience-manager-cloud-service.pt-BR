---
title: Gerenciar endpoints de GraphQL no AEM
description: Saiba como gerenciar endpoints de GraphQL no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
feature: Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 88%

---

# Gerenciar endpoints de GraphQL no AEM {#graphql-aem-endpoint}

O endpoint é o caminho usado para acessar o GraphQL no AEM. Usando esse caminho, você (ou seu aplicativo) pode:

* acessar o esquema de GraphQL,
* enviar suas consultas de GraphQL,
* receber as respostas (para suas consultas de GraphQL).

Há dois tipos de endpoints no AEM:

* Global
   * Disponível para uso por todos os sites.
   * Esse endpoint pode usar todos os modelos de fragmento de conteúdo de todas as configurações do Sites (definidas no [Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)).
   * Se houver modelos de fragmento de conteúdo que devem ser compartilhados entre as configurações do Sites, eles devem ser criados nas configurações globais do Sites.
* Configurações do Sites:
   * Corresponde a uma configuração do Sites, conforme definido no [Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).
   * Específico de um site/projeto especificado.
   * Um endpoint específico de uma configuração do Sites usará os modelos de fragmento de conteúdo dessa configuração, junto com aqueles da configuração global do Sites.

>[!CAUTION]
>
>O Editor de fragmento de conteúdo pode permitir que um fragmento de conteúdo de uma configuração do Sites faça referência a um fragmento de conteúdo de outra configuração do Sites (por meio de políticas).
>
>Nesse caso, nem todo o conteúdo poderá ser recuperado usando um ponto de acesso específico de uma configuração do Sites.
>
>O autor de conteúdo deve controlar esse cenário; por exemplo, pode ser útil considerar colocar modelos de fragmento de conteúdo compartilhados na configuração global do Sites.

O caminho do repositório do GraphQL para o endpoint global do AEM é:

`/content/cq:graphql/global/endpoint`

Para o qual seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar um endpoint para GraphQL no AEM, é necessário:

* [Habilitar seu endpoint de GraphQL](#enabling-graphql-endpoint)
* [Publicar seu endpoint de GraphQL](#publishing-graphql-endpoint)

## Habilitação do seu endpoint de GraphQL {#enabling-graphql-endpoint}

Para habilitar um endpoint de GraphQL, primeiro é necessário ter uma configuração apropriada. Consulte [Fragmentos de conteúdo - Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).

>[!CAUTION]
>
>Se o [uso de modelos de fragmento de conteúdo não foi habilitado](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser), a opção **Criar** não estará disponível.

Para habilitar o endpoint correspondente:

1. Navegue até **Ferramentas**, **Geral** e, em seguida, selecione **GraphQL**.
1. Selecione **Criar**.
1. A variável **Criar novo endpoint do GraphQL** será aberta. Aqui, é possível especificar:
   * **Nome**: nome do endpoint; é possível inserir qualquer texto.
   * **Usar esquema do GraphQL fornecido por**: use a lista suspensa para selecionar o site/projeto necessário.

   >[!NOTE]
   >
   >O seguinte aviso é mostrado na caixa de diálogo:
   >
   >* *Os endpoints do GraphQL podem apresentar problemas de desempenho e de segurança de dados se não forem gerenciados com cuidado. Certifique-se de que as permissões apropriadas estejam definidas após a criação de um ponto de acesso.*

1. Confirme com **Criar**.
1. A variável **Próximas etapas** fornecerá um link direto para o console de Segurança, para que você possa garantir que o endpoint criado tenha as permissões adequadas.

   >[!CAUTION]
   >
   >O endpoint é acessível a todos. Isso pode causar uma preocupação de segurança, especialmente em instâncias de publicação, já que as consultas de GraphQL podem colocar uma carga pesada sobre o servidor.
   >
   >É possível configurar ACLs apropriadas ao seu caso de uso no endpoint.

## Publicar seu endpoint de GraphQL {#publishing-graphql-endpoint}

Selecione o novo endpoint e escolha **Publicar** para disponibilizá-lo completamente, em todos os ambientes.

>[!CAUTION]
>
>O endpoint é acessível a todos.
>
>Isso pode causar uma preocupação de segurança em instâncias de publicação, já que as consultas de GraphQL podem colocar uma carga pesada sobre o servidor.
>
>Configurar [ACLs apropriadas ao seu caso de uso](/help/headless/security/permissions.md) no endpoint.
