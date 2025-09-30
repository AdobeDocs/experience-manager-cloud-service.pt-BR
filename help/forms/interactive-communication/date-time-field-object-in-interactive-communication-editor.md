---
title: Objeto de campo de data/hora no Editor de comunicação interativa
description: Objeto de campo de data/hora no Editor de comunicação interativa no AEM Forms para permitir que os autores insiram campos em que os usuários podem selecionar ou inserir valores de data e/ou hora.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Objeto de campo de data/hora no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente **Campo de Data/Hora** no editor de IC (Comunicação Interativa) permite que os autores insiram campos em que os usuários podem selecionar ou inserir valores de data e/ou hora. Esse componente é normalmente usado para capturar informações como data de nascimento, horários de compromisso, slots de reserva ou datas de emissão/expiração de documentos.

O campo oferece suporte a várias opções de formatação (por exemplo, formatos DD/MM/AAAA, 24 horas ou 12 horas), restrições de validação e personalização da aparência para corresponder ao design da comunicação. Ele melhora a experiência do usuário ao reduzir erros manuais de entrada e promover consistência na coleta de dados.

![Localizar IC Docu](/help/forms/interactive-communication/assets/datetime.png)

## &#x200B;2. Propriedades

O objeto do Campo de data/hora inclui várias propriedades configuráveis:

2.1. Campo de base

- **Nome:** um identificador exclusivo para o campo. Usado para referência em regras, expressões e associações de dados.

- **Legenda:** o rótulo exibido ao lado do campo para indicar sua finalidade (por exemplo, &quot;Data de Nascimento&quot;).

- **Data:** permite que os usuários escolham ou insiram uma data de calendário.

- **Hora:** Habilita a entrada ou a seleção de valores de hora específicos, se configurada.

- **Reserva:** um valor de fallback exibido quando nenhuma entrada é fornecida; útil para cenários somente leitura ou de impressão.

- **Aparência:** selecione um estilo visual, como sublinhado, bordado ou plano, para renderização consistente da interface do usuário.

2.2. Tipografia

Controla o estilo do texto dentro do campo de data/hora:

- **Variação de fonte:** As opções incluem Regular, Negrito, Itálico, dependendo dos requisitos do tema.

- **Tamanho da fonte:** Padrão definido como 10 pt para manter a consistência com o layout do formulário.

2.3. Localização

- **Descrição:** Define o posicionamento do campo de data/hora no layout do formulário.

- **Configurações:**

   - **Coordenadas X e Y**

   - **Altura e largura** (medidas em mm ou pixels) para dimensionar o campo com precisão.

2.4. Margem

Define o espaçamento em torno do campo para obter alinhamento limpo e flexibilidade de layout:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.5. Aspecto

Define o estilo do contêiner para manter a consistência visual e a clareza:

- **Preenchimento:** Cor de fundo do campo.

- **Traço:** Cor da borda ao redor do campo.

- **Largura:** Espessura da borda.

- **Estilo:** tipos de borda como sólida, tracejada ou nenhuma.

- **Arestas:** escolha entre cantos arredondados ou afiados, dependendo do tema do formulário.

2.6. Presença

Determina como o campo se comporta no tempo de execução:

- **Visível:** o campo é mostrado aos usuários e ocupa espaço de layout.

- **Oculto (mantém espaço):** O campo não está visível, mas o espaço reservado ainda está no layout.

2.7. Vinculação de dados

Vincula o campo a uma fonte de dados para armazenar ou recuperar valores.

- **Tipo de Associação de Dados:** Especifica como o campo se conecta aos dados.

- **Nome de Uso:** Associa o campo usando o nome de campo definido no esquema.

- **Usar dados globais:** Conecta o campo aos dados de nível global compartilhados na comunicação.

- **Sem Associação de Dados:** O campo não está conectado a nenhum dado de back-end (usado apenas para valores visuais ou calculados).

## &#x200B;3. Utilização

O Campo de data/hora é ideal em cenários nos quais dados temporais consistentes são necessários. Casos de uso comuns incluem:

- Capturando Data de Nascimento, Data do Compromisso ou Hora do Evento

- Registrando em Log Datas de Emissão/Expiração de Documentos

- Selecionando Slots de Entrega ou Retirada

- Registrando Carimbos de Data/Hora de Transação

Os autores podem combinar o campo com contêineres de layout, validações ou regras condicionais para controlar o formato, os campos obrigatórios e a visibilidade contextual.

## &#x200B;4. Práticas recomendadas

- Use legendas ocultas, como &quot;Selecionar uma data&quot; ou &quot;Hora do compromisso&quot; para orientar os usuários.

- Habilite o seletor de data/hora para melhorar o UX e reduzir os erros de entrada.

- Aplicar restrições de formato (por exemplo, somente datas futuras) quando necessário.

- Forneça um valor de reserva para acessibilidade ou fallback de impressão.

- Mantenha a tipografia e a aparência consistentes com o design geral do formulário.

- Vincule o campo a um caminho de esquema válido para garantir a captura e o processamento adequados dos dados.

O objeto de campo de data/hora no editor de comunicação interativa é um componente eficiente e fácil de usar que simplifica a entrada com base no tempo. Com a configuração correta de estilo, manuseio de dados e controles de layout, ele permite experiências de formulário limpas, confiáveis e intuitivas para usuários e sistemas de back-end.