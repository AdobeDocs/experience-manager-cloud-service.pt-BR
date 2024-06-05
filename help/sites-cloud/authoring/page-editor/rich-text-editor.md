---
title: Usar o editor de rich text no  [!DNL Adobe Experience Manager]  para criar conteúdo.
description: Usar o  [!DNL Experience Manager]  editor de rich text para criar conteúdo.
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 95%

---

# Usar o editor de rich text para criar conteúdo {#use-rich-text-editor-to-author-content}

O editor de rich text (RTE) é um elemento básico fundamental para adicionar conteúdo textual ao [!DNL Adobe Experience Manager]. Além disso, muitos outros componentes que permitem operações de criação se baseiam no RTE. Os desenvolvedores do Experience Manager podem personalizar o RTE e os administradores configuram o RTE para que seja usado por autores.

## Edição no local {#in-place-editing}

Selecionar um componente baseado em texto com um único clique para revelar a [componente.](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)

![A barra de ferramentas do componente](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

Clique novamente ou selecione inicialmente o componente com um clique duplo lento para abrir a edição no local. O modo de edição contém uma barra de ferramentas. Você pode editar o conteúdo e fazer alterações básicas na formatação.

![Edição no local com o RTE](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

Normalmente, a barra de ferramentas fornece as seguintes opções:

* **Formato**: realçar o texto em negrito ou itálico ou sublinhar o texto.
* **Listas**: criar listas com marcadores ou numeradas e definir o recuo.
* **Hiperlink**: criar links.
* **Desvincular**: remover o hiperlink.
* **Tela cheia**: abrir o editor no modo de tela cheia.
* **Fechar**: parar de editar.
* **Salvar**: salvar as alterações.

## Edição em tela cheia {#full-screen-editing}

Para componentes baseados em texto, clique no modo de tela cheia ![botão de tela cheia do RTE](/help/sites-cloud/authoring/assets/editing-full-screen.png) na [barra de ferramentas](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) para abrir o editor de rich text e ocultar o restante do conteúdo da página.

O modo de tela cheia exibe todas as opções configuradas que podem ser usadas para criação. A disponibilidade das opções [depende da configuração](/help/implementing/developing/extending/rich-text-editor.md).

![RTE no modo de tela cheia](/help/sites-cloud/authoring/assets/rte-full-screen.png)

Outras opções do editor de rich text incluem:

* **Âncora**: crie uma âncora no texto para acessá-la posteriormente por meio de um link ou incluir em uma referência.
* **Alinhar texto à esquerda**.
* **Centralizar texto**.
* **Alinhar texto à direita**.

Clique em Minimizar para fechar o modo de tela cheia.

>[!TIP]
>
>Copiar listas aninhadas do [!DNL Microsoft Word] para o RTE pode gerar resultados inconsistentes. Em vez disso, cole como texto e faça o ajuste manual.

>[!MORELIKETHIS]
>
>* [Configurar editores de rich text](/help/implementing/developing/extending/rich-text-editor.md)
