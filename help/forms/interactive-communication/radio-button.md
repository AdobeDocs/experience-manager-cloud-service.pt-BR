---
title: Componente de Botão de opção no Editor de comunicação interativa
description: O componente de Botão de opção no Editor de comunicação interativa no AEM Forms permite que os autores apresentem um conjunto de opções mutuamente exclusivas para os usuários, o que significa que apenas uma opção pode ser selecionada de cada vez.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Componente de Botão de opção no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente **Botão de opção** no editor de IC (comunicação interativa) permite que os autores apresentem um conjunto de opções mutuamente exclusivas para os usuários, o que significa que apenas uma opção pode ser selecionada de cada vez. Isso o torna ideal para casos de uso como perguntas do tipo Sim/Não, seleção de gênero, níveis de classificação ou respostas categóricas predefinidas.
Os botões de opção são intuitivos, fáceis de configurar e podem ser vinculados a modelos de dados de back-end para captura e integração de dados perfeitas.

![Localizar IC Docu](/help/forms/interactive-communication/assets/radio.png)

## &#x200B;2. Propriedades

O componente Botão de opção inclui várias propriedades configuráveis:

2.1. Campo de base

- **Nome:** um identificador exclusivo para o campo. É usado para referência em modelos de dados, regras e lógica de negócios.

- **Alternar:** Permite definir cada opção selecionável no grupo de botões. Cada alternância representa um valor possível.

- **Legenda:** o rótulo associado ao grupo de botões de opção para guiar o usuário.

- **Reservar:** valor de fallback opcional se nenhuma seleção for feita ou a associação de dados estiver vazia.

2.2. Localização

Descrição: controla o posicionamento espacial do grupo de botões de opção no layout.

**Configurações:**

- **Coordenadas X e Y**

- **Altura e Largura** (definido em mm ou % para design de layout responsivo)

2.3. Margem

Defina o espaçamento em torno da caixa de texto:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4. Presença

- **Descrição:** Determina a visibilidade do componente de botão de opção no tempo de execução.

- **Opções:**

   - **Visível:** Exibido para usuários e ocupa espaço.

   - **Oculto (mantém espaço):** Não visível, mas mantém o espaçamento do layout.



2.5. Ligação de dados

- **Descrição:** Conecta o grupo de botões de opção a um modelo de dados para capturar a opção selecionada.

- **Tipos de Associação:**

   - **Nome de Uso:** Usa o nome de campo atribuído como a referência para associação.

   - **Usar Dados Globais:** Associa o campo a um modelo de dados global ou elemento de esquema.

   - **Sem Associação de Dados:** A seleção do botão de opção não está vinculada a nenhuma fonte de dados; usada somente para comportamento de interface do usuário.

## &#x200B;3. Utilização

O componente de Botão de opção é adequado para cenários em que os usuários devem escolher apenas um valor em uma lista. Casos de uso típicos incluem:

- Selecionar um método de comunicação preferencial (Email/Telefone/SMS)

- Confirmação de decisões binárias (Sim/Não)

- Escolha entre opções limitadas (por exemplo, Gênero, Estado civil)

- Indicando níveis de satisfação ou escalas de acordo (por exemplo, Discordo / Neutro / Concordo)

Os autores podem agrupar botões de opção relacionados e posicioná-los dentro de contêineres de layout para um alinhamento consistente. As etiquetas podem ser posicionadas em linha ou acima dos botões, dependendo dos requisitos de design visual.

## &#x200B;4. Práticas recomendadas

- Limite o número de opções a 5 ou menos para evitar sobrecarregar o usuário.

- Use legendas claras e concisas para descrever o que o usuário está selecionando.

- Pré-selecione a opção mais comum ou segura, se apropriado.

- Evite usar botões de opção quando os usuários tiverem permissão para escolher mais de uma opção. Use caixas de seleção.

- Vincule botões de opção diretamente aos nós do esquema ao integrar com modelos de dados de back-end.

- Aplique espaçamento e alinhamento consistentes para maior clareza visual, especialmente em layouts amigáveis para dispositivos móveis.

O componente de Botão de opção no Editor de comunicação interativa é um componente de entrada fundamental que oferece tomada de decisão limpa e estruturada para os usuários finais. Quando configurado com rótulos claros, espaçamento detalhado e vinculação de dados, ele garante a coleta de dados confiável e uma experiência do usuário mais estável para formulários, pesquisas e fluxos de trabalho de integração.


