---
title: Configurar o conteúdo do Source
description: Saiba como configurar a fonte de conteúdo para seu site do Edge Delivery. Use "fstab.yaml" com a arquitetura Helix 4 ou use o assistente guiado no Cloud Manager (ou a API do serviço de configuração) com a arquitetura Helix 5.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---

# Configure sua fonte de conteúdo em um clique para o Edge Delivery Services {#config-content-source}

>[!IMPORTANT]
>
>*Helix* é o nome interno da arquitetura subjacente que capacita o AEM Sites com a criação baseada em documentos. Não é um nome de recurso ou de produto. Neste artigo, *Helix* refere-se à versão de arquitetura usada pelo seu Edge Delivery Sites. Helix 5 é a versão atual da arquitetura subjacente; Helix 4 é a versão anterior.

O Adobe Experience Manager (AEM) Edge Delivery Services permite a entrega de conteúdo de várias fontes, como o Google Drive, o SharePoint ou o próprio AEM, usando uma rede de borda rápida e distribuída globalmente.

A configuração da fonte de conteúdo difere entre as duas versões de arquitetura da seguinte maneira:

| Versão | Método de configuração da fonte de conteúdo |
| --- | --- |
| Helix | Arquivo YAML (`fstab.yaml`) |
| Helix 5 | API do Serviço de Configuração (*no`fstab.yaml`*) |

Este artigo fornece etapas de configuração abrangentes, exemplos e instruções de validação para ambas as versões.

**Antes de começar**

Se você usa o [Edge Delivery com um clique no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), seu site está usando a Helix 5 com um único repositório. [Siga as instruções da Helix 5](#config-helix5) e use a versão da Helix 4 YAML fornecida das instruções como um fallback.

**Determinar sua versão da Helix**

* Helix 4 - Seu projeto inclui um arquivo `fstab.yaml`.
* Hélice 5 - Seu projeto *não* usa `fstab.yaml` e foi configurado por meio do [Cloud Manager usando o assistente guiado](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) ou a API.

Confirme por meio dos metadados do repositório ou consulte o administrador se ainda não tiver certeza.

## Configurar a fonte de conteúdo do Helix 4

Na Helix 4, o arquivo `fstab.yaml` define a fonte de conteúdo do seu site. Localizado na raiz do seu repositório GitHub, esse arquivo mapeia prefixos de caminho de URL (chamados de pontos de montagem) para fontes de conteúdo externas. Um exemplo típico seria semelhante ao seguinte:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

O exemplo acima serve apenas para fins ilustrativos. O URL real deve apontar para sua fonte de conteúdo, como uma pasta do Google Drive, um diretório do SharePoint ou um caminho do AEM.

**Para configurar a fonte de conteúdo para a Helix 4:**

As etapas variam de acordo com o sistema de origem que você usa.

* **Google Drive**

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

A hélice 5 é sem resposta, não usa `fstab.yaml` e oferece suporte a vários sites que compartilham o mesmo diretório. A configuração é gerenciada por meio da API de Serviço de Configuração ou da interface do usuário do Edge Delivery Sites. A configuração é no nível do site (não no nível do repositório).

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
