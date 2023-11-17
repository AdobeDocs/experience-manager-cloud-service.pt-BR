---
title: Edição com contexto no Editor universal
description: Explore como você pode usar o Editor universal para editar qualquer aspecto do conteúdo no local e no contexto em qualquer implementação.
hidefromtoc: true
index: false
exl-id: a4854a56-9434-4d15-a56a-f1798f27263a
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 11%

---


# Edição com contexto no Editor universal {#editing-in-context}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor"
>title="Edição com contexto no Editor universal"
>abstract="Veja como seus aplicativos headless podem aproveitar o Universal Editor para trazer uma edição contextual e de baixo atrito ao alcance de seus autores."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide"
>title="Iniciar o Editor universal"
>abstract="Neste guia, exploraremos o Editor universal e como ele permite que as pessoas editem cada aspecto de seu conteúdo em qualquer implementação, resultando em uma velocidade de conteúdo aprimorada.<br><br>Inicie este módulo em uma nova guia clicando abaixo e, em seguida, siga este guia."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide_footer"
>title="Neste módulo, você aprendeu a personalizar conteúdo para o contexto e local usando o Universal Editor."
>abstract=""

## Editar texto no contexto {#edit-text}

A edição no local e no contexto geralmente pode ser vantajosa em relação à edição de conteúdo headless estruturado, como no editor de fragmentos de conteúdo, que você viu nos módulos anteriores.

>[!NOTE]
>
>Para usar o Editor universal nesta versão de avaliação, você deve usar o Chrome como navegador e não no modo incógnito. Essa é uma limitação da experiência de avaliação, não do Universal Editor.

Com o Editor universal, você tem uma maneira ágil de editar seu texto no contexto e no local, permitindo a criação de conteúdo simples e intuitiva.

1. O editor deve ser carregado por padrão no **Componentes** modo. Caso contrário, selecione o **Componentes** ícone no painel de modo no lado esquerdo do editor.

1. Selecione duas vezes o título do artigo mais recente para editá-lo.

   ![O Editor universal](assets/do-not-localize/ue-component-mode.png)

1. O componente é selecionado conforme indicado por uma borda azul com uma guia indicando que é um componente de texto. Há um cursor na borda aguardando a entrada de texto. Alterar o texto para `Aloha Spirit in Lofoten`.

   ![Edição de texto no Editor universal](assets/do-not-localize/ue-edit-text-2.png)

1. Pressione a tecla enter/return ou selecione fora do componente de texto e suas alterações são salvas automaticamente.

O Editor universal salva as alterações automaticamente no ambiente de criação. Você ainda precisa publicá-las para que seus leitores vejam, o que faremos em uma etapa posterior.

## Editar mídia no contexto {#edit-media}

Você também pode trocar imagens enquanto ainda permanece no contexto do conteúdo usando o Editor universal.

1. Restante em **Componentes** selecione a imagem do surfer que será selecionada.

1. No painel de componentes, é possível ver os detalhes do ativo. Selecione o **Imagem em destaque** miniatura.

   ![Seleção de uma imagem para edição](assets/do-not-localize/ue-edit-media.png)

1. No **Selecionar ativos** , role para baixo e selecione o `surfer-wave-02.JPG` imagem para selecioná-la.

1. Selecionar **Selecionar** no **Selecionar ativos** janela.

   ![Uso da janela Selecionar ativo para selecionar uma imagem](assets/do-not-localize/ue-select-asset.png)

A imagem é substituída pela que você selecionou.

## Experimente Seu Conteúdo Como Seus Reader {#emulators}

O Editor universal permite interagir com o conteúdo em seu contexto, vendo o conteúdo conforme é entregue aos dispositivos dos usuários.

1. Por padrão, o editor renderiza a versão para desktop do seu conteúdo. Selecione o botão Emulador na parte superior direita do editor para alterar o dispositivo de destino.

   ![O item de menu do emulador](assets/do-not-localize/ue-emulator-1.png)

1. Os Reader podem estar em diferentes dispositivos com diferentes taxas de proporção, de modo que o editor oferece modos de emulação para ver como a página será apresentada aos usuários. Por exemplo, selecione a opção de dispositivo móvel no modo retrato.

   ![O item de menu do emulador](assets/do-not-localize/ue-emulator-2.png)

1. Veja a alteração de conteúdo no editor. O ícone do emulador também muda para refletir o modo em que está. Selecione qualquer lugar fora do menu do emulador para fechá-lo e interagir com seu conteúdo.

1. Retorne o emulador ao modo desktop.

Você também pode especificar dimensões exatas para o emulador e girar o dispositivo emulado para exibir seu conteúdo em qualquer dispositivo de destino em potencial.

## Pré-visualização e publicação {#preview}

Como é necessário selecionar o conteúdo para selecioná-lo no editor, o editor não permite que você siga links ou interaja com o conteúdo tocando ou clicando quando ele está em modo de edição. Usando o modo de visualização, você pode seguir os links no seu conteúdo e experimentá-lo como seus usuários fariam antes de publicar.

1. No painel de modos no lado esquerdo do editor, selecione **Visualizar**.

1. Agora selecione a variável **Leia mais** para o artigo principal.

   ![Modo de visualização](assets/do-not-localize/ue-preview-publish-1.png)

1. Navegue pelo artigo e use o **Voltar** para retornar à página principal.

   ![Retornar à página principal usando o link Voltar](assets/do-not-localize/ue-preview-publish-3.png)

1. Agora selecione a variável **Publish** botão na parte superior direita do editor para publicar seu conteúdo.

   ![Os itens de menu de visualização e publicação](assets/do-not-localize/ue-preview-publish-4.png)

Seu conteúdo foi publicado.

## Edição de fragmentos de conteúdo {#editing-fragments}

Para acelerar sua experiência de criação de conteúdo quando a edição estruturada de conteúdo headless for mais vantajosa do que a edição no local, o Editor universal também oferece acesso rápido ao editor de fragmentos de conteúdo.

1. Role mais para baixo na página até a **Aventuras** seção.

1. No painel de modos no lado esquerdo do editor, selecione **Componentes**. Isso permite selecionar componentes de página no editor.

1. Selecione uma das aventuras, como **Campo de Surf de Bali** para selecioná-la.

   * Observe o contorno azul do componente selecionado. A guia deve exibir o nome do fragmento de conteúdo quando um fragmento de conteúdo for selecionado. Nesse caso **Campo de Surf de Bali**.
   * Como o Editor universal permite selecionar qualquer objeto na página, os componentes que fazem parte de um fragmento de conteúdo também podem ser selecionados individualmente. Selecione onde indicado na ilustração para selecionar o componente Fragmento de conteúdo inteiro.

1. A variável **Editar** ícone é exibido no painel de componentes. Selecione o **Editar** ícone para abrir o editor de Fragmento de conteúdo em uma nova guia.

![Seleção de fragmentos de conteúdo no editor universal](assets/do-not-localize/ue-content-fragments.png)

Na nova guia, agora é possível editar o fragmento de conteúdo selecionado no Editor universal.
