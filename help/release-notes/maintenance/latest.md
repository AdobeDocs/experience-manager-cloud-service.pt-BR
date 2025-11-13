---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 39993d115d58d9dfe1f9328c5ceba0d30a78569d
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 8%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 23385 {#23385}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 23385, lançada publicamente em sexta-feira, 13 de novembro de 2025. A versão de manutenção anterior era 22943.

A ativação de recursos do 2025.11.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

>[!NOTE]
>
>As versões 23320 e 23122 foram tornadas privadas.

### Aprimoramentos {#enhancements-23385}

* CQ-4361363: traduções mais recentes do AEM e Granite.
* FORMS-21594: Ativar o bloqueio de conteúdo e layout de modelo de comunicações interativas para autores de conteúdo.
* FORMS-20385: Suporte à edição XDP no Editor de comunicações interativas.
* FORMS-10883: suporte a JSON com tags de namespace XHTML na geração do DoR para garantir a renderização precisa de dados de rich text enviados por APIs.
* FORMS-21751: Recursos da tela de desenho - Estouro de texto, IU para Quebra de página.
* FORMS-22049: Editor de comunicações interativas - Migração para o Spectrum 2.
* FORMS-22050: Suporte para numeração dinâmica de páginas no Editor de comunicações interativas.
* FORMS-21606: SPIs de renderização OSGi públicas para comunicações interativas.
* FORMS-21613: Relatório de transações e registro de desempenho para SPIs de Comunicação interativa de renderização.
* GRANITE-62394: atualização do tempo joda para 2.12.7.
* GRANITE-36205: atualize a versão do Oak para 1.88.0.
* GRANITE-62020: Melhore a política de novas tentativas em `RepositoryServiceHttpClient`.
* GRANITE-62169: atualize o commons-lang para 3.19.0.
* SITES-35092: Fragmentos de conteúdo - Novo procedimento de mixin e atualização para pesquisa semântica.
* SITES-32319: Delivery OpenAPI - Referências da página de suporte.
* SITES-20123: GraphQL: suporte a elementos sobrescritos na resposta JSON.
* SITES-34744: Nova propriedade &quot;card&quot; na resposta do Fragmento de conteúdo que contém dados que podem ser usados para renderizar uma miniatura.
* SITES-34571: permite que os campos de enumeração fiquem vazios.
* SITES-34812: adição da capacidade de recuperar um fragmento de conteúdo sem suas referências, usando o parâmetro &quot;references&quot; com o valor &quot;none&quot;.
* SITES-35176: Fazer o check-out de um fragmento de conteúdo por meio da interface para toque agora impede a edição do fragmento de conteúdo no novo editor por outros usuários.
* SITES-30371: adição de suporte para campos de referência baseados em uuid.
* SITES-19309: recupera um máximo de 150 referências ao abrir o assistente para mover página.
* SITES-32515: Edge Delivery com Universal Editor - Adicione suporte para vários campos e vários campos compostos (acesso antecipado).
* SITES-33784: Edge Delivery com editor universal - Adicione suporte para ld-json em metadados de página.
* SITES-34832: Edge Delivery com Universal Editor - adicione o caminho público de uma página à resposta do servlet de informações da página.
* SITES-25893: Edge Delivery com Universal Editor - adicione suporte para strong e stress à renderização de texto em blocos.
* SITES-26158: Edge Delivery com Universal Editor - adiciona suporte para marcação de tabela em blocos e colunas (acesso antecipado).
* SITES-27949: Edge Delivery com Universal Editor - torna o mapeamento de caminho opcional.
* SITES-35811: use o novo índice em consultas de fragmentos de conteúdo.
* SKYOPS-120857: atualização do cofre de arquivos para 4.1.4.
* SKYOPS-118390: Atualize o recurso JCR para 3.3.6.
* SKYOPS-121082: atualização de versões de `org.apache.sling.discovery.standalone`, `org.apache.sling.jcr.packageinit` e `org.apache.sling.commons.fsclassloader` conjuntos de sling.

### Problemas corrigidos {#fixed-issues-23385}

* ASSETS-58926: Corrigir o recurso de miniatura de alteração de vídeo no DM.
* ASSETS-58623: Corrija o npe no omnisearch quando a configuração existir.
* CQ-4361144: corrigido o cancelamento de fragmentos de conteúdo de trabalhos de tradução.
* CQ-4355446: corrigida a cadeia de caracteres não localizada no projeto de tradução que ocorria na caixa de diálogo Cancelar tarefa de tradução.
* CQ-4360747: corrija um problema em que os Trabalhos de tradução repetíveis criam cargas vazias e são acionados com muita frequência.
* GRANITE-61318: corrija um problema em que o assistente de criação de página destaca apenas campos obrigatórios na guia básico.
* GRANITE-60514: corrija um problema em que interrompia publicações agendadas durante a execução do pipeline de pilha completa.
* GRANITE-61019: corrija o problema com o GC na primeira execução após a reinicialização do AEM.
* GRANITE-60456: corrija o problema quando o administrador abre qualquer página de propriedades do usuário.
* SITES-34555: GraphQL - QueryValidationError após implantações.
* SITES-35077: fragmentos de conteúdo - o cancelamento da publicação falha para fragmentos com parênteses devido à codificação incorreta de URL.
* SITES-35374: Fragmentos De Conteúdo - Fragmento De Conteúdo Editado Desaparece Após A Navegação De Volta.
* SITES-36130: NPE em `EditorRestrictionsStatusImpl`.
* SITES-35810: NullPointerException em Inicializações bloqueia a fila publishEdgeDeliverySubscriber.
* SITES-34368: o AEM CIF gera 12 aliases GraphQL - excede o limite de 10 do Magento 2.4.6-P12.
* SITES-36193: Correções do conector CCS.
* SITES-35169: resolvido um problema que causava paginação incorreta quando recursos de fragmento inválidos eram retornados pela pesquisa.
* SITES-34574: corrigido um problema em que, em alguns casos, o cursor não era retornado pela API de pesquisa de fragmento de conteúdo.
* SITES-35520: correção de um problema que causava ClassCastException ou tempos limite ao tentar publicar conteúdo.
* SITES-35210: correção de uma NullPointerException que ocorria ao tentar publicar um fragmento quebrado com filtro de referências vazio.
* SITES-35933: correção de um erro que resultava no acionamento de fluxos de trabalho vazios de &quot;Solicitação de ativação&quot; após a publicação do fragmento de conteúdo.
* SITES-35925: correção de um erro relacionado à correção de modelos de fragmento de conteúdo que excluía as propriedades &quot;translatable&quot; e &quot;showThumbnail&quot; do modelo.
* SITES-35409: correção de um erro que impedia a republicação de fragmentos ajustados ao mover uma página.
* SITES-15757: correção de um erro que impedia a republicação de páginas ajustadas ao mover uma página.
* SITES-34638: correção de um erro em que as propriedades de páginas avô não eram incluídas ao criar novas versões.
* SITES-35226: correção de uma regressão que fazia com que o seletor de ativos no editor de páginas falhasse no carregamento em determinadas circunstâncias.
* SITES-35071: a exportação de CSV retorna resultados não filtrados quando o omnisearch usa a frase entre aspas.
* SITES-32182: Edge Delivery com Universal Editor - corrija problemas de codificação com URLs que contêm parâmetros de solicitação já codificados.
* SITES-34324: Edge Delivery com Universal Editor - corrija a renderização de links com um protocolo tel:.
* SITES-35333: Edge Delivery com Universal Editor - corrija a seleção de representação de ativos para imagens nos metadados da página.
* SITES-35549: Edge Delivery com Universal Editor - corrija entidades html de codificação dupla nos metadados da página.

#### Guias do AEM {#guides-23385}

* GUIDES-33597: Se um elemento `prop` vazio sem atributos ou valores for adicionado a um arquivo DITAVAL, não será possível adicionar outros elementos `prop`.
* GUIDES-33693: Ao fazer upload de uma imagem editada novamente por meio da interface do usuário do Experience Manager Guides, a representação original da imagem é atualizada, mas o conteúdo DITA associado continua a exibir a versão anterior da imagem.
* GUIDES-35607: Logs de erro gerados ao carregar um ativo por meio da interface do Assets ou ao criar um novo arquivo a partir da interface do Editor. Use incorretamente o termo `predecessor` em vez de `successor` na mensagem de log.
* GUIDES-37649: Ao publicar um mapa DITA usando a linha de base no AEM Sites (com mapeamento de componente herdado), os elementos do mapa com o atributo `processing-role = resource-only` também são publicados.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).


### Problemas conhecidos {#known-issues-23385}

* FORMS-22633: Os envios de formulários podem falhar quando um código personalizado que depende das APIs do GuideBridge (`getData` ou `getDataXML`) estiver sendo usado. Se você enfrentar esse problema, entre em contato com o Suporte da Adobe para obter assistência.

### Recursos e APIs obsoletos {#deprecated-23385}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-23385}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 31 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-23385}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.88.0 | [API do Oak 1.88.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
