---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0.
feature: Release Information
role: Admin
exl-id: b1d25db0-d4a8-4663-b7fe-2d7381e12567
source-git-commit: 76ccdf13f56d7020ef266bc54bebbcc6eff1067d
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 7%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.7.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.7.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.7.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 7 de agosto de 2025. O próximo lançamento de recursos (2025.8.0) está planejado para sexta-feira, 28 de agosto de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no Experience Manager Sites {#enhancements-sites}

* Agora você pode copiar fragmentos de conteúdo com fragmentos referenciados (secundários) em uma operação. Isso permite reutilizar estruturas de fragmento de conteúdo existentes para criar novo conteúdo.
* Na interface do administrador dos fragmentos de conteúdo, agora é possível visualizar o status do fluxo de trabalho para fragmentos de conteúdo, com informações detalhadas sobre fluxos de trabalho anteriores e atuais de um fragmento selecionado.
* Renomear ou mover uma página de origem de live copy agora acionará a republicação de uma página de live copy renomeada ou movida correspondentemente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Adicionar formas aos modelos do Dynamic Media**

Agora você pode [adicionar camadas de forma a modelos do Dynamic Media](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas) no Experience Manager Assets. Semelhante às camadas de imagem e texto, as camadas de forma são compatíveis com parâmetros para atualizações em tempo real por meio da URL do modelo. Também é possível incluir links do call-to-action (CTA) para formas em seus modelos.

![Adicionar formas aos modelos do Dynamic Media](/help/assets/assets/enable-uniform-radius-shape.png)

**Aprimoramentos de metadados gerados por IA**

O AEM Assets agora permite [configurar a exibição de títulos de ativos no modo de exibição Cartão ou em Lista](/help/assets/smart-tags.md#configure-ai-generated-titles) na página Procurar Ativos. Você pode optar por exibir o título do ativo definido por você, o título gerado usando IA ou usar o título gerado por IA somente se não houver um título existente para o ativo.

![Configurar títulos gerados por IA](/help/assets/assets/configure-title-ai-generated.png)

Agora, também é possível optar por desativar os metadados gerados por IA no nível da pasta.

### Novos recursos no Content Hub {#new-features-content-hub}

**Flexibilidade de marca aprimorada no Content Hub**

Com base nos recursos de personalização existentes, o Content Hub agora permite que os administradores personalizem ainda mais sua implantação adicionando imagens de logotipo personalizadas. O suporte para o formato de arquivo do TIFF também foi adicionado para imagens de banner e logotipo, permitindo maior flexibilidade de design.

**Compartilhamento mais inteligente com links denominados**

Agora é possível adicionar um título ao gerar um link compartilhado, seja na exibição de detalhes do ativo ou após selecionar um ou mais ativos. Isso ajuda os recipients a identificar facilmente a finalidade de cada link, especialmente ao receber vários ativos compartilhados.

![link privado e público](/help/assets/assets/shared-link-for-assets.png)

**Navegação de filtro aprimorada**

O Content Hub agora inclui uma opção **Mostrar tudo** nos filtros, permitindo que os usuários visualizem todas as facetas disponíveis junto com as contagens de ativos a partir da limitação atual de visualizar apenas até dez facetas. Os recursos aprimorados de pesquisa e classificação em cada filtro facilitam a descoberta e o gerenciamento de ativos com mais eficiência.

### AEM Desktop App versão 3.0.0 {#desktop-app-release-3.0.0}

Aproveite o upload automatizado de novos arquivos e pastas, as operações aprimoradas de arquivos, a detecção mais inteligente de ativos e a integração perfeita com o AEM — tornando o gerenciamento de conteúdo mais rápido, claro e intuitivo.

Para obter a lista completa de recursos, consulte as [Notas de Versão do Aplicativo de Desktop](https://experienceleague.adobe.com/pt-br/docs/experience-manager-desktop-app/using/release-notes).

### Novos recursos no Dynamic Media com recursos OpenAPI {#new-features-dynamic-media-with-openapi}

**Visualizar ativos antes de publicar**

[!DNL Dynamic Media with OpenAPI capabilities] agora permite a visualização de ativos diretamente nas [!DNL AEM Sites] páginas do autor, antes de torná-los disponíveis publicamente. Compartilhe páginas de visualização com as partes interessadas para coletar feedback sobre a qualidade visual e o ajuste contextual. Durante o ciclo de revisão, é possível criar e gerenciar várias versões de ativos antes de finalizá-los para publicação.

**Imagem inteligente aprimorada para solicitações de imagem OpenAPI**

Todas as solicitações de imagem do OpenAPI agora aproveitam totalmente o Smart Imaging com promoção automática e lógica de fallback. Esse aprimoramento otimiza as imagens com base nas condições do dispositivo e da rede, oferecendo carregamentos de página mais rápidos e uso reduzido da largura de banda — enquanto mantém a qualidade visual.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms {#forms-new-features}

**Editor Universal para Forms Adaptável e Fragmentos de Formulário**

O [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) agora oferece suporte à criação de Fragmentos de formulário adaptáveis e reutilizáveis do Forms. Os autores podem criar formulários visualmente, configurar ações de envio e adicionar a validação do reCAPTCHA, tudo em um ambiente de criação simplificado do WYSIWYG. Esse recurso acelera a criação de formulários, melhora a consistência e melhora a proteção contra spam e abuso automatizado.

![Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**Serviço de envio do Forms para o Edge Delivery Services Forms**

Consulte [Serviço de Envio do Forms](/help/forms/forms-submission-service.md). O permite armazenar dados diretamente de envios do Formulário adaptável em plataformas de planilhas populares, como Google Sheets, Microsoft OneDrive ou SharePoint. Essa integração simplifica o gerenciamento de dados permitindo o envio direto de dados de formulário para a planilha escolhida, eliminando a transferência manual de dados e reduzindo erros.

Os principais benefícios incluem:

* **Integração direta:** configure seus formulários para enviar dados diretamente para uma planilha especificada.
* **Mapeamento de dados personalizado:** Mapeie campos de formulário para colunas de planilha correspondentes para armazenamento organizado.
* **Controle de acesso:** use as permissões de planilha existentes para gerenciar quem pode acessar ou modificar os dados enviados.

**Gerar e sincronizar representações AFP do Forms Adaptável**

A [API de Sincronização de Saída AFP](/help/forms/document-generation-afp-api.md) permite que administradores e usuários gerem a saída AFP (Advanced Function Presentation) do Adaptive Forms e sincronizem a saída com sistemas externos ou locais de armazenamento. O AFP é um formato de documento de alto desempenho otimizado para impressão, geralmente usado em ambientes corporativos de grande escala.

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### Novos recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O Programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Essas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**Editor de Regras para o Editor de Comunicações Interativas**

Crie ações dinâmicas orientadas por dados diretamente nos seus documentos usando uma interface intuitiva do tipo apontar-e-clicar. Defina facilmente a lógica condicional, automatize fluxos de trabalho e personalize o conteúdo sem gravar código.

**CLI do AEM Forms Scaffolder para Componentes Personalizados**

>[!VIDEO](https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms development tool)

Acelere o desenvolvimento do AEM Forms Edge Delivery Services com essa ferramenta de CLI. Gere instantaneamente o código e a fiação necessários para iniciar o desenvolvimento de componentes personalizados — sem chapas metálicas, sem complicações.

**Ferramenta de Integração de API para Dados de Formulário Dinâmicos**

A Ferramenta de integração de API permite que os autores de formulários criem formulários dinâmicos e inteligentes que buscam e preenchem automaticamente dados de APIs REST externas com base nas interações do usuário. Esse recurso de integração sem código transforma formulários estáticos em interfaces responsivas de coleção de dados.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Exibição de nó para gerenciamento de permissões {#node-view}

O AEM apresenta o Gerenciamento de permissões de visualização de nó. A funcionalidade principal permanece a mesma da interface clássica, mas é mais amigável e eficiente. Consulte o [artigo dedicado](/help/security/touch-ui-principal-view.md) para obter mais informações.

### Processo de descontinuação atualizado {#updated-deprecation-process}

A Adobe analisa regularmente recursos, bibliotecas, APIs e configurações para garantir que atendam aos padrões de desempenho, segurança e valor. Quando os recursos do não atenderem mais a esses padrões, eles serão marcados para desativação e o uso deverá parar até uma data de remoção especificada. Até essa data, a Adobe lembrará os clientes sobre notificações por email e ações que precisam ser executadas no Cloud Manager antes de continuar com ou implantar novas builds. Se as ações necessárias não forem executadas, poderá ocorrer uma incapacidade de atualizar para novas versões do AEM, resultando em possíveis impactos em termos de segurança, desempenho, confiabilidade e disponibilidade.

Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md) para obter mais informações.

#### APIs Java obsoletas e configuração OSGi próximas das datas de remoção {#deprecated-near-removals}

Expanda a lista abaixo para visualizar as APIs obsoletas e as configurações de OSGi que não devem mais ser usadas. Para obter detalhes completos, incluindo linhas do tempo de remoção, consulte o artigo sobre descontinuação.

<details>
  <summary>Expandir para ver as descontinuações</summary>

APIs Java:

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

Propriedades OSGi:

* `org.apache.sling.commons.log.LogManager` (todas as propriedades)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Descontinuação do Java 11 Runtime {#java11-runtime-deprecation}

O **Java 11 runtime*- agora está obsoleto, e a maioria dos ambientes já foi atualizada para o &#x200B;** Java 21 runtime** de maior desempenho.

Se seu ambiente não pôde ser atualizado devido a dependências sem suporte (consulte [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), você deve ter recebido um email da Adobe com as próximas etapas específicas. Verifique se todas as atualizações necessárias foram concluídas até **28 de agosto de 2025** para que seu ambiente possa ser atualizado sem interrupções.

Observação: a versão de tempo de execução é separada da versão de build do seu código. Embora recomendemos a criação com o Java 21, as builds do Java 11 ainda são compatíveis por enquanto. Um aviso de descontinuação separado para builds do Java 11 será compartilhado no futuro.

### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Conforme observado nas notas de versão de abril, os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **final de agosto**, qualquer substituição de log personalizado sem suporte será ignorada. Com base em nossa análise, a maioria dos clientes não será afetada e a Adobe entrou em contato com clientes cuja configuração atual pode ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Limpeza padrão de versões anteriores e logs de auditoria {#mt-defaults}

Atualmente, as versões de conteúdo e logs de auditoria têm suas *tarefas de manutenção de limpeza* associadas desabilitadas por padrão e, portanto, nenhum dado é removido, a menos que seja configurado explicitamente.

No entanto, para otimizar o desempenho do repositório, a limpeza será ativada por padrão em uma data futura anunciada.

Para obter mais detalhes, consulte o [artigo sobre Tarefas de manutenção](/help/operations/maintenance.md#defaults).

#### Versões de conteúdo {#mt-content}

* **Novos ambientes** (criados após uma data futura, a ser comunicada posteriormente):
   * As versões com mais de 30 dias serão excluídas periodicamente.
   * As cinco versões mais recentes nos últimos 30 dias são mantidas, juntamente com a versão mais recente e a versão atual, independentemente da idade.

* **Ambientes existentes** (criados antes desta data futura):
   * As versões com mais de 7 anos serão excluídas periodicamente.
   * Todas as versões nos últimos 7 anos são mantidas.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio da configuração YAML, implantada usando o pipeline de configuração.

#### Log de auditoria {#mt-auditlogs}

* **Novos ambientes** (criados após uma data futura, que serão comunicados separadamente):
   * A replicação, o DAM e os logs de auditoria de página com mais de 7 dias serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.

* **Ambientes existentes** (criados antes desta data futura):
   * A replicação, o DAM e os logs de auditoria de página com mais de 7 anos serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio da configuração YAML, implantada usando o pipeline de configuração.

### Computação Edge (Programa Alpha) {#edge-computing}

A computação Edge permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Autenticação de usuários com um provedor de identidade antes de conceder acesso ao conteúdo
* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatar respostas de APIs de terceiros (e talvez agregar várias respostas de APIs) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

### Configuração da CDN para o Edge Delivery Services (programa Beta) {#cdn-eds-beta}

A CDN gerenciada pela Adobe oferece opções de configuração flexíveis, conforme descrito no [artigo sobre Pipeline de configuração](/help/operations/config-pipeline.md#configurations).

Agora em uma versão beta, implante um pipeline de configuração para recursos que incluem seletores de origem de CDN, transformações de resposta e solicitação, encaminhamento de log de CDN e muito mais. Entre em contato com [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) com os detalhes do seu caso de uso.

### Instantâneos para RDEs (Programa Alpha) {#rde-snapshot-beta}

Em alfa, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em fornecer feedback sobre esse recurso.

### Encaminhamento de logs do AEM para mais destinos (programa Beta) {#log-forwarding-beta}

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao encaminhamento de logs do AEM e do CDN para o Armazenamento de Blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Agora na versão beta, você pode encaminhar logs do AEM para o Amazon S3, Sumo Logic, Dynatrace e sua própria conta da New Relic (não a conta fornecida pela Adobe). Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis com esses destinos de log, mas não com os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

Saiba mais na [documentação sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md).

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
