---
title: Objeto de código de barras no Editor de comunicação interativa
description: O objeto de código de barras no Editor de comunicação interativa no AEM Forms permite que os autores representem visualmente dados codificados em modelos de comunicação.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Objeto de código de barras no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O objeto Código de barras no editor de comunicação interativa permite que os autores representem visualmente dados codificados em modelos de comunicação. Isso é particularmente útil para aplicativos que envolvem rastreamento, identificação, faturamento ou automação. Com suporte para vários padrões de código de barras, como Código 128, QR e outros, esse componente oferece opções flexíveis de estilo, posicionamento e vinculação de dados para atender a uma grande variedade de necessidades comerciais.

Quer você esteja criando faturas de clientes, etiquetas de remessa ou cartões de associação, o objeto do Código de barras simplifica o processo, incorporando dados legíveis por computador diretamente no seu documento.

![Localizar IC Docu](/help/forms/interactive-communication/assets/barcode.png)

## &#x200B;2. Propriedades

O objeto de código de barras vem com um conjunto abrangente de opções configuráveis para controlar seu comportamento e aparência:

2.1 Campo básico

**Nome:** Um identificador exclusivo para o código de barras. É usado para fazer referência ao objeto em modelos de dados e conjuntos de regras.

**Local:** Especifica onde o texto do código de barras é exibido em relação ao símbolo de código de barras.

**Opções:**

- **Nenhum:** oculta o texto.

- **Acima:** Exibe o texto acima do código de barras.

- **Abaixo:** Exibe o texto abaixo do código de barras.

- **Acima Incorporado:** Incorpora o texto dentro da área superior do código de barras.

- **Abaixo Incorporado:** Incorpora o texto dentro da área inferior do código de barras.

- **Tipo:** Especifica o padrão de código de barras (por exemplo, Código 128, Código 39, Código QR, etc.).

- **Padrão:** um valor predefinido que aparece se nenhum dado for fornecido.

- **Comprimento dos Dados:** Indica o número máximo ou esperado de caracteres que o código de barras pode conter.

- **Soma de verificação:** valida a precisão dos dados de código de barras.

   - **Opções:**

      - **Nenhum:** Nenhuma validação de soma de verificação.

      - **Automático:** Calcula automaticamente a soma de verificação com base no tipo.

- **Proporção ampla/estreita:** Define a largura relativa das barras largas para as estreitas (usadas em alguns códigos de barras 1D).

2.2 Localização

Determina onde o código de barras aparece em relação ao conteúdo:

- **Nenhum:** Nenhum posicionamento adicional.

- **Acima:** Coloca o código de barras acima do conteúdo relacionado.

- **Abaixo:** Coloca o código de barras abaixo do conteúdo.

- **Acima Incorporado:** O código de barras está incorporado e flutua acima do conteúdo.

- **Abaixo Incorporado:** Inserido abaixo do conteúdo.

2.3 Posição

Define o posicionamento exato do código de barras no layout:

- Coordenadas de **X e Y:** posicione o código de barras dentro do formulário usando unidades milimétricas.

- **Altura e Largura:** Defina as dimensões físicas do código de barras.

2.4 Margem

Adiciona espaçamento ao redor do código de barras para uma melhor separação visual:

- Superior

- Parte inferior

- Esquerda

- Direita

Essas margens ajudam na consistência do layout e na legibilidade.

Aparência 2.5

Personalizar o estilo visual do código de barras:

- **Preenchimento:** Cor do plano de fundo da área do código de barras.

- **Traço:** Cor da borda.

- **Largura:** Define a espessura das linhas de código de barras.

- **Estilo:** escolha entre predefinições como simples, bordada ou elevada.

- **Bordas:** Decida entre cantos arredondados ou nítidos para a caixa de código de barras.

2.6 Presença

Controla se o código de barras está visível ou oculto no tempo de execução:

- **Visível:** O código de barras é mostrado na saída final.

- **Oculto:** O espaço é reservado, mas o código de barras não é exibido.

2.7 Vinculação de dados

Vínculo de dados: conecta o código de barras a um modelo de dados de back-end (XML ou JSON). Isso garante que o código de barras reflita dinamicamente dados exclusivos por instância do documento, como uma ID de pedido ou um número de rastreamento.

## &#x200B;3. Utilização

O objeto de código de barras é particularmente útil ao automatizar processos que dependem de dados digitalizados. Ele pode ser adicionado aos modelos de comunicação, como:

- Faturas (para referência de cliente e pagamentos de verificação rápida)

- Etiquetas de remessa (para rastreamento de pacotes)

- Cartões de participação ou de fidelidade (para identificação com base em digitalização)

- Cupons e vouchers (para validação no ponto de venda)

Os autores podem incorporar o código de barras em contêineres de layout e estilizá-lo de acordo com a marca ou o tema do documento.

## &#x200B;4. Práticas recomendadas

- Use um tipo de código de barras apropriado para o caso de uso, por exemplo, Código QR para URLs, Código 128 para IDs alfanuméricas.

- Valide a legibilidade do código de barras imprimindo versões de teste e digitalizando-as.

- Garanta a integridade dos dados usando a opção de soma de verificação se o padrão do código de barras permitir.

- Escolha tamanhos legíveis e larguras de linha para evitar problemas de digitalização.

- Mantenha margens adequadas para evitar recorte quando impresso.

O objeto de código de barras no Editor de comunicação interativa permite que os criadores de documentos preencham a lacuna entre sistemas digitais e físicos. Quando implementado de maneira eficaz, ele aprimora a automação, melhora a conveniência do usuário e oferece suporte à integração perfeita com dispositivos e fluxos de trabalho de digitalização.
