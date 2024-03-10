---
title: Publicar um formulário do AEM Forms Edge Delivery Services
description: Publicar um formulário do AEM Forms Edge Delivery Services
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Publicar seu formulário

Quando estiver pronto para compartilhar o formulário com os clientes para coleta ou envio de dados, você pode simplesmente publicá-lo, disponibilizando o formulário prontamente para uso pelos clientes.

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Pré-requisitos

* A variável [O bloco adaptável do Forms está ativado para seu projeto EDS no GitHub](/help/edge/docs/forms/create-forms.md).
* O formulário foi totalmente testado e está pronto para uso.
* Seu [a planilha está configurada](/help/edge/docs/forms/submit-forms.md) para aceitar dados.

## Publicar seu formulário

+++ 1. Publique sua planilha

1. Abra sua conta do Microsoft SharePoint ou Google Drive e navegue até o diretório do projeto do Delivery de borda do AEM.

1. Abra a planilha que tem seu formulário. Por exemplo, a variável `enquiry` formulário da pasta de trabalho do Microsoft Excel.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a planilha.

   ![Usar AEM Sidekick para visualizar a planilha](/help/edge/assets/preview-form.png)

   Após a conclusão bem-sucedida da operação de visualização, o conteúdo da planilha é convertido para o formato JSON. A página de pré-visualização apresenta esse conteúdo em um formato de tabela estruturada. Por exemplo, a imagem que acompanha ilustra o conteúdo de um formulário de &quot;consulta&quot;.

   ![Visualização do formato JSON do Forms](/help/edge/assets/forms-preview-json-format.png)

1. Use AEM Sidekick para publicar a planilha. capture a URL de publicação, pois ela é necessária para renderizar o formulário na próxima seção. O formato do URL é o seguinte:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda o repositório GitHub.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;portal&quot;, estiver localizado na conta &quot;wkndforms&quot; e você estiver usando a ramificação &quot;main&quot;, o URL será semelhante ao seguinte:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Adicionar o formulário à sua página da Web

Adicione o `<form>.json` para uma página da Web para facilitar a interação com o cliente, permitindo que os preenchimentos de formulário preencham e enviem o formulário sem esforço.


Para adicionar o formulário à sua página da Web:

1. Acesse sua conta do Microsoft SharePoint ou Google Drive e navegue até o `[AEM Edge Delivery project directory]`.

1. Abra um arquivo de documento no qual você pretende incorporar o formulário. Por exemplo, você pode abrir a variável `index.docx` arquivo ou, como alternativa, crie um novo documento.

1. Identifique a seção desejada no documento onde deseja inserir o formulário e navegue até ele de acordo.

1. Adicione um bloco chamado &quot;Formulário&quot; ao arquivo, semelhante ao exemplo fornecido abaixo:

   | Formulário |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Esse bloco serve como um espaço reservado em que o formulário é incorporado. Na segunda linha do bloco, adicione o URL do `<form>.json` arquivo como um hiperlink.

   >[!IMPORTANT]
   >
   >
   > Verifique se o URL está formatado como um hiperlink em vez de ser exibido como texto simples.

   Use o URL de visualização (URL .page) para fins de desenvolvimento ou teste, ou o URL de publicação (.live) para produção. Estes são exemplos com URL de pré-visualização e publicação:

   **Visualizar URL**
| Formulário | |—| | [https://main--portal--wkndforms.hlx.page/enquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **URL de publicação**
| Formulário | |—| | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a página da web. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na variável [planilha de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Um exemplo de formulário EDS](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. Use AEM Sidekick para publicar o formulário. Agora, seus clientes podem preencher o formulário e enviá-lo.

+++

## Resolução de problemas

+++ Não é possível enviar dados para o formulário

Se você encontrar um erro semelhante à mensagem a seguir, isso indica que a planilha não está configurada para [aceitar o enviado](/help/edge/docs/forms/submit-forms.md) dados ainda.

![erro no envio do formulário](/help/edge/assets/form-error.png)

+++




## Veja mais
