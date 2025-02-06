---
title: Reutilizar código entre sites
description: Se você tiver muitos sites semelhantes que parecem e se comportam principalmente da mesma forma, mas têm conteúdo diferente, saiba como compartilhar código em vários sites em um modelo de resposta.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Reutilizar código entre sites {#repoless}

Se você tiver muitos sites semelhantes que parecem e se comportam principalmente da mesma forma, mas têm conteúdo diferente, saiba como compartilhar código em vários sites em um modelo de resposta.

## Uma base de código para vários sites {#one-codebase}

Por padrão, o AEM está rigorosamente vinculado ao seu repositório de código, que atende à maioria dos casos de uso. No entanto, você pode ter vários sites que diferem principalmente em seu conteúdo, mas que podem aproveitar a mesma base de código.

Em vez de criar vários repositórios GitHub e executar cada site fora de um repositório GitHub dedicado enquanto os mantém em sincronia, o AEM oferece suporte à execução de vários sites a partir da mesma base de código.

Essa configuração simplificada, que elimina a necessidade de replicação de código, também é conhecida como [&quot;resposta&quot;](https://www.aem.live/docs/repoless), porque todos, exceto seu primeiro site, não precisam de um repositório GitHub próprio.

Se o projeto exigir a flexibilidade de resposta da reutilização de código entre sites, você poderá ativar o recurso.

Independentemente de quantos sites você deseja criar, no final das contas, de maneira ininterrupta, você deve criar seu primeiro site, que serve como site base. Este documento explica como criar seu primeiro site para uso de respostas.

## Pré-requisitos {#prerequisites}

Para aproveitar esse recurso, verifique se você fez o seguinte.

* Seu site já está totalmente configurado, seguindo o documento [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Você está executando o AEM as a Cloud Service 2024.08 no mínimo.

Você também precisará pedir ao Adobe para configurar os seguintes itens para você. Entre em contato com o canal Slack ou gere um problema de suporte para solicitar que o Adobe faça as seguintes alterações:

* Peça para ativar o [serviço de configuração aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) para seu ambiente e que você esteja configurado como administrador.
* Peça para ativar o recurso de resposta para o seu programa por Adobe.
* Peça ao Adobe para criar a organização para você.

## Recurso Ativar Respostas {#activate}

Há várias etapas para ativar a funcionalidade de resposta para o seu projeto.

1. [Recuperar token de acesso](#access-token)
1. [Definir serviço de configuração](#config-service)
1. [Adicionar configuração de site e conta técnica](#access-control)
1. [Atualizar configuração do AEM](#update-aem)
1. [Autenticar site](#authenticate-site)

Essas etapas usam o site `https://wknd.site` como exemplo. Substitua o seu adequadamente.

### Recuperar token de acesso {#access-token}

Primeiro, você precisará de um token de acesso para usar o serviço de configuração e configurá-lo para o caso de uso de resposta.

1. Vá para `https://admin.hlx.page/login` e use o endereço `login_adobe` para fazer logon com o provedor de identidade Adobe.
1. Você será encaminhado a `https://admin.hlx.page/profile`.
1. Ao usar as ferramentas de desenvolvedor do seu navegador, copie o valor do `x-auth-token` do cookie JSON web token que a página `admin.hlx.page` define.

Depois de receber o token de acesso, ele poderá ser passado no cabeçalho de solicitações cURL no formato a seguir.

```text
--header 'x-auth-token: <your-token>'
```

### Adicionar mapeamento de caminho para configuração do site e definir conta técnica {#access-control}

É necessário criar uma configuração de site e adicioná-la ao mapeamento de caminho.

1. Crie uma nova página na raiz do site e escolha o modelo [**Configuração**](/help/edge/wysiwyg-authoring/tabular-data.md#other).
   * Você pode deixar a configuração vazia apenas com as colunas `key` e `value` predefinidas. Você só precisa criá-lo.
1. Crie um mapeamento na configuração pública para a configuração do site usando um comando cURL semelhante ao seguinte.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```
1. Valide se a configuração pública foi definida e está disponível com um comando cURL semelhante ao seguinte.

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

Depois que a configuração do site for mapeada, você poderá configurar o controle de acesso definindo sua conta técnica para que ela tenha privilégios para publicar.

1. No navegador, recupere a conta técnica na resposta do link a seguir.

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

1. A resposta será semelhante ao mostrado a seguir.

   ```json
   {
     "total": 1,
     "offset": 0,
     "limit": 1,
     "data": [
       {
         "key": "admin.role.publish",
         "value": "<tech-account-id>@techacct.adobe.com"
       }
     ],
     ":type": "sheet"
   }
   ```

1. Defina a conta técnica em sua configuração com um comando cURL semelhante ao seguinte.

   * Adapte o bloco `admin` para definir os usuários que devem ter acesso administrativo total ao site.
      * É uma matriz de endereços de email.
      * O curinga `*` pode ser usado.
      * Consulte o documento [Configurando a autenticação para autores](https://www.aem.live/docs/authentication-setup-authoring#default-roles) para obter mais informações.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "<email>@<domain>.<tld>"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

Como você agora usa o serviço de configuração, é possível remover `fstab.yaml` e `paths.json` do repositório Git.

>[!NOTE]
>
>Ao usar o serviço de configuração e expor o mapeamento de caminho via `config.json`, o arquivo `path.json` é ignorado.

Depois que o AEM é configurado para uso de resposta, você deve usar o serviço de configuração e fornecer um `config.json` válido com o mapeamento de caminhos.

### Atualizar configuração do AEM {#update-aem}

Agora você está pronto para fazer as mudanças necessárias para o seu Edge Delivery Services no AEM.

1. Entre na instância de autor do AEM e vá para **Ferramentas** -> **Cloud Service** -> **Configuração de Edge Delivery Services** e selecione a configuração que foi criada automaticamente para seu site e toque ou clique em **Propriedades** na barra de ferramentas.
1. Na janela **Configuração de Edge Delivery Services**, altere o tipo de projeto para **aem.live com configuração de resposta** e toque ou clique em **Salvar e fechar**.
   ![Configuração de Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Retorne ao site usando o Editor universal e verifique se ele ainda é renderizado corretamente.
1. Modifique parte do seu conteúdo e publique-o novamente.
1. Visite seu site publicado em `https://main--<your-aem-project>--<your-github-org>.aem.page/` e verifique se as alterações foram refletidas corretamente.

Seu projeto está configurado para uso sem resposta.

## Próximas etapas {#next-steps}

Agora que o site base está configurado para uso sem resposta, você pode criar sites adicionais que utilizam a mesma base de código. Consulte a documentação a seguir dependendo do caso de uso.

* [Gerenciamento de vários sites de resposta](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Ambientes de preparo e produção de respostas](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)

## Resolução de problemas {#troubleshooting}

O problema mais comum encontrado após a configuração do caso de uso de resposta é que as páginas no Universal Editor não são mais renderizadas ou você recebe uma página branca ou uma mensagem de erro genérica do AEM as a Cloud Service. Nesses casos:

* Visualize o código-fonte da página renderizada.
   * Há realmente algo renderizado (cabeçalho de HTML correto com `scripts.js`, `aem.js` e arquivos JSON relacionados ao editor)?
* Verifique se há exceções no AEM `error.log` da instância do autor.
   * O problema mais comum é que o componente de Página falha com erros 404.
   * `config.json or paths.json` não pode ser carregado
   * `component-definition.json` etc. não pode ser carregado
