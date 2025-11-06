---
title: Editor de regras para o Edge Delivery Services Forms
description: Crie formulários dinâmicos e inteligentes usando o Editor de regras no Editor universal. Adicionar lógica condicional, cálculos e comportamentos interativos sem codificação.
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 0%

---


# Editor de regras para o Edge Delivery Services Forms

O Editor de regras permite que os autores transformem formulários estáticos em experiências responsivas e inteligentes sem escrever código. Você pode mostrar campos condicionalmente, realizar cálculos, validar dados, orientar usuários por meio de fluxos e integrar uma lógica de negócios que se adapta à medida que as pessoas digitam.

## O que você vai aprender

Ao final deste guia, você será capaz de:

- Entenda como as regras funcionam e quando usar diferentes tipos de regras
- Habilitar e acessar o Editor de regras no Editor universal
- Criar lógica condicional para mostrar ou ocultar campos dinamicamente
- Implementar cálculos automatizados e validação de dados
- Criar funções personalizadas para regras de negócios complexas
- Aplicar práticas recomendadas para desempenho, capacidade de manutenção e UX

## Por que usar o Editor de regras?

- **Lógica condicional**: mostrar campos relevantes somente quando necessário para reduzir ruído e carga cognitiva.
- **Cálculos dinâmicos**: Calcule valores automaticamente (totais, taxas, impostos) conforme o tipo de usuário.
- **Validação de dados**: evite erros antecipadamente com verificações em tempo real e mensagens claras.
- **Experiências guiadas**: conduza usuários pelas etapas lógicas (assistentes, ramificação).
- **Criação sem código**: configure um comportamento poderoso por meio de uma interface visual.

Cenários comuns incluem calculadoras de impostos, estimadores de empréstimos e prêmios, fluxos de elegibilidade, aplicativos em várias etapas e pesquisas com perguntas condicionais.

## Como as regras funcionam

Uma regra define o que deve acontecer quando uma condição é atendida. Conceitualmente, uma regra tem duas partes:

- **Condição**: uma instrução que é avaliada como verdadeira ou falsa.
   - Exemplos: &quot;Renda > 50.000&quot;, &quot;Cobertura = &#39;Sim&#39;&quot;, &quot;Campo vazio&quot;
- **Ação**: o que ocorre quando a condição é verdadeira (e, opcionalmente, quando ela é falsa).
   - Exemplos: Mostrar/Ocultar um campo, Definir/Limpar um valor, Validar entrada, Ativar/Desativar um botão

+++ Padrões lógicos de regra

- **Condição → Ação (Quando/Depois)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Melhor para visibilidade condicional e divulgação progressiva.

- **Ação ← Condição (Definir Se/Somente se)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Melhor para cálculos e transformações de dados.

- **Se → Então → Outro (Ação alternativa)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Melhor para a lógica de ramificação e fluxos mutuamente exclusivos.

+++

+++ Exemplo do mundo real

- **Condição**: &quot;O salário bruto excede $50.000&quot;
- **Ação principal**: mostrar &quot;Dedução adicional&quot;
- **Ação alternativa**: ocultar &quot;Dedução adicional&quot;
- **Resultado**: os usuários veem somente os campos que se aplicam a eles

+++

## Pré-requisitos


+++ Requisitos de acesso

**Configuração e permissões essenciais**:

- **AEM as a Cloud Service**: acesso de criação com permissões de edição de formulário
- **Editor Universal**: instalado e configurado em seu ambiente
- **Extensão do Editor de Regras**: habilitada via [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Permissões de edição de formulário**: capacidade de criar e modificar componentes de formulário no Universal Editor

**Etapas de verificação**:

1. Confirme se você pode acessar o Universal Editor no console do AEM Sites
2. Verificar se é possível criar e editar componentes de formulário
3. Verifique se o ícone do Editor de regras ![edit-rules](/help/forms/assets/edit-rules-icon.svg) aparece ao selecionar componentes de formulário

+++

+++ Requisitos técnicos

**Conhecimentos e habilidades necessários**:

- **Proficiência do Editor Universal**: experiência na criação de formulários com entradas de texto, menus suspensos e propriedades básicas de campo
- **Entendimento da lógica de negócios**: capacidade de definir requisitos condicionais e regras de validação para seu caso de uso específico
- **Familiaridade do componente de formulário**: conhecimento dos tipos de campo (texto, número, lista suspensa), propriedades (obrigatório, visível, somente leitura) e estrutura do formulário

**Opcional para uso avançado**:

- **Fundamentos do JavaScript**: necessário apenas para criar funções personalizadas (tipos de dados, funções, sintaxe básica)
- **Noções básicas sobre JSON**: útil para manipulação de dados complexos e integrações de API

**Perguntas de avaliação**:

- Você pode criar um formulário básico com entradas de texto e um botão de envio no Universal Editor?
- Você entende quando os campos devem ser obrigatórios e opcionais no contexto de negócios?
- Você consegue identificar quais elementos de formulário precisam de visibilidade condicional no seu caso de uso?

+++

+++ Ativar a extensão Editor de regras

**Importante**: a extensão do Editor de Regras não é habilitada por padrão em ambientes do Editor Universal.

**Etapas de ativação**:

1. Navegue até a [Extension Manager](/help/implementing/developing/extending/extension-manager.md) no seu ambiente do AEM
2. Localize a extensão &quot;Editor de regras&quot; na lista de extensões disponíveis
3. Clique em **Habilitar** e confirme a ativação
4. Aguarde a atualização do sistema (pode levar de 1 a 2 minutos)

**Verificação**:

- Depois de habilitar, o ícone Editor de regras aparece quando você seleciona um componente de formulário: ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![Editor de regras do Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Figura: o ícone Editor de regras aparece ao selecionar componentes de formulário

Para abrir o Editor de regras:

1. Selecione um componente de formulário no Editor universal.
2. Clique no ícone Editor de regras.
3. O Editor de regras é aberto em um painel lateral.

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Figura: interface do Editor de regras para editar regras de componentes

>[!NOTE]
>
> Neste artigo, &quot;componente de formulário&quot; e &quot;objeto de formulário&quot; se referem aos mesmos elementos (por exemplo, entradas, botões, painéis).

## Visão geral da interface do Editor de regras

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-interface.png)
Figura: Interface completa do Editor de regras com componentes numerados

1. **Título e tipo de regra do componente**: confirma o componente selecionado e o tipo de regra ativo.
2. **Painel de Funções e Objetos de Formulário**:

   - Objetos de formulário: exibição hierárquica de campos e containers para referência em regras
   - Funções: auxiliares de matemática, string, data e validação integrados

3. **Alternância de painel**: mostrar/ocultar o painel de objetos e funções para aumentar o espaço de trabalho
4. **Construtor visual de regras**: arrastar e soltar, criador de regras orientado por lista suspensa
5. **Controles**: Concluído (salvar), Cancelar (descartar). Sempre teste as regras antes de salvar.

+++

+++ Gerenciamento de regras existentes

Quando um componente já tem regras, é possível:

- **Exibir**: consulte os resumos e a lógica da regra
- **Editar**: modificar condições e ações
- **Reordenar**: alterar a ordem de execução (de cima para baixo)
- **Habilitar/Desabilitar**: alternar regras para teste
- **Excluir**: remover regras com segurança

>[!TIP]
>
> Coloque regras específicas antes das gerais. A execução é de cima para baixo.

+++

## Tipos de regras disponíveis

Escolha o tipo de regra que melhor corresponda à sua intenção.

+++ Lógica condicional

- **Quando**: regra primária para comportamento condicional complexo (Condição → Ação ± Else)
- **Ocultar/Mostrar**: controla a visibilidade com base em uma condição (divulgação progressiva)
- **Habilitar/Desabilitar**: controla se um campo é interativo (por exemplo, desabilite Enviar até que os campos obrigatórios sejam válidos)

+++

+++ Manipulação de dados

- **Definir Valor de**: preencher valores automaticamente (por exemplo, datas, totais, cópias)
- **Limpar Valor de**: Remover dados quando as condições forem alteradas
- **Formato**: transformar a formatação de exibição (moeda, telefone, data) sem alterar os valores armazenados

+++

+++ Validação

- **Validar**: lógica de validação personalizada, incluindo verificações entre campos e regras de negócios

+++

+++ Cálculo

- **Expressão matemática**: calcular valores em tempo real (totais, impostos, taxas)

+++

+++ Interface do usuário

- **Definir Foco**: Mover o foco para um campo específico (use com moderação)
- **Definir Propriedade**: modifique propriedades do componente dinamicamente (espaço reservado, opções etc.)

+++

+++ Controle de formulários

- **Enviar Formulário**: enviar o formulário de forma programática (somente após a aprovação das validações)
- **Redefinir Formulário**: Limpar e redefinir para o estado inicial (confirme antes de usar)
- **Salvar Formulário**: Salvar como rascunho para mais tarde (formulários longos, várias sessões)

+++

+++ Avançado

- **Invocar Serviço**: chamar APIs/serviços externos (manipular carregamento e erros)
- **Adicionar/Remover Instância**: Gerenciar seções que podem ser repetidas (por exemplo, dependentes, endereços)
- **Navegar para**: rotear para outros formulários/páginas (preservar dados antes da navegação)
- **Navegar Entre Painéis**: navegação e salto da etapa do assistente de controle
- **Evento de expedição**: acionar eventos personalizados para integrações ou análises

+++

## Tutorial passo a passo: Criar uma calculadora de impostos inteligente

+++ Visão geral do tutorial

Este exemplo demonstra visibilidade condicional e cálculos automáticos.

![Captura de tela da interface do Editor de regras mostrando a criação de uma regra condicional com lógica Quando-Então para visibilidade do campo de formulário](/help/edge/docs/forms/assets/rule-editor-1.png)
Figura: Formulário de cálculo de imposto com campos condicionais inteligentes

Você criará um formulário que:

1. Adapta-se à entrada do usuário mostrando campos relevantes
2. Calcula os valores em tempo real
3. Valida dados para melhorar a precisão

+++

+++ Estrutura do formulário

| Nome do campo | Tipo | Propósito | Comportamento |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Salário Bruto | Entrada de número | Receita anual do usuário | Aciona a lógica condicional |
| Dedução Adicional | Entrada de número | Deduções adicionais (se elegíveis) | Visível somente quando Salário > US$ 50.000 |
| Receita Tributável | Entrada de número | Valor calculado | Somente leitura, atualizações na alteração |
| Imposto a Pagar | Entrada de número | Valor calculado | Somente leitura, calculado em uma taxa uniforme |

+++

+++ Lógica de negócios

- **Regra 1: exibição condicional**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **Regra 2: Cálculo de receita tributável**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **Regra 3: Cálculo de imposto a pagar**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ Etapa 1: criar o formulário

**Objetivo**: criar o formulário base com todos os campos e configurações iniciais.

1. **Abrir editor universal**:
   - Navegue até o console AEM Sites, selecione sua página, clique em **Editar**
   - Verifique se o [Editor Universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) está configurado corretamente

2. **Adicionar componentes de formulário nesta ordem**:
   - Título (H2): &quot;Formulário de cálculo de imposto&quot;
   - Entrada de Número: &quot;Salário Bruto&quot; (Obrigatório: Sim, Espaço Reservado: &quot;Informar salário anual&quot;)
   - Entrada de Número: &quot;Dedução Adicional&quot; (Obrigatório: Não, Espaço Reservado: &quot;Informar deduções adicionais&quot;)
   - Entrada de Número: &quot;Renda Tributável&quot; (Somente Leitura: Sim)
   - Entrada de Número: &quot;Imposto a Pagar&quot; (Somente Leitura: Sim)
   - Botão Enviar: &quot;Calcular Imposto&quot;

3. **Configurar propriedades do campo inicial**:
   - Ocultar &quot;Dedução adicional&quot; (definido como Visível: Não no painel Propriedades)
   - Defina &quot;Renda Tributável&quot; e &quot;Imposto a Pagar&quot; como Somente Leitura: Sim

![Captura de tela de um formulário de cálculo de imposto com campos de entrada para salário bruto, estado civil e filhos dependentes, demonstrando a estrutura do formulário antes da aplicação das regras](/help/edge/docs/forms/assets/rule-editor2.png)
Figura: estrutura do formulário inicial com componentes básicos configurados

**Ponto de verificação**: você deve ter um formulário com todos os campos obrigatórios em que &quot;Dedução adicional&quot; esteja oculta e os campos calculados sejam somente leitura.

+++

+++ Etapa 2: adicionar regra de visibilidade condicional

**Meta**: mostrar o campo &quot;Dedução Adicional&quot; somente quando o Salário Bruto exceder $50.000.

1. **Selecione o campo Salário Bruto** e clique no ícone do Editor de Regras ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **Criar uma nova regra**:
   - Clique em **Criar**
   - Alterar tipo de regra de &quot;Definir Valor de&quot; para **&quot;Quando&quot;**
3. **Configurar a condição**:
   - Selecione **&quot;é maior que&quot;** na lista suspensa
   - Digite `50000` no campo de número
4. **Defina a ação Then**:
   - Escolha **&quot;Mostrar&quot;** na lista suspensa Selecionar ação
   - Arraste ou selecione o campo **&quot;Dedução Adicional&quot;** dos Objetos de Formulário
5. **Adicionar a ação Else**:
   - Clique em **&quot;Adicionar outra seção&quot;**
   - Escolha **&quot;Ocultar&quot;** na lista suspensa Selecionar ação
   - Selecionar o campo **&quot;Dedução Adicional&quot;**
6. **Salvar a regra**: Clique em **Concluído**

>[!NOTE]
>
> Abordagem alternativa: Você pode obter o mesmo resultado criando uma regra Mostrar/Ocultar diretamente no campo &quot;Dedução Adicional&quot; em vez de uma regra Quando em &quot;Salário Bruto&quot;.

+++

+++ Etapa 3: Adicionar regras de cálculo

**Meta**: calcular automaticamente &quot;Receita Tributável&quot; e &quot;Imposto a Pagar&quot; com base na entrada do usuário.

**Configurar cálculo de Renda Tributável**:

1. **Selecione o campo &quot;Receita Tributável&quot;** e abra o Editor de Regras
2. **Criar expressão matemática**:
   - Clique em **Criar** → Selecionar **&quot;Expressão matemática&quot;**
   - Expressão de compilação: **Salário Bruto - Dedução Adicional**
   - Arraste &quot;Salário Bruto&quot; para o primeiro campo
   - Selecionar operador **&quot;Menos&quot;**
   - Arraste &quot;Dedução adicional&quot; para o segundo campo
3. **Salvar**: Clique em **Concluído**

**Configurar cálculo de Imposto a Pagar**:

1. **Selecione o campo &quot;Imposto a Pagar&quot;** e abra o Editor de Regras
2. **Criar expressão matemática**:
   - Clique em **Criar** → Selecionar **&quot;Expressão matemática&quot;**
   - Expressão de compilação: **Receita Tributável × 10 ÷ 100**
   - Arraste &quot;Renda Tributável&quot; para o primeiro campo
   - Selecione o operador **&quot;Multiplicado por&quot;**
   - Inserir `10` como número
   - Clique em **&quot;Estender expressão&quot;**
   - Selecione o operador **&quot;dividido por&quot;**
   - Inserir `100` como número
3. **Salvar**: Clique em **Concluído**

+++

+++ Etapa 4: testar o formulário

**Verifique sua implementação testando o fluxo completo**:

1. **Visualizar o formulário**: clique no modo de visualização no Editor Universal
2. **Testar a lógica condicional**:
   - Insira o Salário Bruto = `30000` → &quot;Dedução Adicional&quot; deve permanecer oculta
   - Insira o Salário Bruto = `60000` → &quot;Dedução Adicional&quot; deve aparecer
3. **Cálculos de teste**:
   - Com Salário Bruto = `60000`, insira Dedução Adicional = `5000`
   - Verificar Receita Tributável = `55000` (60000 - 5000)
   - Verificar Imposto a Pagar = `5500` (55000 × 10%)

![Visualizar um formulário](/help/edge/docs/forms/assets/rule-editor-form.png)
Figura: Calculadora de imposto concluída com campos condicionais e cálculos automáticos

**Critério de sucesso**: o formulário deve mostrar/ocultar campos dinamicamente e calcular valores em tempo real à medida que os usuários digitam.


+++

## Avançado: funções personalizadas

Para uma lógica de negócios complexa além dos recursos incorporados, é possível criar funções personalizadas do JavaScript que se integram perfeitamente ao Editor de regras.

+++ Quando usar funções personalizadas

**Cenários ideais para funções personalizadas**:

- **Cálculos complexos**: os cálculos em várias etapas não são facilmente expressos na regra de Expressão matemática
- **Validações específicas de negócios**: lógica de validação personalizada específica para sua organização ou setor
- **Transformações de dados**: conversões de formato, manipulações de cadeia de caracteres ou análise de dados
- **Integrações externas**: chamadas para APIs internas ou serviços de terceiros (com limitações)

**Vantagens das funções personalizadas**:

- **Reusabilidade**: Gravar uma vez, usar em vários formulários e regras
- **Manutenção**: lógica centralizada, mais fácil de atualizar e depurar
- **Desempenho**: execução otimizada de JavaScript em comparação a cadeias de regras complexas
- **Flexibilidade**: tratar casos de borda e cenários complexos não solucionados pelas regras padrão

+++

+++ Criação e implementação de funções personalizadas

**Local do arquivo**: todas as funções personalizadas devem ser definidas em `/blocks/form/functions.js` no seu projeto do Edge Delivery Services.

**Fluxo de trabalho de desenvolvimento**:

1. **Design da função**
   - Usar nomes de função descritivos e orientados por ação
   - Definir tipos claros de parâmetros e valores de retorno
   - Lidar com casos de borda e entradas inválidas normalmente

2. **Implementação**
   - Escreva JavaScript limpo e bem comentado
   - Incluir validação de entrada e tratamento de erros
   - Testar funções independentemente antes da integração

3. **Documentação**
   - Adicionar comentários JSDoc abrangentes
   - Incluir exemplos de uso e descrições de parâmetros
   - Documentar quaisquer limitações ou dependências

4. **Implantação**
   - Exportar funções usando exportações nomeadas
   - Implantar no repositório do projeto
   - Verificar a conclusão da criação antes do teste

**Exemplo de implementação**:

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![Adicionando Função personalizada](/help/edge/docs/forms/assets/create-custom-function.png)
Figura: Adicionar funções personalizadas ao arquivo functions.js

+++

+++ Uso de funções personalizadas no Editor de regras

**Etapas de integração**:

1. **Adicionar função ao projeto**
   - Criar ou editar `/blocks/form/functions.js` em seu projeto
   - Inclua sua função na declaração de exportação

2. **Implantar e compilar**
   - Confirmar alterações no repositório
   - Garantir que o processo de criação seja concluído com êxito
   - Permitir tempo para atualizações de cache da CDN

3. **Acesso no Editor de Regras**
   - Abrir o Editor de regras para qualquer componente do formulário
   - Selecione **&quot;Saída da Função&quot;** na lista suspensa **Selecionar Ação**
   - Escolha sua função personalizada na lista de funções disponíveis
   - Configurar parâmetros de função usando campos de formulário ou valores estáticos

4. **Testar completamente**
   - Visualize o formulário para verificar o comportamento da função
   - Teste com várias combinações de entrada, incluindo casos de borda
   - Verificar o impacto no desempenho do carregamento e da interação do formulário

![Função personalizada no editor de regras](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Figura: Seleção e configuração de funções personalizadas na interface do Editor de regras

>[!NOTE]
>
> As melhorias no Editor de regras, incluindo regras personalizadas baseadas em eventos, suporte para variáveis dinâmicas e integração de API, também estão disponíveis para o Edge Delivery Services Forms. Para saber mais sobre esses aprimoramentos e como usá-los, consulte o artigo [Aprimoramentos do Editor de regras e Casos de uso](/help/forms/rule-editor-enhancements-use-cases.md).

**Práticas recomendadas para uso de função**:

- **Tratamento de erros**: sempre incluir comportamento de fallback para falhas de função
- **Desempenho**: funções de perfil com volumes de dados realistas
- **Segurança**: validar todas as entradas para evitar vulnerabilidades de segurança
- **Testes**: criar casos de teste que cubram casos normais e de borda

+++


### Importações estáticas para funções personalizadas

O Editor de regras do Editor universal oferece suporte a importações estáticas, permitindo organizar a lógica reutilizável em vários arquivos e formulários. Em vez de manter todas as funções personalizadas em um único arquivo (/blocks/form/functions.js), você pode importar funções de outros módulos.
Por exemplo: Importando Funções de um Arquivo Externo
Considere a seguinte estrutura de pastas:

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

Você pode importar funções de `commonLib/functions.js` para seu arquivo `functions.js` principal conforme mostrado abaixo:

```
`import {days} from './commonLib/functions';
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in String format
 * @param {string} lastname in String format
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

// Export multiple functions for use in Rule Editor
export { getFullName, days};
```

### Organização de funções personalizadas em diferentes Forms

É possível criar diferentes conjuntos de funções em arquivos ou pastas separados e exportá-los conforme necessário:

- Se quiser que determinadas funções estejam disponíveis somente em formulários específicos, forneça o caminho para o arquivo de funções na configuração do formulário.

- Se a caixa de texto do caminho for deixada em branco, o Editor de Regras assumirá como padrão o carregamento de funções de `/blocks/form/functions.js`

![Função personalizada em UE](/help/forms/assets/custom-function-in-ue.png){width=50%}

Na captura de tela acima, o caminho da função personalizada é adicionado na caixa de texto Caminho da função personalizada. As funções personalizadas para este formulário são carregadas do arquivo especificado (`cc_function.js`).

Isso permite flexibilidade ao compartilhar funções em vários formulários ou mantê-las isoladas por formulário.

## Práticas recomendadas para o desenvolvimento de regras


+++ Otimização do desempenho

- Minimize a complexidade das regras; divida uma grande lógica em regras pequenas e focadas
- Ordenar regras por frequência (mais comum primeiro)
- Manter conjuntos de regras por componente gerenciável
- Preferir funções personalizadas reutilizáveis à lógica de duplicação

+++

+++ Experiência do usuário

- Fornecer validação clara e feedback em linha
- Evite alterações visuais estranhas; use mostrar/ocultar cuidadosamente
- Testar em dispositivos e layouts

+++

+++ Higiene do desenvolvimento

- Testar com casos de borda e valores conhecidos
- Verificar entre navegadores
- Intenção de documentos por trás de regras complexas, não apenas mecânica
- Manter um estoque de regras para formulários grandes
- Usar nomenclatura consistente para componentes e regras
- Funções personalizadas de versão e teste em ambientes não relacionados à produção

+++

## Solução de problemas comuns


+++ Regras que não acionam

- Verificar nomes e referências de componentes
- Verificar ordem de execução (de cima para baixo)
- Validar condições com valores conhecidos
- Inspecionar o console do navegador em busca de erros de bloqueio

+++

+++ Comportamento incorreto

- Revisar operadores e agrupamento (E/OU)
- Testar fragmentos de expressão individualmente
- Confirmar tipos de dados (números versus sequências de caracteres)

+++

+++ Problemas de desempenho

- Simplificar condições aninhadas profundamente
- Funções personalizadas de perfil
- Minimizar chamadas externas dentro de regras
- Usar seletores e referências específicos

+++

+++ Problemas de função personalizada

- Confirmar caminho do arquivo: `/blocks/form/functions.js`
- Verifique se as exportações nomeadas estão corretas
- Confirme se a build inclui suas alterações
- Limpar o cache do navegador após a implantação
- Validar tipos de parâmetros e tratamento de erros

+++

+++ Integração do Editor universal

- Confirmar se a extensão Editor de regras está ativada
- Selecione um componente compatível
- Usar um navegador compatível (Chrome, Firefox, Safari)
- Verifique se você tem as permissões necessárias

## Limitações importantes

>[!IMPORTANT]
>
> Restrições de função personalizada:
>
> - Importações estáticas/dinâmicas não são suportadas
> - Toda a lógica deve residir em `/blocks/form/functions.js`
> - As funções devem ser síncronas (sem assíncronas/aguardar ou Promessas)
> - O acesso à API do navegador é limitado

>[!WARNING]
>
> Considerações sobre a produção:
>
> - Testar completamente no preparo
> - Monitorar o desempenho após a implantação
> - Ter um plano de reversão para problemas de regras
> - Considere redes lentas e dispositivos de baixa especificação

## Resumo

O Editor de regras no Universal Editor transforma formulários estáticos em experiências inteligentes e responsivas que se adaptam à entrada do usuário em tempo real. Aproveitando a lógica condicional, os cálculos automatizados e as regras de negócios personalizadas, você pode criar fluxos de trabalho de formulário sofisticados sem gravar o código do aplicativo.

**Principais recursos que você aprendeu**:

- **Lógica condicional**: mostrar e ocultar campos com base na entrada do usuário para criar experiências focalizadas e relevantes
- **Cálculos dinâmicos**: calcule valores automaticamente (impostos, totais, taxas) conforme os usuários interagem com o formulário
- **Validação de dados**: implementar a validação em tempo real com mensagens de comentários claras e acionáveis
- **Funções personalizadas**: estenda os recursos do JavaScript para obter lógicas e integrações de negócios complexas
- **Otimização do desempenho**: aplique as práticas recomendadas para o desenvolvimento eficiente e manutenível de regras

**Valor entregue**:

- **Experiência aprimorada do usuário**: reduza a carga cognitiva com divulgação progressiva e fluxos de formulários inteligentes
- **Erros reduzidos**: evitar envios inválidos por meio da validação em tempo real e da entrada guiada
- **Maior eficiência**: automatize cálculos e entradas de dados para minimizar o esforço do usuário
- **Soluções de manutenção**: crie regras reutilizáveis e bem documentadas que se expandam pela sua organização

**Impacto nos negócios**:

O Forms se torna ferramentas eficientes para a coleta de dados, a qualificação de clientes potenciais e o engajamento do usuário. O Editor de regras permite que autores não técnicos implementem uma lógica de negócios sofisticada, reduzindo os custos de desenvolvimento e, ao mesmo tempo, melhorando as taxas de conclusão de formulários e a qualidade dos dados.

+++

## Próximas etapas

**Caminho de Aprendizado recomendado**:

1. **Comece com as noções básicas**: crie regras simples de mostrar/ocultar para entender os conceitos principais
2. **Prática com tutoriais**: use o exemplo da calculadora de imposto como base para seus próprios formulários
3. **Expanda gradualmente**: adicione expressões matemáticas e regras de validação à medida que sua confiança aumentar
4. **Implementar funções personalizadas**: desenvolver funções do JavaScript para requisitos empresariais especializados
5. **Otimizar e dimensionar**: aplique as práticas recomendadas de desempenho e mantenha a documentação da regra

**Recursos adicionais**:

- [Documentação do Editor Universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) para contexto mais amplo
- [guia do Extension Manager](/help/implementing/developing/extending/extension-manager.md) para habilitar recursos adicionais
- [Edge Delivery Services forms](/help/edge/docs/forms/overview.md) para obter orientação abrangente sobre o desenvolvimento de formulários

