---
title: Configuração da exibição da linha do tempo para o AEM Screens
description: Esta página descreve como configurar uma visualização de linha do tempo no Screens as a Cloud Service.
exl-id: 53afe1f5-8f0b-4cca-a819-d3e9375cbe37
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 12%

---

# Configuração da exibição da linha do tempo para o AEM Screens {#configuring-timelineview-screens}

## Introdução {#introduction}

Esta seção descreve como criar uma Exibição de linha do tempo para o AEM Screens.

O AEM fornece um conjunto de recursos que permitem que várias pessoas em grupos em uma organização colaborem na criação, no gerenciamento e no uso de canais.
A linha do tempo, localizada na barra à esquerda, descreve os canais, o local ou o ciclo de vida de qualquer pasta de tela em ordem de tempo, transmitindo o que aconteceu com ela durante sua vida útil. Isso pode ser filtrado por tipo.
O painel da linha do tempo fornece os recursos abaixo, além dos logs de ciclo de vida.

![Aplicar perfil à pasta](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![Aplicar perfil à pasta](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

Para criar uma Exibição de linha do tempo para o AEM Screens, conclua as seguintes etapas:

1. Adicionar comentário
1. Salvar uma versão
1. Iniciar um fluxo de trabalho

As seções a seguir descrevem essas etapas em detalhes.

### Adicionar um comentário {#addcomment}

Os comentários disponíveis por meio da linha do tempo permitem que os usuários criem um registro centralizado e histórico para discussões que ocorrem sobre o canal, o local ou qualquer pasta na tela.
Os comentários fornecem uma maneira consolidada e agradável para os usuários do AEM discutirem uma maneira que pode ser persistente, permitindo que outros entendam as principais decisões.

1. Navegue até o canal ao qual deseja adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do Tempo**.
1. Adicione seu comentário e pressione **Enter**.

![Adicionar um comentário](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

As informações na linha do tempo são atualizadas para indicar que o comentário foi adicionado.

![Adicionar um comentário](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### Salvar uma versão {#saveversion}

O controle de versão cria um &quot;instantâneo&quot; de um canal em um ponto específico no tempo. Com o controle de versão, você pode executar as seguintes ações:

* Crie uma versão de um canal.
* Restaurar um canal para uma versão anterior; por exemplo:
   * para desfazer uma alteração feita na página.
* Comparar a versão atual de um canal com uma versão anterior:
   * para realçar as diferenças no conteúdo do canal.


#### Criar uma nova versão {#createnewversion}

1. Navegue até o canal ao qual deseja adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do Tempo**.
1. Clique no botão (três pontos) ao lado do campo de comentário na parte inferior da página.

   ![Adicionar um comentário](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. Selecione **Salvar como versão**.
1. Insira um **Rótulo** e um **Comentário** para a versão.

   ![Adicionar um comentário](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. Confirme a nova versão selecionando **Criar**. As informações na linha do tempo são atualizadas para indicar a nova versão.

#### Reverter para uma versão {#revertversion}

Para Reverter a página selecionada para uma versão anterior:

1. Navegue até o canal para adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do Tempo**.
1. Selecione **Mostrar tudo** ou **Versões** na lista suspensa de filtros. As versões de canal do canal selecionado são listadas.
1. Selecione a versão para a qual deseja reverter. As opções possíveis são mostradas:

   ![Adicionar um comentário](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. Selecione **Reverter para essa versão**. A versão selecionada é restaurada e as informações na linha do tempo atualizadas.

#### Visualizar uma versão {#previewversion}

É possível visualizar uma versão específica:

1. Navegue até o canal para adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do Tempo**.
1. Selecione **Mostrar tudo** ou **Versões** na lista suspensa de filtros. As versões de canal do canal selecionado são listadas.
1. Selecione a versão que deseja visualizar. As opções possíveis são mostradas:

   ![Versão de Visualização](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. Selecione **Visualizar**. O canal é mostrado em uma nova guia.

#### Comparar uma versão com a versão atual {#compareversion}

É possível comparar uma versão específica com a versão atual:

1. Navegue até o canal ao qual deseja adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do tempo**
1. Selecione **Mostrar tudo** ou **Versões** na lista suspensa de filtros. As versões de canal do canal selecionado são listadas.
1. Selecione a versão que deseja comparar. As opções possíveis são mostradas:

   ![Comparar Versão](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. Selecione **Comparar com a atual**. O pop-up é aberto para exibir as diferenças.

### Iniciar um fluxo de trabalho {#workflowstart}

Ao criar, é possível chamar fluxos de trabalho para realizar ações em seus canais; também é possível aplicar mais de um fluxo de trabalho.
Ao aplicar o fluxo de trabalho, especifique as seguintes informações:

* O fluxo de trabalho a ser aplicado.
* Opcionalmente, um título que ajude a identificar a instância do fluxo de trabalho na caixa de entrada de um usuário.
* A carga do workflow.

#### Início do fluxo de trabalho

1. Navegue até o canal ao qual deseja adicionar um comentário.
1. Selecione o canal.
1. Abra a coluna **Linha do Tempo**.
1. Clique no botão (três pontos) ao lado do campo de comentário na parte inferior.

   ![Iniciar Fluxo de Trabalho](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. Selecione **Iniciar Fluxo de Trabalho**.
1. O assistente Criar workflow será aberto para especificar os detalhes do workflow.
1. Selecione **Modelo de fluxo de trabalho** na lista suspensa e insira o título do Fluxo de trabalho.

   ![Iniciar Fluxo de Trabalho](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. Continue clicando em **Avançar**.
1. Na etapa escopo, você pode:
   * **Adicionar conteúdo** para adicionar recursos ao fluxo de trabalho.
   * **Incluir filhos** para especificar que os filhos desse recurso serão incluídos no fluxo de trabalho.
   * A opção **Remover seleção** remove o recurso do fluxo de trabalho.

   ![Iniciar Fluxo de Trabalho](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. Selecione **Criar** para fechar o assistente e criar a instância do fluxo de trabalho.
1. Talvez seja necessário executar algumas ações adicionais para concluir o fluxo de trabalho, dependendo do modelo de fluxo de trabalho selecionado.

   ![Iniciar Fluxo de Trabalho](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
