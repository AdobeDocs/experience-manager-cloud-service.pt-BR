---
title: Mostrar uma mensagem de agradecimento personalizada após o envio do formulário
description: Saiba como configurar páginas de agradecimento e redirecionamento para o Bloqueio do Forms para otimizar a experiência do usuário e simplificar as jornadas do usuário.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Mostrar uma mensagem de agradecimento personalizada após o envio do formulário

Depois que um usuário envia um formulário, é crucial fornecer uma experiência perfeita por meio de uma mensagem de agradecimento. Ele não só confirma o envio bem-sucedido, mas também aumenta a satisfação do usuário e o orienta ainda mais em sua jornada.

- **Mensagem de agradecimento**: uma mensagem de agradecimento é a base da experiência do usuário, oferecendo tranquilidade e transmitindo informações importantes, além de reforçar a identidade da marca. Ele serve como um reconhecimento direto da ação do usuário, fomentando uma sensação de conclusão e satisfação.

- **Redirecionar**: um redirecionamento tem uma função essencial na orientação dos usuários para destinos relevantes, otimizando o engajamento e, em última análise, aumentando as taxas de conversão. Ao orientar os usuários para a próxima etapa da jornada de maneira contínua, o redirecionamento garante uma experiência de navegação tranquila. Por exemplo, redirecionando o usuário para a página de pagamentos após coletar os detalhes iniciais.

O comportamento padrão do bloco adaptável do Forms é exibir a seguinte mensagem de agradecimento no envio. A mensagem é exibida na parte superior do formulário no envio bem-sucedido do formulário.

![mensagem de agradecimento padrão](/help/edge/assets/thank-you-message.png)

No entanto, você tem a flexibilidade de personalizar essa experiência para atender às suas necessidades específicas. As opções incluem:

- Mostrar uma mensagem de agradecimento personalizada após o envio do formulário
- Redirecionar usuários para outra página após o envio para obter mais ações

>[!NOTE]
>
> Você pode consultar a [planilha de consulta](/help/edge/docs/forms/assets/enquiry.xlsx) a seguir para personalizar a mensagem de agradecimento de acordo com suas necessidades.

## Configurar uma mensagem de agradecimento personalizada

Caso deseje mostrar uma mensagem de agradecimento personalizada após o envio bem-sucedido do formulário, você pode configurar sua planilha para exibi-la.

Siga as etapas abaixo para configurar uma mensagem de agradecimento personalizada para o bloco adaptável do Forms:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.
1. Adicione uma mensagem de agradecimento personalizada na coluna `value` para o tipo de campo `submit` na planilha.

   ![Mensagem de agradecimento personalizada](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Por exemplo, adicione a mensagem `Submission Successful!` na coluna `value` para o tipo de campo `submit`.

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Mensagem de agradecimento personalizada](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Redirecionar usuários para outra página após o envio

Redirecionar um usuário para outra página após o envio do formulário pode aprimorar a experiência do usuário fornecendo informações relevantes, confirmando ações e orientando os usuários para os resultados desejados. Por exemplo,

- depois que um usuário conclui um formulário de compra, ele é redirecionado a uma página de pagamento para concluir a transação de forma segura.
- ao enviar um formulário de inscrição para um evento ou webinário, os usuários são redirecionados para uma página de confirmação exibindo detalhes do evento, como data, hora e local.

Siga as etapas abaixo para redirecionar os usuários para outra página:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.
1. Cole a URL na coluna `value` para o tipo de campo `submit` na planilha para redirecionar o usuário no envio bem-sucedido do formulário.
Para redirecionar a página para uma página diferente, use a URL da página [Documentação do Edge Delivery](https://www.aem.live/docs/).

   ![URL de redirecionamento de agradecimento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Redirecionar mensagem de agradecimento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

Você também pode criar um novo arquivo de documento e adicionar sua URL de visualização na coluna `value` para o tipo de campo `submit`.

Depois que um usuário enviar um formulário, é importante fornecer uma mensagem de agradecimento clara. Ele confirma que o envio foi bem-sucedido e melhora a satisfação do usuário.

