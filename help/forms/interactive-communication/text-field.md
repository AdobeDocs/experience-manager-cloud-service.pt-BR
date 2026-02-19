---
title: Componente Campo de texto no Editor de comunicação interativa
description: O componente Campo de texto no Editor de comunicação interativa no AEM Forms para permitir que os autores exibam informações como nomes, endereços, comentários ou IDs numéricas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 6bb41cf2-8a9d-499c-979b-b0ee7d092e11
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# Componente Campo de texto no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

## &#x200B;1. Introdução

O componente Campo de texto no editor de IC (comunicação interativa) permite que os autores exibam informações como nomes, endereços, comentários ou IDs numéricas. O valor mostrado no campo de texto é predefinido (estático) ou preenchido dinamicamente usando a vinculação de dados. Ele oferece suporte a entradas de linha única, regras de validação e formatação flexível, tornando-o um dos elementos mais usados e versáteis em comunicações personalizadas.

![Localizar IC Doc](/help/forms/interactive-communication/assets/textfield.png)

## &#x200B;2. Propriedades

2.1 Campo básico

- **Nome:** Defina um identificador exclusivo para o campo, usado em modelos de dados, regras e scripts.

- **Legenda:** exibe o rótulo na tela mostrado aos usuários (por exemplo, &quot;Nome&quot;).

- **Valor:** Exibir texto como nomes, endereços, comentários ou outros detalhes. O valor é estático ou derivado da associação de dados.

- **Reserva:** Defina o alinhamento do valor, esquerda, direita, superior ou inferior ou especifique uma posição personalizada usando unidades como milímetros (por exemplo, 20 mm).

- **Aparência:** Defina a aparência da caixa de valor como Nenhum, Caixa Sólida ou Sublinhado com base no layout visual desejado.

2.2 Tipografia

Controla o estilo visual dos caracteres digitados:

- **Validação de Fontes:** aplique restrições opcionais para validar o formato do valor exibido, como permitir somente letras, números ou padrões personalizados específicos.

- **Tamanho da Fonte:** Ajuste o tamanho do texto dentro do campo usando valores de ponto como 10 pt, 12 pt, 20 pt etc. para garantir legibilidade e alinhamento com os padrões de design.

2.3 Posição

Define o posicionamento do campo no layout:

- **Coordenadas X/Y**

- **Largura e Altura** (mm, px ou %)

2.4 Margem

Especifica o espaçamento em torno do contêiner de campo:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

Aparência 2.5

Estila o próprio contêiner de campo:

- **Preenchimento:** Defina a cor de fundo da caixa de texto. Isso ajuda a distinguir as áreas de entrada ou alinhá-las com as cores da marca.

- **Traço:** Adicione bordas ao redor da caixa de texto com as seguintes propriedades personalizáveis:

- **Largura:** Defina a espessura da borda.

- **Estilo:** escolha entre estilos de borda sólida, tracejada ou pontilhada.

- **Edge:** Selecione a forma dos cantos — arredondada ou nítida.

- **Raio:** Ajuste a curvatura do canto usando valores de raio (por exemplo, 4 px, 10 px) para obter uma aparência mais suave ou mais angular.

2.6 Presença

Determina a visibilidade no tempo de execução:

- **Visível:** Mostrado e ocupa espaço

- **Oculto (mantém espaço):** Invisível, mas o espaço de layout é reservado

2.7 Vinculação de dados

Vincula o campo de texto a uma fonte de dados para exibir valores de forma dinâmica ou estática na comunicação.

- **Tipo de Associação de Dados:** Especifica como o campo se conecta a uma fonte de dados ou esquema.

- **Nome de Uso:** Associa o campo de texto usando o nome de campo definido no modelo de dados ou esquema, permitindo a exibição de texto dinâmico com base em dados externos.

- **Usar Dados Globais:** Conecta o campo a dados globais que são compartilhados em toda a comunicação para exibição consistente de informações.

- **Nenhuma Associação de Dados:** Mantém o campo desvinculado de qualquer origem de back-end. É usado para exibir valores estáticos ou texto destinado apenas ao contexto visual.

## &#x200B;3. Utilização

Cenários comuns incluem:

- Captura de detalhes pessoais (nomes, endereços, números de telefone)

- Aceitar comentários ou comentários (várias linhas)

- Inserção de números de apólices ou IDs de conta

- Coleta de valores numéricos curtos, como códigos PIN ou OTPs

Os autores podem colocar o campo em subformulários ou grades de layout para alinhamento e anexar regras de validação (limites de comprimento, padrões regex) para garantir uma entrada limpa.

## &#x200B;4. Práticas recomendadas

- Aplique a validação (sinalizadores obrigatórios, verificações de padrão) para feedback imediato.

- Fornece texto de Reserva significativo para exibições impressas ou somente leitura.

- Mantenha a tipografia consistente com as diretrizes da marca.

- Reduza a largura do campo em layouts móveis para ajustá-los a telas menores.

- Associe-se diretamente ao modelo de dados sempre que possível para obter uma manutenção mais simples.

O componente Campo de texto no editor IC é um elemento versátil que simplifica a captura de dados. Quando configurado cuidadosamente, com tipografia bem escolhida, rótulos claros, validação adequada e sólida ligação de dados, ele oferece uma experiência contínua e fácil de usar, além de dados confiáveis para processamento downstream.
