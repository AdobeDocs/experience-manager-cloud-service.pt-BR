---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0ddc7c0b1dc7dd3350dd91576011dc26f57afa51
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 8%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2026.2.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é quarta-feira, 3 de março de 2026. O próximo lançamento de recursos (2026.3.0) está planejado para sexta-feira, 26 de março de 2026.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de fevereiro de 2026 para obter um resumo dos recursos adicionados na versão 2026.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3480404/?captions=por_br&quality=12)


## Programas do AEM Beta {#aem-beta-programs}

Os programas beta do Adobe Experience Manager (AEM) são uma maneira de os clientes obterem acesso a recursos e código de pré-lançamento, fornecerem feedback e guiarem o futuro do AEM.

>[!IMPORTANT]
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

**Vantagens de participar**
Obter acesso antecipado aos recursos que a Adobe está desenvolvendo permite que clientes e parceiros forneçam feedback e modelem o desenvolvimento de produtos. Também os ajuda a se preparar para adotar novos recursos antes da disponibilidade geral.

**Programas beta atuais**
As seções a seguir listam os programas beta ativos.

### Agentes no AEM {#agents-in-aem}

Se você quiser explorar os novos e poderosos recursos do AEM em produção, governança, otimização, descoberta e desenvolvimento, [saiba mais sobre como acessá-los aqui.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (programas do Beta) {#aem-foundation-beta-programs}

Consulte [programas beta do AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas do Beta) {#cloud-manager-beta-programs}

Consulte [programas beta do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Supervisor de Conteúdo para acessar o AEM Assets no Adobe Express**

[O Supervisor de Conteúdo agora está disponível no Adobe Express](/help/assets/native-integration-adobe-express.md), introduzindo a descoberta inteligente de ativos para o AEM Assets diretamente na interface do Express. O Supervisor de conteúdo fornece recomendações com reconhecimento de contexto com base no conteúdo da tela e nos resumos da campanha, oferece suporte à pesquisa alimentada por IA, habilita o suporte nativo para representações prontas para canal on-line viabilizadas pelo Dynamic Media e muitos outros recursos. O Supervisor de conteúdo transforma o modo como você detecta e usa ativos aprovados, ajudando a encontrar o conteúdo correto mais rapidamente para simplificar seus fluxos de trabalho criativos.

### Novos recursos no Dynamic Media com OpenAPI {#dynamic-media-openAPI-new-features}

**Controle de acesso baseado em atributo (ABAC) para Dynamic Media com OpenAPI**

O controle de acesso baseado em atributos (ABAC) permite que os administradores controlem o acesso ao Dynamic Media com ativos OpenAPI usando regras orientadas por metadados. Os administradores podem definir regras para grupos de usuários com base em metadados de ativos para determinar quais ativos estão visíveis para grupos específicos. Quando os metadados de um ativo correspondem às condições definidas, o acesso é concedido automaticamente. Esse recurso ajuda as organizações a aplicar uma melhor governança, garantindo que os usuários só possam visualizar e trabalhar com o Dynamic Media com ativos OpenAPI relevantes para sua função ou permissões.

>[!NOTE]
>
>O controle de acesso baseado em atributos (ABAC) para Dynamic Media com OpenAPI é um recurso de disponibilidade limitada. Você pode habilitá-lo criando um [tíquete de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de acesso antecipado no AEM Forms {#forms-early-access-features}

* **Exibir rótulos para a lista suspensa de várias seleções na PDF de Envio**: os componentes da lista suspensa de várias seleções na Forms Adaptável agora renderizam seus rótulos de exibição selecionados na [PDF de Envio gerada](/help/forms/generate-document-of-record-core-components.md), garantindo que o documento reflita com precisão o que os usuários veem no formulário.

* **Acessibilidade aprimorada para componentes de caixa de seleção, botão de opção e painel**: os Componentes principais do Adaptive Forms apresentam marcação semântica compatível com WCAG 2.2 para [grupos de caixas de seleção(v2)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [grupos de botões de opção(v2)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) e o [componente Painel](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Esses componentes usam os elementos do HTML `<fieldset>` e `<legend>` para estabelecer relações significativas entre os rótulos de grupo e suas opções, permitindo a interpretação precisa por leitores de tela e outras tecnologias de assistência.

* **Suporte ao controle de versão no Forms Manager**: o Forms Manager agora oferece suporte ao controle de versão para o Adaptive Forms (Componentes principais e Componentes de base), fragmentos de formulário, temas, modelos XDP e ativos binários. Crie versões, visualize o histórico completo de versões e restaure estados anteriores dos ativos de formulário diretamente do console Forms e Documentos.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Novos recursos {#foundation-new}

#### Pausar Atualizações de Manutenção Automática {#pause-updates}

Dias de ativação, eventos ao vivo, pico de vendas — esses momentos não quebram. [Nossos novos recursos de autoatendimento](/help/implementing/deploying/quiet-hours-update-free-periods.md) interrompem as atualizações de manutenção automáticas quando é importante, para que suas equipes permaneçam focadas.

* Quiet Hours: bloqueia a manutenção automática durante os horários definidos a cada dia. Ideal para horas de trabalho, corridas noturnas ou cortes matinais.
* Período Livre de Atualização: Bloqueia a manutenção automática por uma semana inteira. Use-o para inicializações, promoções ou congelamentos anuais.

#### Solução de problemas do pipeline de qualidade de código com o agente de desenvolvimento {#devagent-codequality}

Os recursos de solução de problemas de pipeline do Agente de desenvolvimento ajudam os desenvolvedores a diagnosticar e resolver problemas de forma mais eficiente nas implantações do AEM as a Cloud Service.

Anteriormente focada na etapa **Teste de compilação e unidade**, a solução de problemas do pipeline agora também oferece suporte à etapa **Verificação de código** nos pipelines de Implantação de pilha completa e Qualidade de código.

A etapa Verificação de código avalia o código em relação às regras de qualidade, detecta vulnerabilidades de segurança e gera relatórios de qualidade detalhados. Se essa etapa falhar, você poderá usar o Assistente de IA para solicitar ao Agente de desenvolvimento uma análise da causa raiz, juntamente com orientações de correção recomendadas.

Saiba mais sobre o [Agente de Desenvolvimento](/help/ai-in-aem/agents/brand-experience/development/development.md) e a solução de problemas do pipeline.

### Avisos importantes sobre a base [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-notices}

#### Desaprovações da API Java {#java-api-deprecation}

As APIs obsoletas que direcionam a remoção de 26/02/2026 não devem mais ser usadas no código. Para evitar bloqueios de implantação, remova o uso da API antes de 30 de março de 2026. Datas importantes:

* **A partir de 26 de janeiro de 2026**: os emails de notificação da Central de Ações são enviados como um lembrete para remover o uso dessas APIs.
* **26 de fevereiro de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **pausarão** durante a etapa **Qualidade do Código**. Um Gerente de implantação, Gerente de projeto ou Proprietário da empresa pode substituir o problema para permitir que o pipeline continue. *Isso pode retardar sua capacidade de validar e liberar alterações no código.*
* **30 de março de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **falharão** durante a etapa **Qualidade do código**. As implantações serão bloqueadas até que o uso da API obsoleta seja removido. *Isso pode impedir que você libere atualizações com prazo determinado e pode afetar suas operações comerciais.*
* **4 de maio de 2026**: os ambientes que ainda usam APIs obsoletas **não receberão atualizações críticas de versões do Adobe** e não estão sujeitos aos compromissos padrão da Adobe sobre desempenho e disponibilidade. Como resultado, você não receberá novos recursos ou correções de erros, a estabilidade e o tempo de atividade do aplicativo podem ser afetados negativamente e a exposição ao risco de segurança pode aumentar ainda mais.

Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md#aem-apis) para obter detalhes completos, mas, para conveniência, essas APIs estão listadas abaixo:

+++ Expanda para ver as descontinuações da API Java

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Recursos do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Funções do AEM Edge (Programa Beta) {#edge-functions}

O AEM Edge Functions permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

#### Cloud Manager MCP Server (Programa Beta) {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480347/?captions=por_br&quality=12)

IDEs modernos usam o protocolo de contexto de modelo (MCP) para permitir que modelos de linguagem grandes (LLMs) chamem ferramentas expostas por servidores MCP. Em vez de integrar diretamente com especificações de API de baixo nível, os desenvolvedores podem simplesmente descrever sua intenção em linguagem natural.

Agora disponível na versão beta, o servidor MCP do Cloud Manager permite que você interaja com as APIs do Cloud Manager diretamente do IDE usando prompts. Os cenários compatíveis incluem a execução de pipelines, a verificação do status do ambiente e muito mais.

Saiba mais sobre [Servidores MCP do AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Para solicitar acesso ao Cloud Manager MCP Server beta, envie um email para [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com) e inclua uma descrição do seu caso de uso.

#### Solução de problemas do pipeline de configuração no nível da Web com o agente de desenvolvimento (Programa Beta) {#devagent-webtier}

Os recursos de [solução de problemas de pipeline](/help/ai-in-aem/agents/brand-experience/development/development.md) do Agente de Desenvolvimento ajudam os desenvolvedores a diagnosticar e resolver problemas de forma eficiente nas implantações do AEM as a Cloud Service. Além de oferecer suporte a pipelines de Empilhamento completo (Implantação e Qualidade de Código), o Agente de Desenvolvimento agora oferece suporte à solução de problemas do **Pipeline de configuração no nível da Web** como parte de um programa beta.

Para solicitar acesso ao beta, envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). É necessário acesso pré-existente aos Agentes no AEM.

#### Ferramentas de IA do IDE para desenvolvimento em Java e Dispatcher do AEM (Programa Beta) {#ai-dev-beta}

As equipes de pilha em Java estão cada vez mais usando o desenvolvimento assistido por IA em ferramentas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar a entrega de recursos e melhorar a qualidade do código. Associe-se à versão beta para:

* Compartilhar experiências reais para ajudar a moldar futuros recursos de IA compatíveis com a Adobe
* Experimente as ferramentas do IDE que podem ser usadas pelos agentes de IA para gerar e depurar o código AEM e a configuração do Dispatcher

Envie um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) para obter mais informações.

#### Ferramentas de IA do IDE para AEM 6.5 para migração do AEM Cloud Service (Programa Alpha) {#cm-ide-migration}

Acelere sua migração do AEM 6.5 para o AEM as a Cloud Service (pilha Java) usando as ferramentas de IA do IDE para agir de acordo com as recomendações do [Relatório do Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) para obter mais informações.

#### Autenticação do Edge para Edge Delivery Services (Programa Beta) {#edge-authentication}

A autenticação da Edge permite restringir o acesso às páginas do Edge Delivery Services somente àqueles que se autenticaram com seu provedor de identidade (IdP). Isso é feito implantando um arquivo YAML de configuração do OpenID Connect (OIDC).

Se estiver interessado, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do caso de uso e suas dúvidas.

#### Implantações de produção canária para testar o código antes de aceitar o tráfego direto (programa Beta) {#canary-beta}

Valide uma build de produção com tráfego de teste somente interno antes de expô-la aos usuários finais. Entregar para produção, rotear apenas tráfego canário (usando um cabeçalho especial), monitorar o comportamento e promover para tráfego ativo ou reverter, sem afetar os clientes.

Implante as versões de código para produção, mas restrinja-as somente ao tráfego de teste interno antes de decidir se aceita o tráfego ativo ou não.

Envie um email [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acesso e compartilhar feedback.

#### Instantâneos para RDEs (Programa Beta) {#rde-snapshot-program}

Na versão beta, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em usar e fornecer feedback sobre este recurso.

#### APM (Application Performance Monitoring, monitoramento do desempenho de aplicativos) expandido (programa Alpha) {#apm-alpha}

Para fins de observação, o AEM Cloud Service oferece suporte atualmente ao [New Relic One](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornecido pela Adobe e ao [Dynatrace](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gerenciado pelo cliente. À medida que exploramos o suporte para opções adicionais de APM, envie um email para [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) com seu fornecedor ou tecnologia de preferência, juntamente com casos de uso.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
