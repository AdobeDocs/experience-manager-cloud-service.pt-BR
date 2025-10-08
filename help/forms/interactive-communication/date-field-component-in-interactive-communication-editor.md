---
title: Objeto de campo de data no Editor de comunicação interativa
description: O objeto de campo de data no Editor de comunicação interativa no AEM Forms permite que os autores insiram um campo de seleção de data com base no calendário em um documento.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Objeto de campo de data no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente **Campo de data** no editor de IC (Comunicação interativa) permite que os autores insiram um campo de seleção de data com base em calendário em um documento. Isso permite que os usuários escolham facilmente uma data em um seletor de datas ou a insiram manualmente em um formato predefinido.

Ideal para capturar datas de nascimento, agendamentos de compromissos, datas de aplicação ou datas de início/término da política, o Campo de data melhora a precisão e reduz erros de entrada. Ele oferece suporte a formatação, estilo e vinculação de dados para integração perfeita com modelos de dados e sistemas de back-end.

![Localizar IC Docu](/help/forms/interactive-communication/assets/date.png)

## &#x200B;2. Propriedades

O objeto de Campo de data inclui várias propriedades configuráveis:

2.1. Campo de base

- **Nome:** um identificador exclusivo usado para fazer referência ao campo em regras, scripts e modelos de dados.

- **Legenda:** o rótulo de exibição mostrado ao usuário (por exemplo, &quot;Data de Nascimento&quot;).

- **Data:** o valor de data real, que pode estar vazio por padrão ou pré-preenchido com dados dinâmicos.

- **Reservar:** uma data de fallback opcional (exibida se nenhuma data estiver selecionada ou se os dados não estiverem disponíveis).

- **Aparência:** uma predefinição rápida de estilo (por exemplo, sublinhado, plano, bordado) para consistência visual.

2.2. Tipografia

Controla como a data aparece visualmente no campo:

- **Variação de fonte:** escolha família de fontes, peso (por exemplo, Regular, Negrito) e estilo (por exemplo, Itálico).

- **Tamanho:** normalmente definido como 10 pt por padrão, mas personalizável para consistência com o conteúdo ao redor.

2.3. Localização

Define o posicionamento espacial no layout do documento:

- Coordenadas de **X e Y:** determina o posicionamento horizontal e vertical.

- **Largura e Altura:** Definido em milímetros ou porcentagens para alinhar com outros elementos de formulário.

2.4. Margem

Especifica o espaçamento ao redor dos limites do campo:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

Esses valores ajudam com o alinhamento preciso em subformulários ou grades de layout.

2.5. Aspecto

Define o estilo visual do contêiner de campo:

- **Preenchimento:** Cor de fundo do campo (por exemplo, branco, cinza claro).

- **Traço:** Cor ou contorno da borda.

- **Largura:** Espessura da borda do campo.

- **Estilo:** opções de linha sólida, tracejada ou pontilhada.

- **Bordas:** personalize cantos como arredondados ou nítidos para preferências de design diferentes.

2.6. Presença

Determina como e quando o campo é exibido:

- **Visível:** Configuração padrão em que o campo é exibido em tempo de execução.

- **Oculto (mantém espaço):** O campo permanece invisível, mas o espaço de layout é preservado.

Isso é útil ao alternar a visibilidade dinamicamente com base na entrada do usuário ou nas regras.

2.7. Vinculação de dados

Conecta o Campo de data às estruturas de dados para armazenar ou preencher previamente os valores.

**Tipo de Associação de Dados:**

- **Nome de Uso:** Associa o campo ao esquema usando seu atributo de nome.

- **Usar Dados Globais:** Associações que usam um modelo de dados ou elemento de esquema predefinido.

- **Sem Associação de Dados:** O campo permanece estático, não está conectado a nenhuma fonte de dados.

Isso permite que os valores de data dinâmicos sejam buscados, exibidos ou armazenados com base na lógica do aplicativo.

## &#x200B;3. Utilização

O Campo de data é particularmente útil nos seguintes cenários:

- Captura da data de nascimento ou data de adesão nos formulários de integração.

- Seleção de datas de início e término para serviços, assinaturas ou eventos.

- Inserção de prazos de inscrição, espaços para compromissos ou datas de verificação.

Os autores podem colocar o Campo de data dentro de contêineres ou subformulários de layout e configurar a validação (por exemplo, formato de data, limites de intervalo) para melhorar a qualidade dos dados.

## &#x200B;4. Práticas recomendadas

- Use legendas ocultas como &quot;Data inicial&quot; ou &quot;Selecionar data de compromisso&quot; para melhor UX.

- Defina intervalos de datas mínimos e máximos para evitar entrada inválida (por exemplo, DOB futuro).

- Aplique estilos de fonte consistentes (recomenda-se 10 pt) para facilitar a leitura.

- Vincule campos ao esquema sempre que for necessária a integração de dados de back-end.

- Ocultar campos de data não relevantes dinamicamente usando regras de visibilidade.

O objeto **Campo de data** no editor de comunicação interativa é uma ferramenta poderosa para capturar dados sensíveis ao tempo com precisão e facilidade. Quando estilizado cuidadosamente e conectado a caminhos de dados significativos, ele oferece suporte a uma experiência perfeita do usuário e ao processamento eficiente de entradas baseadas em tempo.


