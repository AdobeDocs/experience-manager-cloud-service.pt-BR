---
title: Noções básicas sobre o Universal Editor
description: Este tutorial ajuda você a começar a usar a interface do Universal Editor. Ele orienta você a entender a interface do usuário para criar seus próprios formulários Edge Delivery Services no Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 0%

---


# Explorar a interface do editor universal (WYSIWYG)

O [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) oferece uma interface simples, visual e intuitiva do What You See Is What You Get (WYSIWYG) para o Adobe Edge Delivery Services Forms. Ele fornece uma interface moderna com funcionalidade de arrastar e soltar para uma criação de formulários eficiente.

![Interface de Usuário do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## O que você vai aprender

Ao final deste tutorial, você irá:

- Entender os principais componentes da interface do Universal Editor
- Navegar com confiança pelas diferentes seções da interface
- Saber como acessar e usar ferramentas essenciais de criação de formulários
- Estar familiarizado com atalhos de teclado que aumentam a produtividade

## Compreender a interface do editor universal

Ao editar um formulário usando o Editor universal, o console abre uma interface interativa do WYSIWYG que permite iniciar a edição imediatamente. Essa interface fornece feedback visual em tempo real enquanto você trabalha, mostrando exatamente como seu formulário aparecerá para os usuários finais.

>[!NOTE]
>
> Para saber como criar formulários usando o Universal Editor, consulte o artigo [Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interface de Usuário do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

A interface do Editor universal é dividida em quatro partes lógicas:

- **[A: Cabeçalho Do Experience Cloud](#experience-cloud-header)**
- **[B: Barra de Ferramentas do Editor Universal](#universal-editor-toolbar)**
- **[C: Painel Propriedades](#properties-panel)**
- **[D: Editor](#editor)**

Vamos explorar cada seção em detalhes.

### Cabeçalho Experience Cloud

O Cabeçalho do Experience Cloud é exibido na parte superior do console e fornece o contexto de navegação dentro do ecossistema mais amplo da Adobe Experience Cloud. Ele mostra sua localização atual e permite acesso rápido a outros aplicativos da Experience Cloud.

![Cabeçalho Experience Cloud do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

Vamos examinar cada componente:

- **Adobe Experience Cloud**

  Clicar no link **Adobe Experience Cloud** no lado esquerdo da tela permite navegar até a raiz da solução do Experience Manager. A partir daí, você pode acessar outras ferramentas, como o Experience Manager Sites, o Experience Manager Assets e o Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **Nome da Organização**

  O **Nome da Organização** exibe o nome da organização do Identity Management System (IMS) na qual você está conectado no momento. Se você tiver acesso a várias organizações, poderá alternar entre elas usando esse menu suspenso. Por exemplo, na captura de tela, a organização IMS selecionada no momento é &quot;AEM Forms Internal01&quot;.

  ![Organização](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **Ajuda**

  O ícone Ajuda fornece acesso rápido aos recursos de aprendizagem e suporte. Isso é particularmente valioso quando você encontra desafios ou precisa de orientação sobre recursos específicos. Você também pode enviar feedback por meio desta seção.

  ![Ajuda](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **Notificações**

  A seção **Notificações** exibe o número de notificações incompletas, solicitações e tarefas atuais atribuídas atualmente na sua organização IMS. Estar de olho nesta seção ajuda você a se manter atualizado em relação ao fluxo de trabalho.

  ![Notificação](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **Soluções**

  O menu **Soluções** permite alternar para outras soluções da Adobe Experience Cloud, facilitando a movimentação entre diferentes ferramentas em seu fluxo de trabalho.

  ![Soluções](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **Perfil de usuário**

  Esse ícone exibe as informações do seu perfil, juntamente com o nome da organização IMS na qual você está conectado no momento. Clique neste ícone para acessar as configurações da conta e as opções de saída.

  ![Autor](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### Barra de ferramentas do editor universal

A barra de ferramentas fornece ferramentas essenciais de navegação e edição. Com ele, você pode mover-se entre formulários, publicar ou desfazer a publicação de formulários, editar propriedades do formulário e acessar o editor de regras para adicionar comportamentos dinâmicos.

![Barra de Ferramentas do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Veja o que cada componente oferece:

- **Botão da Página Inicial**

  O botão Home retorna à página inicial do Universal Editor. Isso é útil quando você precisa começar a trabalhar em um formulário diferente. Você também pode inserir diretamente um URL na barra de localização para navegar para qualquer formulário que deseja editar.

  ![Página Inicial do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **Barra de Localização**

  A **Barra de Localização** exibe o endereço do formulário que você está editando no momento. Para alternar para um formulário diferente, basta clicar na barra de localização e inserir sua URL. O atalho de teclado para focalizar a barra de localização é `l`.

  ![Barra de Localização](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **Editor de regras**

  O **Editor de regras** permite que você adicione comportamentos dinâmicos aos seus formulários por meio de uma interface visual intuitiva. Com ele, você pode criar condições, validações e ações que respondam à entrada do usuário, tornando seus formulários interativos e inteligentes.

  ![Editor de regras](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - A extensão Editor de Regras não está habilitada por padrão no Editor Universal. Para habilitar este recurso avançado, contate-nos em [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) pelo seu endereço de email oficial.
  > - Para saber como criar e gerenciar regras, consulte o artigo [Introdução ao Editor de regras em Criação no WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

- **Editar Propriedades do Formulário**

  A opção **Editar propriedades do formulário** permite definir configurações importantes do formulário, como o Modelo de dados de formulário (FDM) e a data de publicação. Essas propriedades influenciam como o formulário se comporta e se integra a sistemas de back-end.

  ![Editar Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **Configurações do Cabeçalho de Autenticação**

  A opção **Configurações do Cabeçalho de Autenticação** permite definir cabeçalhos de autenticação personalizados para fins de desenvolvimento local. Isso é particularmente útil ao testar formulários que exigem credenciais de autenticação.

  ![Cabeçalho de Autenticação](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **Modo responsivo**

  O recurso **Modo responsivo** permite testar como o formulário será exibido em diferentes dispositivos. Por padrão, o editor é aberto no layout de desktop, mas você pode alternar para o modo de exibição móvel para garantir que o formulário permaneça utilizável e atraente em telas menores.

  ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **Modo de visualização**

  **Modo de Visualização** mostra o formulário exatamente como ele será exibido quando publicado. Isso permite que você interaja com o formulário clicando em links e botões, como seus usuários fariam. Essa é uma etapa essencial antes da publicação para verificar se tudo funciona conforme o esperado. Alternar entre os modos de edição e visualização usando o atalho de teclado `p`.

  ![Visualização](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **Abrir página**

  O botão **Abrir Página** abre o formulário em uma nova guia do navegador para visualização. Isso fornece uma visualização em tela cheia do formulário sem a interface do editor. O atalho de teclado desta ação é `o`.

  ![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **Publicar**

  Quando o formulário estiver pronto para os usuários, o botão **Publicar** o tornará online e disponível para o seu público-alvo. Esta é a etapa final no fluxo de trabalho de criação do formulário.

  ![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **Menu de reticências**

  Clicar nas reticências (...) revela opções adicionais, incluindo a capacidade de **Desfazer a publicação** de um formulário que está ativo no momento. Isso é útil quando você precisa remover temporariamente um formulário do acesso público ou substituí-lo por uma versão atualizada.

  ![Reticências](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### Painel Propriedades

O **Painel de Propriedades** aparece no lado direito da interface e exibe informações contextuais com base no que você selecionou no formulário. Quando nenhum componente é selecionado, ele mostra a estrutura geral do formulário.

![Painel de propriedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

Vamos explorar seus principais componentes:

- **Modo de Propriedades**

  O modo **Propriedades** exibe configurações e opções para o componente selecionado no momento. É aqui que você personaliza elementos individuais do formulário para atender aos seus requisitos específicos. O atalho de teclado para abrir as propriedades de um componente selecionado é `d`.

  ![Propriedades](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **Árvore de conteúdo**

  A **Árvore de conteúdo** exibe a estrutura hierárquica do formulário. Essa representação visual ajuda você a entender como os componentes são aninhados entre si. Clicar em qualquer item na árvore seleciona-o no editor e rola a tela até seu local. Isso é especialmente útil em formas complexas. Alternar a exibição da árvore de conteúdo com o atalho de teclado `f`.

  ![Árvore de conteúdo](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **Gerar Variações**

  O recurso **Gerar variações** aproveita a inteligência artificial para criar diferentes versões do formulário com base em prompts específicos. Isso ajuda você a experimentar com diferentes abordagens e designs sem criar manualmente cada variação. Os prompts podem ser fornecidos pela Adobe ou personalizados por você.

  ![Gerar Variações](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > Para obter instruções detalhadas sobre como usar a opção Gerar variações para formulários, consulte o artigo [Gerar variações](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations).

- **Experimentação**

  O recurso **Experimentação** permite executar testes controlados comparando diferentes designs e layouts de formulário. Analisando como os usuários interagem com cada variante, é possível tomar decisões orientadas por dados para otimizar as taxas de conversão e a experiência do usuário.

  ![Experimentação](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **Personalização**

  As configurações do **Personalization** permitem que você conecte seus formulários com o Adobe Experience Platform (AEP) ou aplicativos externos. Essa conexão permite criar experiências de formulário personalizadas com base nos dados e comportamentos do usuário, aumentando a relevância e o engajamento.

  ![Personalização](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **Teste A/B**

  O **Teste A/B** ajuda você a comparar variações específicas do seu formulário para determinar qual tem melhor desempenho. Diferentemente da experimentação mais ampla, os testes A/B normalmente se concentram na comparação de elementos ou alterações específicos para identificar a opção mais eficaz.

  ![Teste A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **Gerenciamento de tarefas**

  O recurso **Gerenciamento de tarefas** simplifica a colaboração, ajudando sua equipe a organizar, rastrear e concluir tarefas relacionadas à criação e otimização de formulários. Isso mantém os projetos avançando eficientemente com uma responsabilidade clara.

  ![Gerenciamento de tarefas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **Rascunhos de Conteúdo**

  O recurso **Rascunhos de Conteúdo** permite criar e salvar versões preliminares de elementos de texto no formulário. Você pode criar rascunhos usando texto de formulário existente ou começar do zero e, em seguida, editá-los ou excluí-los conforme necessário. Por padrão, você verá três rascunhos, mas ao clicar em **Mostrar tudo** serão exibidos rascunhos adicionais.

  ![Rascunhos de Conteúdo](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **Source de dados**

  A opção **Data Source** permite configurar e selecionar as fontes de dados para seu Modelo de Dados de Formulário (FDM). Essa integração disponibiliza para uso no formulário todos os objetos, propriedades e serviços do modelo de dados das fontes selecionadas, permitindo a recuperação e o envio de dados dinâmicos.

  ![Source de dados](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **Adicionar**

  O botão **Adicionar** revela uma lista suspensa de componentes que podem ser adicionados ao contêiner selecionado no momento. Por exemplo, quando uma seção Formulário adaptável é selecionada, essa lista mostra todos os componentes que podem ser adicionados a essa seção. O atalho de teclado para abrir esta lista de componentes é `a`.

  ![Adicionar ícone](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **Duplicar**

  A opção **Duplicar** cria uma cópia exata do componente selecionado. Isso economiza tempo quando você precisa de vários elementos semelhantes, pois é possível duplicar e modificar em vez de criar do zero.

  ![Ícone Duplicado](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **Excluir**

  A opção **Excluir** remove o componente selecionado do formulário. Tenha cuidado ao usar essa opção, pois ela remove imediatamente o elemento sem um prompt de confirmação.

  ![Excluir](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### Editor

O Editor é o espaço de trabalho central onde você cria e modifica o formulário. Ele exibe o formulário especificado na barra de localização e fornece uma experiência do WYSIWYG que mostra exatamente como o formulário será exibido para os usuários. No modo de visualização, você pode interagir com o formulário da mesma forma que seus usuários fariam, testando a navegação por botões e links.

![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

O Editor é onde você passa a maior parte do seu tempo, adicionando componentes, configurando suas propriedades e organizando-os para criar uma experiência de formulário intuitiva e eficaz.

## Resumo de atalhos de teclado

Para aumentar sua produtividade, lembre-se desses atalhos essenciais do teclado:

- `l` - Focalizar a barra de localização
- `p` - Alternar entre os modos de edição e de visualização
- `o` - Abrir o formulário em uma nova guia
- `d` - Abrir propriedades do componente selecionado
- `f` - Alternar a exibição da árvore de conteúdo
- `a` - Abrir a lista de componentes a serem adicionados


