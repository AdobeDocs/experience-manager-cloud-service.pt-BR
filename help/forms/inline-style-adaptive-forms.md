---
title: Como aplicar estilos em linha aos componentes de formulário adaptáveis?
description: Embora seja possível aplicar estilos personalizados em um Formulário adaptável, também é possível aplicar propriedades de CSS em linha em componentes individuais de um Formulário adaptável. Saiba como aplicar estilos em linha aos componentes do Formulário adaptável. Aprofunde-se usando um exemplo para aplicar o estilo em linha a um componente de campo de texto.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Estilo em linha dos componentes do formulário adaptável {#inline-styling-of-adaptive-form-components}

Você pode definir a aparência e o estilo gerais de um formulário adaptável especificando estilos usando [editor de temas](themes.md). Além disso, você pode aplicar estilos CSS em linha a componentes individuais do Formulário adaptável e visualizar as alterações dinamicamente. Os estilos em linha substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos em linha a um componente:

1. Abra o formulário no editor de formulário e altere o modo para o modo de estilo. Para alterar o modo para o modo de estilo, na barra de ferramentas da página, toque em ![lista suspensa de tela](assets/Smock_ChevronDown.svg) > **[!UICONTROL Estilo]**.
1. Selecione um componente na página e toque no botão Editar ![botão editar](assets/edit.svg). Propriedades de estilo abertas na barra lateral.

   Você também pode selecionar componentes da árvore de hierarquia do formulário na barra lateral. A árvore da hierarquia do formulário está disponível como Objetos de formulário na barra lateral.

   No [!UICONTROL Estilo] , é possível ver componentes listados em Objetos de formulário. No entanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes, como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. Você pode selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades de CSS. É possível especificar propriedades, como:

   * [!UICONTROL Dimension &amp; Posição] (Configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuante, limpar, sobrefluxo)
   * [!UICONTROL Texto] (Família de fontes, peso, cor, tamanho, altura da linha e alinhamento)
   * [!UICONTROL Histórico] (Imagem e gradiente, cor de fundo)
   * [!UICONTROL Borda] (Largura, estilo, cor, raio)
   * [!UICONTROL Efeitos] (Sombra, Opacidade)
   * [!UICONTROL Avançado] (Permite gravar CSS personalizado para o componente)

1. Da mesma forma, é possível aplicar estilos para outras partes de um componente, como [!UICONTROL Widget], [!UICONTROL Legenda]e [!UICONTROL Ajuda].
1. Toque **[!UICONTROL Concluído]** para confirmar as alterações ou **[!UICONTROL Cancelar]** para descartar as alterações.

## Exemplo: estilos em linha para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois da aplicação dos estilos em linha.

![Componente de caixa de texto antes da aplicação do estilo em linha](assets/no-style.png)

Componente de caixa de texto antes de aplicar as propriedades de estilo em linha

Observe a alteração no estilo da caixa de texto, como mostrado na imagem a seguir, após aplicar as seguintes propriedades de CSS.

<table>
 <tbody>
  <tr>
   <td><p>Seletor</p> </td>
   <td><p>Propriedade CSS</p> </td>
   <td><p>Valor</p> </td>
   <td><p>Efeito</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>border</p> </td>
   <td><p>Largura da borda =2px</p> <p>Estilo da borda=Sólido</p> <p>Cor da borda=#1111</p> </td>
   <td><p>Cria uma borda em preto de 2 px ao redor do campo</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Altera a cor de fundo para CornflorBlue (#6495ED)</p> <p>Observação: Você pode especificar um nome de cor ou seu código hexadecimal no campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimension &amp; Posição &gt; largura</p> </td>
   <td><p>100px</p> </td>
   <td><p>Corrige a largura como 100px para o rótulo</p> </td>
  </tr>
  <tr>
   <td>Ícone da ajuda do campo</td>
   <td>Texto &gt; Cor da fonte</td>
   <td>#2ECC40</td>
   <td>Altera a cor da face do ícone de ajuda.</td>
  </tr>
  <tr>
   <td><p>Descrição longa</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Alinha a descrição longa para a ajuda do centro</p> </td>
  </tr>
 </tbody>
</table>

![Estilo da caixa de texto após a aplicação do estilo em linha](assets/applied-style.png)

Componente de caixa de texto após aplicar as propriedades de estilo em linha

Após as etapas acima, você pode selecionar e criar um estilo para outros componentes, como painéis, botões Enviar e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam de acordo com o componente selecionado.

## Copiar e colar estilos {#copy-paste-styles}

Também é possível copiar e colar um estilo de um componente para outro componente em um formulário adaptável. No **[!UICONTROL Estilo]** , toque no componente e no ícone Copiar ![Copiar](assets/property-copy-icon.svg).

Toque no outro componente do mesmo tipo e toque no ícone Colar ![Copiar](assets/Smock_Paste_18_N.svg) para colar o estilo copiado. Também é possível tocar no ícone Limpar estilo ![Copiar](assets/clear-style-icon.svg) para limpar o estilo aplicado.

## Definir estilos para diferentes estados de um componente {#set-styles-for-states}

É possível definir estilos para diferentes estados de um tipo de componente. Os diferentes estados incluem: [!UICONTROL Foco], [!UICONTROL Desabilitado], [!UICONTROL Hover], [!UICONTROL Erro], [!UICONTROL Sucesso]e [!UICONTROL Obrigatório].

Para definir o estilo de um estado de um componente:

1. No **[!UICONTROL Estilo]** , toque no componente e no ícone Editar ![Editar](assets/Smock_Edit_18_N.svg).

1. Selecione o estado do componente usando o **[!UICONTROL Estado]** lista suspensa.

   ![Selecionar estado](assets/select-state.png)

1. Defina o estilo do estado selecionado do componente e toque em ![Salvar](assets/save_icon.svg) para salvar as propriedades.

Também é possível simular os estados de sucesso e erro. Toque no ícone Expandir para exibir o **[!UICONTROL Simular sucesso]** e **[!UICONTROL Erro Simular]** opções.

![Simular estados](assets/simulate-states.png)
