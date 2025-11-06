---
title: Gerenciar sites do Edge Delivery no Cloud Manager
description: Saiba como adicionar uma configuração de CDN a um site do Edge Delivery ou excluir um site do Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

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
