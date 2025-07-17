---
title: Criação de estilos CSS para formulários HTML5
description: Saiba como alterar a aparência dos formulários HTML5 modificando a classe CSS associada ao elemento de formulário HTML.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms,Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 2%

---

# Criação de estilos CSS para formulários HTML5 {#creating-css-styles-for-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

A representação HTML5 de um modelo de formulário baseado em XFA consiste em vários elementos HTML. Esses elementos são organizados em uma ordem. Cada elemento tem classes CSS bem definidas. Você pode usar essas classes CSS para selecionar e alterar a aparência de um elemento.

>[!NOTE]
>
>Nas classes CSS, não altere o valor da largura, altura, espessura da borda, superior, esquerda, direita, inferior, preenchimento, margem e outros atributos de posição e tamanho. Qualquer alteração nos atributos de posição e tamanho traz alterações ao layout do formulário.

## Classes CSS  para elementos  {#css-classes-nbsp-for-elements-nbsp}

Cada elemento contém classes CSS bem definidas. Você pode modificar essas classes para alterar a aparência de um elemento. Todos os elementos, exceto os elementos field e draw, têm duas classes CSS - classe Type e classe Name.

* A classe **Type** representa o tipo do campo XFA. Você pode substituir a classe `type` para modificar os estilos de todos os elementos de um tipo específico.

* A **classe Name** corresponde ao nome do campo XFA. Você pode substituir a classe `name` para modificar e aplicar um estilo personalizado a um elemento.

>[!NOTE]
>
>Alguns elementos XFA não têm um nome. Para alterar os estilos desses componentes, modifique todos os componentes desse tipo específico.

Para as páginas não nomeadas no AEM Forms Designer, as páginas em um formulário HTML5 são nomeadas na ordem crescente de seu número. Por exemplo, para um formulário HTML5 com duas páginas, as páginas são nomeadas como Página1, Página2.

## Elemento de campo {#field-element}

O elemento field contém dois elementos aninhados: widget e legenda.

**Elemento de widget**

O elemento widget contém o elemento da interface do usuário para interação com os usuários. Ele tem três classes CSS:

* **Widget**: todos os widgets têm essa classe.
* **nome**: todos os widgets fornecidos com o AEM contêm a classe de nome de widget. Para widgets personalizados, o desenvolvedor do widget fornece a classe Nome do widget.
* **tipo**: cada widget tem um elemento de interface do usuário. Essa classe define o tipo do elemento da interface do usuário.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Além do tipo e da classe de nome, o componente de campo também contém uma classe CSS adicional denominada **subtype**. Um subtipo identifica que tipo de campo é, por exemplo, NumericField, DateField, TextField. Você pode substituir a classe do subtipo para modificar o estilo de todos os campos do tipo, subtipo.

## Classes CSS para componentes diferentes {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome</strong></td>
  </tr>
  <tr>
   <td>Página</td>
   <td>página</td>
   <td>Nome definido pelo usuário<br /> ou<br /> Página&lt;pageNumber&gt; (padrão)</td>
  </tr>
  <tr>
   <td>Área de conteúdo</td>
   <td>área de conteúdo</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Subformulário</td>
   <td>subformulário</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Grupo de exclusão</td>
   <td>exclgroup</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>desenhar</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>campo</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Legenda</td>
   <td>legenda</td>
   <td>ND</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>O desenvolvedor do widget o define (Para widgets definidos pelo usuário, consulte a tabela na seção seguinte)</td>
  </tr>
 </tbody>
</table>

## Classes CSS para campos diferentes {#css-classes-for-different-fields}

O AEM Forms Designer é compatível com diferentes tipos de campos em um formulário como NumericField, DecimalField e Date Field. Todos esses campos no HTML contêm as classes CSS mencionadas acima. Eles também contêm algumas classes extras, dependendo do tipo de campo.

Cada campo tem um widget associado que representa o elemento da interface do usuário. As classes de cada campo e os widgets associados a cada campo estão listados abaixo.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de campo</strong></td>
   <td><strong>Subtipo</strong></td>
   <td><strong>Nome do widget</strong></td>
   <td><strong>Tipo de widget</strong></td>
   <td><strong>Tag da interface do usuário do HTML</strong></td>
  </tr>
  <tr>
   <td>Botão<br type="_moz" /> </td>
   <td>ND</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=caixa de seleção<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>campo numérico<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Suspenso<br type="_moz" /> </td>
   <td>lista de opções<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>selecionar</td>
  </tr>
  <tr>
   <td>CaixaDeListagem<br type="_moz" /> </td>
   <td>lista de opções<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>CampoNumérico<br type="_moz" /> </td>
   <td>campo numérico<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoSenha<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=senha<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiofield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=rádio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoTexto<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classes CSS para diferentes elementos Draw {#css-classes-for-different-draw-elements}

Você pode inserir elementos de desenho estáticos, como texto e imagens, usando o AEM Forms Designer. Para cada elemento de desenho, uma classe CSS separada é associada a esse elemento. A lista de classes CSS para elementos de desenho está listada abaixo. Cada elemento de desenho tem uma classe de desenho associada a ele.

| **Tipo de Desenho** | **classe CSS** |
|---|---|
| Texto | text |
| Imagem | imagem |
| Retângulo | retângulo |
| Linha | linha |

## Estilizar outras partes do formulário {#styling-other-parts-of-the-form}

Além da aparência dos componentes da interface do usuário no formulário do HTML, você pode alterar o estilo de elementos como Erros em linha, Avisos em linha e campos com erros de validação.

`Styling Inline Errors`

Quando a validação de um campo resulta em erro, um erro em linha é exibido quando o campo está ativo. Para alterar o estilo de erros em linha, substitua a ID de CSS **error-msg**.

`Styling Inline Warnings`

Quando a validação de um campo resulta em um aviso, um aviso em linha é exibido quando o campo está ativo. Para alterar o estilo desses avisos incorporados, substitua a ID de CSS **warning-msg**.

`Styling Fields with Validation Errors`

Quando a validação de um campo falhar, o estilo do widget será alterado. Esta alteração de estilo é feita através da aplicação de uma classe CSS **widgetError** no componente widget. Para modificar o estilo padrão, substitua a classe **widgetError**.
