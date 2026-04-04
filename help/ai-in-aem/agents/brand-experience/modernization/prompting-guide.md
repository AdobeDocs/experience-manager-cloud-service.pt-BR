---
title: Guia de solicitação do Agente de modernização de experiência
description: Este guia fornece dicas para o prompt eficaz do Agente de modernização de experiência e descreve o que suas habilidades fazem.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 4771606b-a327-48b3-b142-44e03e4dc41d
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---

# Guia de solicitação do Agente de modernização de experiência {#prompting-guide}

O Agente de modernização de experiência seleciona automaticamente a habilidade apropriada com base em solicitações em linguagem natural. Este guia fornece dicas para um prompt eficaz e descreve o que as habilidades fazem.

## Dicas gerais {#general-tips}

### Algumas habilidades dependem dos resultados de outras habilidades. {#dependency}

* Como a importação em massa precisa da infraestrutura de importação criada pela migração de página, migre pelo menos uma página antes de executar a importação em massa.
* Como o CSS de bloco faz referência aos tokens de design globais, conclua o design em todo o site antes de estilizar blocos individuais.

### A IA segue fluxos de trabalho estruturados e fará perguntas esclarecedoras quando precisar de mais informações. {#workflows}

* Confie no processo e responda a essas perguntas de qualificação à medida que elas surgirem.
* Não tente carregar todos os requisitos no prompt inicial.

### Crie arquivos de marcação no projeto para documentar regras, diretrizes, decisões de design ou restrições específicas do projeto. {#markdown-files}

* Esses arquivos de marcação (por exemplo, INSTRUCTIONS.md, CONTEXT.md) podem incluir convenções de nomenclatura de arquivo, regras de mapeamento de conteúdo ou diretrizes de marca.
* Ao iniciar uma nova conversa, peça ao agente para &quot;aquecer lendo a documentação do projeto&quot; para que ele carregue esse contexto antes de prosseguir com as tarefas.

### A janela de contexto do agente não é infinita. {#limited-window}

* Durante longas conversas, instruções mais antigas podem ser compactadas ou esquecidas.
* Se o agente parecer ter perdido o contexto, lembre-o dos pontos principais ou limpe o bate-papo e comece a usar um prompt de aquecimento para ler a documentação do projeto.

### Use o prompt iterativo para refinar os resultados. {#iterate}

* Se algo não parecer certo (por exemplo, cor de fundo incorreta em um bloco), peça ao agente para corrigir o problema específico em vez de começar novamente.

## Habilidades de criação e migração do site {#site-migration}

O Agente de modernização do site oferece muitas habilidades para criar novos sites do Edge Delivery Services e migrar sites existentes. Qualquer novo site do Edge Delivery ou projeto de migração deve aproveitar essas habilidades.

### Migrar um site ou uma página para o AEM {#migrate-a-site}

Use esse prompt ao migrar o conteúdo de um site existente para o Edge Delivery Services.

#### Exemplo de Prompts {#example-migrate}

* &quot;Migrar esta página: `https://example.com/about`
* &quot;Migrar estas páginas: URL1, URL2, URL3&quot;

#### O que saber {#wtk-migrate}

* A migração segue um fluxo de trabalho de sete etapas:
   1. O agente remove a página de origem.
   1. Identifica a estrutura da seção.
   1. Ele executa a análise de criação.
   1. Ele mapeia o conteúdo para variantes de bloco.
   1. Ele gera marcação.
   1. Ele cria infraestrutura de importação.
   1. Ele visualiza o resultado.
* O agente analisa as páginas usando uma hierarquia de dois níveis:
   * Primeiro, identifica os limites da seção (alterações no plano de fundo, deslocamentos de espaçamento)
   * Em seguida, identifica as sequências de conteúdo em cada seção.
* A análise de criação segue o [Modelo de David.](https://www.aem.live/docs/davidsmodel)
   * para cada sequência de conteúdo, ele verifica primeiro &quot;Um autor pode criar isso digitando normalmente?&quot;
   * O conteúdo padrão (cabeçalhos, parágrafos, listas, imagens integradas) é preferível aos blocos.
* O agente tenta reutilizar blocos existentes da biblioteca de blocos do repositório antes de criar outros novos.
   * Quando o conteúdo não pode ser mapeado para um bloco existente, ele cria novas variantes de bloco.
   * Você pode solicitar alterações, solicitar novas variantes ou ajustar mapeamentos interativamente.
* As variantes de bloco são rastreadas com metadados.
   * Ao migrar várias páginas, o agente carrega as variantes personalizadas existentes primeiro e as reutiliza quando o estilo é compatível (limite de similaridade de 70% com base na finalidade, nas cores, na tipografia, no espaçamento e no layout).
* O cabeçalho, a navegação e o rodapé são excluídos da migração de página. Elas são tratadas por habilidades específicas.
* Cada migração cria uma infraestrutura de importação (modelos de página, analisadores de blocos, transformadores) para importações futuras em massa.

### Importação em massa {#bulk-import}

Use este prompt para importar muitas páginas do mesmo modelo depois de concluir uma [migração inicial de página única.](#migrate-a-site)

#### Exemplo de Prompts {#example-prompts-bulk-import}

* &quot;Execute a importação em massa nestas páginas: URL1, URL2, URL3.&quot;
* &quot;Executar importação em massa em todas as páginas de produto.&quot;
* &quot;Importar estas páginas do blog em massa: URL1, URL2.&quot;

#### O que saber {#wtk-bulk-import}

* A importação em massa depende da infraestrutura de importação criada durante uma migração anterior de página única.
   * Isso inclui modelos de página (estrutura de seção), transformadores (limpeza DOM em todo o site) e analisadores (conversão de HTML em tabela específica de bloco).
* Você deve migrar pelo menos uma página representativa por modelo antes que a importação em massa possa ser executada.
* A importação em massa reutiliza a estrutura e os mapeamentos estabelecidos durante a migração de página única.
   * Ele não infere modelos do zero.
* Os transformadores operam em todo o DOM antes e depois da análise. Os analisadores operam no nível de bloco individual.
* Todos os analisadores são validados antes que a importação em massa possa continuar.
* Um modelo corresponde a uma configuração de importação em massa.
   * Não há suporte para a combinação de modelos em uma única execução.

#### Fluxo de trabalho típico {#typical-workflow}

O fluxo de trabalho recomendado é iterativo: valide em um conjunto pequeno primeiro e, em seguida, dimensione.

1. **Execute primeiro uma migração de página única.** - Migre uma página representativa para o modelo que você planeja importar em massa.
   * Isso cria a infraestrutura de importação necessária.
1. **Execute a importação em massa em um pequeno conjunto de páginas.** - Peça ao agente para executar a importação em massa e fornecer uma pequena lista de URLs que seguem o mesmo modelo.
1. **Revise e refine os resultados.** - Inspecione as páginas importadas.
   * Se algo parecer incorreto, peça ao agente para ajustar analisadores, transformadores ou lógica de importação.
1. **Aumentar.** - Quando os resultados parecerem corretos, forneça a lista completa de URLs.
   * O agente reutilizará a mesma lógica de importação e executará uma importação em massa em escala.

### Rascunho de páginas da Web {#scraping-webpages}

Use esse prompt para extrair conteúdo, metadados e imagens de um URL de origem para análise ou migração.

#### Exemplo de Prompts {#example-scraping}

* &quot;Raspar esta página para análise: `https://example.com`&quot;
* &quot;Extrair conteúdo de `https://example.com/product`&quot;

#### O que saber {#wtk-scraping}

* Normalmente, esse prompt é chamado automaticamente como a primeira etapa da migração da página.
* O conteúdo oculto via CSS também é capturado se presente no DOM.
* Imagens carregadas lentamente e conteúdo renderizado do lado do cliente são tratados ao rolar pela página no Chromium headless e permitir que os scripts sejam executados.
* Imagens WebP/AVIF/SVG são convertidas em PNG para compatibilidade.
* Os metadados são extraídos, incluindo título, descrição, tags Open Graph, dados estruturados JSON-LD e URL canônico.
* As imagens no DOM são fixas.
   * background-image é convertido em img.
   * Os elementos da figura estão desenrolados
   * srcset é resolvido como src
   * URLs relativos são convertidos em absolutos
   * O SVG em linha para é convertido em arquivos img.
* Caminhos de documentos limpos são gerados (minúsculas sem extensão `.html`).
* As seguintes saídas são produzidas:
   * `screenshot.png`
   * `cleaned.html` (sem scripts/estilos)
   * `metadata.json`
   * Pasta `images/` com cópias locais
* Os usuários podem perguntar sobre dimensões de captura de tela e solicitar tamanhos específicos de dispositivos (dispositivos móveis, desktop) para extração de conteúdo.
* Extrair conteúdo em vários pontos de interrupção aumenta o tempo de processamento.

### Migração do projeto {#design-migration}

Use este prompt para extrair e aplicar o design visual de um site de origem ao Edge Delivery Services.

#### Exemplo de Prompts {#example-design}

* &quot;Migrar o design de `https://example.com`&quot;
* &quot;Extrair tokens de design&quot;
* &quot;Estilo do bloco herói&quot;

#### O que saber {#wtk-design}

* A migração do projeto tem duas fases:
   1. A Fase 1 (em todo o site) extrai o seguinte para `styles/styles.css`:
      * Paleta de cores global e cores de ênfase
      * Sistema de tipografia (fontes, tamanhos, pesos)
      * Sistema de espaçamento (preenchimento, margens, espaços)
      * Planos de fundo da seção (claro, escuro, colorido)
      * Estilos básicos de componentes (botões, links, imagens)
      * Saídas para
   1. A Fase 2 migra estilos de bloco individuais e cria CSS específico de bloco no `/blocks/{name}/{name}.css`.
* O estilo de bloco (fase 2) requer que o design em todo o site (fase 1) seja concluído primeiro.
   * O sistema de design global fornece propriedades personalizadas de CSS que bloqueiam a referência.
* Tempo estimado:
   * Fase 1: 5 a 10 minutos
   * Fase 2: 10 a 15 minutos
* As solicitações ambíguas são padronizadas para concluir a migração (ambas as fases).

### Bloco Crítico {#block-critique}

Use esse prompt para validar e refinar blocos migrados individuais e garantir a precisão visual em relação ao site original.

#### Exemplo de Prompts {#example-block-critique}

* &quot;Bloco de herói da crítica&quot;
* &quot;Validar cartões personalizados de bloco&quot;

#### O que saber {#wtk-block-critique}

* A crítica de bloco compara um bloco migrado com sua origem original e aplica iterativamente correções CSS até que uma similaridade visual de 85% seja alcançada ou três iterações sejam concluídas.
* A habilidade exige que o bloco seja criado primeiro pela migração de página.
* Uma crítica de bloco segue um fluxo de trabalho de seis etapas:
   1. Ele captura o bloco original da página de origem usando um seletor XPath.
   1. Ele inicializa a sessão crítica.
   1. Ele inspeciona o bloco original (capturas de tela, estilos, HTML).
   1. Ele inspeciona o bloco migrado.
   1. Ele compara elementos e gera uma pontuação de similaridade com correções CSS.
   1. Ela aplica correções e inspeciona novamente até que o target de 85% seja atingido.
* Cada iteração exibe um relatório de crítica completo com todas as diferenças, aplica todas as correções CSS (priorizadas por impacto visual), verifica na pré-visualização, inspeciona novamente e mostra métricas de melhoria.
* Use a crítica de bloco após a [migração de design](#design-migration) ser concluída.

### Crítica da página {#page-critique}

Use este prompt para validar páginas migradas inteiras para fidelidade visual de página inteira em relação ao site original.

#### Exemplo de Prompts {#example-page-critique}

* &quot;Crítica à página sobre&quot;
* &quot;Validar a página migrada em relação a `https://example.com/about`&quot;

#### O que saber {#wtk-page-critique}

* A crítica de página realiza uma comparação visual de página inteira entre a página original e a migrada, iterando até atingir uma meta de similaridade de 85% ou três iterações serem concluídas.
* Uma crítica de página tem um fluxo de trabalho de cinco etapas:
   1. Inicializa uma sessão crítica.
   1. Ele inspeciona todos os elementos na página original.
   1. Ele inspeciona todos os elementos na página migrada.
   1. Ele compara e gera uma pontuação de similaridade com correções CSS priorizadas.
   1. Ela aplica correções e inspeciona novamente até que o target de 85% seja atingido.
* Uma crítica de página precisa do URL da página de origem e do caminho migrado (por exemplo, &quot;/about&quot;) como entrada.
* Use críticas de página ao validar a fidelidade geral da página ou ao validar vários blocos simultaneamente.
* [Use a crítica de bloco](#block-critique) para validação focalizada em componentes específicos.
* Recomenda-se o seguinte workflow:
   1. Migrar uma página.
   1. Aplicar um design.
   1. Executar uma crítica de bloco nos blocos principais
   1. Execute uma crítica de página de aplicativo para validação completa.

### Migração de bloco de Figma {#figma-block-migration}

Use este prompt para migrar um bloco do design do Figma para o Edge Delivery Services.

Observe que você deve configurar os detalhes do Figma no [Console de Modernização da Experiência](/help/ai-in-aem/agents/brand-experience/modernization/console.md) para usar esse prompt.

#### Exemplo de Prompts {#example-figma}

* &quot;Migrar o bloco `https://figma.com/design/{fileKey}?node-id={nodeId}` para o Edge Delivery Services&quot;
* &quot;Migrar `{blockName}` de `https://figma.com/file/{fileKey}` para Edge Delivery Services&quot;

#### O que saber {#wtk-figma}

* Essa habilidade migra um bloco de cada vez, não páginas inteiras ou arquivos Figma completos.
* Para obter melhores resultados:
   * Selecione o bloco específico que deseja migrar no Figma e copie seu link (com `node-id`) ou nome.
   * Forneça o parâmetro `node-id` na URL para direcionar o bloco exato.
* Quando você executa essa habilidade, as seguintes etapas são executadas automaticamente no ambiente hospedado:
   1. **Descoberta de estrutura de bloco** — O agente lê o nó Figma para compreender camadas e componentes.
   1. **Extração de estilo global** — O agente extrai cores, tipografia e espaçamento para `styles/styles.css` como propriedades personalizadas de CSS (tokens de design).
   1. **Criação de estilo específico de bloco** — O agente cria propriedades personalizadas CSS adicionais específicas para o bloco que está sendo migrado.
   1. **Mapeamento para blocos existentes** — O agente identifica o bloco correspondente mais próximo na biblioteca de blocos do projeto e cria uma variante personalizada.
   1. **Geração de CSS** — o agente grava estilos que fazem referência às propriedades personalizadas de CSS extraídas, garantindo a consistência do design.
   1. **Download de ativos** — o agente salva imagens e ícones do Figma no espaço de trabalho do ambiente hospedado.
   1. **Geração de conteúdo do Edge Delivery Services** — O agente cria o arquivo de Markdown seguindo a estrutura de bloco do EDS
   1. **Validação de saída** — o agente pré-visualiza o resultado e executa uma comparação visual com o design original do Figma.
* A habilidade lê primeiro os metadados (etapa 1) para entender a estrutura e, em seguida, extrai o contexto detalhado do design (etapas 2 a 5).
   * Essa abordagem em fases evita problemas com arquivos Figma grandes ou complexos.
* Essa habilidade tem uma abordagem de estilo.
   * Todos os estilos são extraídos como propriedades personalizadas de CSS (tokens de design) antes que qualquer CSS seja gravado.
   * Isso garante que o bloco migrado permaneça consistente com seu sistema de design.
* O prompt requer a URL do Figma (com `fileKey` e `node-id` opcional) ou uma chave de arquivo do Figma diretamente como entrada.

### Configuração da navegação {#navigation-setup}

Use este prompt para configurar ou migrar a navegação do site.

#### Exemplo de Prompts {#example-navigation}

* &quot;Configurar navegação de `https://example.com`&quot;
* &quot;Corrigir o menu de navegação&quot;

#### O que saber {#wtk-navigation}

* A navegação do Edge Delivery Services impõe uma estrutura de três seções (executada por `header.js`):
   1. **Marca** (seção 1): link para o logotipo e marca primária
   1. **Seções** (seção 2): menu de navegação principal com menus suspensos opcionais
   1. **Ferramentas** (seção 3): links de utilitários (inscrição, logon, carrinho)
* O conteúdo de navegação reside em `nav.md` no diretório raiz.
* Seções são separadas por marcadores (`---`).
* Itens em negrito (`**Text**`) com listas aninhadas criam menus suspensos.
* Os links na navegação podem ser renderizados como botões devido ao comportamento de quebra automática da Criação de documento.
   * O bloco de cabeçalho inclui código para retirar classes de botão de links de navegação.

## Recursos de desenvolvimento de blocos {#block-development-capabilities}

Esses prompts são usados para criar e evoluir blocos, fornecendo valor contínuo além da criação ou migração inicial do site.

### Desenvolvimento de bloco {#block-development}

Use este prompt para criar novos blocos ou modificar os existentes.

#### Exemplo de Prompts {#example-block-development}

* &quot;Criar um bloco de depoimentos&quot;
* &quot;Adicionar uma variante de plano de fundo de vídeo ao bloco principal&quot;

#### O que saber {#wtk-block-development}

* O agente segue o CDD (Content-Driven Development, desenvolvimento orientado por conteúdo), um processo obrigatório para todo o desenvolvimento de Edge Delivery Services.
   * Ele perguntará sobre modelos de conteúdo e testará o conteúdo antes de gravar o código.
* A filosofia da CDD é que as necessidades do autor vêm antes das necessidades do desenvolvedor.
   * Os modelos de conteúdo devem ser intuitivos para os autores, mesmo que isso signifique um código de decoração mais complexo.
* A criação do conteúdo de teste primeiro fornece:
   * Capacidade de teste imediato
   * Links de validação de PR para verificações de PSI
   * Documentação dinâmica para autores
   * Detecção de casos de borda que falham das abordagens code-first
* O agente procurará blocos semelhantes na [Coleção de Blocos](https://www.aem.live/developer/block-collection) e na [Parte do Bloco](https://www.aem.live/developer/block-party/) antes da implementação, para encontrar padrões e códigos reutilizáveis.
* Ignorar o CDD somente para ajustes comuns somente em CSS (mas ainda identificar o conteúdo do teste para validação).

### Modelagem de conteúdo {#content-modeling}

Use esse prompt para projetar a estrutura da tabela com a qual os autores trabalham ao criar conteúdo em bloco.

#### Exemplo de Prompts {#example-modeling}

* &quot;Projetar um modelo de conteúdo para um bloco de depoimentos&quot;
* &quot;Qual é o melhor modelo de conteúdo para este carrossel?&quot;

#### O que saber {#wtk-modeling}

* O Edge Delivery Services tem quatro tipos de modelo canônico:
   * **Independente:** elementos visuais/narrativos distintos (herói, citação de bloqueio)
      * Tabela única com conteúdo de bloco
   * **Coleção:** conteúdo semiestruturado repetitivo (cartões, carrossel)
      * Tabela com padrão de linha de repetição
   * **Configuração:** conteúdo dinâmico ou orientado por API onde os controles de configuração são exibidos (listagem de blog, resultados de pesquisa)
      * Tabela com linhas de configuração de valor-chave.
   * **Bloqueado Automaticamente:** estruturas complexas que os autores criam como seções/conteúdo padrão, então são transformadas (guias, incorporações do YouTube)
* Há um limite de quatro células por linha.
   * Agrupar elementos relacionados em células.
* Prefira variantes de bloco a células de configuração para diferenças de estilo.
* [Siga a Lei do Postel](https://en.wikipedia.org/wiki/Robustness_principle): seja flexível quanto à estrutura de entrada.
   * Um bloco herói deve funcionar independentemente de o conteúdo estar em uma célula, dividido em duas células ou em linhas separadas.
* Normalmente, essa habilidade é chamada automaticamente pelo Desenvolvimento orientado por conteúdo durante a criação do bloco.

### Localizando blocos de referência {#reference-blocks}

Use esse prompt para procurar implementações existentes para usar como pontos de partida.

#### Exemplo de Prompts {#example-reference}

* &quot;Localizar blocos semelhantes a uma tabela de preços&quot;
* &quot;Quais blocos estão disponíveis para depoimentos?&quot;
* &quot;Parte do bloco de pesquisa para uma implementação de guias&quot;

#### O que saber {#wtk-reference}

* A [Coleção de Blocos](https://www.aem.live/developer/block-collection) é mantida pela Adobe e testada para práticas recomendadas, modelagem de conteúdo excelente, alto desempenho e acessibilidade.
   * É limitado aos blocos comumente necessários. Comece aqui.
* O [Bloco de Partes](https://www.aem.live/developer/block-party/) é conduzido pela comunidade e oferece uma variedade mais ampla, incluindo abordagens experimentais.
   * Ele também inclui plug-ins do sidekick, ferramentas de build (webpack, vite, sass) e integrações.
   * Use quando a Coleção de blocos não tiver o que você precisa.
* Pense em nomes alternativos ao pesquisar
   * Perguntas frequentes = Accordion
   * Galeria = carrossel/apresentação de slides
   * Navegação = menu/cabeçalho
* A Parte do Bloco só retorna entradas aprovadas/com curadoria.

### Pesquisando documentação {#searching-documentation}

Use este prompt para encontrar informações sobre os recursos do Edge Delivery Services ou orientação de implementação.

#### Exemplo de Prompts {#example-documentation}

* &quot;Como implementar o carregamento lento no Edge Delivery Services?&quot;
* &quot;Pesquisar os documentos por metadados de seção&quot;

#### O que saber {#wtk-documentation}

* Ele pesquisa especificamente a documentação do [aem.live](https://aem.live) (documentos e publicações do blog).
* Use palavras-chave específicas (&quot;decoração de blocos&quot;,&quot;plug-in sidekick&quot;,&quot;metadados&quot;) em vez de termos genéricos (&quot;aem&quot;,&quot;site&quot;,&quot;como criar&quot;).
* Para exemplos de código e implementações de referência, use &quot;localizar blocos de referência&quot;.
* Os dez principais resultados mais relevantes retornados por padrão.

### Testes {#testing}

Use esse prompt para validar as alterações de código antes de abrir uma solicitação de pull.

#### Exemplo de Prompts {#example-testing}

* &quot;Test the new cards block&quot; (Testar o novo bloco de placas)
* &quot;Executar os testes antes que eu abra uma PR&quot;

#### O que saber {#wtk-testing}

* Os testes seguem uma filosofia de &quot;valor vs. custo&quot;, na qual você cria e mantém testes quando o valor excede o custo.
   * **Testes de guardião** (testes de unidade) são para utilitários lógicos pesados, processamento de dados, integrações de API. Elas são rápidas, fáceis de manter e capturam regressões no código reutilizado.
   * **Testes de descarte** (testes de navegador) são para transformações DOM e validação visual. Use para validar a implementação, capturar capturas de tela para revisão de PR e, em seguida, descartar.
* Os testes de descarte entram em `test/tmp/` e testam o conteúdo em `drafts/tmp/` (ambos gerados por gig).
* Antes de abrir uma PR, verifique se:
   * Os testes existentes foram bem-sucedidos
   * Testes de unidade são escritos para a nova lógica
   * Validação do navegador concluída
   * Todas as variantes são testadas
   * O comportamento responsivo é verificado
   * Passes para listas

### Depuração {#debugging}

Use este prompt para solucionar problemas com blocos, imagens, CSS ou pré-visualização.

#### Exemplo de Prompts {#example-debugging}

* &quot;Depurar por que as imagens são exibidas como sobre :error&quot;
* &quot;Corrigir o bloco herói que não está sendo renderizado&quot;
* &quot;Por que minhas alterações não são exibidas na visualização?&quot;

#### O que saber {#wtk-debugging}

* Problemas comuns têm padrões conhecidos:
   * **Imagens mostrando &quot;sobre:error&quot;**: geralmente falta a chamada `createOptimizedPicture` no bloco JS, ou chamada antes da reestruturação de DOM
   * **Blocos não renderizados**: verifique o formato do nome do bloco no Markdown e verifique se o bloco tem arquivos `.js` e `.css` em `blocks/`.
   * **O CSS não está carregando**: verifique os caminhos do arquivo, verifique se o arquivo CSS existe e verifique a guia Rede no navegador.
   * **As alterações não aparecem**: a sincronização de código leva de 3 a 5 segundos. Experimente atualizar permanentemente (Ctrl+Shift+R).
* O agente verifica sistematicamente cada camada:
   1. Arquivos do Source
   1. Saída renderizada
   1. Código de bloco
   1. Console do navegador
* O agente pode verificar visualizações locais em `http://localhost:3000`.
