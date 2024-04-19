---
title: Criar e organizar páginas
description: Saiba como organizar seu site criando e gerenciando páginas com AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '2424'
ht-degree: 85%

---


# Criar e organizar páginas {#creating-and-organizing-pages}

Este documento descreve como criar e gerenciar páginas com o Adobe Experience Manager Cloud Service para depois usá-las para [criar o conteúdo](/help/sites-cloud/authoring/fundamentals/editing-content.md).

>[!NOTE]
>
>Sua conta precisa de direitos de acesso apropriados e permissões para atuar em páginas como criar, copiar, mover, editar, excluir.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to act on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Há vários [atalhos de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) que você pode usar no console sites, que torna a organização das suas páginas mais eficiente.

{{edge-delivery-authoring}}

## Organizar seu site {#organizing-your-website}

Como autor, você precisa organizar seu site dentro do AEM. Isso envolve criar e nomear suas páginas de conteúdo de modo que:

* Você pode encontrá-las facilmente no ambiente de criação
* Os visitantes do seu site possam navegar facilmente por elas no ambiente de publicação

Você também pode usar [pastas](#creating-a-new-folder) para ajudar a organizar o seu conteúdo.

A estrutura de um site pode ser considerada como uma árvore que armazena suas páginas de conteúdo. Os nomes dessas páginas de conteúdo são usadas para formar os URLs, ao passo que os títulos são mostrados quando o conteúdo da página é visualizado.

O exemplo a seguir mostra o site [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR), onde um artigo sobre skateparks ( `la-skateparks`) é acessado:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Esta estrutura pode ser visualizada do console **Sites**, onde é possível [navegar através das páginas do seu site](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e executar ações nas páginas. Você também pode criar novos sites e [páginas](#creating-a-new-page).

De qualquer ponto, você pode visualizar a ramificação ascendente da navegação estrutural na barra do cabeçalho:

![Uso de navegações estruturais para navegar](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Convenções de nomenclatura da página {#page-naming-conventions}

Ao criar uma página, há dois campos principais:

* **[Título](#title)**:

   * O título é exibido ao usuário no console, na parte superior do conteúdo da página ao editar.
   * Esse campo é obrigatório.

* **[Nome](#name)**:

   * Usado para gerar o URI.
   * A entrada do usuário para este campo é opcional. Se não especificado, o nome é derivado do título. Consulte a seguinte seção [Restrições de nome de página e práticas recomendadas](#page-name-restrictions-and-best-practices) para obter detalhes.

#### Restrições de nome de página e práticas recomendadas {#page-name-restrictions-and-best-practices}

O **Título** da página e o **Nome** podem ser criados separadamente, mas estão relacionados:

* Ao criar uma página, somente o campo **Título** é obrigatório. Se nenhum **Nome** for fornecido na criação da página, o AEM gerará um nome a partir dos primeiros 64 caracteres do título (observando o conjunto definido abaixo). Somente os primeiros 64 caracteres são usados para seguir a prática recomendada de nomes de página curtos.
* Se um nome de página for especificado manualmente pelo autor, o limite de 64 caracteres não se aplicará. Contudo, outras limitações técnicas no comprimento de nome de página poderão ser aplicadas.

>[!TIP]
>
>Ao definir um nome de página, um princípio básico é manter o nome da página curto, mas tão expressivo e memorável quanto possível para facilitar a compreensão do leitor. Consulte o [guia de estilo W3C](https://www.w3.org/Provider/Style/TITLE.html) no elemento `title`para obter mais informações.
>
>Lembre-se também de que alguns navegadores (por exemplo, versões mais antigas do IE) só podem aceitar URLs com um limite de comprimento, por isso também há um motivo técnico para manter os nomes de página curtos.

Ao criar uma página, AEM [valida o nome da página de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostos pelo AEM e pelo JCR.

Os caracteres mínimos permitidos são:

* `a` a `z`
* `A` a `Z`
* `0` a `9`
* `_` (sublinhado)
* `-` (hífen/sinal de menos)

Detalhes completos sobre todos os caracteres permitidos podem ser encontrados nas [convenções de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Os nomes de página são limitados a 150 caracteres.

#### Título {#title}

Se você fornecer apenas uma página **Título** ao criar uma página, o AEM deriva a página **Nome** desta cadeia de caracteres e [validar o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostos pelo AEM e pelo JCR.

Um campo de **Título** contendo caracteres inválidos é aceito, mas o nome derivado terá os caracteres inválidos substituídos. Por exemplo:

| Título | Nome derivado |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### Nome {#name}

Quando você fornece uma página **Nome** ao criar uma página, AEM [valida o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostos pelo AEM e pelo JCR. Não é possível inserir caracteres inválidos no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é destacado com uma mensagem explicativa.

![Exemplo de inserção de um nome de página inválido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Evite usar um código de duas letras, conforme definido por ISO-639-1 como um nome de página, a menos que seja uma raiz de idioma.
>
>Consulte [Preparação de conteúdo para tradução](/help/sites-cloud/administering/translation/preparation.md) para obter mais informações.

### Modelos {#templates}

No AEM, um modelo especifica um tipo especializado de página. Um modelo é usado como a base para qualquer nova página que está sendo criada.

O modelo define a estrutura de uma página, incluindo uma imagem em miniatura e outras propriedades. Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de site e informações de contato. Os modelos são compostos de [componentes](#components).

O AEM vem com vários modelos prontos para uso. Os modelos disponíveis dependem do site individual. Os campos principais são:

* **Título** O título exibido na página da Web resultante.

* **Nome** Usado ao nomear a página.

* **Modelo** Uma lista de modelos disponíveis para uso ao gerar a nova página.

>[!TIP]
>
>Se configurado na instância,[ os autores de modelo poderão criá-los com o Editor de modelo](/help/sites-cloud/authoring/features/templates.md).

### Componentes {#components}

Os componentes são os elementos fornecidos pelo AEM, desse modo, é possível adicionar tipos específicos de conteúdo. O AEM vem com vários componentes prontos para uso que fornecem funcionalidade abrangente. Esses componentes incluem:

* Texto
* Imagem
* Título
* Carrossel
* E muito mais

Depois de criar e abrir uma página, é possível [adicionar conteúdo usando os componentes](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), que estão disponíveis no [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>O console [Componentes](/help/sites-cloud/authoring/features/components-console.md) fornece uma visão geral dos componentes na instância.

## Gerenciamento de páginas {#managing-pages}

### Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, é necessário criar uma página antes de começar a criar o conteúdo:

1. Abra o console Sites (por exemplo, `https://<host>:<port>/sites.html/content`.
1. Navegue até o local onde deseja criar a nova página.
1. Abra o seletor suspenso usando **Criar** na barra de ferramentas e selecione **Página** na lista:

   ![Criação de uma página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. A partir do primeiro estágio do assistente, você pode:

   * Selecione o modelo que deseja usar para criar a nova página e selecione **Próxima** para continuar.

   * **Cancelar** para suspender o processo.

   ![Seleção de um modelo para uma nova página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. A partir do último estágio do assistente, você pode:

   * Use as três guias para inserir a variável [propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md) que deseja atribuir à nova página, selecione **Criar** para realmente criar a página.

   * Use **Voltar** para retornar à seleção do modelo.

   Os campos principais são:

   * **Título**:

      * Ele é exibido ao usuário e é obrigatório.

   * **Nome**:

      * Usado para gerar o URI. Se não especificado, o nome é derivado do título.
      * Se você fornecer uma página **Nome** ao criar uma página, AEM [valida o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostos pelo AEM e pelo JCR.
      * **Não é possível inserir caracteres inválidos** no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é destacado e uma mensagem explicativa é exibida para indicar os caracteres que precisam ser removidos/substituídos.

   >[!TIP]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   As informações mínimas necessárias para criar uma página são **Título**.

   ![Fornecimento do título da página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Use **Criar** para concluir o processo e criar a sua nova página. A caixa de diálogo de confirmação perguntará se você deseja **Abrir** a página imediatamente ou voltar para o console (**concluído**):

   ![Êxito na criação da página](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Caso crie uma página usando um nome que já existe no local, o sistema vai gerar automaticamente uma variação do nome, ao anexar um número. Por exemplo, se `beach` já existir, uma nova página se tornará `beach1`.

1. Se você retornar ao console, poderá ver sua nova página:

   ![Nova página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Assim que uma página tiver sido criada, seu modelo não poderá ser alterado, a menos que você [crie um lançamento com um novo modelo; ](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)porém, o conteúdo existente será perdido.

### Abrir uma página para edição {#opening-a-page-for-editing}

Após criar uma página ou navegar para uma página existente (no console), você pode abri-la para edição:

1. Abra o console do **Sites**.
1. Navegue até encontrar a página que deseja editar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas

   E, em seguida, selecione o ícone **Editar**:

   ![Botão Editar](/help/sites-cloud/authoring/assets/edit.png)

1. A página é aberta e será possível [editá-la](/help/sites-cloud/authoring/fundamentals/editing-content.md) conforme necessário.

>[!NOTE]
>
>Navegar para outras páginas do editor de páginas só é possível no modo de visualização, pois os links não estão ativos no modo de Edição...

### Copiar e colar uma página      {#copying-and-pasting-a-page}

É possível copiar uma página e todas as respectivas subpáginas para um novo site:

1. No console do **Sites**, navegue até encontrar a página que deseja copiar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas

   E, em seguida, o ícone da página **Copiar**:

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

### Mover ou renomear uma página {#moving-or-renaming-a-page}

O procedimento para mover ou renomear uma página é basicamente o mesmo e é realizado pelo assistente Mover página. Com este assistente você pode:

* Renomear uma página sem movê-la
* Mover a página sem renomeá-la
* Mover e renomear ao mesmo tempo

O AEM oferece a funcionalidade de atualizar todos os links internos que se referem à página que está sendo renomeada/movida. Isso pode ser feito página por página para proporcionar total flexibilidade.

1. Navegue até encontrar a página que deseja mover.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas

   Em seguida, selecione o ícone de página **Mover**:

   ![Botão Mover](/help/sites-cloud/authoring/assets/move.png)

   Isso abre o assistente para mover página.

1. No estágio **Renomear** do assistente, é possível:

   * Especifique o nome que deseja para a página após movê-la, depois selecione **Próxima** para continuar.
   * **Cancelar** para suspender o processo.

   ![Mover e renomear página](/help/sites-cloud/authoring/assets/move-page-rename.png)

   O nome da página pode permanecer o mesmo se você estiver apenas movendo a página.

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `beach` já existir, uma nova página com o nome `beach` se tornará `beach1`.

1. No estágio **Selecionar destino** do assistente, é possível:

   * Use a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) para navegar até o novo local da página:

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

   Você pode indicar o que deve ser ajustado e/ou republicado, conforme necessário.

   >[!NOTE]
   >
   >Se a página não estiver vinculada nem referenciada, essa etapa não estará disponível.

   ![Republicar página ao mover](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Selecionar **Mover** concluirá o processo e moverá/renomeará a página conforme apropriado.

>[!NOTE]
>
>Se a página já tiver sido publicada, movê-la cancelará automaticamente a publicação. Por padrão, ela é publicada novamente quando a movimentação é concluída, mas isso pode ser alterado desmarcando o campo **Republicar** na etapa **Ajustar/Republicar**.

>[!NOTE]
>
>Se a página não for referenciada de forma alguma, a etapa **Ajustar/Republicar** será ignorada.

>[!NOTE]
>
>A renomeação de uma página também está sujeita às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar o nome da nova página.

>[!NOTE]
>
>Uma página só pode ser movida para um local que permita o uso do modelo no qual a página se baseia. Consulte [Disponibilidade de modelo](/help/implementing/developing/components/templates.md#template-availability) para obter mais informações.

#### Ações assíncronas {#asynchronous-actions}

As ações de movimentação de página são sempre processadas de forma assíncrona, permitindo que o usuário continue a criação na interface do usuário desimpedida.

* O usuário deve definir quando a operação assíncrona deve ser executada
   * **Agora** a execução do trabalho assíncrono começa imediatamente.
   * **Mais tarde** permite que o usuário defina quando o trabalho assíncrono será iniciado.

<!--
  ![Asynchronous page move](assets/asynchronous-page-move.png)
-->

O status de trabalhos assíncronos pode ser verificado no campo [**Status de trabalhos assíncronos** painel](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação global** > **Ferramentas** > **Operações** > **Tarefas**

>[!NOTE]
>
>Para obter mais informações sobre o processamento de trabalhos assíncronos e sobre como configurar o limite para ações de mover/renomear páginas, consulte o documento [Trabalhos assíncronos](/help/operations/asynchronous-jobs.md) no guia de Operações.

### Excluir uma página {#deleting-a-page}

1. Navegue até que você possa visualizar a página que deseja excluir.
1. Use o [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para selecionar a página pretendida, em seguida, use **Excluir** na barra de ferramentas:

   ![Botão Excluir](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Como uma precaução de segurança, o ícone de **Excluir página** não está disponível como uma ação rápida.

1. Uma caixa de diálogo pedirá confirmação.

   ![Caixa de diálogo Excluir](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Você deseja arquivar as páginas antes de excluir?** - Se marcada, as versões das páginas selecionadas para exclusão serão criadas na exclusão.
      * [As versões podem ser restauradas em uma data posterior](/help/sites-cloud/authoring/features/page-versions.md).
      * As páginas excluídas sem versões anteriores não podem ser restauradas.
   * Use a opção **Cancelar** para suspender a ação
   * Clique em **Excluir** para confirmar a ação:

      * Se a página não tiver referências, a página será excluída.
      * Se a página tiver referências, uma caixa de mensagem informará que **Uma ou mais páginas são mencionadas.** É possível selecionar **Forçar Exclusão** ou **Cancelar**.

>[!NOTE]
>
>Se uma página já estiver publicada, sua publicação será automaticamente removida antes da exclusão.

### Bloquear uma página   {#locking-a-page}

É possível [bloquear/desbloquear uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) a partir de um console ou ao editar uma página individual. As informações sobre se uma página está bloqueada também são exibidas em ambos os locais.

![Botão Bloquear](/help/sites-cloud/authoring/assets/lock.png)
![Botão Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

### Criação de uma nova pasta {#creating-a-new-folder}

Você pode criar pastas para ajudar a organizar seus arquivos e páginas.

1. Abra o console **Sites** e navegue até o local necessário.
1. Para abrir a lista de opções, selecione **Criar** na barra de ferramentas
1. Selecione **Pasta** para abrir a caixa de diálogo. Aqui você pode inserir o **Nome** e o **Título**:

   ![Criar pasta](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Selecione **Criar** para criar a pasta.

>[!NOTE]
>
>As pastas também estão sujeitas às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar um novo nome de pasta.

>[!CAUTION]
>
>* Pastas só podem ser criadas diretamente em **Sites** ou em outras pastas. Elas não podem ser criadas em uma página.
>* As ações padrão de mover, copiar, colar, excluir, publicar, cancelar a publicação e exibir/editar propriedades podem ser executadas em uma pasta.
>* As pastas não estão disponíveis para seleção em uma live copy.
