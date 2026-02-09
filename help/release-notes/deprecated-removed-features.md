---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para recursos obsoletos e removidos do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
mini-toc-levels: 1
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 910876ef77698680266a2ef99cd5650b0adbd1ac
workflow-type: tm+mt
source-wordcount: '3695'
ht-degree: 30%

---

# Recursos e APIs obsoletos e removidos {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Recursos obsoletos e removidos do AEM as a Cloud Service"
>abstract="O AEM as a Cloud Service tem um modelo de implantação nativo em nuvem. Essa guia destaca as funcionalidades e os recursos substituídos por seus equivalentes nativos da nuvem."

A Adobe analisa regularmente os recursos, incluindo APIs e configurações, para garantir que eles atendam aos padrões em evolução de desempenho, segurança e valor geral do AEM as a Cloud Service. Com base nessas avaliações, certos recursos podem ser marcados para desativação. Quando viável, a Adobe fornecerá uma substituição adequada.

Quando uma descontinuação for anunciada, o recurso permanecerá disponível somente por um período limitado e os clientes deverão remover todo o uso antes de qualquer data de remoção especificada. A Adobe fornecerá aviso e orientação razoáveis para oferecer suporte a uma transição tranquila.

Durante a janela de tempo de desativação, a Adobe lembrará os clientes das ações que precisam tomar para sair do uso de um recurso por meio de notificações por email, alertas da Central de ações ou lembretes no Cloud Manager.

>[!WARNING]
>
>Em alguns casos, a remoção de um recurso pode ser necessária antes da implantação de uma nova build do Cloud Manager ou da atualização para a versão mais recente do AEM as a Cloud Service.

>[!IMPORTANT]
>
>Várias [APIs obsoletas](#aem-apis) estão direcionando a remoção em **26 de fevereiro de 2026**. Revise estas datas e impactos principais:
>
>* **A partir de 26 de janeiro de 2026**: os emails de notificação da Central de Ações são enviados **semanalmente por ambiente** como um lembrete para remover o uso dessas APIs.
>* **26 de fevereiro de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **pausarão** durante a etapa **Qualidade do Código**. Um Gerente de implantação, Gerente de projeto ou Proprietário da empresa pode substituir o problema para permitir que o pipeline continue.
>* **26 de março de 2026**: os pipelines de Cloud Manager que contêm código usando essas APIs **falharão** durante a etapa **Qualidade do Código**, **bloqueando implantações** de novos códigos até que o uso seja removido.
>* **30 de abril de 2026**: os ambientes que ainda usam essas APIs podem **não receber mais atualizações críticas de versões do Adobe**.
>
>Para evitar bloqueios de implantação, remova o uso da API antes de 26 de março de 2026.

## Funcionalidade obsoleta {#deprecated-features}

A funcionalidade na tabela abaixo foi anunciada como obsoleta, mas ainda não foi removida.  O uso da funcionalidade deve cessar antes da data de remoção do público alvo ou você corre o risco de ter problemas relacionados a desempenho, disponibilidade e segurança.

| Recursos | Recurso obsoleto | Substituição |
| ------------ | ------------------ | ----------- |
| Sites | [Suporte a Fragmento de Conteúdo na API HTTP do Assets](/help/assets/content-fragments/assets-api-content-fragments.md) | [Entrega de fragmento de conteúdo com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)<br>em conjunto com<br> [OpenAPIs de gerenciamento de fragmentos de conteúdo e modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md) |
| Sites | [Recursos do PWA](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | Nenhum |
| Sites | [Editor SPA](/help/implementing/developing/hybrid/introduction.md) | Os editores preferidos para gerenciar conteúdo headless no AEM são:<br>- [O editor universal](https://www.aem.live/docs/aem-authoring) para edição visual.<br>- [O editor de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md) para editar com base em formulários. |
| [!DNL Sites] | [API de uso do JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [API de uso do Java](https://experienceleague.adobe.com/pt-br/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | Propriedades dos Fragmentos de experiência para **Status da rede social**. | A remoção do recurso está prevista para breve. |
| Sites | [Automação da Instalação do Experience Cloud](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | Nenhum |
| [!DNL Sites] | Fragmentos de conteúdo simples baseados em modelo. | [Fragmentos de conteúdo estruturado com base em modelo](/help/assets/content-fragments/content-fragments-models.md) agora. |
| [!DNL Assets] | fluxo de trabalho `DAM Asset Update` para processar imagens ingeridas. | A ingestão de ativos usa [microsserviços de ativos](/help/assets/asset-microservices-overview.md) agora. |
| [!DNL Assets] | Carregar ativos diretamente no [!DNL Experience Manager]. Consulte [APIs de carregamento de ativos obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Use [Upload binário direto](/help/assets/add-assets.md). Para obter detalhes técnicos, consulte [APIs de upload direto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Determinadas etapas do fluxo de trabalho](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` não são compatíveis, incluindo a chamada de ferramentas de linha de comando, como o [!DNL ImageMagick]. | Os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) oferecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodificação FFmpeg de vídeos. | Para gerar miniaturas do FFmpeg, use os [Microserviços de ativos](/help/assets/asset-microservices-overview.md). Para a transcodificação FFmpeg, use o [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interface de replicação em árvore na guia &quot;Distribuir&quot; dos agentes de replicação (remoção após 30 de setembro de 2021) | [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Etapa do Fluxo de Trabalho de Ativação da Árvore](/help/operations/replication.md#tree-activation) se aproxima. |
| [!DNL Foundation] | A guia Distribuir da tela do administrador do agente de replicação e a API de replicação não podem replicar pacotes de conteúdo maiores que 10 MB. | [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [Etapa do Fluxo de Trabalho de Ativação da Árvore](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | As integrações que usam credenciais geradas de projetos da Adobe Developer Console estão perdendo gradualmente o suporte às credenciais da Conta de serviço (JWT). A partir de 1º de maio de 2024, novas credenciais de Conta de serviço (JWT) não poderão ser criadas no Adobe Developer Console. As credenciais da Conta de serviço (JWT) existentes permanecem utilizáveis para integrações configuradas até 1º de janeiro de 2025, quando param de funcionar, exigindo que os clientes migrem para as credenciais de servidor para servidor do OAuth. [Saiba mais](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrar](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview) para credenciais OAuth de servidor para servidor. |
| [!DNL Foundation] | Fluxo de trabalho da árvore de conteúdo de publicação e a etapa relacionada do Fluxo de trabalho da árvore de conteúdo de publicação, que foi usada para replicações de hierarquias de conteúdo. | Use a [Etapa ](/help/operations/replication.md#tree-activation) do Fluxo de Trabalho de Ativação da Árvore, que tem melhor desempenho. |
| [!DNL Foundation] | Utilização da interface do usuário do para compactar/minificar bibliotecas de clientes do JavaScript. A Adobe não planeja atualizar ainda mais a biblioteca YUI. | A Adobe recomenda que os clientes mudem para o Google Closure Compiler (GCC) para sua implementação. |
| [!DNL Foundation] | Suporte para com.adobe.granite.oauth.server | Integração do Adobe IMS |

## Funcionalidade removida {#removed-features}

Esta seção lista as funcionalidades que foram removidas.

| Área | Destaque | Substituição | Data definida para remoção |
| ------------ | ------------------ | ----------- | ------------------- |
| Interface do usuário | A interface clássica é removida da interface do usuário do produto. Algumas caixas de diálogo da interface clássica estão disponíveis para alguns recursos selecionados, como o Verificador de links, a Limpeza de versão e algumas configurações do Cloud Service. As próximas [atualizações do produto](/help/release-notes/home.md) podem remover ainda mais a disponibilidade da interface clássica. | Interface do usuário padrão | Removido |
| [!DNL Dynamic Media] | As integrações anteriores com o [Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) e o [Dynamic Media Hybrid mode](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic) não estão disponíveis no [!DNL Experience Manager] as a [!DNL Cloud Service]. | Use o [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornecido com o [!DNL Experience Manager] as a [!DNL Cloud Service]. | Removido |
| [!DNL Sites] | Portal Director e Portlet Component | Estes recursos foram descontinuados no [!DNL Experience Manager] 6.4 e agora foram removidos do [!DNL Experience Manager]. | Removido |
| [!DNL Sites] | Importador de design | Este recurso foi removido porque as seções imutáveis do repositório do [!DNL Experience Manager] não estão acessíveis no tempo de execução. | Removido |
| [!DNL Assets] | O compartilhamento do [!DNL Assets] com os serviços Assets Core Service e Creative Cloud não está disponível. | Para integração com a [!DNL Adobe Creative Cloud], use o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html). | Removido |
| [!DNL Foundation] | Suporte para fontes de dados do Apache Sling (pacote OSGi org.apache.sling.datasource) | N/A | Removido |
| [!DNL Foundation] | Suporte para modelos de script JST (pacote OSGi org.apache.sling.scripting.jst) | N/A | Removido |
| [!DNL Foundation] | Suporte para o quadro de permissões Apache Felix Http | OSGi Http Whiteboard | Março de 2022 |
| [!DNL Foundation] | Suporte para o recurso org.apache.sling.serviceusermapping para [obter a ID de usuário do serviço](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | N/A | 30/08/24 |
| [!DNL Foundation] | O tempo de execução do Java 11 está obsoleto e foi substituído pelo Adobe com o tempo de execução do Java 21. Observe que é aceitável que o código ainda seja criado com o Java 11 (Java 17 e 21 são as outras opções) | O tempo de execução do Java 21 é aplicado. Para garantir a compatibilidade, é essencial atualizar as versões da biblioteca conforme descrito nos [Requisitos de tempo de execução](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) | 29/05/25 de março |

## APIs obsoletas {#aem-apis}

As APIs na tabela abaixo (clique para expandir e ver) foram anunciadas como obsoletas, mas ainda não foram removidas.  O uso dessas APIs deve terminar antes da data de remoção do público-alvo, caso contrário você corre o risco de ter problemas relacionados a desempenho, disponibilidade e segurança. Algumas APIs fazem referência à seção Diretrizes de remoção de API abaixo.

>[!IMPORTANT]
> Várias APIs estão agendadas para remoção em **26 de fevereiro de 2026**. Revise estas datas e impactos principais:
>
> * **A partir de 26 de janeiro de 2026**: os emails de notificação da Central de Ações são enviados **semanalmente por ambiente** como um lembrete para remover o uso dessas APIs.
> * **26 de fevereiro de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **pausarão** durante a etapa **Qualidade do Código**. Um Gerente de implantação, Gerente de projeto ou Proprietário da empresa pode substituir o problema para permitir que o pipeline continue.
> * **26 de março de 2026**: os pipelines de Cloud Manager que contêm código usando essas APIs **falharão** durante a etapa **Qualidade do Código**, **bloqueando implantações** de novos códigos até que o uso seja removido.
> * **30 de abril de 2026**: os ambientes que ainda usam essas APIs podem **não receber mais atualizações críticas de versões do Adobe**.
>
> Para evitar bloqueios de implantação, remova o uso da API antes de 26 de março de 2026.


<details>
  <summary>Expanda para ver a lista de APIs obsoletas.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Pacote/Classe</th>
    <th>Comentários</th>
    <th>Data de descontinuidade</th>
    <th>Data definida para remoção</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>Use as interfaces Auth Core/Auth Core SPI do Sling como alternativa. <a href="#org.apache.sling.commons.auth">Consulte as notas de remoção abaixo.</a></td>
    <td>2015</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>Os pacotes Eclipse Jetty e Felix Http Jetty não são mais suportados. <a href="#org.eclipse.jetty">Consulte as notas de remoção abaixo.</a></td>
    <td>27/05/2021</td>
    <td>26/02/2026</td>
  </tr>
 <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>O uso dessa API não é compatível com o AEM as a Cloud Service. <a href="#com.mongodb">Consulte as notas de remoção abaixo.</a></td>
    <td>27/05/2021</td>
    <td>26/02/2026</td>
  </tr>
   <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Esta API está obsoleta porque o Apache Abdera é um projeto inativo desde 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte as notas de remoção abaixo.</a></td>
    <td>29/07/2021</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Esta API está obsoleta porque o Apache Abdera é um projeto inativo desde 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte as notas de remoção abaixo.</a></td>
    <td>08/04/2019</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>O quadro de permissões Apache Felix Http não é mais suportado. Migre seu código para o OSGi Http Whiteboard. <a href="#org.apache.felix.http.whiteboard">Consulte as notas de remoção abaixo.</a></td>
    <td>27/01/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Essa API está obsoleta. Migre seu código para as APIs XML fornecidas pelo JDK.</td>
    <td>27/01/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>O AEM as a Cloud Service não oferece suporte a essa API de log back interna. <a href="#ch.qos.logback">Consulte as notas de remoção abaixo.</a></td>
    <td>27/01/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>O AEM as a Cloud Service não é compatível com essa API de log4j interna. <a href="#org.slf4j">Consulte as notas de remoção abaixo.</a></td>
    <td>27/01/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>O Apache Log4j 1 chegou ao fim da vida útil em 2015 e não é mais compatível. <a href="#org.apache.log4j">Consulte as notas de remoção abaixo.</a></td>
    <td>27/01/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>  <td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>As bibliotecas principais do Google Guava estão obsoletas no Cloud Service. <a href="#com.google.common">Consulte as notas de remoção abaixo.</a></td>
    <td>15/05/2023</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>O AEM as a Cloud Service não é compatível com essa API slf4j interna. <a href="#org.slf4j">Consulte as notas de remoção abaixo.</a></td>
    <td>11/04/2022</td>
    <td>26/02/2026</td>
  </tr>
    <tr>
    <td>com.drew.*</td>
    <td>A extração de metadados de imagens e vídeos deve ser feita via Asset Compute no Cloud Service ou via Apache POI ou Apache Tika.</td>
    <td>17/09/2024</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td>Essa API é somente para uso interno.</td>
    <td>23/09/2024</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>Essa API é somente para uso interno.</td>
    <td>23/09/2024</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
<td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>O Felix web console não é suportado em ambientes em nuvem. <a href="#org.apache.felix.webconsole">Consulte as notas de remoção abaixo.</a></td>
    <td>30/04/2021</td>
    <td>26/02/2026</td>
  </tr>
<td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>O uso desta API não é compatível com o AEM as a Cloud Service.</td>
    <td>31/10/2022</td>
    <td>26/02/2026</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>A ser definido</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>Recomenda-se a implementação e o uso do Apache Johnzon do <a href="https://johnzon.apache.org/index.html">javax.json</a>. </td>
    <td>30/04/2021</td>
    <td>A ser definido</td>
  </tr>
  <tr>
<td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>O Commons Lang 2 está em modo de manutenção. O Commons Lang 3 deve ser usado em seu lugar. <a href="#apache.commons">Consulte as notas de remoção abaixo.</a></td>
    <td>30/04/2021</td>
    <td>A ser definido</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>O Commons Collections 3 está em modo de manutenção. O Commons Collections 4 deve ser usado em seu lugar. <a href="#apache.commons">Consulte as notas de remoção abaixo.</a></td>
    <td>30/04/2021</td>
    <td>A ser definido</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Essa API está obsoleta. Em vez disso, use os Construtores do Apache Sling.</td>
    <td>31/10/2022</td>
    <td>A ser definido</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>O AEM as a Cloud Service não é compatível com essa API.</td>
    <td>15/05/2023</td>
    <td>A ser definido</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>Em vez disso, use org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>A ser definido</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>Em vez disso, use org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>A ser definido</td>
  </tr>
  </tbody>
</table>
</details>

## APIs removidas {#removed-apis}

Esta seção lista APIs que foram descontinuadas e removidas. Algumas APIs fazem referência à seção Diretrizes de remoção de API abaixo.

<details>
  <summary>Expanda para ver a lista de APIs removidas.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Pacote/Classe</th>
    <th>Comentários</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>O uso da Sling's Discovery API é uma alternativa</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Os gerenciadores de persistência personalizados não são compatíveis com o AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>É recomendado que use a API Apache Felix HealthCheck em seu lugar</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Os pacotes Eclipse Jetty e Felix Http Jetty não são mais suportados.</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>O metatipo Apache Felix e as APIs SCR estão obsoletos.  Em vez disso, use o metatipo OSGi e as APIs de Serviço Declarativo.</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>As classes de implementação de logs não são compatíveis com o AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>Legacy AEM 6.x API.</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Esta API não é suportada no Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>As classes de utilitários relacionadas ao Apache Xerces estão removidas nas versões subsequentes, causando uma alteração importante da versão. Como esses utilitários são para uso interno no File vault, a API está ficando obsoleta da superfície pública da API.</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>API herdada do AEM 6.x. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte as notas de remoção abaixo.</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>O AEM as a Cloud Service não oferece suporte a essa API de log back interna.</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>É necessário atualizar o Handlebars da versão 4.0.5 para a 4.3.0, devido a uma vulnerabilidade de segurança. Este pacote não está mais presente no Handlebars atualizado.</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Essa API não é mais aceita. Em vez disso, use org.apache.sling.api.resource.ResourceResolverFactory.</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>O uso desta API não é compatível com o AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>Essa API é somente para uso interno.</td>
  </tr>
</tbody>
</table>
</details>

## Diretrizes de remoção da API {#api-removal-guidance}

Esta seção reflete a orientação de remoção de APIs para várias APIs nas tabelas acima.

Para identificar quais APIs Java obsoletas seu código está usando, integre o [Plug-in Maven do AEM as a Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) ao seu projeto Maven e execute-o localmente. O relatório lista todos os usos de API obsoletos detectados e indica qual pacote OSGi está fazendo referência a cada API.

Embora você deva corrigir todas as APIs obsoletas ao longo do tempo, priorize quaisquer APIs listadas na tabela API obsoleta com uma data de remoção do Target de 26 de fevereiro de 2026 (ou anterior). No relatório do AEM Analyzer, essas APIs podem aparecer com uma data de remoção efetiva em 31/8/2025.

Depois de atualizar o código, verifique se nenhum uso de API obsoleto permanece no Cloud Manager verificando os resultados da etapa de qualidade do código.

### Diretrizes gerais

Se você usar uma biblioteca de terceiros que atualmente requer a API obsoleta, tente atualizar para uma versão mais recente dessa biblioteca de terceiros.

Se você estiver usando o ACS AEM Commons, use pelo menos a versão 6.11.0 (recomenda-se a versão mais recente) e certifique-se de [incluir a versão para Cloud Service](https://adobe-consulting-services.github.io/acs-aem-commons/pages/maven.html) especificando o classificador `cloud` para o pacote de conteúdo.

Se a importação de uma API obsoleta estiver marcada como `optional`, você ainda deverá tentar removê-la. No entanto, esse uso opcional não bloqueará as implantações. Mas sua implantação pode ser afetada, uma vez que a importação opcional não é mais satisfeita.

### Remoção de `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

Se você estiver usando o `org.apache.sling.commons.auth`, o `org.apache.sling.commons.auth.spi` ou ambos, o uso poderá ser substituído por meio da migração do código para o `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`. Se você estiver usando uma versão antiga do [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), atualize para a versão mais recente.

Lista de ações:

* Atualizar o ACS AEM Commons para a versão mais recente (pelo menos 6.11.0)
* Migrar de `org.apache.sling.commons.auth` e/ou `org.apache.sling.commons.auth.spi` para `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`.

### Remoção de `org.apache.felix.webconsole*` {#org.apache.felix.webconsole}

Se você estiver usando pacotes de `org.apache.felix.webconsole*`, remova este código do seu projeto. O console da Web não está acessível no Cloud Service.

Lista de ações:

* Remover código usando pacotes de `org.apache.felix.webconsole*`

### Remoção de `org.eclipse.jetty*` {#org.eclipse.jetty}

Se você usar qualquer item do pacote `org.eclipse.jetty` ou de um de seus pacotes secundários, talvez queira migrar para outras bibliotecas de terceiros com uma funcionalidade semelhante. Se a migração não for viável, adicione os pacotes necessários da lista abaixo ao seu projeto.

Lista de ações:

* Substitua o uso de `org.eclipse.jetty` pacotes por outro código próprio/bibliotecas de terceiros ou
* Selecione os pacotes necessários nesta lista e adicione-os ao seu projeto:
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### Remoção de `com.mongodb` {#com.mongodb}

Adicione a API do cliente Mongo ao seu projeto.

Lista de ações:

* Adicionar este pacote ao seu projeto
   * `org.mongodb:mongo-java-driver:3.12.7`

Você pode escolher uma versão diferente, dependendo de suas necessidades.

### Remoção de `com.google.common*` {#com.google.common}

Remova o uso das bibliotecas principais do Google Guava ou inclua uma versão apropriada em seu projeto. Em muitos casos, o uso dessa biblioteca pode ser substituído por classes de coleção do JDK ou Apache Commons Collections4. Se você não encontrar nenhuma substituição, inclua a versão mais recente da Biblioteca principal do Google Guave no seu projeto. Se você estiver usando uma versão antiga do [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), atualize para a versão mais recente.

Lista de ações:

* Atualizar o ACS AEM Commons para a versão mais recente (pelo menos 6.11.0)
* Substituir o uso da biblioteca principal do Google Guava por coleções JDK ou coleções Apache Commons4
* Se ainda for necessário, adicione este pacote ao seu projeto (substitua a versão pela mais recente disponível):
   * `com.google.guava:guava:33.4.8-jre`

### Remoção de `Apache Commons Lang 2 and Apache Commons Collections 3` {#apache.commons}

Remova o uso das bibliotecas não mantidas do Apache Commons e substitua-as pelo uso das versões de suporte. Na maioria dos casos, é necessário apenas ajustar as importações de pacote. Somente em alguns casos, as classes ou os métodos foram renomeados. Se você estiver usando uma versão antiga do [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), atualize para a versão mais recente.

Lista de ações:

* Atualizar o ACS AEM Commons para a versão mais recente (pelo menos 6.11.0)
* Substituir importações de `org.apache.commons.lang*` por `org.apache.commons.lang3`
* Substituir importações de `org.apache.commons.collections*` por `org.apache.commons.collecitons4`

### Uso de `org.apache.abdera*` e `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

Substitua o uso de qualquer pacote de `org.apache.abdera` e `org.apache.sling.atom.taglib` por uma biblioteca de terceiros que forneça funcionalidade semelhante ou seu próprio código.

Lista de ações:

* Substituir o uso de pacotes de `org.apache.abdera` e `org.apache.sling.atom.taglib` por outro código próprio/bibliotecas de terceiros.

### Uso do `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

Substitua o uso de `org.apache.felix.http.whiteboard` pelo [Quadro de permissões OSGi Http](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html). A API OSGi oficial tem recursos semelhantes e, na maioria das vezes, a substituição requer apenas a alteração das propriedades de registro do serviço.

Lista de ações:

* Substituir o uso de `org.apache.felix.http.whiteboard` pelo [Quadro de permissões OSGi Http](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

### Uso do `ch.qos.logback*` {#ch.qos.logback}

O logback não é compatível com o Cloud Service. Remova todo o uso. Se você estiver usando uma versão antiga do [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), atualize para a versão mais recente.

Lista de ações:

* Atualizar o ACS AEM Commons para a versão mais recente (pelo menos 6.11.0)
* Remover o código usando pacotes de `ch.qos.logback`

### Uso do `org.slf4j.event and org.slf4j.spi` {#org.slf4j}

Se você estiver usando `org.slf4j.event` ou `org.slf4j.spi`, remova todo o uso dele. Se você estiver usando uma versão antiga do [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), atualize para a versão mais recente.

Lista de ações:

* Atualizar o ACS AEM Commons para a versão mais recente (pelo menos 6.11.0)
* Remover o código usando `org.slf4j.event` e `org.slf4j.spi`
* Se você estiver usando o Cliente Apache Kafka e incluir o pacote do invólucro OSGi do Apache ServiceMix (`org.apache.servicemix.bundles.kafka-clients`), substitua-o pelo [AEM Apache Kafka Client Wrapper](https://repo.maven.apache.org/maven2/com/adobe/aem/osgi/com.adobe.aem.osgi.kafka-clients/4.0.0_1.0/). Essa é a mesma versão que a do Apache ServiceMix com apenas o uso desses dois pacotes removidos.

### Uso do `org.apache.log4j` {#org.apache.log4j}

Se você estiver usando a opção `org.apache.log4j` para SLF4J (`org.slf4j`) ou Log4J 2.x (`org.apache.logging.log4j`).

Lista de ações:

* Substituir o uso de `org.apache.log4j` por `org.slf4j` (recomendado) ou `org.apache.logging.log4j`

## Configuração OSGI {#osgi-configuration}

As seções abaixo refletem a superfície de configuração OSGi do AEM as a Cloud Service, descrevendo o que os clientes podem configurar.

1. O código do cliente não deve definir as configurações OSGi listadas.
1. Uma lista de configurações OSGi cujas propriedades podem ser configuradas, mas devem obedecer às regras de validação indicadas. Essas regras incluem se a declaração da propriedade é obrigatória, seu tipo e, em alguns casos, seu intervalo permitido de valores.

O código do cliente pode configurar qualquer configuração OSGi não listada.

Essas regras são validadas durante o processo de criação do Cloud Manager. Regras adicionais podem ser adicionadas ao longo do tempo e a data de aplicação esperada é anotada na tabela. Espera-se que os clientes cumpram essas regras até a data de aplicação prevista. O não cumprimento das regras após a data de remoção gera erros no processo de criação do Cloud Manager. Os projetos Maven devem incluir o [Plug-in Maven do AEM as a Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) para sinalizar erros de configuração OSGI durante o desenvolvimento local do SDK.

Informações adicionais sobre a configuração OSGI podem ser encontradas em [este local](/help/implementing/deploying/configuring-osgi.md).

### Propriedades OSGi obsoletas (não poderão ser modificadas em breve) {#deprecated-unmodifiable-osgi-properties}

As propriedades para os seguintes PIDs de componente OSGi estão obsoletos e o uso deve ser interrompido na data de imposição.

| **ID do componente OSGI** | **Propriedades Não Modificáveis** | **Descontinuação** | **Imposição** |
|---|---|---|---|
| **`org.apache.sling.commons.log.LogManager`** | todas | 24/04/25 | 31/08/25 (configuração ignorada em junho) |
| **`org.apache.sling.commons.log.LogManager.factory.config`** | org.apache.sling.commons.log.file, org.apache.sling.commons.log.pattern | 24/04/25 | 31/08/25 (configuração ignorada em junho) |
| **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** | todas | 2024 | 31/08/25 |
| **`com.adobe.granite.toggle.impl.dev.DynamicToggleProviderImpl`** | todas | 03/06/25 | 31/08/25 |
| **`org.apache.http.proxyconfigurator`** | todas | 03/06/25 | 31/08/25 |

### Configurações OSGi não modificáveis {#unmodifiable-osgi-properties}

As propriedades para os seguintes PIDs de componente OSGi não podem ser modificadas, portanto, não devem ser configuradas.

| **ID do componente OSGI** | **Propriedades Não Modificáveis** |
|---|---|
| **`com.day.cq.auth.impl.cug.CugSupportImpl`** |  |
| **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** | todas |
| **`com.adobe.granite.toggle.impl.ToggleRouterImpl`** | todas |
| **`org.apache.sling.engine.impl.log.RequestLoggerFilter`** | todas |
| **`org.apache.sling.feature.apiregions.impl`** | todas |
| **`org.apache.sling.jcr.resource.internal.helper.jcr.BinaryDownloadUriProvider`** | todas |
| **`com.adobe.cq.unifiedshell.impl.discovery.DiscoveryServlet`** | todas |
| **`com.adobe.cq.unifiedshell.impl.ui.FrameErrorHandler`** | todas |
| **`com.adobe.cq.unifiedshell.impl.config.UnifiedShellConfService`** | todas |
| **`com.adobe.cq.unifiedshell.impl.config.RepositoryIdentifier`** | todas |
| **`org.apache.sling.feature.apiregions.factory`** | todas |
| **`com.adobe.granite.toggle.monitor.systemproperty`** | todas |


### Restrições futuras de propriedade OSGi impostas {#future-restrictions-osgi-properties}

No futuro, o Adobe aplicará as seguintes restrições de propriedades OSGi. Para os PIDs mencionados, somente as propriedades listadas podem ser configuradas.

| PID do componente OSGi |   | Obrigatório | Tipo | Restrição (se aplicável) |
|---|---|---|---|---|
| `com.day.cq.mailer.DefaultMailService` | `smtp.host` |   | string |   |
|   | `smtp.port` | Sim | inteiro | &quot;465&quot;, &quot;587&quot; ou &quot;25&quot; |
|   | `smtp.user` |   | string |   |
|   | `smtp.password` |   | string |   |
|   | `from.address` |   | string |   |
|   | `smtp.ssl` |   | string |   |
|   | `smtp.starttls` |   | booleano |   |
|   | `smtp.requiretls` |   | booleano |   |
|   | `debug.email` |   | booleano |   |
|   | `oauth.flow` |   | booleano |   |
| `org.apache.sling.commons.log.LogManager.factory.config` | `org.apache.sling.commons.log.level` | Sim | string | &quot;INFO&quot;, &quot;DEBUG&quot; ou &quot;TRACE&quot; |
|   | `org.apache.sling.commons.log.names` |   | matriz de strings |   |
|   | `org.apache.sling.commons.log.additiv` |   | booleano |   |
| `com.day.cq.commons.impl.ExternalizerImpl` | `externalizer.domains` | Não | cadeia de caracteres[] |   |
|   | `externalizer.encodedpath` | Não | booleano |   |
|   | `externalizer.host` | Não | string |   |
|   | `externalizer.contextpath` | Não | string |   |

### Restrições de propriedade OSGi {#restrictions-osgi-properties}

Os valores dessas propriedades OSGi são restritos às regras descritas abaixo.

| PID do componente OSGi |   | Obrigatório | Tipo | Restrição (se aplicável) |
|---|---|---|---|---|
| `org.apache.felix.eventadmin.impl.EventAdmin` | `org.apache.felix.eventadmin.ThreadPoolSize` | Sim | inteiro | 2-100 |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | duplo | -- |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | inteiro | -- |
|   | `org.apache.felix.eventadmin.RequireTopic` |   | booleano | -- |
|   | `org.apache.felix.eventadmin.IgnoreTimeout` | Sim | matriz de strings | Deve incluir pelo menos todos `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*` |
|   | `org.apache.felix.eventadmin.IgnoreTopic` |   | matriz de strings | -- |
| `org.apache.felix.http` | `org.apache.felix.http.timeout` |   | inteiro |   |
|   | `org.apache.felix.http.session.timeout` |   | inteiro |   |
|   | `org.apache.felix.http.jetty.threadpool.max` |   | inteiro |   |
|   | `org.apache.felix.http.jetty.headerBufferSize` |   | inteiro |   |
|   | `org.apache.felix.http.jetty.requestBufferSize` |   | inteiro |   |
|   | `org.apache.felix.http.jetty.responseBufferSize` |   | inteiro |   |
|   | `org.apache.felix.http.jetty.maxFormSize` |   | inteiro |   |
|   | `org.apache.felix.https.jetty.session.cookie.httpOnly` |   | booleano |   |
|   | `org.apache.felix.https.jetty.session.cookie.secure` |   | booleano |   |
|   | `org.eclipse.jetty.servlet.SessionIdPathParameterName` |   | string |   |
|   | `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding` |   | booleano |   |
|   | `org.eclipse.jetty.servlet.SessionCookie` |   | string |   |
|   | `org.eclipse.jetty.servlet.SessionDomain` |   | string |   |
|   | `org.eclipse.jetty.servlet.SessionPath` |   | string |   |
|   | `org.eclipse.jetty.servlet.MaxAge` |   | inteiro |   |
|   | `org.eclipse.jetty.servlet.SessionScavengingInterval` |   | inteiro |   |
|   | `org.apache.felix.jetty.gziphandler.enable` |   | booleano |   |
|   | `org.apache.felix.jetty.gzip.minGzipSize` |   | inteiro |   |
|   | `org.apache.felix.jetty.gzip.compressionLevel` |   | inteiro |   |
|   | `org.apache.felix.jetty.gzip.inflateBufferSize` |   | inteiro |   |
|   | `org.apache.felix.jetty.gzip.syncFlush` |   | booleano |   |
|   | `org.apache.felix.jetty.gzip.excludedUserAgents` |   | string |   |
|   | `org.apache.felix.jetty.gzip.includedMethods` |   | matriz de strings |   |
|   | `org.apache.felix.jetty.gzip.excludedMethods` |   | matriz de strings |   |
|   | `org.apache.felix.jetty.gzip.includedPaths` |   | matriz de strings |   |
|   | `org.apache.felix.jetty.gzip.excludedPaths` |   | matriz de strings |   |
|   | `org.apache.felix.jetty.gzip.includedMimeTypes` |   | matriz de strings |   |
|   | `org.apache.felix.http.session.invalidate` |   | booleano |   |
|   | `org.apache.felix.http.session.container.attribute` |   | matriz de strings |   |
|   | `org.apache.felix.http.session.uniqueid` |   | booleano |   |
| `org.apache.sling.scripting.cache` | `org.apache.sling.scripting.cache.size` | Sim | inteiro | >= 2048 |
|   | `org.apache.sling.scripting.cache.additional_extensions` | Sim | matriz de strings | deve incluir &quot;js&quot; |
| `org.apache.sling.engine.impl.log.RequestLogger` | `request.log.output` | Não | string |   |
|   | `request.log.outputtype` | Não | string |   |
|   | `request.log.entry.format` | Não | string |   |
|   | `request.log.exit.format` | Não | string |   |
|   | `request.log.enabled` | Não | string |   |
|   | `access.log.output` | Não | string |   |
|   | `access.log.outputtype` | Não | string |   |
|   | `access.log.enabled` | Não | string |   |
| `org.apache.sling.servlets.resolver.SlingServletResolver` | `servletresolver.servletRoot` | Não | string |   |
|   | `servletresolver.cacheSize` | Não | inteiro |   |
|   | `servletresolver.paths` | Não | cadeia de caracteres[] |   |
|   | `servletresolver.defaultExtensions` | Não | string |   |
|   | `servletresolver.mountProviders` | Não | booleano |   |
|   | `servletresolver.scriptUser` | Não | string | obsoleto, não use |

## Atualização do Java Runtime para a versão 21 {#java-runtime-update-21}

O Adobe Experience Manager as a Cloud Service fez a transição para o Java 21 runtime. Para garantir a compatibilidade, é essencial atualizar as versões da biblioteca conforme descrito nos [Requisitos de tempo de execução](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

