---
title: Configurar página de agradecimento do EDS Forms
description: Saiba como configurar páginas de agradecimento e redirecionamento para o EDS Forms para otimizar a experiência do usuário e simplificar as jornadas do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Configuração de páginas de agradecimento e redirecionamento em blocos do Adaptive Forms

As páginas de agradecimento e o redirecionamento são aspectos vitais do aprimoramento da experiência do usuário, fornecendo aos usuários confirmação, comunicação clara e navegação sem problemas após o envio do formulário.

## Configurando páginas de agradecimento

As páginas de agradecimento servem como um reconhecimento tranquilizador para os usuários e permitem que as organizações comuniquem informações essenciais e, ao mesmo tempo, reforcem a identidade da marca. Siga estas etapas para configurar uma página de agradecimento do EDS Forms:

1. Acesse sua pasta do projeto AEM Edge Delivery no Microsoft SharePoint ou no Google Workspace.
1. Crie um arquivo do Microsoft Word ou Google Docs chamado &quot;obrigado&quot; no diretório do projeto.
1. Adicione sua mensagem de agradecimento ao arquivo &quot;thankyou&quot;.
   ![Exemplo de página de agradecimento](/help/edge/assets/sample-thankyou-page.png)
1. Utilize o AEM Sidekick para visualizar e publicar o arquivo &quot;obrigado&quot;.

## Redirecionar usuários após o envio

O redirecionamento facilita jornadas ininterruptas de usuários, orientando-os para destinos relevantes, otimizando o engajamento e aumentando as taxas de conversão.

Por padrão, o bloco Adaptive Forms redireciona os usuários para a página &quot;obrigado&quot;. Para redirecionar usuários para uma página diferente da página padrão &quot;obrigado&quot;, você tem duas opções:

* substitua a página de agradecimento existente por outra página, ou
* redirecione a página &quot;obrigado&quot; para outra página de sua escolha.

### Substituir a página de agradecimento existente

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


### Usar redirecionamentos do site

Configure um redirecionamento de site para direcionar a página &quot;obrigado&quot; para uma página diferente. Consulte a [Redireciona a documentação](https://www.aem.live/docs/redirects) para obter instruções detalhadas.


