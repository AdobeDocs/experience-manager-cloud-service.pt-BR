---
title: Configurar o conteúdo do Source
description: Saiba como configurar a fonte de conteúdo para seu site do Edge Delivery usando fstab.yaml no Helix 4 ou a interface do usuário do Edge Delivery Services (ou a API de serviço de configuração) no Helix 5.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Configure sua fonte de conteúdo em um clique para o Edge Delivery Services {#config-content-source}

O Adobe Experience Manager (AEM) Edge Delivery Services permite a entrega de conteúdo de várias fontes, como o Google Drive, o SharePoint ou o próprio AEM, usando uma rede de borda rápida e distribuída globalmente.

A configuração da fonte de conteúdo difere entre a Helix 4 e a Helix 5 da seguinte maneira:

| Versão | Método de configuração da fonte de conteúdo |
| --- | --- |
| Helix | Arquivo YAML (`fstab.yaml`) |
| Helix 5 | API do Serviço de Configuração (*no`fstab.yaml`*) |

Este artigo fornece etapas de configuração abrangentes, exemplos e instruções de validação para ambas as versões.

**Antes de começar**

Se você usar o [Edge Delivery com um clique no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), seu site será a Helix 5 com um único repositório. [Siga as instruções da Helix 5](#config-helix5) e use a versão da Helix 4 YAML fornecida das instruções como um fallback.

**Determinar sua versão da Helix**

* Helix 4 - Seu projeto inclui um arquivo `fstab.yaml`.
* Hélice 5 - Seu projeto *não* usa `fstab.yaml` e foi configurado por meio da [interface do usuário do Edge Delivery Services](#config-helix5) ou da API.

Confirme por meio dos metadados do repositório ou consulte o administrador se ainda não tiver certeza.

## Configurar a fonte de conteúdo do Helix 4

Na Helix 4, o arquivo fstab.yaml define a fonte de conteúdo do seu site. Localizado na raiz do seu repositório GitHub, esse arquivo mapeia prefixos de caminho de URL (chamados de pontos de montagem) para fontes de conteúdo externas. Um exemplo típico seria semelhante ao seguinte:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Este exemplo é apenas ilustrativo. O URL real deve apontar para sua fonte de conteúdo, como uma pasta do Google Drive, um diretório do SharePoint ou um caminho do AEM.

**Para configurar a fonte de conteúdo para a Helix 4:**

As etapas variam de acordo com o sistema de origem que você usa.

* **Unidade Google**

   1. Crie uma pasta Google Drive.
   1. Compartilhar a pasta com `helix@adobe.com`.
   1. Obter o link de pasta compartilhável.
   1. Atualize seu `fstab.yaml` conforme mostrado a seguir:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Confirme e envie alterações para o GitHub.

* **SharePoint**

   1. Crie uma pasta ou biblioteca de documentos do SharePoint.
   1. Compartilhar acesso com `helix@adobe.com`.
   1. Obtenha o URL da pasta.
   1. Atualize seu `fstab.yaml` conforme mostrado a seguir:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Confirme e envie alterações para o GitHub.

* **AEM**

   1. Identifique o caminho do conteúdo do AEM.
   1. Use o URL de exportação de conteúdo do AEM como mostrado no seguinte:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Confirme e envie alterações para o GitHub.

### Validação

* Usando a Extensão do AEM Sidekick Chrome, clique em **Visualizar** > **Publicar** > **Testar o site ativo**.
* Validar URL: `https://main--<repo>--<org>.hlx.page/`

## Configurar a fonte de conteúdo do Helix 5 {#config-helix5}

A hélice 5 é sem resposta, não usa `fstab.yaml` e oferece suporte a vários sites que compartilham o mesmo diretório. A configuração é gerenciada por meio da API de serviço de configuração ou da interface do usuário do Edge Delivery Services. A configuração é no nível do site (não no nível do repositório).

As diferenças conceituais são as seguintes:

| Aspecto | Helix | Helix 5 |
| --- | --- | --- |
| Configuração | Concluído até `fstab.yaml` | Feito por meio da API ou da interface do usuário, em vez de YAML. |
| Pontos de montagem | Definido em `fstab.yaml`. | Não obrigatório. A raiz é entendida implicitamente. |

**Para configurar a fonte de conteúdo para a Helix 5:**

1. Usando a API do Serviço de configuração, autentique por meio de uma chave de API ou token de acesso.
1. Fazer a seguinte chamada de API `PUT`:

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. Validar resposta (esperado: HTTP 200 OK).

### Validação

* Usando a Extensão do AEM Sidekick Chrome, clique em **Visualizar** > **Publicar** > **Testar o site ativo**.
* Validar URL: `https://main--<repo>--<org>.aem.page/`
* (Opcional) Inspecione a configuração atual por meio da seguinte chamada de API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
