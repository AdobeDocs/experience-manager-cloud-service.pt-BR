---
title: Ambientes de preparo e produção de respostas
description: Saiba como configurar sites separados para seus ambientes de preparo e produção, aproveitando uma única base de código de maneira imperceptível.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 701bd9bc-30e8-4654-8248-a06d441d1504
source-git-commit: c9d0d3cd7e18b56db36a379b63f8fb48e18a40db
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# Ambientes de preparo e produção de respostas {#repoless-stage-prod}

Saiba como configurar sites separados para seus ambientes de preparo e produção, aproveitando uma única base de código de maneira imperceptível.

## Visão geral {#overview}

Talvez você queira configurar um site para seu ambiente de produção separado do ambiente de preparo. A configuração de um segundo site para uma configuração de preparo e produção separada é semelhante à [configuração necessária para o gerenciamento de vários sites](/help/edge/wysiwyg-authoring/repoless-msm.md). Na verdade, ele pode ser combinado com estruturas de site do MSM, se necessário.

Este documento usa o exemplo típico de ambientes de preparo e produção separados. É possível criar ambientes separados para qualquer ambiente.

## Requisitos {#requirements}

Para configurar ambientes de preparo e produção de respostas, primeiro conclua as seguintes tarefas:

* Este documento supõe que você já tenha criado um site para o seu projeto com base no [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o guia do Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Você já deve ter [habilitado o recurso de resposta para o seu projeto.](/help/edge/wysiwyg-authoring/repoless.md)

## Configuração {#configuration}

Este documento descreve como configurar um site de produção separado para seu projeto usando a mesma base de código. As seguintes suposições são feitas.

* O site de preparo já está configurado e você agora deseja criar uma configuração para o site de produção.
* A estrutura de conteúdo na criação do AEM é semelhante.
* Os mesmos mapeamentos de caminho serão usados para preparo e produção.

Neste exemplo, pressupomos que um site de produção já foi criado para o projeto chamado wknd, cujo repositório GitHub também é chamado de wknd.

Há duas etapas para configurar um site de produção separado.

1. [Crie novos sites do Edge Delivery Services para seu ambiente de produção](#create-edge-site).
1. [Atualize a configuração da nuvem no AEM para seu site de produção](#update-cloud-configuration).

### Criar novos sites do Edge Delivery Services para seu ambiente de produção {#create-edge-site}

1. Recupere o token de autenticação e a conta técnica do programa.
   * Consulte o documento **Reutilizando Código entre Sites** para obter detalhes sobre como [obter seu token de acesso](/help/edge/wysiwyg-authoring/repoless.md#access-token) e a [conta técnica](/help/edge/wysiwyg-authoring/repoless.md#access-control) para seu programa.
1. Crie um novo site fazendo a seguinte chamada para o serviço de configuração. Considere:
   * O nome do projeto na URL POST deve ser o novo nome de site que você está criando. Neste exemplo, ele é `wknd-prod`.
   * A configuração `code` deve ser a mesma usada para a criação inicial do projeto.
   * O `content` > `source` > `url` deve ser adaptado ao nome do novo site que você está criando. Neste exemplo, ele é `wknd-prod`.
   * Ou seja, o nome do site na URL POST e o `content` > `source` > `url` devem ser os mesmos.
   * Adapte o bloco `admin` para definir os usuários que devem ter acesso administrativo total ao site.
      * É uma matriz de endereços de email.
      * O curinga `*` pode ser usado.
      * Consulte o documento [Configurando a autenticação para autores](https://www.aem.live/docs/authentication-setup-authoring#default-roles) para obter mais informações.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
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
       }
   }'
   ```

1. Adicione o mapeamento de caminho para o novo site fazendo a seguinte chamada para o serviço de configuração.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

Verifique se a configuração pública do novo site está funcionando chamando `https://main--wknd-prod--<your-github-org>.aem.page/config.json` e verificando o conteúdo do JSON retornado.

### Atualize as configurações da nuvem no AEM para seu site de produção {#update-cloud-configuration}

Seu AEM de produção deve ser configurado para usar o novo Edge Delivery Sites criado na seção anterior para um site de produção dedicado. Neste exemplo, o conteúdo em `/content/wknd` no seu ambiente de produção precisa saber para usar o site `wknd-prod` que você criou.

1. Faça logon na instância de produção do AEM e acesse **Ferramentas** -> **Cloud Services** -> **Configuração do Edge Delivery Services**.
1. Selecione a configuração que foi criada automaticamente para o seu projeto.
1. Toque ou clique em **Propriedades** na barra de ferramentas.
1. Na janela **Configuração do Edge Delivery Services**:
   * Forneça sua organização do GitHub no campo **Organização**.
   * Altere o nome do site para o nome do site criado na seção anterior. Nesse caso, seria `wknd-prod`.
   * Altere o tipo de projeto para **aem.live com a configuração de resposta**.
1. Toque ou clique em **Salvar e fechar**.

## Verificar a configuração {#verify}

Agora que você fez todas as alterações necessárias na configuração, verifique se tudo está funcionando como esperado.

1. Faça logon na instância de criação de produção do AEM.
1. Navegue até o **Console de Sites**, acessando **Navegação** -> **Sites**.
1. Selecione uma página no seu site.
1. Toque ou clique em **Editar** na barra de ferramentas.
1. Verifique se a página é renderizada corretamente no Editor universal e usa o mesmo código da raiz do site.
1. Faça uma alteração na página e publique-a novamente.
1. Visite seu novo site do Edge Delivery Services para essa página em `https://main--wknd-prod--<your-github-org>.aem.page`.

Se você vir as alterações feitas, a configuração separada do site de produção está funcionando corretamente.
