---
title: Notas de versão do Cloud Manager 2026.1.0
description: Saiba mais sobre o lançamento do Cloud Manager 2026.1.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 5%

---

# Notas de versão do Cloud Manager 2026.1.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2026.1.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2026.1.0 no AEM as a Cloud Service é quinta-feira, 22 de janeiro de 2026.

A próxima versão está planejada para sexta-feira, 5 de fevereiro de 2026.

## Novidades - Cloud Manager {#cloud-manager-whats-new}

* **Os pipelines de configuração agora oferecem suporte a segredos gerenciados**

  Agora os usuários podem adicionar e gerenciar segredos diretamente nos pipelines de configuração do Cloud Manager. Esses segredos substituem com segurança os valores na especificação de configuração do pipeline e oferecem suporte a implantações flexíveis e específicas do ambiente.

  ![Opção Exibir/Editar variáveis no menu suspenso de um pipeline selecionado](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  *Opção Exibir/Editar variáveis no menu suspenso de um pipeline selecionado.*

  ![Caixa de diálogo Configuração de Variáveis &#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*Caixa de diálogo Configuração de Variáveis.*

* **Estabilidade, desempenho e confiabilidade aprimoradas**

  Esta versão do inclui atualizações de otimização e manutenção que melhoraram a estabilidade, o desempenho e a confiabilidade do Cloud Manager.




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

## Correções de erros {#bug-fixes}

Não há correções de erros significativas na versão de dezembro de 2025 do Cloud Manager.


<!-- ## Known issues {#known-issues} -->

