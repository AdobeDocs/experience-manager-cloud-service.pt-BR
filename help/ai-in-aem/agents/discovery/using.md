---
title: Visão geral do Discovery Agent
description: Saiba como usar o Discovery Agent para fornecer conteúdo relevante do AEM sob demanda por meio de solicitações naturais e conversacionais para obter uma experiência de descoberta simplificada e sem cliques.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: d4b5b0e606e9e680b0950538cce267d094a57d13
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---


# Agente de Descoberta {#discovery-agent}

O Discovery Agent fornece conteúdo do AEM sob demanda por meio de solicitações naturais e conversacionais para uma experiência de detecção simplificada e sem cliques. Ele faz pesquisas de forma inteligente em Assets, Fragmentos de conteúdo e Forms adaptável para fornecer materiais relevantes, como imagens, vídeos, documentos PDF, artigos e modelos de formulário. Usando a linguagem natural, você pode pesquisar conteúdo sem criar consultas complexas ou aplicar filtros na interface do AEM Assets. Com base em seu prompt, o agente retorna resultados preparados juntamente com metadados de ativos e URLs de entrega, prontos para serem incorporados em outros aplicativos.

Alguns dos principais benefícios do Discovery Agent incluem:

* **Descoberta de Conteúdo Unificado**: acesse todos os tipos de conteúdo do AEM, como imagens, vídeos, documentos do PDF, artigos e formulários em uma única interface conversacional.

* **Planejamento mais rápido de campanha**: colete rapidamente visuais e formulários para campanhas de marketing em canais de email, da Web e sociais.

* **Produtividade aprimorada**: reduza o tempo gasto navegando em repositórios ou filtrando metadados por meio de pesquisa automatizada e baseada em intenções.

* **Utilização de conteúdo consistente**: garante a reutilização de ativos e fragmentos aprovados, mantendo a consistência da marca entre canais.

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Habilidades {#skills-discovery-agent}

O Agente de descoberta oferece as seguintes habilidades:

* **Descoberta de conteúdo de linguagem natural**\
  O Discovery Agent permite que os usuários encontrem ativos, fragmentos de conteúdo e formulários adaptáveis relevantes no Adobe Experience Manager (AEM) usando prompts de linguagem natural simples — sem a necessidade de consultas de pesquisa complexas.

* **Descoberta de ativos baseada em marcas**

  O Discovery Agent usa prompts de linguagem natural para encontrar ativos associados a tags específicas no repositório do AEM, ajudando os usuários a acessar rapidamente o conteúdo organizado ou não de acordo com a taxonomia da organização.

* **Descoberta de conteúdo com base em pasta:**\
  O Discovery Agent pode identificar ativos interpretando prompts de idioma natural que fazem referência a nomes de pastas no AEM. Os usuários podem simplesmente mencionar a pasta em seu prompt, sem navegar manualmente pelo repositório, reduzindo significativamente o número de cliques necessários para localizar o conteúdo correto.

## Personas {#personas-discovery-agent}

### Gerentes de campanha {#campaign-managers}

O Discovery Agent permite que os gerentes de campanha identifiquem e reutilizem rapidamente conteúdo confiável e de alto desempenho para ideação.

### Profissionais de marketing de canal {#channel-marketers}

O Discovery Agent permite que os profissionais de marketing de canal encontrem ativos relevantes com eficiência para criar experiências coesas e de vários canais.

### Bibliotecários DAM {#dam-librarians}

Os bibliotecários do DAM podem sinalizar ativos que não têm os padrões de metadados definidos pela organização, apoiando a governança consistente e garantindo que os ativos permaneçam completos e prontos para uso em todos os canais.

### Agências e parceiros {#agencies-partners}

As agências e os parceiros podem encontrar facilmente ativos aprovados pela marca na Content Hub e reutilizá-los para acelerar o trabalho criativo e, ao mesmo tempo, manter-se alinhados aos padrões da marca.

## Como acessar o Discovery Agent? {#access-discovery-agent}

Você pode acessar os AEM Business Agents por meio do Assistente de IA. Faça logon em experience.adobe.com e você pode começar a interagir com o AI Assistant especificando seu prompt no idioma natural usando a caixa de pesquisa:

![Agente de Descoberta de Acesso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

Para obter informações sobre o terminal MCP para acessar o Discovery Agent, entre em contato com o Suporte da Adobe.

## Casos de uso comuns e prompts de amostra {#use-cases-prompts}

### Ativos {#discovery-agent-use-cases-assets}

**Descoberta de ativos baseada em marcas**

O Discovery Agent usa prompts de linguagem natural para encontrar ativos associados a tags específicas no repositório do AEM, ajudando os usuários a acessar rapidamente o conteúdo organizado de acordo com a taxonomia de sua organização.

Exemplo de prompt:

Mostrar imagens marcadas `office` na pasta `WKND`.

**Descoberta de conteúdo com base em pasta:**\
O Discovery Agent pode identificar ativos interpretando prompts de idioma natural que fazem referência a nomes de pastas no AEM. Os usuários podem simplesmente mencionar a pasta em seu prompt, sem navegar manualmente pelo repositório, reduzindo significativamente o número de cliques necessários para localizar o conteúdo correto.

Exemplos de prompts:

* Há algum svgs na pasta `WKND`?
* Mostrar ativos modificados após `Nov 1 2025` na pasta `WKND`.
* Listar `lifestyle` imagens na pasta `WKND`.

**Descoberta de ativos baseada em resolução e formato**

O Discovery Agent pode identificar ativos que atendem a requisitos específicos de qualidade, como formato de arquivo ou resolução mínima, permitindo que os usuários localizem rapidamente os visuais do produto que estão prontos para entrega e reutilização de alta qualidade em todos os canais.

Exemplo de prompt:

Encontre imagens PNG da embalagem do produto com pelo menos 2000 px de largura.

**Descoberta de conteúdo com base em orientação**

O Discovery Agent pode filtrar ativos reconhecendo atributos visuais, como a presença de pessoas e a orientação de uma imagem. Isso permite que os usuários restrinjam rapidamente o conteúdo aos visuais mais relevantes, sem aplicar manualmente vários filtros no AEM.

Exemplo de prompt:

Mostrar ativos com a pessoa na orientação paisagem.

### Fragmentos de conteúdo {#discovery-agent-use-cases-content-fragments}

O Discovery Agent ajuda os usuários a localizar rapidamente os fragmentos de conteúdo corretos, interpretando referências de linguagem natural a nomes de campanha, marcas de produtos, status da publicação e atividade de criação recente. Ele permite que as equipes apresentem fragmentos prontos para campanha e visualizem conteúdo específico da marca, tudo sem navegar manualmente pelas pastas ou aplicar vários filtros no AEM.

Exemplos de prompts:

* Mostrar fragmentos de conteúdo para criar a campanha de oferta WKND.

* Mostre o fragmento de conteúdo para bebida americana.

* Mostre-me todos os fragmentos de conteúdo publicados para bebidas WKND.

* Listar todos os fragmentos de conteúdo criados nas últimas 2 semanas.

### Forms {#discovery-agent-use-cases-forms}

O Discovery Agent ajuda a encontrar rapidamente formulários adaptáveis usando prompts de linguagem natural. Ele faz pesquisas no conteúdo e nos metadados do formulário para encontrar correspondências com base em palavras-chave de seus prompts. Isso significa que você pode descobrir formulários relevantes com êxito, mesmo se os termos de pesquisa não estiverem no título ou na descrição do formulário.

Exemplos de prompts:

* Mostre-me todos os formulários de solicitação de empréstimo.
* Localize formulários para candidatar-se a um cargo.
* Localizar formulários de contato.
* Estou procurando formulários de integração de funcionários.
* Mostre-me formulários de solicitação de cartão de crédito.

Observação: no momento, a descoberta de formulários é compatível apenas com formulários do Edge Delivery Services e a pesquisa baseada em tags não está disponível para formulários no momento.

## Resultados da pesquisa {#discovery-agent-search-results}

### Ativos {#discovery-agent-search-results-assets}

O Discovery Agent retorna os 20 resultados principais de cada consulta, classificados por relevância para garantir que as correspondências exatas apareçam primeiro. O agente combina consultas orientadas por metadados com pesquisa semântica para reunir um conjunto focalizado de correspondências prováveis e, em seguida, usa um LLM para classificá-las com base na intenção do usuário. Essa abordagem combinada fornece resultados precisos e sensíveis ao contexto sem depender totalmente de uma correspondência direta de palavra-chave.

Cada resultado inclui o nome do ativo junto com os principais metadados do ativo, como o caminho do ativo, criador, data de criação, título, descrição, formato, último modificador, data da última modificação, tamanho do arquivo, dimensões, [URL do Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) e marcas associadas. Se um ativo estiver no estado aprovado, os resultados também incluirão o [Dynamic Media com OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md).

Você pode clicar no caminho do ativo para navegar facilmente até o local do ativo no AEM.

![Pesquisar ativos usando o Agente de Descoberta](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

Você pode usar esses detalhes do ativo para avaliar rapidamente se um ativo atende aos requisitos sem navegar até cada ativo para exibir esses detalhes.

>[!NOTE]
>
>O campo [URL do Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) é exibido nos resultados da pesquisa somente se o ativo for publicado e você tiver uma licença válida do Dynamic Media. Da mesma forma, o campo [Dynamic Media com OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md) será exibido somente se você tiver uma licença válida do Dynamic Media e o Dynamic Media com OpenAPI estiver habilitado para sua instância do AEM as a Cloud Service.

### Fragmentos de conteúdo {#discovery-agent-search-results-content-fragments}

O Agente de descoberta fornece recursos de pesquisa de texto completo para Fragmentos de conteúdo, retornando os 20 principais resultados que melhor correspondem ao prompt especificado. Cada resultado inclui o nome do Fragmento do conteúdo junto com campos de metadados principais, como caminho do Fragmento do conteúdo, criador, data de criação, variações, último modificador e campos de data da última modificação.

![Pesquisar fragmentos de conteúdo usando o Agente de Descoberta](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

Você pode clicar no caminho do Fragmento de conteúdo para navegar facilmente até o local do Fragmento de conteúdo no AEM.

## Solicitação de práticas recomendadas {#prompting-best-practices-discovery-agent}

Especifique detalhes concisos nos prompts em seu idioma, para que o agente possa retornar resultados precisos e relevantes. Quanto mais claramente você descrever o que está procurando, melhor o agente poderá refinar e restringir a saída. Por exemplo, você pode:

* Defina metadados de ativos, como tags, nomes de pastas, datas de criação, status de publicação, nomes de autores em suas solicitações para filtrar ativos.

* Use os metadados específicos da sua organização, como categorias (tênis de corrida, eletrônicos), estações (outono, primavera), eventos (sexta-feira preta, lançamento de produto) e canais (Web, email, impressão) para filtrar ainda mais o conteúdo.

