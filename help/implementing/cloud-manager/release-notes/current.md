---
title: Notas de versão do Cloud Manager 2025.5.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.5.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f9f4226bff8a0772878c144773eb8ff841a0a8d0
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 12%

---

# Notas de versão do Cloud Manager 2025.5.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.5.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.5.0 no AEM as a Cloud Service é quinta-feira, 8 de maio de 2025.

A próxima versão está planejada para sexta-feira, 5 de junho de 2025.

## Novidades {#what-is-new}

### Configure a fonte de conteúdo com um clique para o Edge Delivery Services

O Adobe Experience Manager (AEM) Edge Delivery Services permite a entrega de conteúdo de várias fontes, como o Google Drive, o SharePoint ou o próprio AEM, usando uma rede de borda rápida e distribuída globalmente.

A configuração da fonte de conteúdo difere entre a Helix 4 e a Helix 5 da seguinte maneira:

| Versão | Método de configuração da fonte de conteúdo |
| --- | --- |
| Helix | Arquivo YAML (`fstab.yaml`) |
| Helix 5 | API do Serviço de Configuração (*no`fstab.yaml`*) |

Este artigo fornece etapas de configuração abrangentes, exemplos e instruções de validação para ambas as versões.

**Antes de começar**

Se você usar o [Edge Delivery com um clique no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), seu site será a Helix 5 com um único repositório. Siga as instruções da Helix 5 e use a versão de instruções da Helix 4 YAML fornecida como um fallback.

**Determinar sua versão da Helix**

* Helix 4 - Seu projeto inclui um arquivo `fstab.yaml`.
* Hélice 5 - Seu projeto *não* usa `fstab.yaml` e foi configurado por meio da interface ou da API do Edge Delivery Services.

Confirme por meio dos metadados do repositório ou consulte o administrador se ainda não tiver certeza.

#### Configurar a fonte de conteúdo do Helix 4

Na Helix 4, o arquivo fstab.yaml define a fonte de conteúdo do seu site. Localizado na raiz do seu repositório GitHub, esse arquivo mapeia prefixos de caminho de URL (chamados de pontos de montagem) para fontes de conteúdo externas. Um exemplo típico seria semelhante ao seguinte:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Este exemplo é apenas ilustrativo. O URL real deve apontar para sua fonte de conteúdo, como uma pasta específica do Google Drive, diretório do SharePoint ou caminho do AEM.

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

##### Validação

* Usando a Extensão do AEM Sidekick Chrome, clique em **Visualizar** > **Publicar** > **Testar o site ativo**.
* Validar URL: `https://main--<repo>--<org>.hlx.page/`

#### Configurar a fonte de conteúdo do Helix 5

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

##### Validação

* Usando a Extensão do AEM Sidekick Chrome, clique em **Visualizar** > **Publicar** > **Testar o site ativo**.
* Validar URL: `https://main--<repo>--<org>.aem.page/`
* (Opcional) Inspecione a configuração atual por meio da seguinte chamada de API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## Programa de adoção antecipada {#early-adoption}

Participe do Programa de primeiros usuários da Cloud Manager para obter acesso exclusivo a recursos futuros antes do lançamento geral.

As seguintes oportunidades de adoção antecipada estão disponíveis no momento:

### Adicionar pipeline do Edge Delivery {#add-eds-pipeline}

**Pipelines** agora têm suporte para sites criados com o Edge Delivery Services, expandindo esse recurso além dos ambientes do Cloud Service. Você pode usar **Pipelines** para gerenciar configurações, como regras de filtragem de tráfego e configurações do Firewall do Aplicativo Web (WAF), quando aplicável. Consulte [Configurações com Suporte](/help/operations/config-pipeline.md#configurations).

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) com seu endereço de email associado à sua Adobe ID.

### Traga seu próprio Git - agora com suporte para Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Os clientes agora podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios DevOps do Azure modernos e repositórios VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

Em breve, haverá suporte para tipos adicionais de pipeline e validação de solicitação de pull por meio de pipelines de qualidade de código.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) do seu endereço de email associado à sua Adobe ID. Inclua qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou empresarial.

<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

