---
title: Como aplicar estilos em linha a componentes de formulário adaptáveis?
description: Saiba como aplicar estilos personalizados em um Formulário adaptável, você também pode aplicar propriedades CSS em linha a componentes individuais de um Formulário adaptável.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---

# Estilo em linha dos componentes do formulário adaptável {#inline-styling-of-adaptive-form-components}

>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/inline-style-adaptive-forms.html) |
| AEM as a Cloud Service | Este artigo |

Você pode definir a aparência geral e o estilo de um Formulário adaptável especificando estilos com o [editor de temas](themes.md). Além disso, você pode aplicar estilos CSS em linha a componentes individuais do Formulário adaptável e visualizar as alterações em tempo real. Os estilos embutidos substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos em linha a um componente:

1. Abra o formulário no construtor de formulários e altere o modo para o modo de estilo. Para alterar o modo para o modo de estilo, na barra de ferramentas da página, selecione ![tela suspensa](assets/Smock_ChevronDown.svg) > **[!UICONTROL Estilo]**.
1. Selecione um componente na página e selecione o botão de edição ![botão de edição](assets/edit.svg). As propriedades de estilo são abertas na barra lateral.

   Você também pode selecionar componentes da árvore de hierarquia de formulários na barra lateral. A árvore de hierarquia de formulários está disponível como Objetos de formulário na barra lateral.

   No modo [!UICONTROL Style], é possível ver os componentes listados em Objetos de formulário. No entanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. É possível selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades de CSS. É possível especificar propriedades como:

   * [!UICONTROL Dimensões e Posição] (Configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuante, limpar, estouro)
   * [!UICONTROL Texto] (Família da fonte, peso, cor, tamanho, altura da linha e alinhamento)
   * [!UICONTROL Plano de fundo] (imagem e gradiente, cor do plano de fundo)
   * [!UICONTROL Borda] (Largura, estilo, cor, raio)
   * [!UICONTROL Efeitos] (Sombra, Opacidade)
   * [!UICONTROL Avançado] (Permite gravar CSS personalizado para o componente)

1. Da mesma forma, você pode aplicar estilos a outras partes de um componente, como o [!UICONTROL Widget], [!UICONTROL Legenda] e [!UICONTROL Ajuda].
1. Selecione **[!UICONTROL Concluído]** para confirmar as alterações ou **[!UICONTROL Cancelar]** para descartar as alterações.

## Exemplo: estilos em linha para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois que estilos em linha são aplicados a ele.

![Componente de caixa de texto antes da aplicação do estilo embutido](assets/no-style.png)

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
   <td><p>Rótulo</p> </td>
   <td><p>Dimensões e posição &gt; largura</p> </td>
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

![Estilo da caixa de texto após a aplicação do estilo incorporado](assets/applied-style.png)

Componente Caixa de texto após aplicar propriedades de estilo em linha

Seguindo as etapas acima, você pode selecionar e estilizar outros componentes, como painéis, botões de envio e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam de acordo com o componente selecionado.

## Copiar e colar estilos {#copy-paste-styles}

Também é possível copiar e colar um estilo de um componente para outro em um Formulário adaptável. No modo **[!UICONTROL Estilo]**, selecione o componente e o ícone Copiar ![Copiar](assets/property-copy-icon.svg).

Selecione o outro componente do mesmo tipo e selecione o ícone Colar ![Copiar](assets/Smock_Paste_18_N.svg) para colar o estilo copiado. Você também pode selecionar o ícone Limpar Estilo ![Copiar](assets/clear-style-icon.svg) para limpar o estilo aplicado.

## Definir estilos para diferentes estados de um componente {#set-styles-for-states}

É possível definir estilos para diferentes estados de um tipo de componente. Os diferentes estados incluem: [!UICONTROL Foco], [!UICONTROL Desabilitado], [!UICONTROL Foco], [!UICONTROL Erro], [!UICONTROL Sucesso] e [!UICONTROL Obrigatório].

Para definir o estilo para o estado de um componente:

1. No modo **[!UICONTROL Estilo]**, selecione o componente e o ícone Editar ![Editar](assets/Smock_Edit_18_N.svg).

1. Selecione o estado do componente usando a lista suspensa **[!UICONTROL Estado]**.

   ![Selecionar estado](assets/select-state.png)

1. Defina o estilo para o estado selecionado do componente e selecione ![Salvar](assets/save_icon.svg) para salvar as propriedades.

Também é possível simular os estados de sucesso e erro. Selecione o ícone Expandir para exibir as opções **[!UICONTROL Simular Êxito]** e **[!UICONTROL Simular Erro]**.

![Simular estados](assets/simulate-states.png)


## Consulte também {#see-also}

{{see-also}}


<!--

>[!MORELIKETHIS]
>
>* [Use themes in Adaptive Form Core Components ](/help/forms/using-themes-in-core-components.md)

-->