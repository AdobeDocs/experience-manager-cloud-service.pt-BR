---
title: Quais são as melhorias no VRE do serviço de Chamada para formulários baseados nos Componentes principais?
description: Aprimoramentos no serviço de Chamada do editor de regras
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: chame os aprimoramentos do serviço no VRE, preenchendo as opções suspensas usando invocar serviço, Defina o painel repetível usando a saída de invocar serviço, Defina o painel usando a saída de invocar serviço, Use o parâmetro de saída de invocar serviço para validar outro campo.
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 33dcc771c8c2deb2e5fcb582de001ce5cfaa9ce4
workflow-type: tm+mt
source-wordcount: '1598'
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
* Certifique-se de que os Componentes principais estejam habilitados para o seu ambiente. Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service.

## Explorar o serviço de chamada por meio de diferentes casos de uso

O **Invoke Service** do editor visual de regras permite executar várias operações úteis. Você pode usá-lo para preencher opções suspensas, definir painéis simples ou que possam ser repetidos e validar campos de formulário, tudo com base na resposta de saída do **Chamar serviço**. Dessa forma, melhorando a flexibilidade e a interatividade de seus formulários.

A tabela abaixo descreve alguns cenários nos quais o **Chamar Serviço** pode ser usado:

| **Caso de uso** | **Descrição** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Preencha as opções suspensas usando a saída do Invoke Service** | Preenche opções suspensas dinamicamente com base nos dados recuperados da saída Chamar serviço. [Clique aqui](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service) para ver a implementação. |
| **Definir painel repetível usando a saída de Invocar Serviço** | Configura um painel repetível usando dados da saída Chamar serviço, permitindo painéis dinâmicos. [Clique aqui](#use-case-2-set-repeatable-panel-using-output-of-invoke-service) para ver a implementação. |
| **Definir o painel usando a saída de Chamar Serviço** | Define o conteúdo ou a visibilidade de um painel usando valores específicos da saída Chamar serviço. [Clique aqui](#use-case-3-set-panel-using-output-of-invoke-service) para ver a implementação. |
| **Use o parâmetro de saída do Invoke Service para validar outros campos** | Usa parâmetros de saída específicos do serviço de chamada para validar os campos de formulário. [Clique aqui](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields) para ver a implementação. |

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

#### Saída

Digite `101` na caixa de texto `Pet ID` para preencher dinamicamente as opções suspensas com base no valor inserido.

![Resultado](/help/forms/assets/output1.png)

### Caso de uso 2: definir painel repetível usando a saída de Chamar serviço

Este caso de uso demonstra como preencher painéis repetíveis dinamicamente com base na saída de um **Chamar serviço**.

#### Considerações

* Verifique se o nome do painel repetível corresponde ao parâmetro do **Chamar Serviço** para o qual você deseja definir o painel.
* O painel se repete para o número de valores retornados pelo campo **Chamar Serviço** correspondente.

#### Implementação

Crie uma regra na caixa de texto `Pet ID` para invocar o serviço `getPetById`. Em **[!UICONTROL Adicionar Manipulador de Êxito]**, adicione outra resposta de manipulador de êxito. Defina o valor do painel `tags` como `tags` na regra.

![Criar regra para o painel repetível](/help/forms/assets/create-rule-repeatable-panel.png)

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

>[!NOTE]
>
> Você também pode [integrar a API diretamente na interface do Editor de regras](/help/forms/api-integration-in-rule-editor.md) sem usar um modelo de dados de formulário predefinido.

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
