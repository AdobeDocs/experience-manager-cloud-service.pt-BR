---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: c9e9664b8dd17946a340fbf58318b9e6f11a4ff0
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 7%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 16357 {#release-16357}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 16357, lançada publicamente em quinta-feira, 22 de maio de 2024. A versão de manutenção anterior era a versão 16145.

A Ativação de recursos 2024.5.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-16357}

* ASSETS-30379: a verificação da licença DRM percorre toda a árvore de ativos que estão sendo baixados.
* ASSETS-35535: [Erro de adaptador de dados] Downloads de ativos vazios precisam ser ignorados para eventos v1.
* CQ-4356445: Produtor de eventos e implementação de esquema.
* CQ-4356625: melhore a verificação de autorização em languageCopyrendercondition.jsp.
* CQ-4356629: Melhore a verificação de autorização em isWorkflowUser rendercondition.
* CQ-4356934: simplifique a API RequestProcessor ao trabalhar com ResponseEntities.
* CQ-4357214: os processadores de solicitação não devem depender da lógica do servlet.
* FORMS-11295: Adição de suporte para SHA256 com algoritmo ECDSA para Assinatura digital AEM Forms.
* FORMS-12052: Um autor de formulário agora pode aplicar funções personalizadas ao pré-processamento de dados antes do envio.
* FORMS-13209: um manipulador é incluído para substituir os manipuladores padrão de envio e falha de envio do Adaptive Forms. Você pode configurar esses manipuladores por meio do Editor de regras adaptáveis do Forms.
* FORMS-13612: Os leitores de tela agora leem mensagens de erro, descrições curtas e descrições longas para campos no Forms adaptável baseado em componentes principais. Além disso, o suporte foi adicionado para invalidar entradas de formulários adaptáveis quando o formulário contém erros e não é válido para envio.
* FORMS-7483: o Analisador de esquema JSON do AEM Forms agora é compatível com o esquema JSON (2020-12).
* FORMS-9432: Um tipo de conteúdo adicional (Ponto de extremidade REST) foi adicionado à configuração da nuvem da fonte de dados. Ele permite o envio de dados em pares de valores chave para um endpoint autenticado.
* SITES-16392: a criação de inicialização com falha não deve deixar conteúdo de lixo.
* SITES-17854: Suporte UUID para referências de CF e ativos (Pfizer MVP).
* SITES-19555: API de modelo simples para esquema de interface do usuário.
* SITES-19579: API Java para migrar fragmentos de conteúdo de um modelo para o outro.
* SITES-19611: [API aberta] Criar operação de gravação/atualização para gerenciar um Esquema de interface do usuário por modelo na definição de OpenAPI.
* SITES-19614: [Xwalk] Paginação da planilha/rolagem infinita.
* SITES-19698: [API aberta] Criar operação de leitura para gerenciar um Esquema de interface do usuário por modelo na definição de OpenAPI.
* SITES-19834: evento Adobe I/O sem ids para publicar/desfazer a publicação.
* SITES-19973: Implementação da API de pesquisa CFM.
* SITES-20005: o pipeline do autor deve ter um atraso de evento configurável.
* SITES-20121: permitir defaultValue para campos de enumeração.
* SITES-20146: Ativar a versão de visualização / Comparar para páginas movidas.
* SITES-20149: RTC: [cq-wcm-launches-core] Exportar nova API para Inicializações para CFs.
* SITES-20150: RTC: [cq-command] Adicione novos métodos à API existente.
* SITES-20238: [RTC] Pfizer MVP - Adicione a API CF para resolver caminhos CF para IDs e vice-versa.
* SITES-20333: melhore a validação ao criar fragmentos de conteúdo.
* SITES-20334: melhore a validação ao editar modelos de fragmento de conteúdo.
* SITES-20342: [Infraestrutura] Publicar no nível da pasta - adicione o filtro para publicar somente os CFs.
* SITES-20355: remova modelos de fragmento de conteúdo e servlets de API de permissões.
* SITES-20387: navegar pelo tagadmin sempre calcula o uso da tag.
* SITES-20405: [Xwalk] Suporte a mimeType para o recolhimento de campo.
* SITES-20451: Adicionar plug-in do sidecar ao wcm-commons.
* SITES-20495: [BE] Capacidade de obter permissão para publicar no nível da pasta.
* SITES-20499: [MSM][Async] Extraia o código de AsyncOperationServlet para uma classe de utilitário.
* SITES-20583: adicionar etag como propriedade em `LIST`/search fragmentos.
* SITES-20585: Melhore a API de pesquisa do fragmento de conteúdo para filtrar por localidade.
* SITES-20594: retorna o nome completo do usuário que está criando/modificando/replicando um recurso.
* SITES-20601: [OpenAPI] Atualize a API de pesquisa do CF para permitir a busca apenas de fragmentos de conteúdo secundários diretos.
* SITES-20653: [Xwalk] adicione a data de início e a data de término do experimento.
* SITES-20656: [BE] Forneça a opção para corresponder letras maiúsculas e minúsculas ao substituir uma string.
* SITES-20666: [Xwalk] os experimentos devem ser desativados por padrão na criação.
* SITES-20752: [cq-wcm-core] Apple Launches para CFs.
* SITES-20763: atualizar endpoints da API de entrega na integração de sites.
* SITES-20946: adicionar etag como uma propriedade no endpoint de modelos LIST.
* SITES-20947: [persistência] buscar subtarefa por id de fragmento de conteúdo.
* SITES-21012: mesclar esquema de metadados do modelo ao produto.
* SITES-21043: [CF][launches] Melhorias de desempenho de porta lateral para o Cloud Service.
* SITES-21044: [CF][launches] Implementação de carga de edição assíncrona de porta lateral para Cloud Service.
* SITES-21550: [Xwalk] Metadados personalizados: campos de número, data, data e hora.
* SITES-21769: use o prefixo /jcr:id/ path para recuperação de recurso por id.

### Problemas corrigidos {#fixed-issues-16357}

* ASSETS-37611: o fluxo de trabalho &quot;Solicitação para concluir a operação de movimentação&quot; é acionado para o ativo não publicado.
* ASSETS-38723: NPE lançado por MetadataRulesProviderImpl quando getReadRulesForMetadataChildNodes() é chamado antes da inicialização de this.readRules.
* CQ-4357161: a tela AEM Inbox Payload está retornando 404.
* CQ-4357278: DispatcherServlet lança NPE se getRequestBodyType retornar nulo.
* CQ-4357279: o processamento de solicitações falha quando não há pathInfo para uma solicitação.
* FORMS-11589: para usuários somente com a solução da AEM Forms (sem nenhuma outra solução), o pipeline de front-end não está funcionando.
* FORMS-11952: Quando um formulário é enviado, o URL de envio gerado pelo formulário começa com /content/ em vez de /portale/, fazendo o roteamento incorreto da solicitação. Isso impede que a solicitação chegue aos servidores desejados.
* FORMS-13587: no Editor Forms adaptável, o recurso Device Emulator não está funcionando corretamente para componentes principais baseados em Forms adaptável.
* FORMS-13616: O seletor de datas está mostrando a data atual como um dia atrasada, provavelmente devido a um problema de fuso horário, e há dificuldade em definir o formato de data correto devido a essa inconsistência e um problema adicional de padrão de exibição.
* FORMS-13786: no Editor de regras do Forms adaptável, a funcionalidade arrastar e soltar não funciona para funções personalizadas.
* FORMS-13801: mesmo que o componente de termos e condições esteja desativado, a caixa de seleção correspondente permanece ativada.
* FORMS-13827: no Editor de regras do Forms adaptável, a operação WHEN não é compatível atualmente com diferentes tipos de campos com seletores de data.
* FORMS-13829: a lista suspensa, controlada por regras para imitar a funcionalidade do botão de opção, falha ao ser preenchida corretamente após uma seleção ser limpa e selecionada novamente. O comportamento desejado é que as caixas de seleção individuais atuem como botões de opção, permitindo somente uma seleção por vez e desmarcando todas as opções.
* FORMS-13896: Na saída do DoR (Documento de registro), as datas e os números são exibidos em árabe, independentemente de os dados de entrada serem mesclados usando números gregorianos.
* FORMS-14244: em um formulário adaptável baseado em um XDP com scripts incorporados em caixas de seleção, os scripts não são executados para elementos após essas caixas de seleção.
* FORMS-14267: os usuários estão enfrentando erros consistentes de tempo limite ao enviar solicitações de API em ambientes de desenvolvimento, preparo e produção. Essas solicitações estão relacionadas à geração de PDF, às vezes com dados pré-preenchidos usando a vinculação de dados. O problema resulta em um processo de deslocamento que acaba expirando, mas é bem-sucedido ao tentar novamente após o erro.
* FORMS-14376 Quando um usuário pressiona o botão Redefinir, resulta em erros de console se o texto estático for marcado como desvinculado.
* SCRNS-3945: Skyline: cadeia de caracteres &quot;Agendada&quot; não localizada no Screens.
* SITES-11727: [GQL] A hidratação completa das referências do fragmento de conteúdo não tem dados.
* SITES-16674: a caixa de seleção Herdar configurações de implantação não funciona nas propriedades da live copy.
* SITES-17772: AEM: usuário com grupo de administradores não pode desbloquear a página com o que outro usuário bloqueou.
* SITES-18680: não é possível obter variações de referência na consulta graphql (Apple).
* SITES-19462: a pesquisa de ativos não está funcionando corretamente na nuvem AEM.
* SITES-19554: [Xwalk] Editor de planilhas: não é possível esvaziar uma célula.
* SITES-19971: corrigir um CFM contendo guias altera a ordem dos campos.
* SITES-19994: fecha a temporização do botão quando os usuários tentam fechar o fragmento de conteúdo.
* SITES-20023: o upload de arquivo não está funcionando para ativos remotos (ativos de próxima geração) em vários campos.
* SITES-20029: as versões do fragmento de conteúdo são criadas logo após o seu fechamento, sem alterar o conteúdo.
* SITES-20168: modelo de fragmento de conteúdo `locked` O campo não foi atualizado corretamente.
* SITES-20214: problema de sequência de configuração de implantação do AEM ao salvar.
* SITES-20364: 302 redirecionamentos não funcionam com o seletor no URL.
* SITES-20367: problema com a exclusão de inicializações no AEM.
* SITES-20401: [Xwalk] Os metadados da seção não oferecem suporte a propriedades de vários valores.
* SITES-20496: [Xwalk] Nenhuma opção de propriedades ao selecionar uma planilha no administrador do site.
* SITES-20522: quebra de fragmentos de conteúdo corrompido /adobe/sites/cf/fragments no ponto de extremidade.
* SITES-20547: caminhos truncados na lista de caminhos excluídos da Live Copy no AEM as a Cloud Service.
* SITES-20559: [MSM][XF][Lufthansa] A implantação de fragmentos de experiência do idioma principal para o idioma/país não atualiza as referências.
* SITES-20582: a pesquisa e a listagem de fragmentos de conteúdo devem permitir profundidade 0.
* SITES-20586: carimbo de data/hora &quot;Publicado&quot; do modelo não atualizado.
* SITES-20608: fragmentos de experiência com personalização ativada quando incluídos em um modelo causam um loop infinito.
* SITES-20691: a restrição do modelo de fragmento de experiência não atende ao cq:allowedTemplates.
* SITES-20816: CF OpenAPI - Inconsistência de saída com modelo ausente para o fragmento referenciado.
* SITES-21122: Falha do AEM CS Live Copy com fragmentos de conteúdo.
* SITES-21233: [CoreCmp] Acordeão quebrado para GS1 US após a atualização para 15860.
* SITES-21239: remover a dependência circular ContentFragmentSearchService.
* SITES-21316: Visualização do fragmento: a visualização falha devido a alterações de código do SITES-11727.
* SITES-21391: [Evento OpenAPI] Nenhum evento foi acionado ao modificar o título ou as tags (propriedades) de um modelo de fragmento de conteúdo.
* SKYOPS-73234: Aumento da falha do log de erros na atualização do programa AEM Assets Global DAM para AEM versão 15553 e PR Id 35362.
* SKYOPS-75341: NoSoMethodError no pacote de distribuição Crosswalk.

### Problemas conhecidos {#known-issues-16357}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-16357}

Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-16357}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.22-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.25.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
