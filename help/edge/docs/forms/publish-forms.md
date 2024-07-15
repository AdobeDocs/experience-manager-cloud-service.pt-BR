---
title: Formulário Publish e AEM Forms Edge Delivery Services
description: Formulário Publish e AEM Forms Edge Delivery Services
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Publish seu formulário e comece a coletar dados

Quando estiver pronto para compartilhar o formulário com os clientes para coleta ou envio de dados, você pode simplesmente publicá-lo, disponibilizando o formulário prontamente para uso pelos clientes.

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Pré-requisitos

* Você tem um projeto AEM com base em [Modelo do AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionou um Bloco Forms AEM Adaptável ao seu projeto existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
* O formulário foi totalmente testado e está pronto para uso.
* Sua [planilha está configurada](/help/edge/docs/forms/submit-forms.md) para aceitar os dados.


## Publish seu formulário

+++ 1. Publish sua planilha

1. Abra a conta do Microsoft SharePoint ou do Google AEM Drive e navegue até o diretório do projeto do Edge Delivery.

1. Abra a planilha que tem seu formulário. Por exemplo, o formulário `enquiry` da pasta de trabalho do Microsoft Excel.

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a planilha.

   ![Usar AEM Sidekick para visualizar a planilha](/help/edge/assets/preview-form.png)

   Após a conclusão bem-sucedida da operação de visualização, o conteúdo da planilha é convertido para o formato JSON. A página de pré-visualização apresenta esse conteúdo em um formato de tabela estruturada. Por exemplo, a imagem que acompanha ilustra o conteúdo de um formulário de &quot;consulta&quot;.

   ![Formato JSON de Visualização do Forms](/help/edge/assets/forms-preview-json-format.png)

1. Use AEM Sidekick para publicar a planilha. capture a URL de publicação, pois ela é necessária para renderizar o formulário na próxima seção. O formato do URL é o seguinte:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda seu repositório GitHub.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;portal&quot;, estiver localizado na conta &quot;wkndforms&quot; e você estiver usando a ramificação &quot;main&quot;, o URL será semelhante ao seguinte:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Adicionar o formulário à sua página da Web

Adicione o `<form>.json` a uma página da Web para facilitar a interação com o cliente, permitindo que os preenchimentos de formulário sejam preenchidos e enviados com facilidade.


Para adicionar o formulário à sua página da Web:

1. Acesse sua conta do Microsoft SharePoint ou do Google Drive e navegue até o `[AEM Edge Delivery project directory]`.

1. Abra um arquivo de documento no qual você pretende incorporar o formulário. Por exemplo, você pode abrir o arquivo `index.docx` ou, como alternativa, criar um novo documento.

1. Identifique a seção desejada no documento onde deseja inserir o formulário e navegue até ele de acordo.

1. Adicione um bloco chamado &quot;Formulário&quot; ao arquivo, semelhante ao exemplo fornecido abaixo:

   | Formulário |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |

   ![Adicionar um bloco chamado &#39;Formulário&#39; ao arquivo](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Esse bloco serve como um espaço reservado em que o formulário é incorporado. Na segunda linha do bloco, adicione a URL do arquivo `<form>.json` como um hiperlink.

   >[!IMPORTANT]
   >
   >
   > Verifique se o URL está formatado como um hiperlink em vez de ser exibido como texto simples.

   Use o URL de visualização (URL .page) para fins de desenvolvimento ou teste, ou o URL de publicação (.live) para produção. Estes são exemplos com URL de pré-visualização e publicação:

   **Visualizar URL**

   | Formulário |
   |---|
   | [https://main--wefinance--wkndforms.hlx.page/enquiry.json](https://main--wefinance--wkndforms.hlx.page/enquiry.json) |


   **URL DO Publish**

   | Formulário |
   |---|
   | [https://main--wefinance--wkndforms.hlx.live/enquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a página da Web. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na [planilha de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   ![Um exemplo de formulário EDS](/help/edge/assets/eds-form.png)

1. Use AEM Sidekick para publicar o formulário. Agora, seus clientes podem preencher o formulário e enviá-lo.

+++

## Resolução de problemas

+++ Não é possível enviar dados para o formulário

Se você encontrar um erro semelhante à mensagem a seguir, isso indica que a planilha ainda não está configurada para [aceitar os dados](/help/edge/docs/forms/submit-forms.md) enviados.

![erro no envio do formulário](/help/edge/assets/form-error.png)

+++


## Consulte também:

{{see-more-forms-eds}}
