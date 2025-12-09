---
title: Componente Caixa de texto no Editor de comunicação interativa
description: O componente Caixa de texto no Editor de comunicação interativa no AEM Forms permite que os autores insiram e exibam conteúdo de texto em uma comunicação.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Componente Caixa de texto no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente **Caixa de Texto** no Editor de Comunicação Interativa permite que os autores insiram e exibam conteúdo de texto em uma comunicação. É um dos componentes mais fundamentais e amplamente usados, geralmente usado para coletar nomes, comentários, feedback ou dados personalizados ao projetar comunicações interativas ou fragmentos de comunicação.

A Caixa de Texto oferece suporte à **associação de dados**, permitindo que os autores combinem conteúdo estático e dinâmico perfeitamente, por exemplo: ***&quot;Nome do usuário: @name&quot;***, em que @name é um campo de dados vinculado que é preenchido dinamicamente quando o documento é salvo como um PDF. Além disso, ele oferece suporte à formatação de rich text e ao posicionamento flexível para um controle de layout preciso.

![Localizar IC Doc](/help/forms/interactive-communication/assets/textbox.png)

## &#x200B;2. Propriedades

O componente Caixa de texto fornece um amplo conjunto de propriedades para ajudar a configurar sua aparência, comportamento e comportamento.

2.1 Tipografia

**Família da Fonte:** permite a seleção de estilos de fonte, como Arial, Helvetica, Times New Roman, etc.

**Validação de Fonte:** Restrições de entrada opcionais podem ser aplicadas para garantir que apenas formatos de texto, numéricos ou especiais sejam aceitos.

**Alinhamento de Texto:** As opções incluem alinhamento à esquerda, à direita, ao centro ou justificado.

**Estilo do Texto:** Habilite a formatação do texto com os recursos negrito, itálico, tachado e sublinhado.

**Listas:** suporta a inserção de listas ordenadas (numeradas) e não ordenadas (com marcadores).

2.2 Posição

**Largura e altura:** Defina as dimensões da caixa de texto em pixels ou porcentagem relativa ao contêiner.

2.3 Margem

Defina o espaçamento em torno da caixa de texto:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4 Aparência

- **Preenchimento de Texto:** Personalize a cor e a transparência do texto.

- **Preenchimento:** Defina a cor de fundo da caixa de texto.

- **Traço:** Adicione bordas com personalizáveis:

   - Largura (espessura)

   - Estilo (sólido, tracejado, pontilhado)

   - Edge (cantos arredondados ou pontiagudos)

2.5 Presença

**Visível:** Configuração padrão; a caixa de texto é exibida para o usuário.

**Oculto:** A caixa de texto está incluída no formulário, mas não está exibida.



## &#x200B;3. Utilização

A caixa de texto é usada para:

- Coleta de informações do cliente, como nomes, comentários ou feedback.

- Inserção de valores alfanuméricos.

- Integração de mensagens personalizadas usando modelos de dados vinculados.

- Incorporação dentro de fragmentos para uso repetido em documentos.

Os autores podem arrastar a Caixa de texto da Biblioteca de componentes para a Exibição de design ou a exibição mestre e configurar seu comportamento usando o Painel Propriedades.

## &#x200B;4. Práticas recomendadas

- Sempre associe Caixas de texto a rótulos de campo significativos para melhorar a acessibilidade.

- Use validações de entrada apropriadas para evitar erros de entrada de dados.

- Garanta um layout responsivo definindo margens e larguras relativas aos contêineres principais.

- Evite estilos de fonte excessivos que possam atrapalhar a legibilidade.

Ao configurar cuidadosamente as propriedades da Caixa de texto, os autores podem criar experiências de comunicação interativas, responsivas e amigáveis no Editor de comunicação interativa do AEM.
