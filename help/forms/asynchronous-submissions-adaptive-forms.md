---
title: Como configurar o envio assíncrono para o Adaptive Forms?
description: Saiba como configurar o envio assíncrono para o Adaptive Forms. Saiba mais sobre como o envio assíncrono funciona no Adaptive Forms.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Envio assíncrono do Adaptive Forms {#asynchronous-submission-of-adaptive-forms}

Tradicionalmente, os formulários web são configurados para envio síncrono. No envio síncrono, quando os usuários enviam um formulário, ele é redirecionado para uma página de confirmação, uma página de agradecimento ou, em caso de falha de envio, uma página de erro. No entanto, experiências modernas da Web, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática, enquanto a interação cliente-servidor acontece em segundo plano. Você pode configurar o envio assíncrono para fornecer essa experiência com o Adaptive Forms.

No envio assíncrono, quando um usuário envia um formulário, o desenvolvedor do formulário conecta uma experiência separada, como redirecionar para outro formulário ou uma seção separada do site. O autor também pode conectar serviços separados como o envio de dados para um armazenamento de dados diferente ou adicionar um mecanismo de análise personalizado. No caso de envio assíncrono, um formulário adaptável se comporta como um aplicativo de página única, pois o formulário não é recarregado ou sua URL não é alterada quando os dados do formulário enviados são validados no servidor.

Leia para obter detalhes sobre o envio assíncrono no Adaptive Forms.

## Configurar envio assíncrono {#configure}

Para configurar o envio assíncrono para um formulário adaptável:

1. No modo de criação do Formulário adaptável, selecione o objeto Contêiner de formulários e toque em ![cmppr1](assets/configure-icon.svg) para abrir suas propriedades.
1. No **[!UICONTROL Submissão]** seção propriedades, habilitar **[!UICONTROL Usar envio assíncrono]**.
1. No **[!UICONTROL Ao enviar]** selecione uma das opções a seguir para executar no envio bem-sucedido do formulário.

   * **[!UICONTROL Redirecionar para URL]**: Redireciona para o URL ou página especificada no envio do formulário. Você pode especificar um URL ou navegar para escolher o caminho para uma página no **[!UICONTROL Redirecionar URL/caminho]** campo.
   * **[!UICONTROL Mostrar mensagem]**: Exibe uma mensagem no envio do formulário. Você pode gravar uma mensagem no campo de texto abaixo da variável **[!UICONTROL Mostrar mensagem]** opção. O campo de texto oferece suporte à formatação Rich Text.

1. Toque ![botão de seleção1](assets/save_icon.svg) para salvar as propriedades.

## Como funciona o envio assíncrono {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] O fornece manipuladores de erros e sucesso prontos para uso para envios de formulários. Os manipuladores são funções do lado do cliente que são executadas com base na resposta do servidor. Quando um formulário é enviado, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o sucesso ou o evento de erro do envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Além disso, autores e desenvolvedores de formulários podem gravar regras no nível de formulário para substituir manipuladores padrão. Para obter mais informações, consulte [Substituir manipuladores padrão usando regras](#custom).

Vamos primeiro analisar a resposta do servidor em busca de eventos bem-sucedidos e de erros.

### Resposta do servidor para evento bem-sucedido de envio {#server-response-for-submission-success-event}

A estrutura para a resposta do servidor para o evento bem-sucedido de envio é a seguinte:

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

* Tipo de formato de dados do formulário: XML ou JSON
* Dados do formulário no formato XML ou JSON
* Opção selecionada para redirecionar para uma página ou exibir uma mensagem conforme configurado no formulário
* URL da página ou conteúdo da mensagem, conforme configurado no formulário

O manipulador de sucesso lê a resposta do servidor e, de acordo, redireciona para o URL da página configurada ou exibe uma mensagem.

### Resposta do servidor para evento de erro de envio {#server-response-for-submission-error-event}

A estrutura para a resposta do servidor para o evento de erro de envio é a seguinte:

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

* Motivo do erro, CAPTCHA com falha ou validação do lado do servidor
* Lista de objetos de erro, que inclui a expressão SOM do campo que falhou na validação e a mensagem de erro correspondente

O manipulador de erros lê a resposta do servidor e, portanto, exibe a mensagem de erro no formulário.

## Substituir manipuladores padrão usando regras {#custom}

Desenvolvedores e autores de formulários podem gravar regras, no nível de formulário, para substituir manipuladores padrão. A resposta do servidor para eventos bem-sucedidos e de erro é exposta no nível do formulário, que os desenvolvedores podem acessar usando `$event.data` em regras.

Execute as etapas a seguir para gravar regras para lidar com eventos bem-sucedidos e de erro.

1. Abra o Formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em ![edit-rules1](assets/edit-rules-icon.svg) para abrir o editor de regras.
1. Selecionar **[!UICONTROL Formulário]** na árvore Objetos de formulário e toque em **[!UICONTROL Criar]**.
1. Choose **[!UICONTROL é submetido com êxito]** ou **[!UICONTROL falha no envio]** do **[!UICONTROL Selecionar estado]** lista suspensa.
1. Defina um **[!UICONTROL Então]** para o estado selecionado. Por exemplo, selecione **[!UICONTROL Navegar para]** e, em seguida, digite ou cole um URL. Também é possível arrastar qualquer função usando a variável **[!UICONTROL Funções]** para a regra.

   ![manipulador de envio bem-sucedido](assets/form-submission-handler.png)

1. Toque **[!UICONTROL Concluído]** para salvar a regra.
