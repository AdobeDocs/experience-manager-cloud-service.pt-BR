---
title: Componente de Caixa de seleção no Editor de comunicação interativa
description: O componente Caixa de seleção no Editor de comunicação interativa no AEM Forms permite que os usuários façam seleções binárias únicas ou múltiplas (sim/não, verdadeiro/falso).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Componente de Caixa de seleção no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente Caixa de seleção no editor de Comunicação interativa (IC) permite que os usuários façam seleções binárias únicas ou múltiplas (sim/não, verdadeiro/falso). Normalmente usado para termos e condições, preferências, campos de consentimento e opções de participação, fornece uma maneira rápida de capturar entradas booleanas em um formulário de comunicação.

A caixa de seleção oferece suporte a estilos flexíveis, opções de vínculo de dados e regras de visibilidade, tornando-a uma ferramenta leve, mas eficiente, no design de formulários interativos e fáceis de usar.

![Localizar IC Docu](/help/forms/interactive-communication/assets/checkbox.png)

## &#x200B;2. Propriedades

2.1 Campo básico

- **Nome:** um identificador exclusivo usado para fazer referência à caixa de seleção em modelos de dados, regras ou scripts.

- **Alternar:** permite que a caixa de seleção seja ativada/desativada ao ser clicada. Isso pode ser usado no modo simples ou agrupado.

- **Legenda:** o rótulo descritivo exibido ao lado da caixa de seleção, orientando os usuários sobre o que eles estão concordando ou selecionando.

- **Reservar:** texto ou símbolo opcional de espaço reservado mostrado em modos somente leitura ou de fallback quando nenhuma interação é feita.

2.2 Posição

Define onde a caixa de seleção é colocada no layout:

- Coordenadas de **X e Y:** defina o local da caixa de seleção na grade de layout.

- **Altura e Largura:** Define as dimensões da caixa de seleção (em mm ou px), especialmente importantes ao usar ícones ou estilos visuais personalizados.

2.3 Margem

Permite espaçamento ao redor da caixa de seleção para ajustes de layout:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4 Aparência

Controla o estilo visual da caixa de seleção e seu quadro:

- **Preenchimento:** Cor de fundo da caixa de seleção (quando selecionada ou desmarcada).

- **Traço:** a cor de contorno da borda da caixa de seleção.

- **Largura do Traço:** Espessura da linha de borda.

- **Estilo:** padrão de contorno sólido, tracejado ou personalizado.

- **Bordas:** Define o estilo de canto da caixa de seleção: bordas arredondadas ou nítidas, dependendo da preferência de design.

2.5 Presença

Determina como e quando a caixa de seleção é exibida no tempo de execução:

- **Visível:** Exibido normalmente e ocupa espaço.

- **Oculto (mantém espaço):** Oculto da interface do usuário, mas o espaço de layout é mantido. Útil para visibilidade condicional sem quebra de layout.

2.6 Vinculação de dados

Permite que a caixa de seleção interaja com fontes de dados externas ou internas:

**Tipo de Associação de Dados:**

**Nome de Uso:** Associa o valor usando o nome de campo do componente.

**Usar Dados Globais:** Conecta-se a um modelo de dados global compartilhado na comunicação.

**Nenhuma Associação de Dados:** A caixa de seleção permanece independente e não é armazenada no modelo de dados.

&#x200B;3. Utilização

As caixas de seleção geralmente são usadas em cenários como:

- **Campos de consentimento:** por exemplo, &quot;Concordo com os termos e condições&quot;

- **Preferências do usuário:** por exemplo, &quot;Assinar informativo&quot;

- **Várias seleções de opção:** por exemplo, &quot;Selecionar todas as opções aplicáveis&quot;

- **Confirmações de formulário:** por exemplo, &quot;Confirmo que os detalhes acima estão corretos&quot;

As caixas de seleção podem ser colocadas dentro de grades ou painéis de layout e agrupadas para melhorar a organização em formulários.

&#x200B;4. Práticas recomendadas

- Use legendas claras e concisas para ajudar os usuários a entender o que estão selecionando.

- Evite desordem usando caixas de seleção somente para entradas binárias — use botões de opção para opções exclusivas.

- Verifique o espaçamento adequado usando as configurações de margem e layout para uma interface de usuário limpa.

- Vincule as caixas de seleção a uma referência de modelo de dados significativa quando a escolha capturada precisar ser armazenada ou processada.

- Use regras de visibilidade quando as caixas de seleção dependerem de entradas ou condições anteriores.

O componente Caixa de seleção no editor de comunicação interativa é um componente simples, mas essencial para entradas binárias. Com suporte para estilo, presença condicional e vinculação de dados flexível, ele desempenha um papel fundamental no aprimoramento da interatividade e do controle do usuário em formulários digitais inteligentes. Quando implementadas com rótulos elaborados, estilo consistente e integração de dados significativa, as caixas de seleção contribuem significativamente para uma experiência de formulário suave e intuitiva.


