---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bdc0e7623592efed5270a3cb8322ef22e50cbad9
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 7%

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

A data de lançamento da versão atual (2025.9.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 25 de setembro de 2025. O próximo lançamento de recursos (2025.10.0) está planejado para sexta-feira, 30 de outubro de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no pré-lançamento do Experience Manager Sites {#prerelease-sites}

O Editor de modelos de conteúdo para Fragmentos de conteúdo do AEM foi modernizado para se alinhar a outras interfaces baseadas no Espectro React no AEM. Seu modelo de implementação e extensibilidade da interface do usuário agora é consistente com o Editor de fragmento de conteúdo e o Editor universal. O novo Editor de modelos agora é padrão quando aberto na nova interface do Administrador do modelo de conteúdo. A abertura de um modelo de conteúdo na interface para toque abre o editor da interface para toque e se oferece para experimentar o novo editor.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Assets {#new-features-assets-view}

**Formatação de Texto Aprimorada com Subsequências em Modelos do Dynamic Media**

Agora é possível aplicar formatação a substrings em camadas de texto de modelo do Dynamic Media. Uma palavra ou frase selecionada é tratada como uma camada separada, permitindo que você ajuste sua fonte, tamanho da fonte, cor e muito mais. A camada da substring é parametrizada para que você possa atualizá-la em tempo real usando o URL de entrega do template

### Novos recursos no Dynamic Media com recursos OpenAPI {#new-features-dynamic-media-with-openapi}

**DM compatível com SEO com URLs OpenAPI**

Crie URLs personalizados para entrega de ativos no DM com OpenAPI, substituindo UUIDs longos gerados pelo sistema por identificadores curtos e legíveis. Isso torna os links de SEO amigáveis e mais alinhados à sua marca ou campanhas. Os URLs personalizados são resolvidos automaticamente para a UUID do ativo original no tempo de execução, sem interromper os fluxos de trabalho existentes.

>[!NOTE]
>
>Esse recurso está disponível como um recurso de Disponibilidade limitada. Você pode [criar e enviar um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para habilitá-lo para sua implantação.

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no Experience Manager Forms {#new-features-forms}

**Componente de Entrada de Data e Hora**

Um [componente de Data e Hora](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component) está disponível, permitindo que os usuários selecionem data e hora usando um calendário e uma interface de relógio ou inserindo valores manualmente em um formato com suporte.

**Tratamento de Erros Aprimorado para Carregamentos de Arquivos**

O [componente Anexo de Arquivo](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab) agora valida automaticamente o tipo de arquivo carregado em relação à lista de permissões. Se um usuário carregar um arquivo em um formato não compatível, o formulário exibirá um erro durante o envio. O componente também verifica o conteúdo do arquivo para validar seu tipo, melhorando a segurança geral do formulário.

**Resposta de Erro Especificada para Ação de Envio Personalizada**

Quando uma [ação de envio personalizada](/help/forms/custom-submit-action-troubleshooting.md) encontra um erro sem tratamento, o sistema retorna o código de erro 502. Isso ajuda a identificar que o problema está relacionado à ação de envio personalizada, facilitando a depuração.

**Excluindo campos ocultos do documento de registro**

Uma nova propriedade permite a exclusão de campos ocultos do [Documento de Registro](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings). Por padrão, essa opção não está selecionada e se aplica a todos os campos de formulário.


### Recursos de pré-lançamento no AEM Forms

**Gerar e sincronizar representações AFP**

Agora você pode usar a [API de comunicação do AEM Forms](/help/forms/document-generation-afp-api.md) para converter um arquivo XDP para o formato AFP. O AFP é um formato de alto desempenho amplamente usado em impressão corporativa em larga escala.

**Aprimoramentos no Editor de Regras**

* [Validar método na Lista de Funções](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): os métodos validate e reset agora oferecem suporte para execução nos níveis de painel, campo e formulário. Anteriormente, eles só eram compatíveis no nível do formulário.
* [Suporte a JavaScript Moderno](/help/forms/rule-editor-core-components-difference-tables.md): o suporte a recursos do ECMAScript 2019 e posteriores foi adicionado para funções personalizadas, permitindo que você escreva código mais eficiente, modular e reutilizável.
* [Opção Baixar DoR no Editor de Regras](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): uma função para baixar o Documento de Registro (DoR) foi adicionada como uma opção pronta para uso (OOTB) no Editor de Regras.

  ![Documento de Registro](/help/forms/assets/document-of-record-rn.gif)

* [Variáveis dinâmicas no Editor de regras](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): agora você pode usar variáveis dinâmicas (temporárias) no Editor de regras para obter maior flexibilidade na definição de condições e ações. Campos ocultos não são mais necessários para armazenar valores temporários.
* [Suporte a Regras Personalizadas Baseadas em Eventos](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): Agora é possível definir eventos personalizados e acionar regras com base nesses eventos.
* [Regras de painel repetíveis sensíveis ao contexto](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): em painéis repetíveis, as regras agora são executadas com base no contexto, em vez de serem aplicadas somente à última instância do painel.
* [Regras acionadas por Parâmetros](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): o Editor de Regras agora oferece suporte à execução de regras com base em parâmetros de consulta, parâmetros UTM ou parâmetros do navegador.
* [Funções personalizadas específicas de formulário](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): o Edge Delivery Services Forms agora oferece suporte a scripts de funções personalizadas específicas de formulário, fornecendo maior flexibilidade no gerenciamento de lógica reutilizável.
* [Importações Estáticas para Funções Personalizadas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): o Editor de Regras no Universal Editor agora oferece suporte a importações estáticas, permitindo que os desenvolvedores organizem, compartilhem e reutilizem funções em vários formulários.

### Novos recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O Programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Essas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

**Componente de assinatura de assinatura de assinatura**

Agora você pode usar o [componente de Assinatura Escrita](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature) para ajudar os usuários a adicionar suas assinaturas a um formulário, como em um formulário de contrato. O componente permite aos usuários desenhar sua assinatura diretamente no formulário usando um mouse, caneta ou tela sensível ao toque.

**Integração de API direta no Editor de regras**

O Forms adaptável agora oferece suporte à [integração de API direta](/help/forms/api-integration-in-rule-editor.md) no Editor de regras visuais sem exigir um Modelo de dados de formulário. Os autores podem configurar APIs usando uma importação de URL ou cURL, mapear parâmetros de entrada/saída e chamadas seguras com autenticação.

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

### Novos recursos no Release Management {#new-features-release-management}

**Pausar Atualizações de Manutenção Automática**

Dias de ativação, eventos ao vivo, pico de vendas — esses momentos não quebram. [Nossos novos recursos de autoatendimento](/help/implementing/deploying/quiet-hours-update-free-periods.md) interrompem as atualizações de manutenção automáticas quando é importante, para que suas equipes permaneçam focadas.

* Quiet Hours: bloqueia a manutenção automática durante os horários definidos a cada dia. Ideal para horas de trabalho, corridas noturnas ou cortes matinais.
* Período Livre de Atualização: Bloqueia a manutenção automática por uma semana inteira. Use-o para inicializações, promoções ou congelamentos anuais.

>[!NOTE]
>
>Disponível como um recurso de Disponibilidade limitada em 25 de setembro.
>>Envie um email para [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para ativá-lo em seus programas.

### Nova versão das ferramentas de desenvolvedor do AEM para Eclipse {#aem-develeper-tools-for-eclipse}

A versão 1.4.0 das Ferramentas de desenvolvedor do AEM para Eclipse foi lançada. Esta versão adiciona suporte para o Eclipse IDE 2022-12 ou mais recente e foi validada com a versão atual (2025-09). A ferramenta agora funciona com versões modernas do Arquétipo de projeto do AEM e incorpora melhorias da ferramenta Sling IDE 1.3.0.

Instale a partir do [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) e consulte a [página Ferramentas para desenvolvedores do AEM](https://eclipse.adobe.com) para obter mais detalhes.

### Futuras descontinuações da API Java {#java-api-deprecation}

Várias APIs obsoletas foram marcadas para remoção em 31 de agosto e, portanto, não devem mais ser referenciadas. Você receberá notificações da Central de ações se o uso obsoleto da API for detectado no código e, após 13 de novembro, avisos serão exibidos durante os builds do Cloud Manager para reforçar a importância de remover o uso. Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md#aem-apis) para obter detalhes completos, mas, para conveniência, essas APIs estão listadas abaixo:

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

### Descontinuação do Java 11 Runtime {#java11-runtime-deprecation}

O *Java 11 runtime* está obsoleto, e a maioria dos ambientes já foi atualizada para o **Java 21 runtime** de maior desempenho.

Se seu ambiente não pôde ser atualizado devido a dependências sem suporte (consulte os [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), você deve ter recebido um email do Adobe com as próximas etapas. Conforme descrito, a Adobe atualizou seus ambientes **Dev** e **RDE** em **18 de setembro de 2025** para que você possa validar seu site e processos e resolver quaisquer problemas. As atualizações para o **Estágio** e a **Produção** continuarão em **14 de outubro de 2025**.

>[!NOTE]
>
>A versão de tempo de execução é separada da versão de build do seu código. Embora recomendemos a criação com o Java 21, as builds do Java 11 ainda são aceitas por enquanto. Um aviso de descontinuação separado para builds do Java 11 será compartilhado no futuro.

### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Conforme observado nas notas de versão de abril, os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **30 de outubro**, todas as substituições de log personalizadas não suportadas serão ignoradas. Com base em nossa análise, a maioria dos clientes não será afetada e a Adobe entrou em contato com clientes cuja configuração atual pode ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Computação Edge (Programa Beta) {#edge-computing}

A computação Edge permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

### Autenticação do Edge para Edge Delivery Services (Programa Beta) {#edge-authentication}

A autenticação da Edge permite restringir o acesso às páginas do Edge Delivery Services somente àqueles que se autenticaram com seu provedor de identidade (IdP). Isso é feito implantando um arquivo YAML de configuração do OpenID Connect (OIDC).

Se estiver interessado, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do caso de uso e suas dúvidas.

Separadamente da Edge Delivery Services, observe que no início deste ano lançamos um recurso para configurar o Open ID Connect [para projetos de nível de publicação do AEM Cloud Service](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md) para proteger páginas do AEM.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Instantâneos para RDEs (Programa Alpha) {#rde-snapshot-program}

Em alfa, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em fornecer feedback sobre esse recurso.

### Encaminhamento de logs do AEM para mais destinos (programa Beta) {#log-forwarding-beta}

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao encaminhamento de logs do AEM e do CDN para o Armazenamento de Blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Agora na versão beta, você pode encaminhar logs do AEM para o Amazon S3, Sumo Logic, Dynatrace e sua própria conta da New Relic (não a conta fornecida pela Adobe). Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis com esses destinos de log, mas não com os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

Saiba mais na [documentação sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md).

### APM (Application Performance Monitoring, monitoramento do desempenho de aplicativos) expandido (programa Alpha) {#apm-alpha}

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
