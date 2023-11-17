---
title: Trabalhar com versões de páginas
description: Saiba como criar, comparar e restaurar versões de suas páginas no AEM.
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 97%

---

# Trabalhar com versões de páginas {#working-with-page-versions}

O controle de versão cria um “instantâneo” de uma página em um momento específico. Com o controle de versão, você pode executar as seguintes ações:

* Criar uma versão de uma página.
* Restaurar uma versão anterior de uma ou mais páginas para:
   * Desfazer alterações feitas nas páginas.
   * Restaurar páginas que foram excluídas.
   * Restaure uma árvore (como em uma data e hora especificadas).
* Visualizar uma versão.
* Comparar a versão atual da página com uma versão anterior.
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
1. Selecione as reticências do campo de comentário para revelar as opções:

   ![Versões no painel da linha do tempo](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Selecione **Salvar como versão**.
1. Insira um **rótulo** e **comentário**, se necessário.

   ![Adicionar etiqueta a uma versão](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Confirme a nova versão com a opção **Criar**.

   As informações na linha do tempo serão atualizadas para indicar a nova versão.

### Criar uma nova versão - Criar com um recurso selecionado {#creating-a-new-version-create-with-a-selected-resource}

1. Navegue para mostrar a página para a qual você deseja criar uma versão.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Selecione a opção **Criar** na barra de ferramentas.
1. A mesma caixa de diálogo é aberta. É possível inserir um **rótulo** e um **comentário**, se necessário.
1. Confirme a nova versão com a opção **Criar**.

A linha do tempo será aberta com as informações atualizadas para indicar a nova versão.

## Restaurar versões {#reinstating-versions}

Depois de criar uma versão da página, há vários métodos para restaurar uma versão anterior:

* a opção **Reverter para esta versão** do painel [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

  Restaure uma versão anterior de uma página selecionada.

* a opção **Restaurar** na parte superior da [barra de ferramentas Ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **Restaurar versão**

     Restaure as versões das páginas especificadas na pasta selecionada no momento. Isso também pode incluir a restauração de páginas excluídas anteriormente.

   * **Restaurar árvore**

     Restaure uma versão de uma árvore inteira em uma data e hora específicas. Isso também pode incluir páginas que foram excluídas anteriormente.

>[!NOTE]
>
>Ao restaurar uma página, a versão criada será parte da nova ramificação.
>
>Para ilustrar:
>
>1. Crie versões de qualquer página.
>1. Os nomes dos rótulos iniciais e do nó da versão serão 1.0, 1.1, 1.2 e assim por diante.
>1. Restaure a primeira versão; ou seja, a 1.0.
>1. Crie as versões novamente.
>1. Os rótulos e nomes de nó gerados agora serão 1.0.0, 1.0.1, 1.0.2 e assim por diante.

### Reverter para uma versão {#revert-to-a-version}

Para **Reverter** a página selecionada para uma versão anterior:

1. Navegue até a página que deseja reverter para uma versão anterior.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**. As versões da página selecionada serão listadas.
1. Selecione a versão para a qual deseja reverter. As opções possíveis são mostradas:

   ![Reverter para essa versão](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Reverter para essa versão**. A versão selecionada é restaurada e as informações na linha do tempo são atualizadas.

### Restaurar versão {#restore-version}

Este método pode ser usado para restaurar versões de páginas especificadas na pasta atual. Isso também pode incluir a restauração de páginas excluídas anteriormente:

1. Navegue até a pasta necessária e [selecione-a](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).

1. Selecione **Restaurar** e, em seguida, **Restaurar versão** na [barra de ferramentas de ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar) localizada na parte superior.

   >[!NOTE]
   >
   >Se você tiver:
   >
   >* selecionado uma página única que nunca teve páginas secundárias,
   >* ou se nenhuma das páginas na pasta tiver versões,
   >
   >A exibição fica vazia porque não há versões aplicáveis.

1. As versões disponíveis estão listadas:

   ![Restaurar versão - Lista de todas as páginas na pasta](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. Para escolher uma página específica, use o seletor suspenso em **RESTAURAR À VERSÃO** para selecionar a versão necessária dessa página.

   ![Restaurar versão - Selecionar versão](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. Na exibição principal, selecione a página que deseja restaurar:

   ![Restaurar versão - Selecionar página](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. Selecione **Restaurar** para que a versão selecionada da página seja restaurada como a versão atual.

>[!NOTE]
>
>A ordem em que você seleciona uma página desejada e a versão relacionada é intercambiável.

### Restaurar árvore {#restore-tree}

Esse método pode ser usado para restaurar uma versão de uma árvore em uma data e hora específicas. Isso pode incluir páginas que foram excluídas anteriormente:

1. Navegue até a pasta desejada e [selecione-a](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).

1. Selecione **Restaurar** e, em seguida, **Restaurar árvore** na [barra de ferramentas de ações](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar) localizada na parte superior. A versão mais recente da árvore será mostrada:

   ![Restaurar árvore](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Use o seletor de data e hora em **Últimas versões na data** para selecionar outra versão da árvore, ou seja, a que será restaurada.

1. Defina o sinalizador **Páginas sem controle de versão preservadas** conforme necessário:

   * Se estiver ativo (selecionado), quaisquer páginas sem controle de versão serão mantidas e não serão afetadas pela restauração.

   * Se estiver inativo (não selecionado), quaisquer páginas sem controle de versão serão removidas, pois não existiam na árvore com controle de versões.

1. Selecione **Restaurar** para que a versão selecionada da árvore seja restaurada como a versão *atual*.

## Visualização de uma versão   {#previewing-a-version}

É possível visualizar uma versão específica:

1. Navegue até a página que deseja comparar.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**.
1. As versões da página são listadas. Selecione a versão que deseja visualizar:

   ![Versão de visualização](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Visualizar**. A página é exibida em uma nova guia.

   >[!CAUTION]
   >
   >Se uma página tiver sido movida, não será mais possível visualizar versões criadas antes da movimentação.
   >
   >Se tiver problemas com uma visualização, verifique a [linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) da página para ver se a página foi movida.

## Comparar uma versão com a página atual {#comparing-a-version-with-current-page}

Para comparar uma versão anterior com a página atual:

1. Navegue até a página que deseja comparar.
1. Selecione a página no [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra a coluna **Linha do tempo** e selecione **Mostrar tudo** ou **Versões**.
1. As versões da página são listadas. Selecione a versão que deseja comparar:

   ![Comparar versões](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Selecione **Comparar com a atual**. A variável [diferencial de páginas](/help/sites-cloud/authoring/features/page-diff.md) é aberta, exibindo as diferenças.

## Timewarp   {#timewarp}

O Timewarp é um recursos criado para simular o estado *publicado* de uma página em ocasiões específicas no passado.

>[!TIP]
>
>[O Timewarp também pode ser usado com Inicializações para visualizar o futuro](/help/sites-cloud/authoring/launches/preview.md).

Como a criação de conteúdo é um processo contínuo e colaborativo, o objetivo do Timewarp é permitir que autores(as) rastreiem o site publicado ao longo do tempo, para entender como o conteúdo mudou. Esse recurso usa as versões de página para determinar o estado do ambiente de publicação.

Para usar este recurso:

* O sistema procura a versão da página que estava ativa no momento selecionado.
* Isso significa que a versão mostrada foi criada/ativada *antes* do momento selecionado no Timewarp.
* Ao navegar para uma página que foi excluída, isso também será renderizado, desde que as versões antigas da página ainda estejam disponíveis no repositório.
* Se nenhuma versão publicada for encontrada, o Timewarp reverterá para o estado atual da página no ambiente de criação (o objetivo é evitar um erro de página/404, que poderia impedir a navegação).

### Uso do Timewarp {#using-timewarp}

O Timewarp é um [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) do editor de páginas. Para iniciá-lo, basta ativá-lo como faria com qualquer outro modo.

1. Inicie o editor da página em que deseja iniciar o Timewarp e selecione **Timewarp** na seleção de modo.

   ![Modo Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. Na caixa de diálogo, defina uma data e hora de destino e clique ou toque em **Definir data**. Se você não selecionar uma hora, o padrão será a hora atual.

   ![Data de destino do Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. A página é exibida com base no conjunto de datas. O modo Timewarp é indicado pela barra de status azul na parte superior da janela. Use os links na barra de status para selecionar uma nova data de destino ou sair do modo Timewarp.

   ![No modo Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Limitações do Timewarp {#timewarp-limitations}

O Timewarp se esforça ao máximo para reproduzir uma página em um ponto selecionado no tempo. No entanto, devido às complexidades da criação contínua de conteúdo no AEM, isso nem sempre é possível. Lembre-se dessas limitações ao usar o Timewarp.

* **O Timewarp funciona com base nas páginas publicadas**: o Timewarp só funcionará por completo se você tiver publicado a página anteriormente. Caso contrário, ele mostrará a página atual no ambiente de criação.
* **O Timewarp usa versões de página**: se você navegar para uma página que foi removida/excluída do repositório, ela será renderizada corretamente se ainda houver versões antigas disponíveis no repositório.
* **As versões removidas afetam o Timewarp** - se as versões forem removidas do repositório, o Timewarp não poderá mostrar a exibição correta.
* **O Timewarp é somente leitura** - não é possível editar a versão antiga da página. Ela só está disponível para exibição. Se deseja restaurar a versão mais antiga, é necessário fazer isso manualmente usando a opção [Restaurar](#revert-to-a-version).
* **O Timewarp é baseado no conteúdo da página**: se os elementos de renderização do site forem alterados, como código, CSS e ativos, a exibição será diferente da original. Esses itens não têm um controle de versão no repositório.

>[!CAUTION]
>
>O Timewarp foi criado como ferramenta para auxiliar os autores a compreender e criar conteúdo. Ele não se destina a ser um registro de auditoria ou a fins legais.
