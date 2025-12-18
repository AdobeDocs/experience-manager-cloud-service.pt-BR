---
title: Notas de versão do Cloud Manager 2025.12.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.12.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 7c1f1f1022fd63c190a493d312ab1f355859d15a
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 4%

---

# Notas de versão do Cloud Manager 2025.12.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.12.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.12.0 no AEM as a Cloud Service é quinta-feira, 4 de dezembro de 2025.

A próxima versão está planejada para sexta-feira, 22 de janeiro de 2026.

## Novidades - Experience Hub {#experience-hub-whats-new}

* **Acesso simplificado ao Experience Hub**

  A seleção da função do usuário foi removida e um guia foi adicionado para a seleção **Predefinição** (Autor de conteúdo, Bibliotecário de ativos, Administrador e TI).

* **Avisos** e **Atualizações de produto**

  Você pode alternar e iterar entre os anúncios disponíveis, mas também ignorá-los.

* **Recentes**

  Adição de suporte para páginas e recursos adicionais, incluindo o editor de páginas, ativos, programas, detalhes de execução de pipeline e páginas de segurança.

* **Lista de programas**

  Mostrar os programas do AEM Cloud Manager em sua organização com acesso rápido à página de detalhes do Cloud Manager.

* **Guias do AEM**

  Ação rápida e Atalho para os Ambientes de criação que têm os complementos do AEM Guides ativados.

## Novidades - Cloud Manager {#cloud-manager-whats-new}

* **Estabilidade, desempenho e confiabilidade aprimoradas**

  Esta versão do inclui atualizações de otimização e manutenção que melhoraram a estabilidade, o desempenho e a confiabilidade do Cloud Manager.

* **Ambiente de teste especializado**

  >[!NOTE]
  >
  >Os ambientes de teste especializados agora estão disponíveis para compra. Entre em contato com seu representante da Adobe para fazer um pedido.

  O Cloud Manager agora oferece suporte à adição de um novo tipo de ambiente chamado **Ambiente de teste especializado**. O ambiente foi projetado para ajudar as equipes a validar recursos em condições próximas da produção antes de entrar em funcionamento. Este tipo de ambiente é diferente dos ambientes *Produção + Preparo*, *Desenvolvimento* ou *Desenvolvimento rápido* e oferece um espaço focalizado para execução de cenários de validação avançados.

  Consulte [Adicionar um ambiente de teste especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

  ![Caixa de diálogo Adicionar ambiente com o botão de opção Ambiente de teste especializado selecionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

<!--
>[!NOTE]
>
>Adobe has closed beta access requests for Specialized Testing Environments, having reached a sufficient number of participants. The feature is now in preparation for general availability.

If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


* **Reversão de um clique para implantações de pipeline**

  Reverta rapidamente para uma implantação anterior se o código-fonte do cliente mais recente não estiver funcionando como esperado. Não há necessidade de executar novamente o pipeline completo ou reverter as confirmações manualmente. <!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

  Consulte [Restaurar o código anterior implantado no AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

  Consulte também [Restauração de Conteúdo no AEM as a Cloud Service](/help/operations/restore.md).

* **Configuração de autoatendimento do WAF para Edge Delivery Services**

  Ao criar um programa do Edge Delivery Services no Cloud Manager, você pode ativar o Firewall do aplicativo web (WAF). Essa configuração protege seu site contra tráfego mal-intencionado e ataques de DDoS imediatamente, reduzindo o trabalho de configuração manual.

  Consulte [Criar seu Primeiro Site do Edge Delivery com Um Clique](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md).


## Programas do Beta {#private-beta-program}

Participe dos programas beta da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

>[!IMPORTANT]
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

Consulte também [Programas do AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

As seguintes oportunidades estão disponíveis no momento:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Extensibilidade e personalização do Experience Hub {#exp-hub-extensibility}

O [Experience Hub](/help/experience-hub.md) serve como ponto de entrada para o AEM, personalizado para as necessidades da sua organização. Conte à Adobe sobre suas extensões existentes da interface do usuário do AEM para que elas possam ajudá-lo a ativá-las no Experience Hub com o mínimo de esforço.

![Diagrama do fluxo de trabalho de extensibilidade e personalização do Experience Hub](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Incorpore experiências personalizadas no Experience Hub para estender e personalizar o painel de sua organização. Além dos widgets integrados do Adobe, adicione os seus próprios usando a estrutura [Extensibilidade da interface](https://developer.adobe.com/uix/docs/). Crie aplicativos de interface do usuário com base no JavaScript e os mostre aos seus usuários para atender aos requisitos e fluxos de trabalho específicos da empresa.

Interessado no beta? Envie um email para [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) com sua Organização da Adobe e uma breve descrição da personalização que pretende criar.

### Criações mais rápidas com cache de módulo {#quick-build-cm-pipelines}

Um novo modelo de build compila apenas os módulos alterados (em vez do repositório inteiro) usando o armazenamento em cache no nível do módulo para reduzir os tempos de compilação. Ela se aplica a pipelines de qualidade de código, pilha completa e somente estágio.

![Caixa de diálogo Editar Pipeline de Não Produção mostrando as duas opções de Estratégia de Compilação que são Compilação Completa e Compilação Inteligente](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Caixa de diálogo Editar Pipeline de Não Produção mostrando as duas opções de Estratégia de Compilação que são Compilação Completa e Compilação Inteligente.*

Na caixa de diálogo **Adicionar/Editar Pipeline**, na guia **Código Source**, uma nova seção **Estratégia de Compilação** permite escolher uma das seguintes opções de compilação:

* **Compilação Completa** — compila todos os módulos no repositório em cada execução.
* **Compilação Inteligente** — cria apenas módulos que foram alterados desde a última confirmação, o que reduz o tempo geral de compilação.

Você controla quais pipelines usam a **Compilação inteligente**. Durante a versão beta, essa opção aparece somente para os pipelines **Qualidade do Código** e **Implantação de Desenvolvimento**.

Interessado? Envie um email para [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) com sua ID organizacional e ID do programa da Adobe.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

### Traga seu próprio Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Os clientes agora podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios DevOps do Azure modernos e repositórios VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

Em breve, haverá suporte para tipos adicionais de pipeline e validação de solicitação de pull por meio de pipelines de qualidade de código.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Perguntas frequentes sobre o BYOG**

| Interrogação | Resposta |
|---|---|
| *Como um projeto pode voltar para o repositório Git gerenciado pela Adobe, se necessário?* | É simples voltar atrás. [Atualize os pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para apontar para o repositório do Adobe e remover o repositório externo se ele não for mais necessário. |
| *É possível configurar repositórios diferentes para ambientes diferentes (por exemplo, não produção versus produção) para permitir testes em não produção primeiro?* | Sim, repositórios diferentes podem ser configurados para ambientes separados. Por exemplo, o pipeline de desenvolvimento ou qualidade do código pode apontar para um repositório externo enquanto o pipeline de produção permanece conectado ao repositório do Adobe. Verifique se o trabalho de sincronização entre os dois repositórios permanece ativo durante essa configuração. |
| *As configurações existentes como as listas `IP Allow` continuam a funcionar?* | Sim, as listas `IP Allow` existentes continuam a funcionar normalmente. No entanto, se o repositório Git externo estiver protegido por um firewall, os [endereços IP Adobe necessários deverão ser adicionados à lista de permissões](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Todos os URLs de repositório do GitLab funcionam? A URL de repositório em uso segue o formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difere do exemplo na documentação.* | Sim, qualquer repositório do GitLab com suporte para API V3 ou V4 tem suporte, incluindo URLs do GitLab auto-hospedados como o descrito em [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gerenciar tokens de acesso{#manage-access-tokens}

Use **Gerenciar Tokens de Acesso** no Cloud Manager para exibir, renomear e excluir tokens de acesso associados a repositórios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulte [Gerenciar Tokens de Acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## Correções de erros {#bug-fixes}

Não há correções de erros significativas na versão de dezembro de 2025 do Cloud Manager.


<!-- ## Known issues {#known-issues} -->

