---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fa2da21ef6424bce0830d503eba650e1c1bf3dc2
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 8%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 17964 {#release-17964}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 17964, lançada publicamente em quinta-feira, 25 de setembro de 2024. A versão de manutenção anterior era a versão 17689. A versão 17882 foi tornada privada devido a um problema.

A ativação de recursos 2024.10.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-17964}

* ASSETS - 37750: [Prioridade 4] [GraphQL] Suporte para URLs DM scene7: recortes inteligentes de imagem.
* CQ - 4354583: [AEMaaCS] Enviar eventos do processo de tradução por meio do Pipeline de Adobe.
* CQ - 4357642: atualizar credenciais do MSFT no Conector OOTB.
* CQ - 4358217: desserializar o corpo da solicitação da entidade de solicitação.
* CQ - 4358342: registre RequestProcessors em apenas um método HTTP.
* FORMS - 10781: aprimorar o editor de regras para criar regras para o item seguinte/anterior em um painel.
* FORMS - 14595: [Os valores do recurso sem navegador] estão ausentes no DoR quando dados pré-preenchidos são usados para calcular o DoR para renderização sem navegador.
* FORMS - 15619: Kit de tradução atualizado do AEM Forms.
* FORMS - 16113: [Adobe Sign]Não é possível atualizar o status do contrato por um usuário diferente.
* FORMS - 16155: [Editor de regras] para implementar a função assíncrona.
* GRANITE - 53872: adicione novas variáveis de ambiente para a ID do cliente IMS.
* SITES - 23738: Componentes principais de versão 2.27.0.
* SITES - 16610: Fragmentos de conteúdo: obter endpoint de detalhes da inicialização.
* SITES - 16614: Fragmentos de conteúdo: endpoint de rebase do Launch.
* SITES - 16615: Fragmentos de conteúdo: Promover endpoint do Launch.
* SITES - 24215: Fragmentos de conteúdo: implementar obter endpoint de origens do Launch.
* SITES - 20336: fragmentos de conteúdo: melhore a validação ao excluir um modelo de fragmento de conteúdo.
* SITES - 21090: Fragmentos de conteúdo: adicionar suporte para valores fracionais mín./máx. para campos de número
* SITES - 21658: Fragmentos de conteúdo: atualize para usar referências UUID.
* SITES - 23054: fragmentos de conteúdo: copiar modelos de fragmento de conteúdo.
* SITES - 23264: Fragmentos de conteúdo: criar um esquema estático de um modelo.
* GET SITES - 23265: fragmentos de conteúdo: exponha o esquema estático de um modelo por meio do ponto de acesso do esquema da interface do usuário.
* SITES - 23266: fragmentos de conteúdo: capacidade de adicionar restrições aos modelos de fragmento de conteúdo.
* SITES - 23778: fragmentos de conteúdo: os modelos de fragmento de conteúdo de pesquisa devem permitir a pesquisa de modelos que nunca foram publicados.
* SITES - 23335: Fragmentos de conteúdo: adicionar suporte para referências de ativos externos.
* SITES - 24626: Fragmentos de conteúdo: RTC: Permissões para migração de UUID: 2.
* SITES - 24786: Fragmentos de conteúdo: melhorias para o ponto de extremidade `referencesTree`.
* SITES - 24833: fragmentos de conteúdo: remova a validação da entrada de HTML em relação a uma lista de tags de HTML permitidas.
* SITES - 23380: GraphQL: use a API adequada para ler os metadados do ativo.
* SITES - 22864: [Edge Delivery] Editor universal com nova integração de estrutura de conteúdo AEM H2 2024.
* SITES - 23584: Os testes de componentes do Foundation falham no Java 17.
* SITES - 23662: evento: o usuário que aciona uma solicitação de publicação não pode ser extraído de instruções de log JCR em logs do servidor.
* SITES - 23301: adicione suporte para iniciar um novo fluxo de trabalho para criar estruturas de pastas ao criar traduções de fragmentos de conteúdo.
* SITES - 23336: Fragmentos de conteúdo: adicionar suporte para referências de ativos externos
* SITES - 24091: Divisão do pacote de conteúdo do MSM: principal.
* SITES - 24114: isSourceRenderCondition: reduzir mensagem de log de erros para DEBUG.
* SITES - 24166: mitigação de ativos remotos para o editor de interface para toque.
* SITES - 24409: registra todos os processadores de solicitação em apenas um método HTTP.
* SITES - 25008: Melhore a manipulação de PersistenceExceptions e problemas de permissões.
* SITES - 24821: [Xwalk] Torne aem.page / aem.live o padrão.

### Problemas corrigidos {#fixed-issues-17964}

* CQ - 4356887: inconsistência no status do projeto de tradução para a Akamai Technologies Inc.
* CQ - 4357878: a estrutura de tradução não está definindo o estado de erro na tradução com falha do fornecedor.
* CQ - 4358028: falha ao criar projeto se a miniatura for carregada.
* CQ - 4358290: a configuração do Target NÃO está funcionando na página publicada.
* FORMS - 13173: Desalinhamento da lista suspensa no Formulário adaptável > Editor de regras > Campo Soltar objeto.
* FORMS - 13873: AFv2: (&quot;-&quot;) no nome do componente resulta na falha das regras.
* FORMS - 14340: Erro na instanciação de FormsAndDocumentOmniSearchHandler e CloudStorageSubmitActionInserter.
* FORMS - 15363: Nome exibido no Editor de regras.
* FORMS - 15381: melhoria da interface do usuário da mensagem Escopo de autorização.
* FORMS - 15595: AEM Formulário TnC Consentimento Texto quebra linha problema.
* FORMS - 15623: AEMaaCS Forms - Alternativas para atualizar várias tabelas no Dynamics com um POST.
* FORMS - 15682: AEM Forms - Não é possível vincular DOR ao Dynamics FDM.
* FORMS - 15799: a página Assinatura do Adobe Sign GovCloud não é renderizada no iframe.
* FORMS - 15835: problema de reescrita do URL do formulário pós-envio.
* FORMS - 16091: Consumindo o Binary.java reestruturado.
* FORMS - 16096: O usuário do Forms não tem acesso à caixa de diálogo do restendpoint.
* FORMS - 16139: Adição do registro necessário para DoR no formulário Componentes principais.
* FORMS - 6935: o estado do componente ativo não tem relação de contraste de 3 para 1.
* FORMS - 7018: elemento vazio recebe foco.
* GRANITE - 53028: NPE em ExternalProcessPollingHandler.
* GRANITE - 53907: não é possível identificar o usuário do serviço como superusuário do workflow.
* SITES - 24405: Fragmentos de conteúdo: as informações estendidas para enumerações devem ser mais resilientes
* SITES - 23024: Fragmentos de conteúdo: a enumeração não retorna bloqueado: verdadeiro em fragmentos de GET.
* SITES - 23269: fragmentos de conteúdo: a criação de fragmentos de conteúdo permite definir campos bloqueados.
* SITES - 23337: Fragmentos de conteúdo: O ponto de extremidade do lote com `body` falha com a exceção de conversão.
* SITES - 23474: Fragmentos de conteúdo: a paginação deve excluir recursos corrompidos em Pesquisar fragmentos de conteúdo.
* SITES - 23615: Fragmentos de conteúdo: a cópia do fragmento de conteúdo AuthoringInfo não é atualizada
* SITES - 23668: fragmentos de conteúdo: a live copy do patch com vários campos falha com 400
* SITES - 23695: fragmentos de conteúdo: a descrição da guia não está disponível no UiSchema
* SITES - 23704: Fragmentos de conteúdo: enumerações de vários valores não compatíveis no _extendedInfo
* SITES - 23781: Fragmentos de conteúdo: valores duplicados não são permitidos em campos de enumeração
* SITES - 24150: Fragmentos de conteúdo: versão do fragmento de conteúdo Os dados de criação sobre a criação estão ausentes
* SITES - 24230: Fragmentos de conteúdo: corrigir a filtragem após o status de replicação `modified` em Pesquisar modelos de fragmento de conteúdo
* SITES - 24233: Fragmentos de conteúdo: a filtragem por `publishedBy` pode incluir recursos não publicados em Pesquisar modelos de fragmento de conteúdo
* SITES - 24355: fragmentos de conteúdo: o relacionamento dinâmico não é respeitado para fragmentos de conteúdo criados por pastas
* SITES - 24816: Fragmentos de conteúdo: ordem das mensagens ValidationStatus inconsistente.
* SITES - 23896: evento: mais eventos estão se juntando com um evento de página movida
* SITES - 23899: evento: os eventos de página estão atrasados ou não são gerados
* SITES - 23961: evento: a criação de modelos de fragmento de conteúdo com referências falha quando a pasta de configuração está presente
* SITES - 23963: evento: eventos excluídos da página às vezes não vêm
* SITES - 23443: GraphQL: comportamento inconsistente da consulta do cursor do GraphQL.
* SITES - 10994: a ordem de foco do teclado não é lógica.
* SITES - 16357: AEM: o botão está truncado na guia Configurar o Analytics do menu Sites.
* SITES - 19836: o componente fantasma no contêiner é exibido em instâncias de publicação e visualização.
* SITES - 22348: a página Visão geral da Live Copy não é carregada se houver mais de 100 live copies para um projeto.
* SITES - 22960: resolvedor de recursos não fechado em ContentFragmentModelOmniSearchHandler.
* SITES - 23284: codificação de URL que causa uma caixa de diálogo em branco do navegador de caminho.
* SITES - 23505: os componentes mostram URLs incorretos quando a página é movida para outro local.
* SITES - 23574: não é possível visualizar/comparar com as versões atuais de muitas páginas
* SITES - 23585: problema com a restauração da herança para componentes que têm o nó cq:responsive
* SITES - 23650: discrepância na contagem de links recebidos no ambiente de autor do AEM
* SITES - 23659: regressão do Servlet de linguagem de conteúdo causada pela alternância FT_* SITES - 9757
* SITES - 23759: Assets adicionados ao fragmento de experiência não são publicados com inicializações
* SITES - 24025: 302 redirecionamentos no AEM que retornam o cabeçalho do local usando DNS interno em vez de DNS público
* SITES - 24036: É necessário investigar caracteres persistentes AEM RTE no formato ASCII
* SITES - 24317: A configuração de proxy não funciona com a Autenticação básica
* SITES - 24918: [Xwalk] corrija erros 504 retornados ocasionalmente ao usar saída de ip dedicada.

### Problemas conhecidos {#known-issues-17964}

* FORMS - 15818: A entrada do descritor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` não encontrou instruções nos logs do servidor. Estas são instruções de registro inofensivas.

### Recursos e APIs obsoletos {#deprecated-17964}

Observe que estamos no processo de atualização do `com.day.cq.wcm.api` e, com a versão atual, marcamos como `@Deprecated` alguns de seus métodos e classes. Eles serão removidos em versões futuras. Portanto, considere mudar para as alternativas sugeridas se estiver usando alguma delas.

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-17964}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 16 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-17964}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
