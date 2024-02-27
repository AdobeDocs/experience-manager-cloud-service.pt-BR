---
description: Este tutorial inclui todas as informações relacionadas aos componentes do EDS.
title: Componentes de formulário compatíveis no bloco de formulário - Tutorial do desenvolvedor
feature: Edge Delivery Services
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 5%

---


# Componentes de HTML compatíveis com a Entrega de borda de bloco de formulário

O AEM Forms Edge Delivery inclui um bloco de formulário. O Bloco de formulário ajuda a criar formulários facilmente para capturar e armazenar dados capturados.

O bloco Formulário é compatível com componentes HTML-5, como texto, email, número, data e muito mais. Ele também suporta elementos de área de texto, seleção e conjunto de campos, e inclui recursos de validação de entrada que são nativos do HTML-5. O Bloco de formulário cria estrutura de HTML uniforme para todos os tipos de campo e containers, garantindo a consistência. Você também [estilo dos tipos de campo](https://adobe-rnd.github.io/form-block/customization/styling_form) usando o `form.css` arquivo.

## Tipos de entrada de HTML 5 compatíveis no bloco de formulário

O Bloco de formulário é compatível com diversos tipos de entrada de HTML 5 e também renderiza formulários criados com os componentes principais de AEM.

Esta é a tabela que descreve como os componentes principais correspondem aos seus tipos de entrada de HTML-5 no Edge Delivery:

<table>
 <tbody>
  <tr>
   <td><b>Componentes principais</b> </td>
   <td><b>tipo de entrada HTML 5</b> </td>
   <td><b>Detalhes</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Container de formulário</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">formulário </td>
   <td> Crie um formulário para capturar entradas de usuário.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Entrada de texto</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Define um campo de entrada de texto de linha única. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Entrada de número</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">número</a></td>
   <td>Permite que o usuário insira um número. Você também pode adicionar validação interna para rejeitar entradas não numéricas. Permite que o usuário insira um número. Você também pode adicionar validação interna para rejeitar entradas não numéricas. Inicialmente, o campo de entrada é exibido como uma entrada de número. Se um usuário aplicar um padrão de exibição, ele será alterado para o texto para permitir que o autor aplique a formatação de número, já que o HTML 5 não é compatível com padrões de exibição. No entanto, quando o usuário clica nele, ele retorna para digitar números.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Seletor de data</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">data </a></td>
   <td> Crie um campo de entrada para inserir uma data. Você tem a opção de inserir a data por meio de uma caixa de texto, que valida a entrada, ou por meio de uma interface dedicada do seletor de datas. Inicialmente, o campo de entrada de data nativo é exibido. Se um usuário aplicar um padrão de exibição, ele será alterado para texto para permitir que o usuário aplique formatação, já que o HTML 5 não é compatível com padrões de exibição. No entanto, quando o usuário clica nele, ele retorna para digitar uma data.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">Anexo de arquivo</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">arquivo</a></td>
   <td> Permite que o usuário escolha um ou mais arquivos do armazenamento do dispositivo. Ela é compatível com validações aprimoradas de entrada de arquivos, como tipos de arquivos aceitos, restrições de tamanho de arquivos e limites mínimos/máximos de seleção de arquivos. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Lista suspensa</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">selecionar</a></td>
   <td> Permite que os usuários selecionem uma ou mais opções de uma lista de opções predefinidas. As opções podem ser do tipo String, Number ou Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Grupos de caixa de seleção</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">caixa de seleção múltipla</a></td>
   <td> Permite que os usuários selecionem uma ou mais opções de uma lista. Várias caixas de seleção são geradas com nomes idênticos, cada um correspondente a um item no enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Grupo de botões de opção</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">vários rádios</a></td>
   <td> Permite que um usuário selecione uma opção de um grupo de opções relacionadas. Vários botões de opção são gerados com nomes idênticos, cada um correspondente a um item no enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Botão</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">botão</a></td>
   <td>Um elemento da interface do usuário que permite aos usuários acionar uma ação quando clicados. </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Painel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset com legenda</a></td>
   <td> Agrupe seções em um formulário, onde um elemento *legend* aninhado adiciona uma legenda para o formulário.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=pt-br">Assistente</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Agrupa seções relacionadas em um formulário. Também controla a organização, suportando opções de exibição para posicioná-los na parte superior ou no lado esquerdo. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Texto</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>Uma tag p marca um parágrafo. No conteúdo visual, os parágrafos são blocos de texto separados por linhas em branco ou uma primeira linha recuada</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Botão Enviar</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">enviar</a></td>
   <td> Um elemento da interface do usuário que permite aos usuários enviar um formulário ao servidor ao clicar em. Se um usuário adicionar uma regra de envio a um botão, ele funcionará como o botão de envio. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Botão de redefinição</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">redefinir</a></td>
   <td>Um elemento da interface que redefine um formulário ao clicar em. Se um usuário adicionar uma regra de redefinição a um botão, ele funcionará como o botão de redefinição. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Entrada de e-mail</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Permite que o usuário insira e edite um endereço de email. Se o usuário adicionar os vários atributos, uma lista de endereços de email poderá ser adicionada ou editada.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Entrada de telefone</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Permite que o usuário insira e edite um número de telefone.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Cabeçalho</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> cabeçalho</a></td>
   <td>Ele inclui conteúdo de introdução, normalmente um grupo de ajudas de introdução ou navegação. Há suporte para isso fora do contêiner de Formulário. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Rodapé</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">rodapé</a></td>
   <td> Contém informações como dados de copyright ou links para documentos relacionados. Há suporte para isso fora do contêiner de Formulário.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=pt-BR">Acordeão<a></td>
   <td><i>Ainda não suportado no bloco de formulário</i></td>
   <td> Permite que o usuário crie seções expansíveis e recolhíveis em um formulário. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=pt-br">Guias horizontais</a></td>
   <td><i>Ainda não suportado no bloco de formulário</i></td>
   <td>Organiza várias seções de um formulário em guias separadas exibidas horizontalmente.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Imagem</a></td>
   <td><i>Ainda não suportado no bloco de formulário</i></td>
   <td> Permite que o usuário inclua imagens em um formulário.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Título</a></td>
   <td><i>Ainda não suportado no bloco de formulário</i></td>
   <td> Refere-se ao texto que aparece na parte superior do formulário. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Interruptor</td>
   <td><i>Ainda não suportado no bloco de formulário</i></td>
   <td> Um botão de alternância de dois estados, que permite ao usuário selecionar entre dois estados, como ativar ou desativar um recurso, configuração ou funcionalidade.</td>
  </tr>
 </tbody>
</table>


