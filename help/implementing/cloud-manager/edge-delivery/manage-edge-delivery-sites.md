---
title: Gerenciar sites do Edge Delivery no Cloud Manager
description: Saiba como adicionar uma configuração de CDN a um site do Edge Delivery ou excluir um site do Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---

# Gerenciar o site do Edge Delivery no Cloud Manager {#manage-edge-delivery-sites}

Saiba como gerenciar sites do Edge Delivery no Cloud Manager adicionando uma configuração de CDN a um site existente. Ou exclua um site do Edge Delivery.

## Adicionar um mapeamento de domínio a um site existente do Edge Delivery {#add-cdn-to-edge-delivery-site}

Consulte [Adicionar um mapeamento de domínio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Renomear um site do Edge Delivery (#rename-edge-delivery-site)

No Adobe Cloud Manager, talvez você queira renomear um site do Edge Delivery por vários motivos:

* **Clareza e organização**: descrever melhor a finalidade do site ou seu ambiente associado (por exemplo, produção, preparo).
* **Evitando confusão**: se vários sites estiverem em uso, renomeá-los pode ajudar a diferenciá-los facilmente, reduzindo a chance de aplicar configurações ou atualizações ao site errado.
* **Padronização**: para seguir uma convenção de nomenclatura consistente que se alinhe às diretrizes de sua organização para facilitar o gerenciamento e a auditoria.

**Para renomear um site do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Na tabela do site do Edge Delivery, clique nas reticências no final de uma linha cujo site você deseja renomear.
Clique em **Renomear**.
   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo. No cabeçalho **Serviços**, clique em ![ícone de páginas da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja renomear. Clique em **Renomear**.

1. Na caixa de diálogo **Editar Site do Edge Delivery**, no campo de texto **Nome do Site**, digite o novo nome do site.
1. Clique em **Editar**.


## Ativar o nível de publicação para um site do Edge Delivery (Beta) {#activate-publish-tier-for-eds}

>[!NOTE]
>
>O recurso de publicação descrito aqui está no Beta. Para ingressar na Beta, envie um email para [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) com sua ID da organização da Adobe e a ID do programa.

Esse recurso se aplica somente aos sites do Edge Delivery criados com a opção **Criação do AEM** em Programas nos quais o recurso de camada de publicação flexível está habilitado.

Se o site do Edge Delivery usa criação do AEM, o nível de publicação não será provisionado por padrão, pois o Edge Delivery lida com a entrega de conteúdo. No entanto, você pode ativar o nível de publicação a qualquer momento se o site exigir. Por exemplo, se você precisar oferecer suporte à publicação tradicional do AEM junto com o Edge Delivery.

Depois que o site do Edge Delivery for criado e o status mostrar **Verificado** no Cloud Manager, você poderá criar e publicar conteúdo usando o Editor Universal do AEM.

**Para acessar o Editor Universal do Cloud Manager:**

1. Na guia Edge Delivery, na lista de sites do Edge Delivery, localize o site.

   ![Publicando conteúdo do Autor do AEM na Edge Delivery.](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. Clique no link **Source de Conteúdo** na linha do site. O link abre a página do Editor universal do AEM, na qual você pode criar e editar conteúdo para seu site.—>

**Para ativar o nível de publicação para um Site do Edge Delivery:**

1. Na página **Visão geral do programa**, na guia **Publicar entrega**, no cartão **Ambiente**, clique no ícone Informações.

1. Na janela pop-up informativa, em **Publicar URL**, selecione **Clicar para ativar** para habilitar o provisionamento do nível de publicação na interface do usuário do Cloud Manager.

   ![Clique para ativar o provisionamento do nível de publicação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

1. Na caixa de diálogo Ativar camada de publicação, clique em **Ativar**.

   ![Ativar caixa de diálogo Publicar camada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

   Depois de ativado, o nível de publicação é provisionado automaticamente. Como alternativa, o nível de publicação pode ser provisionado automaticamente se o autor tentar publicar conteúdo diretamente da interface do usuário do AEM.

   Depois que o nível de publicação é ativado e provisionado com êxito, o link **Clicar para Ativar** fica esmaecido/indisponível.

* **De Autor do AEM** — Na interface de criação do AEM, clique em **Publicação rápida** para publicar conteúdo diretamente no seu site do Edge Delivery. O nível de publicação não é necessário para esta operação quando o Edge Delivery lida com a entrega.

Depois de publicar, visualize seu conteúdo na URL `.page` do site ou faça uma visualização ao vivo na URL `.live`.—>

>[!NOTE]
>
>Ativar o nível de publicação adiciona a infraestrutura de publicação ao seu ambiente. Essa funcionalidade pode afetar o consumo de recursos do programa. Para configurar se o nível de publicação é necessário no nível do programa, consulte [Nível de Publicação Flexível (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).


## Excluir um site do Edge Delivery {#delete-edge-delivery-site}

Se você excluir um site do Edge Delivery Services, todas as configurações de CDN associadas também serão removidas. Essa ação interrompe a conexão entre domínios personalizados e o site. Para obter mais detalhes, consulte Configurações de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para excluir um site do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja remover.
Clique em ![Excluir ícone do site do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Excluir** e em **Excluir** novamente para confirmar a remoção do site.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo. No cabeçalho **Serviços**, clique em ![Página da Web do ícone Sites do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sites do Edge Delivery**.
Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja remover. Clique em ![Excluir ícone do site do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Excluir** e em **Excluir** novamente para confirmar a remoção do site.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Gerenciar um site do Edge Delivery entre a Helix 4 e a Helix 5

Use o ponto de extremidade de API `/program/{programId}/site/{siteId}` para migrar um site do Edge Delivery entre a Helix 4 e a Helix 5.

>[!IMPORTANT]
>
>As configurações de CDN para sites Helix 4 não podem ser migradas automaticamente para o Helix 5. Essa limitação existe porque as instalações de produção dos clientes ainda podem funcionar no Helix 4, enquanto suas versões do Helix 5 ainda estão em desenvolvimento.

**Pré-requisitos**

* O `sitename` já deve existir.
* Conhecer os valores apropriados de `branchName`, Hélice `version` e `repo`.
* A migração modifica apenas `branchName`, Helix `version` e `repo`. O campo de proprietário não pode ser alterado.

**Formato da API**

```http
PUT /api/program/{programId}/site/{siteId}
```

**Solicitar parâmetros de corpo**
Cria uma substituição para um site do Edge Delivery para impor a origem especificada no corpo da solicitação.

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### Exemplo 1: Migrar para o Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**Resultado da URL de origem**
Retorna um site do Edge Delivery com o seguinte URL de origem:

`"origin": "branch--my-website–Teo48.aem.live"`


### Exemplo 2: Migrar para o Helix 4

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**Resultado da URL de origem**
Retorna um site do Edge Delivery com o seguinte URL de origem:

`"origin": "branch--my-website--Teo48.hlx.live"`

### Exemplo 3: Migrar site de resposta para Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**Resultado da URL de origem**
Retorna um site do Edge Delivery com o seguinte URL de origem:

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## Registrar um tíquete de suporte {#eds-support-ticket}

{{support-ticket}}
