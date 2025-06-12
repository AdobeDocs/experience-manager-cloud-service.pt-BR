---
title: Notas de versão do Cloud Manager 2025.6.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.6.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 10%

---

# Notas de versão do Cloud Manager 2025.6.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.6.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.6.0 no AEM as a Cloud Service é quinta-feira, 5 de junho de 2025.

A próxima versão está planejada para sexta-feira, 10 de julho de 2025.

## Novidades {#what-is-new}

* **O painel de licenças agora inclui uma licença do Edge Delivery Services**

  O uso de licença da Edge Delivery Services agora é exibido no painel de Licenças, fornecendo uma visibilidade mais clara de seus direitos e status. <!-- CMGR-67686 -->

  ![Painel de licenças](/help/implementing/cloud-manager/assets/license-dashboard.png)

  Consulte [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

* **Configuração de site do Edge Delivery atualizada**

  Simplificou o fluxo para adicionar um site Edge Delivery solicitando a **Edge Delivery Origin** em vez da **URL do Repositório**, tornando a integração e a configuração mais rápidas e intuitivas <!-- CMGR-67686 -->

  ![Caixa de diálogo Adicionar site do Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  Consulte [Adicionar um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md).

* **Favoritos do pipeline**

  Nesta versão, o Cloud Manager apresenta a capacidade de fixar pipelines favoritos, permitindo que você marque pipelines específicos como favoritos para que eles apareçam no topo da lista na página **Pipelines**. Esse aprimoramento facilita a localização e a execução de pipelines acessados com frequência. <!-- CMGR-68293 -->

  ![Pipelines marcados como favoritos](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *Dois pipelines marcados como favoritos.*

  Consulte [Marcar favoritos do pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites).


## Programa beta privado {#private-beta-program}

Participe do Programa Beta privado da Cloud Manager para obter acesso exclusivo a recursos futuros antes de seu lançamento geral.

As seguintes oportunidades de beta privado estão disponíveis no momento:


### Ambiente de testes especializados {#specialized-test-environment}

O Cloud Manager agora oferece suporte à adição de um novo tipo de ambiente chamado **Ambiente de teste especializado**. O ambiente foi projetado para ajudar as equipes a validar recursos em condições próximas da produção antes de entrar em funcionamento. Este tipo de ambiente é diferente dos ambientes *Produção + Preparo*, *Desenvolvimento* ou *Desenvolvimento rápido* e oferece um espaço focalizado para execução de cenários de validação avançados.

Consulte [Adicionar um ambiente de teste especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Caixa de diálogo Adicionar ambiente com o botão de opção Ambiente de teste especializado selecionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) com seu endereço de email associado à sua Adobe ID.


### Traga seu próprio Git (BYOG) - agora com suporte para Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Os clientes agora podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios DevOps do Azure modernos e repositórios VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

Em breve, haverá suporte para tipos adicionais de pipeline e validação de solicitação de pull por meio de pipelines de qualidade de código.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) do seu endereço de email associado à sua Adobe ID. Inclua qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou empresarial.


**Perguntas frequentes sobre o BYOG**

| Pergunta | Resposta |
|---|---|
| *Como um projeto pode voltar para o repositório Git gerenciado pela Adobe, se necessário?* | É simples voltar atrás. [Atualize os pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para apontar para o repositório do Adobe e remover o repositório externo se ele não for mais necessário. |
| *É possível configurar repositórios diferentes para ambientes diferentes (por exemplo, não produção versus produção) para permitir testes em não produção primeiro?* | Sim, repositórios diferentes podem ser configurados para ambientes separados. Por exemplo, o pipeline de desenvolvimento ou qualidade do código pode apontar para um repositório externo enquanto o pipeline de produção permanece conectado ao repositório do Adobe. Verifique se o trabalho de sincronização entre os dois repositórios permanece ativo durante essa configuração. |
| *As configurações existentes, como listas de permissões IP, continuam a funcionar?* | Sim, as listas de permissões IP existentes continuam a funcionar normalmente. No entanto, se o repositório Git externo estiver protegido por um firewall, os [endereços IP Adobe necessários deverão ser adicionados à lista de permissões](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Todos os URLs de repositório do GitLab funcionam? A URL de repositório em uso segue o formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difere do exemplo na documentação.* | Sim, qualquer repositório do GitLab com suporte para API V3 ou V4 tem suporte, incluindo URLs do GitLab auto-hospedados como o descrito em [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gerenciar tokens de acesso{#manage-access-tokens}

Use **Gerenciar Tokens de Acesso** no Cloud Manager para exibir, renomear e excluir tokens de acesso associados a repositórios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulte [Gerenciar Tokens de Acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) com seu endereço de email associado à sua Adobe ID.


### Adicionar pipeline de configuração do Edge Delivery {#add-eds-pipeline}

Os Pipelines de configuração agora são compatíveis com sites criados com o Edge Delivery Services, expandindo esse recurso além dos ambientes do Cloud Service. Você pode usar **Pipelines de configuração** para gerenciar configurações como regras de filtragem de tráfego e configurações do Firewall do Aplicativo Web (WAF), quando aplicável. Consulte [Configurações com Suporte](/help/operations/config-pipeline.md#configurations).

![Adicionar pipeline do Edge Delivery na lista suspensa Adicionar pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adicionar um pipeline do Edge Delivery da página **Visão geral do programa**,**Pipelines**&#x200B;cartão.*

![Caixa de diálogo Adicionar pipeline do Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Caixa de diálogo Adicionar pipeline do Edge Delivery.*

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) com seu endereço de email associado à sua Adobe ID.


## Correções de erros

* Os ambientes de sandbox marcados anteriormente como `HIBERNATED` não permanecem mais presos nesse estado, permitindo que a execução ou implantação do pipeline continue como esperado. <!-- CMGR-67705 -->
* Agora, o AEM Cloud Manager mapeia corretamente as falhas de compilação do Maven causadas por erros 409 (conflitos) ao buscar artefatos do cliente para uma falha causada pelo cliente. Essa alteração melhora as mensagens de erro, distinguindo entre erros internos e problemas relacionados à configuração do ambiente do cliente. <!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

