---
title: Criação de conteúdo com o Editor universal
description: Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: ffe90d3919c0f0c1a1c60efccc0191118dfaa84a
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 24%

---


# Criação de conteúdo com o Editor universal {#authoring}

Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.

## Introdução {#introduction}

O Editor universal permite a edição de qualquer aspecto de qualquer conteúdo em qualquer implementação, para que você possa oferecer experiências excepcionais, aumentar a velocidade do conteúdo e proporcionar uma experiência de desenvolvedor de última geração.

Para isso, o editor universal oferece aos autores de conteúdo uma interface intuitiva que exige apenas um treinamento mínimo para que eles possam simplesmente entrar e começar a editar o conteúdo. Este documento descreve a experiência de criação do Editor Universal.

>[!NOTE]
>
>Este documento supõe que você já esteja familiarizado com como acessar e navegar pelo Editor universal. Se você não estiver, consulte o documento [Acessando e Navegando no Editor Universal.](/help/sites-cloud/authoring/universal-editor/navigation.md)

>[!TIP]
>
>Para obter uma introdução mais detalhada do Editor universal, consulte o documento [Introdução ao Editor universal.](/help/implementing/universal-editor/introduction.md)

## Editar o conteúdo {#editing-content}

A edição de conteúdo é simples e intuitiva. À medida que você passa o mouse sobre o conteúdo no editor, o conteúdo editável é realçado com um contorno azul fino.

![O conteúdo editável é destacado por uma caixa azul](assets/editable-content.png)

>[!TIP]
>
>Por padrão, tocar ou clicar em um conteúdo o seleciona para edição. Se você deseja navegar pelo seu conteúdo seguindo os links, alterne para o [modo de visualização.](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)

Dependendo do conteúdo selecionado, você pode ter diferentes opções de edição no local e outras informações e opções para o conteúdo no painel de propriedades [.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

### Edição de Texto sem Formatação {#edit-plain-text}

É possível editar o texto no local clicando duas vezes ou tocando duas vezes no componente.

![Editar o conteúdo](assets/editing-content.png)

O contorno azul fino se transforma em um contorno azul pesado para indicar a seleção e a exibição de um cursor. Faça as alterações e pressione Enter/Return ou selecione fora da caixa de texto para salvar as alterações.

Ao selecionar o componente de texto, seus detalhes são mostrados no painel de propriedades [.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) Também é possível editar o texto no painel.

![Editando texto no painel de propriedades](assets/ue-editing-text-component-rail.png)

Além disso, os detalhes do texto estão disponíveis no painel de propriedades. As alterações são salvas automaticamente quando o foco sai do campo editado no painel de propriedades.

### Edição de Rich Text {#edit-rich-text}

É possível editar o texto no local clicando duas vezes ou tocando duas vezes no componente.

![Edição de um componente de rich text](assets/rich-text-editing.png)

Para sua conveniência, as opções de formatação e os detalhes do texto estão disponíveis em dois lugares.

#### O Menu de Contexto {#context-menu}

O menu de contexto é aberto acima do bloco de rich text e oferece opções básicas de formatação no contexto. Devido a limitações de espaço, algumas opções podem estar ocultas atrás do botão de reticências.

![Menu de contexto de rich text](assets/rich-text-context-menu.png)

As alterações são salvas automaticamente quando o foco sai do campo editado.

#### O painel Propriedades {#properties-rail}

O [painel de propriedades](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) mostra um item para o texto selecionado. Toque na entrada para abrir uma caixa de diálogo apresentando uma tela maior para editar o texto.

![Caixa de diálogo de edição de rich text](assets/rich-text-canvas.png)

Toque ou clique em **Cancelar** ou **Concluído** para descartar ou salvar as alterações, respectivamente.

### Editando mídia {#edit-media}

Você pode exibir seus detalhes no [painel de propriedades.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

![Editando mídia](assets/ue-edit-media.png)

1. Toque ou clique na visualização da imagem selecionada no painel de propriedades.
1. A janela [seletor de ativos](/help/assets/overview-asset-selector.md#using-asset-selector) é aberta para permitir que você selecione um ativo.
1. Selecione para selecionar um novo ativo.
1. Selecione **Selecionar** para retornar ao painel de propriedades onde o ativo foi substituído.

As alterações são salvas no conteúdo automaticamente.

### Edição de fragmentos de conteúdo {#edit-content-fragment}

Se você selecionar um [Fragmento do conteúdo](/help/sites-cloud/administering/content-fragments/overview.md), poderá editar seus detalhes no [painel de propriedades.](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

![Editando um fragmento de conteúdo](assets/ue-edit-cf.png)

Os campos definidos no modelo de conteúdo do fragmento de conteúdo selecionado são exibidos e editáveis no painel de propriedades.

Se você selecionar um campo relacionado a um Fragmento de conteúdo, ele será carregado no painel Componentes e o campo será rolado automaticamente para o.

As alterações são salvas automaticamente quando o foco sai do campo editado no painel de propriedades.

Se, em vez disso, você quiser editar seu Fragmento de Conteúdo no [editor de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md), toque ou clique no botão [**Abrir no Editor de Conteúdo**](/help/sites-cloud/authoring/universal-editor/navigation.md#edit) no painel de propriedades.

>[!TIP]
>
>Use a tecla de atalho `e` para editar o fragmento de conteúdo selecionado no editor de fragmentos de conteúdo.

Dependendo das necessidades do fluxo de trabalho, talvez você queira editar o Fragmento de conteúdo no Editor universal ou diretamente no editor de Fragmento de conteúdo.

>[!NOTE]
>
>O Editor Universal [valida campos de Fragmento de Conteúdo com base em seus modelos](/help/assets/content-fragments/content-fragments-models.md#validation), permitindo que você imponha regras de integridade de dados, como padrões de regex e restrições de exclusividade.
>
>Isso garante que seu conteúdo atenda às necessidades específicas dos negócios antes de ser publicado.

### Adicionar componentes a contêineres {#adding-components}

1. Selecione um componente de contêiner na [árvore de conteúdo](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) ou no editor.
1. Em seguida, selecione o ícone adicionar no painel de propriedades.

   ![Selecionar um componente para adicionar a um contêiner](assets/ue-add-component.png)

O componente é inserido no container e pode ser editado no editor.

>[!TIP]
>
>Use a tecla de atalho `a` para adicionar um componente ao contêiner selecionado.

### Exclusão de componentes de contêineres {#deleting-components}

1. Selecione um componente de contêiner na [árvore de conteúdo](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) ou no editor.
1. Selecione o ícone de divisa do container para expandir seu conteúdo na árvore de conteúdo.
1. Em seguida, na árvore de conteúdo, selecione um componente no contêiner.
1. Selecione o ícone excluir no painel de propriedades.

   ![Excluindo um componente](assets/ue-delete-component.png)

O componente selecionado foi excluído.

>[!TIP]
>
>Use a tecla de atalho `Shift+Backspace` para excluir o componente selecionado de seu contêiner.

### Reorganização de componentes em contêineres {#reordering-components}

1. Se ainda não estiver no modo de árvore de conteúdo [, ](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) alterne para ele.
1. Selecione um componente de container na árvore de conteúdo ou no editor.
1. Selecione o ícone de divisa do container para expandir seu conteúdo na árvore de conteúdo.
1. Arraste os ícones de alça ao lado dos componentes dentro do contêiner para mostrar que você pode reorganizá-los. Arraste os componentes para reordená-los no contêiner.

   ![Reordenando componentes](assets/ue-reordering-components.png)

1. O componente arrastado fica cinza na árvore de conteúdo, enquanto o ponto de inserção é representado por uma linha azul. Libere o componente para colocá-lo em seu novo local.

Os componentes são reordenados na árvore de conteúdo e no editor

## Visualização de conteúdo {#previewing-content}

Ao terminar de editar o conteúdo, você geralmente deseja navegar por ele e observar como ele é exibido em outras páginas. No [modo de visualização](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode), é possível clicar em links e navegar pelo conteúdo, como um leitor faria. O conteúdo é renderizado no editor como seria publicado.

No modo de visualização, tocar ou clicar em um conteúdo reage como faria com um leitor do conteúdo. Se quiser selecionar o conteúdo para edição, desative o [modo de visualização.](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)

## Recursos adicionais {#additional-resources}

Para saber como publicar conteúdo com o editor universal, consulte este documento.

* [Publicando Conteúdo com o Editor Universal](publishing.md) - Saiba como o Editor Universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.

Para saber mais sobre os detalhes técnicos do Universal Editor, consulte estes documentos do desenvolvedor.

* [Introdução ao Editor universal](/help/implementing/universal-editor/introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.
* [Introdução ao Editor universal no AEM](/help/implementing/universal-editor/getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](/help/implementing/universal-editor/architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](/help/implementing/universal-editor/attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](/help/implementing/universal-editor/authentication.md): saiba como funciona a autenticação do Editor universal.

## Editar herança de componente {#inheritance}

Herança é o mecanismo no qual o conteúdo pode ser vinculado de modo que a alteração de um altere automaticamente o outro.

Usando o Editor universal, você pode cancelar a herança de conteúdo simplesmente atualizando o conteúdo. O editor desativa automaticamente a herança de todas as alterações feitas pelos autores nessa página, garantindo que o conteúdo modificado seja retido quando as atualizações forem sincronizadas do blueprint.

Para obter mais detalhes sobre como a herança funciona usando o Editor Universal, consulte o documento [Herança de Conteúdo no Editor Universal.](/help/sites-cloud/authoring/universal-editor/inheritance.md)
