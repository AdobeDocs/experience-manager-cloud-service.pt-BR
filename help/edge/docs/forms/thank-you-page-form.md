---
title: Configurar página de agradecimento ou formulário de redirecionamento após o envio
description: Saiba como configurar páginas de agradecimento e redirecionamento para o Bloqueio do Forms para otimizar a experiência do usuário e simplificar as jornadas do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d6b1048c44022da47a9d7443f564a2ff9d1802cf
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---


# Mostrar a página de agradecimento ou o formulário de redirecionamento após o envio

Depois que um usuário envia um formulário, é crucial fornecer uma experiência contínua por meio de uma página de agradecimento ou de um redirecionamento. Esses elementos não apenas confirmam o envio bem-sucedido, mas também melhoram a satisfação do usuário e os orientam ainda mais em sua jornada.

* **Página de agradecimento**: uma página de agradecimento é uma pedra angular da experiência do usuário, oferecendo garantia e transmitindo informações importantes, além de reforçar a identidade da marca. Ele serve como um reconhecimento direto da ação do usuário, fomentando uma sensação de conclusão e satisfação.

* **Redirecionar**: um redirecionamento desempenha um papel fundamental ao direcionar os usuários para destinos relevantes, otimizando o engajamento e, em última análise, aumentando as taxas de conversão. Ao orientar os usuários para a próxima etapa da jornada de maneira contínua, o redirecionamento garante uma experiência de navegação tranquila. Por exemplo, redirecionando o usuário para a página de pagamentos após coletar os detalhes iniciais.

No bloco Adaptive Forms, o comportamento padrão é exibir uma página de agradecimento. No entanto, você tem a flexibilidade de personalizar essa experiência para atender às suas necessidades específicas. As opções incluem:

* [Configuração da página de agradecimento e da mensagem para alinhar-se às suas metas de marca e comunicação](#configuring-the-thank-you-page-and-message)
* [Redirecionar usuários para outra página após o envio para obter mais ações](#redirect-users-to-another-page-post-submission)

## Configurando a página de agradecimento e a mensagem

O comportamento padrão do bloco Adaptive Forms é exibir a página &quot;obrigado&quot; no envio. Siga estas etapas para configurar a página &quot;obrigado&quot; do bloco Adaptive Forms:

1. Acesse sua pasta do projeto AEM Edge Delivery no Microsoft SharePoint ou no Google Workspace.
1. Crie um arquivo do Microsoft Word ou Google Docs chamado &quot;obrigado&quot; no diretório do projeto.
1. Adicione sua mensagem de agradecimento ao arquivo &quot;thankyou&quot;. </br>

   ![Exemplo de página de agradecimento](/help/edge/assets/sample-thankyou-page.png)

1. Use o AEM Sidekick para visualizar e publicar o arquivo &quot;obrigado&quot;.

O bloco Adaptive Forms exibe a página &quot;obrigado&quot; no envio do formulário.

## Redirecionar usuários para outra página após o envio

Por padrão, o bloco Adaptive Forms redireciona os usuários para a página &quot;obrigado&quot;. Para redirecionar usuários para uma página diferente da página padrão &quot;obrigado&quot;, você tem duas opções:

* [Substituir a página de &quot;obrigado&quot; por uma página diferente](#replace-the-existing-thankyou-page)
* [Use redirecionamentos de site para o redirecionamento de página de agradecimento](#use-website-redirects-for-thankyou-page-redirection)

### Substitua a página de &quot;obrigado&quot;

1. Abra o &quot;[Projeto EDS]/blocks/form/form.js&quot; para edição.
1. Altere o `thankyou` página na linha a seguir para a página de sua escolha:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Por exemplo,

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Verifique se existe uma página com o mesmo nome na pasta do projeto do Serviço de entrega de borda no Microsoft SharePoint ou no Google Workspace. Se a página não existir, prossiga para criá-la e publicá-la.

1. Continue verificando a pasta &#39;form.js&#39; atualizada e seus arquivos subjacentes no projeto do Serviço de entrega de borda no GitHub. Essa atualização garante que o formulário agora redirecione para a página atualizada conforme especificado.

1. Verifique se a página existe na pasta do projeto EDS e publique-a.


### Use redirecionamentos de site para o redirecionamento de página de agradecimento

Redirecionar um usuário para outra página após o envio do formulário pode aprimorar a experiência do usuário fornecendo informações relevantes, confirmando ações e orientando os usuários para os resultados desejados. Por exemplo,

* depois que um usuário conclui um formulário de compra, ele é redirecionado a uma página de pagamento para concluir a transação de forma segura.
* ao enviar um formulário de inscrição para um evento ou webinário, os usuários são redirecionados para uma página de confirmação exibindo detalhes do evento, como data, hora e local.

Para redirecionar a página &quot;obrigado&quot; para uma página diferente, use o [redirecionamentos do site](https://www.aem.live/docs/redirects) planilha eletrônica.


## Veja mais

* [Componentes de formulários](/help/edge/docs/forms/form-components.md)
* [Propriedades do campo de formulário](/help/edge/docs/forms/eds-form-field-properties)
* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)
