---
title: Recursos obsoletos e removidos
description: Notas de versão específicas para recursos obsoletos e removidos do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: d80872b1df4d31d784745dabeb0e1680fc921cb8
workflow-type: tm+mt
source-wordcount: '2172'
ht-degree: 73%

---

# Recursos e APIs obsoletos e removidos {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Recursos obsoletos e removidos do AEM as a Cloud Service"
>abstract="O AEM as a Cloud Service tem um modelo de implantação nativo em nuvem. Determinados recursos foram substituídos por equivalentes nativos em nuvem e esta guia mostra esses recursos."


A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores. Além disso, como o [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] fornece um modelo de implantação nativo em nuvem, certos recursos e funcionalidades foram substituídos por seus equivalentes nativos em nuvem.

Para comunicar a remoção/substituição iminente das funcionalidades do [!DNL Experience Manager], as seguintes regras de aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Os recursos obsoletos continuam disponíveis, mas não estão aprimorados.
1. Os recursos anunciados como obsoletos são removidos na versão principal subsequente, com a maior brevidade. A data de destino real para remoção é anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoletos no [!DNL Experience Manager] as a [!DNL Cloud Service]. Normalmente, os recursos planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, como uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação atual, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Recursos | Recurso obsoleto | Substituição |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Propriedades dos Fragmentos de experiência para **Status da rede social**. | O recurso será removido em breve. |
| [!DNL Sites] | Fragmentos de conteúdo simples baseados em modelo. | [Fragmentos de conteúdo estruturado com base em modelo](/help/assets/content-fragments/content-fragments-models.md) agora. |
| [!DNL Assets] | fluxo de trabalho `DAM Asset Update` para processar imagens ingeridas. | A assimilação de ativos usa [microsserviços de ativos](/help/assets/asset-microservices-overview.md) agora. |
| [!DNL Assets] | Carregar ativos diretamente no [!DNL Experience Manager]. Consulte [APIs de carregamento de ativos obsoletos](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Use [Upload binário direto](/help/assets/add-assets.md). Para obter detalhes técnicos, consulte [APIs de upload direto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Determinadas etapas do fluxo de trabalho](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) `DAM Asset Update` não são compatíveis, incluindo a chamada de ferramentas de linha de comando, como o [!DNL ImageMagick]. | Os [microsserviços de ativos](/help/assets/asset-microservices-overview.md) oferecem uma substituição para muitos fluxos de trabalho. Para processamento personalizado, use [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodificação FFmpeg de vídeos. | Para gerar miniaturas do FFmpeg, use os [Microserviços de ativos](/help/assets/asset-microservices-overview.md). Para a transcodificação FFmpeg, use o [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interface de replicação em árvore na guia &quot;Distribuir&quot; do agente de replicação (remoção após 30 de setembro de 2021) | Abordagens [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [fluxo de trabalho Publicar árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Nem a guia Distribuir da tela do administrador do agente de replicação nem a API de replicação podem ser usadas para replicar pacotes de conteúdo com mais de 10 MB. Em vez disso, use [Gerenciar publicação](/help/operations/replication.md#manage-publication) ou [fluxo de trabalho de publicação da árvore de conteúdo](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Integrações que usam credenciais geradas de projetos da Adobe Developer Console perderão gradualmente o suporte às credenciais da Conta de serviço (JWT). As novas credenciais da Conta de serviço (JWT) não podem ser criadas na Adobe Developer Console em ou após 1º de maio de 2024, embora as credenciais da Conta de serviço (JWT) existentes ainda possam ser usadas para integrações já configuradas até 1º de janeiro de 2025, momento em que as credenciais da Conta de serviço (JWT) existentes não funcionarão mais e os clientes deverão migrar para as credenciais de Servidor para Servidor do OAuth. [Saiba mais](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrar](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) para credenciais OAuth de servidor para servidor. |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades que foram removidas do [!DNL Experience Manager] com o [!DNL Experience Manager] as a [!DNL Cloud Service].

| Área | Destaque | Substituição | Data definida para remoção |
| ------------ | ------------------ | ----------- | ------------------- |
| Interface do usuário | A interface clássica é removida da interface do usuário do produto. Algumas caixas de diálogo da interface clássica estão disponíveis para alguns recursos selecionados, como o Verificador de links, a Limpeza de versão e algumas configurações do Cloud Service. As próximas [atualizações do produto](/help/release-notes/home.md) podem remover ainda mais a disponibilidade da interface clássica. | Interface do usuário padrão | Removido |
| [!DNL Dynamic Media] | As integrações anteriores com o [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=pt-BR#integration) e o [Dynamic Media Hybrid mode](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=pt-BR#dynamic) não estão disponíveis no [!DNL Experience Manager] as a [!DNL Cloud Service]. | Use o [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornecido com o [!DNL Experience Manager] as a [!DNL Cloud Service]. | Removido |
| [!DNL Sites] | Portal Director e Portlet Component | Estes recursos foram descontinuados no [!DNL Experience Manager] 6.4 e agora foram removidos do [!DNL Experience Manager]. | Removido |
| [!DNL Sites] | Importador de design | Este recurso foi removido porque as seções imutáveis do repositório do [!DNL Experience Manager] não estão acessíveis no tempo de execução. | Removido |
| [!DNL Assets] | O compartilhamento do [!DNL Assets] com os serviços Experience Cloud Assets Core Service e Creative Cloud não está disponível. | Para integração com a [!DNL Adobe Creative Cloud], use o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html). | Removido |
| [!DNL Foundation] | Suporte para fontes de dados do Apache Sling (pacote OSGi org.apache.sling.datasource) | N/A | Removido |
| [!DNL Foundation] | Suporte para modelos de script JST (pacote OSGi org.apache.sling.scripting.jst) | N/A | Removido |
| [!DNL Foundation] | Suporte para o quadro de permissões Apache Felix Http | OSGi Http Whiteboard | Março de 2022 |
| [!DNL Foundation] | Suporte para com.adobe.granite.oauth.server | Integração do Adobe IMS | Março de 2023 |
| [!DNL Foundation] | Suporte para o recurso org.apache.sling.serviceusermapping para [obter a ID de usuário do serviço](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | N/A | 30/08/24 |


## APIs AEM {#aem-apis}

Veja abaixo uma extensa lista de APIs obsoletas do AEM e a data esperada da remoção de cada uma delas. Espera-se que os clientes removam as APIs de seu código até a data de remoção prevista. Qualquer uso da API após a data de remoção gerará erros no SDK/Ambiente de Desenvolvimento local e no processo de construção do Cloud Manager.

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
    <td>Use as interfaces Auth Core/Auth Core SPI do Sling como alternativa</td>
    <td>2015</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>O uso da Sling's Discovery API é uma alternativa</td>
    <td>2015</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>01/03/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>05/03/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>Recomenda-se a implementação e o uso do Apache Johnzon do <a href="https://johnzon.apache.org/index.html">javax.json</a>. </td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Os gerenciadores de persistência personalizados não são compatíveis com o AEM as a Cloud Service.</td>
    <td>30/04/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>O Commons Lang 2 está em modo de manutenção. O Commons Lang 3 deve ser usado em seu lugar.</td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>O Commons Collections 3 está em modo de manutenção. O Commons Collections 4 deve ser usado em seu lugar.</td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>É recomendado que use a API Apache Felix HealthCheck em seu lugar</td>
    <td>30/04/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>O Felix web console não é suportado em ambientes em nuvem</td>
    <td>30/04/2021</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml<br>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.client.util</td>
    <td>Os pacotes Eclipse Jetty e Felix Http Jetty não são mais suportados.</td>
    <td>27/05/2021</td>
    <td>26/08/2021</td>
  </tr>
  <tr>
    <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>O uso desta API não é compatível com o AEM as a Cloud Service.</td>
    <td>27/05/2021</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>O metatipo Apache Felix e as APIs SCR estão obsoletos.  Em vez disso, use o metatipo OSGi e as APIs de Serviço Declarativo.</td>
    <td>27/05/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>As classes de implementação de logs não são compatíveis com o AEM as a Cloud Service.</td>
    <td>04/07/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Esta API está obsoleta porque o Apache Abdera é um projeto inativo desde 2017.</td>
    <td>29/07/2021</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Esta API está obsoleta porque o Apache Abdera é um projeto inativo desde 2017.</td>
    <td>08/04/2019</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>Legacy AEM 6.x API.</td>
    <td>08/04/2019</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Esta API não é suportada no Cloud Service.</td>
    <td>30/09/2021</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>As classes de utilitários relacionadas ao Apache Xerces estão removidas nas versões subsequentes, causando uma alteração importante da versão. Como estes utilitários são para uso interno no Filevault, a API está ficando obsoleta da superfície pública da API.</td>
    <td>01/09/2021</td>
    <td>removida</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>Legacy AEM 6.x API.</td>
    <td>08/04/2019</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>O quadro de permissões Apache Felix Http não é mais suportado. Migre o seu código para o OSGi HTTP Whiteboard.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Esta API está obsoleta, migre seu código para as APIs XML fornecidas pelo JDK.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>Esta API de logback interna não é compatível com o AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>Esta API de log4j interna não é compatível com o AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>O Apache Log4j 1 chegou ao fim da vida útil em 2015 e não é mais compatível.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>Esta API de logback interna não é compatível com o AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>removida</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>É necessário atualizar o Handlebars da versão 4.0.5 para a 4.3.0, devido à vulnerabilidade de segurança. Este pacote não está mais presente no Handlebars atualizado.</td>
    <td>05/05/2022</td>
    <td>05/08/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Essa API não é mais aceita. Em vez disso, use org.apache.sling.api.resource.ResourceResolverFactory.</td>
    <td>29/09/2022</td>
    <td>24/11/2022</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Essa API está obsoleta. Em vez disso, use os Construtores do Apache Sling.</td>
    <td>31/10/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>Esta API não é compatível com o AEM as a Cloud Service.</td>
    <td>15/05/2023</td>
    <td>15/06/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>As bibliotecas principais do Google Guava estão obsoletas.</td>
    <td>15/05/2023</td>
    <td>15/06/2023</td>
  </tr>
  <tr>
    <td>org.slf4j.event	</td>
    <td>Esta API slf4j interna não é compatível com o AEM as a Cloud Service</td>
    <td>11/04/2022</td>
    <td>30/08/2024</td>
  </tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>O uso desta API não é compatível com o AEM as a Cloud Service.</td>
    <td>17/05/2024</td>
    <td>30/06/2024</td>
  </tr>  
</tbody>
</table>
</details>

## Configuração OSGI {#osgi-configuration}

As duas listas abaixo refletem a superfície de configuração OSGi do AEM as a Cloud Service, descrevendo o que os clientes podem configurar.

1. Uma lista de configurações OSGi que não devem ser definidas pelo código do cliente
1. Uma lista de configurações OSGi cujas propriedades podem ser configuradas, mas devem obedecer às regras de validação indicadas. Essas regras incluem se a declaração da propriedade é obrigatória, seu tipo e, em alguns casos, seu intervalo permitido de valores.

Se uma configuração OSGI não estiver listada, ela poderá ser configurada pelo código do cliente.

Essas regras são validadas durante o processo de criação do Cloud Manager. Regras adicionais podem ser adicionadas ao longo do tempo e a data de aplicação esperada é anotada na tabela. Espera-se que os clientes cumpram essas regras até a data de aplicação prevista. Não seguir as regras após a data de remoção gerará erros no processo de criação do Cloud Manager. Os projetos Maven devem incluir o [Plug-in Maven Build Analyzer do SDK da AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR) para sinalizar erros de configuração OSGI durante o desenvolvimento do SDK local.

Informações adicionais sobre a configuração OSGI podem ser encontradas em [este local](/help/implementing/deploying/configuring-osgi.md).

+++Configurações OSGi que não podem ser modificadas.
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Data do Anúncio: 25/8/2021, Data de Imposição: 26/11/2021)
+++

+++Configurações OSGi sujeitas às regras de validação de compilação.
* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * Tipo: número inteiro
   * Intervalo obrigatório: 2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * Tipo: duplo
* `org.apache.felix.eventadmin.Timeout`
   * Tipo: número inteiro
* `org.apache.felix.eventadmin.RequireTopic`
   * Tipo: booleano
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * Obrigatório
   * Tipo: matriz de cadeias de caracteres
   * Intervalo obrigatório: deve incluir pelo menos todos os `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * Tipo: matriz de cadeias de caracteres
* **`org.apache.felix.http`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: número inteiro
   * `org.apache.felix.http.session.timeout`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: número inteiro
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: número inteiro
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: sequência de caracteres
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: número inteiro
      * Intervalo obrigatório: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obrigatório
      * Tipo: matriz de cadeias de caracteres
      * Intervalo obrigatório: deve incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Data do Anúncio: 30/4/2021, Data de Imposição: 31/7/2021)
   * `smtp.host`
      * Tipo: sequência de caracteres
   * `smtp.port`
      * Tipo: número inteiro
      * Intervalo obrigatório: 465, 587 ou 25
   * `smtp.user`
      * Tipo: sequência de caracteres
   * `smtp.password`
      * Tipo: sequência de caracteres
   * `from.address`
      * Tipo: sequência de caracteres
   * `smtp.ssl`
      * Tipo: sequência de caracteres
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Data do Anúncio: 16/11/21, Data de Imposição: 16/2/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumeração
      * Intervalo obrigatório: INFO, DEBUG ou TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: sequência de caracteres
   * `org.apache.sling.commons.log.file`
      * Tipo: sequência de caracteres
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano
+++

