---
title: Noções básicas do editor universal - Tutorial do desenvolvedor
description: Este tutorial ajuda você a começar a usar a interface do Universal Editor. Ele orienta você a entender a interface do usuário para criar seus próprios formulários Edge Delivery Services no Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Explorar a interface do editor universal (WYSIWYG)

O [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) oferece uma interface simples, visual e intuitiva do What You See Is What You Get (WYSIWYG) para o Adobe Edge Delivery Services (EDS) Forms. Ele fornece uma interface moderna com funcionalidade de arrastar e soltar para uma criação de formulários eficiente.

![Interface de Usuário do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Compreensão da interface do editor universal

Quando o autor do formulário edita o formulário usando o Editor universal, o console abre uma interface interativa do WYSIWYG, permitindo que o usuário comece a editar o formulário.

>[!NOTE]
>
> Para saber como criar formulários usando o Universal Editor, consulte o artigo [Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interface de Usuário do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

A interface do Editor universal está dividida em quatro partes:

* **[A: Cabeçalho Do Experience Cloud](#experience-cloud-header)**
* **[B: Barra de Ferramentas do Editor Universal](#universal-editor-toolbar)**
* **[C: Painel Propriedades](#properties-panel)**
* **[D: Editor](#editor)**

### Cabeçalho Experience Cloud

O cabeçalho do Experience Cloud está localizado na parte superior do console. Ela fornece informações sobre a localização atual no Experience Cloud. Também permite navegar para outros aplicativos da Experience Cloud.

![Cabeçalho Experience Cloud do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Vamos entender cada um de seus componentes.

* **Adobe Experience Cloud**

  Você pode clicar no link **Adobe Experience Cloud** no lado esquerdo da tela para navegar até a raiz da solução da Experience Manager e acessar ferramentas como o Experience Manager Sites, o Experience Manager Assets e o Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Nome da organização**

  O **nome da organização** exibe o nome da organização IMS na qual você está conectado no momento. É possível alternar para outra organização IMS, se ela tiver acesso a outras organizações, selecionando na lista suspensa. Por exemplo, o nome da organização IMS selecionada no momento é `AEM Forms Internal01`.

  ![Organização](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Ajuda**

  O ícone de ajuda fornece acesso rápido aos recursos de aprendizagem e suporte. O autor do formulário também pode adicionar comentários na seção **Ajuda**.
  ![Ajuda](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Notificações**

  A seção **Notificação** exibe o número de notificações incompletas atribuídas atualmente, as solicitações e as tarefas atuais na organização IMS.

  ![Notificação](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Soluções**

  Você pode alternar para outras soluções da Experience Cloud usando o link **Soluções**.
  ![Soluções](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Autor**
O ícone representa os detalhes do autor do formulário, juntamente com o nome da organização IMS na qual o autor está conectado no momento.
  ![Autor](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Barra de ferramentas do editor universal

A barra de ferramentas permite navegar até outros formulários e editá-los. Também permite publicar ou desfazer a publicação do formulário, editar as propriedades do formulário e acessar o editor de regras.
![Barra de Ferramentas do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Vamos entender cada um de seus componentes.

* **Botão da Página Inicial**
O botão Início permite navegar até a página inicial do Universal Editor. Você também pode inserir diretamente a URL do formulário que deseja editar usando o Editor universal.
  ![Página Inicial do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Barra de Localização**
A **barra de localização** exibe o endereço do formulário que o autor está editando. Você também pode inserir outro URL de formulário clicando na barra de localização. A tecla de atalho para abrir a barra de localização é a tecla `l`.
  ![Barra de Localização](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Editor de regras**

  O **Editor de regras** oferece uma interface visual intuitiva para criar e gerenciar regras. É possível adicionar comportamento de formulário dinâmico usando o Editor de regras.

  ![Editor de regras](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * No Editor universal, a extensão Editor de regras não é ativada por padrão. Para habilitar a gravação da extensão do Editor de Regras em [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) da sua ID de email oficial.
  > * Para saber como criar regras, consulte o artigo [Introdução ao Editor de regras em Criação no WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Editar Propriedades do Formulário**
É possível editar as propriedades do formulário, como o modelo de dados de formulário e a data de publicação, clicando na opção **Editar propriedades do formulário**.
  ![Editar Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Configurações do Cabeçalho de Autenticação**
As **configurações do cabeçalho de autenticação** permitem que o autor defina um cabeçalho de autenticação personalizado para fins de desenvolvimento local.
  ![cabeçalho de autenticação](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Modo responsivo**
  A opção **Modo Responsivo** permite definir como o Editor Universal renderiza o formulário. Por padrão, o editor é aberto em um layout de desktop, onde a altura e a largura são determinadas automaticamente pelo navegador. Como alternativa, você pode optar por emular um dispositivo móvel e verificar como o formulário aparece em dispositivos móveis.

  ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Modo de visualização**
No modo de visualização, o formulário é exibido no editor exatamente como é publicado. Isso permite que o autor navegue pelo formulário clicando em links e botões. Depois de satisfeito com as edições, o autor pode publicar o formulário para usuários ativos. A tecla de atalho para alternar entre os modos de edição e visualização é `p`.
  ![Visualização](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Abrir página**
A opção **Abrir página** abre o formulário em uma nova guia para visualização. A tecla de atalho para abrir o formulário no modo de visualização em uma nova guia é `o`.
  ![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Publicar**

  Você pode disponibilizar o formulário para usuários ativos usando o botão **Publicar**.
  ![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Reticências**
Quando o autor clica na opção de reticências (...), a opção **Desfazer publicação** é exibida. Você pode cancelar a publicação de um formulário usando a opção **Cancelar publicação**.
  ![Reticências](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Painel Propriedades

O **Painel de Propriedades** está localizado no lado direito do editor. Ele exibe os detalhes do componente selecionado na hierarquia do formulário. É a estrutura padrão quando nenhum componente é selecionado.
![painel ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Vamos entender cada um de seus componentes.


* **Modo de Propriedades**
A opção Em **Propriedades** mostra as propriedades do componente selecionado no editor. Por exemplo, a imagem exibe as propriedades do componente de entrada do número selecionado. É possível modificar as propriedades do componente usando essa opção. A tecla de atalho para abrir propriedades do componente é `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Árvore de conteúdo**
A opção **Árvore de conteúdo** exibe a hierarquia do formulário. Quando o autor clica em um item na árvore de conteúdo, o editor o seleciona e rola para esse componente. A tecla de atalho para alternar entre o modo de exibição de árvore de conteúdo é a tecla `f`.

  ![Árvore de conteúdo](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Gerar Variações**
  **Gerar variações** usa inteligência artificial para produzir diferentes versões de formulários com base em prompts específicos. Esses prompts podem ser fornecidos pelo Adobe ou criados e gerenciados pelo autor do formulário.

  ![variação](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Para obter instruções sobre como usar a opção Gerar variações para formulários, consulte o artigo [Gerar variações](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Experimentação**:

  **Experimentação** refere-se às técnicas usadas para testar diferentes variações de formulários e layout para otimizar a experiência do usuário e o desempenho.
  ![experimentação](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalization**
A opção **Personalization** define as configurações para estabelecer uma conexão entre os formulários e o Adobe Experience Platform (AEP) que fazem parte do ecossistema do Adobe ou de aplicativos externos.
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **Teste A/B**:
  **Teste A/B** refere-se às técnicas usadas para testar diferentes variações de formulários e layouts para otimizar a experiência e o desempenho do usuário.
  ![Teste A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Gerenciamento de tarefas**:
O recurso **Gerenciamento de Tarefas** permite que você dinamize os fluxos de trabalho e aprimore a colaboração, permitindo que as equipes gerenciem, acompanhem e executem tarefas relacionadas à personalização e otimização de formulários
  ![gerenciamento de tarefas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Rascunhos de Conteúdo**

  A opção **Rascunhos de Conteúdo** permite criar rascunhos para elementos rich text. Rascunhos podem ser criados usando texto de formulário existente ou do zero. É possível editar ou excluir rascunhos conforme necessário. Por padrão, apenas três rascunhos ficam visíveis, mas clicar em **Mostrar tudo** exibe o restante.

  ![gerenciamento de tarefas](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Source de dados**

  A opção **Data Source** permite configurar fontes de dados e selecioná-las ao criar um Modelo de Dados de Formulário (FDM). Ele disponibiliza todos os objetos, propriedades e serviços do modelo de dados das fontes de dados selecionadas para uso no Modelo de dados do formulário.
  ![Data Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Adicionar**

  A opção **Adicionar** abre uma lista suspensa de componentes que podem ser adicionados ao contêiner selecionado. Por exemplo, em uma seção Formulário adaptável, a lista exibe os componentes disponíveis que podem ser adicionados a um formulário. A tecla de atalho para abrir a lista de componentes é `a`.
  ![Ícone Adicionar](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplicar**

  A opção **Duplicar** cria uma cópia do componente, que é selecionado na árvore de conteúdo ou no editor.
  ![Ícone duplicado](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Excluir**
A opção **Excluir** exclui um componente, que é selecionado na árvore de conteúdo ou no editor.

  ![Excluir](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Editor

O editor permite editar o formulário, e o formulário especificado na barra de localização é renderizado na área de edição. Se o editor estiver no modo de visualização, você poderá navegar pelo formulário usando os botões e links disponíveis.
![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Consulte também:

{{universal-editor-see-also}}
