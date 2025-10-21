---
title: Gerenciamento de fragmentos de conteúdo (Assets - Fragmentos de conteúdo)
description: Saiba como usar o console Assets para gerenciar os fragmentos de conteúdo do AEM, como base para o conteúdo headless ou para a criação de páginas.
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
feature: Content Fragments
role: User, Admin
solution: Experience Manager Sites
source-git-commit: 8a3ee333a0bd5904c43c424967a7b9c752fd38c2
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 63%

---

# Gerenciamento dos Fragmentos de conteúdo {#managing-content-fragments}

Saiba como usar o console Assets para gerenciar os fragmentos de conteúdo do AEM, como base para o conteúdo headless ou para a criação de páginas.

Depois de definir os [Modelos de fragmentos de conteúdo](#creating-a-content-model), você pode usá-los para [criar fragmentos de conteúdo](#creating-a-content-fragment).

O [Editor de fragmentos de conteúdo](#opening-the-fragment-editor) fornece vários [modos](#modes-in-the-content-fragment-editor) para permitir:

* [Editar o conteúdo](#editing-the-content-of-your-fragment) e [gerenciar as variações](#creating-and-managing-variations-within-your-fragment)
* [Anotar em seu fragmento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associar conteúdo ao fragmento](#associating-content-with-your-fragment)
* [Configurar os metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visualizar a árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar a representação JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Os fragmentos de conteúdo podem ser usados:
>
>* ao criar páginas; consulte [Criação de páginas com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* para [entrega de conteúdo headless usando fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>Os fragmentos de conteúdo são um recurso do **Sites**, mas são armazenados como **Assets**.
>
>Eles são gerenciados principalmente com o console **[Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, embora ainda possam ser gerenciados no console **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>Existem dois editores para a criação de fragmentos de conteúdo: o novo editor e o editor original. O novo editor é o padrão. Embora a funcionalidade básica seja a mesma, há algumas diferenças.
>
>Esta seção aborda o editor original.
>
>O editor padrão de [Fragmentos de conteúdo - Criação](/help/sites-cloud/administering/content-fragments/authoring.md) é o novo editor, acessado do console **Fragmentos de conteúdo** e do console **Assets**. Consulte a documentação do Sites, [Fragmentos de conteúdo - Criação](/help/sites-cloud/administering/content-fragments/authoring.md), para obter detalhes sobre o novo editor.
>
>Para usar o [editor original](/help/assets/content-fragments/content-fragments-variations.md), abra o novo editor e desative a opção **Novo Editor**.
>
>Ambos os editores têm um botão de alternância na barra de ferramentas superior para fornecer acesso rápido ao outro editor.

## Criação de fragmentos de conteúdo {#creating-content-fragments}

### Criação de um modelo de conteúdo {#creating-a-content-model}

Os [modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) podem ser habilitados e criados antes da criação de fragmentos de conteúdo com conteúdo estruturado.

### Criação de um fragmento de conteúdo {#creating-a-content-fragment}

O método para criar um fragmento de conteúdo é:

1. Navegue até a pasta **Ativos** na qual deseja criar o fragmento.
1. Selecione **Criar** e **Fragmento de conteúdo** para abrir o assistente.
1. A primeira etapa do assistente requer que você especifique a base do novo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md) - usado para criar um fragmento que requer conteúdo estruturado; por exemplo, o modelo **Aventura**

      * Todos os modelos disponíveis são exibidos.

   Após a seleção, use **Avançar** para continuar.

   ![Selecionar modelo de fragmento de conteúdo](assets/cfm-managing-01.png)

1. Na etapa **Propriedades**, especifique:

   * **Básico**

      * **Título**

        O título do fragmento.

        Obrigatório.

      * **Descrição**

      * **Tags**

   * **Avançado**

      * **Nome**

        O name; é usado para formar o URL.

        Obrigatório; é derivado automaticamente do título, mas pode ser atualizado.

1. Selecione **Criar** para concluir a ação e, em seguida, **Abra** o fragmento para editar ou retorne ao console com **Concluído**.

   >[!NOTE]
   >No modo **Lista** do console, você pode atualizar as **Configurações de Exibição** para habilitar a coluna **Modelo de Fragmento de Conteúdo**.

## Ações para um fragmento de conteúdo no console do Assets {#actions-for-a-content-fragment-assets-console}

No console do **Assets**, várias ações estão disponíveis para seus fragmentos de conteúdo:

* Na barra de ferramentas; após a seleção do fragmento, todas as ações apropriadas ficam disponíveis.
* Como [ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions); um subconjunto de ações disponíveis para os cartões de fragmento individuais.

![Ações na barra de ferramentas](assets/cfm-managing-02.png)

Selecione o fragmento para revelar a barra de ferramentas com ações aplicáveis:

* **Reprocessar Assets**
* **Criar**
* **Download**

   * Salve o fragmento como um arquivo ZIP; é possível definir se deseja incluir Elementos, Variações, Metadados.

* **Check-out**
* **Propriedades**

   * Permite visualizar ou editar os metadados do fragmento, ou ambos.

* **Editar**

   * Permite [abrir o fragmento para edição de conteúdo](/help/assets/content-fragments/content-fragments-variations.md) junto com seus elementos, variações, conteúdo associado e metadados.

* **Publicação rápida**
* **Gerenciar publicação**
* **Gerenciar Marcas**
* **Para a coleção**
* **Copiar** (e **Colar**)
* **Mover**
* **Excluir**

>[!NOTE]
>
>Muitas delas são [ações padrão para o Assets](/help/assets/manage-digital-assets.md) e/ou o [aplicativo de desktop da AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/get-started.html?lang=pt-BR).

## Abrir o editor de fragmentos {#opening-the-fragment-editor}

Para abrir o fragmento para edição no editor original:

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o(a) administrador(a) do sistema em caso de problemas.

1. Navegue até o local do fragmento de conteúdo.

1. Abra o fragmento para edição.

1. O fragmento é aberto no novo editor. Desative a opção **Novo Editor** (canto superior direito) para abrir o editor original:

   ![Editor de fragmento](assets/cfm-managing-03.png)

1. Faça as alterações necessárias.

1. Quando estiver pronto, use **Salvar**, **Salvar e fechar** ou **Fechar**, conforme necessário.

   >[!NOTE]
   >
   >**Salvar e fechar** está disponível por meio da lista suspensa **Salvar**.

   >[!NOTE]
   >
   >Tanto a opção **Salvar e fechar** quanto **Fechar** fecharão o editor — consulte [Salvar, fechar e versões](#save-close-and-versions) para obter informações completas sobre como as várias opções operam para os fragmentos de conteúdo.

## Modos e ações no Editor de fragmento de conteúdo {#modes-actions-content-fragment-editor}

Há vários modos e ações disponíveis no Editor de fragmento de conteúdo.

### Modos no Editor de fragmento de conteúdo {#modes-in-the-content-fragment-editor}

Navegue pelos vários modos usando os ícones no painel lateral:

* Variações: [Edição de conteúdo](#editing-the-content-of-your-fragment) e [Gerenciamento de variações](#creating-and-managing-variations-within-your-fragment)

* [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Conteúdo associado](#associating-content-with-your-fragment)
* [Metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar](/help/assets/content-fragments/content-fragments-json-preview.md)

![Modos no editor de fragmento de conteúdo](assets/cfm-managing-04.png)

### Ações da barra de ferramentas no Editor de fragmento de conteúdo {#toolbar-actions-in-the-content-fragment-editor}

Alguns recursos na barra de ferramentas superior estão disponíveis em vários modos:

![Ações da barra de ferramentas disponíveis em vários modos](assets/cfm-managing-top-toolbar.png)

* Uma mensagem será exibida quando o fragmento já tiver sido referenciado em uma página de conteúdo. Você pode **Fechar** a mensagem.

* O painel lateral pode ser oculto/exibido usando o ícone **Ativar painel lateral**.

* Abaixo do nome do fragmento, você pode ver o nome do [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) usado para criar o fragmento atual:

   * O nome também é um link que abre o editor de modelo.

* Veja o status do fragmento; por exemplo, informações sobre quando ele foi criado, modificado ou publicado. O status também é codificado por cores:

   * **Novo**: cinza
   * **Rascunho**: azul
   * **Publicado**: verde
   * **Modificado**: laranja
   * **Desativado**: vermelho

* Um botão permite que você **Experimente o Novo Editor**, abrindo diretamente o *novo* [Editor de Fragmentos de Conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md), que pode ser acessado por meio do [console de Fragmentos de Conteúdo](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

  >[!WARNING]
  >
  >O novo editor é aberto na mesma guia. Não é recomendável ter ambos os editores abertos ao mesmo tempo.

* **Salvar** fornece acesso à opção **Salvar e fechar**.

* O menu suspenso de três pontos (**...**) fornece acesso a ações adicionais:
   * **Atualizar referências de página**
      * Isso atualiza todas as referências de página.
   * **[Publicação rápida](#publishing-and-referencing-a-fragment)**
   * **[Gerenciar publicação](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Salvar, fechar e versões {#save-close-and-versions}

>[!NOTE]
>
>As versões também podem ser [criadas, comparadas e revertidas a partir da linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

O editor tem várias opções:

* **Salvar** e **Salvar e fechar**

   * **Salvar** salva as alterações mais recentes e permanece no editor.
   * **Salvar e fechar** salva as alterações mais recentes e fecha o editor.

  >[!CAUTION]
  >
  >Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o(a) administrador(a) do sistema em caso de problemas.

  >[!NOTE]
  >
  >É possível permanecer no editor e fazer uma série de alterações antes de salvar.

  >[!CAUTION]
  >
  >Além de simplesmente salvar suas alterações, as ações também atualizam quaisquer referências e garantem que o Dispatcher seja liberado conforme necessário. Essas alterações podem levar tempo para serem processadas. Devido a esse tempo, pode haver um impacto no desempenho de um sistema grande/complexo/com bastante conteúdo.
  >
  >Lembre-se desse processo ao usar **Salvar e fechar** e, em seguida, entrar novamente rapidamente no editor de fragmentos para fazer mais alterações e salvá-las.

* **Fechar**

  Fechará o editor sem salvar as alterações mais recentes (ou seja, feitas desde o último **Salvamento**).

Ao editar o fragmento de conteúdo, o AEM cria versões automaticamente para garantir que o conteúdo anterior possa ser restaurado se você cancelar as alterações (usando **Fechar** sem salvar):

1. Quando um fragmento de conteúdo é aberto para edição, o AEM verifica a existência do token baseado em cookie que indica se uma *sessão de edição* existe:

   1. Se o token for encontrado, o fragmento será considerado parte da sessão de edição existente.
   2. Se o token *não* estiver disponível e o usuário iniciar a edição do conteúdo, uma versão será criada e um token para essa nova sessão de edição será enviado ao cliente e salvo em um cookie.

2. Enquanto houver uma seção de edição *ativa*, o conteúdo que está sendo editado será salvo automaticamente a cada 600 segundos (padrão).

   >[!NOTE]
   >
   >O intervalo de salvamento automático pode ser configurado usando o mecanismo `/conf`.
   >
   >Valor padrão, consulte:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se o usuário cancelar a edição, a versão criada no início da sessão de edição será restaurada e o token será removido para encerrar a sessão de edição.
4. Se o usuário escolher **Salvar** as edições, os elementos/variações atualizados serão mantidos e o token será removido para encerrar a sessão de edição.

## Edição do conteúdo do fragmento {#editing-the-content-of-your-fragment}

Após abrir o fragmento, é possível usar a guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) para criar o conteúdo.

## Criação e gerenciamento de variações dentro do fragmento {#creating-and-managing-variations-within-your-fragment}

Depois de criar o conteúdo Principal, é possível criar e gerenciar [Variações](/help/assets/content-fragments/content-fragments-variations.md) desse conteúdo.

## Associar conteúdo ao fragmento {#associating-content-with-your-fragment}

Você também pode [associar conteúdo](/help/assets/content-fragments/content-fragments-assoc-content.md) a um fragmento. Isso fornece uma conexão para que os ativos (ou seja, imagens) possam ser usados (opcionalmente) com o fragmento quando ele é adicionado a uma página de conteúdo.

## Visualização e edição dos metadados (propriedades) do fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

É possível visualizar e editar as propriedades de um fragmento usando a guia [Metadados](/help/assets/content-fragments/content-fragments-metadata.md).

## Linha de tempo dos fragmentos de conteúdo {#timeline-for-content-fragments}

Além das opções padrão, a [Linha de tempo](/help/assets/manage-digital-assets.md#timeline) fornece informações e ações específicas para fragmentos de conteúdo:

* Visualizar informações sobre versões, comentários e anotações
* Ações para versões

   * **[Reverter para esta versão](#reverting-to-a-version)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **[Comparar com atual](#comparing-fragment-versions)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * Adicionar um **Rótulo** e/ou **Comentário** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **Salvar como versão** (selecione um fragmento existente e, em seguida, a seta para cima na parte inferior da Linha de tempo)

* Ações para anotações

   * **Excluir**

>[!NOTE]
>
>Os comentários são:
>
>* Uma funcionalidade padrão para todos os ativos
>* Feitos na Linha de tempo
>* Relacionados ao ativo de fragmento
>
>As anotações (para fragmentos de conteúdo) são:
>
>* Inseridas no editor de fragmentos
>* Específicas de um segmento de texto selecionado no fragmento
>
>Nem mostra os comentários inseridos no novo [editor de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment).

Por exemplo:

![Linha do tempo](assets/cfm-managing-05.png)

## Comparação de versões do fragmento {#comparing-fragment-versions}

A ação **Comparar com atual** fica disponível na [Linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) após selecionar uma versão específica.

Isso abre:

* a versão (à esquerda) **Atual** (mais recente)

* a versão selecionada **v&lt;*x.y*>** (à direita)

Eles são mostrados lado a lado, onde:

* Quaisquer diferenças serão destacadas

   * Texto excluído — vermelho
   * Texto inserido — verde
   * Texto substituído — azul

* O ícone de tela cheia permite abrir uma versão por conta própria e, em seguida, voltar para a visualização paralela
* É possível **Reverter** para a versão específica
* **Concluído** retornará ao console

>[!NOTE]
>
>Não é possível editar o conteúdo do fragmento ao comparar fragmentos.

![Comparando variações](assets/cfm-managing-06.png)

## Reverter para uma versão  {#reverting-to-a-version}

Você pode reverter para uma versão específica do fragmento:

* Diretamente da [Linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  Selecione a versão necessária e, em seguida, a ação **Reverter para esta versão**.

* Ao [comparar uma versão com a versão atual](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions), é possível **Reverter** para a versão selecionada.

## Publicar e referenciar um fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Se o fragmento for baseado em um modelo, é preciso certificar-se de que o [modelo foi publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Se você publicar um fragmento de conteúdo cujo modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado junto com o fragmento.

Os fragmentos de conteúdo devem ser publicados para uso no ambiente de publicação. Isso é feito usando a funcionalidade padrão do Assets:

* [Publicação rápida](/help/assets/manage-publication.md#quick-publish)
* [Gerenciar publicação](/help/assets/manage-publication.md#manage-publication)

Isso pode ser acessado:

* Após a criação; usando [ações disponíveis no console Assets](#actions-for-a-content-fragment-assets-console).
* No [Editor de Fragmento de Conteúdo](#toolbar-actions-in-the-content-fragment-editor).

Além disso, ao [publicar uma página que use o fragmento](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing); o fragmento é listado nas referências da página.

>[!CAUTION]
>
>Depois que um fragmento tiver sido publicado e/ou referenciado, o AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Excluir um fragmento {#deleting-a-fragment}

Para excluir um fragmento:

1. No console de **Ativos**, navegue até o local do fragmento de conteúdo.
2. Selecione o fragmento.

   >[!NOTE]
   >
   >A opção **Excluir** não está disponível como uma ação rápida.

3. Selecione **Excluir** na barra de ferramentas.
4. Confirme a ação **Excluir**.

   >[!CAUTION]
   >
   >Se o fragmento já estiver referenciado em uma página, você verá uma mensagem de aviso e será solicitado a confirmar se deseja continuar com uma **Exclusão forçada**. O fragmento, junto com seu componente de fragmento de conteúdo, é excluído de qualquer página de conteúdo.
