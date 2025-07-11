---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: c8391e09b7e2888423187f48360423c52b18fe0a
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 8%

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

A data de lançamento da versão atual (2025.6.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de junho de 2025. O próximo lançamento de recursos (2025.7.0) está planejado para sexta-feira, 31 de julho de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Gerenciamento aprimorado do formulário de metadados no Assets View**

Agora é possível importar formulários de metadados da Exibição de administração diretamente para a Exibição do Assets. Qualquer atualização feita nesses formulários na exibição do Assets reflete automaticamente na exibição do Administrador, garantindo a consistência em ambas as experiências. Esse recurso oferece suporte a uma transição contínua para a nova visualização do Assets, mantendo a continuidade com as configurações de metadados existentes.

![Metadados gerados pela IA](/help/assets/assets/import-metadata-forms-page.png)

### Novos recursos no Content Hub {#new-features-content-hub}

**Governança de coleções**

O Content Hub agora permite [controlar o acesso às coleções durante a criação, garantindo que somente usuários autorizados possam exibir ou gerenciar ativos agrupados](/help/assets/collections-content-hub.md##create-collections). Ele garante maior segurança, melhor colaboração, gerenciamento organizado de ativos e governança simplificada.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [Editor Universal para Forms Forms Adaptável e Fragmentos de Formulário](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): o Editor Universal agora oferece suporte à criação de Fragmentos de Formulário Adaptáveis e Reutilizáveis. Os autores podem criar formulários visualmente, configurar ações de envio e adicionar a validação do reCAPTCHA, tudo em um ambiente de criação simplificado do WYSIWYG. Esse recurso acelera a criação de formulários, melhora a consistência e melhora a proteção contra spam e abuso automatizado.

### Recursos de pré-lançamento

* [Gerar e Sincronizar representações AFP do Forms Adaptive](/help/forms/document-generation-afp-api.md): a API de Sincronização de Saída AFP permite que administradores e usuários gerem a saída AFP (Advanced Function Presentation) do Forms Adaptive e sincronizem a saída com sistemas externos ou locais de armazenamento. O AFP é um formato de documento de alto desempenho otimizado para impressão, geralmente usado em ambientes corporativos de grande escala.

* [Biblioteca de documentos do SharePoint - Salvar anexos com nomes de arquivo originais](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): agora há a opção de salvar anexos de formulário usando seus nomes de arquivo originais ao armazená-los em uma Biblioteca de Documentos do SharePoint. Esse aprimoramento simplifica a identificação e o gerenciamento de arquivos carregados.

* **Editor de regras**:
   * [Condição Binária com Evento de Clique na Cláusula &quot;When&quot;](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): o Editor de Regras agora permite combinar um evento de clique de botão (_É Clicado_) com outras condições na cláusula &quot;When&quot;. Isso permite um controle mais preciso sobre a execução da regra com base na interação do usuário e outros fatores. Observação: ao usar várias condições, o evento de clique deve ser a primeira condição listada.
   * [Condições de Validação para Campos e Painéis](/help/forms/rule-editor-core-components-usecases.md): o Editor de Regras agora inclui condições _IsValid_ e _IsNotValid_. Isso permite verificar o status de validação de campos específicos ou painéis inteiros (incluindo layouts como Guias horizontais, Guias verticais, Acordeões e Assistentes), facilitando a navegação aprimorada do formulário e a experiência do usuário com base nos resultados da validação.
* [Gerenciamento de Escopo aprimorado para Listas do SharePoint](/help/forms/connect-forms-to-sharepoint-list.md): os sites do SharePoint agora oferecem suporte a todos os caminhos gerenciados, por exemplo, /sites e /team. Esse aprimoramento permite uma integração mais ampla em várias estruturas de site do SharePoint, oferecendo maior flexibilidade na conexão com o conteúdo organizacional.
* [Suporte para Salvar Documento de Registro na Lista do SharePoint](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): o Forms criado usando um Modelo de Dados de Formulário (FDM) baseado em Lista do SharePoint agora pode salvar o Documento de Registro (DoR) nas Listas do SharePoint configurando a propriedade do campo Documento de Referência de Associação de Registro. Esse aprimoramento permite a integração perfeita de dados e documentos de formulário compatíveis com o armazenamento da SharePoint.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Integração do Adobe Experience Platform (AEP) com o Forms

* [Integração do AEM Forms com o Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md): o AEM Forms ao Adobe Experience Platform Connector permite a integração perfeita entre o Adaptive Forms e o Adobe Experience Platform. Esse recurso permite que os dados do formulário sejam mapeados para esquemas XDM e enviados diretamente para a AEP em tempo real. Ele simplifica a captura de dados para casos de uso de personalização e ativação em soluções da Adobe Experience Cloud.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

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

O **Java 11 runtime** agora está obsoleto, e a maioria dos ambientes já foi atualizada para o **Java 21 runtime** mais eficiente.

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

No entanto, para otimizar o desempenho do repositório, a partir de **início de julho de 2025**, a limpeza será habilitada por padrão, seguindo estas diretrizes:

#### Versões de conteúdo {#mt-content}

* **Novos ambientes** (criados após uma data futura) (a ser comunicada posteriormente)
   * Versões com mais de **30 dias** serão excluídas periodicamente.
   * As cinco versões mais recentes nos últimos 30 dias são mantidas, juntamente com a versão mais recente e a versão atual, independentemente da idade.

* **Ambientes existentes** (criados antes desta data futura):
   * Versões com mais de **7 anos** serão excluídas periodicamente.
   * Todas as versões nos últimos 7 anos são mantidas.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio da configuração YAML, implantada usando o pipeline de configuração.

#### Log de auditoria {#mt-auditlogs}

* **Novos ambientes** (criados após uma data futura, que serão comunicados separadamente):
   * Logs de replicação, DAM e auditoria de página com mais de **7 dias** serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.

* **Ambientes existentes** (criados antes desta data futura):
   * Logs de replicação, DAM e auditoria de página com mais de **7 anos** serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio da configuração YAML, implantada usando o pipeline de configuração.

Para obter mais detalhes, consulte o [artigo sobre Tarefas de manutenção](/help/operations/maintenance.md#defaults).

### Computação Edge (Programa Alpha) {#edge-computing}

A computação Edge permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Autenticação de usuários com um provedor de identidade antes de conceder acesso ao conteúdo
* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatar respostas de APIs de terceiros (e talvez agregar várias respostas de APIs) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

### Configuração da CDN para o Edge Delivery Services (programa Beta) {#cdn-eds-beta}

A CDN gerenciada pela Adobe oferece opções de configuração flexíveis, conforme descrito no [artigo sobre Pipeline de configuração](/help/operations/config-pipeline.md#configurations).

Agora em uma versão beta, implante um pipeline de configuração para recursos que incluem seletores de origem CDN, transformações de resposta e solicitação e muito mais. Entre em contato com [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) com os detalhes do seu caso de uso.

### Encaminhamento de logs do AEM para mais destinos (programa Beta) {#log-forwarding-beta}

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao encaminhamento de logs do AEM e do CDN para o Armazenamento de Blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Agora na versão beta, você pode encaminhar logs do AEM para o Amazon S3, o Sumo Logic e sua própria conta da New Relic (não a conta fornecida pela Adobe). Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis com esses destinos de log, mas não com os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

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
