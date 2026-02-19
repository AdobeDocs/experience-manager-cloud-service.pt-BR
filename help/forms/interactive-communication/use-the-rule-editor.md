---
title: Criar regras no Editor de comunicação interativa
description: Criar regras no Editor de comunicações interativas permite que os autores definam comportamentos dinâmicos que tornam as comunicações interativas e inteligentes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9538ae2e-e0f5-4e85-943e-00fe99a64725
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Editor de regras no Editor de comunicações interativas


>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.


## &#x200B;1. Introdução


O Editor de regras no Editor de comunicação interativa permite que os autores definam comportamentos dinâmicos que tornam as comunicações interativas e inteligentes. As regras controlam como os campos se comportam, são exibidos ou calculados com base nas ações do usuário ou nos dados subjacentes, garantindo que cada comunicação seja personalizada e sensível ao contexto.


De configurações de visibilidade simples a lógicas condicionais complexas, as regras capacitam os autores a fornecer experiências que se adaptam em tempo real, melhorando a usabilidade, a precisão e o engajamento.


![Localizar IC Doc](/help/forms/interactive-communication/assets/rule-creation.png)


## &#x200B;2. Propriedades


2.1 Configuração de propriedades e comportamentos de campo


- **Tipos de Entrada:** Defina o tipo de dados que um campo aceita, como texto, números, datas ou valores booleanos, garantindo a validação e a formatação adequadas.


- **Regras de visibilidade:** controla se um campo está visível, oculto ou exibido dinamicamente com base nas condições (por exemplo, &quot;Mostrar campo de desconto somente se o código promocional for aplicado&quot;).


- **Valores padrão:** valores predefinidos em campos (por exemplo, a data de hoje, o nome do cliente do modelo de dados) para economizar tempo e melhorar a precisão.


2.2 Implementar cálculos, validações e lógica de regras


- **Lógica de Campo:** Automatize cálculos e relações de campo, como calcular valores de fatura ou preencher automaticamente campos dependentes.


- **Regras Personalizadas:** crie lógica avançada usando o Editor de Regras para cenários complexos, como verificações de elegibilidade ou preços baseados em camada.


- **Ações Condicionais:** defina disparadores que respondam a valores de dados ou de entrada do usuário, como campos de habilitação/desabilitação, exibição de mensagens ou ramificação para seções diferentes.


![Localizar IC Doc](/help/forms/interactive-communication/assets/rule-creation1.png)


## &#x200B;3. Utilização


O Editor de regras é amplamente usado para garantir que os formulários e as comunicações sejam responsivos e orientados por contexto:


- **Exibição Dinâmica:** Ocultar ou revelar seções com base no tipo de cliente ou nas opções selecionadas.


- **Validação:** evite erros verificando formatos, intervalos ou entradas obrigatórias.


- **Cálculos automáticos:** simplifique as tarefas do usuário com fórmulas (por exemplo, impostos, totais ou descontos).


- **Controle de Fluxo de Trabalho:** Habilite botões, campos ou ações específicos somente quando os pré-requisitos forem atendidos.


- **Personalization:** adapte a comunicação ao perfil, preferências ou critérios de qualificação do destinatário.


## &#x200B;4. Práticas recomendadas


- **Mantenha as regras simples:** divida a lógica complexa em regras menores e modulares para facilitar a manutenção.


- **Priorizar lógica de visibilidade:** oculte campos desnecessários antecipadamente para simplificar a experiência do usuário.


- **Teste completamente:** Visualize as regras com vários conjuntos de dados para confirmar a precisão e evitar conflitos.


- **Use os valores padrão sabiamente:** Preencha previamente os campos que raramente mudam, mas que permitem flexibilidade para edições.


- **Aproveite as ações condicionais:** Aplique-as para aprimorar a interatividade, mas evitar sobrecarregar os usuários.


- **Regras de documentos:** mantenha um registro da lógica de negócios para garantir clareza para desenvolvedores e partes interessadas.


Ao configurar regras criteriosamente, os autores podem criar comunicações que respondam de forma inteligente aos dados e ações do usuário — simplificando processos, reduzindo erros e fornecendo uma experiência perfeita e personalizada.
