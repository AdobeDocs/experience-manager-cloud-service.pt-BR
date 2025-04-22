---
title: Gerenciamento de vários sites de resposta
description: Saiba mais sobre as práticas recomendadas de como configurar um projeto de maneira responsiva com sites localizados que aproveitam uma única base de código, cada um disponibilizado pelo Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 1%

---

# Gerenciamento de vários sites de resposta {#repoless-msm}

Saiba mais sobre as práticas recomendadas de como configurar um projeto de maneira responsiva com sites localizados que aproveitam uma única base de código, cada um disponibilizado pelo Edge Delivery Services.

## Visão geral {#overview}

O [Gerenciador de vários sites (MSM)](/help/sites-cloud/administering/msm/overview.md) e seus recursos de Live Copy permitem usar o conteúdo do mesmo site em vários locais, permitindo variações. Você pode criar conteúdo uma vez e Live Copies. O MSM mantém relacionamentos dinâmicos entre o conteúdo original e suas Live Copies, de modo que, quando você alterar o conteúdo original, a origem e as Live Copies possam ser sincronizadas.

Você pode usar o MSM para criar uma estrutura completa de conteúdo para sua marca em localidades e idiomas, criando o conteúdo centralmente. Seus sites localizados podem ser entregues pela Edge Delivery Services, aproveitando uma base de código central.

## Requisitos {#requirements}

Para configurar o MSM em um caso de uso de resposta, primeiro conclua as seguintes tarefas:

* Este documento supõe que você já tenha criado um site para o seu projeto com base no [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Você já deve ter [habilitado o recurso de resposta para o seu projeto](/help/edge/wysiwyg-authoring/repoless.md).

## Caso de uso {#use-case}

Este documento supõe que você já tenha criado uma estrutura básica de site localizada para o seu projeto. Como exemplo, ela usa a seguinte estrutura para a marca wknd com presença na Suíça e na Alemanha.

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

O conteúdo em `language-masters` é a origem das Live Copies para os sites localizados: Alemanha (`de`) e Suíça (`ch`). O objetivo deste documento é criar sites do Edge Delivery Services que usam a mesma base de código para cada site localizado.

## Configuração {#configuration}

Há várias etapas para configurar o caso de uso de resposta do MSM.

1. [Atualizar configurações do site AEM](#update-aem-configurations).
1. [Crie novos sites do Edge Delivery Services para suas páginas localizadas](#create-edge-sites).
1. [Atualize a configuração da nuvem no AEM para seus sites localizados](#update-cloud-configurations).

### Atualizar configurações do site do AEM {#update-aem-configurations}

[As configurações](/help/implementing/developing/introduction/configurations.md) podem ser consideradas espaços de trabalho que podem ser usados para coletar grupos de configurações e seu conteúdo associado para fins organizacionais. Ao criar um site no AEM, uma configuração é criada automaticamente para ele.

Em geral, você deseja compartilhar determinado conteúdo entre sites, como:

* Modelos criados a partir do conteúdo no blueprint
* Modelos de fragmentos de conteúdo, consultas persistentes etc.

É possível criar configurações adicionais para facilitar esse compartilhamento. Para o caso de uso wknd, precisaríamos de configurações para os seguintes caminhos.

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

Ou seja, você terá uma configuração para a raiz do conteúdo da marca wknd (`/content/wknd`) usado pelos blueprints e uma configuração usada por cada site localizado (Suíça e Alemanha).

1. Faça logon na instância de criação do AEM.
1. Navegue até o **Navegador de Configuração** acessando **Ferramentas** -> **Geral** -> **Navegador de Configuração**.
1. Selecione a configuração que foi criada automaticamente para o seu projeto (neste caso, wknd) e toque ou clique em **Criar** na barra de ferramentas.
1. Na caixa de diálogo **Criar Configuração**, forneça um **Nome** descritivo para o site localizado (como `Switzerland`) e para o **Título** use o mesmo título do tamanho localizado (neste caso, `ch`).
1. Selecione o recurso **Configuração da nuvem** e todos os recursos adicionais necessários para o seu projeto, como **Modelos editáveis**.
1. Toque ou clique em **Criar**.

Crie configurações para cada site localizado necessário. No caso do wknd, você precisaria criar uma configuração para `de`, bem como junto com a configuração `ch`.

Depois que as configurações forem criadas, você precisará garantir que os sites localizados as usem.

1. Faça logon na instância de criação do AEM.
1. Navegue até o **Console de Sites**, acessando **Navegação** -> **Sites**.
1. Selecione o site localizado, como `Switzerland`.
1. Toque ou clique em **Propriedades** na barra de ferramentas.
1. Na janela de propriedades da página, selecione a guia **Avançado** e, no cabeçalho **Configuração**, desmarque a opção **Herdado de /content/wknd**, em que `wknd` é a raiz do site.
1. No campo **Configuração da nuvem**, use o navegador de caminho para selecionar a configuração que você criou para seu site localizado, como `Switzerland` em `/conf/wknd/ch`.
1. Toque ou clique em **Salvar e fechar**.

Atribua as respectivas configurações aos sites localizados adicionais. No caso do wknd, também seria necessário atribuir a configuração `/conf/wknd/de` ao site da Alemanha.

### Criar novos sites do Edge Delivery Services para suas páginas localizadas {#create-edge-sites}

Para conectar mais sites ao Edge Delivery Services para uma configuração de site com várias regiões e vários idiomas, você deve configurar um novo site aem.live para cada um dos sites do AEM MSM. Há uma relação 1:1 entre os sites do AEM MSM e os sites aem.live com um repositório Git compartilhado e uma base de código.

Neste exemplo, criaremos o site `wknd-ch` para a presença suíça do wknd, cujo conteúdo localizado está no caminho do AEM `/content/wknd/ch`.

1. Recupere o token de autenticação e a conta técnica do programa.
   * Consulte o documento **Reutilizando Código entre Sites** para obter detalhes sobre como [obter seu token de acesso](/help/edge/wysiwyg-authoring/repoless.md#access-token) e a [conta técnica](/help/edge/wysiwyg-authoring/repoless.md#access-control) para seu programa.
1. Crie um novo site fazendo a seguinte chamada para o serviço de configuração. Considere:
   * O nome do projeto na URL POST deve ser o novo nome de site que você está criando. Neste exemplo, ele é `wknd-ch`.
   * A configuração `code` deve ser a mesma usada para a criação inicial do projeto.
   * O `content` > `source` > `url` deve ser adaptado ao nome do novo site que você está criando. Neste exemplo, ele é `wknd-ch`.
   * Ou seja, o nome do site na URL POST e o `content` > `source` > `url` devem ser os mesmos.
   * Adapte o bloco `admin` para definir os usuários que devem ter acesso administrativo total ao site.
      * É uma matriz de endereços de email.
      * O curinga `*` pode ser usado.
      * Consulte o documento [Configurando a autenticação para autores](https://www.aem.live/docs/authentication-setup-authoring#default-roles) para obter mais informações.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
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
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
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
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. Verifique se a configuração pública do novo site está funcionando chamando `https://main--wknd-ch--<your-github-org>.aem.page/config.json` e verificando o conteúdo do JSON retornado.

Repita as etapas para criar sites localizados adicionais. No caso do wknd, também seria necessário criar um site `wknd-de` para a presença alemã.

### Atualizar configurações da nuvem no AEM para suas páginas localizadas {#update-cloud-configurations}

Suas páginas no AEM devem ser configuradas para usar os novos Sites do Edge Delivery criados na seção anterior para sua presença localizada. Neste exemplo, o conteúdo em `/content/wknd/ch` precisa saber como usar o site `wknd-ch` que você criou. Da mesma forma, o conteúdo em `/content/wknd/de` precisa usar o site `wknd-de`.

1. Entre na instância do autor do AEM e vá para **Ferramentas** -> **Serviços da Nuvem** -> **Configuração do Edge Delivery Services**.
1. Selecione a configuração que foi criada automaticamente para o projeto e, em seguida, a pasta que foi criada para a página localizada. Nesse caso, seria a Suíça (`ch`).
1. Toque ou clique em **Criar** > **Configuração** na barra de ferramentas.
1. Na janela **Configuração do Edge Delivery Services**:
   * Forneça sua organização do GitHub no campo **Organização**.
   * Altere o nome do site para o nome do site criado na seção anterior. Nesse caso, seria `wknd-ch`.
   * Altere o tipo de projeto para **aem.live com a configuração de resposta**.
1. Toque ou clique em **Salvar e fechar**.

## Verificar a configuração {#verify}

Agora que você fez todas as alterações necessárias na configuração, verifique se tudo está funcionando como esperado.

1. Faça logon na instância de criação do AEM.
1. Navegue até o **Console de Sites**, acessando **Navegação** -> **Sites**.
1. Selecione o site localizado, como `Switzerland`.
1. Toque ou clique em **Editar** na barra de ferramentas.
1. Verifique se a página é renderizada corretamente no Editor universal e usa o mesmo código da raiz do site.
1. Faça uma alteração na página e publique-a novamente.
1. Visite seu novo site do Edge Delivery Services para a página localizada em `https://main--wknd-ch--<your-github-org>.aem.page`.

Se você vir as alterações feitas, a configuração do MSM está funcionando corretamente.
