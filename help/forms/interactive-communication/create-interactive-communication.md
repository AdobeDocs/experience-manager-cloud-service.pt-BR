---
title: Criar uma comunicação interativa
description: Crie comunicações personalizadas orientadas por dados. Explore os principais recursos, etapas de integração e casos de uso reais com guias e tutoriais.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 17a75e271377d9c7bfdac28c9f3d9d8178b565fd
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Criar uma comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

A comunicação interativa permite criar, gerenciar e fornecer comunicações personalizadas e interativas, incluindo atendimento ao cliente, faturamento, documentos de integração, cartas de oferta, atualizações de conta e muito mais. Ele foi projetado para suportar qualquer cenário em que o conteúdo dinâmico e específico do usuário melhore a experiência de comunicação entre os setores.

Imagine que você precise enviar um extrato bancário, uma apólice de seguro ou uma conta de serviços públicos a milhares de clientes. Cada um tem o mesmo layout, mas dados personalizados. A comunicação interativa (IC) torna isso possível com eficiência.

![Localizar IC Docu](/help/forms/interactive-communication/assets/Picture1.png)

A produção manual desses documentos pode ser demorada e geralmente resulta em inconsistências, especialmente quando a personalização e a integração de dados são necessárias. Com o Editor de comunicação interativa, os usuários podem simplificar o processo de criação da comunicação interativa.

## Pré-requisitos

* [Certifique-se de que o autor é membro do grupo de formulários-usuários](/help/forms/setup-forms-cloud-service.md#configure-users)

## Criar uma comunicação interativa

Escolha entre diferentes cenários para criar uma Comunicação interativa, com base no nível de reutilização e na integração de dados necessária:

+++ Criar uma comunicação interativa em branco

A criação de uma comunicação interativa em branco permite iniciar do zero, ideal quando você deseja ter controle total sobre layout, estrutura e lógica.
Etapas a serem seguidas:

1. Abra sua **instância do Forms as a Cloud Service do Adobe Experience Manager (AEM)**.
1. Navegue até **Forms > Forms e Documentos**.
1. Clique em **Criar > Comunicação interativa**.

   ![Localizar IC Docu](/help/forms/interactive-communication/assets/comm.png)

1. Na tela de criação, deixe o campo **Modelo** em branco.

   ![Localizar IC Docu](/help/forms/interactive-communication/assets/create-ic-document.png)

1. Preencha outros detalhes como Título, Nome, Autor etc.
1. Clique em **Criar** para entrar na interface do Editor de Comunicações Interativas e começar a projetar.
1. Ele abre o Editor IC, onde você pode começar a projetar sua comunicação.
+++

+++ Criar uma comunicação interativa baseada em modelo

Usar um modelo ajuda a acelerar o design, reutilizando elementos de layout consistentes, como cabeçalhos, rodapés, logotipos ou formatação padrão.
Os modelos garantem a consistência da marca e economizam tempo para tipos de comunicação usados com frequência. Execute as etapas abaixo:

1. Abra a instância do AEM Forms as a Cloud Service.
1. Vá para **Forms > Forms e Documentos**, clique em **Criar > Comunicação Interativa**.
1. No formulário de criação, **selecione** um modelo habilitado na lista suspensa.
1. Preencha outros detalhes como Título, Nome, Autor etc.
1. Clique em **Criar** para criar sua comunicação com a estrutura de modelo selecionada.
1. Ele abre o Editor IC, onde você pode começar a projetar sua comunicação.
+++

+++ Criar uma comunicação interativa com interação de dados

As comunicações com interação de dados personalizam automaticamente o conteúdo usando dados de back-end.
Ideal para demonstrativos, faturas ou avisos em que a estrutura permanece constante, mas os dados variam de acordo com o recipient. Etapas a serem seguidas:

1. Abra a instância do AEM Forms as a Cloud Service.
1. Vá para **Forms > Forms e Documentos**, clique em **Criar > Comunicação Interativa**.
1. No campo **Modelo de dados de formulário**, vincule seu **FDM (Modelo de dados de formulário)** predefinido.
1. Preencha outros detalhes como Título, Nome, Autor etc.
1. Use o **Modelo de Dados** dentro do editor para associar campos a dados dinâmicos (por exemplo, nome do cliente, saldo, número de conta).
1. Use **Áreas de Conteúdo, Subformulários** e **Fragmentos** para estruturar e repetir dados onde necessário.
1. Visualize usando a **Visualização do PDF** e finalize a comunicação para entrega.
1. Ele abre o Editor IC, onde você pode começar a projetar sua comunicação.

![Localizar IC Docu](/help/forms/interactive-communication/assets/ic-ui.png)
+++

Comece a criar Comunicações interativas para simplificar seus fluxos de trabalho e fornecer experiências impactantes e específicas do usuário.

## Próximas etapas

[Criar um Modelo de comunicação interativa](/help/forms/interactive-communication/create-interactive-communication-template.md)
[Criar um fragmento de comunicação interativa](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
