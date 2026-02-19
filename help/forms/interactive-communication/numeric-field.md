---
title: Componente de campo numérico no editor de comunicação interativa
description: Componente de campo numérico no Editor de comunicação interativa no AEM Forms para permitir que os autores coletem entradas numéricas dos usuários em um formato controlado.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 1f6bda20-7bce-4cfd-9985-f8b49d6e50e0
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Componente de campo numérico no editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

## &#x200B;1. Introdução

O componente Campo numérico no editor de IC (Comunicação interativa) permite que os autores coletem entradas numéricas dos usuários em um formato controlado. Seja capturando números de telefone, códigos PIN, IDs de política ou números financeiros, esse campo garante que somente valores numéricos sejam aceitos. O componente também oferece suporte a estilo, formatação, validação e vinculação de dados, tornando-o essencial para comunicações estruturadas.

![Localizar IC Doc](/help/forms/interactive-communication/assets/numericfield.png)

## &#x200B;2. Propriedades

2.1 Campo básico

- **Nome:** Defina um identificador exclusivo para o campo, usado em modelos de dados, regras e scripts.

- **Legenda:** Exibir o rótulo na tela mostrado aos usuários (por exemplo, &quot;Número de Contato&quot; ou &quot;ID de Funcionário&quot;).

- **Valor:** permite que os usuários insiram entradas numéricas, como números de telefone, IDs, quantidades ou valores monetários.

- **Reserva:** Defina o alinhamento do valor numérico (esquerda, direita, superior ou inferior) ou especifique uma posição personalizada usando unidades como milímetros (por exemplo, 20 mm).

- **Aparência:** Defina a aparência da caixa de valor como Nenhum, Caixa Sólida ou Sublinhado com base no layout visual desejado.

2.2 Tipografia

Controla o estilo visual dos caracteres numéricos inseridos pelo usuário:

- **Validação de Fontes:** aplique restrições para garantir que apenas entradas numéricas válidas sejam aceitas, como números inteiros, decimais ou intervalos numéricos, de acordo com o tipo de dados pretendido.

- **Tamanho da Fonte:** Ajuste o tamanho do texto numérico usando valores de ponto como 10 pt, 12 pt ou 20 pt para manter a consistência e a legibilidade no formulário.

2.3 Posição

Controla o posicionamento espacial do campo numérico na tela de desenho.

- Coordenadas de **X e Y:** defina o posicionamento exato do campo.

- **Largura e Altura (em mm):** Determina o tamanho da caixa de entrada.

2.4 Margem

Define o espaçamento ao redor do limite do campo numérico para um alinhamento limpo.

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

Aparência 2.5

Estila o contêiner do campo de entrada numérico para corresponder ao layout visual desejado:

- **Preenchimento:** Defina a cor de plano de fundo do campo numérico. Isso ajuda a separá-lo visualmente de outros elementos ou combiná-lo com o tema geral.

- **Traço:** Adicione bordas ao redor do campo numérico com as seguintes opções personalizáveis:

- **Largura:** Defina a espessura da borda para atender à ênfase visual.

- **Estilo:** Escolha um padrão de borda—sólido, tracejado ou pontilhado.

- **Edge:** selecione entre cantos arredondados ou nítidos para a borda.

- **Raio:** Ajuste o arredondamento do canto usando valores de raio específicos (por exemplo, 4 px, 10 px) para suavizar ou afiar a aparência do campo.

2.6 Presença

Controla a visibilidade do campo numérico durante o tempo de execução.

- **Visível:** Estado padrão; o campo é exibido normalmente.

- **Oculto (mantém espaço):** O campo é invisível, mas o espaço é mantido no layout.

2.7 Vinculação de dados

**Tipo de Associação de Dados:** Conecta o campo numérico a uma fonte de dados (XML ou JSON) para integração em tempo real.

**Usar Nome:** Associa o campo ao seu nome exclusivo para captura de valor simples.

**Usar dados globais:** vincula o campo a um nó de dados compartilhado em formulários ou fragmentos.

**Nenhuma Associação de Dados:** Mantém o campo estático para uso apenas visual ou entrada temporária.

## &#x200B;3. Utilização

Os campos numéricos são ideais em cenários nos quais apenas dígitos são entradas válidas. Casos de uso comuns incluem:

- Capturando **números de celular, OTPs e PINs**

- Inserindo **números de política ou IDs de funcionário**

- Coletando **quantidades numéricas ou valores monetários**

- Habilitando **campos de números baseados em etapas** (por exemplo, contadores ou entradas de pontuação)

Os autores podem colocar campos numéricos dentro de contêineres ou subformulários de layout e aplicar validação (como restrições de comprimento, mínimo ou valor máximo) para melhorar a qualidade dos dados.

## &#x200B;4. Práticas recomendadas

- Identifique claramente os campos numéricos com unidades, se necessário (por exemplo, &quot;Valor em Rum&quot;).

- Aplique a validação de formato (como limites de 10 dígitos para números de telefone) para melhorar a precisão.

- Use valores de reserva quando os campos forem obrigatórios, mas os dados dinâmicos puderem estar ausentes.

- Associe campos numéricos cuidadosamente a caminhos de esquema para suportar o processamento de backend.

- Mantenha a aparência e a tipografia consistentes para corresponder às diretrizes da marca.

O componente **Campo Numérico** no editor de Comunicação Interativa é uma ferramenta precisa e confiável para coleta de dados baseada em dígitos. Com formatação robusta, controles de visibilidade e opções de vinculação de dados, ele garante que as entradas numéricas sejam capturadas de forma limpa e perfeitamente integradas a formulários digitais. Quando estilizado e configurado corretamente, ele melhora significativamente a usabilidade do formulário e a precisão geral dos dados.
