---
title: Como aplicar estilos em linha a componentes de formulário adaptáveis?
description: Embora você possa aplicar estilos personalizados em um Formulário adaptável, também pode aplicar propriedades CSS em linha a componentes individuais de um Formulário adaptável. Saiba como aplicar estilos em linha aos componentes do Formulário adaptável. Saiba mais usando um exemplo para aplicar o estilo em linha a um componente de campo de texto.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 3%

---

# Estilo em linha dos componentes do formulário adaptável {#inline-styling-of-adaptive-form-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/inline-style-adaptive-forms.html) |
| AEM as a Cloud Service | Este artigo |

Você pode definir a aparência geral e o estilo de um Formulário adaptável especificando estilos usando [editor de tema](themes.md). Além disso, você pode aplicar estilos CSS em linha a componentes individuais do Formulário adaptável e visualizar as alterações em tempo real. Os estilos embutidos substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos em linha a um componente:

1. Abra o formulário no editor de formulários e altere o modo para o modo de estilo. Para alterar o modo para o modo de estilo, na barra de ferramentas da página, toque em ![tela suspensa](assets/Smock_ChevronDown.svg) > **[!UICONTROL Estilo]**.
1. Selecione um componente na página e toque no botão editar ![botão editar](assets/edit.svg). As propriedades de estilo são abertas na barra lateral.

   Você também pode selecionar componentes da árvore de hierarquia de formulários na barra lateral. A árvore de hierarquia de formulários está disponível como Objetos de formulário na barra lateral.

   No [!UICONTROL Estilo] você pode ver os componentes listados em Objetos de formulário. No entanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. É possível selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades de CSS. É possível especificar propriedades como:

   * [!UICONTROL Dimension e Posição] (Configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuação, limpar, estouro)
   * [!UICONTROL Texto] (Família da fonte, peso, cor, tamanho, altura da linha e alinhamento)
   * [!UICONTROL Histórico] (Imagem e gradiente, cor do plano de fundo)
   * [!UICONTROL Borda] (Largura, estilo, cor, raio)
   * [!UICONTROL Efeitos] (Sombra, Opacidade)
   * [!UICONTROL Avançado] (Permite escrever CSS personalizado para o componente)

1. Da mesma forma, é possível aplicar estilos a outras partes de um componente, como [!UICONTROL Widget], [!UICONTROL Legenda], e [!UICONTROL Ajuda].
1. Toque **[!UICONTROL Concluído]** para confirmar as alterações ou **[!UICONTROL Cancelar]** para descartar as alterações.

## Exemplo: estilos em linha para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois que estilos em linha são aplicados a ele.

![Componente de caixa de texto antes da aplicação do estilo em linha](assets/no-style.png)

Componente Caixa de texto antes de aplicar propriedades de estilo em linha

Observe a alteração no estilo da caixa de texto, como mostrado na imagem a seguir, após aplicar as seguintes propriedades CSS.

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
   <td><p>borda</p> </td>
   <td><p>Largura da borda =2px</p> <p>Estilo da borda=Sólido</p> <p>Cor da borda=#1111</p> </td>
   <td><p>Cria uma borda preta com 2 pixels de largura em torno do campo</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Altera a cor de fundo para CornflowerBlue (#6495ED)</p> <p>Observação: você pode especificar um nome de cor ou seu código hexadecimal no campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimension e Posição &gt; largura</p> </td>
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
   <td><p>centro</p> </td>
   <td><p>Alinha a descrição longa da ajuda para centralizar</p> </td>
  </tr>
 </tbody>
</table>

![Estilo da caixa de texto após a aplicação do estilo em linha](assets/applied-style.png)

Componente Caixa de texto após aplicar propriedades de estilo em linha

Seguindo as etapas acima, você pode selecionar e estilizar outros componentes, como painéis, botões de envio e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam de acordo com o componente selecionado.

## Copiar e colar estilos {#copy-paste-styles}

Também é possível copiar e colar um estilo de um componente para outro em um Formulário adaptável. No **[!UICONTROL Estilo]** toque no componente e no ícone Copiar ![Copiar](assets/property-copy-icon.svg).

Toque no outro componente do mesmo tipo e toque no ícone Colar ![Copiar](assets/Smock_Paste_18_N.svg) para colar o estilo copiado. Também é possível tocar no ícone Limpar estilo ![Copiar](assets/clear-style-icon.svg) para limpar o estilo aplicado.

## Definir estilos para diferentes estados de um componente {#set-styles-for-states}

É possível definir estilos para diferentes estados de um tipo de componente. Os diferentes estados incluem: [!UICONTROL Foco], [!UICONTROL Desabilitado], [!UICONTROL Hover], [!UICONTROL Erro], [!UICONTROL Sucesso], e [!UICONTROL Obrigatório].

Para definir o estilo para o estado de um componente:

1. No **[!UICONTROL Estilo]** toque no componente e no ícone Editar ![Editar](assets/Smock_Edit_18_N.svg).

1. Selecione o estado do componente usando a variável **[!UICONTROL Estado]** lista suspensa.

   ![Selecionar estado](assets/select-state.png)

1. Defina o estilo para o estado selecionado do componente e toque em ![Salvar](assets/save_icon.svg) para salvar as propriedades.

Também é possível simular os estados de sucesso e erro. Toque no ícone Expandir para exibir a **[!UICONTROL Simular o sucesso]** e **[!UICONTROL Simular Erro]** opções.

![Simular estados](assets/simulate-states.png)
