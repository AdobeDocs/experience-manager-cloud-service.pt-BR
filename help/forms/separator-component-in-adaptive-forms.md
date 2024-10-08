---
title: O que é o componente separador no Adaptive Forms?
description: O componente Separador no Adaptive Forms ajuda a segregar visualmente as seções de um formulário.
feature: Adaptive Forms, Foundation Components
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# Componente separador no Adaptive Forms{#separator-component-in-adaptive-forms}

Você pode usar o componente separador para segregar visualmente os painéis de um formulário. Você pode definir a aparência geral e o estilo de um componente separador especificando as seguintes propriedades do componente separador:

* **Nome do Elemento:** Especifica o nome do componente. As expressões SOM endereçam o componente com um valor especificado no campo Nome do elemento.
* **Espessura:** Especifica a espessura do componente separador em pixels.

* **Classe CSS:** Especifica a classe CSS personalizada para o componente separador

* **Estilos embutidos:** com [!DNL AEM Forms], agora é possível aplicar estilos CSS embutidos a componentes individuais do Formulário adaptável e visualizar as alterações em tempo real.

Você pode usar o modo Layout para definir o número de colunas ao qual o componente separador se estende. Para obter mais informações, consulte [Usar o modo de layout para redimensionar componentes](resize-using-layout-mode.md).

Para especificar as propriedades de um componente separador:

1. Selecione um componente separador e selecione ![cmppr](assets/cmppr.png). As propriedades são abertas na barra lateral.
1. Clique em uma guia na seção Propriedades CSS em linha para especificar propriedades CSS. Por exemplo, a. Na guia Field, clique em **Add Item**. Uma linha com dois campos é adicionada.
1. No primeiro campo à esquerda, especifique uma propriedade CSS3 que deseja aplicar. Por exemplo, **borda**. Você também pode selecionar uma propriedade clicando no botão de seta para baixo. A lista suspensa não é exaustiva e você pode especificar qualquer nome de propriedade CSS3 compatível nesse campo.
1. No campo adjacente, especifique um valor válido para a propriedade CSS3 especificada. Por exemplo, **3 pixels de preto sólido**.
1. Clique em **Adicionar Item** para especificar outra propriedade e seu valor.
1. Clique em **Visualizar** para que você possa ver as alterações no formulário.
1. Siga uma das seguintes opções:
   * Confirme as alterações clicando em **OK**
   * Saia da caixa de diálogo sem nenhuma alteração clicando em **Cancelar**.

