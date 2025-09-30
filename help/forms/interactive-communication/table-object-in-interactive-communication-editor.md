---
title: Objeto de tabela no Editor de comunicação interativa
description: O Table Object no Editor de comunicação interativa no AEM Forms permite que os autores insiram tabelas personalizáveis em modelos de comunicação com facilidade.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---


# Objeto de tabela no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O objeto de tabela no editor de comunicação interativa (IC) permite que os autores insiram tabelas personalizáveis em modelos de comunicação com facilidade. Esse objeto oferece suporte à representação de dados tabulares para casos de uso, como resumos, listas de itens, entrada estruturada ou layouts de comparação.

Os autores podem arrastar e soltar o componente de tabela na tela, configurar o número de linhas e colunas e escolher opções como incluir linhas de cabeçalho e rodapé ou definir a direção do layout. As tabelas podem ser definidas como modelos padrão para consistência em várias comunicações.

![Localizar IC Docu](/help/forms/interactive-communication/assets/table.png)

## &#x200B;2. Propriedades

O Objeto de tabela inclui várias propriedades configuráveis para ajudar os autores a personalizar o comportamento e a aparência da tabela:


2.1 Campo básico

- **Nome:** Um identificador exclusivo para a tabela. Esse nome é usado internamente para fazer referência à tabela nos modelos e na lógica de dados.

- **Linhas:** Especifica o número de linhas de conteúdo (excluindo o cabeçalho e o rodapé).

- **Colunas:** Define o número de colunas na tabela.

- **Linha de Cabeçalho:** Opção para incluir uma linha de cabeçalho na parte superior da tabela para rótulos de coluna.

- **Linha de Rodapé:** Opção para incluir uma linha de rodapé para valores totais ou resumidos.

- **Definir como Padrão:** Permite que os usuários salvem a configuração atual como um modelo de tabela padrão para uso futuro.

- **Direção de Layout:** Define como as linhas são preenchidas — normalmente definido como Da Esquerda para a Direita.

2.2 Posição

- **Descrição:** Controla o posicionamento da tabela no layout.

- **Configurações:**

   - Coordenadas de **X e Y:** define as posições horizontal (X) e vertical (Y) da tabela na tela.

   - **Altura e Largura:** Define o tamanho geral da tabela (em mm), permitindo a alocação flexível de espaço.

2.3 Aparência

**Aparência:** define o estilo visual da tabela. Os autores podem escolher entre predefinições predefinidas, como bordada, plana ou elevada.

- **Preenchimento:** Cor do plano de fundo da(s) tabela(s).

- **Traço:** Cor da borda ao redor da tabela ou de células específicas.

- **Largura:** Espessura das linhas de borda.

- **Estilo:** escolha os tipos de borda: cantos arredondados ou cantos nítidos.

- **Bordas:** configure a visibilidade das bordas da célula e do raio do canto.

2.4 Presença

- **Descrição:** Determina a visibilidade da tabela no tempo de execução.

- **Opções:**

   - **Visível:** Exibir a tabela normalmente na saída.

   - **Oculto:** oculta a tabela, mas mantém espaço dentro do layout.

2.5 Vinculação de dados

**Associação de Dados:** conecte a tabela a uma fonte de dados (por exemplo, JSON, esquema XML) para preencher dinamicamente linhas e colunas com valores durante a geração. Isso é útil para faturamento discriminado, registros de transação ou listagens de produtos.

## &#x200B;3. Utilização

O objeto de tabela é ideal para exibir informações estruturadas ou repetitivas. Casos de uso típicos incluem:

- Faturas e listas com linhas de item

- Comparações de políticas ou planos

- Resumos de dados do perfil ou da conta

- Catálogos de produtos ou matrizes de recursos

Os autores podem configurar o número de linhas e colunas, aplicar visibilidade condicional ou vincular dados para exibir informações dinâmicas.

## &#x200B;4. Práticas recomendadas

- Use linhas de cabeçalho para rotular claramente cada coluna para melhorar a leitura.

- Aplique linhas de rodapé para totais ou notas importantes, onde aplicável.

- Aproveite a vinculação de dados para preencher linhas dinamicamente com base em entrada estruturada.

- Mantenha um estilo e um espaçamento consistentes usando as configurações de aparência e margem.

- Ao ocultar uma tabela, garanta a continuidade do layout escolhendo se deseja ou não manter espaço.

- Use modelos padrão para padronizar o conteúdo tabular em documentos.

O Table Object no editor IC é um componente flexível e fácil de usar, projetado para suportar conteúdo estruturado em suas comunicações. Com opções de layout personalizáveis, recursos de estilo e uma poderosa vinculação de dados, ele permite que os autores apresentem as informações de forma clara e eficaz.


