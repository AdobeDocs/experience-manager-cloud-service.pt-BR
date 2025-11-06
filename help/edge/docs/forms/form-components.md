---
title: Componentes de bloco de formulário adaptável e suas propriedades
description: Este documento fornece uma visão geral dos componentes de formulário e suas propriedades disponíveis no Edge Delivery Services for AEM Forms.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---

# Componentes de bloco de formulário adaptável e suas propriedades

O Edge Delivery Services para AEM Forms permite criar formulários amigáveis e interativos usando vários componentes. Esses componentes atendem a diferentes tipos de coleção de dados e podem ser facilmente personalizados para atender às suas necessidades específicas.


![Uma planilha de exemplo com alguns componentes e propriedades](/help/edge/assets/sample-form-in-spreadsheet.png)

O bloco Adaptive Forms gera uma [estrutura uniforme do HTML](/help/edge/docs/forms/style-theme-forms.md) para todos os tipos de campos e containers (painéis), garantindo a consistência. Essa estrutura consistente facilita [estilizar um formulário](/help/edge/docs/forms/style-theme-forms.md).

## Componentes disponíveis

Esta é uma visão geral dos componentes disponíveis:

### Campos de entrada

- Todos os [tipos de entrada](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/input#input_types) e [textarea](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/textarea) válidos do HTML5. Por exemplo, botão, caixa de seleção, cor, data, data-hora-local, email, arquivo, oculto, imagem, mês, número, senha, rádio, intervalo, redefinição, enviar, tel, texto, hora, url e semana.

### Controles de seleção

- [Grupos de caixas de seleção](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): para selecionar várias opções.
- [Grupos de opções](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): para selecionar uma única opção de um grupo.
- [Menus suspensos](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): para exibir um menu de opções. Por exemplo, a caixa suspensa.

### Contêineres

- Painéis/Contêineres: para agrupar elementos de formulário relacionados para obter uma melhor organização. É uma combinação do [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) e [legend](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


## Propriedades dos componentes

Cada componente de formulário vem com várias propriedades que permitem controlar seu comportamento e aparência. Estas são as propriedades compatíveis com componentes de bloco adaptáveis do Forms:


| Propriedade | Componentes aplicáveis | Detalhes |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Todos | Especifica o tipo do componente. Essa propriedade determina o comportamento e a aparência do campo de entrada. Por exemplo, para entradas de texto, o tipo pode ser &quot;texto&quot;, &quot;email&quot; para entradas de email, &quot;senha&quot; para entradas de senha. O Bloco Forms Adaptável oferece suporte a <a href="https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/input#input_types">todos os tipos de entrada HTML5 válidos</a>, <a href="https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a> e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> como tipo. |
| Nome | Todos | Identifica o componente para envio de formulário. O atributo name é usado quando os dados de formulário são enviados ao servidor, associando a entrada do usuário a um campo específico. |
| Rótulo | Todos | Fornece informações contextuais aos usuários. O rótulo é o texto exibido ao lado do componente, fornecendo aos usuários orientação sobre quais informações inserir. |
| Valor | Texto, Senha, Email, Número, Intervalo, Data e suas variantes (datetime-local, mês, semana, hora), Caixa de seleção, Rádio, Oculto, Enviar, Botão | Especifica o valor inicial do componente. Para entradas de texto, área de texto e elementos de seleção, este é o texto ou opção padrão exibido. Para componentes de rádio e caixa de seleção, este é o valor/dado enviado quando eles são selecionados. O atributo value é opcional, mas deve ser considerado obrigatório para entradas de rádio e caixa de seleção. |
| Espaço reservado | Texto, Telefone, Email, Senha, Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Oferece dicas para a entrada esperada. O atributo de espaço reservado fornece uma breve dica que descreve o valor esperado do campo de entrada. Ele desaparece assim que o usuário começa a digitar. |
| Descrição | Todos | Fornece informações adicionais sobre o componente e serve como texto de ajuda. O campo de descrição permite obter mais explicações sobre a finalidade ou instruções para preencher o componente. Ele auxilia os usuários na compreensão do contexto do campo de entrada. |
| Visível | Todos | Controla a visibilidade inicial. O atributo visible é uma propriedade booleana que determina se o componente está inicialmente visível ou oculto quando o formulário é carregado. Se definido como true, o campo é exibido; caso contrário, ele fica oculto. |
| Obrigatório | Texto, Tel, Email, Senha, Data e suas variantes (data e hora local, mês, semana, hora), Número, Caixa de seleção, Rádio, Arquivo, Selecionar (lista suspensa), Textarea | Indica se o campo deve ser preenchido antes do envio. O atributo obrigatório é uma propriedade booleana usada para especificar se o usuário deve fornecer entrada para o campo antes de enviar o formulário. |
| Mín | Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Especifica o valor mínimo permitido. O atributo min define o valor mínimo que o usuário pode inserir no campo. Por exemplo, para entradas de número, define o número mais baixo aceitável. |
| Max | Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Especifica o valor máximo permitido. O atributo max define o valor máximo que o usuário pode inserir no campo. Por exemplo, para entradas de data, define a data mais alta aceitável. |
| Aceitar | Arquivo | Define os tipos de arquivos permitidos. O atributo accept é uma lista separada por vírgulas de especificadores de tipo de arquivo exclusivo que restringem os tipos de arquivos que os usuários podem selecionar em um campo de entrada de arquivo. |
| Múltiplas | Arquivo | Permite várias seleções. O atributo multiple é uma propriedade booleana usada com campos de entrada de arquivo. Quando definido como verdadeiro, permite que os usuários selecionem mais de um arquivo. |
| Opções | Lista suspensa | Especifica opções para menus suspensos. A propriedade options é uma lista separada por vírgulas de opções para menus suspensos que define as opções selecionáveis exibidas para o usuário. |
| Marcado | Caixa de seleção, Rádio | Determina se o campo é selecionado por padrão. O atributo marcado é uma propriedade booleana usada com entradas de caixa de seleção e rádio. Quando definido como true, indica que o campo é selecionado por padrão quando o formulário é carregado. |
| Fieldset | Todos | Agrupa campos para criar seções visualmente distintas em um formulário. O elemento fieldset agrupa campos relacionados em um formulário, separando-os visualmente para melhorar a organização e a experiência do usuário. </br> Para organizar um conjunto de campos em um conjunto de campos, use a propriedade `fieldset` e especifique seu atributo de nome. No exemplo abaixo, demonstramos como os botões de opção são encapsulados em um único conjunto de campo para melhorar a organização. ![Exemplo de conjunto de campos](/help/edge/assets/fieldset-example.png) |
| Repetível | Todos | Uma propriedade booleana para `fieldset` indicando que um conjunto de campos específico pode ser repetido por `Min` e `Max` vezes especificados. A propriedade `Min` deve ser definida como 1 ou superior, não defina a propriedade `Min` como 0. |
| Expressão visível | Todos | Uma expressão visível se refere a uma fórmula de planilha, indicada pela tag &#39;=&#39;, usada para controlar a visibilidade de um campo. Nesta fórmula, somente a propriedade value de outros campos pode ser empregada, permitindo o gerenciamento direto da visibilidade do campo dentro do sistema. |
| Expressão de valor | Todos | Uma expressão de valor refere-se a uma fórmula de planilha, indicada pela tag &#39;=&#39;, usada para controlar o valor de um campo. Nesta fórmula, somente a propriedade value de outros campos pode ser empregada, permitindo o gerenciamento direto do valor do campo no sistema. |
