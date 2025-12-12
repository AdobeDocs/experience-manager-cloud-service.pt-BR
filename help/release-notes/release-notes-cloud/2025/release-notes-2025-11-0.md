---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.11.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.11.0.
feature: Release Information
role: Admin
source-git-commit: 2cc6f1bea3fc9cd56a20048db0ce5357dbb5ee0e
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.11.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.11.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.11.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 20 de novembro de 2025. O próximo lançamento de recursos (2025.12.0) está planejado para sexta-feira, 11 de dezembro de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440925?captions=por_br&quality=12)

-->

## Agentes no AEM {#agents-in-aem}

O AEM fornece diversos agentes que permitem acelerar a criação de conteúdo e orquestrar alterações automaticamente. Para obter mais informações, consulte [Visão geral dos agentes](/help/ai-in-aem/agents/overview.md).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### Novos recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O Programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Essas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Aprimoramentos na comunicação interativa

##### Bloqueio de modelo

Bloqueie o conteúdo e os elementos de layout nos modelos para manter a integridade da marca e evitar modificações não autorizadas. Isso garante a consistência do design em todas as comunicações.

##### Suporte a estouro de conteúdo

Introdução da opção &quot;Permitir quebras de página no conteúdo&quot; para layouts com fluxo. Esse aprimoramento permite uma edição suave de várias páginas e um melhor gerenciamento de texto para documentos complexos.

##### Edição de arquivo XDP

O editor de comunicação interativa agora é compatível com a edição de XDP, incluindo a integração de fragmentos. Agora é possível editar arquivos XDP em um navegador em vez do Forms Designer, que é executado somente na área de trabalho do Microsoft Windows.

##### Numeração dinâmica de páginas

Exiba automaticamente &quot;Número da página de ##&quot; nas páginas mestras para uma paginação clara e consistente em documentos de várias páginas.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Novos recursos {#foundation-new}

#### Futuras descontinuações da API Java {#java-api-deprecation}

Várias APIs obsoletas foram marcadas para remoção em 31 de agosto e, portanto, não devem mais ser referenciadas. Você receberá notificações da Central de ações se o uso obsoleto da API for detectado no código e, após 3 de dezembro, avisos serão exibidos durante os builds do Cloud Manager para reforçar a importância de remover o uso. Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md#aem-apis) para obter detalhes completos, mas, para conveniência, essas APIs estão listadas abaixo:

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
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

#### Descontinuação do Java 11 Runtime {#java11-runtime-deprecation}

A Adobe atualizou os ambientes **Preparo** e **Produção** para o **tempo de execução do Java 21** de maior desempenho em 14 de outubro de 2025. A partir de **final de janeiro**, nem o AEM Cloud Service SDK nem qualquer ambiente de nuvem funcionarão com o Java 11 runtime.

>[!NOTE]
>
> Para aproveitar as otimizações de desempenho e aprimoramentos de linguagem mais recentes, é recomendável criar com Java 17 ou Java 21 (preferencial). A construção com Java 8 e Java 11 permanece suportada por enquanto, mas será descontinuada em uma versão futura. Uma comunicação separada será emitida antes da desativação. Consulte a seção *requisitos de tempo de compilação* de [este artigo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Conforme observado nas notas de versão de abril, os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **10 de dezembro**, todas as substituições de log personalizadas não suportadas serão ignoradas. Com base em nossa análise, a maioria dos clientes não será afetada e a Adobe entrou em contato com clientes cuja configuração atual pode ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Recursos do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Pausar Atualizações de Manutenção Automática {#pause-updates}

Dias de ativação, eventos ao vivo, pico de vendas — esses momentos não quebram. [Nossos novos recursos de autoatendimento](/help/implementing/deploying/quiet-hours-update-free-periods.md) interrompem as atualizações de manutenção automáticas quando é importante, para que suas equipes permaneçam focadas.

* Quiet Hours: bloqueia a manutenção automática durante os horários definidos a cada dia. Ideal para horas de trabalho, corridas noturnas ou cortes matinais.
* Período Livre de Atualização: Bloqueia a manutenção automática por uma semana inteira. Use-o para inicializações, promoções ou congelamentos anuais.

>[!NOTE]
>
>Disponível como um recurso de Disponibilidade limitada em 25 de setembro.
>Envie um email para [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para ativá-lo em seus programas.
>

#### Computação Edge (Programa Beta) {#edge-computing}

A computação Edge permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

#### Autenticação do Edge para Edge Delivery Services (Programa Beta) {#edge-authentication}

A autenticação da Edge permite restringir o acesso às páginas do Edge Delivery Services somente àqueles que se autenticaram com seu provedor de identidade (IdP). Isso é feito implantando um arquivo YAML de configuração do OpenID Connect (OIDC).

Se estiver interessado, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do caso de uso e suas dúvidas.

<!--
#### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

#### Implantações de produção canária para testar o código antes de aceitar o tráfego direto (programa Beta) {#canary-beta}

Valide uma build de produção com tráfego de teste somente interno antes de expô-la aos usuários finais. Entregar para produção, rotear apenas tráfego canário (usando um cabeçalho especial), monitorar o comportamento e promover para tráfego ativo ou reverter, sem afetar os clientes.

Implante as versões de código para produção, mas restrinja-as somente ao tráfego de teste interno antes de decidir se aceita o tráfego ativo ou não.

Envie um email [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acesso e compartilhar feedback.


#### Respostas da IA - Respostas mais inteligentes e sensíveis ao contexto para o AEM Sites (Programa Beta) {#ai-answers-beta}

As respostas de IA apresentam uma nova maneira de os visitantes interagirem com o conteúdo. Desenvolvido pela tecnologia Retrieval-Augmented Generation (RAG), ele usa seus dados gerenciados pela AEM para fornecer respostas precisas e consistentes com a marca, diretamente em suas experiências digitais.

Estamos nos preparando para lançar o Programa Beta de Respostas de IA e agora convidamos os clientes a registrar seu interesse. Como o beta terá capacidade muito limitada, as inscrições antecipadas receberão consideração de prioridade. A participação na versão beta permitirá explorar as respostas de IA no ambiente do AEM Cloud Service, validar o desempenho e a precisão e ajudar a definir a experiência futura antes que ela esteja disponível.

Para solicitar participação ou receber atualizações, contate [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com).

#### Acelere o desenvolvimento do AEM com IA (Programa Alpha)  {#ai-dev-alpha}

As equipes do AEM Java-stack estão usando cada vez mais o desenvolvimento assistido por IA em ferramentas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar a entrega de recursos e melhorar a qualidade do código. Estamos reunindo experiências reais para ajudar a moldar os futuros recursos de IA compatíveis com o Adobe.

Compartilhe o que está trabalhando para a sua equipe — e o que você gostaria que a Adobe fornecesse — enviando um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

#### Instantâneos para RDEs (Programa Alpha) {#rde-snapshot-program}

Em alfa, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em fornecer feedback sobre esse recurso.

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
