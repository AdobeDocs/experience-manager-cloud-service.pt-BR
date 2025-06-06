---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 6f4c2a8d6e4d4e67bfd0bd4da68bcef11668b8c5
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 7%

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


A data de lançamento da versão atual (2025.5.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 5 de junho de 2025. O próximo lançamento de recursos (2025.6.0) está planejado para sexta-feira, 26 de junho de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440925?quality=12&captions=por_br)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Metadados gerados pela IA**

O AEM Assets agora usa a [IA para gerar metadados automaticamente, incluindo Título, Descrição e Palavras-chave](/help/assets/metadata-assets-view.md#ai-smart-tags). Esses campos gerados pela IA melhoram a precisão dos metadados, tornando os ativos mais fáceis de pesquisar, categorizar e recomendar. Essa abordagem não só aumenta a eficiência eliminando a marcação manual, mas também garante a consistência e a escalabilidade em grandes volumes de conteúdo digital.

![Metadados gerados pela IA](/help/assets/assets/enhanced-smart-tags.png)

**Integração com o Figma**

O AEM Assets se integra nativamente ao Figma, o que permite que os designers acessem diretamente os ativos armazenados no AEM Assets na interface do usuário do Figma. Você pode colocar conteúdo gerenciado no AEM Assets na tela do Figma e depois salvar conteúdo novo ou editado no repositório do AEM Assets.

![Integração com o Figma](/help/assets/assets/figma-integration.png)


### Novos recursos no Content Hub {#new-features-content-hub}

**Controle de Acesso Baseado em Atributo (ABAC)**

O Content Hub agora permite aplicar restrições baseadas em regras para acessar ativos. As permissões de ativos garantem a governança e também garantem que somente os ativos relevantes estejam acessíveis aos usuários.

As regras de restrição de ativos são baseadas em metadados e, se as condições definidas na regra corresponderem aos metadados do ativo, o ativo será exibido para os grupos de usuários.

Alguns dos principais benefícios do Controle de acesso baseado em atributos incluem:

* Elimina a dependência da estrutura de pastas para permissões

* Permite que os administradores façam upload de ativos e determinem retroativamente as estruturas de permissão

* Reduz o número de duplicatas - melhora a integridade do ativo. São necessárias duplicatas em permissões baseadas em pastas quando os mesmos ativos são compartilhados com grupos diferentes.

**Identidade Visual da Interface**

O Content Hub agora permite que os administradores personalizem a interface do usuário com elementos específicos da marca, incluindo imagens de banner, títulos de banner e texto de corpo, bem como cores primárias e secundárias. Esses aprimoramentos ajudam a garantir a consistência da marca, simplificar a integração do usuário e criar confiança.

![Identidade Visual da Interface](/help/assets/assets/content-hub-ui-branding.png)

**Compartilhamento de link público**

O Content Hub agora oferece suporte à geração de links compartilháveis para permitir que usuários externos, sem acesso a aplicativos, visualizem metadados de ativos ou baixem ativos.

![Identidade Visual da Interface](/help/assets/assets/public-and-private-link.png)

**Governança de coleções**

O Content Hub agora permite controlar o acesso às coleções durante a criação, garantindo que somente usuários autorizados possam visualizar ou gerenciar ativos agrupados. Ele garante maior segurança, melhor colaboração, gerenciamento organizado de ativos e governança simplificada.

![Governança de coleções](/help/assets/assets/collection-permissions.png)

>[!NOTE]
>
>A governança de coleções é um recurso de disponibilidade limitada. Você pode ativá-lo criando um tíquete de suporte.

**Baixar vários ativos como um ZIP**

O Content Hub agora também permite baixar os ativos selecionados e suas representações em um arquivo ZIP, e não como arquivos separados que simplificam o gerenciamento de arquivos para você.

**Representações do Dynamic Media no Content Hub**

Acesse todas as representações predefinidas do Dynamic Media e os recortes inteligentes para download, diretamente na Interface do usuário do Content Hub.

&#x200B;![Representações do Dynamic Media](/help/assets/assets/dm-renditions-content-hub.png)

### Novos recursos no Dynamic Media {#new-features-dynamic-media}

**Integração nativa do Dynamic Media com o AJO B2C&#x200B;**

Integração nativa do Experience Manager (AEM) Dynamic Media com o Journey Optimizer (AJO) B2C, permitindo que os profissionais de marketing incorporem facilmente os ativos do AEM Dynamic Media (representação e modelo DM) ao conteúdo do AJO e entreguem atualizações em tempo real e experiências hiperpersonalizadas em todos os canais.

&#x200B;![Representações do Dynamic Media](/help/assets/assets/dm-ajo-integration.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de pré-lançamento

* [Editor universal - Fragmentos de formulário](/help/edge/docs/forms/universal-editor/creating-form-fragments.md): o Editor universal agora permite criar e reutilizar fragmentos de formulário do Forms adaptável. Esses fragmentos são seções de formulário reutilizáveis (por exemplo, detalhes de contato, campos de consentimento) que podem ser criadas uma vez e aplicadas em vários formulários. Esse recurso simplifica a criação de formulários, garante a consistência e melhora a eficiência da criação.

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

Os recursos de integração entre o Forms e o AEP agora estão disponíveis para os primeiros usuários.

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

Se seu ambiente não pôde ser atualizado devido a dependências sem suporte (consulte [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), você deve ter recebido um email do Adobe com as próximas etapas específicas. Verifique se todas as atualizações necessárias foram concluídas até **28 de agosto de 2025** para que seu ambiente possa ser atualizado sem interrupções.

Observação: a versão de tempo de execução é separada da versão de build do seu código. Embora recomendemos a criação com o Java 21, as builds do Java 11 ainda são compatíveis por enquanto. Um aviso de descontinuação separado para builds do Java 11 será compartilhado no futuro.

### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Conforme observado nas notas de versão de abril, os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **final de agosto**, qualquer substituição de log personalizado sem suporte será ignorada. Com base em nossa análise, a maioria dos clientes não será afetada e a Adobe entrará em contato diretamente com qualquer cliente cuja configuração atual possa ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Limpeza padrão de versões anteriores e logs de auditoria {#mt-defaults}

Atualmente, as versões de conteúdo e logs de auditoria têm suas *tarefas de manutenção de limpeza* associadas desabilitadas por padrão e, portanto, nenhum dado é removido, a menos que seja configurado explicitamente por meio de suas respectivas propriedades OSGi.

No entanto, para otimizar o desempenho do repositório, a partir de **final de junho de 2025**, a limpeza será habilitada por padrão, seguindo estas diretrizes:

#### Versões de conteúdo {#mt-content}

* **Novos ambientes** (criados após uma data futura) (a ser comunicada posteriormente)
   * Versões com mais de **30 dias** serão excluídas periodicamente.
   * As cinco versões mais recentes nos últimos 30 dias são mantidas, juntamente com a versão mais recente e a versão atual, independentemente da idade.

* **Ambientes existentes** (criados antes desta data futura):
   * Versões com mais de **7 anos** serão excluídas periodicamente.
   * Todas as versões nos últimos 7 anos são mantidas.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio de substituições de configuração OSGi.

#### Log de auditoria {#mt-auditlogs}

* **Novos ambientes** (criados após uma data futura, que serão comunicados separadamente):
   * Logs de replicação, DAM e auditoria de página com mais de **7 dias** serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.

* **Ambientes existentes** (criados antes desta data futura):
   * Logs de replicação, DAM e auditoria de página com mais de **7 anos** serão excluídos periodicamente.
   * Todos os eventos são registrados por padrão.
   * Esse alto limite padrão impede a remoção não intencional de dados recentes. No entanto, é recomendável configurar valores mais baixos para otimizar o desempenho do repositório.

* Você pode modificar esses padrões por meio de substituições de configuração OSGi.

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
