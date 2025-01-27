---
title: Modelos de e-mail de HTML no Adaptive Forms no Forms as a Cloud Service
description: Saiba como usar modelos de email com formulários adaptáveis.
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: b9364394f683fa8af5d28723e5f10b20b001ea37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# Modelos de email no Adaptive Forms

O Adaptive Forms permite usar modelos de email de HTML e texto sem formatação. Os templates de email de HTML permitem enviar emails avançados, personalizados e visualmente atraentes quando um formulário é enviado. Esses emails podem ser personalizados com dados de formulário e aprimorados usando várias tags de email, como imagens e links. Com o Adaptive Forms, você pode carregar um arquivo contendo um modelo de HTML ou usar um editor de texto simples para criar esses modelos.

![modelos de email de HTML](/help/forms/assets/html-email.png)

Este artigo ajuda a configurar e usar modelos de email no Adaptive Forms. Ao final, você poderá:

* [Configurar um modelo de HTML para um formulário adaptável](#configure-an-html-template-for-an-adaptive-form)
* [Configurar um modelo de email de texto sem formatação para um formulário adaptável](#configure-a-plain-text-template-for-an-adaptive-form)
* [Usar dados de formulários em seus modelos de email](#use-form-data-in-your-email-templates)


Veja a seguir uma rápida visão geral das etapas envolvidas:

1. Abra o Formulário adaptável para edição.
1. Configure a ação de envio [Enviar Email](/help/forms/configure-submit-action-send-email.md).
1. Selecione ou faça upload de um modelo de HTML ou insira manualmente o modelo de email.
1. Teste a configuração do email.

## Configurar um modelo de HTML para um formulário adaptável

Você pode configurar um Formulário adaptável para enviar um email ao enviar usando a ação de envio [**Enviar Email**](/help/forms/configure-submit-action-send-email.md). A ação fornece dois métodos para configurar um modelo de HTML:

### Opção 1: Selecione um arquivo contendo o modelo HTML

Antes de continuar, verifique se você carregou o modelo de HTML no ambiente do AEM Forms.

1. Abra o Formulário adaptável para edição.
1. Vá para o **Navegador de Conteúdo**, selecione o **Contêiner do Guia** e toque no ícone de propriedades. Uma caixa de diálogo com o título `Adaptive Form Container` é exibida.
1. Vá para a guia **Envio** e selecione a ação de envio **Enviar Email**.
1. Habilitar a opção **Usar modelo externo**.
1. Habilite a opção **Usar modelo de HTML**.
1. Clique no ícone de pasta da opção Caminho do modelo externo e procure para selecionar seu modelo de HTML.
1. Clique em Concluído para salvar a configuração.

O modelo de HTML agora está configurado para o Formulário adaptável.

### Opção 2: Inserir ou colar manualmente um modelo de HTML

1. Abra o Formulário adaptável para edição.
1. Vá para o **Navegador de Conteúdo**, selecione o **Contêiner do Guia** e toque no ícone de propriedades. Uma caixa de diálogo com o título `Adaptive Form Container` é exibida.
1. Vá para a guia **Envio** e selecione a ação de envio **Enviar Email**.
1. Habilitar a opção **Usar modelo externo**.
1. Habilite a opção **Usar modelo de HTML**.
1. Digite ou cole seu código de HTML diretamente na caixa **Modelo de email** fornecida.


## Configurar um modelo de texto sem formatação para um formulário adaptável

Você pode configurar um Formulário adaptável para enviar um email ao enviar usando a ação de envio [**Enviar Email**](/help/forms/configure-submit-action-send-email.md). A ação fornece dois métodos para configurar um template de texto sem formatação:

### Opção 1: Selecione um arquivo contendo o modelo

Antes de continuar, verifique se você carregou o modelo de HTML no ambiente do AEM Forms.

1. Abra o Formulário adaptável para edição.
1. Vá para o **Navegador de Conteúdo**, selecione o **Contêiner do Guia** e toque no ícone de propriedades. Uma caixa de diálogo com o título `Adaptive Form Container` é exibida.
1. Vá para a guia **Envio** e selecione a ação de envio **Enviar Email**.
1. Habilitar a opção **Usar modelo externo**.
1. Clique no ícone de pasta da opção **Caminho do Modelo Externo** e procure e selecione seu modelo de texto sem formatação.
1. Clique em Concluído para salvar a configuração.

Seu modelo agora está configurado para o Formulário adaptável.

### Opção 2: Inserir ou colar manualmente um modelo de HTML

1. Abra o Formulário adaptável para edição.
1. Vá para o **Navegador de Conteúdo**, selecione o **Contêiner do Guia** e toque no ícone de propriedades. Uma caixa de diálogo com o título `Adaptive Form Container` é exibida.
1. Vá para a guia **Envio** e selecione a ação de envio **Enviar Email**.
1. Digite ou cole seu código de modelo de texto sem formatação diretamente na caixa **Modelo de email** fornecida.

## Usar dados de formulário em modelos de email

É possível incluir dados de formulário em seus modelos de email usando espaços reservados. Esses espaços reservados são substituídos dinamicamente por valores reais do campo de formulário quando o email é enviado. Por exemplo:

* ${name}: o valor do campo chamado &quot;name&quot;.
* ${email}: o valor do campo chamado &quot;email&quot;.
* ${message}: o valor do campo chamado &quot;message&quot;.

### Modelo de email HTML de amostra

Este é um exemplo de um template de email de HTML que usa espaços reservados para dados de formulário:

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### Modelo de e-mail de texto sem formatação

Este é um exemplo de um template de email de texto sem formatação:

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

Substitua os espaços reservados (${name}, ${email}, etc.) pelos nomes de campos de formulário correspondentes no Formulário adaptável.

## Práticas recomendadas para modelos de email do HTML

* Verifique se seus estilos estão em linha para uma melhor compatibilidade com os clientes de email.
* Torne seu modelo responsivo para obter uma melhor experiência em dispositivos móveis.
* Use ferramentas como Litmus ou Email no Acid para visualizar seu email em vários clientes de email.
* Verifique se os nomes dos espaços reservados correspondem exatamente aos nomes dos campos de formulário.
* Verifique se há tags ausentes ou incorretas no modelo de HTML.
* Verifique se a ação de envio [Enviar Email](/help/forms/configure-submit-action-send-email.md) está configurada corretamente.
