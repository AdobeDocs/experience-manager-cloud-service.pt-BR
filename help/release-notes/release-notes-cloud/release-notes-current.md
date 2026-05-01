---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 687be0c3895cbcd8a9530d25f279100f610efe96
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 6%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2026.4.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 30 de abril de 2026. A próxima versão do recurso (2026.5.0) está planejada para 28 de maio de 2026.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)
-->

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

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Integração da tradução de IA {#ai-translation-integration}

Os usuários do AEM agora podem aproveitar os Modelos de idiomas grandes (LLMs) para tradução de conteúdo, fornecendo qualidade de tradução humana com velocidade de tradução automática. Semelhante aos serviços tradicionais de tradução de terceiros, o Azure OpenAI pode ser configurado como um provedor de tradução no AEM, com suporte para LLMs adicionais planejados para versões futuras. Os clientes usam suas próprias licenças LLM para esse recurso. Além disso, os guias de estilo de tradução corporativa podem ser carregados no AEM, permitindo a extração de regras de tradução para garantir a consistência da marca e do estilo. Consulte [Configurando a integração da tradução de IA](/help/sites-cloud/administering/translation/ai-translation-integration.md) para obter mais informações.

### Editor de fragmento de conteúdo {#cf-editor}

O novo Editor de fragmento de conteúdo agora permite visualizar a representação em JSON de um fragmento de conteúdo. Isso ajuda a validar a estrutura do conteúdo independentemente da renderização e restaura a paridade com o Editor de fragmento de conteúdo anterior na interface para toque do AEM para esse recurso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**O Supervisor de Conteúdo agora está disponível para aplicativos Adobe Workfront e não Adobe**

O Supervisor de conteúdo agora está disponível para aplicativos Adobe Workfront e não-Adobe (de terceiros), ampliando a detecção inteligente de ativos e a reutilização de conteúdo para além da Adobe Express e da AEM Sites. Esta versão oferece a experiência completa do Supervisor de conteúdo, incluindo pesquisa habilitada por IA, recomendações com reconhecimento de contexto, descoberta de campanhas com base em resumo, acesso a representações do Dynamic Media, descoberta de fragmentos de conteúdo, filtros e metadados de ativos para fluxos de trabalho do Adobe Workfront e aplicativos externos.

Agora você pode detectar, avaliar e reutilizar ativos aprovados da AEM Assets diretamente de seus aplicativos preferidos, permitindo o uso consistente de ativos, a maior eficiência e a criação simplificada de conteúdo em aplicativos Adobe e não Adobe.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms

* **Substituir configuração de nuvem do reCAPTCHA por OSGi** 
As IDs de projeto, chaves de site e segredos do reCAPTCHA Enterprise que você mantém com seus arquivos de origem podem ser resolvidos em valores diferentes em cada ambiente do Cloud Service depois que você [adicionar a substituição e a implantação da Configuração Sensível ao Contexto pelo Cloud Manager](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi).

* **Autenticação baseada em certificado** 
O Forms adaptável que envia para uma lista do Microsoft SharePoint agora oferece suporte à [autenticação baseada em certificado](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication) junto com a autenticação de URL OAuth. Para logon baseado em certificado, registre um alias de certificado e detalhes do locatário no AEM e no Microsoft Azure.

* **Aprimoramentos do Editor de Regras**

   * O editor de regras do Adaptive Forms agora oferece suporte à gramática simplificada para [regras de Evento de Despacho e Evento de Acionamento para acionadores prontos para uso (OOTB) e para eventos personalizados](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events), de modo que os autores não estão limitados à gramática somente em acionadores personalizados.
   * Quando as regras no Forms Adaptável baseadas em Componentes Principais agora incluem o [componente de Anexo de Arquivo junto com outras condições usando a lógica AND ou OR](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component), de modo que a regra executa suas ações somente quando o estado do anexo e as outras verificações avaliam como pretendido.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Novos recursos {#foundation-new}

#### Ferramentas de IA do IDE para desenvolvimento em Java e Dispatcher do AEM {#ai-dev}

As equipes de pilha em Java estão cada vez mais usando o desenvolvimento assistido por IA em ferramentas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar a entrega de recursos e melhorar a qualidade do código.

As ferramentas do IDE podem ser usadas pelos agentes de codificação para gerar e depurar o código AEM e a configuração do Dispatcher. Como exemplo, a apresentação em vídeo abaixo demonstra como criar um componente do AEM usando as Habilidades do agente.

Saiba mais sobre o [Desenvolvimento local com Ferramentas de IA](/help/ai-in-aem/local-development-with-ai-tools.md) e sinta-se à vontade para enviar um email para [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) com perguntas ou comentários.


>[!VIDEO](https://video.tv.adobe.com/v/3484978/?learn=on&enablevpops)

#### Servidor MCP de governança da experiência {#gov-mcp-server}

O Servidor MCP de governança de experiência agora está disponível ao público em geral (GA). Ele se integra a ferramentas de desenvolvedor de IA e chatbots que oferecem suporte ao protocolo de contexto de modelo (MCP), permitindo que você proteja a integridade e a conformidade da marca usando prompts de linguagem natural em seu chatbot ou IDE. Você pode avaliar o conteúdo (texto, imagens, páginas) em relação às regras de governança da marca e recuperar as configurações da marca e as verificações de governança disponíveis.

Saiba mais sobre [Servidores MCP do AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) e o [Agente de Governança](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview).

#### Claude Connector {#aem-claude-connector}

Os usuários do Claude podem navegar no [Marketplace do Conector](https://claude.ai/settings/connectors) do Anthropic para instalar o [Conector do Adobe Experience Manager](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector) com um clique. Esse servidor MCP expõe um conjunto crescente de ferramentas para interagir com o AEM, incluindo a edição de conteúdo por meio de prompts.

#### AEM OIDC em Publicar novos recursos {#aem-oidc-on-publish-new-features}

* Correção: os parâmetros de consulta da solicitação original são perdidos após a autenticação
* Redirecionamento Personalizado Após Autenticação na [documentação](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication) de Autenticação OIDC

#### Suporte ao serviço de email para a API de gráfico do Microsoft {#mail-service-graph-api}

O Serviço de email da AEM agora é compatível com o Microsoft® Outlook (via Microsoft 365) usando a API de gráfico do Microsoft. Isso é particularmente útil para organizações que não permitem o SMTP, que já é compatível com o serviço de email. A autenticação é via OAuth 2.0. [Saiba como configurar](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api).

#### Os logs do CDN podem ser encaminhados para a lógica do Sumo {#sumo-cdn-logforwarding}

O [recurso de Encaminhamento de Log](/help/implementing/developing/introduction/log-forwarding.md#sumologic) agora dá suporte ao envio de logs CDN para o Sumo Logic. Anteriormente, o encaminhamento de logs para o Sumo Logic era limitado aos logs do AEM.

### Avisos importantes sobre a base [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-notices}

#### Erros ricos de autenticação do IMS {#ims-auth-rich-errors}

Para ajudar a solucionar problemas de integrações IMS, `imsauth` adicionou suporte para *erros avançados*.

Em vez de retornar apenas um código de status HTTP, esses erros fornecem contexto adicional para ajudar a diagnosticar e resolver problemas que podem bloquear a autenticação e o acesso.

#### Desaprovações da API Java {#java-api-deprecation}

É essencial remover o uso de APIs obsoletas.

Desde **14 de abril**, os pipelines do Cloud Manager que contêm código usando APIs direcionadas à remoção de 26/02/2026 **falham durante a etapa Qualidade do código**. As implantações serão bloqueadas até que o uso da API obsoleta seja removido. *Isso pode impedir que você libere atualizações com prazo determinado e pode afetar suas operações comerciais.*

A partir de **11 de junho de 2026**, os ambientes que ainda usam essas APIs obsoletas **não receberão atualizações críticas de versões do Adobe** e não estarão sujeitos aos compromissos padrão da Adobe sobre desempenho e disponibilidade. Como resultado, você não receberá novos recursos ou correções de erros, a estabilidade e o tempo de atividade do aplicativo podem ser afetados negativamente e a exposição ao risco de segurança pode aumentar ainda mais.

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

### Recursos do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Funções do AEM Edge (Programa Beta) {#edge-functions}

[O AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md) permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para assistentes de IA como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

#### Solução de problemas do pipeline de configuração no nível da Web (Programa Beta) {#devagent-webtier}

Os recursos de [solução de problemas de pipeline](/help/ai-in-aem/agents/brand-experience/development/development.md) do Agente de Desenvolvimento ajudam os desenvolvedores a diagnosticar e resolver problemas de forma eficiente nas implantações do AEM as a Cloud Service. Além de oferecer suporte a pipelines de Empilhamento completo (Implantação e Qualidade de Código), o Agente de Desenvolvimento agora oferece suporte à solução de problemas do **Pipeline de configuração no nível da Web** como parte de um programa beta.

Para solicitar acesso ao beta, envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). É necessário acesso pré-existente aos Agentes no AEM.

#### Solução de problemas do Replication AI (Programa Alpha) {#replication-ai-troubleshooting-alpha}

Usando o Assistente de IA no AEM Author e em outras interfaces, você pode solucionar problemas relacionados à replicação, como filas bloqueadas. Para participar do Programa Alpha, envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com), descrevendo seu interesse.

#### Ferramentas de IA do IDE para AEM 6.5 para migração do AEM Cloud Service (Programa Beta) {#cm-ide-migration}

Acelere sua migração do AEM 6.5 para o AEM as a Cloud Service (pilha Java) usando as ferramentas de IA do IDE para agir de acordo com as recomendações do [Relatório do Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Email [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) para obter mais informações e para solicitar acesso ao recurso.

#### Autenticação do Edge para Edge Delivery Services (Programa Beta) {#edge-authentication}

A autenticação da Edge permite restringir o acesso às páginas do Edge Delivery Services somente àqueles que se autenticaram com seu provedor de identidade (IdP). Isso é feito implantando um arquivo YAML de configuração do OpenID Connect (OIDC).

Se estiver interessado, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do caso de uso e suas dúvidas.

#### Implantações de produção canária para testar o código antes de aceitar o tráfego direto (programa Beta) {#canary-beta}

Valide uma build de produção com tráfego de teste somente interno antes de expô-la aos usuários finais. Entregar para produção, rotear apenas tráfego canário (usando um cabeçalho especial), monitorar o comportamento e promover para tráfego ativo ou reverter, sem afetar os clientes.

Envie um email [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acesso e compartilhar feedback.

#### Instantâneos para RDEs (Programa Beta) {#rde-snapshot-program}

Na versão beta, os Ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso [para obter um instantâneo](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots) do estado atual do código e conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em usar e fornecer feedback sobre este recurso.

#### APM (Application Performance Monitoring, monitoramento do desempenho de aplicativos) expandido (programa Alpha) {#apm-alpha}

Para fins de observação, o AEM Cloud Service oferece suporte atualmente ao [New Relic One](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornecido pela Adobe e ao [Dynatrace](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gerenciado pelo cliente. À medida que exploramos o suporte para opções adicionais de APM, envie um email para [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) com seu fornecedor ou tecnologia de preferência, juntamente com casos de uso.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
