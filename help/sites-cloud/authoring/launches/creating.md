---
title: Criação de inicializações
description: É possível criar um lançamento para permitir a atualização de uma nova versão das páginas da Web existentes para ativação futura.
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 100%

---

# Criação de inicializações {#creating-launches}

Crie um lançamento para permitir a atualização de uma nova versão de páginas da web existentes para ativação futura. Ao criar a inicialização, especifique um título e a página de origem:

* O título é exibido no painel [Referências](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references), onde os autores podem acessá-lo para trabalhar nele.
* As páginas secundárias da página de origem são incluídas no lançamento por padrão. Você pode usar apenas a página de origem, se desejar.
* Por padrão, a [Live Copy](/help/sites-cloud/administering/msm/overview.md) atualiza automaticamente as páginas de lançamento conforme as páginas de origem são alteradas. Você pode especificar que uma cópia estática seja criada para evitar alterações automáticas.

Como opção, especifique a **Data de inicialização** (e a hora) para definir quando as páginas de inicialização devem ser promovidas e ativadas. No entanto, a **Data de inicialização** só funciona em combinação com o sinalizador **Pronto para produção** (consulte [Editar uma configuração de inicialização](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)); para que as ações realmente ocorram automaticamente, ambas devem ser definidas.

>[!NOTE]
>
>Ao criar uma inicialização, as páginas mais altas na hierarquia não são cópias das páginas de origem. São marcadores de posição, criados com o modelo:
>
>* `/libs/launches/templates/outofscope`
>
>Essas páginas não podem ser editadas. Você verá a mensagem:
>
>* **Esta página não faz parte da inicialização. Acesse a página de produção**


## Criação de um lançamento {#creating-a-launch}

É possível criar um lançamento do console Sites ou Lançamentos:

1. Abra o console **Sites** ou **Inicializações**.

   >[!NOTE]
   >
   >Ao usar o console **Sites**, é normal navegar até o local da página de origem, mas isso não é obrigatório, pois você pode navegar para selecionar **Iniciar origem** no assistente.

1. Dependendo do console que está usando:
   * **Inicializações**:
      1. Selecione **Criar lançamento** na barra de ferramentas para abrir o assistente.
   * **Sites**:
      1. Selecione **Criar** na barra de ferramentas para abrir a caixa de seleção.
      1. Aqui, selecione **Criar lançamento** para abrir o assistente.

   >[!NOTE]
   >
   >No console **Sites**, também é possível usar o [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para selecionar uma página antes de selecionar **Criar**.
   >
   >Esta ação utilizará a página selecionada como a página de origem inicial.

1. Na etapa **Selecionar origem**, é necessário **Adicionar páginas**. É possível selecionar várias páginas, especificando o caminho de cada uma delas:
   * Navegue até o local necessário.
   * Selecione as páginas de origem e confirme-as (marca de verificação).

   Repita conforme necessário.

   ![Selecionar origem da inicialização](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Para adicionar páginas e/ou ramificações a um lançamento, elas devem estar em um site (ou seja, abaixo de uma raiz de nível superior comum).
   >
   >Se o site contém raízes de idioma abaixo do nível superior, as páginas e as ramificações de um lançamento devem estar abaixo de uma raiz de idioma comum.

1. Para cada entrada, é possível especificar:

   * **Incluir subpáginas**:

      * Especifique se você deseja criar a inicialização com ou sem as páginas secundárias.  Por padrão, essas subpáginas são incluídas.

   Continue clicando em **Próximo**.

   ![Selecionar origem da inicialização](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. Na etapa **Propriedades** do assistente, é possível especificar:

   * **Título do lançamento**: o nome do lançamento. O nome deve ser significativo para os autores.
   * **com conteúdo existente**: o conteúdo original será usado para criar a inicialização.
   * **usar um novo modelo para substituir a página**: consulte [Criar inicialização com um novo modelo](#create-launch-with-new-template) para obter mais detalhes.
   * **Herdar dados online da página de origem:** selecione essa opção para atualizar automaticamente o conteúdo das páginas de inicialização quando as páginas de origem forem alteradas. Essa opção faz isso transformando a inicialização em uma [Live Copy](/help/sites-cloud/administering/msm/overview.md). Por padrão, esta opção é selecionada.-->
   * **Data da inicialização**: a data e a hora em que a cópia de inicialização deve ser ativada (dependendo do sinalizador de **Pronto para produção**; consulte [Inicializações - a ordem dos eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).

   ![Propriedades da inicialização](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Use **Criar** para concluir o processo e criar seu novo lançamento. A caixa de diálogo de confirmação irá perguntar se deseja abrir o lançamento imediatamente.

   Se retornar ao console (com a opção **Concluído**), poderá visualizar (e acessar) seu lançamento:

   * O console [**Inicializações**](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * As [**Referências** no console **Sites**](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Criar inicialização com um novo modelo {#create-launch-with-new-template}

Ao criar uma inicialização, é possível escolher se deseja usar um novo modelo:

>[!NOTE]
>
>Essa opção está disponível apenas ao criar uma inicialização no console **Sites**. Não está disponível ao criar uma inicialização no console **Inicializações**.

![Criação de uma inicialização com um novo modelo](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Selecionar isso irá:

* Atualizar as outras opções disponíveis,
* Incluir uma nova etapa, que permite selecionar o modelo obrigatório.

![Seleção de um novo modelo](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Como um modelo diferente foi usado, a nova página estará em branco. Devido a uma estrutura de página diferente, nenhum conteúdo será copiado.
>
>Este mecanismo pode ser usado para alterar o modelo de uma [página existente](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page), embora a perda de conteúdo deva ser levada em consideração.

### Criação de um lançamento aninhado {#creating-a-nested-launch}

Criar um lançamento aninhado (um lançamento dentro de outro) permite criar um lançamento a partir de um lançamento existente, de modo os autores possam aproveitar as alterações feitas, em vez de ter que fazer as mesmas alterações várias vezes para cada lançamento.

>[!NOTE]
>
>Consulte também [Promover uma inicialização aninhada](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Criação de uma inicialização aninhada - Console Inicializações {#creating-a-nested-launch-launches-console}

A criação de uma inicialização aninhada no console **Inicializações** segue basicamente o mesmo processo de criação de qualquer outra forma de inicialização, com a exceção de que você precisa acessar a ramificação de inicializações `/content/launches`:

1. No console **Inicializações**, selecione **Criar**.
1. Selecione **Adicionar páginas** e acesse a ramificação de inicializações especificando `/content/launches` no painel **Filtros**. Selecione a inicialização necessária e confirme com **Selecionar**:

   ![Criação de uma inicialização aninhada](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Continue clicando em **Próximo**.

1. Complete as **Propriedades** como em qualquer outra inicialização.

1. Conclua com **Criar**.

#### Criação de uma inicialização aninhada - Console Sites {#creating-a-nested-launch-sites-console}

Para criar uma inicialização aninhada no console **Sites**, com base em uma inicialização existente:

1. Acesse [Inicialização a partir de Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis.
1. Selecione **Criar inicialização** para abrir o assistente (como a origem já foi selecionada, ele ignorará a etapa **Selecionar origem**).
1. Insira o **Título da inicialização** e todos os outros detalhes necessários (como em uma inicialização normal).
1. Use **Criar** para concluir o processo e criar seu novo lançamento. A caixa de diálogo de confirmação irá perguntar se deseja abrir o lançamento imediatamente.

Ao selecionar **Concluído**, você retornará ao painel **Referências** do console **Sites**. Ao selecionar a página apropriada, a nova inicialização será exibida.

### Exclusão de um lançamento {#deleting-a-launch}

É possível excluir um lançamento do console [Lançamentos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Selecione o lançamento, tocando/clicando na miniatura.
* A barra de ferramentas será exibida; selecione Excluir.
* Confirme a ação.

>[!CAUTION]
>
>Excluir um lançamento removerá o próprio lançamento e qualquer lançamento descendente aninhado.
