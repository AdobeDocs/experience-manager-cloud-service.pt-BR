---
title: Como usar chamadas de função assíncronas no Editor de regras visuais?
description: Chamadas de função assíncronas no editor de regras visual
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Uso de funções assíncronas em um Formulário adaptável com base nos Componentes principais

O [editor de regras no Forms Adaptável](/help/forms/rule-editor-core-components.md) oferece suporte a funções assíncronas, permitindo que você integre e gerencie operações que exigem espera por processos externos ou recuperação de dados sem interromper a interação do usuário com o formulário.

## Quais fatores determinam o uso de funções assíncronas ou síncronas?

Gerenciar a interação do usuário de maneira eficaz é fundamental para criar uma experiência perfeita. Duas abordagens comuns para lidar com operações são as funções síncronas e assíncronas.

**As funções síncronas** executam tarefas uma após a outra, fazendo com que o aplicativo aguarde a conclusão de cada operação antes de continuar. Isso pode levar a atrasos e a uma experiência do usuário menos envolvente, especialmente quando as tarefas envolvem a espera por recursos externos, como uploads de arquivos ou busca de dados.

Por exemplo, considere um cenário em que um usuário carrega uma imagem, o formulário inteiro é interrompido, aguardando a conclusão do upload. Essa pausa impede que o usuário interaja com outros campos, causando frustração e atrasos. À medida que esperam o processamento da imagem, qualquer informação inserida pode ser perdida se eles saírem ou perderem a paciência, tornando a experiência complicada e ineficiente.

Por outro lado, as **funções assíncronas** permitem que as tarefas sejam executadas simultaneamente. Isso significa que os usuários podem continuar interagindo com o aplicativo enquanto os processos em segundo plano são executados. As operações assíncronas melhoram a capacidade de resposta, permitindo que os usuários recebam feedback imediato e mantenham o engajamento sem interrupções.

Por outro lado, com uma abordagem assíncrona, os usuários podem carregar imagens em segundo plano e, ao mesmo tempo, continuar a preencher o restante do formulário sem interrupções. A interface permanece responsiva, permitindo atualizações em tempo real e feedback imediato à medida que o upload avança. Ele melhora o engajamento do usuário, garantindo uma experiência perfeita sem interrupções.

![Funções assíncronas e síncronas](/help/forms/assets/sync-async.png){align=center}

## Implementação de funções assíncronas do Adaptive Forms

É possível implementar as funções assíncronas do Adaptive Forms usando os seguintes tipos de regras no editor de regras:

* [Chamada de função assíncrona](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [Saída de função](#how-to-use-function-output-rule-type)

## Como usar o tipo de regra Chamada de função assíncrona?

Você pode gravar as [funções personalizadas](/help/forms/custom-function-core-component-create-function.md) para operações assíncronas e configurar as funções assíncronas usando o tipo de regra **[!UICONTROL Chamada de Função Assíncrona]** no editor de regras.

### Explorar o tipo de regra Chamada de função assíncrona por meio de um caso de uso

Considere um formulário de registro em um site onde os usuários inserem uma senha ocasional (OTP). O painel para adicionar detalhes do usuário é exibido somente após a inserção do OTP correto. Se o OTP estiver incorreto, o painel permanecerá oculto e uma mensagem de erro será exibida na tela.

![Formulário de logon](/help/forms/assets/rule-editor-login-form.png) {width-50%}

Em um formulário de registro, quando o usuário clica no botão **Confirmar**, a função `matchOTP()` é chamada de forma assíncrona para verificar o OTP inserido. A função `matchOTP()` é implementada como uma [função personalizada](/help/forms/custom-function-core-component-create-function.md). Usando o tipo de regra **[!UICONTROL Chamada de função assíncrona]** no editor de regras, você pode configurar a função `matchOTP()` no editor de regras de um Formulário adaptável. Também é possível implementar as chamadas de retorno com êxito e falha no editor de regras.

A figura a seguir ilustra as etapas para usar o tipo de regra **[!UICONTROL Chamada de função assíncrona]** para invocar funções assíncronas para o Adaptive Forms:

![Fluxo de trabalho para adicionar funções assíncronas](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. Grave uma função personalizada para a operação assíncrona no arquivo JS

>[!NOTE]
>
> * O editor de regras de um formulário exibe somente funções com um tipo de retorno de `Promise` quando você seleciona o tipo de regra **Chamada de função assíncrona**.
> * Para saber como criar uma função personalizada, consulte o artigo intitulado [Criar uma função personalizada para um formulário adaptável com base nos componentes principais](/help/forms/custom-function-core-component-create-function.md).

A função `matchOTP()` é implementada como uma função personalizada. O código abaixo é adicionado ao arquivo JS da função personalizada:

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

O código define uma função `matchOTP()` que gera uma promessa para validar uma OTP (senha ocasional) de forma assíncrona. Ele usa uma função `asyncOperationForOTPMatch()` para simular o processo de correspondência de OTP. A função verifica se o OTP fornecido é igual a `111`. Se o OTP inserido estiver correto, ele chamará o retorno de chamada com nulo para o erro e um objeto indicando que o OTP é válido `({'valid':'true'})`. Se o OTP não for válido, ele chamará o retorno de chamada com um objeto de erro `({'valid':'false'})` e nulo para o resultado.

### 2. Configure a função assíncrona no editor de regras

Execute as seguintes etapas para configurar a função assíncrona no editor de regras:

1. [Criar uma regra para usar a função assíncrona usando o tipo de regra de chamada Função assíncrona](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [Implementar retornos de chamada para a função assíncrona](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 Criar uma regra para usar a função assíncrona usando o tipo de regra de chamada Função assíncrona

Para criar uma regra para usar a operação assíncrona, use o tipo de regra **[!UICONTROL Chamada de função assíncrona]**. Execute as seguintes etapas:

1. Abra um Formulário adaptável no modo de criação, selecione um componente de formulário e selecione **[!UICONTROL Editor de regras]** para abrir o editor de regras.
1. Selecione **[!UICONTROL Criar]**.
1. Crie uma condição na seção **When** da regra para clicar no botão. Por exemplo, **Quando[Confirmar]** é clicado.
1. Na seção **Then**, selecione **[!UICONTROL Chamada de função assíncrona]** na lista suspensa **Selecionar ação**.
Ao selecionar **[!UICONTROL Chamada de função assíncrona]** e as funções com o tipo de retorno `Promise` são exibidas.
1. Selecione a função assíncrona na lista. Por exemplo, selecione a função `matchOTP()` e seus retornos de chamada como `Add success callback` e `add failure callback` são exibidos.
1. Agora, selecione as associações de **[!UICONTROL Entrada]**. Por exemplo, selecione **[!UICONTROL Entrada]** como `Form Object` e compare-a com o campo `OTP`.

A captura de tela abaixo exibe a regra:

![tipo de regra](/help/forms/assets/asyn-function-rule-type.png)

Agora, você pode prosseguir com a implementação dos retornos de chamada: `Success` e `Failure` para a função `matchOTP`.

#### 2.2 Implementar retornos de chamada para a função assíncrona

Implemente os métodos de retorno de chamada de sucesso e falha para a função assíncrona usando o editor visual de regras.

**Criar uma regra para o método `Add Success callback`**

Vamos criar uma regra para exibir o painel `userdetails`, se o OTP corresponder ao valor `111`.

1. Clique em **[!UICONTROL Adicionar retorno de chamada bem-sucedido]**.
1. Clique em **[!UICONTROL Adicionar instrução]** para criar a regra.
1. Crie uma condição na seção **When** da regra.
1. Selecione a **[!UICONTROL Saída da Função]** > **[!UICONTROL Obter Carga do Evento]**.

   >[!NOTE]
   >
   > A função **[!UICONTROL Obter Carga do Evento]** recupera dados associados a um evento específico para gerenciar dinamicamente as interações do usuário.

1. Selecione as associações correspondentes na seção **Input**. Por exemplo, selecione **[!UICONTROL Cadeia de caracteres]** e digite `valid`. Comparar a cadeia de caracteres inserida a `true`.
1. Na seção **Then**, selecione **[!UICONTROL Show]** na lista suspensa **Selecionar Ação**. Por exemplo, mostrar o painel `userdetails`.
1. Clique em **[!UICONTROL Adicionar instrução]**.
1. Selecione **[!UICONTROL Ocultar]** na lista suspensa **Selecionar ação**. Por exemplo, ocultar a caixa de texto `error message`.
1. Clique em **[!UICONTROL Concluído]**.

![Chamada bem-sucedida](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

Consulte a captura de tela abaixo, onde o usuário insere o OTP como `111`, e o painel `User Details` é exibido quando o botão `Confirm` é clicado.

![Êxito](/help/forms/assets/success.gif)

**Criar uma regra para o método `Add Failure callback`**

Vamos criar uma regra para exibir uma mensagem de falha se o OTP não corresponder ao valor `111`.

1. Clique em **[!UICONTROL Adicionar retorno de chamada de falha]**.

1. Clique em **[!UICONTROL Adicionar instrução]** para criar a regra.
1. Crie uma condição na seção **When** da regra.
1. Selecione a **[!UICONTROL Saída da Função]** > **[!UICONTROL Obter Carga do Evento]**.
1. Selecione as associações correspondentes na seção **Input**. Por exemplo, selecione **[!UICONTROL Cadeia de caracteres]** e digite `valid`. Comparar a cadeia de caracteres inserida a `false`.
1. Na seção **Then**, selecione **[!UICONTROL Show]** na lista suspensa **Selecionar Ação**. Por exemplo, mostrar a caixa de texto `error message`.
1. Clique em **[!UICONTROL Adicionar instrução]**.
1. Selecione **[!UICONTROL Ocultar]** na lista suspensa **Selecionar ação**. Por exemplo, oculte o painel `userdetails`.
1. Clique em **[!UICONTROL Concluído]**.

![Método de retorno de chamada de falha](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

Consulte a captura de tela abaixo, onde o usuário insere o OTP como `123`, e a mensagem de erro aparece quando o botão `Confirm` é clicado.

![Falha](/help/forms/assets/failure.gif)

A captura de tela abaixo exibe a regra completa para usar a **[!UICONTROL Chamada de Função Assíncrona]** para implementar uma função assíncrona:

![Regra para chamada de função assíncrona](/help/forms/assets/rule-editor-async-callbacks.png)

Você também pode editar os retornos de chamada clicando em **[!UICONTROL Editar retorno de chamada com êxito]** e **[!UICONTROL Editar retorno de chamada com falha]**.

## Como usar o tipo de regra de Saída de função?

Você também pode chamar as funções assíncronas indiretamente usando as funções síncronas. As funções síncronas são executadas usando o tipo de regra **[!UICONTROL Saída de Função]** no editor de regras de um Formulário Adaptável.

Examine o código abaixo para ver como invocar funções assíncronas usando o tipo de regra **[!UICONTROL Saída de Função]**:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

No exemplo acima, a função asyncFunction é um `asynchronous function`. Ele executa uma operação assíncrona fazendo uma solicitação `GET` para `https://petstore.swagger.io/v2/store/inventory`. Ele aguarda a resposta usando `await`, analisa o corpo da resposta como JSON usando `response.json()` e retorna os dados. A função `callAsyncFunction` é uma função personalizada síncrona que chama a função `asyncFunction` e exibe os dados de resposta no console. Embora a função `callAsyncFunction` seja síncrona, ela chama a função asyncFunction assíncrona e manipula seu resultado com instruções `then` e `catch`.

Para ver seu funcionamento, vamos adicionar um botão e criar uma regra para o botão que chama a função assíncrona em um clique de botão.

![criando regra para função assíncrona](/help/forms/assets/rule-for-async-funct.png){width=50%}

Consulte a captura de tela da janela de console abaixo para demonstrar que, quando o usuário clica no botão `Fetch`, a função personalizada `callAsyncFunction` é invocada, o que, por sua vez, chama uma função assíncrona `asyncFunction`. Inspecione a janela do console para exibir a resposta ao clique de botão:

![Janela de console](/help/forms/assets/async-custom-funct-console.png)

## Consulte também

{{see-also-rule-editor}}
