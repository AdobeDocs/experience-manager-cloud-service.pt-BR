---
title: Notas de versão do Cloud Manager 2026.3.0
description: Saiba mais sobre o lançamento do Cloud Manager 2026.3.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2556f606db8b74bce25cd504a183abdc43e31227
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 4%

---

# Notas de versão do Cloud Manager 2026.3.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2026.3.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2026.3.0 no AEM as a Cloud Service é quinta-feira, 5 de março de 2026.

A próxima versão está planejada para sexta-feira, 2 de abril de 2026.


## Novidades - Cloud Manager {#cloud-manager-whats-new}

* **O Cloud Manager agora oferece suporte à opção** Apagar **para** Importações de cópia de conteúdo **&#x200B;**

  Ao habilitar o **Apagar**, o Cloud Manager exclui o conteúdo existente no destino antes de iniciar a importação, para que você possa começar do zero e evitar conflitos com o conteúdo pré-existente. Se você deixar **Apagar** desativado, o Cloud Manager importará o novo conteúdo para cima do conteúdo de destino existente. Um prompt de confirmação é exibido antes do início do apagamento e o Cloud Manager registra a ação de apagamento e os detalhes de importação para rastreabilidade.

  Consulte também [Copiar conteúdo](/help/implementing/developing/tools/content-copy.md#copy-content).

* **Suporte para extensibilidade da interface do usuário no AEM Experience Hub**
O suporte para Extensões de Interface do Usuário no [AEM Experience Hub](https://experience.adobe.com/experiencemanager) agora está habilitado, permitindo que os desenvolvedores estendam a interface com funcionalidades e widgets personalizados criados com o Adobe App Builder.

  Para saber mais, consulte [AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/).

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

### Servidor Cloud Manager MCP para IDEs alimentados por IA{#mcp-server-for-cm}

Agora você pode experimentar um servidor MCP (Model Context Protocol) que expõe as APIs públicas do Cloud Manager como ferramentas para IDEs habilitadas para IA (como o Cursor). Depois de conectá-lo, você pode usar prompts conversacionais para listar e gerenciar programas, pipelines, ambientes e repositórios, ajudando você a se mover mais rápido sem sair do editor.

Consulte a documentação [Usar MCP com AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

Consulte o tutorial [Cloud Manager MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#).

Interessado no beta? Envie um email para [GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com) com sua ID organizacional e ID do programa da Adobe.


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### Criações mais rápidas com cache de módulo {#quick-build-cm-pipelines}

Um novo modelo de build compila apenas os módulos alterados (em vez do repositório inteiro) usando o armazenamento em cache no nível do módulo para reduzir os tempos de compilação. Ela se aplica a pipelines de qualidade de código, pilha completa e somente estágio.

![Caixa de diálogo Editar Pipeline de Não Produção mostrando as duas opções de Estratégia de Compilação que são Compilação Completa e Compilação Inteligente](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Caixa de diálogo Editar Pipeline de Não Produção mostrando as duas opções de Estratégia de Compilação que são Compilação Completa e Compilação Inteligente.*

Na caixa de diálogo **Adicionar/Editar Pipeline**, na guia **Código Source**, uma nova seção **Estratégia de Compilação** permite escolher uma das seguintes opções de compilação:

* **Compilação Completa** — compila todos os módulos no repositório em cada execução.
* **Compilação Inteligente** — cria apenas módulos que foram alterados desde a última confirmação, o que reduz o tempo geral de compilação.

Você controla quais pipelines usam a **Compilação inteligente**. Durante a versão beta, essa opção aparece somente para os pipelines **Qualidade do código** e **Implantação de pilha completa de desenvolvimento**.

Consulte [Sobre o uso da Compilação Inteligente em um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build) e [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

Interessado? Envie um email para [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) com sua ID organizacional e ID do programa da Adobe.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## Correções de erros {#bug-fixes}

* Solução de um problema em que a API de pontos de restauração podia retornar um erro 500 ao recuperar pontos de restauração. O endpoint agora lida com valores nulos corretamente, garantindo respostas consistentes e confiáveis. (CMGR-72963)
* O Cloud Manager agora aceita URLs de repositório do GitHub com ou sem o sufixo `.git`, alinhando o comportamento da API com a interface do usuário e tornando a integração do repositório mais flexível. (CMGR-73296)
* A validação do nome do perfil do produto agora não diferencia maiúsculas de minúsculas, evitando erros ao criar perfis com nomes que diferem apenas com letras maiúsculas. (CMGR-74075)
* Agora é possível executar várias operações de restauração a partir da mesma execução de pipeline, permitindo restaurações sequenciais para ambientes como Preparo e Produção sem exigir uma nova execução de pipeline. (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

