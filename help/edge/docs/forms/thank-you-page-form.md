---
title: Configurar página de agradecimento do EDS Forms
description: Configurar página de agradecimento do EDS Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 1%

---


# Configurar redirecionamentos de bloco de formulário

Você tem a opção de configurar o bloco de formulário para redirecionar para uma página diferente em seu site em vez da página padrão &quot;obrigado&quot;,. Para configurar outra página como destino de redirecionamento

1. Abra o `[EDS Project]/blocks/form/form.js` arquivo para edição.

   ![código do nó thank you](/help/edge/assets/change-thankyou-node.png)

1. Altere o `thankyou` na seguinte linha, para o nó de sua escolha:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Por exemplo,

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > Certifique-se de que uma página de documento com o mesmo nome seja criada na pasta do projeto do Serviço de entrega de borda no Microsoft SharePoint ou no Google Sheets, caso ainda não tenha sido criada.


1. Prossiga para o check-in da pasta &#39;form.js&#39; atualizada e seus arquivos subjacentes para o projeto do Serviço de entrega de borda no GitHub. Essa atualização garante que o formulário agora redirecione para o nó atualizado, conforme especificado.
