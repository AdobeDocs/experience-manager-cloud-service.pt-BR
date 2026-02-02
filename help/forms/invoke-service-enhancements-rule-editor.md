---
title: Quais são as melhorias no VRE do serviço de Chamada para formulários baseados nos Componentes principais?
description: Aprimoramentos no serviço de Chamada do editor de regras
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: chame os aprimoramentos do serviço no VRE, preenchendo as opções suspensas usando invocar serviço, Defina o painel repetível usando a saída de invocar serviço, Defina o painel usando a saída de invocar serviço, Use o parâmetro de saída de invocar serviço para validar outro campo.
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 17dfa6e28d2510484731a736c1cf7fda22961e66
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 1%

---

# Integração de APIs externas com o Editor de regras visuais no Forms dos Componentes principais

O Editor de Regras Visuais em um Formulário Adaptável oferece suporte ao recurso **Chamar Serviço**, permitindo que você se conecte a APIs externas por meio de Modelos de Dados de Formulário (FDM) configurados para sua instância. Você pode mapear campos de formulário diretamente para os parâmetros de entrada do serviço e usar a opção de carga útil do evento para mapear os parâmetros de saída. O Editor visual de regras também permite definir regras para manipuladores de sucesso e falha com base na resposta do serviço: manipuladores de sucesso lidam com chamadas de API bem-sucedidas, enquanto manipuladores de falha gerenciam erros.

Isso permite enviar facilmente solicitações de API do seu formulário, processar as respostas da API e exibir ou usar os dados retornados dinamicamente no formulário. Ele garante uma integração perfeita entre seu Formulário adaptável e sistemas externos ou fontes de dados.


## Vantagens de usar a função Chamar serviço no editor de regras do formulário

Estas são algumas das vantagens de usar a operação Chamar serviço no editor de regras de um Formulário adaptável:

* **Integração simplificada de API**: o Editor de regras visuais simplifica o processo de integração de serviços externos ou APIs ao Forms adaptável. Ao usar o **Invocar Serviço**, você pode conectar formulários facilmente a várias fontes de dados e serviços sem a necessidade de uma codificação complexa, tornando a integração de formulários mais eficiente.

* **Manipulação de resposta dinâmica**: você pode gerenciar respostas de sucesso e erro com base nas respostas de saída do **Invoke Service**, permitindo que os formulários reajam dinamicamente a diferentes cenários. Garante que os formulários lidem com várias condições adequadamente, melhorando a flexibilidade e o controle.

* **Interação do usuário aprimorada**: usar o **Invocar Serviço** no editor de regras permite a validação em tempo real em seus formulários, proporcionando uma melhor experiência ao usuário. Ela também garante que os dados sejam validados com precisão no lado do servidor, reduzindo erros e melhorando a confiabilidade dos formulários.

## Chamar manipuladores de serviço para respostas com êxito e falha

>[!NOTE]
>
> Você pode usar os manipuladores de sucesso e falha **Invocar Serviço** somente para formulários baseados em componentes principais. O Forms baseado em componentes de base não oferece suporte a **Manipuladores de êxito e falha de Chamar Serviço**.

O editor visual de regras permite criar regras para manipuladores de sucesso e falha para operações de **Chamar Serviço** com base nas respostas de saída. A imagem abaixo mostra o **Invocar Serviço** no editor de regras visuais para um Formulário Adaptável:

![Invocar manipuladores de serviço](/help/forms/assets/invoke-service-rule-editor.png)

### Adicionando Manipulador de Sucesso e Manipulador de Falhas

Para adicionar manipulador de êxito ou falha, clique em **[!UICONTROL Adicionar manipulador de sucesso]** ou **[!UICONTROL Adicionar manipulador de falha]**, respectivamente.

Quando você clica em **[!UICONTROL Adicionar Manipulador de Êxito]**, o editor de regras **[!UICONTROL Invocar Manipulador de Êxito do Serviço]** é exibido, permitindo que você especifique regras ou lógica para gerenciar a resposta de saída **Invocar Serviço** quando a operação for bem-sucedida. Você pode especificar regras mesmo sem definir condições; no entanto, você pode adicionar condições para o manipulador de sucesso clicando na opção **[!UICONTROL Adicionar Condição]**.

![Invocar manipulador de êxito do serviço](/help/forms/assets/invoke-service-success-handler.png)

Você pode adicionar várias regras para lidar com respostas bem-sucedidas para a operação **Invocar Serviço**:

![Vários manipuladores de sucesso](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

Da mesma forma, você pode adicionar regras para manipular a resposta de saída **Chamar Serviço** quando a operação não for bem-sucedida. A imagem abaixo exibe o editor de regras do **[!UICONTROL Manipulador de Falha de Serviço de Chamada]**:

![Invocar manipulador de falha do serviço](/help/forms/assets/invoke-service-failue-handler.png)

Você também pode adicionar várias regras para lidar com respostas malsucedidas da operação **Chamar Serviço**.

O recurso **Habilitar Validação de Erros no Servidor** também permite validações adicionadas pelo autor ao criar um Formulário Adaptável para execução no servidor.

## Pré-requisitos para usar a função Chamar serviço no editor de regras

Abaixo estão os pré-requisitos que você deve atender antes de usar **Chamar Serviço** no editor de regras:

* Verifique se você configurou uma fonte de dados. Para obter instruções sobre como configurar uma fonte de dados, [clique aqui](/help/forms/configure-data-sources.md).
* Crie um modelo de dados de formulário usando a fonte de dados configurada. Para obter orientação sobre como criar um Modelo de dados de formulário, [clique aqui](/help/forms/create-form-data-models.md).

## Explorar o serviço de chamada por meio de diferentes casos de uso

O **Invoke Service** do editor visual de regras permite executar várias operações úteis. Você pode usá-lo para preencher opções suspensas, definir painéis simples ou que possam ser repetidos e validar campos de formulário, tudo com base na resposta de saída do **Chamar serviço**. Dessa forma, melhorando a flexibilidade e a interatividade de seus formulários.

A tabela abaixo descreve alguns cenários nos quais o **Chamar Serviço** pode ser usado:

| **Caso de uso** | **Descrição** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Preencha as opções suspensas usando a saída do Invoke Service** | Preenche opções suspensas dinamicamente com base nos dados recuperados da saída Chamar serviço. [Clique aqui](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service) para ver a implementação. |
| **Definir painel repetível usando a saída de Invocar Serviço** | Configura um painel repetível usando dados da saída Chamar serviço, permitindo painéis dinâmicos. [Clique aqui](#use-case-2-set-repeatable-panel-using-output-of-invoke-service) para ver a implementação. |
| **Definir o painel usando a saída de Chamar Serviço** | Define o conteúdo ou a visibilidade de um painel usando valores específicos da saída Chamar serviço. [Clique aqui](#use-case-3-set-panel-using-output-of-invoke-service) para ver a implementação. |
| **Use o parâmetro de saída do Invoke Service para validar outros campos** | Usa parâmetros de saída específicos do serviço de chamada para validar os campos de formulário. [Clique aqui](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields) para ver a implementação. |
| **Usar carga do evento na ação Navegar para no Serviço de Chamada** | Usa a carga do evento para lidar com respostas de sucesso e falha e para transmitir dados para a ação Navegar para durante a navegação. [Clique aqui](#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service) para ver a implementação. |

Crie um formulário `Get Information` que recupere valores com base na entrada inserida na caixa de texto `Pet ID`. A captura de tela abaixo mostra o formulário usado nesses casos de uso:

![Obter formulário de informações](/help/forms/assets/get-information-form.png)

**Campos de formulário**

Adicione os seguintes campos ao formulário:

* **Inserir identificação do animal de estimação**: Caixa de texto
* **Selecionar URLs de Fotos**: Lista Suspensa
* **Marcas**: Painel
   * Nome: Caixa de texto
   * ID: Caixa de texto
* **Categoria**: Painel
   * Nome: Caixa de texto
* **Enviar**: botão Enviar

>[!NOTE]
>
> No campo **Referência de Ligação** da caixa de diálogo **Propriedades** dos campos de formulário, selecione ![foldersearch_18](assets/folder-search-icon.svg) e navegue para selecionar a propriedade binária adicionada no Modelo de Dados de Formulário (FDM).

**Configurando painéis**

Defina os painéis como repetitivos com as seguintes restrições:

* Valor mínimo: 1
* Valor máximo: 4

Você pode ajustar os valores dos painéis repetitivos para atender às suas necessidades.

**Fonte de dados**

Neste exemplo, a API [Swagger Petstore](https://petstore.swagger.io/) é usada para configurar uma fonte de dados. O [Modelo de Dados de Formulário](/help/forms/create-form-data-models.md) está configurado para o serviço [getPetById](https://petstore.swagger.io/#/pet/getPetById), que recupera detalhes de animal de estimação com base na ID inserida.

Vamos publicar o seguinte JSON usando o serviço [addPet](https://petstore.swagger.io/#/pet/addPet) na API [Swagger Petstore](https://petstore.swagger.io/):

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```

As regras e a lógica são implementadas usando a ação **Invocar Serviço** no editor de regras na caixa de texto `Pet ID` para demonstrar os casos de uso mencionados.

Agora vamos explorar a implementação de cada caso de uso em detalhes.

### Caso de uso 1: Preencher valores suspensos usando a saída de Chamar serviço

Este caso de uso demonstra como preencher opções suspensas dinamicamente com base na saída de um `Invoke Service`.

#### Implementação

Para fazer isso, crie uma regra na caixa de texto `Pet ID` para invocar o serviço `getPetById`. Na regra, defina a propriedade `enum` da lista suspensa `photo-url` como `photoUrls` em **[!UICONTROL Adicionar Manipulador de Êxito]**.

![Definir valor suspenso](/help/forms/assets/set-dropdownoption.png)

>[!NOTE]
>
> Consulte a seção [Adicionando Manipulador de Êxito e Manipulador de Falha](#adding-success-handler-and-failure-handler) para saber como definir manipuladores de sucesso e falha.

#### Saída

Digite `101` na caixa de texto `Pet ID` para preencher dinamicamente as opções suspensas com base no valor inserido.

![Resultado](/help/forms/assets/output1.png)

> 
>
> As opções suspensas também podem ser preenchidas dinamicamente chamando um serviço, analisando a resposta JSON e aplicando funções personalizadas. Para obter mais detalhes, consulte [esta seção](#retrieve-property-values-from-a-json-array).

### Caso de uso 2: definir painel repetível usando a saída de Chamar serviço

Este caso de uso demonstra como preencher painéis repetíveis dinamicamente com base na saída de um **Chamar serviço**.

#### Considerações

* Verifique se o nome do painel repetível corresponde ao parâmetro do **Chamar Serviço** para o qual você deseja definir o painel.
* O painel se repete para o número de valores retornados pelo campo **Chamar Serviço** correspondente.

#### Implementação

Crie uma regra na caixa de texto `Pet ID` para invocar o serviço `getPetById`. Em **[!UICONTROL Adicionar Manipulador de Êxito]**, adicione outra resposta de manipulador de êxito. Defina o valor do painel `tags` como `tags` na regra.

![Criar regra para o painel repetível](/help/forms/assets/create-rule-repeatable-panel.png)

>[!NOTE]
>
> Consulte a seção [Adicionando Manipulador de Êxito e Manipulador de Falha](#adding-success-handler-and-failure-handler) para saber como definir manipuladores de sucesso e falha.

#### Saída

Digite `101` na caixa de texto `Pet ID` para preencher o painel repetível dinamicamente com base no valor de entrada.

![Saída](/help/forms/assets/output2.png)

### Caso de uso 3: definir painel usando a saída de Chamar serviço

Este caso de uso demonstra como definir dinamicamente o valor de um painel com base na saída de um **Chamar serviço**.

#### Considerações

* Verifique se o nome do painel corresponde ao parâmetro do **Chamar Serviço** para o qual você deseja definir o painel.
* O painel repete o número de valores retornados pelo campo Chamar serviço correspondente.

#### Implementação

Crie uma regra na caixa de texto `Pet ID` para invocar o serviço `getPetById`. Em **[!UICONTROL Adicionar Manipulador de Êxito]**, adicione outra resposta de manipulador de êxito. Defina o valor da caixa de texto `categoryname` como `category.name` na regra.

>[!NOTE]
>
> Consulte a seção [Adicionando Manipulador de Êxito e Manipulador de Falha](#adding-success-handler-and-failure-handler) para saber como definir manipuladores de sucesso e falha.

![Criar regra para o painel repetível](/help/forms/assets/set-panel-values.png)

#### Saída

Digite `101` na caixa de texto `Pet ID` para preencher o painel dinamicamente com base no valor de entrada.

![Saída](/help/forms/assets/output3.png)

### Caso de uso 4: usar o parâmetro de saída de Chamar serviço para validar outros campos

Este caso de uso demonstra como usar a saída de um **Chamar Serviço** para validar dinamicamente outros campos de formulário.

#### Implementação

Crie uma regra na caixa de texto `Pet ID` para invocar o serviço `getPetById`. Em **[!UICONTROL Adicionar Manipulador de Falha]**, adicione uma resposta de manipulador de falha. Ocultar o botão **Enviar** se um `Pet ID` incorreto for inserido.

![Manipulador de falhas](/help/forms/assets/create-rule-failure-handler.png)

#### Saída

Digite `102` na caixa de texto `Pet ID` e o botão **Enviar** ficará oculto.

![Saída](/help/forms/assets/output4.png)

### Caso de uso 5: Carga útil do evento de uso em Navegar para ação em Chamar serviço

Este caso de uso demonstra como configurar uma regra no botão **Enviar** que chama um **Chamar Serviço** e redireciona o usuário para outra página usando a ação **Navegar para**.

#### Implementação

Crie uma regra no botão **Enviar** para invocar o serviço de API `redirect-api`. Este serviço é responsável por redirecionar o usuário para o formulário **Fale Conosco**.

Você pode integrar diretamente uma API como o serviço de API `redirect-api` no Editor de regras usando os dados JSON fornecidos abaixo:

```json
{
  "id": "1",
  "path": "/content/dam/formsanddocuments/contact-detail/jcr:content?wcmmode=disabled"
}
```

>[!NOTE]
>
> Para saber como integrar a API diretamente na interface do Editor de regras, [clique aqui](/help/forms/api-integration-in-rule-editor.md) sem usar um Modelo de dados de formulário predefinido.

Em **[!UICONTROL Adicionar Manipulador de Êxito]**, configure a ação **Navegar para** para redirecionar o usuário para a página **Fale Conosco** usando o parâmetro `Event Payload`. Aqui, o usuário pode enviar seus detalhes de contato.

![Carga do evento](/help/edge/docs/forms/assets/navigate-to-eventpayload.png)

Opcionalmente, configure um manipulador de falhas para exibir uma mensagem de erro se a chamada de serviço falhar.

#### Saída

Quando o botão **Enviar** é clicado, o serviço de API `redirect-api` é chamado. Após o sucesso, o usuário será redirecionado para a página **Fale Conosco**.

![Saída de carga do evento](/help/forms/assets/output5.gif)

## Recuperar valores de propriedade de uma matriz JSON

<span class="preview"> Este é um recurso pioneiro. Se você estiver interessado, envie um email rápido do seu endereço comercial para mailto:aem-forms-ea@adobe.com para solicitar acesso ao recurso</a>. </span>

O Adaptive Forms oferece suporte à chamada de um serviço, ao processamento de respostas JSON e ao preenchimento dinâmico de campos de formulário. Esta seção descreve como extrair valores de propriedade de uma matriz JSON e vinculá-los a campos de formulário.

### Exemplo de resposta JSON

O exemplo a seguir representa as regiões de vendas dos EUA e a lista de representantes de vendas:


```json
[
  {
    "region": "East",
    "salesPerson": "Emily Carter"
  },
  {
    "region": "South",
    "salesPerson": "Michael Brown"
  },
  {
    "region": "Midwest",
    "salesPerson": "Sophia Martinez"
  },
  {
    "region": "Southwest",
    "salesPerson": "David Johnson"
  },
  {
    "region": "West",
    "salesPerson": "Linda Walker"
  }
]
```

### Função personalizada para extrair valores de propriedade

Use a seguinte função personalizada para extrair valores de propriedade da matriz JSON.

```js
/**
 * Returns an array of values for a specific property from an array of objects.
 *
 * @name getPropertyValues
 * @param {Object[]} jsonArray An array of objects
 * @param {string} propertyName The property whose values should be extracted
 * @returns {Array} An array containing the values of the specified property
 *
 */

function getPropertyValues(jsonArray, propertyName)
{
    return jsonArray.map((obj) => obj[propertyName]);

}
```

A função personalizada aceita:

* **jsonArray**: matriz JSON retornada do serviço
* **propertyName**: propriedade para extrair o valor

A função personalizada retorna uma matriz simples de valores.

>[!NOTE]
>
> Para obter etapas detalhadas sobre como adicionar funções personalizadas, consulte o artigo [Introdução a Funções personalizadas para Forms adaptável com base em Componentes principais](/help/forms/create-and-use-custom-functions.md).


### Usar a função no Editor de regras

Para recuperar o valor específico da matriz JSON:

```
event.payload.invokeServiceResponse.rawPayloadBody
```

O exemplo a seguir demonstra como preencher um formulário `Sales Department` usando esta resposta.

Por exemplo, vamos criar um formulário `Sales Department` que inclua os menus suspensos `Select Region` e `Select Sales Representative`.

**Etapa 1: chamar o serviço na inicialização do formulário**

```
WHEN
    Form is initialized
THEN
    Invoke Service → salesdeptinfo
```

>[!NOTE]
>
> Para saber como integrar a API sem criar um Modelo de dados de formulário no Editor de regras visuais, [clique aqui](/help/forms/api-integration-in-rule-editor.md).

**Etapa 2: Preencher a lista suspensa de Região**

Adicione um Manipulador de sucesso para a chamada de serviço e configure a seguinte ação:

```
Set enum → Region dropdown
getPropertyValues(
    event.payload.invokeServiceResponse.rawPayloadBody,
    "region"
)
```

Esta regra lê a matriz JSON, extrai os valores de propriedade `region` e atribui os valores à lista suspensa `Select Region`.

Da mesma forma, configure a ação para a lista suspensa `Select Sales Representative` no Manipulador de sucesso.

![Carga do evento para a matriz JSON](/help/forms/assets/event-payload.png)

Quando o formulário carrega, os dados JSON são retornados e a função personalizada extrai os valores de propriedade e a lista suspensa é preenchida automaticamente:

![Formulário de carga do evento](/help/forms/assets/event-payload-form.png)

## Perguntas frequentes

**P: O que acontece se eu tiver criado uma regra usando o Serviço de Chamada e depois atualizar para a versão mais recente dos componentes principais?**

**A:** Quando você atualiza para a versão mais recente dos componentes principais, a regra **Invocar Serviço** atualiza automaticamente para a interface do usuário mais recente, pois ela é compatível com versões anteriores.

**P: Posso adicionar várias regras para lidar com respostas bem-sucedidas ou com falhas para a operação Invoke Service?**

**A:** Sim, você pode adicionar várias regras para lidar com respostas bem-sucedidas ou com falhas para a operação **Invocar Serviço**.

## Artigos relacionados

* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário (FDM)](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário (FDM)](work-with-form-data-model.md)
* [Usar o modelo de dados de formulário (FDM)](using-form-data-model.md)


## Recursos adicionais

{{see-also-rule-editor}}
