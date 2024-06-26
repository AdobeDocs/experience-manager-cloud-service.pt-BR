---
title: Como configurar o Envio assíncrono para AEM Adaptive Forms?
description: Saiba como configurar o envio assíncrono para o Adaptive Forms. Saiba mais sobre como o envio assíncrono funciona para o Adaptive Forms.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Configurar envio assíncrono do AEM Adaptive Forms {#asynchronous-submission-of-adaptive-forms}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/asynchronous-submissions-adaptive-forms.html) |
| AEM as a Cloud Service | Este artigo |


Tradicionalmente, os formulários web são configurados para enviar de forma síncrona. No envio síncrono, quando os usuários enviam um formulário, eles são redirecionados para uma página de confirmação, uma página de agradecimento ou, em caso de falha de envio, uma página de erro. No entanto, experiências da Web modernas, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática enquanto a interação cliente-servidor acontece em segundo plano. É possível configurar o envio assíncrono para fornecer essa experiência com o Adaptive Forms.

No envio assíncrono, quando um usuário envia um formulário, o desenvolvedor do formulário conecta uma experiência separada, como redirecionar para outro formulário ou uma seção separada do site. O autor também pode conectar serviços separados, como enviar dados para um armazenamento de dados diferente ou adicionar um mecanismo de análise personalizado. No caso de envio assíncrono, um Formulário adaptável se comporta como um aplicativo de página única, pois o formulário não é recarregado ou sua URL não é alterada quando os dados do formulário enviado são validados no servidor.

Leia para obter detalhes sobre o envio assíncrono no Adaptive Forms.

## Configurar envio assíncrono {#configure}

Para configurar o envio assíncrono para um Formulário adaptável:

1. No modo de criação do Formulário adaptável, selecione o objeto Contêiner de formulário e selecione ![cmppr1](assets/configure-icon.svg) para abrir suas propriedades.
1. No **[!UICONTROL Envio]** seção de propriedades, ativar **[!UICONTROL Usar envio assíncrono]**.
1. No **[!UICONTROL Ao enviar]** selecione uma das seguintes opções a serem executadas no envio bem-sucedido do formulário.

   * **[!UICONTROL Redirecionar para URL]**: redireciona para a URL ou página especificada no envio do formulário. Você pode especificar um URL ou procurar para escolher o caminho para uma página no **[!UICONTROL URL/caminho de redirecionamento]** campo.
   * **[!UICONTROL Mostrar mensagem]**: exibe uma mensagem no envio do formulário. Você pode escrever uma mensagem no campo de texto abaixo de **[!UICONTROL Mostrar mensagem]** opção. O campo de texto é compatível com a formatação de rich text.

1. Selecionar ![botão de seleção1](assets/save_icon.svg) para salvar as propriedades.

## Como o envio assíncrono funciona {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] O fornece manipuladores de sucesso e erro prontos para uso para envios de formulários. Os manipuladores são funções do lado do cliente executadas com base na resposta do servidor. Quando um formulário é enviado, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou com erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Além disso, os autores e desenvolvedores de formulários podem escrever regras no nível do formulário para substituir os manipuladores padrão. Para obter mais informações, consulte [Substituir manipuladores padrão usando regras](#custom).

Primeiro, vamos analisar a resposta do servidor em busca de eventos de sucesso e erro.

### Resposta do servidor para evento de sucesso de envio {#server-response-for-submission-success-event}

A estrutura da resposta do servidor para o evento de sucesso de envio é a seguinte:

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

A resposta do servidor em caso de envio de formulário bem-sucedido inclui:

* Tipo de formato de dados de formulário: XML ou JSON
* Dados de formulário em formato XML ou JSON
* Opção selecionada para redirecionar para uma página ou exibir uma mensagem conforme configurado no formulário
* URL da página ou conteúdo da mensagem conforme configurado no formulário

O manipulador de sucesso lê a resposta do servidor e redireciona adequadamente para o URL da página configurada ou exibe uma mensagem.

### Resposta do servidor para evento de erro de envio {#server-response-for-submission-error-event}

A estrutura da resposta do servidor para o evento de erro de envio é a seguinte:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

A resposta do servidor em caso de erro no envio do formulário inclui:

* Motivo do erro, falha no CAPTCHA ou validação no lado do servidor
* Lista de objetos de erro, que inclui a expressão SOM do campo cuja validação falhou e a mensagem de erro correspondente

O manipulador de erros lê a resposta do servidor e exibe a mensagem de erro no formulário.

## Substituir manipuladores padrão usando regras {#custom}

Desenvolvedores de formulários e autores podem escrever regras, no nível do formulário, para substituir manipuladores padrão. A resposta do servidor para eventos de sucesso e erro é exposta no nível do formulário, que os desenvolvedores podem acessar usando `$event.data` nas regras.

Execute as seguintes etapas para escrever regras para lidar com eventos bem-sucedidos e errados.

1. Abra o Formulário adaptável no modo de criação, selecione qualquer objeto de formulário e ![edit-rules1](assets/edit-rules-icon.svg) para abrir o editor de regras.
1. Selecionar **[!UICONTROL Formulário]** na árvore Objetos de formulário e selecione **[!UICONTROL Criar]**.
1. Escolher **[!UICONTROL foi enviado com sucesso]** ou **[!UICONTROL falha no envio]** do **[!UICONTROL Selecionar estado]** lista suspensa.
1. Definir um **[!UICONTROL Depois]** ação para o estado selecionado. Por exemplo, selecione **[!UICONTROL Navegar para]** e, em seguida, digite ou cole um URL. Você também pode arrastar qualquer função usando o **[!UICONTROL Funções]** para a regra.

   ![manipulador de envio bem-sucedido](assets/form-submission-handler.png)

1. Selecionar **[!UICONTROL Concluído]** para salvar a regra.