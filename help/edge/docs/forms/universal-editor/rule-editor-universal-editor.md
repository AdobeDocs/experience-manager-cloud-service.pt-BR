---
title: Editor de regras para Forms dinâmico no editor universal
description: Crie formulários dinâmicos e inteligentes usando o Editor de regras no Editor universal. Adicionar lógica condicional, cálculos e comportamentos interativos sem codificação.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 1%

---


# Editor de regras para Forms dinâmico no editor universal

O Editor de regras no Universal Editor permite criar formulários inteligentes e dinâmicos que respondem à entrada do usuário em tempo real. Você pode transformar formulários estáticos em experiências interativas com visibilidade de campo condicional, cálculos automatizados e lógica de negócios complexa, tudo sem escrever código.

## O que você vai aprender

Ao final deste guia, você deverá:

- Entenda como as regras funcionam e quando usar diferentes tipos de regras
- Habilitar e acessar o Editor de regras no Editor universal
- Criar lógica condicional para mostrar ou ocultar campos de formulário dinamicamente
- Implementar cálculos automatizados e validação de dados
- Criar funções personalizadas para regras de negócios complexas
- Aplicar práticas recomendadas para obter o desempenho ideal do formulário

## Por que usar o editor de regras?

**Transformar Forms Estático em Experiências Inteligentes:**

- **Lógica condicional**: mostrar campos relevantes com base em seleções de usuário
- **Cálculos Dinâmicos**: Calcular valores automaticamente como tipo de usuários
- **Validação de dados**: forneça feedback em tempo real e evite erros
- **UX aprimorado**: reduza a complexidade do formulário e oriente os usuários pelos fluxos lógicos
- **Nenhuma Codificação Necessária**: Interface visual acessível para não desenvolvedores

**Casos de uso comuns:**

- Formulários de cálculo de imposto com deduções condicionais
- Assistentes de várias etapas com caminhos de ramificação
- Formulários de seguro com cálculos de taxa
- Formulários de pesquisa com perguntas condicionais
- Formulários de comércio eletrônico com preços dinâmicos

## Como as regras funcionam

As regras são instruções automatizadas que tornam seus formulários inteligentes e responsivos. Eles especificam o que deve acontecer quando determinadas condições são atendidas.

### **Componentes da Regra**

**Condição**: um teste lógico que é avaliado como verdadeiro ou falso.

- &quot;A renda do usuário é superior a US$ 50 mil?&quot;
- &quot;O usuário selecionou &#39;Sim&#39; para cobertura de seguro?&quot;
- &quot;O campo de formulário está vazio?&quot;

**Ação**: o resultado que ocorre quando a condição é atendida.

- Mostrar ou ocultar campos de formulário
- Calcular valores automaticamente
- Exibir mensagens de validação
- Ativar ou desativar componentes

### **Padrões Lógicos da Regra**

**1. Condition-Action (When-Then)**

```
WHEN gross salary > 50000
THEN show "Additional Deduction" field
```

*Recomendado para:* Visibilidade de campo condicional, conteúdo dinâmico

**2. Condição de Ação (Set-If)**

```
SET taxable income = gross salary - deductions
IF deductions are applicable
```

*Recomendado para:* Cálculos, transformações de dados

**3. Action-Condition-Alternate (If-Then-Else)**

```
IF income > 50000
THEN show "High Income" fields
ELSE show "Standard Income" fields
```

*Recomendado para:* Lógica de ramificação, opções mutuamente exclusivas

### **Exemplo do mundo real**

**Cenário**: formulário de cálculo de imposto

- **Condição**: &quot;O salário bruto excede $50.000&quot;
- **Ação primária**: mostrar o campo &quot;Dedução adicional&quot;
- **Ação alternativa**: ocultar o campo &quot;Dedução adicional&quot;
- **Resultado**: os usuários só veem campos relevantes com base em seus níveis de renda

## Pré-requisitos

Antes de começar a trabalhar com o Editor de regras, verifique se você tem o seguinte:

### **Requisitos de Acesso**

- Acesso de criação ao **AEM as a Cloud Service**
- **Editor Universal** com a extensão do Editor de Regras habilitada
- Permissões de edição de formulários no ambiente do AEM

### **Requisitos técnicos**

- **Conhecimento básico sobre design de formulário**: familiaridade com componentes de formulário e suas propriedades
- **Familiaridade da lógica de negócios**: capacidade de definir requisitos condicionais
- **Conhecimento básico sobre o JavaScript** (necessário somente para funções personalizadas)

### **Habilitar Extensão de Editor de Regras**

A extensão Editor de Regras não está habilitada por padrão no Editor Universal. Você pode habilitá-lo no [Extension Manager](/help/implementing/developing/extending/extension-manager.md).

**Depois de habilitar a extensão:**
O ícone ![editar-regras](/help/forms/assets/edit-rules-icon.svg) aparece no canto superior direito ao selecionar componentes de formulário.

![Editor de regras do Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
*Figura: o ícone Editor de regras aparece ao selecionar componentes de formulário*

**Para acessar o Editor de Regras:**

1. Selecione qualquer componente de formulário no Universal Editor.
2. Clique no ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg) que aparece.
3. A interface do Editor de regras é aberta em um novo painel.

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-for-field.png)
*Figura: interface do Editor de regras para editar regras de componentes*

>[!NOTE]
>
> Neste artigo, o &quot;componente de formulário&quot; e o &quot;objeto de formulário&quot; se referem aos mesmos elementos (como campos de entrada, botões, painéis, etc.).

## Visão geral da interface do editor de regras

O Editor de regras oferece uma interface visual simples para criar e gerenciar regras:

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-interface.png)
*Figura: Concluir a interface do Editor de Regras com componentes numerados*

### **Componentes da Interface**

**1. Título de Componente e Tipo de Regra**

- **Propósito**: exibe o nome do componente selecionado e o tipo de regra atual.
- **Exemplo**: &quot;Insira o Salário Bruto&quot; (Entrada de Texto) com a regra &quot;Quando&quot; selecionada.
- **Dica**: sempre confirme se você está editando o componente correto.

**2. Painel de Funções e Objetos de Formulário**

- **Guia Objetos de Formulário**: fornece uma exibição hierárquica de todos os componentes de formulário.
   - Usar para: fazer referência a outros campos nas regras.
   - Navegação: expanda ou recolha para localizar componentes específicos.
- **Guia Funções**: contém funções matemáticas e lógicas internas.
   - Usar para: execução de cálculos complexos e manipulação de dados.
   - Categorias: funções de Matemática, String, Data e Validação.

**3. Botão de Alternância do Painel**

- **Propósito**: mostra ou oculta o painel de objetos e funções.
- **Dica**: desative o painel para aumentar o espaço de trabalho de edição de regras.
- **Atalho do teclado**: útil ao trabalhar com regras complexas.

**4. Construtor de Regras Visual**

- **Propósito**: a área principal para a construção da lógica da regra.
- **Recursos**: seletores de lista suspensa e interface de arrastar e soltar.
- **Fluxo de trabalho**: Selecione o tipo de regra → Defina condições → Defina ações.

**5. Botões de Controle**

- **Concluído**: salva a regra e fecha o editor.
- **Cancelar**: descarta as alterações e fecha o editor sem salvar.
- **Dica**: sempre teste suas regras antes de clicar em Concluído.

### **Gerenciamento de regras**

Ao abrir o Editor de regras para um componente que já tem regras:

![mostrar as regras disponíveis do objeto de formulário](/help/edge/docs/forms/assets/rule-editor15.png)
*Figura: gerenciamento de regras existentes para um componente de formulário*

**Ações disponíveis:**

- **Exibir**: revise os resumos e a lógica da regra.
- **Editar**: modificar as condições ou ações da regra existentes.
- **Reordenar**: alterar a ordem de execução das regras (regras são executadas de cima para baixo).
- **Habilitar/Desabilitar**: habilitar ou desabilitar temporariamente regras para fins de teste.
- **Excluir**: remover regras permanentemente.

>[!TIP]
>
> **A ordem de execução das regras é importante**: as regras são executadas de cima para baixo. Coloque condições mais específicas antes das gerais.

## Tipos de regras disponíveis

O Editor de regras oferece um conjunto abrangente de tipos de regras organizados por funcionalidade. Selecione o tipo apropriado com base no seu caso de uso específico:

### **Regras de Lógica Condicional**

**Quando**

- **Propósito**: serve como a regra condicional primária para implementar lógica complexa.
- **Caso de uso**: por exemplo, &quot;Quando o usuário selecionar &#39;Casado&#39;, mostrar campos de informações do cônjuge.&quot;
- **Padrão lógico**: Condição → Ação (com uma ação alternativa opcional)

**Ocultar/Mostrar**

- **Propósito**: controla a visibilidade do campo com base nas condições especificadas.
- **Caso de uso**: ocultar seções irrelevantes ou habilitar divulgação progressiva.
- **Prática recomendada**: usar para criar uma experiência do usuário limpa e focalizada.

**Habilitar/Desabilitar**

- **Propósito**: controla se um campo pode ter interação, com base nas condições.
- **Caso de uso**: desabilite o botão enviar até que todos os campos necessários sejam preenchidos.
- **Prática recomendada**: fornecer feedback visual claro aos usuários.

### **Regras de Manipulação de Dados**

**Definir Valor De**

- **Propósito**: preenche automaticamente os valores do campo.
- **Caso de uso**: definir a data de hoje, calcular totais ou copiar valores entre campos.
- **Prática recomendada**: usar para reduzir o esforço do usuário e garantir a precisão.

**Limpar Valor De**

- **Propósito**: remove dados de campos quando as condições são alteradas.
- **Caso de uso**: limpar campos dependentes quando uma seleção pai for alterada.
- **Prática recomendada**: mantenha a integridade dos dados e evite valores órfãos.

**Formato**

- **Propósito**: transforma como os valores são exibidos.
- **Caso de uso**: moeda de formato, números de telefone ou datas.
- **Prática recomendada**: melhorar a legibilidade sem alterar os dados subjacentes.

### **Regras de validação**

**Validar**

- **Propósito**: implementa a lógica de validação personalizada.
- **Caso de uso**: aplicar regras comerciais complexas ou validação entre campos.
- **Prática recomendada**: fornecer mensagens de erro claras e acionáveis.

### **Regras de Cálculo**

**Expressão matemática**

- **Propósito**: executa cálculos automatizados.
- **Caso de uso**: cálculos de impostos, totais ou porcentagens.
- **Prática recomendada**: atualizar cálculos em tempo real conforme os usuários digitam.

### **Regras da Interface do Usuário**

**Definir Foco**

- **Propósito**: direciona a atenção do usuário para campos específicos.
- **Caso de uso**: concentre-se em campos de erro ou oriente os usuários pelas etapas do assistente.
- **Prática recomendada**: use com moderação para não interromper o fluxo do usuário.

**Definir Propriedade**

- **Propósito**: modifica dinamicamente as propriedades do componente.
- **Caso de uso**: alterar o texto do espaço reservado ou modificar opções em uma lista suspensa.
- **Prática recomendada**: aprimorar a experiência do usuário com alterações contextuais.

### **Regras de Controle de Formulário**

**Enviar Formulário**

- **Propósito**: aciona o envio de formulários de forma programática.
- **Caso de uso**: envio automático depois que condições específicas forem atendidas.
- **Prática recomendada**: sempre validar o formulário antes de enviar.

**Redefinir Formulário**

- **Propósito**: Limpa todos os dados do formulário e redefine o formulário para seu estado inicial.
- **Caso de uso**: funcionalidade &quot;Recomeçar&quot;.
- **Prática recomendada**: confirmar a ação com o usuário antes de redefinir.

**Salvar formulário**

- **Propósito**: salva o formulário como rascunho para conclusão posterior.
- **Caso de uso**: útil para formulários longos ou fluxos de trabalho de várias sessões.
- **Prática recomendada**: fornecer feedback claro sobre o status salvo.

### **Regras avançadas**

**Invocar Serviço**

- **Finalidade**: chama APIs ou serviços externos.
- **Caso de uso**: pesquisa de endereço, validação em tempo real ou enriquecimento de dados.
- **Prática recomendada**: lidar adequadamente com estados de carregamento e cenários de erro.

**Adicionar/Remover Instância**

- **Propósito**: gerencia dinamicamente seções que podem ser repetidas.
- **Caso de uso**: adicionar membros da família ou vários endereços.
- **Prática recomendada**: fornecer controles claros para adicionar ou remover instâncias.

**Navegar Para**

- **Propósito**: redireciona os usuários para outros formulários ou páginas.
- **Caso de uso**: fluxos de trabalho de vários formulários ou roteamento condicional.
- **Prática recomendada**: preservar dados de formulário antes da navegação.

**Navegar Entre Painéis**

- **Propósito**: controla a navegação em formulários de estilo de assistente.
- **Caso de uso**: formulários de várias etapas ou ignorando etapa condicional.
- **Prática recomendada**: exibir indicadores de progresso claros.

**Evento de expedição**

- **Propósito**: aciona eventos personalizados para integrações avançadas.
- **Caso de uso**: rastreamento do Analytics ou integrações de terceiros.
- **Prática recomendada**: usar somente para ações não bloqueadoras.


## Tutorial Passo a Passo: Criando uma Calculadora de Imposto Inteligente

Esta seção fornece um exemplo prático para demonstrar os recursos do Editor de regras. O exemplo orienta você na criação de um formulário de cálculo de imposto que usa lógica condicional e cálculos automatizados.

![Captura de tela da interface do Editor de regras mostrando a criação de uma regra condicional com lógica Quando-Então para visibilidade do campo de formulário](/help/edge/docs/forms/assets/rule-editor-1.png)
*Figura: formulário de cálculo de imposto com campos condicionais inteligentes*

### **Visão geral do tutorial**

Neste tutorial, você criará um formulário que:

1. **Adapta-se à entrada do usuário**: exibe campos relevantes com base no nível de renda.
2. **Calcula automaticamente**: calcula a obrigação fiscal em tempo real.
3. **Valida dados**: garante cálculos precisos e entrada de dados.

### **Estrutura do formulário**

| Nome do campo | Tipo | Propósito | Comportamento |
|------------|------|---------|----------|
| **Salário bruto** | Entrada de número | Usuário insere renda anual | Aciona a lógica condicional |
| **Dedução Adicional** | Entrada de número | Deduções adicionais (se aplicável) | Exibe quando o salário é superior a US$ 50.000 |
| **Renda Tributável** | Entrada de número | Calculado automaticamente | Atualizações em alterações de entrada |
| **Imposto a Pagar** | Entrada de número | Valor final do imposto | Calcula em uma taxa de 10% |

### **Lógica de negócios a ser implementada**

**Regra 1: Exibição de Campo Condicional**

```
WHEN Gross Salary > 50,000
THEN Show "Additional Deduction" field
ELSE Hide "Additional Deduction" field
```

**Regra 2: Cálculo de Receita Tributável**

```
SET Taxable Income = Gross Salary - Additional Deduction
(When Additional Deduction is applicable)
```

**Regra 3: Cálculo de Imposto**

```
SET Tax Payable = Taxable Income × 10%
(Simplified flat rate for demonstration)
```

### **Etapas de implementação**

Siga estas etapas para criar seu form de imposto inteligente:



+++ 1: Criar o formulário de base

**Objetivo**: criar a estrutura básica do formulário com todos os componentes necessários

Para criar o formulário de cálculo de imposto no Universal Editor:

1. **Abrir editor universal**
   - Navegue até o console AEM Sites
   - Selecione a página onde deseja adicionar o formulário
   - Clique em **Editar** para abrir o Editor Universal

2. **Adicionar componentes de formulário**

   Adicione esses componentes na ordem:

   | Componente | Tipo | Rótulo | Configurações |
   |-----------|------|-------|----------|
   | Título | Título | &quot;Formulário de Cálculo de Imposto&quot; | Nível do cabeçalho H2 |
   | Entrada de número | Entrada de número | &quot;Salário Bruto&quot; | Obrigatório: Sim, Espaço Reservado: &quot;Informar salário anual&quot; |
   | Entrada de número | Entrada de número | &quot;Dedução Adicional&quot; | Obrigatório: Não, Espaço Reservado: &quot;Informar deduções adicionais&quot; |
   | Entrada de número | Entrada de número | &quot;Renda Tributável&quot; | Obrigatório: Não, Somente leitura: Sim |
   | Entrada de número | Entrada de número | &quot;Imposto a Pagar&quot; | Obrigatório: Não, Somente leitura: Sim |
   | Botão de enviar | Enviar | &quot;Calcular Imposto&quot; | Tipo: enviar |

3. **Definir Configurações Iniciais**

   - **Ocultar o campo Dedução Adicional**:
      - Selecione o componente &quot;Dedução Adicional&quot;
      - No painel Propriedades, defina **Visível** como **Não**
      - Este campo será exibido condicionalmente com base em regras

   - **Tornar campos calculados somente leitura**:
      - Selecionar os campos &quot;Renda Tributável&quot; e &quot;Imposto a Pagar&quot;
      - Definir **Somente Leitura** como **Sim** em Propriedades

     ![Captura de tela de um formulário de cálculo de imposto com campos de entrada para salário bruto, estado civil e filhos dependentes, demonstrando a estrutura do formulário antes da aplicação das regras](/help/edge/docs/forms/assets/rule-editor2.png)
     *Figura: estrutura de formulário inicial com componentes básicos configurados*

**Ponto de verificação**: agora você deve ter um formulário com todos os campos obrigatórios, em que &quot;Dedução adicional&quot; esteja oculta e os campos calculados sejam somente leitura.

+++

+++ &#x200B;2. Adicionar uma regra condicional para um campo de formulário

Depois de criar o formulário, escreva a primeira regra para mostrar o campo `Additional Deduction` somente se o salário bruto exceder $50.000. Para adicionar uma regra condicional:

1. Abra um formulário no Editor Universal para edição e selecione o campo **[!UICONTROL Salário Bruto]** na árvore de conteúdo e selecione ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Como alternativa, você pode selecionar o campo **[!UICONTROL Salário Bruto]** diretamente do painel **[!UICONTROL Objeto do Forms]**.
   ![Exemplo do Editor de Regras1](/help/edge/docs/forms/assets/rule-editor3.png)
A interface visual do Editor de regras é exibida.
1. Clique em **[!UICONTROL Criar]** para criar regras.
   ![Exemplo do Editor de Regras2](/help/edge/docs/forms/assets/rule-editor4.png)
Por padrão, o tipo de regra `Set Value Of` está selecionado. Embora não seja possível alterar ou modificar o objeto selecionado, você poderá usar o menu suspenso de regras para selecionar outro tipo de regra.\
   ![Exemplo do Editor de Regras3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Abra a lista suspensa tipo de regra e selecione o tipo de regra **[!UICONTROL Quando]**.
   ![Exemplo do Editor de Regras4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Selecione o menu suspenso **[!UICONTROL Selecionar Estado]** e selecione **[!UICONTROL é maior que]**. O campo **[!UICONTROL Inserir um Número]** é exibido.
   ![Exemplo do Editor de Regras5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Insira `50000` no campo **[!UICONTROL Insira um Número]** na regra.
   ![Exemplo do Editor de Regras6](/help/edge/docs/forms/assets/rule-editor8.png)
Você definiu a condição como `When Gross Salary is greater than 50000`. Em seguida, defina a ação a ser executada se esta condição for `True`.
1. Na instrução `Then`, selecione **[!UICONTROL Mostrar]** no menu suspenso **[!UICONTROL Selecionar Ação]**.
   ![Exemplo do Editor de Regras7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Arraste e solte o campo **[!UICONTROL Dedução Adicional]** da guia Objetos de Formulário no campo **[!UICONTROL Soltar objeto ou selecionar aqui]**. Como alternativa, selecione o campo **[!UICONTROL Soltar objeto ou selecione aqui]** e selecione o campo **[!UICONTROL Dedução Adicional]** no menu pop-up, que lista todos os objetos de formulário no formulário.
   ![Exemplo do Editor de Regras8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Clique em **[!UICONTROL Adicionar Seção Mais]** para adicionar outra condição ao campo **[!UICONTROL Salário Bruto]**, caso insira um salário menor que `50000`.
   ![Exemplo do Editor de Regras9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Selecione **[!UICONTROL Ocultar]** no menu suspenso **[!UICONTROL Selecionar Ação]** na instrução `Else`.
   ![Exemplo do Editor de Regras10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Arraste e solte o campo **[!UICONTROL Dedução Adicional]** da guia Objetos de Formulário no campo **[!UICONTROL Soltar objeto ou selecionar aqui]**. Como alternativa, selecione o campo **[!UICONTROL Soltar objeto ou selecione aqui]** e selecione o campo **[!UICONTROL Dedução Adicional]** no menu pop-up, que lista todos os objetos de formulário no formulário.
   ![Exemplo do Editor de Regras11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.
A regra é exibida da seguinte maneira no Editor de regras:
   ![Exemplo do Editor de Regras12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> Como alternativa, você pode escrever uma regra Mostrar no campo Dedução Adicional, em vez de uma regra Quando no campo Salário Bruto, para implementar o mesmo comportamento.

+++

+++ &#x200B;3. Adicionar regras de cálculo para os campos de formulário

Em seguida, escreva uma regra para calcular o `Taxable Income`, que é a diferença entre `Gross Salary` e `Additional Deduction` (se aplicável). Para adicionar uma regra de cálculo ao campo **[!UICONTROL Receita Tributável]**, execute as seguintes etapas:

1. No modo de criação, selecione o campo **[!UICONTROL Receita Tributável]** e selecione o ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Como alternativa, você pode selecionar o campo **[!UICONTROL Receita Tributável]** diretamente do painel **[!UICONTROL Objeto Forms]**.
1. Em seguida, selecione **[!UICONTROL Criar]** para criar a regra.
   ![Exemplo do Editor de Regras13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Selecione **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão Matemática]**. Um campo para escrever expressão matemática é aberto.
   ![Exemplo do Editor de Regras14](/help/edge/docs/forms/assets/rule-editor17.png)

1. No campo de expressão matemática:

   - Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Salário Bruto]** no primeiro objeto **[!UICONTROL Soltar ou selecione aqui]**.

   - Selecione **[!UICONTROL Menos]** no campo **[!UICONTROL Selecionar Operador]**.

   - Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Dedução Adicional]** no outro objeto **[!UICONTROL Soltar ou selecione aqui]**.
     ![Exemplo do Editor de Regras15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

   Agora, adicione uma regra para o campo `Tax Payable `, que é determinado pela multiplicação da receita tributável pela alíquota do imposto. Para simplificar, suponha uma alíquota de imposto fixa de `10%`.

1. No modo de criação, selecione o campo **[!UICONTROL Imposto a Pagar]** e selecione o ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Em seguida, selecione **[!UICONTROL Criar]** para criar regras.
   ![Exemplo do Editor de Regras16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Selecione **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão Matemática]**. Um campo para escrever expressão matemática é aberto.
   ![Exemplo do Editor de Regras17](/help/edge/docs/forms/assets/rule-editor20.png)
1. No campo de expressão matemática:

   - Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Receita Tributável]** no primeiro objeto **[!UICONTROL Soltar ou selecione aqui]**.

   - Selecione **[!UICONTROL Multiplicado por]** no campo **[!UICONTROL Selecionar operador]**.

   - Selecione **Número** no campo **[!UICONTROL Selecionar Opção]** e insira o valor como `10` no campo **[!UICONTROL Inserir um Número]**.
     ![Exemplo do Editor de Regras18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Em seguida, selecione na área destacada ao redor do campo de expressão e selecione **[!UICONTROL Estender expressão]**.
   ![Exemplo do Editor de Regras19](/help/edge/docs/forms/assets/rule-editor22.png)
1. No campo de expressão estendida, selecione **[!UICONTROL dividido por]** no campo **[!UICONTROL Selecionar Operador]** e **[!UICONTROL Número]** no campo **[!UICONTROL Selecionar Opção]**. Em seguida, especifique `100` no campo de número.
   ![Exemplo do Editor de Regras20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

+++

+++ &#x200B;4. Pré-visualizar um formulário

Agora, ao visualizar o formulário e inserir o **Salário Bruto** como `60,000`, o campo **Dedução Adicional** será exibido e a **Renda Tributável** e o **Imposto a Pagar** serão calculados adequadamente.

![Visualizar um formulário](/help/edge/docs/forms/assets/rule-editor-form.png)

+++

Além das funções integradas como Sum e Average, é possível criar funções personalizadas para implementar uma lógica de negócios complexa e personalizada de acordo com suas necessidades específicas.

## Avançado: funções personalizadas

**Quando Usar Funções Personalizadas:**

- Para cálculos complexos que vão além dos recursos de funções integradas
- Para implementar regras de validação específicas de negócios
- Para transformações e formatação de dados
- Para integrar a sistemas ou APIs externos

**Vantagens:**

- **Reusabilidade**: gravar a função uma vez e usá-la em vários formulários e regras
- **Capacidade de manutenção**: lógica centralizada e fácil de atualizar
- **Desempenho**: execução otimizada do JavaScript
- **Flexibilidade**: capacidade de lidar com cenários complexos não resolvidos pelas regras padrão

### **Criando Funções Personalizadas**

**Local do Arquivo**: `/blocks/form/functions.js` em seu projeto do AEM

**Fluxo de Trabalho de Desenvolvimento:**

1. **Declaração de função**
   - Defina nomes e parâmetros de funções claros e descritivos
   - Usar nomes que indicam a finalidade da função
   - Parâmetros de documento e tipos de retorno

2. **Implementação lógica**
   - Escreva um código JavaScript limpo e eficiente
   - Lidar com casos de borda e cenários de erro
   - Seguir as práticas recomendadas de codificação

3. **Exportação de Função**
   - Exportar funções para torná-las disponíveis no Editor de regras
   - Usar exportações nomeadas para uma melhor organização
   - Testar funções antes da implantação

4. **Documentação**
   - Adicionar comentários JSDoc para a documentação da função
   - Incluir exemplos de uso
   - Especificar tipos de parâmetros e valores de retorno

O exemplo a seguir demonstra duas funções personalizadas: `getFullName` e `days`.

```JavaScript
/**
 - Get Full Name
 - @name getFullName Concats first name and last name
 - @param {string} firstname in Stringformat
 - @param {string} lastname in Stringformat
 - @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 - Calculate the number of days between two dates.
 - @param {*} endDate
 - @param {*} startDate
 - @name days Calculates the numebr of days between two dates
 - @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```

![Adicionando Função personalizada](/help/edge/docs/forms/assets/create-custom-function.png)

### Usar uma função personalizada no editor de regras

Para usar uma função personalizada no Editor de regras:

1. **Adicionar a Função**: adicione sua função personalizada ao arquivo `../[blocks]/form/functions.js`. Certifique-se de incluí-lo na instrução `export` no arquivo.
2. **Implantar o arquivo**: implante o arquivo `functions.js` atualizado em seu projeto GitHub e confirme se a compilação foi concluída com êxito.
3. **Uso da Função**: no Editor de Regras do formulário, acesse a função selecionando a opção `Function Output` no campo **[!UICONTROL Selecionar Ação]**.

   ![Função personalizada no editor de regras](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

4. **Visualizar o Formulário**: visualize o formulário para verificar se a função recém-implementada funciona conforme esperado.

## Práticas recomendadas para o desenvolvimento de regras

### **Otimização do desempenho**

**Minimizar Complexidade da Regra**

- Mantenha as regras individuais simples e concentradas.
- Divida a lógica complexa em várias regras menores.
- Evite condições aninhadas profundamente quando possível.

**Otimizar Execução da Regra**

- Coloque as regras acionadas com mais frequência primeiro.
- Use condições específicas para reduzir avaliações desnecessárias.
- Considere o impacto das regras no tempo de carregamento do formulário.

**Gerenciamento de recursos**

- Limitar o número de regras por componente de formulário.
- Use funções personalizadas para lógica repetida em vez de regras de duplicação.
- Teste o desempenho com volumes de dados realistas.

### **Diretrizes de experiência do usuário**

**Fornecer Comentários Claros**

- Use mensagens de validação que orientem os usuários para a entrada correta.
- Mostrar indicadores de carregamento para regras que envolvem serviços externos.
- Implemente a divulgação progressiva para reduzir a carga cognitiva.

**Manter Capacidade De Resposta Do Formulário**

- Evite regras que causam alterações visuais abruptas.
- Implementar transições suaves para operações de mostrar/ocultar.
- Testar regras em diferentes dispositivos e tamanhos de tela.

**Tratamento de erros**

- Fornecer comportamento de fallback quando as regras falharem.
- Exibir mensagens de erro amigáveis.
- Registra erros para depuração enquanto mantém uma experiência do usuário positiva.

### **Práticas recomendadas de desenvolvimento**

**Estratégia de teste**

- Testar regras com casos de borda e valores de limite.
- Verifique o comportamento da regra em navegadores diferentes.
- Teste a funcionalidade do formulário com e sem o JavaScript ativado.

**Documentação**

- Documente a lógica de negócios por trás de regras complexas.
- Manter um estoque de regras para formulários grandes.
- Use convenções de nomenclatura consistentes para componentes e regras.

**Controle de Versão**

- Rastrear alterações em funções personalizadas no controle de versão.
- Testar regras em um ambiente de desenvolvimento antes da produção.
- Manter cópias de backup de configurações de regra de trabalho.

## Solução de problemas comuns

### **Problemas de Execução da Regra**

**Regras Não Estão Sendo Acionadas**

- **Verificar nomes de componentes**: verifique se os componentes referenciados existem e se têm nomes corretos.
- **Verificar ordem da regra**: as regras são executadas de cima para baixo; reordene se necessário.
- **Validar condições**: teste condições com valores conhecidos para verificar a lógica.
- **Console do navegador**: verifique se há erros de JavaScript que possam bloquear a execução.

**Comportamento de Regra Incorreto**

- **Revise os operadores lógicos**: Confirme se as condições E/OU estão estruturadas corretamente.
- **Testar com dados de exemplo**: use valores conhecidos para isolar problemas.
- **Verificar tipos de dados**: verifique se as comparações numéricas usam números, não cadeias de caracteres.
- **Validar expressões**: teste expressões matemáticas separadamente.

### **Problemas de desempenho**

**Resposta lenta do formulário**

- **Reduza a complexidade da regra**: simplifique a lógica condicional complexa.
- **Otimizar funções personalizadas**: criar um perfil e otimizar o código JavaScript.
- **Limitar chamadas externas**: minimize as invocações de serviço nas regras.
- **Usar seletores eficientes**: verifique se as referências a objetos de formulário são específicas.

**Uso de Memória**

- **Limpar ouvintes de eventos**: Remova as associações de regra não usadas.
- **Otimizar funções personalizadas**: evite vazamentos de memória no código JavaScript.
- **Escopo de regra de limite**: use regras de destino em vez de condições globais.

### **Problemas de função personalizada**

**Funções Não Disponíveis**

- **Verificar caminho do arquivo**: verifique se `functions.js` está no local correto: `/blocks/form/functions.js`.
- **Verificar exportações**: verifique se as funções foram exportadas corretamente.
- **Processo de compilação**: confirme se a compilação do projeto inclui o arquivo de funções atualizado.
- **Limpeza de cache**: limpe o cache do navegador após implantar novas funções.

**Erros de Função**

- **Validação de parâmetro**: verifique se os parâmetros de função correspondem aos tipos esperados.
- **Manipulação de erros**: adicione blocos try-catch para manipular exceções normalmente.
- **Log de console**: use console.log para a execução da função de depuração.
- **Validação de JSDoc**: verifique se a documentação da função corresponde à implementação.

### **Integração do Editor Universal**

**O Editor De Regras Não Aparece**

- **Extensão habilitada**: verifique se a extensão do Editor de Regras está ativada.
- **Seleção de componente**: verifique se você selecionou um componente de formulário com suporte.
- **Compatibilidade de navegador**: testar em navegadores compatíveis (Chrome, Firefox, Safari).
- **Permissões de acesso**: confirme se o usuário tem as permissões necessárias do AEM.

**Problemas de interface**

- **Visibilidade do painel**: use o botão de alternância para mostrar ou ocultar o painel de objetos de formulário.
- **Salvando regra**: verifique se as regras estão salvas antes de fechar o editor.
- **Zoom do navegador**: redefina o zoom do navegador para 100% para uma exibição de interface ideal.

## Limitações importantes

>[!IMPORTANT]
>
> **Restrições de Função Personalizada**:
>
> - Importações estáticas e dinâmicas não são suportadas em scripts de função personalizados.
> - Todo o código deve ser incluído diretamente no arquivo `/blocks/form/functions.js`.
> - As funções devem ser síncronas (sem assíncronas/espera ou Promessas).
> - O acesso às APIs do navegador é limitado por motivos de segurança.

>[!WARNING]
>
> **Considerações sobre a produção**:
>
> - Teste todas as regras completamente em um ambiente de preparo.
> - Monitore o desempenho do formulário após implantar regras complexas.
> - Ter um plano de reversão para problemas relacionados a regras.
> - Considere o impacto em usuários com conexões de rede lentas.

## Resumo

O Editor de regras no Universal Editor permite criar formulários inteligentes e dinâmicos que proporcionam experiências excepcionais para o usuário. Ao implementar lógica condicional, cálculos automatizados e regras de negócios personalizadas, você pode:

**Transformar Forms Estática**:

- Adicione visibilidade de campo condicional para interfaces mais limpas e focadas.
- Implementar cálculos em tempo real e validação de dados.
- Crie uma lógica de negócios sofisticada sem codificar.

**Melhorar a Experiência do Usuário**:

- Orientar usuários por meio de fluxos de formulário lógicos.
- Reduza erros com validação inteligente.
- Forneça feedback e assistência imediatos.

**Aumentar a Eficiência**:

- Automatize cálculos repetitivos e a entrada de dados.
- Simplifique workflows complexos com roteamento inteligente.
- Reduza a carga de suporte com recursos de autoatendimento.

### **Próximas etapas**

Agora que você entende os fundamentos do Editor de regras:

1. **Iniciar como Simples**: comece com regras básicas de mostrar/ocultar antes de avançar para cálculos complexos.
1. **Prática com Exemplos**: use o tutorial de calculadora de impostos como base.
1. **Explorar recursos avançados**: experimente funções personalizadas para requisitos especializados.
1. **Testar Completamente**: Sempre validar regras em diferentes cenários e dispositivos.
1. **Monitorar Desempenho**: certifique-se de que as regras melhorem em vez de dificultarem a experiência do usuário.
