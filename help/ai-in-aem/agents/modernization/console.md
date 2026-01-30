---
title: Console de Modernização da experiência
description: Guia de referência para a interface e os recursos do Console de modernização de experiência
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c2f258bfcfff8392af2863d874d4a4235f042193
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# Console de Modernização da experiência {#console-reference}

Guia de referência para a interface e os recursos do Console de modernização de experiência

>[!NOTE]
>
>Se você estiver interessado em usar o Console de modernização de experiência, poderá solicitar acesso para garantir uma experiência de integração tranquila.

## Visão geral {#overview}

O Console de Modernização da Experiência é um ambiente de desenvolvimento hospedado e assistido por IA para o Edge Delivery Services, exposto como uma interface da Web em [`aemcoder.adobe.io`.](https://aemcoder.adobe.io) Depois de se conectar ao projeto GitHub, você pode iniciar imediatamente a solicitação de alterações na linguagem natural sem precisar de mais instalação ou configuração de ambiente local.

>[!TIP]
>
>Se você estiver interessado em começar imediatamente a usar o console, confira o documento [Introdução ao Agente de Modernização de Experiência.](/help/ai-in-aem/agents/modernization/getting-started.md)

## Recursos {#capabilities}

Principais recursos do console:

* Painel de bate-papo interativo com o agente e suas habilidades
* Visualização do Live AEM para feedback visual imediato sobre as alterações
* Navegador de arquivos de conteúdo e visualizador de Markdown
* Sincronização de conteúdo com [Criação de documentos](https://da.live)
* Navegador de código e visualizador de diferenças para revisar as alterações feitas
* Integração do GitHub com a capacidade de criar solicitações de pull a partir de alterações

Os desenvolvedores mantêm controle total sobre quais envios. Todas as alterações feitas pelo console exigem análise e aprovação antes da implantação, garantindo a governança, a consistência da marca e a segurança.

## Navegação {#navigation}

Depois de entrar no console às [`aemcoder.adobe.io`,](https://aemcoder.adobe.io) você acessa a tela inicial do console.

![Tela inicial do console](assets/console-home.png)

### Barra de menus {#menu-bar}

A barra do menu superior fornece:

* Um botão **Abrir menu** à esquerda para expandir e recolher os detalhes do painel lateral esquerdo
* Um botão **Conta** à direita para alternar para o modo escuro e sair do console

### Barra lateral esquerda {#sidebar}

A barra lateral esquerda permite acesso rápido a exibições importantes do console.

* **[Exibição da página inicial](#home-view)** (ícone da casa) - O ponto de partida para usar o console
* **[Exibição de Conteúdo](#content-view)** (ícone de arquivo) - Conteúdo que você importou
* **[Modo de Exibição de Código](#code-view)** (`</>` ícone) - Código do site em que você está trabalhando
* **[Exibição de configurações](#settings-view)** (ícone de engrenagem) - Configurações do console

## Exibição da página inicial {#home-view}

A exibição **Página Inicial** é o seu ponto de partida para usar o console.

* Na parte superior há um [painel de prompt](#prompt-panel) para fazer solicitações do console.
* Abaixo do painel de aviso são sugeridos prompts para usar para iniciar seu projeto.

### Painel de seleção {#prompt-panel}

O painel de prompt fornece controles para interagir com a IA.

* **Planejar / Executar modos** (ícones de lâmpada e varinha mágica): alternar entre os modos de planejamento e execução, respectivamente
   * **Modo de plano**: a IA analisa solicitações e descreve uma abordagem sem fazer alterações, o que é útil para entender a estratégia antes de confirmar.
   * **Modo de execução**: a IA executa o plano e faz alterações reais no arquivo.
* **Anexar arquivos** (ícone de clipe de papel): carregue e anexe arquivos ao prompt para contexto adicional (por exemplo, designs de referência, capturas de tela, especificações)
* **Configurações** (ícone de engrenagem): ignorar perguntas de confirmação da IA
* **Limpar chat**: redefine a conversa e limpa a janela de contexto da IA. Use esta opção ao iniciar uma nova tarefa não relacionada à conversa anterior.

## Exibição de conteúdo {#content-view}

A **Exibição de conteúdo** fornece ferramentas para navegar e visualizar conteúdo. Por padrão, a exibição é dividida em três painéis, da esquerda para a direita:

* Solicitar painel para interagir com o console e o projeto
* Navegador de arquivos para obter uma visão geral de seus arquivos de conteúdo (alterne mostrar este painel com o ícone de divisa)
* Painel Visualizar para visualizar o conteúdo selecionado no navegador de arquivos

![Exibição de conteúdo](assets/content-imported.png)

O painel de visualização oferece três modos:

* **Visualizar** (documento com ícone de lupa) para exibir o conteúdo do HTML renderizado
* **exibição do HTML** (ícone de documento) para exibir a estrutura de conteúdo de criação do documento subjacente, respectivamente
* **Modo de design** (ícone de pincel) para selecionar elementos da página para o contexto do prompt

Você sempre pode clicar no ícone **Atualizar visualização** para atualizar o painel de visualização.

O botão **Carregar conteúdo** abre uma janela modal para carregar arquivos para o AEM Document Authoring.

* Os campos **Organização** e **Repositório** serão preenchidos previamente se o projeto tiver um arquivo `fstab.yaml`
* A seleção de arquivo fornece caminhos de destino editáveis
* Upload para JCR (para Universal Editor) não suportado

![Carregar conteúdo](assets/upload-content.png)

## Visualização de código {#code-view}

A **Visualização de código** fornece ferramentas para procurar código e gerenciar alterações de código. A exibição é dividida em três painéis, da esquerda para a direita:

* Solicitar painel para interagir com o console e o projeto
* Navegador de arquivos para obter uma visão geral dos arquivos de código ou alterações como diferenciais
* Painel Visualizar para visualizar um arquivo de código ou diferenciar selecionado no navegador de arquivos

![Modo de exibição de código](assets/code-view.png)

O painel de visualização oferece dois modos diferentes:

* **Arquivos Workspace** para navegar pelos arquivos de código no espaço de trabalho atual
* **Alterações do Git** para exibir as diferenças de arquivos, alterações criadas pelo seu trabalho no projeto
   * Clique no ícone `+` para preparar o arquivo alterado
   * Clique no ícone de seta para descartar o arquivo alterado

O ícone **Informações** lista a conta GitHub e o projeto conectados no momento.

O menu **Ações do GitHub** (canto superior direito) fornece operações do repositório.

* **Conectar/Reconectar**: inicia o GitHub OAuth
* **Alternar Repositório**: substitui o espaço de trabalho por um repositório diferente. Qualquer trabalho não comprometido será perdido.
* **Alternar ramificação**: alterna ramificações dentro do mesmo repositório
* **Sincronização**: obtém as alterações mais recentes da origem remota
* **Push**: abre um modal para enviar alterações do espaço de trabalho para o GitHub
* **Logout**: desconecta-se do GitHub

Ao enviar alterações, você deve ter as primeiras alterações preparadas para incluí-las no push. Ao enviar, você pode optar por criar uma nova PR ou enviar diretamente para a ramificação atual

![Enviar alterações](assets/push-changes.png)

## Exibição de configurações {#settings-view}

A visualização de configurações permite gerenciar configurações básicas do console.

![Modo de exibição de configurações](assets/settings-view.png)

* **Credenciais** permite que você especifique um token de acesso pessoal para o Figma, para que o console possa acessar blocos de design para o seu projeto.
* **Redefinir espaço de trabalho** reverte o console para seu estado inicial e todas as alterações não enviadas ou não carregadas serão perdidas.
