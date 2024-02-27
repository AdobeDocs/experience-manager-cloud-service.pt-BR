---
title: Gerenciamento de páginas
description: Saiba como gerenciar as páginas do seu site no AEM, incluindo movimentação, cópia e exclusão.
source-git-commit: faac7c803a5145f4207154bfb3c9aa06274bbb86
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 64%

---


# Gerenciamento de páginas {#managing-pages}

Saiba como gerenciar as páginas do seu site no AEM, incluindo movimentação, cópia e exclusão.

>[!TIP]
>
>Antes de começar a gerenciar suas páginas, familiarize-se com o [como suas páginas estão organizadas no AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

>[!TIP]
>
>Há vários [atalhos de teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) que você pode usar no console sites, que torna a organização das suas páginas mais eficiente.

## Privilégios de Acesso {#access-privileges}

Sua conta precisa de direitos de acesso apropriados e permissões para atuar em páginas como criar, copiar, mover, editar, excluir.

Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

## Abrir uma página para edição {#opening-a-page-for-editing}

Depois [criação de uma página](/help/sites-cloud/authoring/sites-console/creating-pages.md) ou navegar para uma página existente usando [o **Sites** console,](/help/sites-cloud/authoring/sites-console/introduction.md) você pode abri-lo para edição.

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue para localizar a página que deseja editar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e a barra de ferramentas

1. Toque ou clique no **Editar** ícone.

   ![Botão Editar](/help/sites-cloud/authoring/assets/edit.png)

1. A página é aberta e você pode editá-la conforme necessário. Dependendo de como a página selecionada foi criada, a variável **Editar** Essa ação abrirá o editor apropriado.
   * [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) - Para páginas criadas com o Editor de páginas AEM
   * [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) - Para páginas criadas com o Editor universal

## Copiar e colar uma página      {#copying-and-pasting-a-page}

É possível copiar uma página e todas as respectivas subpáginas para um novo site:

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue para localizar a página que deseja copiar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e a barra de ferramentas

1. Toque ou clique no **Copiar** ícone da página.

   ![Copiar](/help/sites-cloud/authoring/assets/copy.png)

1. Navegue até o local para a nova cópia da página.
1. Selecione o **Colar** ícone que ficou disponível.

   ![Colar](/help/sites-cloud/authoring/assets/paste.png)

1. A caixa de diálogo Colar apresenta um resumo da transação de colagem e a capacidade de:
   * **Nome do novo site:** alterar o nome da página colada
   * **Colar sem páginas secundárias:** omitir as páginas secundárias da página selecionada ao colar (por padrão, as páginas secundárias são coladas)

   ![Caixa de diálogo Colar](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Selecione o **Colar** botão para confirmar a transação de colagem e criar a(s) nova(s) página(s).

>[!NOTE]
>
>Se você copiar a página para um local onde uma página com o mesmo nome que a original já existir, o sistema gerará automaticamente uma variação do nome anexando um número. Por exemplo, se `beach` já existir, uma nova página com o nome `beach` se tornará `beach1`.

>[!NOTE]
>
>Caso esteja no modo de seleção ao iniciar a ação de colagem, ele será encerrado automaticamente assim que a página for copiada.

## Mover ou renomear uma página {#moving-or-renaming-a-page}

O procedimento para mover ou renomear uma página é basicamente o mesmo e é realizado pelo assistente Mover página. Com este assistente você pode:

* Renomear uma página sem movê-la.
* Mover a página sem renomeá-la.
* Mover e renomear ao mesmo tempo.

O AEM oferece a funcionalidade de atualizar todos os links internos que se referem à página que está sendo renomeada/movida. Isso pode ser feito página por página para proporcionar total flexibilidade.

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue para localizar a página que deseja mover.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e a barra de ferramentas

1. Toque ou clique no **Mover** ícone de página para abrir o assistente para mover página.

   ![Botão Mover](/help/sites-cloud/authoring/assets/move.png)

1. No **Renomear** etapa do assistente, é possível:

   * Especifique o nome que deseja para a página após movê-la, depois selecione **Próxima** para continuar.
   * **Cancelar** para suspender o processo.

   ![Mover e renomear página](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * O nome da página pode permanecer o mesmo se você estiver apenas movendo a página.

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `beach` já existir, uma nova página com o nome `beach` se tornará `beach1`.

1. No **Selecionar destino** etapa do assistente, é possível:

   * Use a [exibição de coluna](/help/sites-cloud/authoring/basic-handling.md#column-view) para navegar até o novo local da página:

      * Para selecionar o destino, clique em sua miniatura.
      * Clique em **Avançar** para continuar.

   * Use **Voltar** para retornar à especificação do nome da página.

   >[!NOTE]
   >
   >Por padrão, o principal da página que você está movendo ou renomeando é selecionada como destino.

   ![Selecionar destino de movimentação da página](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `winter` já existir, `winter` se tornará `winter1`.

1. Se a página tiver um link, uma referência ou tiver sido publicada, os detalhes serão listados na etapa **Ajustar/Republicar**.

   * Você pode indicar o que deve ser ajustado e/ou republicado, conforme necessário.

   >[!NOTE]
   >
   >Se a página não estiver vinculada nem referenciada, essa etapa não estará disponível.

   ![Republicar página ao mover](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Toque ou clique **Mover** para definir quando a ação de mover deve ocorrer.

   * **Agora** acionará um [trabalho assíncrono](#asynchronous-actions) para mover a página imediatamente.
   * **Mais tarde** permitirá que você programe uma data para a movimentação ser processada.

   ![Definição de quando mover](assets/managing-pages-move-page-now-later.png)

1. Toque ou clique **Continuar** para concluir a movimentação da página.

>[!NOTE]
>
>Se a página já tiver sido publicada, movê-la cancelará automaticamente a publicação. Por padrão, ela é publicada novamente quando a movimentação é concluída, mas isso pode ser alterado desmarcando o campo **Republicar** na etapa **Ajustar/Republicar**.

>[!NOTE]
>
>A renomeação de uma página também está sujeita às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar o nome da nova página.

>[!NOTE]
>
>Uma página só pode ser movida para um local que permita o uso do modelo no qual a página se baseia. Consulte [Disponibilidade de modelo](/help/implementing/developing/components/templates.md#template-availability) para obter mais informações.

### Ações assíncronas {#asynchronous-actions}

As ações de movimentação de página são sempre processadas de forma assíncrona, permitindo que o usuário continue a criação na interface do usuário desimpedida.

O status de trabalhos assíncronos pode ser verificado no campo [**Status de trabalhos assíncronos** painel](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação global** > **Ferramentas** > **Operações** > **Tarefas**

>[!TIP]
>
>Para obter mais informações sobre o processamento de trabalhos assíncronos e sobre como configurar o limite para ações de mover/renomear páginas, consulte o documento [Trabalhos assíncronos](/help/operations/asynchronous-jobs.md) no guia de Operações.

### Excluir uma página {#deleting-a-page}

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue até a página que deseja excluir.
1. Use o [modo de seleção](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) para selecionar a página pretendida, em seguida, use **Excluir** na barra de ferramentas:

   ![Botão Excluir](/help/sites-cloud/authoring/assets/delete.png)

1. Uma caixa de diálogo pedirá confirmação.

   ![Caixa de diálogo Excluir](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Você deseja arquivar as páginas antes de excluir?** - Se marcada, as versões das páginas selecionadas para exclusão serão criadas na exclusão.
      * [As versões podem ser restauradas em uma data posterior](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * As páginas excluídas sem versões anteriores não podem ser restauradas.
1. Toque ou clique **Cancelar** para suspender a ação ou **Excluir** para confirmar a ação
   * Se a página não tiver referências, a página será excluída.
   * Se a página tiver referências, uma caixa de mensagem informará que **Uma ou mais páginas são mencionadas.** É possível selecionar **Forçar Exclusão** ou **Cancelar**.

>[!NOTE]
>
>Se uma página já estiver publicada, sua publicação será automaticamente removida antes da exclusão.

### Bloquear uma página   {#locking-a-page}

É possível [bloquear/desbloquear uma página](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) a partir de um console ou ao editar uma página individual. As informações sobre se uma página está bloqueada também são exibidas em ambos os locais.

![Botão Bloquear](/help/sites-cloud/authoring/assets/lock.png)
![Botão Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

### Criação de uma nova pasta {#creating-a-new-folder}

Você pode criar pastas para ajudar a organizar seus arquivos e páginas.

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue até o local necessário.
1. Para abrir a lista de opções, selecione **Criar** na barra de ferramentas
1. Selecione **Pasta** para abrir a caixa de diálogo. Aqui você pode inserir o **Nome** e o **Título**:

   ![Criar pasta](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Selecione **Criar** para criar a pasta.

>[!NOTE]
>
>* As pastas também estão sujeitas às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar um novo nome de pasta.
>* Pastas só podem ser criadas diretamente em **Sites** ou em outras pastas. Elas não podem ser criadas em uma página.
>* As ações padrão de mover, copiar, colar, excluir, publicar, cancelar a publicação e exibir/editar propriedades podem ser executadas em uma pasta.
>* As pastas não estão disponíveis para seleção em uma live copy.
