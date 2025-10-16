---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0.
feature: Release Information
role: Admin
source-git-commit: 245ad07ba6abbf18e2011cb71a15948c9b92f80f
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 8%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.8.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.8.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 28 de agosto de 2025. O próximo lançamento de recursos (2025.9.0) está planejado para sexta-feira, 25 de setembro de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

O [Experience Hub](/help/experience-hub.md) é o seu ponto de partida centralizado para acessar todos os recursos do AEM. Ele é personalizado com base na persona do usuário e nas licenças disponíveis para você, permitindo que cada usuário atinja seus resultados com eficiência.

## Assistente de IA no AEM {#AI-assistant}

O [Assistente de IA](/help/implementing/cloud-manager/ai-assistant-in-aem.md) para AEM oferece uma interface conversacional projetada para lhe dar respostas instantâneas às suas perguntas sobre produtos da AEM (*disponível para todos os usuários*) e para automatizar a criação de tíquete de suporte (*disponível para Administradores de Suporte*). Ele é diretamente incorporado ao AEM e acessível no AEM Experience Hub, Cloud Manager e na interface do usuário do autor.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no Experience Manager Sites {#enhancements-sites}

* Na interface do administrador dos fragmentos de conteúdo, agora é possível visualizar o status do fluxo de trabalho para fragmentos de conteúdo, com informações detalhadas sobre fluxos de trabalho anteriores e atuais de um fragmento selecionado.
* O desempenho para abrir fragmentos de conteúdo no novo editor de fragmento de conteúdo foi aumentado em 25% em cenários comuns, ao abrir fragmentos por meio da UUID em vez do caminho.
* Ao copiar fragmentos de conteúdo com fragmentos referenciados, as cópias dos fragmentos referenciados agora são armazenadas no mesmo local da cópia do fragmento principal.
* Agora você pode configurar um espaço de trabalho personalizado nas configurações da pasta para exportar os fragmentos de conteúdo para o espaço de trabalho configurado no Adobe Target.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no Content Hub {#new-features-content-hub}

**Pesquisa em massa por meio das propriedades do Filtro**

Agora, o Content Hub agiliza a detecção dos ativos necessários. Com o novo recurso Pesquisa em massa, você pode inserir vários valores para qualquer propriedade de filtro, separados por um delimitador (por exemplo, várias IDs de SKU), e recuperar instantaneamente todos os ativos correspondentes usando uma única pesquisa.

### Novos recursos no Dynamic Media com recursos OpenAPI {#new-features-dynamic-media-with-openapi}

**URLs de entrega de ativos com marca e legíveis**

Torne o Dynamic Media com URLs OpenAPI mais legíveis por humanos, aproveitando URLs personalizados no Dynamic Media com OpenAPI. Os URLs personalizados permitem substituir UUIDs longos, gerados pelo sistema e difíceis de memorizar nos URLs de entrega de ativos por identificadores curtos controlados pela marca. Isso torna os URLs personalizados mais curtos, mais fáceis de ler e compartilhar, e permite um melhor alinhamento com sua marca ou campanhas. Os URLs personalizados são resolvidos automaticamente para a UUID do ativo original no tempo de execução, sem interromper os fluxos de trabalho existentes.

>[!NOTE]
>
>Esse recurso estará disponível como um recurso de Disponibilidade limitada em 10 de setembro. Você pode [criar e enviar um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) para habilitá-lo para sua implantação.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [Componente de entrada de data e hora](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component): um componente de data e hora está disponível, permitindo que os usuários selecionem data e hora usando uma interface de calendário e relógio ou inserindo valores manualmente em um formato com suporte.
* [Tratamento de Erros Aprimorado para Carregamentos de Arquivos](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab): o componente de Anexo de Arquivo agora valida automaticamente o tipo de arquivo carregado em relação à lista de permissões. Se um usuário carregar um arquivo em um formato não compatível, o formulário exibirá um erro durante o envio. O componente também verifica o conteúdo do arquivo para validar seu tipo, melhorando a segurança geral do formulário.
* [Resposta de Erro Especificada para Ação de Envio Personalizada](/help/forms/custom-submit-action-troubleshooting.md): Quando uma ação de envio personalizada encontra um erro sem tratamento, o código de erro 502 é retornado. Isso ajuda a identificar que o problema está relacionado à ação de envio personalizada, facilitando a depuração.
* [Excluindo campos ocultos do documento de registro](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings): uma nova propriedade foi adicionada para permitir a exclusão de campos ocultos do documento de registro. Por padrão, essa opção não está selecionada e se aplica a todos os campos de formulário.

### Recursos de pré-lançamento no AEM Forms

* [Gerar e sincronizar representações AFP](/help/forms/document-generation-afp-api.md): agora você pode usar a API de comunicação do AEM Forms para converter um arquivo XDP para o formato AFP. O AFP é um formato de alto desempenho amplamente usado em impressão corporativa em larga escala.
* **Aprimoramentos no Editor de Regras**
   * [Validar método na Lista de Funções](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): os métodos validate e reset agora oferecem suporte para execução nos níveis de painel, campo e formulário. Anteriormente, eles só eram compatíveis no nível do formulário.
   * [Suporte a JavaScript Moderno](/help/forms/rule-editor-core-components-difference-tables.md): o suporte a recursos do ECMAScript 2019 e posteriores foi adicionado para funções personalizadas, permitindo que você escreva código mais eficiente, modular e reutilizável
   * [Opção Baixar DoR no Editor de Regras](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): uma função para baixar o Documento de Registro (DoR) foi adicionada como uma opção pronta para uso (OOTB) no Editor de Regras.
     ![Documento de Registro](/help/forms/assets/document-of-record-rn.gif)
   * [Variáveis dinâmicas no Editor de regras](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): agora você pode usar variáveis dinâmicas (temporárias) no Editor de regras para obter maior flexibilidade na definição de condições e ações. Campos ocultos não são mais necessários para armazenar valores temporários.
   * [Suporte a Regras Personalizadas Baseadas em Eventos](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): Agora é possível definir eventos personalizados e acionar regras com base nesses eventos.
   * [Regras de painel repetíveis sensíveis ao contexto](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): em painéis repetíveis, as regras agora são executadas com base no contexto, em vez de serem aplicadas somente à última instância do painel.
   * [Regras acionadas por Parâmetros](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): o Editor de Regras agora oferece suporte à execução de regras com base em parâmetros de consulta, parâmetros UTM ou parâmetros do navegador.
   * [Funções personalizadas específicas de formulário](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): o Edge Delivery Services Forms agora oferece suporte a scripts de funções personalizadas específicas de formulário, fornecendo maior flexibilidade no gerenciamento de lógica reutilizável.
   * [Importações Estáticas para Funções Personalizadas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): o Editor de Regras no Universal Editor agora oferece suporte a importações estáticas, permitindo que os desenvolvedores organizem, compartilhem e reutilizem funções em vários formulários.

### Recursos iniciais do usuário no AEM Forms

* [Componente de assinatura assinável](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature): agora você pode usar o componente de assinatura assinável para ajudar os usuários a adicionar suas assinaturas a um formulário, como em um formulário de contrato. O componente permite aos usuários desenhar sua assinatura diretamente no formulário usando um mouse, caneta ou tela sensível ao toque.
* [Integração de API direta no Editor de regras](/help/forms/api-integration-in-rule-editor.md): o Adaptive Forms agora oferece suporte à integração de API direta no Editor de regras visuais sem exigir um Modelo de dados de formulário. Os autores podem configurar APIs usando uma importação de URL ou cURL, mapear parâmetros de entrada/saída e chamadas seguras com autenticação.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Atualização de compilação do JavaScript {#javascript-compilation}

A compilação padrão do JavaScript da biblioteca do lado do cliente (clientlibs) agora é direcionada para ECMASCRIPT_2018 em vez de ECMASCRIPT5. Embora substituível no passado, essa atualização permite melhorias de desempenho, sintaxe moderna do JavaScript e recursos por padrão.

### Futuras descontinuações da API Java {#java-api-deprecation}

Várias APIs obsoletas estão direcionando a remoção em 31 de agosto e, portanto, não devem mais ser referenciadas. No início de setembro, as notificações do Centro de ações serão enviadas se o uso da API for detectado e, após 25 de setembro, os avisos serão exibidos durante os builds do Cloud Manager para reforçar a importância de remover o uso. Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md#aem-apis) para obter detalhes completos, mas, para conveniência, essas APIs estão listadas abaixo:

<details>
  <summary>Expanda para ver as descontinuações da API Java</summary>

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
</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Descontinuação do Java 11 Runtime {#java11-runtime-deprecation}

O *Java 11 runtime* agora está obsoleto, e a maioria dos ambientes já foi atualizada para o **Java 21 runtime** mais eficiente.

Se seu ambiente não pôde ser atualizado devido a dependências sem suporte (consulte [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), você deve ter recebido um email da Adobe com as próximas etapas específicas. Verifique se todas as atualizações necessárias foram concluídas até **1º de outubro de 2025** para que seu ambiente possa ser atualizado sem interrupções.

Observação: a versão de tempo de execução é separada da versão de build do seu código. Embora recomendemos a criação com o Java 21, as builds do Java 11 ainda são compatíveis por enquanto. Um aviso de descontinuação separado para builds do Java 11 será compartilhado no futuro.

### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Conforme observado nas notas de versão de abril, os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **25 de setembro**, todas as substituições de log personalizadas não suportadas serão ignoradas. Com base em nossa análise, a maioria dos clientes não será afetada e a Adobe entrou em contato com clientes cuja configuração atual pode ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Computação Edge (Programa Beta) {#edge-computing}

A computação Edge permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Autenticação de usuários com um provedor de identidade antes de conceder acesso ao conteúdo
* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

### Configuração da CDN para o Edge Delivery Services (programa Beta) {#cdn-eds-beta}

A CDN gerenciada pela Adobe oferece opções de configuração flexíveis, conforme descrito no [artigo sobre Pipeline de configuração](/help/operations/config-pipeline.md#configurations).

Agora, na versão beta, você pode implantar um pipeline de configuração para recursos que incluem seletores de origem de CDN, transformações de resposta e solicitação, encaminhamento de log de CDN e muito mais. Entre em contato com [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) com os detalhes do seu caso de uso.

### Instantâneos para RDEs (Programa Alpha) {#rde-snapshot-program}

Em alfa, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em fornecer feedback sobre esse recurso.

### Encaminhamento de logs do AEM para mais destinos (programa Beta) {#log-forwarding-beta}

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao encaminhamento de logs do AEM e do CDN para o Armazenamento de Blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Agora na versão beta, você pode encaminhar logs do AEM para o Amazon S3, Sumo Logic, Dynatrace e sua própria conta da New Relic (não a conta fornecida pela Adobe). Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis com esses destinos de log, mas não com os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

Saiba mais na [documentação sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md).

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
