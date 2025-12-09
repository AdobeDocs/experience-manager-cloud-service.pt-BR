---
title: Manuseio de estouro de conteúdo no Editor de comunicação interativa
description: O manuseio de estouro de conteúdo no Editor de comunicação interativa melhora o comportamento do texto em layouts Fluxados e Posicionados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Manuseio de estouro de conteúdo no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## Introdução

O recurso Manuseio de estouro de conteúdo no Editor de comunicação interativa melhora o comportamento do texto em layouts Fluxados e Posicionados. Ele garante uma continuidade perfeita do conteúdo para layouts fluídos e fornece alertas visuais para layouts posicionados, proporcionando aos autores melhor controle e flexibilidade ao projetar comunicações.

![Localizar IC Doc](/help/forms/interactive-communication/assets/content-overflow.png)

## Como usar a manipulação de estouro de conteúdo no Editor de comunicação interativa

1. Abra o Editor de comunicação interativa
Abra sua comunicação no Editor IC para começar a editar o layout e o conteúdo.

1. Selecione o tipo de layout
Escolha o layout desejado para seu subformulário, Fluxos ou Posicionados com base em como você deseja que o conteúdo se comporte.

1. Para Layouts em Fluxo

   1. Certifique-se de que a hierarquia de subformulário pai esteja definida como Fluxos.

   1. No painel Propriedades, ative a opção Permitir quebras de página no conteúdo (visível somente se a opção &quot;Permitir quebras de página&quot; do subformulário pai estiver ativada).

   1. Adicionar ou colar texto, quando o conteúdo exceder uma página, ele continuará automaticamente na próxima página.

1. Para layouts posicionados

   1. Adicionar ou editar texto dentro de um contêiner fixo.

   1. Se o conteúdo exceder a altura do contêiner, uma borda vermelha aparecerá na parte inferior para indicar o excesso.

   1. Redimensionar manualmente o container para acomodar o conteúdo extra.

1. Visualizar a comunicação
Use a opção Visualização do PDF para verificar como o conteúdo flui ou transborda entre páginas para ambos os tipos de layout.

## Principais recursos

### Layout fluido

- **Nova Opção:**
Adiciona uma propriedade **permitir quebras de página** no conteúdo para controlar o comportamento de estouro. Esta opção fica visível somente quando o subformulário pai está definido como Fluxado e a propriedade **Permitir quebras de página** está habilitada.

- **Continuação automática de página:**
Quando o conteúdo excede o espaço disponível, uma nova página é criada automaticamente e a edição continua sem interrupções.

- **Suporte para Copiar-Colar:**
O texto grande colado no editor flui automaticamente entre as páginas, mantendo a consistência do layout.

### Layout posicionado

- **Indicador de Estouro:**
Quando o conteúdo excede o contêiner (subformulário ou página), o editor de texto se expande para edição, mas a altura do elemento permanece fixa.

- **Alerta visual:**
Uma borda vermelha é exibida na parte inferior do contêiner para indicar o excesso.

- **Ajuste Manual:**
Os autores redimensionam manualmente o contêiner para ajustá-lo ao conteúdo adicional.

>[!NOTE]
>
> Esse recurso exige que toda a hierarquia pai (como subformulários) seja definida como Fluxograma. Se qualquer subformulário pai na hierarquia estiver Posicionado, a opção **Permitir quebras de página** no conteúdo não funcionará conforme esperado.

## Benefícios

- Melhora a eficiência e o controle da criação de conteúdo.

- Mantém o layout consistente e a legibilidade nas páginas.

- Ajuda a identificar o excesso rapidamente por meio de indicadores visuais.

- Melhora a flexibilidade do design de comunicação para ambos os tipos de layout.
