---
title: Gerenciamento dos fragmentos de conteúdo
description: Saiba como usar o console Assets para gerenciar os Fragmentos de conteúdo AEM, a base do seu conteúdo sem periféricos.
feature: Content Fragments
role: User
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
source-git-commit: b1a1ef0021499872a712c1e4450af9765e46a1a9
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 9%

---

# Gerenciamento dos fragmentos de conteúdo {#managing-content-fragments}

Saiba como usar o console Assets para gerenciar os Fragmentos de conteúdo AEM, a base do seu conteúdo sem periféricos.

Depois de definir o [Modelos de fragmentos do conteúdo](#creating-a-content-model) você pode usá-los para [criar os Fragmentos do conteúdo](#creating-a-content-fragment).

O [Editor de fragmentos de conteúdo](#opening-the-fragment-editor) fornece vários [modos](#modes-in-the-content-fragment-editor) para permitir:

* [Edit the content](#editing-the-content-of-your-fragment) and [manage Variations](#creating-and-managing-variations-within-your-fragment)
* [Anotar em seu fragmento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associar conteúdo ao fragmento](#associating-content-with-your-fragment)
* [Configurar os metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Exibir a árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar a representação JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Fragmentos de conteúdo podem ser usados:
>
>* ao criar páginas; see [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* para [Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>Fragmentos de conteúdo são armazenados como **Ativos**, portanto, são gerenciadas principalmente na variável **Ativos** console.

## Criação de fragmentos de conteúdo {#creating-content-fragments}

### Criação de um modelo de conteúdo {#creating-a-content-model}

[Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) podem ser ativados e criados, antes da criação de fragmentos de conteúdo com conteúdo estruturado.

### Criação de um fragmento de conteúdo {#creating-a-content-fragment}

O método de criação de um fragmento de conteúdo é:

1. Navegue até a pasta **Ativos** na qual deseja criar o fragmento.
1. Selecione **Criar** e **Fragmento de conteúdo** para abrir o assistente.
1. A primeira etapa do assistente requer que você especifique a base do novo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md) - usado para criar um fragmento que requer conteúdo estruturado; por exemplo, a variável **Aventura** modelo

      * Todos os modelos disponíveis são exibidos.

   Após a seleção, use **Próximo** para continuar.

   ![base do fragmento](assets/cfm-managing-01.png)

1. Na etapa **Propriedades**, especifique:

   * **Básico**

      * **Título**

         O título do fragmento.

         Obrigatório.

      * **Descrição**

      * **Tags**
   * **Avançado**

      * **Nome**

         O nome; será usada para formar o URL.

         Obrigatório; serão derivadas automaticamente do título, mas podem ser atualizadas.


1. Selecione **Criar** para concluir a ação e, em seguida, **Abra** o fragmento para editar ou retorne ao console com **Concluído**.

   >[!NOTE]
   >Em **Lista** do console, você pode atualizar o **Exibir configurações** para ativar o **Modelo de fragmento de conteúdo** coluna.

## Actions for a Content Fragment in the Assets Console {#actions-for-a-content-fragment-assets-console}

No **Ativos** no console, uma variedade de ações está disponível para seus fragmentos de conteúdo:

* Na barra de ferramentas; após a seleção do fragmento, todas as ações apropriadas estarão disponíveis.
* As [ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); um subconjunto de ações disponível para os cartões de fragmento individuais.

![ações](assets/cfm-managing-02.png)

Selecione o fragmento para exibir a barra de ferramentas com as ações aplicáveis:

* **Processar ativos novamente**
* **Criar**
* **Download**

   * Salve o fragmento como um arquivo ZIP; você pode definir se deseja incluir Elementos, Variações, Metadados.

* **Check-out**
* **Propriedades**

   * Permite exibir e/ou editar os metadados do fragmento.

* **Editar**

   * Allows you to [open the fragment for editing content](/help/assets/content-fragments/content-fragments-variations.md) together with its elements, variations, associated content and metadata.

* **Publicação rápida**
* **Gerenciar publicação**
* **Gerenciar tags**
* **Para a coleção**
* **Copiar** e **Colar**)
* **Mover**
* **Excluir**

>[!NOTE]
>
>Muitos deles são [ações padrão do Assets](/help/assets/manage-digital-assets.md) e/ou a [AEM aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR).

## Abrir o Editor de fragmentos {#opening-the-fragment-editor}

Para abrir o fragmento para edição:

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa [as permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o administrador do sistema em caso de problemas.

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa das permissões apropriadas. Entre em contato com o administrador do sistema em caso de problemas.

1. Use the **Assets** console to navigate to the location of your content fragment.
1. Abra o fragmento para edição, por:

   * Clicar/tocar no link do fragmento ou fragmento (depende da exibição do console).
   * Selecionar o fragmento e **Editar** na barra de ferramentas.

1. O editor de fragmentos será aberto. Faça as alterações necessárias:

   ![editor de fragmento](assets/cfm-managing-03.png)

1. Depois de fazer alterações, use **Salvar**, **Salvar e fechar** ou **Fechar** conforme necessário.

   >[!NOTE]
   >
   >**Salvar e fechar** está disponível por meio do **Salvar** lista suspensa.

   >[!NOTE]
   >
   >Ambos **Salvar e fechar** e **Fechar** sairá do editor - consulte [Salvar, fechar e versões](#save-close-and-versions) para obter informações completas sobre como as várias opções operam para fragmentos de conteúdo.

## Modos e ações no Editor de fragmento de conteúdo {#modes-actions-content-fragment-editor}

Há vários modos e ações disponíveis no Editor de fragmentos de conteúdo.

### Modos no Editor de fragmento de conteúdo {#modes-in-the-content-fragment-editor}

Navegue pelos vários modos usando os ícones no painel lateral:

* Variações: [Edição de conteúdo](#editing-the-content-of-your-fragment) e [Gerenciamento de variações](#creating-and-managing-variations-within-your-fragment)

* [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Conteúdo associado](#associating-content-with-your-fragment)
* [Metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar](/help/assets/content-fragments/content-fragments-json-preview.md)

![modos](assets/cfm-managing-04.png)

### Ações da barra de ferramentas no Editor de fragmentos de conteúdo {#toolbar-actions-in-the-content-fragment-editor}

Alguns recursos na barra de ferramentas superior estão disponíveis em vários modos:

![modes](assets/cfm-managing-top-toolbar.png)

* Uma mensagem será exibida quando o fragmento já estiver referenciado em uma página de conteúdo. Você pode **Fechar** a mensagem.

* O painel lateral pode ser oculto/exibido usando o **Alternar painel lateral** ícone .

* Underneath the fragment name you can see the name of the [Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md) used for creating the current fragment:

   * The name is also a link that will open the model editor.

* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

   * **Novo**: cinza
   * **Rascunho**: azul
   * **Publicado**: verde
   * **Modified**: orange
   * **Deactivated**: red

* **Salvar** fornece acesso ao **Salvar e fechar** opção.

* Os três pontos (**...**) fornece acesso a ações adicionais:
   * **Atualizar referências de página**
      * Isso atualiza todas as referências de página.
   * **[Publicação rápida](#publishing-and-referencing-a-fragment)**
   * **[Gerenciar publicação](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Save, Close and Versions {#save-close-and-versions}

>[!NOTE]
>
>As versões também podem ser [criado, comparado e revertido a partir da Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

The editor has various options:

* **Salvar** e **Salvar e fechar**

   * **Salvar** O salvará as alterações mais recentes e permanecerá no editor.
   * **Salvar e fechar** O salvará as alterações mais recentes e sairá do editor.

   >[!CAUTION]
   >
   >Para editar um fragmento de conteúdo, você precisa [as permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o administrador do sistema em caso de problemas.

   >[!NOTE]
   >
   >É possível permanecer no editor, fazendo uma série de alterações, antes de salvar.

   >[!CAUTION]
   >
   >Além de simplesmente salvar suas alterações, as ações também atualizam quaisquer referências e garantem que o Dispatcher seja liberado conforme necessário. Essas alterações podem levar tempo para serem processadas. Devido a isso, pode haver um impacto no desempenho de um sistema grande/complexo/com carga intensa.
   >
   >Lembre-se disso ao usar **Salvar e fechar** e, em seguida, insira novamente rapidamente o editor de fragmentos para fazer e salvar mais alterações.

* **Fechar**

   Sairá do editor sem salvar as alterações mais recentes (ou seja, feitas desde a última **Salvar**).

Ao editar o fragmento de conteúdo, o AEM cria automaticamente versões para garantir que o conteúdo anterior possa ser restaurado se você cancelar as alterações (usando **Fechar** sem salvar):

1. Quando um fragmento de conteúdo é aberto para edição, o AEM verifica a existência do token baseado em cookie que indica se uma *sessão de edição* existe:

   1. If the token is found, the fragment is considered to be part of the existing editing session.
   2. Se o token for *not* disponível e o usuário inicia a edição de conteúdo, uma versão é criada e um token para essa nova sessão de edição é enviado ao cliente, onde é salvo em um cookie.

2. Enquanto há um *ative* sessão de edição, o conteúdo que está sendo editado é automaticamente salvo a cada 600 segundos (padrão).

   >[!NOTE]
   >
   >The auto save interval is configurable using the `/conf` mechanism.
   >
   >Valor padrão, consulte:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se o usuário cancelar a edição, a versão criada no início da sessão de edição será restaurada e o token será removido para encerrar a sessão de edição.
4. Se o usuário selecionar **Salvar** as edições, os elementos/variações atualizados são persistentes e o token é removido para encerrar a sessão de edição.

## Edição do conteúdo do fragmento {#editing-the-content-of-your-fragment}

Após abrir o fragmento, é possível usar a variável [Variações](/help/assets/content-fragments/content-fragments-variations.md) para criar o conteúdo.

## Criação e gerenciamento de variações dentro do fragmento {#creating-and-managing-variations-within-your-fragment}

Depois de criar o conteúdo Principal, você pode criar e gerenciar, [Variações](/help/assets/content-fragments/content-fragments-variations.md) desse conteúdo.

## Associar conteúdo ao fragmento {#associating-content-with-your-fragment}

Você também pode [conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) com um fragmento. Isso fornece uma conexão para que os ativos (ou seja, imagens) possam ser usados (opcionalmente) com o fragmento quando ele é adicionado a uma página de conteúdo.

## Visualização e edição dos metadados (propriedades) do fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

É possível exibir e editar as propriedades de um fragmento usando a variável [Metadados](/help/assets/content-fragments/content-fragments-metadata.md) guia .

## Linha do tempo dos fragmentos de conteúdo {#timeline-for-content-fragments}

Além das opções padrão, [Linha do tempo](/help/assets/manage-digital-assets.md#timeline) fornece informações e ações específicas para fragmentos de conteúdo:

* Exibir informações sobre versões, comentários e anotações
* Actions for Versions

   * **[Reverter para esta versão](#reverting-to-a-version)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **[Comparar com Atual](#comparing-fragment-versions)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * Adicione um **Rótulo** e/ou **Comentário** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **Salvar como versão** (selecione um fragmento existente, em seguida, a seta para cima na parte inferior da Linha do tempo)

* Ações para anotações

   * **Excluir**

>[!NOTE]
Os comentários são:
* Funcionalidade padrão para todos os ativos
* Feito na Linha do Tempo
* Relacionado ao ativo de fragmento
>
As anotações (para Fragmentos de conteúdo) são:
* Inserido no editor de fragmentos
* Específico de um segmento selecionado de texto no fragmento
>


Por exemplo:

![linha do tempo](assets/cfm-managing-05.png)

## Comparing Fragment Versions {#comparing-fragment-versions}

The **Compare to Current** action is available from the [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) after you have selected a specific version.

Isso abrirá:

* o **Atual** (mais recente) versão (à esquerda)

* a versão selecionada **v&lt;*x.y*>** (à direita)

Elas serão mostradas lado a lado, onde:

* Quaisquer diferenças são destacadas

   * Texto excluído - vermelho
   * Inserted text - green
   * Replaced text - blue

* O ícone de tela cheia permite abrir uma versão por conta própria; em seguida, voltar para a exibição paralela
* Você pode **Reverter** da versão específica
* **Done** will return you to the console

>[!NOTE]
You cannot edit the fragment content when comparing fragments.

![comparing](assets/cfm-managing-06.png)

## Reverting to a Version  {#reverting-to-a-version}

You can revert to a specific version of your fragment:

* Directly from the [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Selecione a versão necessária, em seguida, a **Reverter para esta versão** ação.

* While [comparing a version to the current version](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) you can **Revert** to the selected version.

## Publicação e referência a um fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Se o fragmento for baseado em um modelo, você deve garantir que a variável [o modelo foi publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

Os Fragmentos de conteúdo devem ser publicados para uso no ambiente de publicação. Isso é feito usando a funcionalidade padrão Ativos :

* [Publicação rápida   ](/help/assets/manage-publication.md#quick-publish)
* [Gerenciar publicação](/help/assets/manage-publication.md#manage-publication)

Isso pode ser acessado:

* Após a criação; usar [ações disponíveis no console Ativos](#actions-for-a-content-fragment-assets-console).
* No [Editor de fragmentos de conteúdo](#toolbar-actions-in-the-content-fragment-editor).

Além disso, ao [publicar uma página que use o fragmento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); o fragmento será listado nas referências da página.

>[!CAUTION]
Depois que um fragmento tiver sido publicado e/ou referenciado, AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Excluir um fragmento {#deleting-a-fragment}

Para excluir um fragmento:

1. No **Ativos** console navegue até o local do fragmento de conteúdo.
2. Selecione o fragmento.

   >[!NOTE]
   O **Excluir** não está disponível como uma ação rápida.

3. Selecionar **Excluir** na barra de ferramentas.
4. Confirme o **Excluir** ação.

   >[!CAUTION]
   Se o fragmento já estiver referenciado em uma página, você verá uma mensagem de aviso e será solicitado a confirmar se deseja continuar com uma **Exclusão forçada**. O fragmento, junto com seu componente do fragmento de conteúdo, será excluído de qualquer página de conteúdo.
