---
title: Administração de tags
description: Saiba como administrar tags no AEM para organizar seu conteúdo.
source-git-commit: af60a2b8f1e2dd7fc55247ecb0251d7b85f63eb3
workflow-type: tm+mt
source-wordcount: '2272'
ht-degree: 1%

---


# Administração de tags {#administering-tags}

As tags são um método intuitivo de classificar o conteúdo. Elas podem ser consideradas palavras-chave ou rótulos (metadados) que permitem que o conteúdo seja encontrado mais rapidamente.

No Adobe Experience Manager (AEM), uma tag pode ser uma propriedade de:

* Um nó de conteúdo para uma página
   * Consulte o documento [Uso de tags](/help/sites-cloud/authoring/features/tags.md) para obter mais informações.
* Um nó de metadados de um ativo
   * Consulte o documento [Gerenciamento de metadados para ativos digitais](/help/assets/manage-metadata.md) para obter mais informações.

>[!TIP]
>
>É uma prática recomendada minimizar o número de tags relacionadas às mesmas ideias. Por exemplo, se você estiver gerenciando conteúdo para uma loja de suprimentos externa, provavelmente não precisará de uma tag para ambos **calçado** e **sapatos**.

## Recursos de tag {#tag-features}

As tags oferecem recursos robustos para organização e gerenciamento de conteúdo.

* As tags podem ser agrupadas em vários namespaces.
   * Os namespaces podem ser considerados hierarquias que permitem a criação de taxonomias.
   * Essas taxonomias são globais por todo o AEM.
* As tags podem ser aplicadas por autores e usadas por visitantes do site.
* Independentemente do criador, todas as formas de tags são disponibilizadas para seleção, tanto ao atribuir a uma página quanto ao pesquisar.
* As tags são usadas pelo [Componente de Lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) para gerar listas dinâmicas com base nas tags selecionadas.

## Requisitos da tag {#requirements}

Existem alguns detalhes técnicos que devem ser considerados ao criar e gerenciar tags.

* As tags devem ser exclusivas em um namespace específico.
* O nome de uma tag não pode incluir delimitadores de tag:
   * Dois pontos (`:`) - Delimita a tag do namespace
   * Barra (`/`) - Delimita subtags
* Se o título de uma tag incluir delimitadores de tag, eles serão suprimidos na interface do.
* As tags podem ser criadas e sua taxonomia pode ser modificada por membros da `tag-administrators` grupo e membros que têm direitos de modificação `/content/cq:tags`.
   * Uma tag que contém tags secundárias é chamada de tag container.
   * Uma tag que não é uma tag container é chamada de tag folha.
   * Um namespace de tag pode ser uma tag folha ou container.

Para obter mais detalhes técnicos sobre como as tags funcionam, consulte o documento [Estrutura de marcação AEM.](/help/implementing/developing/introduction/tagging-framework.md)

## Console de marcação {#tagging-console}

O console de marcação é usado para criar e gerenciar tags e suas taxonomias. Você pode usar o console de marcação para gerenciar as tags ao:

* Agrupá-los em namespaces.
* Analisar o uso de tags existentes antes de criar novas.
* Reorganização das tags sem desconectar a tag do conteúdo referenciado no momento.

Para acessar o console de marcação:

1. Faça logon em um ambiente de criação com privilégios administrativos.
1. No menu de navegação global, selecione **`Tools`** -> **`General`** ->
   **`Tagging`**.

![O console de marcação no AEM](/help/sites-cloud/administering/assets/tagging-console.png)

## Criação de novas tags {#creating-new-tags}

Há várias etapas para criar e usar tags para organizar seu conteúdo.

1. [Criar um namespace para suas tags](#creating-namespaces) (ou escolha uma existente para reutilizar).
1. [Crie uma nova tag.](#creating-tags)
1. [Publique a tag.](#publishing-tags)

### Criação de namespaces {#creating-namespaces}

Um namespace é usado para organizar outras tags. Ela pode ser considerada a tag de nível mais baixo e geralmente é usada para agrupar outras tags.

1. Para criar um novo namespace, abra a variável [console de marcação](#tagging-console) e toque ou clique no botão **Criar** na barra de ferramentas e, em seguida, **Criar namespace**.

   ![Caixa de diálogo Adicionar namespace](/help/sites-cloud/administering/assets/add-namespace.png)

1. Forneça as informações necessárias.

   * **Título** - Um título para o namespace exibido ao usuário na interface do usuário (opcional)
   * **Nome** - Se um nome não for especificado, um nome de nó válido será criado a partir da variável **Título**. Consulte o documento [Estrutura de marcação AEM](/help/implementing/developing/introduction/tagging-framework.md#tagid) para obter mais informações.
   * **Descrição** - Uma descrição do namespace (opcional)

1. Depois que as informações necessárias forem inseridas, toque ou clique **Criar**.

O namespace é criado. Observe que no console de marcação os namespaces estão no nível mais baixo (na extremidade esquerda do console) e são representados por ícones de pasta, refletindo sua natureza como um &quot;contêiner&quot; ou agrupamento de outras tags.

Agora você pode [criar novas tags](#creating-tags) neste namespace ou [gerenciar tags existentes.](#managing-tags)

Um namespace não precisa conter subtags. Como o namespace é, em si, uma tag, ele pode ser usado para organizar o conteúdo como qualquer outra tag. No entanto, para continuar criando uma taxonomia de marcação estruturada, é possível [criar subtags](#creating-tags) nesse namespace com base nos requisitos do projeto.

### Criação de tags {#creating-tags}

As tags geralmente são adicionadas a namespaces.

1. Para criar uma nova tag, abra o [console de marcação.](#tagging-console)

1. Selecione o namespace em que deseja criar a tag. Ou selecione outra tag para criar uma subtag abaixo dela.

1. Toque ou clique no **Criar** na barra de ferramentas e, em seguida, **Criar tag**.

1. A variável **Criar tag** será aberta. Forneça as informações necessárias para a nova tag.

   * **Título** - Um título de exibição para a tag (obrigatório)
   * **Nome** - Um nome para a tag (obrigatório). Se não for especificado, um nome de nó válido será criado a partir da variável **Título**. Consulte [TagID](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **Descrição** - Uma descrição da tag
   * **Caminho da tag** - O padrão é o namespace (ou tag) selecionado no console de marcação. Isso pode ser atualizado manualmente tocando ou clicando no ícone do seletor de caminho.

   ![Caixa de diálogo Criar tag](assets/create-tag.png)

1. Toque ou clique **Enviar**.

A tag é criada e o console é atualizado para mostrar a nova tag.

As tags permitem a criação flexível de sua própria taxonomia com base nas necessidades organizacionais.

* Você pode criar tags secundárias de tags existentes selecionando a tag principal no console antes de criar a nova tag.
* Se você criar uma tag sem selecionar um namespace ou outra tag, você efetivamente cria um novo namespace.

### Publicação de tags {#publishing-tags}

Assim como ocorre com a criação de qualquer outro conteúdo no AEM, uma vez criada uma tag (ou namespace), ela só existe no ambiente de criação. Para que suas tags estejam disponíveis para os usuários, você deve publicá-las.

1. Para publicar uma tag, abra o [console de marcação.](#tagging-console)

1. Selecione a tag ou tags que deseja publicar e, na barra de ferramentas, selecione **Publish**.

   ![Seleção de tags no console](assets/select-tags.png)

1. A variável **Publicar tag** A caixa de diálogo solicita uma confirmação para publicar as tags selecionadas. Toque ou clique em **Publicar**.

   ![O modal de confirmação Publicar tag](assets/publish-tag.png)

1. A ação de publicação é confirmada com uma **Sucesso** diálogo.

   ![Caixa de diálogo de sucesso da tag de publicação](assets/publish-tag-success.png)

As tags selecionadas são colocadas em fila para publicação. Semelhante ao conteúdo da página, somente as tags selecionadas são publicadas, independentemente de terem ou não subtags.

Para publicar uma taxonomia inteira (um namespace e subtags), a prática recomendada é criar uma [pacote](/help/implementing/developing/tools/package-manager.md) do namespace (consulte [Nó raiz da taxonomia](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node)).

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## Gerenciamento de tags {#managing-tags}

É possível realizar várias ações em tags e namespaces existentes para gerenciá-los e organizá-los. Basta selecionar uma tag ou namespace na variável [console de marcação](#tagging-console) para revelar as ações disponíveis na barra de ferramentas.

* [Propriedades da exibição](#viewing-tag-properties)
* [Editar](#editing-tags)
* [Desfazer publicação](#unpublishing-tags)
* [Referências](#viewing-tag-references)
* [Mover](#moving-tags)
* [Mesclar](#merging-tags)
* [Excluir](#deleting-tags)

Observe que quando não há espaço suficiente disponível na barra de ferramentas, opções adicionais ficam disponíveis atrás do ícone de reticências.

### Exibição das propriedades da tag {#viewing-tag-properties}

Quando uma única tag, um namespace ou outra tag é selecionada no console de marcação, os detalhes básicos da tag selecionada, como a hora da última edição e a última publicação, são mostrados na coluna à esquerda da coluna de tag.

![Coluna de detalhes da tag](assets/tag-details-column.png)

Você pode ver mais detalhes sobre a tag, incluindo quem a publicou pela última vez e quando, alternando o console para a tag **Propriedades** exibição.

1. Para exibir as propriedades de uma tag, abra o [console de marcação.](#tagging-console)

1. Selecione a tag cujas propriedades você deseja exibir e, no painel esquerdo, selecione **Propriedades**.

   ![Selecionar visualização de propriedades](assets/view-tag-properties.png)

1. As propriedades detalhadas da tag selecionada são exibidas no painel esquerdo.

   ![Exibição das propriedades da tag](assets/tag-properties.png)

Para obter mais detalhes sobre a seleção dos modos de exibição e do painel, consulte o documento [Manuseio básico.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### Edição de tags {#editing-tags}

Tags e namespaces podem ser editados após a criação.

1. Para editar uma tag, abra o [console de marcação.](#tagging-console)

1. Selecione a tag que deseja editar e, na barra de ferramentas, selecione **Editar**.

1. Faça as alterações desejadas. É possível alterar o:

   * **Título**
   * **Descrição**
   * [**Localização**](#managing-tags-in-different-languages)

1. Depois de fazer as edições, toque ou clique **Enviar**.

Para obter detalhes sobre como adicionar traduções de idioma, consulte a seção sobre [Gerenciamento de tags em diferentes idiomas](#managing-tags-in-different-languages).

Se as alterações feitas foram para uma tag já publicada, talvez você queira [publicá-la novamente.](#publishing-tags)

### Desfazer publicação de tags {#unpublishing-tags}

Para desativar a tag na instância do autor e removê-la da instância de publicação, você pode desfazer a publicação.

1. Para desfazer a publicação de uma tag, abra [console de marcação.](#tagging-console)

1. Selecione a tag ou tags que deseja cancelar a publicação e, na barra de ferramentas, selecione **Cancelar publicação**.

   ![Seleção de tags no console](assets/select-tags.png)

1. A variável **Cancelar publicação da tag** A caixa de diálogo solicita uma confirmação para publicar as tags selecionadas. Toque ou clique em **Publicar**.

   ![O modal de confirmação Publicar tag](assets/unpublish-tag.png)

1. A ação de cancelamento da publicação é confirmada com uma **Sucesso** diálogo.

   ![Caixa de diálogo de sucesso da tag de publicação](assets/unpublish-tag-success.png)

As tags selecionadas são colocadas em fila para cancelamento da publicação. Se a tag selecionada for uma tag container, todas as tags secundárias serão desativadas no ambiente de criação e removidas do ambiente de publicação.

### Exibindo referências de tag {#viewing-tag-references}

Pode ser útil ver a qual conteúdo uma tag específica é aplicada. Você pode fazer isso usando o **Referências** exibir no console de marcação.

1. Para exibir as referências de uma tag, abra o [console de marcação.](#tagging-console)

1. Selecione a tag cujas referências você deseja exibir e, no painel esquerdo, selecione **Referências**.

   ![Selecionar visualização de propriedades](assets/view-tag-references.png)

1. O número total de referências para a tag selecionada é exibido no painel esquerdo.

   ![Exibição de referências de tag](assets/tag-references.png)

1. Toque ou clique no número de referências de tag para exibir a lista detalhada do conteúdo atribuído à tag.

   ![Exibição detalhada das referências da tag](assets/tag-references-detail.png)

Passe o mouse ou toque em um conteúdo de referência na lista para revelar o caminho completo do conteúdo.

Para obter mais detalhes sobre a seleção dos modos de exibição e do painel, consulte o documento [Manuseio básico.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### Mover tags {#moving-tags}

Pode ser necessário limpar ou reorganizar sua taxonomia de tags movendo uma tag para um novo local ou renomeando-a.

>[!TIP]
>
>É prática recomendada que somente os administradores tenham permissão para mover e renomear tags.

1. Para mover ou renomear uma tag, abra [console de marcação.](#tagging-console)

1. Selecione a tag que deseja mover ou renomear e toque ou clique **Mover** na barra de ferramentas.

1. No **Mover tag** especifique qual propriedade você deseja alterar.

   * **Renomear para** - O novo nome que você deseja dar à tag
      * Este campo é pré-preenchido com o nome atual da tag.
      * Deixe inalterado se desejar mover apenas a tag e não renomeá-la.
   * **Mover para** - Para onde deseja mover a tag
      * Este campo é pré-preenchido com o local atual da tag.
      * Deixe inalterado se desejar apenas renomear a tag e não movê-la.

   ![Mover tag](assets/move-tag.png)

1. Toque ou clique **Enviar**.

A tag é renomeada e/ou movida para seu novo local. Quando a tag selecionada for uma tag container, movê-la também moverá todas as tags secundárias.

### Mesclar tags {#merging-tags}

Se sua taxonomia de tags tiver duplicatas ou tags semelhantes, pode ser útil mesclar essas tags. Quando a tag `A` é mesclado à tag `B`, todas as páginas marcadas com tag `A` tornar-se marcado com tag `B` e tag `A` O não está mais disponível para autores.

1. Para mesclar duas tags, abra o [console de marcação.](#tagging-console)

1. Selecione a tag que deseja mesclar com outra tag e toque ou clique **Mesclar** na barra de ferramentas.

1. No **Mesclar tag** toque ou clique no botão **Procurar** ícone do **Mesclar para** para especificar em qual tag você deseja mesclar a tag selecionada.

   ![Caixa de diálogo Mesclar tag](assets/merge-tag.png)

1. Toque ou clique **Enviar**.

A tag selecionada no console é mesclada à tag especificada na caixa de diálogo. Quando uma tag referenciada é movida ou mesclada, a tag não é fisicamente excluída, de modo que é possível manter referências. Consulte o documento [Estrutura de marcação AEM](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags) para obter mais informações.

### Exclusão de tags {#deleting-tags}

Se a taxonomia de marcação for alterada e uma tag ou um namespace for desnecessário, ele poderá ser excluído.

1. Para excluir uma tag, abra o [console de marcação.](#tagging-console)

1. Selecione a tag que deseja excluir e toque ou clique **Excluir** na barra de ferramentas.

1. A variável **Excluir tag** A caixa de diálogo solicita uma confirmação para excluir as tags selecionadas. Toque ou clique **Excluir**.

   ![O modal de confirmação Excluir tag](assets/delete-tag.png)

1. O AEM verifica se a tag não está sendo referenciada.

   1. Se nenhuma referência for encontrada, o AEM solicitará a confirmação final para excluir. Toque ou clique **Excluir**

      ![Nenhuma referência encontrada](assets/no-references-found.png)

   1. Se as referências forem encontradas, o AEM as apresentará e solicitará a confirmação final para excluí-las.

      ![Referências encontradas](assets/references-found.png)

As tags selecionadas são excluídas e removidas permanentemente do ambiente de criação. Se a tag tiver sido publicada, ela também será removida do ambiente de publicação. Se a tag selecionada for uma tag container, todas as tags secundárias também serão removidas.

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![chlimage_1-204](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

A variável `title` A propriedade de uma tag pode ser traduzida em vários idiomas. Depois de traduzido, o título da tag apropriado pode ser exibido de acordo com o idioma do usuário ou do conteúdo.

Vamos supor que temos uma tag chamada `Animals` que queremos traduzir para o alemão e o francês.

1. Abra o [console de marcação.](#tagging-console)

1. Selecione a tag que deseja traduzir e toque ou clique **Editar** na barra de ferramentas.

1. No **Editar tag** , no campo **Localização** selecione o idioma de destino, por exemplo, alemão.

1. No **Alemão** que for exibido, forneça o título traduzido.

1. Repita as duas etapas anteriores para francês.

   ![Tradução de títulos de tags](assets/translate-tag.png)

1. Toque ou clique **Enviar**.

Para páginas de conteúdo, o idioma escolhido para a tag é obtido do idioma da página, quando disponível.

No entanto, no ambiente de criação, o AEM usa a configuração de idioma do usuário. Portanto, no console de marcação, para o `Animals` tag, `Animaux` será exibido para um usuário que define o idioma como francês em suas propriedades de usuário.

Para adicionar um novo idioma ao diálogo, consulte o documento [Criação de tags em aplicativos AEM](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>Se quiser saber mais sobre os recursos de localização do AEM, consulte o documento [Tradução De Conteúdo Para Sites Multilíngues.](/help/sites-cloud/administering/translation/overview.md)
