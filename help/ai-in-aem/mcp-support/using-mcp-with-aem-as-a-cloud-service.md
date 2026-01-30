---
title: Uso do MCP com o AEM as a Cloud Service
description: Saiba como usar o Protocolo de contexto de modelo com o AEM as a Cloud Service
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3ff5ef0be78f5f5a61c81c8ab0388b56fa134047
workflow-type: tm+mt
source-wordcount: '2016'
ht-degree: 0%

---


# Uso do MCP com o AEM as a Cloud Service {#using-mcp-with-aem-as-a-cloud-service}

## Introdução {#introduction}

Muitas equipes do AEM agora trabalham em IDEs e aplicativos baseados em chat, como Cursor, ChatGPT, Anthropic Claude e Microsoft Copilot Studio. Esses aplicativos oferecem suporte ao protocolo MCP, que permite que os aplicativos exponham ferramentas de back-end a LLMs (Large Language Models, modelos de linguagem grande) de maneira padronizada.

Com a integração do MCP do AEM, diferentes perfis podem colaborar em torno do mesmo conteúdo:

* **Desenvolvedores** podem orquestrar operações de conteúdo e fluxos de trabalho a partir de seus aplicativos de bate-papo ou IDE
* **Os profissionais** e os arquitetos de conteúdo podem gerenciar sites, fragmentos de conteúdo e ativos com a assistência da IA enquanto permanecem dentro do modelo de permissão existente da AEM.

>[!IMPORTANT]
>
> Para cenários que modificam ou excluem conteúdo, os profissionais devem usar a interface do Assistente de IA em vez de chamar as ferramentas MCP diretamente, pois os Agentes do AEM executados pelo Assistente de IA incluem salvaguardas integradas.
>

Este artigo explica o que a funcionalidade MCP do AEM oferece, quais aplicativos MCP são compatíveis, como configurá-los e como usá-los na prática.

## Por que o MCP é útil para clientes do AEM {#why-mcp-is-useful-for-aem-customers}

Aplicativos modernos de IDE e chat usam MCP como uma maneira de um LLM chamar ferramentas expostas por trás dos servidores MCP. Em vez de escrever código em relação às especificações de API de baixo nível, os clientes podem descrever sua intenção em linguagem natural (*&quot;atualizar o banner principal desta campanha em todas as páginas&quot;*) e permitir que o LLM chame as ferramentas de MCP apropriadas, que, por sua vez, interagem com as APIs do AEM.

Os principais benefícios incluem:

* **Interação em linguagem natural em vez da canalização de API**
As ferramentas do MCP descrevem quais operações estão disponíveis e como chamá-las. O LLM usa esses esquemas para decidir quais ferramentas chamar e com quais parâmetros.
* **Experiência consistente entre aplicativos**
As mesmas ferramentas de MCP do AEM podem ser usadas a partir de vários aplicativos compatíveis com MCP, permitindo que as equipes trabalhem onde são mais produtivas enquanto chamam os mesmos recursos subjacentes do AEM.
* **Segurança e governança preservadas**
As solicitações para ferramentas MCP do AEM são executadas sob a identidade do usuário autenticado e cada ferramenta impõe as permissões AEM existentes do usuário. As operações assistidas por IA seguem as mesmas regras de acesso que o trabalho manual no AEM.

## Servidores MCP fornecidos pela AEM {#mcp-servers-provided-by-aem}

O AEM expõe os servidores MCP como pontos de extremidade HTTP. Os endpoints listados abaixo são relativos a:

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### Servidores MCP {#mcp-servers}

| **Servidor MCP** | **Ponto de extremidade** | **Descrição** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **Conteúdo** | `/content` | Todas as operações de conteúdo de baixo nível, incluindo criação, leitura, atualização e exclusão (CRUD) de páginas, fragmentos e ativos. |
| **Conteúdo (somente leitura)** | `/content-readonly` | Operações de conteúdo somente leitura (Obter, Listar/Pesquisar) para páginas, fragmentos e ativos. |

As ferramentas específicas expostas por cada servidor MCP podem evoluir com o tempo. Na prática, você pode solicitar que o aplicativo habilitado para MCP descubra ferramentas por meio de um prompt como:

*&quot;Lista todas as ferramentas MCP do AEM disponíveis neste servidor e descreve o que elas fazem.&quot;*

O cliente MCP usará o protocolo MCP para recuperar a lista de ferramentas e os esquemas que o LLM poderá usar.

## Aplicativos MCP suportados {#supported-mcp-applications}

Os servidores MCP da AEM foram projetados para funcionar com um conjunto definido de aplicativos compatíveis com MCP. Os seguintes aplicativos são compatíveis:

* Claude Antrópico
* Cursor
* OpenAI ChatGPT
* Microsoft Copilot Studio

Cada aplicativo fornece sua própria experiência de configuração, mas as etapas de alto nível são semelhantes.

## Visão geral da configuração {#setup-overview}

A configuração do MCP para AEM envolve duas partes principais:

1. **Configuração em cada aplicativo cliente MCP** para que o aplicativo saiba como se conectar aos servidores MCP do AEM e executar o logon OAuth
1. **Selecione o Servidor MCP** antes de começar a solicitar, para que o cliente MCP saiba como usá-lo.

### Configuração do AEM {#aem-configuration}

Por padrão, o acesso aos servidores MCP do AEM é controlado pelas permissões que os usuários individuais têm no AEM. Quando um usuário é autenticado por meio de um aplicativo cliente MCP, as ferramentas MCP impõem as mesmas regras de acesso que as operações manuais no AEM. Um usuário só pode executar ações que já estejam autorizadas a executar.

#### Aplicativos Cliente MCP permitidos {#permitted-mcp-client-applications}

Os seguintes aplicativos de cliente MCP são permitidos por padrão:

* ChatGPT
* Claude
* MS Copilot Studio
* Cursor

#### Restrição de Servidores MCP {#restricting-mcp-servers}

Incluir na lista de permissões Todos os servidores MCP são resolvidos por padrão. Como administrador, você tem a opção de restringir o acesso a servidores MCP específicos no nível de organização, programa ou ambiente. Isso proporciona controle granular sobre quais recursos de MCP estão disponíveis para os usuários em sua organização.

#### Gerenciando o Acesso para Cliente MCP {#managing-mcp-client-access}

Os administradores também podem desativar o acesso para aplicativos clientes MCP específicos se as políticas da organização exigirem. Se desejar que a Adobe habilite o suporte para produtos de cliente MCP adicionais, envie um link para o site do produto. Se precisar incluir na lista de permissões um cliente MCP personalizado, entre em contato também.

Para todas as solicitações relacionadas ao servidor MCP, entre em contato conosco em **aemcs-mcp-feedback@adobe.com**

### Configuração do aplicativo cliente MCP {#mcp-client-application-configuration}

Essa etapa é executada por cada usuário (ou por um administrador do aplicativo cliente MCP, quando houver suporte). Os detalhes de configuração variam um pouco entre os aplicativos. Os clientes MCP estão evoluindo rapidamente e o suporte a servidores MCP remotos está sendo ativamente desenvolvido. Talvez seja necessário ativar o Modo de desenvolvedor para acessar a funcionalidade de adição de servidores remotos, mas o processo geral é:

1. Adicionar o(s) URL(s) do servidor AEM MCP
   * Configure o(s) endpoint(s) de MCP na tabela acima. Por exemplo:`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. Acionar a conexão
   * Salve ou ative a configuração para que o aplicativo cliente MCP tente se conectar ao servidor MCP do AEM
1. Fazer logon com a Adobe ID
   * Quando solicitado, conclua o fluxo de logon do Adobe para que o aplicativo possa obter tokens OAuth vinculados ao seu Adobe ID
1. Verificar ferramentas descobertas
   * Depois de autenticado, o aplicativo descobrirá as ferramentas MCP do servidor. Você pode iniciar solicitando ao LLM a execução das operações do AEM.

Abaixo estão exemplos de como isso ocorre em cada aplicativo compatível em um alto nível.

**GPTchat**

![Configurar ChatGPT Etapa 1](assets/chatgpt-1.png)

![Configurar ChatGPT Etapa 2](assets/chatgpt-2.png)

![Configurar ChatGPT Etapa 3](assets/chatgpt-3.png)

![Configurar ChatGPT Etapa 4](assets/chatgpt-4.png)

![Configurar ChatGPT Etapa 5](assets/chatgpt-5.png)

![Configurar ChatGPT Etapa 6](assets/chatgpt-6.png)

![Configurar ChatGPT Etapa 7](assets/chatgpt-7.png)

* Adicione o(s) URL(s) do servidor MCP do AEM na área em que as conexões ou ferramentas do MCP estão configuradas
* Acionar a conexão e fazer logon com sua Adobe ID quando redirecionado
* Em um chat, consulte as ferramentas configuradas do AEM em seus prompts, por exemplo:

  *&quot;Usando as ferramentas AEM MCP configuradas, liste todos os sites em nosso ambiente de criação.&quot;*

**Claude**

![Configurar Claude Etapa 1](assets/claude-1.png)

![Configurar Claude Etapa 2](assets/claude-2.png)

![Configurar Etapa Claude 3](assets/claude-3.png)

![Configurar Claude Etapa 4](assets/claude-4.png)

![Configurar Claude Etapa 5](assets/claude-5.png)

![Configurar Etapa 6](assets/claude-6.png) do Claude

![Configurar Claude Etapa 7](assets/claude-7.png)

* Na configuração do MCP do Claude, registre o(s) URL(s) do servidor MCP do AEM
* Conclua o fluxo de logon do Adobe
* Como opção, ative a confirmação automática para determinadas ferramentas na área de configuração. Isso é recomendado para operações de pesquisa ou somente leitura.
* Verifique se o servidor MCP está selecionado antes de iniciar a conversa
* Peça a Claude para executar tarefas relacionadas ao AEM; Claude selecionará as ferramentas do AEM expostas pelo servidor MCP com base em seu prompt.

**Cursor**

![Configurar Etapa 1](assets/cursor-1.png) do Cursor

![Configurar Etapa 2](assets/cursor-2.png) do Cursor

![Configurar Etapa 3](assets/cursor-3.png) do Cursor

![Configurar Etapa 4](assets/cursor-4.png) do Cursor

![Configurar Etapa 5](assets/cursor-5.png) do Cursor

* Nas configurações de MCP do cursor, crie uma nova entrada de servidor MCP com o(s) URL(s) MCP do AEM
* Autentique com seu Adobe ID quando solicitado
* Como opção, ative ou desative ferramentas individuais clicando nos nomes das ferramentas. Todas as ferramentas são ativadas por padrão.
* Use o editor ou o chat do cursor para chamar as ferramentas do AEM como parte dos fluxos de trabalho de desenvolvimento ou conteúdo.

**Microsoft Copilot Studio**

![Configurar Copilot Etapa 1](assets/copilot-1.png)

![Configurar Copilot Etapa 2](assets/copilot-2.png)

![Configurar a Etapa 3](assets/copilot-3.png) do Copilot

![Configurar a Etapa 4](assets/copilot-4.png) do Copilot

![Configurar Copilot Etapa 5](assets/copilot-5.png)

![Configurar a Etapa 6](assets/copilot-6.png) do Copilot

![Configurar etapa 7](assets/copilot-7.png) do Copilot

![Configurar a Etapa 8](assets/copilot-8.png) do Copilot

![Configurar a Etapa 9](assets/copilot-9.png) do Copilot

![Configurar a Etapa 10 do Copilot](assets/copilot-10.png)

* Criar um novo agente
* Navegue até a seção de ferramentas e clique em **Adicionar ferramenta**
* Selecione uma ferramenta existente ou crie uma nova
* Configurar uma nova ferramenta de MCP apontando para o(s) URL(s) do servidor MCP do AEM
* Estabelecer uma conexão, que pode ser compartilhada ou dedicada entre agentes
* Fazer logon usando sua Adobe ID quando redirecionado
* Como opção, ative o modo de confirmação automática ou exija a confirmação do usuário final para todas as interações da ferramenta
* Ao testar seu agente, abra o gerenciador de conexões primeiro para atribuir uma conexão à sua sessão e pressione **Repetir**.

## Autenticação {#authentication}

Os servidores MCP hospedados na Adobe implementam o OAuth e são integrados ao sistema de identidade da Adobe.

* Quando um aplicativo cliente MCP se conecta a um servidor MCP do AEM, os usuários veem uma caixa de diálogo de logon do Adobe e se autenticam com sua **Adobe ID**
* Após o login bem-sucedido, o sistema verifica se o aplicativo cliente MCP é permitido em sua organização e se o servidor MCP solicitado é permitido. Se uma das verificações falhar, uma mensagem de erro será exibida.

![Erro de Cliente MCP não permitido](assets/MCP-Client-not-permitted.png)

* Uma vez verificado, o servidor MCP emite tokens que o aplicativo usa para chamadas de ferramenta subsequentes
* As ferramentas do MCP respeitam as permissões do AEM do usuário. Um usuário sem permissão para modificar um fragmento de conteúdo no AEM também não poderá modificá-lo por meio do MCP.

Isso garante que as operações assistidas por IA estejam em conformidade com seu modelo existente de segurança e governança da AEM.

## Uso do MCP com o AEM {#using-mcp-with-aem}

Depois que os aplicativos AEM e cliente MCP forem configurados, você poderá trabalhar no aplicativo de sua escolha e solicitar que o LLM execute as operações do AEM. O LLM lê os esquemas de ferramenta do MCP, escolhe quais ferramentas chamar e os sequencia conforme necessário para atender à sua solicitação.

>[!IMPORTANT]
>
>Para obter melhores resultados, especialmente com prompts que contêm várias etapas ou direcionam diferentes tipos de conteúdo, como imagens e texto, ative um modelo de pensamento ou selecione a opção Pensamento no cliente MCP em vez de depender do modo Automático.

### Exemplo de casos de uso {#example-usecases}

Alguns cenários representativos incluem:

* **Descoberta de ambiente**
   * Listar ambientes e licenças para decidir onde executar um fluxo de trabalho.

* **Gerenciamento de sites**
   * Listar sites
   * Criar, ler, atualizar e excluir páginas e conteúdo da página.

* **Gerenciamento de fragmentos de conteúdo**
   * Pesquisar fragmentos de conteúdo
   * Criar novos fragmentos
   * Atualizar fragmentos existentes quando as mensagens da campanha forem alteradas.

* **Gerenciamento de Assets**
   * Importar ativos
   * Localizar ativos existentes
   * Publicar ativos.

### Exemplo de fluxos de trabalho {#example-workflows}

Os exemplos a seguir ilustram como um LLM pode encadear ferramentas de MCP em conjunto.

1. **Trabalhando com um fragmento de conteúdo referenciado por uma página**
   * **Obter conteúdo da página** - Chame uma ferramenta como `get-aem-page-content` para recuperar a página e localizar a propriedade `fragmentPath`.
   * **Resolver o caminho do fragmento** - Use `resolve_fragment_path` para converter o caminho em uma UUID.
   * **Buscar dados do fragmento** - Chame `get_fragment` para recuperar os campos atuais.
   * **Atualizar o fragmento** - Chame `patch_fragment` para aplicar as alterações ao conteúdo do fragmento.
1. **Criando novo conteúdo com base em um modelo**
   * **Descobrir modelos** - Use `list_models` para ver quais modelos de fragmento de conteúdo estão disponíveis.
   * **Inspecionar um modelo** - Use `get_model` para entender o esquema de campo do modelo.
   * **Criar conteúdo** - Use `create_fragment` para criar um novo fragmento com valores derivados do seu prompt.
1. **Atualizar com segurança o conteúdo existente**
   * **Ler dados atuais** - Use `get_fragment` para recuperar os dados existentes e um ETag.
   * **Aplicar um patch de JSON** - Use `patch_fragment` com o ETag e um documento de patch de JSON para atualizar o fragmento, oferecendo suporte a simultaneidade otimista.

Da perspectiva do usuário, esses workflows podem ser iniciados com prompts como:

*&quot;Crie um novo fragmento de conteúdo para a campanha do primeiro trimestre com base em nosso modelo de banner principal e preencha os campos deste resumo.&quot;*

O LLM escolhe e coordena as ferramentas MCP necessárias automaticamente.

## Gerenciamento de expectativas {#expectation-management}

Ao trabalhar com LLMs por meio do MCP, lembre-se do seguinte:

* **Altamente capaz, mas não infalível**
Os LLMs podem realizar tarefas complexas, mas são propensos a erros ocasionais. O mesmo prompt pode produzir resultados ou apresentações ligeiramente diferentes sem uma razão óbvia. Sempre revise os resultados antes de aplicar as alterações ao conteúdo de produção.

* **Desenvolvendo recursos**
Os modelos de LLM estão melhorando continuamente. Com o tempo, eles se tornam mais inteligentes ao descobrir novas maneiras de combinar ferramentas de MCP para atingir suas metas. Uma tarefa que exigiu vários prompts hoje pode funcionar perfeitamente com um único prompt amanhã.

* **A supervisão humana é essencial**
Pense no LLM como um assistente qualificado que precisa de supervisão. Ele tem amplo conhecimento e pode criar soluções criativas, mas se beneficia de sua orientação e revisão. Verifique os resultados, especialmente para operações críticas, e forneça feedback quando o resultado não corresponder às suas expectativas.

* **Tenha cuidado com as execuções da ferramenta de confirmação automática**
Alguns aplicativos clientes de MCP, como o Claude, oferecem a opção de confirmar automaticamente as execuções da ferramenta solicitadas pelo LLM. Embora isso possa ser conveniente para operações somente leitura, como pesquisa ou recuperação de conteúdo, tenha cuidado com ferramentas que atualizam ou excluem conteúdo. Revise cada solicitação de execução de ferramenta antes de confirmar as ações que modificam seu ambiente do AEM.

## Limitações   {#limitations}

Os servidores MCP da AEM devem ser configurados no ChatGPT, Claude, Cursor e Microsoft Copilot Studio.

Se quiser usar um aplicativo cliente MCP diferente, entre em contato com **aemcs-mcp-feedback@adobe.com** para solicitar suporte para clientes adicionais ou incluir na lista de permissões um personalizado.
