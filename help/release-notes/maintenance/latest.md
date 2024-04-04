---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d07fc976fe9c8e7872468048f80e525fe8484339
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 5%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 15787 {#release-15787}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 15787, lançada publicamente em sexta-feira, 4 de abril de 2024. A versão de manutenção anterior era a versão 15575.

A Ativação de recursos 2024.3.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-15787}

* SITES-19059 - Fragmentos de conteúdo - OpenAPI - Permitir defaultValue para campos de enumeração
* SITES-20013 - Fragmentos de conteúdo - OpenAPI - WCMScriptHelper deve abortar a renderização quando nenhum ServletResolver estiver presente
* SITES-19926 - Fragmentos de conteúdo - OpenAPI - Melhorias no OnOffTriggerProcessor
* SITES-17945 - Fragmentos de conteúdo - OpenAPI - Obter metadados modificados pela última vez para cada versão
* SITES-17298 - Fragmentos de conteúdo - OpenAPI - Permissões de modelos de fragmento de conteúdo
* SITES-14255 - Fragmentos de conteúdo - OpenAPI - Valide a exclusividade do campo de texto se o sinalizador exclusivo estiver definido no modelo de fragmento
* SITES-15557 - Fragmentos de conteúdo - OpenAPI - Permitir defaultValue para campos de enumeração
* SITES-1559 - Fragmentos de conteúdo - OpenAPI - Atualização da API da lista de CF para permitir a busca apenas de fragmentos de conteúdo secundários diretos (BE)
* SITES-16052 - Fragmentos de conteúdo - OpenAPI - Adicione o URL da instância em que um recurso pode ser consumido
* SITES-17944 - Fragmentos de conteúdo - OpenAPI - Mapeamento adequado de ACLs JCR para o endpoint de Permissões CF
* SITES-17513 - Plano de controle do fragmento de conteúdo - Cancelar a publicação de fragmentos de conteúdo
* SITES-8831 - Plano de controle do fragmento de conteúdo - PUT - Atualize um fragmento com informações completas
* GET SITES-8836 - Fragmentos de conteúdo - OpenAPI - Plano de controle - Referências - Obter referências principais de um fragmento (por UUID)
* SITES-8986 - Fragmentos de conteúdo - OpenAPI - Publicar modelo de fragmento de conteúdo
* SITES-18073 - Fragmentos de conteúdo - OpenAPI - Padrão PreviewURL para um CFM
* SITES-15242 - Fragmentos de conteúdo - OpenAPI - Estenda os eventos de publicação para fornecer informações sobre o nível
* SITES-18702 - Fragmentos de conteúdo - OpenAPI - [Infraestrutura] Capacidade de publicar no nível da pasta
* SITES-20020 - Fragmentos de conteúdo - OpenAPI - Remover `X-Adobe-Accept-Unsupported-API` antes da GA
* SITES-16066 - Fragmentos de conteúdo - Editor de fragmentos - Alterar URL do JS do seletor de ativos
* SITES-19326 - Fragmentos de conteúdo - Editor de fragmentos - Atualizar links na interface do usuário do Assets para abrir o CF no novo Editor de CF
* SITES-10515 - Fragmentos de conteúdo - API do GraphQL - GraphQL - Problema de desempenho do AbstractFetcher Carregando fragmentos de conteúdo referenciados
* SITES-17364 - Fragmentos de conteúdo - API do GraphQL - Retorne o nome completo para as propriedades Modificado por e Publicado por
* SITES-19165 - Fragmentos de conteúdo - API do GraphQL - Permite que modelos globais sejam usados, referenciados e consultados em todos os endpoints do GraphQL
* SITES-17768 - Fragmentos de conteúdo - API do GraphQL - Expor o URL do Dynamic Media para imagens via _dmS7Url
* SITES-11057 - Infraestrutura principal - Evitar carregar todas as versões ao abrir Linha do tempo > Versões
* SKYOPS-63033 - HTTPD - Cortar espaços em branco de variáveis de ambiente do Dispatcher
* SKYOPS-65518 - HTTPD - Falha no validador se houver nomes de arquivo ilegais na pasta do Dispatcher
* SITES-19626 - Inicializações - Mesclar campos lastUpdate DAM-CFM no principal
* SITES-19251 - Site rápido - Assistente de criação - Suporte ao painel lateral da interface do administrador de sites quando a referência do tema não for igual ao nome do site
* SITES-15430 - Editor universal - Editor universal sob domínio AEM
* CQ-4344966 - WCM - Tradução - Criação de estrutura básica para atualização estrutural de sites e atualização da existente para ativos
* CQ-4347312 - WCM - Tradução - Crie um fluxo de trabalho para associar &quot;cq:translationsourcejcruuid&quot; em cópias de origem e idioma existentes
* CQ-4354509 - WCM - Tradução - Publicar eventos de tarefa de tradução [OSGi EventAdmin]
* SITES-16318 - Crosswalk - Criação baseada em AEM com Edge Delivery Services
* FORMS-9889: o usuário pode adicionar o URL do POST e a configuração da Nuvem ao configurar a ação Enviar para Enviar para o endpoint REST
* No editor de regras, os usuários podem:
   * FORMS-12160: valide um campo, painel ou formulário na seção Then da condição When.
   * FORMS-12570: redefina um campo, painel ou formulário na seção Then da condição When.
   * FORMS-11541: use objetos de campo e objetos globais no editor de regras por meio das funções personalizadas.
   * FORMS-11714: defina parâmetros como opcionais na função personalizada. Por padrão, os parâmetros declarados nas funções personalizadas são obrigatórios.
   * FORMS-11756: Use o armazenamento em cache para funções personalizadas a fim de melhorar o tempo de resposta ao recuperar a lista de funções personalizadas no editor de regras.
   * FORMS-12053: adicione uma instrução &quot;else&quot; na condição &quot;When&quot; para implementar condições aninhadas.
   * FORMS-11269: Use recursos modernos do JavaScript ES10, como funções de esquerda e seta na função personalizada para formulários baseados em componentes principais.

* FORMS-9014: Várias melhorias relacionadas à acessibilidade para o componente de Assinatura de rabisco


### Problemas corrigidos {#fixed-issues-15787}

* Correção de vários problemas de acessibilidade e internacionalização
* SITES-16966 - AEM: &quot;Sem versão!&quot; não localizado sequência de caracteres em Sites > Restaurar > Restaurar árvore
* SITES-16208 - O ContentFragmentModelIdentifier expõe uma propriedade de título enganosa
* SITES-18024 - Quando o cabeçalho If-Match estiver ausente, a resposta deverá ser 428
* SITES-18003 - O usuário que criou uma versão não é retornado corretamente
* SITES-17937 - O evento Fragmento de conteúdo criado é emitido antes que os pods do autor tenham sincronizado
* SITES-18029 - O pipeline de processamento de eventos trava quando notificado simultaneamente pela observação JCR
* SITES-17882 - Remoção do limite máximo de comprimento do campo de texto do fragmento do esquema
* SITES-19252 - Corrija inconsistências relacionadas ao código de status HTTP 406 e 415
* SITES-16964 - [Infraestrutura] A classificação por &quot;Modificado por&quot; não está funcionando corretamente
* SITES-17519 - Editor de propriedades de páginas do Sites - O nome longo da página está tornando os botões não clicáveis
* SITES-16852 - A API de publicação está publicando referências com o status NOVO
* SITES-18833 - Restrição de exclusividade não visível em pontos de extremidade OpenAPI
* SITES-15553 - Falha ao carregar o painel lateral do XF se o URL do XF contiver um seletor
* SITES-14340 - NPE em VersioningTimelineEventProvider.accept
* SITES-1605 - [Sites] DeletePageCommand lança NPE no caso de caminho de origem nulo
* SITES-16308 - [GB18030]: Mensagem de aviso exibida ao criar uma nova pasta Sites chamada com caracteres GB18030
* SITES-16304 - [GB18030]: Mensagem de aviso exibida ao criar uma nova pasta Fragmentos de experiência chamada com caracteres GB18030
* SITES-8769 - Melhore o desempenho do StyleImpl
* CQ-4343815 - Campaign - Direcionamento - A variante padrão de um teaser tem um url vazio
* CQ-4355889 - Campaign - Direcionamento - A solicitação para criar público-alvo falha com a configuração do IMS.
* SITES-12460 - Integração do Campaign - Integração do Campaign/AEM Cloud Service corrompida
* SITES-11571 - Fragmentos de conteúdo - API GraphQL - PersistedQueryServlet deve enviar 400s em URLs malformados
* SITES-19946 - Fragmentos de conteúdo - API do GraphQL - Os modelos não são mais verificados na inicialização
* SITES-1605 - Back-end principal - DeletePageCommand gera NPE no caso de caminho de origem nulo
* SITES-5429 - Back-end principal - ChildrenListServlet itemResourceType permite a execução direta do código
* SITES-15553 - Fragmentos de experiência - O painel lateral do XF falhou ao carregar se o URL do XF contiver um seletor
* SITES-13666 - Headless - Admin - registro de erros falso positivo &quot;com.adobe.cq.dam.cfm.headless.ui.impl.models.CFHomeCardModelImpl A ID da configuração não deve ser nula&quot;
* SITES-17164 - Editor de páginas - [Cloud, 6.5 Forms] A visualização do Editor de tema de AF está corrompida
* SITES-14340 - Interface do usuário do administrador de sites - NPE em VersioningTimelineEventProvider.accept
* SKYOPS-68611 - Sling - repoinit - Port sling repoinit criar correção de caminho na ramificação de manutenção
* CQ-4354678 - WCM - Tradução - Os trabalhos de tradução estão exportando conteúdo traduzido
* CQ-4355167 - WCM - Tradução - Não obtenção de pop-up ao marcar um trabalho de tradução como Concluído ou Arquivado
* CQ-4355913 - WCM - Tradução - Erros nos cartões de idioma do projeto de tradução
* GRANITE-47694 - Fluxo de trabalho - Não é possível obter subtarefas em um fluxo de trabalho na nuvem para usuário não administrador
* ASSETS-31097 - Assets Cloud - Logs preenchidos com avisos percorridos de índice para /bin/numberofentitiesinfolders.json
* ASSETS-35860 - Nuvem de ativos - Conversão incorreta de fuso horário na exibição em coluna do AEM Assets
* SITES-15260 - Interface clássica (herdada) - O Bulkedit adiciona propriedades VAZIAS na página se a importação de planilhas for usada
* SITES-16834 - Interface clássica (herdada) - Texto ausente após a edição de texto usando o Editor de itens em massa quando o texto contiver vírgulas
* SITES-17767 - Fragmentos de conteúdo - Administrador - Suporte a modelos cf permitidos também para pastas sem um nó jcr:content
* SITES-17683 - Fragmentos de conteúdo - Infraestrutura principal - Os fragmentos de conteúdo não são serializáveis com o exportador Jackson
* SITES-18797 - Fragmentos de conteúdo - Infraestrutura principal - Resultados do GraphQL duplicados após a personalização do índice
* SITES-18076 - Fragmentos de conteúdo - Infraestrutura principal - O texto de vários valores tem @TypeHint incorreto
* SITES-17856 - Fragmentos de conteúdo - Editor de modelos e modelos - Modelos CF não exibidos se a configuração não for uma pasta
* SITES-17071 - Infraestrutura principal - A página específica não exibe a versão na linha do tempo
* SITES-17285 - Componentes principais - O recorte de imagem em linha é diferente no Author e Publish no AEMaCS
* SITES-19187 - Componentes principais - Dois métodos de inserção de ativos no componente de imagem fornecem resultados diferentes na caixa de diálogo
* SITES-20077 - Componentes principais - Recorte de imagem em linha - o recorte está errado e as imagens estão indefinidas
* SITES-17211 - Fragmentos de experiência - Caixa de diálogo do seletor de caminho do componente Fragmentos de experiência que mostra fragmentos de experiência que são excluídos
* SITES-17894 - Inicializações - A promoção de inicializações aninhadas reverte o conteúdo da inicialização para uma versão de seu ancestral
* SITES-16042 - MSM - Live Copies - As anotações são exibidas incorretamente na Live Copy após implantações
* SITES-16691 - MSM - Live Copies - Quando o cliente seleciona &quot;implantação&quot; ou &quot;implantação para&quot; no ícone &quot;implantação&quot; em um componente, o botão &quot;continuar&quot; fica esmaecido.
* SITES-16733 - MSM - Live Copies - A página de índice do blueprint não pode ser implantada quando rep:policy aplicada ao nó
* SITES-17155 - MSM - Live Copies - Cabeçalhos e rodapés são traduzidos de volta para o inglês quando a Live Copy é renomeada
* SITES-17492 - MSM - Live Copies - Inconsistências de layout de Live Copy da página AEM
* SITES-19316 - MSM - Live Copies - O link de referência para o fragmento de experiência não é atualizado na cópia de idioma
* SITES-19347 - MSM - Live Copies - Mensagens de lentidão e interrupção do serviço do autor de produção - pods reiniciando com frequência - alertas de integridade
* SITES-19790 - MSM - Live Copies - Informações de visualização incorretas após a criação do Live Copy
* SITES-20086 - MSM - Live Copies - Implantação do MSM para CF no Assets implantará todas as live copies, mesmo se uma live copy for selecionada para implantação
* SITES-20088 - MSM - Live Copies - Problema em branco da página após a implantação do XF nas propriedades - AEM as a Cloud Service
* SITES-16854 - Editor de páginas - A sobreposição do destino de soltar cobre parsys em componentes com o recurso &quot;Selecionar painel&quot;
* CQ-4355563 - Projetos - O parâmetro de caminho está errado. Preenchendo &quot;?appId=aemshell&quot; para o script de pesquisa da caixa de entrada do projeto
* SITES-16876 - Site rápido - Implantação de tema - CSS e JS ausentes nas páginas de visualização 2
* SITES-18418 - Interface do administrador de sites - A funcionalidade Mostrar/Ocultar para o widget pathfield não funciona corretamente quando o campo é obrigatório
* SITES-19534 - Interface do administrador do Sites - Não é possível abrir a caixa de diálogo de permissões efetivas após a atualização do AEM 6.5.19
* SITES-19203 - Editor de modelo - Políticas de modelo editáveis Texto desalinhado e Estilos se sobrepõem botão de exclusão
* CQ-4354881 - WCM - Tradução - O caminho dos fragmentos de conteúdo é definido como origem (en-us) quando os fragmentos de conteúdo são traduzidos como parte de uma página
* CQ-4355289 - WCM - Tradução - Somente os primeiros 40 elementos são exibidos em Cloud Service de tradução
* CQ-4355866 - WCM - Tradução - Erro de lançamento do fluxo de trabalho de tradução para páginas existentes
* CQ-4355797 - Fluxo de trabalho - Não é possível usar a etapa de fluxo de trabalho OOTB
* GRANITE-48938 - Fluxo de trabalho - O autor que mostra os ativos paralisados em um estado de &quot;publicação pendente&quot;. Problema no novo cache de mapa de carga persistente.
* GRANITE-49036 - Fluxo de trabalho - Solicitação de recurso | Capacidade de agendar e configurar a limpeza de pacotes de fluxo de trabalho
* SITES-17393 - Extensões de fluxo de trabalho - A árvore de conteúdo de publicação falha ao usar iniciadores de fluxo de trabalho para cq:Tag
* SITES-17759 - Extensões de fluxo de trabalho - Fluxo de trabalho de ativação de árvore para tags que não funcionam no AEMaaCS
* FORMS-12411: em dispositivos Android, o plug-in `Maximum Number of Characters Validation` não está funcionando para o componente Caixa de texto de formulário adaptável.
* FORMS-13377: quando um usuário tenta adicionar a fonte personalizada e executa o pipeline para configurá-la, ocorre uma falha com o erro &quot;ContainersNotReady&quot;
* FORMS-13267: quando um usuário adiciona um componente suspenso do Formulário adaptável, a ID do menu suspenso não é gerada
* FORMS-13544: quando um usuário adiciona um componente de Contêiner de formulário adaptável com um layout de assistente, ele não funciona corretamente durante a criação do formulário
* FORMS-13091, FORMS-13414: se o usuário tentar configurar um URL de domínio personalizado no armazenamento de Blob do Azure, ocorrerá uma falha
* FORMS-13595: quando um usuário tenta salvar o formulário em um local diferente, o usuário não pode ver os botões &quot;Selecionar pasta&quot; e &quot;Cancelar&quot; se a resolução do navegador estiver definida como 100%. No entanto, a opção fica visível quando a resolução é definida como 75%
* FORMS-10952: Quando um usuário adiciona um componente Lista suspensa do Formulário adaptável a um Formulário adaptável e usa a propriedade &quot;Definir opções&quot; com base em várias regras personalizadas, a propriedade &quot;Definir opções&quot; funciona somente para a última regra
* FORMS-11471: o carregamento lento de um fragmento falha quando a chamada &quot;emitter.json&quot; falha devido a uma interrupção da rede.
* FORMS-11786: quando um usuário alterna entre meses no widget de calendário, o componente seletor de datas mostra uma linha extra.
* FORMS-12093, FORMS-12093: Quando um usuário marca a caixa de seleção Formulário adaptável para enviar um formulário, o valor incorreto com uma tag extra  `\` é armazenado na caixa de texto
* FORMS-11993: quando um usuário clica em uma imagem usando o botão &quot;Tirar uma foto&quot; no componente Anexo em um dispositivo iOS, todas as imagens são adicionadas à pasta com o mesmo nome
* FORMS-12555: quando um usuário tenta integrar o AEM Forms a uma plataforma de correio com um URL publicado do AEM, o AEM Forms não adiciona method=post durante a renderização da página. Esse problema ocorre mesmo se POST estiver definido na ação de envio com o URL. Isso faz com que a plataforma de correio não reconheça isso como um formulário
* FORMS-12938: Os formulários HTML5 não estão funcionando ou carregando corretamente no navegador Microsoft Edge com modo de compatibilidade do IE
* FORMS-12032: Quando um usuário envia um formulário, o caminho do caminho da ação de envio não está apontando corretamente
* FORMS-12445: valores incorretos são capturados no modelo de dados do formulário depois que a ordem das opções do botão de opção é alterada e o formulário é publicado.
* FORMS-12947: quando um usuário adiciona um novo idioma a um dicionário existente, ele não é mesclado ou adicionado
* FORMS-11363: quando um usuário envia um formulário pelo Workspace, um problema de exibição ocorre nas tabelas enquanto ele é renderizado
* FORMS-11756: quando um usuário adiciona os recursos do JavaScript ES6, como `let` e `const` nas funções personalizadas, o editor de regras não é aberto. Esta versão de manutenção inclui suporte para ES10
* FORMS-13164: Se o usuário gerar um PDF, linhas em branco inesperadas serão adicionadas a ele após o envio
* FORMS-13789: quando o usuário tenta gerar vários PDF, a API do lote de saída falha
* FORMS-11483: Quando um usuário converte PDF em PDF/A-2B ou PDF/A-3B, ele falha na conversão e mostra um erro de validação
* FORMS-10501: Quando um usuário chama o HSM, os documentos são certificados, mas ele não habilita o LTV
* FORMS-11546: quando um autor de formulário usa painéis repetidos em um Formulário adaptável, o atributo ARIA não aparece nas tags HTML. Isso melhora a acessibilidade de painéis repetidos do Formulário adaptável
* FORMS-11826: devido aos rótulos correspondentes Arial® labelledby e Arial®, os leitores de tela não conseguem distinguir esses dois. Para resolver o problema, o rótulo &quot;aria-labelledby&quot; é substituído por &quot;aria-descripbedby&quot; nos campos de formulário. F). Isso melhora a acessibilidade do Adaptive Forms
* FORMS-12626, FORMS-13094: os usuários não podem acessar a barra de ferramentas usando o teclado para salvar ou editar conteúdo na página do editor de formulários. Esse problema de acessibilidade foi corrigido
* FORMS-13102: Durante o processo de criação do formulário, os ícones disponíveis na página Forms e Documentos não têm recursos descritivos para indivíduos com deficiência diferente. Esse problema de acessibilidade foi corrigido

### Problemas conhecidos {#known-issues-15787}

* SITES-17934 - Fragmentos de conteúdo - A visualização falha devido à proteção DoS para uma grande árvore de fragmentos. Consulte [KB](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Recursos e APIs obsoletos {#deprecated-15787}

* [Descontinuação de credenciais JWT no console do Adobe Developer](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Veja [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md) saber o que foi descontinuado ou removido no AEM as a Cloud Service.

### Aviso de mudança {#change-notice-15787}

**Ações necessárias**

#### Defina a versão do Java CM para 11 {#set-java-version-11}

A nova versão do aem-sdk-api contém classes compiladas com um destino Java 11, que não é compatível com a versão 1.8 do JDK padrão do ambiente de compilação do Cloud Manager. Esta atualização requer que o Maven seja executado usando o JDK 11.

Os clientes são aconselhados a adicionar um `.cloudmanager/java-version` para a raiz do repositório Git com o conteúdo: `11`. Consulte [Ambiente de compilação / Configuração da versão do JDK Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologias integradas {#embedded-tech-15787}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.24.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
