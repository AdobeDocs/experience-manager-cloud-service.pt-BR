---
title: Notas de versão do Cloud Manager 2025.10.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.10.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8dfe5316db99860ee8fbf5d0be2fa70412e7cce3
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 3%

---

# Notas de versão do Cloud Manager 2025.10.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.10.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.10.0 no AEM as a Cloud Service é quinta-feira, 2 de outubro de 2025.

A próxima versão está planejada para sexta-feira, 6 de novembro de 2025.

## Novidades {#what-is-new}

* **Pipelines dedicados somente a estágio e somente produção para implantação**

  O Cloud Manager agora oferece pipelines dedicados de implantação somente de preparo e produção, fornecendo maior flexibilidade para gerenciar implantações em ambientes de preparo e produção de maneira independente. Consulte [Pipelines somente de estágio dividido e somente produção](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md).

* **Serviço de Avaliação de Integridade da AEM Cloud**

  A Adobe apresenta o Serviço de avaliação de integridade da AEM Cloud, uma ferramenta de verificação automatizada e não invasiva que mantém seu ambiente AEM as a Cloud Service otimizado, seguro e alinhado às práticas recomendadas.

  Esse serviço faz o seguinte:

   * Examina ambientes para detectar gargalos de desempenho, ineficiências e riscos em potencial.
   * Analisa estruturas de conteúdo (blueprints, live copies) e configurações personalizadas.
   * Identifica dependências desatualizadas (AEM SDK, bibliotecas de terceiros).
   * Sinaliza problemas de qualidade de código (anotações inadequadas, padrões ineficientes).
   * Fornece orientação acionável por meio de painéis, como o **Centro de Ações**.
   * Oferece suporte à otimização proativa por meio da detecção e correção antecipadas de problemas.

  As equipes podem monitorar e melhorar continuamente seus ambientes AEM para obter desempenho ininterrupto, segurança mais forte e capacidade de manutenção de longo prazo.

  Consulte [Avaliação de Integridade para Ambientes de Produção e Preparo](/help/implementing/cloud-manager/reports/report-health-assessment.md).

* **Suporte ao Pipeline de Configuração**

  Os Pipelines de configuração agora são compatíveis com sites criados com o Edge Delivery Services, expandindo esse recurso além dos ambientes do Cloud Service. Você pode usar **Pipelines de configuração** para gerenciar configurações como a configuração de CDN, incluindo regras de filtro de tráfego e seletores de origem. Consulte [Configurações com Suporte](/help/operations/config-pipeline.md#configurations).

  Os pipelines de configuração do Edge Delivery também são compatíveis com segredos por meio de variáveis de pipeline do Cloud Manager.

  Consulte [Adicionar pipeline de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

* **Caixa de diálogo de instalação do Domain Mapping-CDN simplificada**

  A Cloud Manager simplificou o fluxo **Mapear Domínio para CDN** para reduzir confusão e configuração de velocidade. A caixa de diálogo agora enfatiza a **CDN gerenciada pela Adobe** (com um selo &quot;Recomendado&quot;).

  ![Caixa de diálogo Mapear Domínio para CDN com o botão de opção CDN gerenciado pela Adobe selecionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png).

  Consulte [Adicionar um mapeamento de domínio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

  A caixa de diálogo também apresenta uma lista de verificação única e concisa para o cartão **Outro provedor de CDN**, com foco no conteúdo instrucional com o seguinte:

   * Aponte sua origem CDN para `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`.
   * Defina **Host/SNI** para encaminhar o host original.
   * Adicionar `X-AEM-Edge-Key` (após implantar a chave no Cloud Manager).
   * Defina `X-Forwarded-Host` como seu domínio voltado para o cliente.
   * Limpe outros cabeçalhos `X-Forwarded-*` antes de acessar o AEM.

  ![Caixa de diálogo Mapear Domínio para CDN com o botão de opção Outro provedor CDN selecionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->O rodapé que o acompanha fornece dois links úteis: configurações de exemplo para os principais CDNs e um link para a documentação completa. Um único botão de confirmação - Eu configurei meu CDN - conclui o fluxo.

  Consulte [CDN no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN).

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Programas do Beta {#private-beta-program}

Participe dos programas beta da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

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



### Reversão de um clique para implantações de pipeline {#one-click-rollback}

Reverta rapidamente para uma implantação anterior se o código-fonte do cliente mais recente não estiver funcionando como esperado — não é necessário executar novamente o pipeline completo ou reverter as confirmações manualmente.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Restaurar o código-fonte do cliente a partir do cartão Ambientes](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *cartão Ambientes acima, mostrando a opção **Restaurar**>**Código anterior implantado**&#x200B;para um ambiente selecionado.*

![Restaurar caixa de diálogo implantada de código anterior](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*Na caixa de diálogo **Restaurar código anterior implantado**, revise a versão implantada no momento e a versão que deseja restaurar e clique em **Confirmar***.

![Restaurando a ativação](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
O *Cloud Manager reverte o ambiente para a compilação anterior, mantém o conteúdo e a configuração intactos e marca o ambiente **Restaurando**&#x200B;até que a implantação seja concluída.*

![Versão do código Source em uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *A exibição de detalhes do Ambiente, como visto acima, agora também mostra a versão ativa do código-fonte em uso.*

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [restorecode@adobe.com](mailto:restorecode@adobe.com) com seu endereço de email associado à sua Adobe ID.

Consulte [Restaurar o código anterior implantado no AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulte também [Restauração de Conteúdo no AEM as a Cloud Service](/help/operations/restore.md).

### Ambiente de testes especializados {#specialized-test-environment}

O Cloud Manager agora oferece suporte à adição de um novo tipo de ambiente chamado **Ambiente de teste especializado**. O ambiente foi projetado para ajudar as equipes a validar recursos em condições próximas da produção antes de entrar em funcionamento. Este tipo de ambiente é diferente dos ambientes *Produção + Preparo*, *Desenvolvimento* ou *Desenvolvimento rápido* e oferece um espaço focalizado para execução de cenários de validação avançados.

**Aprimoramentos recentes**

* Agora você pode configurar um Ambiente de teste especializado em um pipeline de não produção por meio de um fluxo de trabalho mais simples e intuitivo. A configuração simplificada acelera a conclusão e reduz os erros de configuração.
* Agora há suporte para **Copiar Conteúdo** em Ambientes de Teste Especializados. Agora você pode executar o **Copiar Conteúdo** com segurança em ambientes de teste isolados que espelham a Produção. <!-- (CMGR‑68900) -->

Consulte [Adicionar um ambiente de teste especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Caixa de diálogo Adicionar ambiente com o botão de opção Ambiente de teste especializado selecionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>A Adobe fechou solicitações de acesso beta para Ambientes de teste especializados, tendo atingido um número suficiente de participantes. O recurso agora está em preparação para disponibilidade geral.

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


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

Não há correções de bugs significativas na versão de outubro do Cloud Manager.


<!-- ## Known issues {#known-issues} -->

