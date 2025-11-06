---
title: Publicar uma Edge Delivery Services para o AEM Forms
description: Publicar uma Edge Delivery Services para o AEM Forms
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Publicar seu formulário e começar a coletar dados

Quando estiver pronto para compartilhar o formulário com os clientes para coleta ou envio de dados, você pode simplesmente publicá-lo, disponibilizando o formulário prontamente para uso pelos clientes.

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Pré-requisitos

- Você tem um Projeto do AEM baseado no [Modelo do AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [Bloco do Adaptive Forms adicionado ao seu Projeto do AEM existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
- O formulário foi totalmente testado e está pronto para uso.
- Sua [planilha está configurada](/help/edge/docs/forms/submit-forms.md) para aceitar os dados.


## Publicar seu formulário

+++ &#x200B;1. Publique sua planilha

1. Abra sua conta do Microsoft SharePoint ou Google Drive e navegue até o diretório do projeto do AEM Edge Delivery.

1. Abra a planilha que tem seu formulário. Por exemplo, a [consulta](/help/edge/assets/enquiry.xlsx) da pasta de trabalho do Microsoft Excel.

1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a planilha.

   ![Usar AEM Sidekick para visualizar a planilha](/help/edge/assets/preview-form.png)

   Após a conclusão bem-sucedida da operação de visualização, o conteúdo da planilha é convertido para o formato JSON. A página de pré-visualização apresenta esse conteúdo em um formato de tabela estruturada. Por exemplo, a imagem que acompanha ilustra o conteúdo de um formulário de &quot;consulta&quot;.

   ![Formato JSON de Visualização do Forms](/help/edge/assets/forms-preview-json-format.png)

1. Use o AEM Sidekick para publicar a planilha. capture a URL de publicação, pois ela é necessária para renderizar o formulário na próxima seção. O formato do URL é o seguinte:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   - `<branch>` refere-se à ramificação do seu repositório GitHub.
   - `<repository>` indica seu repositório GitHub.
   - `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda seu repositório GitHub.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, estiver localizado na conta &quot;wkndform&quot; e você estiver usando a ramificação e o formulário &quot;main&quot; como &quot;query&quot;, o URL será semelhante ao seguinte:

   `https://main--wefinance--wkndform.aem.live/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry.json)-->

+++

+++ &#x200B;2. Adicionar o formulário à sua página da Web

Adicione o `<form>.json` a uma página da Web para facilitar a interação com o cliente, permitindo que os preenchimentos de formulário sejam preenchidos e enviados com facilidade.


Para adicionar o formulário à sua página da Web:

1. Acesse sua conta do Microsoft SharePoint ou do Google Drive e navegue até o `[AEM Edge Delivery project directory]`.

1. Abra um arquivo de documento no qual você pretende incorporar o formulário. Por exemplo, você pode abrir o arquivo [inquire-form.docx](/help/edge/assets/enquiry-form.docx) ou, como alternativa, criar um novo documento.

1. Identifique a seção desejada no documento onde deseja inserir o formulário e navegue até ele de acordo.

1. Adicione um bloco chamado &#39;Formulário&#39; ao arquivo. Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, ele estará localizado sob o proprietário da conta &quot;wkndform&quot; e você estará usando a ramificação &quot;main&quot;.

   | Formulário |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

   ![Adicionar um bloco chamado &#39;Formulário&#39; ao arquivo](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Esse bloco serve como um espaço reservado em que o formulário é incorporado. Na segunda linha do bloco, adicione a URL do arquivo `<form>.json` como um hiperlink.

   >[!IMPORTANT]
   >
   >
   > Verifique se o URL está formatado como um hiperlink em vez de ser exibido como texto simples.

   Use o URL de visualização (URL .page) para fins de desenvolvimento ou teste, ou o URL de publicação (.live) para produção.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, ele estará localizado sob o proprietário da conta &quot;wkndform&quot; e você estará usando a ramificação &quot;main&quot;.

   Estes são exemplos com URL de pré-visualização e publicação:

   **Visualizar URL**

   | Formulário |
   |---|
   | `https://main--wefinance--wkndform.aem.page/enquiry.json` |


   **Publicar URL**

   | Formulário |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a página da Web. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na [planilha de consulta](/help/edge/assets/enquiry-form.docx):


   ![Um exemplo de formulário EDS](/help/edge/assets/updated-form.png)

1. Use o AEM Sidekick para publicar o formulário. Agora, seus clientes podem preencher o formulário e enviá-lo.

+++ 

## Resolução de problemas

+++ Não é possível enviar dados para o formulário

Se você encontrar um erro semelhante à mensagem a seguir, isso indica que a planilha ainda não está configurada para [aceitar os dados](/help/edge/docs/forms/submit-forms.md) enviados.

![erro no envio do formulário](/help/edge/assets/form-error.png)

+++



