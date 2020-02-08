---
title: Criar e organizar páginas
description: Como criar e organizar páginas com o AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Criar e organizar páginas {#creating-and-organizing-pages}

This document describes how to create and manage pages with Adobe Experience Manager Cloud Service so that you can then [create content](/help/sites-cloud/authoring/fundamentals/editing-content.md) on those pages.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados] e permissões para executar ações em páginas como criar, copiar, mover, editar e excluir.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Há vários [atalhos de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) que você pode usar no console Sites que tornam a organização das suas páginas mais eficiente.

## Organizar seu site {#organizing-your-website}

Como um autor, você precisará organizar o seu site dentro do AEM. Isto implica criar e nomear suas páginas de conteúdo, de modo que:

* Você pode encontrá-las facilmente no ambiente de criação
* Os visitantes do seu site possam navegar facilmente por elas no ambiente de publicação

Você também pode usar [pastas](#creating-a-new-folder) para ajudar a organizar o seu conteúdo.

A estrutura de um site pode ser considerada como uma árvore que armazena suas páginas de conteúdo. Os nomes dessas páginas de conteúdo são usados para formar os URLs, enquanto os títulos são exibidos quando o conteúdo da página é exibido.

A seguir, é mostrado um exemplo do site Tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) WKND, onde um artigo sobre parques de skate ( `la-skateparks`) é acessado:

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

This structure can be viewed From the **Sites** console, where you can [navigate through the pages of your website](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) and perform actions on the pages. Você também pode criar novos sites e [páginas](#creating-a-new-page).

De qualquer ponto, você pode visualizar o ramo ascendente da navegação estrutural na barra do cabeçalho:

![Uso de navegações estruturais para navegar](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Page Naming Conventions {#page-naming-conventions}

Ao criar uma nova página, existem dois campos principais:

* **[Título](#title)**:

   * O título é exibido ao usuário no console, na parte superior do conteúdo da página ao editar.
   * Esse campo é obrigatório.

* **[Nome](#name)**:

   * Usado para gerar o URI.
   * A entrada do usuário para este campo é opcional. Se não for especificado, o nome é derivado do título. Consulte a seguinte seção [Restrições de nome de página e práticas recomendadas](#page-name-restrictions-and-best-practices) para obter detalhes.

#### Restrições de nome de página e práticas recomendadas {#page-name-restrictions-and-best-practices}

O **Título** da página e o **Nome** podem ser criados separadamente, mas estão relacionados:

* Ao criar uma página, somente o campo **Título** é obrigatório. Se nenhum **Nome** for fornecido na criação da página, o AEM gerará um nome a partir dos primeiros 64 caracteres do título (observando o conjunto definido abaixo). Somente os primeiros 64 caracteres são usados para dar suporte à prática recomendada de nomes de página curtos.
* Se um nome de página for especificado manualmente pelo autor, o limite de 64 caracteres não se aplicará. Contudo, outras limitações técnicas no comprimento de nome de página poderão ser aplicadas.

>[!TIP]
>
>Ao definir um nome de página, um princípio básico é manter o nome da página curto, mas tão expressivo e memorável quanto possível para facilitar a compreensão do leitor. See the [W3C style guide](https://www.w3.org/Provider/Style/TITLE.html) for the `title` element for more information.
>
>Lembre-se também de que alguns navegadores (por exemplo, versões mais antigas do IE) só podem aceitar URLs de até um determinado comprimento, por isso também há um motivo técnico para manter os nomes de página curtos.

When creating a new page, AEM will validate the page name according to the conventions imposed by AEM and the JCR. <!--When creating a new page, AEM will [validate the page name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and the JCR.-->

Os caracteres mínimos permitidos são:

* `a` through `z`
* `A` through `Z`
* `0` through `9`
* `_` (sublinhado)
* `-` (hífen/sinal de menos)

Detalhes completos sobre todos os caracteres permitidos podem ser encontrados nas convenções de nomenclatura. <!--Full details of all characters allowed can be found in [the naming conventions](/help/sites-developing/naming-conventions.md).-->

>[!NOTE]
>
>Os nomes das páginas são limitados a 150 caracteres.

#### Título {#title}

Caso forneça apenas um **Título** de página ao criar uma nova página, o AEM vai derivar o **Nome** de página desta cadeia de caracteres e validá-lo de acordo com as convenções impostas pelo AEM e JCR. <!--If you supply only a page **Title** when creating a new page, AEM will derive the page **Name** from this string and [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR.-->

A **Title** field containing invalid characters will be accepted, but the name derived will have the invalid characters substituted. Por exemplo:

| Título | Nome derivado |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;*ç+ | `sc---c-.html` |

#### Nome {#name}

Quando você fornecer um **Nome** de página ao criar uma nova página, o AEM vai  validar o nome de acordo com as convenções impostas pelo AEM e JCR. Não é possível enviar caracteres inválidos no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo será realçado. <!--When you supply a page **Name** when creating a new page, AEM will [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR. You cannot submit invalid characters in the **Name** field. When AEM detects invalid characters the field will be highlighted with an explanatory message.-->

![Exemplo de inserção de um nome de página inválido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Evite usar um código de duas letras, conforme definido por ISO-639-1 como um nome de página, a menos que seja uma raiz de idioma.
>
>Consulte Preparação de conteúdo para tradução para obter mais informações.
<!--
>See [Preparing Content for Translation](/help/sites-administering/tc-prep.md) for more information.
-->

### Modelos {#templates}

No AEM, um modelo especifica um tipo especializado de página. Um modelo será usado como a base para a criação de qualquer página nova.

O modelo define a estrutura de uma página; incluindo uma imagem em miniatura e outras propriedades. Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de sites e informações de contato. Os modelos são compostos de [componentes](#components).

O AEM vem com vários modelos predefinidos. Os modelos disponíveis dependem do site individual. Os campos principais são:

* **Título** O título exibido na página da Web resultante.

* **Nome** Usado ao nomear a página.

* **Modelo** Uma lista de modelos disponíveis para uso ao gerar a nova página.

>[!TIP]
>
>Se configurado na instância,[ os autores de modelo poderão criá-los com o Editor de modelo](/help/sites-cloud/authoring/features/templates.md).

### Componentes {#components}

Os componentes são os elementos fornecidos pelo AEM, desse modo, é possível adicionar tipos específicos de conteúdo. O AEM vem com diversos componentes prontos para uso que fornecem funcionalidade abrangente. Eles incluem:

* Texto
* Imagem
* Título
* Carrossel
* E muito mais

Depois de criar e abrir uma página, é possível[ adicionar conteúdo usando os componentes](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), que estão disponíveis [no navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>O console [Componentes](/help/sites-cloud/authoring/features/components-console.md) fornece uma visão geral dos componentes na instância.

## Gerenciamento de páginas {#managing-pages}

### Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, é necessário criar uma página antes de começar a criar o conteúdo:

1. Open the Sites console (for example, `https://<host>:<port>/sites.html/content`.
1. Navegue até o local onde deseja criar a nova página.
1. Abra o seletor suspenso usando **Criar** na barra de ferramentas e, em seguida, selecione **Página** na lista:

   ![Criação de uma página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. A partir da primeira etapa do assistente, você pode:

   * Selecionar o modelo que deseja usar para criar a nova página, em seguida, clicar/tocar em **Próximo** para prosseguir.

   * **Cancelar** para suspender o processo.
   ![Selecionar um modelo para uma nova página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. A partir da última etapa do assistente, você pode:

   * Usar as três guias para inserir as [propriedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) que deseja atribuir à nova página, em seguida, clicar/tocar em **Criar** para realmente criar a página.

   * Usar **Voltar** para voltar à seleção do modelo.
   Os campos principais são:

   * **Título**:

      * É exibido ao usuário e é obrigatório.
   * **Nome**:

      * Usado para gerar o URI. Se não for especificado, o nome é derivado do título.
      * Se você fornecer um **Nome** de página ao criar uma nova página, o AEM vai  validar o nome de acordo com as convenções impostas pelo AEM e JCR. <!--If you supply a page **Name** when creating a new page, AEM will [validate the name according to the conventions](/help/sites-developing/naming-conventions.md) imposed by AEM and JCR.-->
      * **Não é possível enviar caracteres inválidos** no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo será destacado e uma mensagem explicativa será exibida para indicar os caracteres que precisam ser removidos/substituídos.
   >[!TIP]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   A informação mínima exigida para criar uma nova página é o **Título**.

   ![Fornecimento do título da página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Use **Criar** para concluir o processo e criar a sua nova página. A caixa de diálogo de confirmação perguntará se você deseja **Abrir** a página imediatamente ou voltar para o console (**concluído**):

   ![Êxito na criação da página](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Caso crie uma página usando um nome que já existe no local, o sistema vai gerar automaticamente uma variação do nome, ao anexar um número. For example if `beach` already exists a new page will become `beach1`.

1. Caso volte ao console, você verá em sua nova página:

   ![Nova página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Once a page has been created its template cannot be changed - unless you [create a launch with a new template](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), though this will lose any existing content.

### Abrir uma página para edição {#opening-a-page-for-editing}

Depois de criar uma página ou navegar até uma página existente (no console), você pode abri-la para edição:

1. Abra o console **Sites**.
1. Navegue até que você encontre a página que deseja editar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas
   And then select the **Edit** icon:

   ![Botão Editar](/help/sites-cloud/authoring/assets/edit.png)

1. A página será aberta e aqui é possível [editar a página](/help/sites-cloud/authoring/fundamentals/editing-content.md) conforme necessário.

>[!NOTE]
>
>Navegar para outras páginas do editor de páginas só é possível no modo de visualização, pois os links não estão ativos no modo de Edição...

### Copiar e colar uma página {#copying-and-pasting-a-page}

É possível copiar uma página e todas as suas subpáginas para um novo local:

1. No console **Sites**, navegue até que você encontre a página que deseja copiar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas
   E, em seguida, o ícone **Copiar** página:

   ![Botão Copiar](/help/sites-cloud/authoring/assets/copy.png)

   >[!NOTE]
   >
   >Caso esteja no modo de seleção, este é encerrado automaticamente assim que a página for copiada.

1. Navegue até o local para a nova cópia da página.
1. Use o ícone de página **Colar:**

   ![Botão Colar](/help/sites-cloud/authoring/assets/paste.png)

   Uma cópia da página original e qualquer subpágina será criada neste local.

   >[!NOTE]
   >
   >Se você copiar a página para um local onde uma página com o mesmo nome que a original já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `beach` já existir uma nova página com o nome `beach` se tornará `beach1`.

### Mover ou renomear uma página {#moving-or-renaming-a-page}

O procedimento para mover ou renomear uma página é basicamente o mesmo e é realizado pelo mesmo assistente. Com este assistente você pode:

* Renomear uma página sem movê-la
* Mover a página sem renomeá-la
* Mover e renomear ao mesmo tempo

O AEM oferece a funcionalidade de atualizar os links internos que se referem à página que está sendo renomeada/movida. Isso pode ser feito página por página para proporcionar uma flexibilidade total.

1. Navegue até que você encontre a página que deseja mover.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e a barra de ferramentas
   E, em seguida, selecione o ícone **Mover** página:

   ![Botão Mover](/help/sites-cloud/authoring/assets/move.png)

   Isto abrirá o assistente de página para movimento.

1. Na etapa **Renomear** do assistente, é possível:

   * Especifique o nome que deseja para a página após movê-la, em seguida, clique/toque em **Próximo** para prosseguir.
   * **Cancelar** para suspender o processo.
   ![Mover e renomear página](/help/sites-cloud/authoring/assets/move-page-rename.png)

   O nome da página pode permanecer o mesmo se você estiver somente movendo a página.

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `beach` já existir uma nova página com o nome `beach` se tornará `beach1`.

1. Na etapa **Selecionar destino** do assistente, é possível:

   * Use a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) para navegar até o novo local da página:

      * Para selecionar o destino, clique em sua miniatura.
      * Clique em **Avançar** para continuar.
   * Use **Voltar** para voltar às especificações do nome de página.
   >[!NOTE]
   >
   >Por padrão, o pai da página que você está movendo/renomeando será selecionado como o destino.

   ![Selecionar destino de movimentação de página](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `winter` já existir, `winter` se tornará `winter1`.

1. Se a página estiver vinculada ou referenciada, ou tiver sido publicada, os detalhes serão listados na etapa **Ajustar/Republicar**.

   Você pode indicar o que deve ser ajustado e/ou republicado, conforme necessário.

   >[!NOTE]
   >
   >Se a página não estiver vinculada nem referenciada, essa etapa não estará disponível.

   ![Publicar novamente página ao mover](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Selecionar **Mover** concluirá o processo e moverá/renomeará sua página, conforme apropriado.

>[!NOTE]
>
>Se a página já tiver sido publicada, movê-la automaticamente removerá a publicação. By default, it will be republished when the move is complete, but this can changed by un-checking the **Republish** field in the **Adjust/Republish** step.

>[!NOTE]
>
>Caso a página não seja mencionada de alguma maneira, então a etapa **Ajustar/republicar** será ignorada.

>[!NOTE]
>
>A opção Renomear uma página também está sujeita às [Convenções de nomenclatura da página](#page-naming-conventions) ao especificar o nome da nova página.

>[!NOTE]
>
>Uma página só pode ser movida para um local onde o modelo no qual a página se baseia está permitido. Consulte Disponibilidade do modelo para obter mais informações.
<!--
>A page can only be moved to a location where the template upon which the page is based is allowed. See [Template Availability](/help/sites-developing/templates.md#template-availability) for more information.
-->

### Excluir uma página {#deleting-a-page}

1. Navegue até que você possa visualizar a página que deseja excluir.
1. Use o [modo de seleção ](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para selecionar a página pretendida, em seguida, use **Excluir** na barra de ferramentas:

   ![Botão Excluir](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Como precaução de segurança, o ícone de página **Excluir** não está disponível como uma ação rápida.

1. Uma caixa de diálogo irá pedir confirmação, use:

   * **Cancelar** para suspender a ação
   * **Excluir** para confirmar a ação:

      * Se a página não possui referências, a página será excluída.
      * Caso a página tenha referências, uma caixa de mensagem vai informá-lo de que **Uma ou mais páginas são mencionadas.** Você pode selecionar **Forçar exclusão** ou **Cancelar**.

>[!NOTE]
>
>Se uma página já estiver publicada, ela será automaticamente despublicada antes da exclusão.

### Bloquear uma página {#locking-a-page}

Você pode [bloquear/desbloquear uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) em um console ou ao editar uma página individual. Informações sobre se uma página está bloqueada são exibidas em ambos os locais.

![Botão](/help/sites-cloud/authoring/assets/lock.png)Bloquear botão![Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

### Creating a New Folder {#creating-a-new-folder}

Você pode criar pastas para ajudar a organizar seus arquivos e páginas.

1. Abra o console **Sites** e navegue até o local desejado.
1. Para abrir a lista de opções, selecione **Criar** na barra de ferramentas
1. Selecione **Pasta** para abrir a caixa de diálogo. Aqui você pode inserir o **Nome** e o **Título**:

   ![Criar pasta](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Selecione **Criar** para criar a pasta.

>[!NOTE]
>
>As pastas também estão sujeitas às [Convenções de nomenclatura da página](#page-naming-conventions) ao especificar o nome da nova pasta.

>[!CAUTION]
>
>* Pastas só podem ser criadas diretamente em **Sites** ou em outras pastas. Eles não podem ser criadas em uma página.
>* As ações padrão de mover, copiar, colar, excluir, publicar, cancelar a publicação e exibir/editar propriedades podem ser executadas em uma pasta.
>* As pastas não estão disponíveis para seleção em uma live copy.

