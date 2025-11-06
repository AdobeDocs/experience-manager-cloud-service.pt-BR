---
title: Editar as propriedades da página
description: Saiba como editar as propriedades de uma página, alterar o comportamento da página e como ela é gerenciada.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 8fee7e24-bbaa-4cc4-a047-165c9f2cd973
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 24%

---

# Editar as propriedades da página {#page-properties}

Saiba como editar [as propriedades de uma página](/help/sites-cloud/authoring/sites-console/page-properties.md) e alterar o comportamento da página e como ela é gerenciada.

>[!TIP]
>
>Para obter detalhes sobre as propriedades de página individuais disponíveis, consulte o documento [Propriedades da Página.](/help/sites-cloud/authoring/sites-console/page-properties.md)

## Onde editar as propriedades da página {#where}

É possível editar propriedades de página de vários locais no AEM.

* [No &#x200B;](#from-the-sites-console)
* [No Editor de páginas](#from-the-page-editor)
* [No Editor universal](#from-the-universal-editor)

Usando o Console Sites, você também pode [editar as propriedades de várias páginas de uma só vez.](#editing-multiple-pages)

### No console Sites {#from-the-sites-console}

Ao navegar pelo seu conteúdo no console do **Sites**, você pode usar o botão **Propriedades** na barra de ferramentas para editar as propriedades da página:

1. Usando o console [**Sites**,](/help/sites-cloud/authoring/sites-console/introduction.md) navegue até o local da página no qual deseja exibir e editar propriedades.
1. Selecione a opção **Propriedades da exibição** para a página desejada usando uma das seguintes opções:
   * [Ações rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)
   * As propriedades da página são exibidas usando as guias adequadas.
1. Exiba ou edite as propriedades conforme necessário.
1. Em seguida, clique em **Salvar** para salvar as atualizações, e em **Fechar** para retornar ao console.

### No Editor de páginas {#from-the-page-editor}

Ao editar uma página usando o Editor de páginas, você pode usar **Informações da página** para definir as propriedades da página:

1. No [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), abra a página na qual deseja editar propriedades.
1. Selecione o ícone **Informações da página** para abrir o menu de seleção:
1. Selecione **Abrir propriedades** e uma caixa de diálogo será aberta permitindo que você edite as propriedades, classificadas pela guia apropriada. Os seguintes botões estão disponíveis à direita da barra de ferramentas:
   * **Cancelar**
   * **Salvar e fechar**
1. Use o botão **Salvar e fechar** para salvar as alterações.

## No Editor universal {#from-the-universal-editor}

Ao editar uma página usando o Editor Universal, você pode usar o ícone **Propriedades da Página** para editar as propriedades:

1. No [Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties), abra a página na qual deseja editar propriedades.
1. Selecione o ícone **Propriedades da página** na barra de ferramentas.
1. A janela de propriedades de página do AEM é aberta em uma nova guia do navegador como se você estivesse editando as propriedades de página no [Editor de páginas.](#from-the-page-editor) Os seguintes botões estão disponíveis à direita da barra de ferramentas:
   * **Cancelar**
   * **Salvar e fechar**
1. Use o botão **Salvar e fechar** para salvar as alterações.
1. Retorne à guia do navegador do Universal Editor.

## Editar as propriedades de várias páginas {#editing-multiple-pages}

No console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), é possível selecionar várias páginas e usar **Propriedades de Exibição** para exibir e/ou editar as propriedades da página. Isso é conhecido como edição em massa das propriedades da página.

Você pode selecionar várias páginas para a edição em massa por meio de vários métodos, incluindo:

* Ao navegar pelos consoles dos **Sites**
* Depois de usar a função **Pesquisar** para localizar um conjunto de páginas

Depois de selecionar as páginas e clicar ou tocar na opção **Propriedades**, as propriedades em massa são mostradas:

![Propriedades da página de edição em massa](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Só é possível editar em massa as páginas que:

* Compartilham o mesmo tipo de recurso
* Não fazem parte de uma Live Copy
   * Se qualquer uma das páginas selecionadas fizer parte de uma Live Copy, uma mensagem será exibida quando as propriedades forem abertas.

A janela de edição de itens em massa é dividida na metade vertical:

* O lado esquerdo é uma lista das páginas selecionadas para edição de itens em massa.

   * Você pode marcar/desmarcar as páginas conforme necessário.
   * Por padrão, todos são selecionados.

* O direito é uma lista de [propriedades disponíveis para edição em massa.](/help/implementing/developing/extending/bulk-editor.md)

   * Assim como ao visualizar propriedades de uma única página, as propriedades são ordenadas em guias.
   * As propriedades que estão disponíveis em todas as páginas selecionadas e tenham sido explicitamente definidas como disponíveis para a edição de itens em massa estão visíveis.
   * Se você reduzir a seleção de página para uma página, em seguida, todas as propriedades ficarão visíveis.
   * Somente as propriedades com um valor comum são exibidas.
   * Quando o campo tem vários valores (por exemplo, Marcas), eles só serão exibidos quando *todos* forem comuns. Se apenas algumas forem comuns, elas só serão exibidas durante a edição.

* Os campos que são comuns, mas têm valores diferentes em várias páginas, são indicados com um valor especial, como o texto `<Mixed Entries>`.

É possível atualizar os valores nos campos disponíveis nas páginas selecionadas. Os novos valores são aplicados a todas as páginas selecionadas ao selecionar **Concluído**. Quando o campo tem vários valores (por exemplo, Tags), você pode anexar um novo valor ou remover um valor comum.

## Herança da propriedade {#inheritance}

Se a página for baseada em um blueprint ou herdar conteúdo de outra página, a herança será refletida na janela **Propriedades da página** do campo individual.

![Propriedades herdadas](assets/property-inhertiance.png)

As propriedades herdadas não podem ser editadas. Toque ou clique no ícone **Cancelar herança** ao lado de um campo específico para interromper sua herança.

![Cancelar herança](assets/cancel-inheritance.png)

Confirme o cancelamento no modal **Cancelar herança**.

![Cancelar modal de confirmação da herança](assets/cancel-inheriance-confirmation.png)

Quando a herança é cancelada para um campo, ele se torna editável.

![Herança cancelada](assets/property-inheritance-broken.png)

Para restabelecer a herança, toque ou clique no ícone **Reverter herança** ao lado do campo.

![Reverter herança](assets/revert-inheritance.png)

Confirme a reversão no modal **Reverter herança**.

![Reverter modal de confirmação de herança](assets/revert-inhertiance-confirmation.png)

Selecione **Sincronizar página após reverter a herança** para atualizar o campo com os valores mais recentes no blueprint. Caso contrário, os valores serão atualizados na próxima vez que o Live Copy for sincronizado.

>[!TIP]
>
>Para obter mais informações sobre herança, consulte o documento [Gerenciador de vários sites e Tradução](/help/sites-cloud/administering/msm-and-translation.md)
