---
title: Notas de versão do Cloud Manager 2026.4.0
description: Saiba mais sobre o lançamento do Cloud Manager 2026.4.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 5%

---

# Notas de versão do Cloud Manager 2026.4.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2026.4.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2026.4.0 no AEM as a Cloud Service é quinta-feira, 2 de abril de 2026.

A próxima versão está planejada para sexta-feira, 7 de maio de 2026.


## Novidades - Cloud Manager {#cloud-manager-whats-new}

* **Servidor MCP do Cloud Manager para IDEs alimentados por IA**

  Agora você pode usar um servidor MCP (Model Context Protocol) que expõe as APIs públicas do Cloud Manager como ferramentas para IDEs habilitadas para IA (como o Cursor). Depois de conectá-lo, você pode usar prompts conversacionais para listar e gerenciar programas, pipelines, ambientes e repositórios, ajudando você a se mover mais rápido sem sair do editor.

  Consulte a documentação [Usar MCP com AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

  Consulte o tutorial [Cloud Manager MCP Server](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager#).

* **Compilações mais rápidas com cache de módulo**

  Um novo modelo de build compila apenas os módulos alterados (em vez do repositório inteiro) usando o armazenamento em cache no nível do módulo para reduzir os tempos de compilação. Aplica-se a pipelines de não produção de Qualidade do código e pipelines de não produção de Empilhamento completo.

  Consulte [Sobre o uso do Smart Build em um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build) e [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

* **Verificação de conectividade de host de autoatendimento**

  O Cloud Manager agora permite executar verificações de autoatendimento do seu ambiente. Essas verificações verificam a acessibilidade do host e da porta e confirmam a resolução DNS usando o caminho de rede configurado do programa, incluindo a saída. Esse recurso ajuda a validar redes avançadas e resolver problemas de integração mais rapidamente sem abrir casos de suporte ou acessar pods. <!-- SKYOPS-23640 -->

  Consulte [Teste de Conectividade de Rede](/help/security/network-connectivity-test.md)

* **Estabilidade, desempenho e confiabilidade aprimoradas**

  Esta versão do inclui atualizações de otimização e manutenção que melhoraram a estabilidade, o desempenho e a confiabilidade do Cloud Manager.


## Programas do Beta {#private-beta-program}

Participe dos programas beta da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

>[!IMPORTANT]
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

Consulte também [Programas do AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

As seguintes oportunidades estão disponíveis no momento:

### Edge Delivery Services com criação no AEM e configuração flexível do nível de publicação {#eds-with-aem-authoring}

O Cloud Manager apresenta dois recursos projetados para oferecer suporte a arquiteturas de entrega modernas.

* **Edge Delivery Services com criação no AEM**
Agora você pode entregar sites usando o Edge Delivery Services e, ao mesmo tempo, continuar a criar conteúdo no modo Autor do AEM. Dependendo das suas preferências de fluxo de trabalho, você pode escolher entre as seguintes abordagens de criação:

   * Criação baseada em documento
   * Criação baseada em autor no AEM

Para obter mais informações, consulte [Criar site do Edge Delivery no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site).

* **Configuração flexível do nível de publicação**

O Cloud Manager agora permite configurar se um nível de publicação é necessário para o programa. Essa flexibilidade permite que você configure ambientes que correspondam melhor à arquitetura de entrega escolhida.

Para obter mais informações, consulte [Nível de publicação flexível (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

Para ingressar na Beta, envie um email para [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) com sua ID da organização da Adobe e a ID do programa.

### Criações mais rápidas com cache de módulo {#quick-build-cm-pipelines}

Um novo modelo de build compila apenas os módulos alterados (em vez do repositório inteiro) usando o armazenamento em cache no nível do módulo para reduzir os tempos de compilação. Aplica-se a pipelines de produção. Você controla quais pipelines de produção usam o **Smart Build**.

Para obter mais informações, consulte o seguinte:

* [Usando o Smart Build em um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build).
* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

Para ingressar na Beta, envie um email para [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) com sua OrgID da Adobe e sua ID do Programa.

<!-- 
OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- 
OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## Correções de erros {#bug-fixes}

Não há correções de erros significativas na versão de abril de 2026 do Cloud Manager.

<!-- ## Known issues {#known-issues} -->

