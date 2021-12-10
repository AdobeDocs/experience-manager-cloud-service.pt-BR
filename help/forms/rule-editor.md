---
title: Como usar o editor de regras do Adaptive Forms?
description: O editor de regras adaptável do Forms permite adicionar comportamento dinâmico e criar lógica complexa em formulários sem codificação ou script. Comece a entender uma regra e diretrizes para escolher uma construção de regra. Saiba mais sobre tipos de operadores e eventos disponíveis no editor de regras.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '6340'
ht-degree: 0%

---

# Adicionar regras a um formulário adaptável {#adaptive-forms-rule-editor}

## Visão geral {#overview}

O recurso de editor de regras permite que usuários e desenvolvedores de negócios criem regras em objetos de formulário adaptável. Essas regras definem ações a serem acionadas em objetos de formulário com base em condições predefinidas, entradas de usuário e ações de usuário no formulário. Ajuda a simplificar ainda mais a experiência de preenchimento de formulários, garantindo a precisão e a velocidade.

O editor de regras oferece uma interface de usuário intuitiva e simplificada para gravar regras. O editor de regras oferece um editor visual para todos os usuários.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Algumas das ações principais que podem ser executadas em objetos de formulário adaptável usando regras são:

* Mostrar ou ocultar um objeto
* Ativar ou desativar um objeto
* Definir um valor para um objeto
* Validar o valor de um objeto
* Executar funções para calcular o valor de um objeto
* Chamar um serviço de Modelo de dados de formulário e executar uma operação
* Definir a propriedade de um objeto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Os usuários adicionados ao grupo usuários avançados de formulários podem criar scripts e editar os existentes. Usuários na [!DNL forms-users] podem usar os scripts, mas não podem criar ou editar scripts.

## Como entender uma regra {#understanding-a-rule}

Uma regra é uma combinação de ações e condições. No editor de regras, as ações incluem atividades como ocultar, mostrar, ativar, desativar ou calcular o valor de um objeto em um formulário. As condições são expressões booleanas avaliadas pela execução de verificações e operações no estado, valor ou propriedade de um objeto de formulário. As ações são executadas com base no valor ( `True` ou `False`) retornado avaliando uma condição.

O editor de regras fornece um conjunto de tipos de regras predefinidos, como Quando, Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar para ajudar você a gravar regras. Cada tipo de regra permite definir condições e ações em uma regra. O documento explica mais detalhadamente cada tipo de regra.

Uma regra geralmente segue uma das seguintes construções:

**Condição-Ação** Nesta construção, uma regra define primeiro uma condição seguida de uma ação a ser acionada. A construção é comparável à declaração if-then em linguagens de programação.

No editor de regras, a variável **When** o tipo de regra impõe a construção de condição-ação.

**Condição de ação** Nesta construção, uma regra define primeiro uma ação a ser acionada, seguida de condições para avaliação. Outra variação dessa construção é a ação alternativa de condição de ação, que também define uma ação alternativa a ser acionada se a condição retornar Falso.

Os tipos de regras Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar no editor de regras impõem a construção da regra de condição de ação. Por padrão, a ação alternativa para Mostrar é Ocultar e para Ativar é Desativar, e do contrário. Não é possível alterar a ação alternativa padrão.

>[!NOTE]
>
>Os tipos de regras disponíveis, incluindo condições e ações definidas no editor de regras, também dependem do tipo de objeto de formulário no qual você está criando uma regra. O editor de regras exibe apenas tipos de regras válidos e opções para escrever condições e declarações de ação para um tipo de objeto de formulário específico. Por exemplo, você não vê os tipos de regras Validar, Definir valor de, Ativar e Desativar para um objeto de painel.

Para obter mais informações sobre tipos de regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Diretrizes para escolher uma construção de regra {#guidelines-for-choosing-a-rule-construct}

Embora seja possível obter a maioria dos casos de uso usando qualquer construção de regra, veja a seguir algumas diretrizes para escolher uma construção em vez de outra. Para obter mais informações sobre as regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Uma regra típica do polegar ao criar uma regra é pensar nela no contexto do objeto no qual você está escrevendo uma regra. Considere que deseja ocultar ou mostrar o campo B com base no valor que um usuário especifica no campo A. Nesse caso, você está avaliando uma condição no campo A e, com base no valor retornado, está acionando uma ação no campo B.

   Portanto, se estiver escrevendo uma regra no campo B (o objeto no qual você está avaliando uma condição), use a construção de condição-ação ou o tipo de regra Quando. Da mesma forma, use o tipo de regra de construção da condição de ação ou Mostrar ou Ocultar no campo A.

* Às vezes, você deve executar várias ações com base em uma condição. Nesses casos, é recomendável usar a construção de condição-ação. Nesta construção, você pode avaliar uma condição uma vez e especificar várias declarações de ação.

   Por exemplo, para ocultar os campos B, C e D com base na condição que verifica o valor que um usuário especifica no campo A, escreva uma regra com construção de condição-ação ou Quando a regra tipo no campo A e especifique ações para controlar a visibilidade dos campos B, C e D. Caso contrário, você precisará de três regras separadas nos campos B, C e D, onde cada regra verifica a condição e mostra ou oculta o respectivo campo. Neste exemplo, é mais eficiente gravar o tipo de regra Quando em um objeto em vez de Mostrar ou Ocultar tipo de regra em três objetos.

* Para acionar uma ação com base em várias condições, é recomendável usar a construção de condição de ação. Por exemplo, para mostrar e ocultar o campo A avaliando as condições nos campos B, C e D, use o tipo de regra Mostrar ou Ocultar no campo A.
* Use condição-ação ou construção de condição de ação se a regra contiver uma ação para uma condição.
* Se uma regra verificar uma condição e executar uma ação imediatamente após fornecer um valor em um campo ou sair de um campo, é recomendável gravar uma regra com construção de condição-ação ou o tipo de regra Quando no campo em que a condição é avaliada.
* A condição na regra Quando é avaliada quando um usuário altera o valor do objeto no qual a regra Quando é aplicada. No entanto, se desejar que a ação seja acionada quando o valor for alterado no lado do servidor, como para pré-preencher o valor, é recomendável gravar uma regra Quando que acione a ação quando o campo for inicializado.
* Ao escrever regras para objetos de listas suspensas, botões de opção ou caixas de seleção, as opções ou valores desses objetos de formulário no formulário são preenchidos previamente no editor de regras.

## Tipos de operador e eventos disponíveis no editor de regras {#available-operator-types-and-events-in-rule-editor}

O editor de regras fornece os operadores lógicos e eventos a seguir que podem ser usados para criar regras.

* **É Igual A**
* **Is Not Equal To**
* **Começa com**
* **Termina com**
* **Contém**
* **Está vazio**
* **Não está vazio**
* **Selecionou:** Retorna verdadeiro quando o usuário seleciona uma opção específica para uma caixa de seleção, lista suspensa e um botão de opção.
* **É Inicializado (evento):** Retorna true quando um objeto de formulário é renderizado no navegador.
* **É alterado (evento):** Retorna true quando o usuário altera o valor inserido ou a opção selecionada para um objeto de formulário.
* **Navegação (evento):** Retorna true quando o usuário clica em um objeto de navegação. Os objetos de navegação são usados para se mover entre painéis.
* **Conclusão da etapa (evento):** Retorna true quando uma etapa de uma regra é concluída.
* **Envio(evento) bem-sucedido:** Retorna true no envio bem-sucedido de dados para um modelo de dados de formulário.
* **Erro no envio (evento):**  Retorna true no envio malsucedido de dados para um modelo de dados de formulário.

## Tipos de regras disponíveis no editor de regras {#available-rule-types-in-rule-editor}

O editor de regras fornece um conjunto de tipos de regras predefinidos que podem ser usados para gravar regras. Vamos analisar cada tipo de regra detalhadamente. Para obter mais informações sobre como escrever regras no editor de regras, consulte [Regras de gravação](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando] {#whenruletype}

O **[!UICONTROL When]** o tipo de regra segue **ação-condição-alternativa** construção de regra, ou às vezes, apenas o **condição-ação** construir. Nesse tipo de regra, primeiro especifique uma condição para avaliação seguida de uma ação para acionar se a condição for atendida ( `True`). Ao usar o tipo de regra Quando , você pode usar vários operadores AND e OR para criar [expressões aninhadas](#nestedexpressions).

Usando o tipo de regra Quando , é possível avaliar uma condição em um objeto de formulário e executar ações em um ou mais objetos.

Em palavras simples, uma regra Quando típica é estruturada da seguinte maneira:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Ação 2 sobre o objeto B; E a ação 3 relativa ao objeto C;

_

Quando você tem um componente de vários valores, como botões de opção ou lista, enquanto cria uma regra para esse componente, as opções são recuperadas automaticamente e disponibilizadas para o criador da regra. Não é necessário digitar os valores de opção novamente.

Por exemplo, uma lista tem quatro opções: Vermelho, Azul, Verde e Amarelo. Ao criar a regra, as opções (botões de opção) são recuperadas automaticamente e disponibilizadas para o criador da regra da seguinte maneira:

![Opções de exibição de vários valores](assets/multivaluefcdisplaysoptions.png)

Ao escrever uma regra de Quando, é possível acionar a ação Limpar valor de. A ação Limpar valor da apaga o valor do objeto especificado. Ter Valor Limpo de como uma opção na instrução Quando permite criar condições complexas com vários campos.

![Limpar valor de](assets/clearvalueof.png)

**[!UICONTROL Ocultar]** Oculta o objeto especificado.

**[!UICONTROL Mostrar]** Mostra o objeto especificado.

**[!UICONTROL Habilitar]** Ativa o objeto especificado.

**[!UICONTROL Desativar]** Desativa o objeto especificado.

**[!UICONTROL Chamar serviço]** Chama um serviço configurado em um modelo de dados de formulário. Quando você escolhe a operação Invoke Service , um campo é exibido. Ao tocar no campo , ele exibe todos os serviços configurados em todos os modelos de dados de formulário em seu [!DNL Experience Manager] instância. Ao escolher um serviço de Modelo de dados de formulário, mais campos são exibidos, onde é possível mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado. Consulte a regra de exemplo para chamar serviços do Modelo de dados de formulário.

Além do serviço do Modelo de dados de formulário, você pode especificar um URL WSDL direto para chamar um serviço da Web. No entanto, um serviço de Modelo de dados de formulário tem muitos benefícios e a abordagem recomendada para invocar um serviço.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [[!DNL Experience Manager Forms] Integração de dados](data-integration.md).

**[!UICONTROL Definir valor de]** Calcula e define o valor do objeto especificado. Você pode definir o valor do objeto como uma string, o valor de outro objeto, o valor calculado usando a expressão ou função matemática, o valor de uma propriedade de um objeto ou o valor de saída de um serviço de Modelo de dados de formulário configurado. Ao escolher a opção serviço da Web, ele exibe todos os serviços configurados em todos os modelos de dados de formulário em seu [!DNL Experience Manager] instância. Ao escolher um serviço de Modelo de dados de formulário, mais campos são exibidos, onde é possível mapear objetos de formulário com parâmetros de entrada e saída para o serviço especificado.

Para obter mais informações sobre como configurar serviços no modelo de dados de formulário, consulte [[!DNL Experience Manager Forms] Integração de dados](data-integration.md).

O **[!UICONTROL Definir propriedade]** o tipo de regra permite definir o valor de uma propriedade do objeto especificado com base em uma ação de condição.

Ele permite definir regras para adicionar caixas de seleção dinamicamente ao formulário adaptável. É possível usar uma função personalizada, um objeto de formulário ou uma propriedade de objeto para definir uma regra.

![Definir Propriedade](assets/set_property_rule_new.png)

Para definir uma regra baseada em uma função personalizada, selecione **[!UICONTROL Saída de função]** na lista suspensa e arraste e solte uma função personalizada do **[!UICONTROL Funções]** guia . Se a ação de condição for atendida, o número de caixas de seleção definido na função personalizada será adicionado ao Formulário adaptável.

Para definir uma regra baseada em um objeto de formulário, selecione **[!UICONTROL Objeto de formulário]** na lista suspensa e arraste e solte um objeto de formulário da **[!UICONTROL Objetos de formulário]** guia . Se a ação de condição for atendida, o número de caixas de seleção definidas no objeto de formulário será adicionado ao Formulário adaptável.

Uma regra Definir propriedade com base em uma propriedade de objeto permite adicionar o número de caixas de seleção em um formulário adaptável com base em outra propriedade de objeto incluída no formulário adaptável.

A figura a seguir descreve um exemplo de adição dinâmica de caixas de seleção com base no número de listas suspensas no Formulário adaptável:

![Propriedade do objeto](assets/object_property_set_property_new.png)

**[!UICONTROL Valor Claro De]** Apaga o valor do objeto especificado.

**[!UICONTROL Definir foco]** Define o foco no objeto especificado.

**[!UICONTROL Salvar formulário]** Salva o formulário.

**[!UICONTROL Enviar Forms]** Envia o formulário.

**[!UICONTROL Redefinir formulário]** Redefine o formulário.

**[!UICONTROL Validar formulário]** Valida o formulário.

**[!UICONTROL Adicionar instância]** Adiciona uma instância do painel repetitivo ou linha de tabela especificada.

**[!UICONTROL Remover instância]** Remove uma instância do painel ou linha de tabela repetível especificado.

**[!UICONTROL Navegar para]** Navega para outro <!--Interactive Communications,--> Forms adaptável, outros ativos, como imagens ou fragmentos de documento, ou um URL externo. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL Definir valor de] {#set-value-of}

O **[!UICONTROL Definir valor de]** o tipo de regra permite definir o valor de um objeto de formulário, dependendo se a condição especificada é atendida ou não. O valor pode ser definido como um valor de outro objeto, uma string literal, um valor derivado de uma expressão matemática ou uma função, um valor de uma propriedade de outro objeto ou a saída de um serviço do Modelo de dados de formulário. Da mesma forma, é possível verificar uma condição em um componente, string, propriedade ou valores derivados de uma função ou expressão matemática.

O **Definir Valor De** o tipo de regra não está disponível para todos os objetos de formulário, como painéis e botões da barra de ferramentas. Uma regra Definir valor de conjunto padrão tem a seguinte estrutura:

Defina o valor do Objeto A como:

(string ABC) OU (propriedade de objeto X do Objeto C) OU (valor de uma função) OU (valor de uma expressão matemática) OU (valor de saída de um serviço de modelo de dados ou serviço da Web);

Quando (opcional):

(Condição 1 E Condição 2 E Condição 3) é TRUE;

O exemplo a seguir pega o valor em `dependentid` como entrada e define o valor da variável `Relation` para a saída do `Relation` argumento do `getDependent` Serviço de Modelo de dados de formulário.

![Set-value-web-service](assets/set-value-web-service.png)

Exemplo de regra Definir valor usando o serviço Modelo de dados de formulário

>[!NOTE]
>
>Além disso, é possível usar a opção Definir valor da regra para preencher todos os valores em um componente de lista suspensa da saída de um serviço do Modelo de dados de formulário ou de um serviço da Web. No entanto, verifique se o argumento de saída escolhido é de um tipo de matriz. Todos os valores retornados em uma matriz ficam disponíveis na lista suspensa especificada.

### [!UICONTROL Mostrar] {#show}

Usar o **[!UICONTROL Mostrar]** tipo de regra , é possível gravar uma regra para mostrar ou ocultar um objeto de formulário com base em se uma condição é atendida ou não. O tipo de regra Mostrar também aciona a ação Ocultar caso a condição não seja atendida ou retorne `False`.

Uma regra de Mostrar típica é estruturada da seguinte maneira:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Ocultar] {#hide}

Semelhante ao tipo de regra Mostrar , você pode usar o **[!UICONTROL Ocultar]** tipo de regra para mostrar ou ocultar um objeto de formulário com base em se uma condição é atendida ou não. O tipo de regra Ocultar também aciona a ação Mostrar caso a condição não seja atendida ou retorne `False`.

Uma regra de Ocultar típica é estruturada da seguinte maneira:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Ativar] {#enable}

O **[!UICONTROL Habilitar]** o tipo de regra permite habilitar ou desabilitar um objeto de formulário com base em se uma condição é atendida ou não. O tipo de regra Ativar também aciona a ação Desativar caso a condição não seja atendida ou retorne `False`.

Uma regra típica de Ativar está estruturada da seguinte maneira:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Desativar] {#disable}

Semelhante ao tipo de regra Ativar , a variável **[!UICONTROL Desativar]** o tipo de regra permite habilitar ou desabilitar um objeto de formulário com base em se uma condição é atendida ou não. O tipo de regra Desativar também aciona a ação Ativar caso a condição não seja atendida ou retorne `False`.

Uma regra de desativação típica é estruturada da seguinte maneira:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Validar] {#validate}

O **[!UICONTROL Validar]** o tipo de regra valida o valor em um campo usando uma expressão. Por exemplo, você pode gravar uma expressão para verificar se a caixa de texto para especificar o nome não contém caracteres especiais ou números.

Uma regra Validar típica está estruturada da seguinte maneira:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se o valor especificado não estiver em conformidade com a regra Validar, você poderá exibir uma mensagem de validação para o usuário. Você pode especificar a mensagem no **[!UICONTROL Mensagem de validação de script]** nas propriedades do componente na barra lateral.

![Validação de script](assets/script-validation.png)

### [!UICONTROL Definir Opções de] {#setoptionsof}

O **[!UICONTROL Definir Opções de]** o tipo de regra permite definir regras para adicionar caixas de seleção dinamicamente ao formulário adaptável. Você pode usar um Modelo de dados de formulário ou uma função personalizada para definir a regra.

Para definir uma regra baseada em uma função personalizada, selecione **[!UICONTROL Saída de função]** na lista suspensa e arraste e solte uma função personalizada do **[!UICONTROL Funções]** guia . O número de caixas de seleção definidas na função personalizada é adicionado ao Formulário adaptável.

![Funções personalizadas](assets/custom_functions_set_options_new.png)

Para criar uma função personalizada, consulte [funções personalizadas no editor de regras](#custom-functions).

Para definir uma regra baseada em um modelo de dados de formulário:

1. Selecionar **[!UICONTROL Saída de serviço]** na lista suspensa.
1. Selecione o objeto de modelo de dados.
1. Selecione uma propriedade de objeto de modelo de dados no **[!UICONTROL Exibir valor]** lista suspensa. O número de caixas de seleção no formulário adaptável é derivado do número de instâncias definidas para essa propriedade no banco de dados.
1. Selecione uma propriedade de objeto de modelo de dados no **[!UICONTROL Salvar valor]** lista suspensa.

![Opções de conjunto do FDM](assets/fdm_set_options_new.png)

## Entendendo a interface do usuário do editor de regras {#understanding-the-rule-editor-user-interface}

O editor de regras fornece uma interface de usuário abrangente, mas simples, para gravar e gerenciar regras. Você pode iniciar a interface do usuário do editor de regras a partir de um formulário adaptável no modo de criação.

Para iniciar a interface do usuário do editor de regras:

1. Abra um formulário adaptável no modo de criação.
1. Toque no objeto de formulário para o qual você deseja gravar uma regra e, na Barra de ferramentas do componente, toque em ![editar regras](assets/edit-rules-icon.svg). A interface do usuário do editor de regras é exibida.

   ![criar regras](assets/create-rules.png)

   Todas as regras existentes nos objetos de formulário selecionados são listadas nesta exibição. Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](rule-editor.md#p-manage-rules-p).

1. Toque **[!UICONTROL Criar]** para escrever uma nova regra. O editor visual da interface do usuário do editor de regras é aberto por padrão quando você inicia o editor de regras pela primeira vez.

   ![Interface do usuário do editor de regras](assets/rule-editor-ui.png)

Vamos analisar cada componente da interface do usuário do editor de regras em detalhes.

### A. Exibição da regra de componente {#a-component-rule-display}

Exibe o título do objeto de formulário adaptável pelo qual você iniciou o editor de regras e o tipo de regra selecionado no momento. No exemplo acima, o editor de regras é iniciado a partir de um objeto de Formulário adaptável intitulado Salário e o tipo de regra selecionado é Quando.

### B. Objetos e funções de formulário {#b-form-objects-and-functions-br}

O painel à esquerda na interface do usuário do editor de regras inclui duas guias: **[!UICONTROL Objetos do Forms]** e **[!UICONTROL Funções]**.

A guia Objetos de formulário mostra uma exibição hierárquica de todos os objetos contidos no Formulário adaptável. Ele exibe o título e o tipo dos objetos. Ao gravar uma regra, é possível arrastar e soltar objetos de formulário no editor de regras. Ao criar ou editar uma regra ao arrastar e soltar um objeto ou função em um espaço reservado, o espaço reservado utiliza automaticamente o tipo de valor apropriado.

Os objetos de formulário que têm uma ou mais regras válidas aplicadas são marcados com um ponto verde. Se qualquer regra aplicada a um objeto de formulário for inválida, o objeto de formulário será marcado com um ponto Amarelo.

A guia Funções inclui um conjunto de funções incorporadas, como Soma, Mín., Máx. de, Média, Número de e Validar formulário. Você pode usar essas funções para calcular valores em painéis repetitivos e linhas de tabela e usá-los em instruções de ação e condição ao gravar regras. No entanto, você pode criar [funções personalizadas](#custom-functions) também.

![A guia Funções](assets/functions.png)

>[!NOTE]
>
>É possível realizar uma pesquisa de texto em objetos e nomes de funções e títulos nas guias Objetos e Funções do Forms .

Na árvore esquerda dos objetos de formulário, é possível tocar nos objetos de formulário para exibir as regras aplicadas a cada um dos objetos. Além de poder navegar pelas regras dos vários objetos de formulário, também é possível copiar e colar regras entre os objetos de formulário. Para obter mais informações, consulte [Copiar e colar regras](rule-editor.md#p-copy-paste-rules-p).

### C. Objetos de formulário e alternância de funções {#c-form-objects-and-functions-toggle-br}

O botão de alternância, quando tocado, alterna os objetos de formulário e o painel de funções.

### D. Editor de regras visuais {#visual-rule-editor}

O editor de regras visuais é a área no modo de editor visual da interface do usuário do editor de regras, onde você grava regras. Ela permite selecionar um tipo de regra e definir condições e ações de acordo com isso. Ao definir condições e ações em uma regra, você pode arrastar e soltar objetos e funções de formulário do painel Objetos de formulário e Funções .

Para obter mais informações sobre o uso do editor de regras visuais, consulte [Regras de gravação](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Botões Concluir e cancelar {#done-and-cancel-buttons}

O **[!UICONTROL Concluído]** é usado para salvar uma regra. Você pode salvar uma regra incompleta. No entanto, incompletos são inválidos e não são executados. Regras salvas em um objeto de formulário são listadas quando você inicia o editor de regras na próxima vez no mesmo objeto de formulário. Você pode gerenciar regras existentes nessa visualização. Para obter mais informações, consulte [Gerenciar regras](rule-editor.md#p-manage-rules-p).

O **[!UICONTROL Cancelar]** descarta qualquer alteração feita em uma regra e fecha o editor de regras.

## Regras de gravação {#write-rules}

Você pode escrever regras usando o editor de regras visuais &lt;!>— ou o editor de códigos>. Ao iniciar o editor de regras pela primeira vez, ele é aberto no modo de editor visual. Você pode alternar para o modo do editor de códigos e para as regras de gravação. No entanto, se você gravar ou modificar uma regra no editor de códigos, não poderá alternar para o editor visual dessa regra, a menos que limpe o editor de códigos. Na próxima vez que você iniciar o editor de regras, ele será aberto no modo usado por último para criar a regra.

Vamos primeiro ver como escrever regras usando o editor visual.

### Uso do editor visual {#using-visual-editor}

Vamos entender como criar uma regra no editor visual usando o seguinte formulário de exemplo.

![Criar-exemplo de regra](assets/create-rule-example.png)

A seção Requisitos de Empréstimo no formulário de pedido de empréstimo de exemplo requer que os requerentes especifiquem o seu estado civil, salário e, se casados, o salário do cônjuge. Com base nos dados de entrada do usuário, a regra calcula o montante de elegibilidade do empréstimo e é exibida no campo Elegibilidade do empréstimo. Aplique as seguintes regras para implementar o cenário:

* O campo Salário do Cônjuge é mostrado somente quando o Status Marital é Casado.
* O valor de elegibilidade do empréstimo é 50% do salário total.

Para gravar regras, execute as seguintes etapas:

1. Primeiro, escreva a regra para controlar a visibilidade do campo Salário do Cônjuge com base na opção que o usuário seleciona para o botão de opção Status Marital .

   Abra o formulário do aplicativo de empréstimo no modo de criação. Toque no **[!UICONTROL Estado civil]** componente e toque ![editar regras](assets/edit-rules-icon.svg). Em seguida, toque em **[!UICONTROL Criar]** para iniciar o editor de regras.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Ao iniciar o editor de regras, a regra Quando é selecionada por padrão. Além disso, o objeto de formulário (nesse caso, Status civil) de onde o editor de regras foi iniciado é especificado na instrução Quando.

   Embora não possa alterar ou modificar o objeto selecionado, você pode usar o menu suspenso de regras, como mostrado abaixo, para selecionar outro tipo de regra. Para criar uma regra em outro objeto, toque em Cancelar para sair do editor de regras e iniciá-la novamente a partir do objeto de formulário desejado.

1. Toque **[!UICONTROL Selecionar Estado]** e selecione **[!UICONTROL é igual a]**. O **[!UICONTROL Digite uma string]** é exibido.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   No botão de opção Estado civil, **[!UICONTROL Casado]** e **[!UICONTROL Único]** opções atribuídas **0** e **1** , respectivamente. Você pode verificar os valores atribuídos na guia Título da caixa de diálogo Editar botão de opção, como mostrado abaixo.

   ![Valores de botões de opção do editor de regras](assets/radio-button-values.png)

1. No **[!UICONTROL Digite uma string]** na regra, especifique **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Você definiu a condição como `When Marital Status is equal to Married`. Em seguida, defina a ação a ser executada se essa condição for True.

1. Na instrução Then , selecione **[!UICONTROL Mostrar]** do **[!UICONTROL Selecionar ação]** lista suspensa.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Arraste e solte a **[!UICONTROL Salário do Cônjuge]** na guia Objetos de formulário na **[!UICONTROL Solte o objeto ou selecione aqui]** campo. Como alternativa, toque no **[!UICONTROL Solte o objeto ou selecione aqui]** e selecione o **[!UICONTROL Salário do Cônjuge]** no menu pop-up, que lista todos os objetos de formulário no formulário.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   A regra aparece da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. Toque **[!UICONTROL Concluído]** para salvar a regra.

1. Repita as etapas de 1 a 5 para definir outra regra para ocultar o campo Salário do Cônjuge se o Status conjugal for Único. A regra aparece da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >Como alternativa, você pode escrever uma regra Mostrar no campo Salário do Cônjuge, em vez de duas regras Quando no campo Status do Marital , para implementar o mesmo comportamento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Em seguida, escreva uma regra para calcular a quantia de elegibilidade do empréstimo, que é 50% do salário total, e exiba-a no campo Loan Eligibility . Para alcançar esse resultado, crie **[!UICONTROL Definir valor de]** regras relativas ao campo Elegibilidade do empréstimo.

   No modo de criação, toque no **[!UICONTROL Elegibilidade do empréstimo]** campo e toque em ![editar regras](assets/edit-rules-icon.svg). Em seguida, toque em **[!UICONTROL Criar]** para iniciar o editor de regras.

1. Selecionar **[!UICONTROL Definir Valor De]** na lista suspensa de regras.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Toque **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão matemática]**. Um campo para gravar expressão matemática é aberto.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. No campo de expressão:

   * Selecione ou arraste para soltar a partir da guia Objeto do Forms **[!UICONTROL Salário]** no primeiro **[!UICONTROL Solte o objeto ou selecione aqui]** campo.

   * Selecionar **[!UICONTROL Plus]** do **[!UICONTROL Selecionar operador]** campo.

   * Selecione ou arraste para soltar a partir da guia Objeto do Forms **[!UICONTROL Salário do Cônjuge]** no outro **[!UICONTROL Solte o objeto ou selecione aqui]** campo.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Em seguida, toque na área realçada ao redor do campo de expressão e toque em **[!UICONTROL Estender expressão]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   No campo de expressão estendida, selecione **[!UICONTROL dividido por]** do **[!UICONTROL Selecionar operador]** e **[!UICONTROL Número]** do **[!UICONTROL Selecionar Opção]** campo. Em seguida, especifique **[!UICONTROL 2]** no campo número.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Você pode criar expressões complexas usando componentes, funções, expressões matemáticas e valores de propriedade no campo Selecionar opção .

   Em seguida, crie uma condição, que quando retornar True, a expressão será executada.

1. Toque **[!UICONTROL Adicionar condição]** para adicionar uma instrução When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Na instrução Quando:

   * Selecione ou arraste para soltar a partir da guia Objeto do Forms **[!UICONTROL Estado civil]** no primeiro **[!UICONTROL Solte o objeto ou selecione aqui]** campo.

   * Selecionar **[!UICONTROL é igual a]** do **[!UICONTROL Selecionar operador]** campo.

   * Selecione String no outro **[!UICONTROL Solte o objeto ou selecione aqui]** e especifique **[!UICONTROL Casado]** no **[!UICONTROL Digite uma string]** campo.

   A regra finalmente aparece da seguinte maneira no editor de regras.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. Toque **[!UICONTROL Concluído]**. Salva a regra.

1. Repita as etapas de 7 a 14 para definir outra regra para calcular a elegibilidade do empréstimo se o Status civil for Único. A regra aparece da seguinte maneira no editor de regras.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>Como alternativa, você pode usar a regra Definir Valor de para calcular a qualificação do empréstimo na regra Quando criada para mostrar e ocultar o campo Salário do Cônjuge. A regra combinada resultante quando o Status Marital é Único aparece da seguinte maneira no editor de regras.
>
>Da mesma forma, você pode escrever uma regra combinada para controlar a visibilidade do campo Salário do Cônjuge e calcular a qualificação do empréstimo quando o Status do Capital estiver Casado.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### Funções personalizadas no editor de regras {#custom-functions}

Além das funções prontas para uso como *Soma de* que estão listadas em Saída das funções, você pode gravar funções personalizadas que precisa com frequência. Certifique-se de que a função gravada seja acompanhada pela função `jsdoc` acima.

Acompanhamento `jsdoc` é obrigatório:

* Se você quiser configuração e descrição personalizadas
* Como há várias maneiras de declarar uma função no `JavaScript,` Os comentários e permitem que você acompanhe as funções.

Para obter mais informações, consulte [jsdoc.app](https://jsdoc.app/).

Suportado `jsdoc` tags:

* **Privado**
Sintaxe: Uma função privada não é incluída como uma função personalizada.`@private`
Uma função privada não é incluída como uma função personalizada.

* **Nome**
Sintaxe: Alternativamente `@name funcName <Function Name>`
Alternativamente `,` você pode usar: `@function funcName <Function Name>` **ou** `@func` `funcName <Function Name>`.
   `funcName` é o nome da função (sem espaços permitidos).
   `<Function Name>` é o nome de exibição da função.

* **membro**
Sintaxe: Anexa um namespace à função .`@memberof namespace`
Anexa um namespace à função .

* **Parâmetro**
Sintaxe: Como alternativa, você pode usar: `@param {type} name <Parameter Description>`
Como alternativa, você pode usar: `@argument` `{type} name <Parameter Description>` **ou** `@arg` `{type}` `name <Parameter Description>`.
Mostra os parâmetros usados pela função. Uma função pode ter várias tags de parâmetro, uma tag para cada parâmetro na ordem de ocorrência.
   `{type}` representa o tipo de parâmetro. Os tipos de parâmetros permitidos são:

   1. sequência de caracteres
   1. número
   1. booleano
   1. scope

   Escopo refere-se aos campos de um formulário adaptável. Quando um formulário usa carregamento lento, você pode usar `scope` para acessar os campos. Você pode acessar campos quando os campos são carregados ou se os campos são marcados como global.

   Todos os tipos de parâmetros são categorizados em um dos acima. Nenhum é suportado. Certifique-se de selecionar um dos tipos acima. Os tipos não fazem distinção entre maiúsculas e minúsculas. Espaços não são permitidos no parâmetro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo de retorno**
Sintaxe: Como alternativa, você pode usar `@return {type}`
Como alternativa, você pode usar `@returns {type}`.
Adiciona informações sobre a função, como seu objetivo.
{type} representa o tipo de retorno da função. Os tipos de retorno permitidos são:

   1. sequência de caracteres
   1. número
   1. booleano

   Todos os outros tipos de retorno são classificados em um dos acima. Nenhum é suportado. Certifique-se de selecionar um dos tipos acima. Os tipos de retorno não fazem distinção entre maiúsculas e minúsculas.

   * **Essa**
Sintaxe: 
`@this currentComponent`
   Use @this para se referir ao componente Formulário adaptativo no qual a regra é gravada.

   O exemplo a seguir é baseado no valor do campo. No exemplo a seguir, a regra oculta um campo no formulário. O `this` porção de `this.value` refere-se ao componente subjacente do Formulário adaptativo, no qual a regra é gravada.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }
   ```

   >[!NOTE]
   >
   >Comentários antes da função personalizada são usados para resumo. O resumo pode estender-se para várias linhas até que uma tag seja encontrada. Limite o tamanho para um único para uma descrição concisa no construtor de regras.

**Adicionar uma função personalizada**

Por exemplo, você deseja adicionar uma função personalizada que calcula a área de um quadrado. Comprimento lateral é a entrada do usuário para a função personalizada, que é aceita por meio de uma caixa numérica no formulário. A saída calculada é exibida em outra caixa numérica do formulário. Para adicionar uma função personalizada, primeiro crie uma biblioteca do cliente e depois adicione-a ao repositório CRX.

Para criar uma biblioteca cliente e adicioná-la ao repositório CRX, execute as seguintes etapas:

1. Criar um clienteExecute as seguintes etapas na biblioteca. Para obter mais informações, consulte [Usar bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. No CRXDE, adicione uma propriedade `categories`com valor do tipo string como `customfunction` para `clientlib` pasta.

   >[!NOTE]
   >
   >`customfunction`é uma categoria de exemplo. Você pode escolher qualquer nome para a categoria que criar na `clientlib`pasta.

Depois de adicionar a biblioteca do cliente ao repositório CRX, use-a no Formulário adaptável. Ele permite usar sua função personalizada como uma regra no formulário. Para adicionar a biblioteca do cliente no formulário adaptável, execute as seguintes etapas:

1. Abra o formulário no modo de edição.
Para abrir um formulário no modo de edição, selecione um formulário e toque em **[!UICONTROL Abrir]**.
1. No modo de edição, selecione um componente e toque em ![nível de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e toque em ![cmppr](assets/configure-icon.svg).
1. Na barra lateral, em Nome da biblioteca do cliente, adicione a biblioteca do cliente. ( `customfunction` no exemplo.)

   ![Adicionar a biblioteca do cliente de função personalizada](assets/clientlib.png)

1. Selecione a caixa numérica de entrada e toque em ![editar regras](assets/edit-rules-icon.svg) para abrir o editor de regras.
1. Toque **[!UICONTROL Criar regra]**. Usando as opções mostradas abaixo, crie uma regra para salvar o valor quadrado da entrada no campo Saída do formulário.

[![Usar funções personalizadas para criar uma regra](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. Toque **[!UICONTROL Concluído]**. Sua função personalizada é adicionada.

#### Tipos suportados da declaração de função {#function-declaration-supported-types}

**Instrução de função**

```javascript
function area(len) {
    return len*len;
}
```

Essa função é incluída sem `jsdoc` comentários.

**Expressão de função**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Expressão de função e declaração**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Declaração de função como variável**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitação: a função personalizada escolhe somente a primeira declaração de função da lista de variáveis, se estiver juntos. Você pode usar a expressão de função para cada função declarada.

**Declaração de função como objeto**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Certifique-se de usar `jsdoc` para cada função personalizada. Embora `jsdoc`os comentários são encorajados, inclua um vazio `jsdoc`comente para marcar sua função como função personalizada. Ela permite a manipulação padrão da sua função personalizada.

## Gerenciar regras {#manage-rules}

Qualquer regra existente em um objeto de formulário é listada ao tocar no objeto e tocar em ![edit-rules1](assets/edit-rules-icon.svg). Você pode exibir o título e um resumo da regra de visualização. Além disso, a interface do usuário permite expandir e exibir o resumo completo da regra, alterar a ordem das regras, editar regras e excluir regras.

![Regras de lista](assets/list-rules.png)

Você pode executar as seguintes ações em regras:

* **Expandir/recolher**: A coluna Conteúdo na lista de regras exibe o conteúdo da regra. Se todo o conteúdo da regra não estiver visível na exibição padrão, toque em ![expand-rule-content](assets/Smock_ChevronDown.svg) para expandi-lo.

* **Reordenar**: Qualquer nova regra criada é empilhada na parte inferior da lista de regras. As regras são executadas de cima para baixo. A regra no topo é executada primeiro, seguida por outras regras do mesmo tipo. Por exemplo, se você tiver as regras Quando, Mostrar, Ativar e Quando na primeira, segunda, terceira e quarta posições a partir da parte superior, respectivamente, a regra Quando na parte superior será executada primeiro, seguida pela regra Quando na quarta posição. Em seguida, as regras Mostrar e Ativar são executadas.
É possível alterar a ordem de uma regra ao tocar em ![regras de classificação](assets/sort-rules.svg) ou arraste-a e solte-a na ordem desejada na lista.

* **Editar**: Para editar uma regra, marque a caixa de seleção ao lado do título da regra. As opções para editar e excluir a regra são exibidas. Toque **[!UICONTROL Editar]** para abrir a regra selecionada no editor de regras <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Excluir**: Para excluir uma regra, selecione-a e toque em **[!UICONTROL Excluir]**.

* **Ativar/Desativar**: Quando for necessário suspender o uso de uma regra temporariamente, é possível selecionar uma ou mais regras e tocar em **[!UICONTROL Desativar]** na barra de ferramentas Ações para desativá-las. Se uma regra estiver desativada, ela não será executada no tempo de execução. Para ativar uma regra que esteja desativada, você pode selecioná-la e tocar em Ativar na barra de ferramentas de ações. A coluna de status da regra exibe se a regra está ativada ou desativada.

![Desativar regra](assets/disablerule.png)

## Copiar e colar regras {#copy-paste-rules}

É possível copiar e colar uma regra de um campo para outros campos semelhantes para economizar tempo.

Para copiar e colar regras, faça o seguinte:

1. Toque no objeto de formulário do qual você deseja copiar uma regra e, na barra de ferramentas do componente, toque em ![editar regra](assets/edit-rules-icon.svg). A interface do usuário do editor de regras é exibida com o objeto de formulário selecionado e as regras existentes são exibidas.

   ![copiar regra](assets/copyrule.png)

   Para obter informações sobre como gerenciar regras existentes, consulte [Gerenciar regras](rule-editor.md#p-manage-rules-p).

1. Marque a caixa de seleção ao lado do título da regra. As opções para gerenciar a regra serão exibidas. Toque em **[!UICONTROL Copiar]**.

   ![copyrule2](assets/copyrule2.png)

1. Selecione outro objeto de formulário no qual deseja colar a regra e toque em **[!UICONTROL Colar]**. Além disso, é possível editar a regra para fazer alterações.

   >[!NOTE]
   >
   >É possível colar uma regra em outro objeto de formulário somente se esse objeto de formulário suportar o evento da regra copiada. Por exemplo, um botão suporta o evento click . É possível colar uma regra com um evento click em um botão, mas não em uma caixa de seleção.

1. Toque **[!UICONTROL Concluído]** para salvar a regra.

## Expressões aninhadas {#nestedexpressions}

O editor de regras permite usar vários operadores AND e OR para criar regras aninhadas. Você pode combinar vários operadores AND e OR em regras.

A seguir, um exemplo de uma regra aninhada que exibe uma mensagem ao usuário sobre a elegibilidade para a custódia de uma criança quando as condições necessárias forem atendidas.

![Expressão complexa](assets/complexexpression.png)

Também é possível arrastar e soltar condições em uma regra para editá-la. Toque e passe o mouse sobre a alça ( ![identificador](assets/drag-handle.svg)) antes de uma condição. Quando o ponteiro se transformar no símbolo da mão, como mostrado abaixo, arraste e solte a condição em qualquer lugar dentro da regra. A estrutura da regra muda.

![Arrastar e soltar](assets/drag-and-drop.png)

## Condições da expressão de data {#dateexpression}

O editor de regras permite usar comparações de datas para criar condições.

A seguir, um exemplo de condição que exibe um objeto de texto estático se a hipoteca na casa já estiver sendo realizada, o que o usuário significa preenchendo o campo de data.

Quando a data da hipoteca da propriedade como preenchida pelo usuário estiver no passado, o Formulário adaptativo exibirá uma nota sobre o cálculo de renda. A regra a seguir compara a data preenchida pelo usuário com a data atual e, se a data preenchida pelo usuário for anterior à data atual, o formulário exibirá a mensagem de texto (denominada Renda).

![Condição de expressão de data](assets/dateexpressioncondition.png)

Quando a data de preenchimento for anterior à data atual, o formulário exibirá a mensagem de texto (Renda) da seguinte maneira:

![Condição de expressão de data cumprida](assets/dateexpressionconditionmet.png)

## Condições de comparação de números {#number-comparison-conditions}

O editor de regras permite criar condições que comparam dois números.

A seguir, um exemplo de condição que exibe um objeto de texto estático se o número de meses que um candidato permanece no endereço atual for menor que 36.

![Condição de comparação de números](assets/numbercomparisoncondition.png)

Quando o usuário significa viver no endereço residencial atual por menos de 36 meses, o formulário exibe uma notificação de que é possível solicitar mais prova de residência.

![Mais provas solicitadas](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## Exemplo de regras {#example}

### Chamar o serviço de Modelo de dados de formulário {#invoke}

Considere um serviço da Web `GetInterestRates` que utiliza o montante do empréstimo, o contrato e a pontuação de crédito do requerente como entrada e retorna um plano de empréstimo incluindo o montante do IME e a taxa de juro. Crie um Modelo de dados de formulário usando o serviço da Web como uma fonte de dados. Você adiciona objetos de modelo de dados e um `get` para o modelo de formulário. O serviço é exibido na guia Services do modelo de dados de formulário. Em seguida, crie um Formulário adaptável que inclua campos de objetos de modelo de dados para capturar entradas de usuário para valor do empréstimo, duração e pontuação de crédito. Adicione um botão que aciona o serviço da Web para buscar detalhes do plano. A saída é preenchida em campos apropriados.

A regra a seguir mostra como configurar a ação Invoke service para realizar o cenário de exemplo.

![Exemplo-invoke-services](assets/example-invoke-services.png)

Chamar o serviço de Modelo de dados de formulário usando a regra de Formulário adaptável

### Acionando várias ações usando a regra Quando {#triggering-multiple-actions-using-the-when-rule}

Em um formulário de pedido de empréstimo, você deseja capturar se o candidato do empréstimo é ou não um cliente existente. Com base nas informações fornecidas pelo usuário, o campo de ID do cliente deve mostrar ou ocultar. Além disso, é necessário definir o foco no campo ID do cliente se o usuário for um cliente existente. O formulário de pedido de empréstimo tem os seguintes componentes:

* Um botão de opção, **[!UICONTROL Você já é cliente do Geometrixx?]**, que [!UICONTROL Sim] e [!UICONTROL Não] opções. O valor para Sim é **0** e Não é **1**.

* Um campo de texto, **[!UICONTROL ID do cliente do Geometrixx]**, para especificar a ID do cliente.

Quando você escreve uma regra Quando no botão de opção para implementar esse comportamento, a regra aparece da seguinte maneira no editor de regras visuais.

![When-rule-example](assets/when-rule-example.png)

Regra no editor visual

Na regra de exemplo, a declaração na seção Quando é a condição, que quando retorna Verdadeiro, executa as ações especificadas na seção Then.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Uso de uma saída de função em uma regra {#using-a-function-output-in-a-rule}

Em um formulário de pedido de compra, há a seguinte tabela, na qual os usuários preenchem seus pedidos. Nesta tabela:

* A primeira linha é repetível, de modo que os usuários podem solicitar vários produtos e especificar quantidades diferentes. O nome do elemento é `Row1`.
* O título da célula na coluna Quantidade de Produto da linha repetível é Quantidade. O nome do elemento desta célula é `productquantity`.
* A segunda linha da tabela não é repetível e o título da célula na coluna Quantidade do Produto nessa linha é Quantidade Total.

![Example-function-table](assets/example-function-table.png)

**A.** Linha1 **B.** Quantidade **C.** Quantidade total

Agora, você deseja adicionar quantidades especificadas na coluna Quantidade de Produto para todos os produtos e exibir a soma na célula Quantidade Total. Você pode obter essa soma escrevendo uma regra Definir valor de na célula Quantidade total, como mostrado abaixo.

![Example-function-output](assets/example-function-output.png)

Regra no editor visual

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Validação de um valor de campo usando expressão {#validating-a-field-value-using-expression}

No formulário de pedido de compra explicado no exemplo anterior, você deseja impedir que o usuário solicite mais de uma quantidade de qualquer produto cujo preço seja superior a 10000. Para fazer essa validação, você pode gravar uma regra Validar como mostrado abaixo.

![Exemplo de validação](assets/example-validate.png)

Regra no editor visual

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
