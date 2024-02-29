---
title: Publicar um formulário do AEM Forms Edge Delivery Services
description: Publicar um formulário do AEM Forms Edge Delivery Services
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 39bb45b285fcd938d44b9748aa8559b89a3636b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Publicar seu formulário

Quando estiver pronto para compartilhar o formulário com os clientes para coleta ou envio de dados, você pode simplesmente publicá-lo, disponibilizando o formulário prontamente para uso pelos clientes.

## Pré-requisitos

* A variável [O bloco de formulário está habilitado para o projeto EDS no Github](/help/edge/docs/forms/create-forms.md).
* O formulário foi totalmente testado e está pronto para uso.
* Seu [a planilha está configurada](/help/edge/docs/forms/submit-forms.md) para aceitar dados.

## Publicar seu formulário

Para publicar o formulário:

1. Acesse sua conta do Microsoft SharePoint ou Google Drive e navegue até o `[AEM Edge Delivery project directory]`.

1. Abra um arquivo de documento no qual você pretende incorporar o formulário. Por exemplo, você pode abrir o arquivo de índice ou criar um novo documento.

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

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a página. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na variável [planilha de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Um exemplo de formulário EDS](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Agora, seus clientes podem preencher o formulário e enviá-lo.

## Resolução de problemas

+++ Não é possível enviar dados para o formulário

Se você encontrar um erro semelhante à mensagem a seguir, isso indica que a planilha ainda não está configurada para aceitar os dados enviados.

![erro no envio do formulário](/help/edge/assets/form-error.png)

+++


## Veja mais

* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)
