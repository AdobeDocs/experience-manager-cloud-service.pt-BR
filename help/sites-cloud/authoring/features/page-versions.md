---
title: Trabalhar com versões de páginas
description: Criar, comparar e restaurar versões de uma página
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
source-git-commit: 2d1b40b8d6f7b6ca5ce112331a7d389816739494
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 66%

---

# Trabalhar com versões de páginas {#working-with-page-versions}

O controle de versão cria um “instantâneo” de uma página em um ponto no tempo específico. Com o controle de versão, você pode executar as seguintes ações:

* Criar uma versão de uma página.
* Instale novamente uma versão anterior de uma ou mais páginas para:
   * Desfazer alterações feitas nas páginas.
   * Restaurar páginas que foram excluídas.
   * Restaure uma árvore (como em uma data e hora especificadas).
* Visualize uma versão.
* Comparar a versão atual de uma página com uma versão anterior.
   * As diferenças no texto e nas imagens são destacadas.
* O Timewarp usa as versões de página para determinar o estado do ambiente de publicação.

## Criar uma nova versão   {#creating-a-new-version}

É possível criar uma versão do recurso usando:

* O [painel Linha do tempo](#creating-a-new-version-timeline)
* A opção [Criar](#creating-a-new-version-create-with-a-selected-resource) (quando um recurso estiver selecionado)

### Criar uma nova versão - Linha do tempo {#creating-a-new-version-timeline}

1. Navegue para mostrar a página para a qual você deseja criar uma versão.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra o painel **Linha do tempo**.
1. Clique/toque no elipse do campo de comentário para revelar as opções:

   ![Versões no painel da linha do tempo](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Selecione **Salvar como versão**.
1. Insira um **Rótulo** e **Comentário**, se necessário.

   ![Adicionar etiqueta a uma versão](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Confirme a nova versão com a opção **Criar**.

   As informações na linha do tempo serão atualizadas para indicar a nova versão.

### Criar uma nova versão - Criar com um recurso selecionado {#creating-a-new-version-create-with-a-selected-resource}

1. Navegue para mostrar a página para a qual você deseja criar uma versão.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Selecione a opção **Criar** na barra de ferramentas.
1. A mesma caixa de diálogo será aberta. É possível inserir um **Rótulo** e um **Comentário**, se necessário.
1. Confirme a nova versão com a opção **Criar**.

A linha do tempo será aberta com as informações atualizadas para indicar a nova versão.

## Reposição de versões {#reinstating-versions}

Depois de criar uma versão da página, há vários métodos para restabelecer uma versão anterior:

* o **Reverter para esta versão** da [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) trilho

   Instale novamente uma versão anterior de uma página selecionada.

* o **Restaurar** opções na parte superior [barra de ferramentas ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **Restaurar versão**

      Instale novamente as versões das páginas especificadas na pasta atualmente selecionada; isso também pode incluir a restauração de páginas que foram excluídas anteriormente.

   * **Restaurar árvore**

      Retomar uma versão de uma árvore inteira em uma data e hora especificadas; isso pode incluir páginas que foram excluídas anteriormente.

>[!NOTE]
>
>Ao reinstalar uma página, a versão criada fará parte de uma nova ramificação.
>
>Para ilustrar:
>
>1. Crie versões de qualquer página.
>1. Os nomes dos rótulos iniciais e do nó da versão serão 1.0, 1.1, 1.2 e assim por diante.
>1. Reinstale a primeira versão; ou seja, 1.0.
>1. Crie novas versões novamente.
>1. Os rótulos e os nomes de nó gerados agora serão 1.0.0, 1.0.1, 1.0.2 etc.


### Reverter para uma versão {#revert-to-a-version}

Para **Reverter** a página selecionada para uma versão anterior:

1. Navegue para mostrar a página para a qual você deseja reverter para uma versão anterior.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**. As versões de página da página selecionada serão listadas.
1. Selecione a versão para a qual você deseja reverter. As opções possíveis serão mostradas:

   ![Reverter para essa versão](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Reverter para esta versão**. A versão selecionada será restaurada e as informações na linha do tempo serão atualizadas.

### Restaurar versão {#restore-version}

Este método pode ser usado para restaurar versões de páginas especificadas na pasta atual; isso também pode incluir a restauração de páginas que foram excluídas anteriormente:

1. Navegue até e [select](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), a pasta necessária.

1. Selecionar **Restaurar**, em seguida **Restaurar versão** na parte superior [barra de ferramentas ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar).

   >[!NOTE]
   >
   >Se, você:
   >* você selecionou uma única página que nunca teve páginas secundárias,
   >* ou nenhuma das páginas na pasta tem versões,

   >
   >Em seguida, a exibição estará vazia, pois não há versões aplicáveis.

1. As versões disponíveis serão listadas:

   ![Restaurar versão - Lista de todas as páginas na pasta](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. Para uma página específica, use o seletor suspenso em **RESTAURAR PARA VERSÃO** para selecionar a versão necessária para essa página.

   ![Restaurar versão - Selecionar versão](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. Na exibição principal, selecione a página desejada a ser restaurada:

   ![Restaurar versão - Selecionar página](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. Selecionar **Restaurar** para a versão selecionada, da página selecionada, a ser restaurada como a versão atual.

>[!NOTE]
>
>A ordem em que você seleciona uma página obrigatória e a versão relacionada é intercambiável.

### Restaurar árvore {#restore-tree}

Esse método pode ser usado para restaurar uma versão de uma árvore como em uma data e hora especificadas; isso pode incluir páginas que foram excluídas anteriormente:

1. Navegue até e [select](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), a pasta necessária.

1. Selecionar **Restaurar**, em seguida **Restaurar árvore** na parte superior [barra de ferramentas ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar). A versão mais recente da árvore será mostrada:

   ![Restaurar árvore](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Use o seletor de data e hora em **Últimas versões na data** para selecionar outra versão da árvore - a que será restaurada.

1. Definir o sinalizador **Páginas sem versão preservadas** conforme necessário:

   * Se estiver ativo (selecionado), quaisquer páginas sem versão serão mantidas e não serão afetadas pela restauração.

   * Se estiver inativo (não selecionado), quaisquer páginas sem versão serão removidas, pois não existiam na árvore com versão.

1. Selecionar **Restaurar** para a versão selecionada da árvore a ser restaurada como a *atual* versão.

## Visualização de uma versão   {#previewing-a-version}

É possível visualizar uma versão específica:

1. Navegue para mostrar a página que você deseja comparar.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**.
1. As versões de página serão listadas. Selecione a versão que você deseja visualizar:

   ![Versão de visualização](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Visualizar**. A página será exibida em uma nova guia.

   >[!CAUTION]
   >
   >Se uma página tiver sido movida, você não poderá mais executar uma visualização em versões feitas antes do movimento.
   >
   >Se você tiver problemas com uma visualização, verifique a [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para ver se a página foi movida.

## Comparar uma versão com a página atual {#comparing-a-version-with-current-page}

Para comparar uma versão anterior com a página atual:

1. Navegue para mostrar a página que você deseja comparar.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**.
1. As versões de página serão listadas. Selecione a versão que você deseja comparar:

   ![Comparar versões](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Comparar a atual**. O [diferencial de páginas](/help/sites-cloud/authoring/features/page-diff.md) será aberto e exibirá as diferenças.

## Timewarp   {#timewarp}

O Timewarp é um recursos criado para simular o estado *publicado* de uma página em ocasiões específicas no passado.

>[!TIP]
>
>[O Timewarp também pode ser usado com Inicializações para visualizar o futuro.](/help/sites-cloud/authoring/launches/preview.md)

Como a criação de conteúdo é um processo contínuo e colaborativo, o objetivo do Timewarp é permitir que os autores rastreiem o site publicado ao longo do tempo, para entender como o conteúdo mudou. Esse recurso usa as versões de página para determinar o estado do ambiente de publicação.

Para fazer isso:

* O sistema procura a versão de página que estava ativa no momento selecionado.
* Isso significa que a versão mostrada foi criada/ativada *antes* do ponto no tempo selecionado no Timewarp.
* Durante a navegação para uma página que foi excluída, isso também será renderizado - desde que as versões antigas da página ainda estejam disponíveis no repositório.
* Se nenhuma versão publicada for encontrada, o Timewarp reverterá para o estado atual da página no ambiente de criação (o objetivo é evitar um erro de página/404, que poderia impedir a navegação).

### Uso do Timewarp {#using-timewarp}

O Timewarp é um [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) do editor de páginas. Para iniciá-lo, basta ativá-lo como você faria com qualquer outro modo.

1. Inicie o editor da página em que você deseja iniciar o Timewarp e selecione **Timewarp** na seleção do modo.

   ![Modo Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. Na caixa de diálogo, defina uma data e hora de destino e clique ou toque em **Definir data**. Se você não selecionar uma hora, a hora atual será padrão.

   ![Data de destino do Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. A página é exibida com base na data definida. O modo Timewarp é indicado na barra de status azul localizada na parte superior da janela. Use os links na barra de status para selecionar uma nova data de destino ou para sair do modo Timewarp.

   ![No modo Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Limitações do Timewarp {#timewarp-limitations}

O Timewarp se esforça ao máximo para reproduzir uma página em um ponto selecionado no tempo. No entanto, devido às complexidades da criação contínua de conteúdo no AEM, isso nem sempre é possível. Essas limitações devem ser levadas em conta ao usar o Timewarp.

* **O Timewarp funciona com base nas páginas publicadas** - o Timewarp só funcionará totalmente se você tiver publicado a página anteriormente. Caso contrário, o Timewarp mostrará a página atual no ambiente de criação.
* **O Timewarp usa versões de página** - se você navegar para uma página que foi removida/excluída do repositório, ela será renderizada corretamente se ainda houver versões antigas disponíveis no repositório.
* **As versões removidas afetam o Timewarp** - se as versões forem removidas do repositório, o Timewarp não poderá mostrar a exibição correta.
* **O Timewarp é somente leitura** - não é possível editar a versão antiga da página. Ela só está disponível para exibição. Se você deseja restaurar a versão mais antiga, é necessário fazer isso manualmente usando [restaurar](#revert-to-a-version).
* **O Timewarp é baseado apenas no conteúdo da página** - se os elementos (como código, css, ativos/imagens, etc) para renderização do site forem alterados, a exibição será diferente da original, pois esses itens não têm controle de versão no repositório.

>[!CAUTION]
>
>O Timewarp foi criado como ferramenta para auxiliar os autores a compreender e criar conteúdo. Ele não se destina a ser um registro de auditoria ou a fins legais.
