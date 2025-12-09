---
title: Componente de linha no editor de comunicações interativas
description: O componente de linha no Editor de comunicação interativa no AEM Forms permite que os autores insiram linhas horizontais ou verticais em um layout de comunicação.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Componente de linha no editor de comunicações interativas

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente de Linha no editor de Comunicação interativa (IC) permite que os autores insiram linhas horizontais ou verticais em um layout de comunicação. Essas linhas ajudam a segmentar visualmente o conteúdo, melhorar a legibilidade ou enfatizar a estrutura do formulário. Com estilos personalizáveis, como linhas sólidas ou sublinhados e posicionamento flexível, o componente de linha pode ser usado para fins funcionais e estéticos no design do formulário.

![Localizar IC Docu](/help/forms/interactive-communication/assets/line.png)

## &#x200B;2. Propriedades

O componente de Linha vem com uma variedade de propriedades configuráveis para definir sua identidade, aparência, posicionamento e visibilidade no documento.

2.1. Campo de base

- **Nome:** um identificador exclusivo usado internamente para fazer referência ao componente de linha em modelos de dados, regras ou scripts.

- **Tipo de Aparência:** Selecione como a linha aparece dentro do formulário.

   - **Nenhuma:** nenhuma linha é exibida.

   - **Caixa Sólida:** Renderiza a linha como uma caixa sólida, geralmente usada como separador.

   - **Sublinhado:** Desenha um sublinhado geralmente usado abaixo de cabeçalhos ou campos.

2.2. Localização

- **Descrição:** Define o posicionamento físico da linha no layout do formulário.

- **Configurações:**

   - Coordenadas de **X e Y:** especifica o posicionamento horizontal e vertical.

   - **Altura e Largura:** Defina o comprimento e a espessura da linha (em mm).

2.3. Margem

- **Descrição:** Adiciona preenchimento ou espaçamento ao redor do componente de linha para controlar a densidade do layout.

- **Opções:**

   - Superior

   - Parte inferior

   - Esquerda

   - Direita

2.4. Aspecto

- **Descrição:** Permite que o estilo da linha corresponda ao design do documento.

- **Opções:**

   - **Traço:** Define a cor e a espessura do traçado de linha.

   - **Largura:** Determina a largura da linha ao longo do formulário.

   - **Estilo:** escolha entre os estilos de linha tracejada, pontilhada ou sólida.

2.5. Presença

- **Descrição:** Controla a visibilidade do componente de linha durante o tempo de execução.

- **Opções:**

   - **Visível:** a linha é renderizada na saída final.

   - **Oculto:** A linha não é exibida, mas seu espaço de layout é preservado.

## &#x200B;3. Utilização

O componente de linha é frequentemente usado para:

- Dividir seções visualmente em um formulário longo

- Sublinhar cabeçalhos ou rótulos para ênfase

- Criar bordas ou caixas ao redor de grupos de campos

- Melhorar a hierarquia visual do layout de comunicação

## &#x200B;4. Práticas recomendadas

- Use estilos de linha consistentes em todo o formulário para manter uma aparência profissional.

- Ajuste as margens para evitar confusão visual e garantir alinhamento.

- Escolha as configurações de traçado e estilo adequadas para corresponder ao design da marca ou do documento.

- Ocultar linhas desnecessárias para evitar distração e preservar o espaçamento do layout.

O componente de linha no editor de comunicação interativa é um elemento de design simples, mas eficiente. Quando usado estrategicamente, ele melhora a estrutura visual dos documentos de comunicação, ajudando os usuários a navegar melhor pelo conteúdo e garantindo um layout mais limpo e polido.


