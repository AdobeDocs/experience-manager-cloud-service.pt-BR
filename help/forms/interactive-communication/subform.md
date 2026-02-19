---
title: Componente de Subformulário no Editor de comunicação interativa
description: O componente de Subformulário no Editor de comunicação interativa no AEM Forms permite organizar vários elementos de formulário de maneira flexível e estruturada.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 60809974-1a39-4e69-9aa5-df9936a26362
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Componente de Subformulário no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

## &#x200B;1. Introdução

O componente **Subformulário** no editor de IC (Comunicação Interativa) atua como um contêiner de layout dinâmico que permite organizar vários elementos de formulário de maneira flexível e estruturada. Normalmente, é usado para agrupar campos relacionados, criar seções de repetição ou definir estruturas de dados aninhadas para melhorar a experiência do usuário e a associação de dados.

Os subformulários podem ser configurados para fluir em diferentes layouts, como de cima para baixo ou da esquerda para a direita, tornando-os ideais para designs de formulários complexos e seções reutilizáveis.

![Localizar IC Docu](/help/forms/interactive-communication/assets/subform.png)

## &#x200B;2. Propriedades

2.1 Propriedades básicas

- **Nome:** um identificador exclusivo para o subformulário usado em referências, modelos de dados e regras de negócios.

- **Conteúdo:** Define como os elementos dentro do subformulário são organizados.

   - **Posicionado:** Posicionamento absoluto de elementos filho usando coordenadas X e Y.

   - **Fluxo (De Cima para Baixo):** Organiza os elementos verticalmente.

   - **Fluxo (Da Esquerda para a Direita):** Organiza os elementos horizontalmente.

2.2 Posição

- **Descrição:** Determina o posicionamento do subformulário no layout de comunicação.

- **Configurações:**

   - Coordenadas X e Y (em mm)

   - Largura e altura (em mm)

2.3 Aparência

- **Preenchimento:** Especifica a cor do plano de fundo da área do subformulário.

- **Traço:** Define a cor da borda.

- **Largura:** Define a espessura da borda.

- **Estilo:** escolha entre predefinições visuais como plano, bordado ou elevado.

- **Bordas:** determina o estilo do canto — arredondado ou nítido.

2.4 Presença

- **Descrição:** Controla a visibilidade do subformulário durante o tempo de execução.

- **Opções:**

   - **Visível:** Sempre exibido.

   - **Oculto:** Não exibido, mas o espaço é mantido no layout.

2.5 Vinculação de dados

- **Tipo de Associação de Dados:** Vincula o subformulário a uma estrutura de dados (geralmente XML ou JSON).

- **Nome de Uso:** Associa dados usando o nome atribuído do subformulário.

- **Usar Dados Globais:** Conecta o subformulário a um caminho de esquema global para uso de dados compartilhados.

- **Sem Associação de Dados:** O subformulário não armazena nem interage com nenhum modelo de dados externo.

## &#x200B;3. Utilização

Subformulários são vitais em cenários que exigem agrupar, aninhar ou repetir conjuntos de campos. As aplicações típicas incluem:

- Organizar blocos de endereço (por exemplo, Rua, Cidade, CEP)

- Seções repetitivas para itens de linha ou várias entradas

- Estruturação da lógica de forma condicional usando visibilidade e regras
Os subformulários também podem ser usados como contêineres para o alinhamento do design de arrastar e soltar em layouts estáticos e dinâmicos.

## &#x200B;4. Práticas recomendadas

- Escolha o layout certo (fluido vs. posicionado) com base no design e nas necessidades de dados.

- Use nomes significativos para facilitar a integração de dados e a referência de regras.

- Subformulários de estilo para distinguir visualmente seções agrupadas.

- Ao usar subformulários de repetição, verifique a vinculação de dados adequada às estruturas de matriz.

- Aplique regras de visibilidade condicional para otimizar a experiência do usuário em formulários complexos.

O componente **Subformulário** no editor de comunicação interativa fornece uma maneira poderosa de estruturar e controlar layouts de formulário complexos. Seja organizando campos de entrada, gerenciando conteúdo dinâmico ou habilitando design modular, os subformulários melhoram a usabilidade e a capacidade de manutenção em todos os modelos de documento.
