---
title: API de integração no Editor de regras para o Forms
description: Saiba mais sobre os últimos aprimoramentos do Serviço de chamada no Editor de regras, incluindo como integrar APIs para Forms adaptável com base em Componentes principais sem usar um Modelo de dados de formulário.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: integração da API no editor de regras, chame as melhorias no serviço
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 478b9c21e5b96dc31f5926a49864ea867e1ae86c
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 2%

---

# Integração da API no Editor de regras

<span>A integração da API no Editor de regras está no Programa de Primeiros Usuários. Você pode escrever para `aem-forms-ea@adobe.com` com sua ID de email oficial para entrar no programa de primeiros usuários e solicitar acesso ao recurso.</span>

>[!NOTE]
>
> O Editor de Regras Visuais oferece suporte à integração de API no Forms Adaptável com base nos Componentes Principais e no [Edge Delivery Services Forms criado no Editor Universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

O Editor de regras visuais no Adaptive Forms oferece suporte à integração direta de API sem criar um Modelo de dados de formulário. Você pode se conectar a um endpoint de API inserindo o URL da API (no formato JSON) ou importando a configuração por meio de um comando cURL. Depois de integrada, a ação **Invocar Serviço** pode ser usada para chamar a API.

Os campos de formulário podem ser mapeados diretamente para os parâmetros de entrada definidos na configuração da API. Da mesma forma, os parâmetros de saída podem ser mapeados para campos de formulário usando a opção **carga do evento** para a resposta da API correspondente.

Além disso, o Editor de Regras Visuais permite que você defina **sucesso** e **manipuladores de falha** ao invocar um serviço. Os manipuladores de sucesso especificam as ações a serem executadas após uma chamada de API bem-sucedida, enquanto os manipuladores de falha definem como o formulário deve responder quando ocorrer um erro.

## Comparação: Métodos de integração de API

| Aspecto | Integração da API com o Modelo de dados de formulário (FDM) | Integração direta de API (via *Criar integração de API*) |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **Finalidade** | Integração de API centralizada e reutilizável em vários formulários | Integração de API rápida e específica do formulário |
| **Local da Instalação** | Criado e editado no Editor de modelo de dados de formulário (console AEM) | Criado e editado diretamente no Editor de regras do formulário adaptável |
| **Complexidade** | Maior esforço de instalação (requer mapeamento e configuração) | Simples e leve |
| **Mais Adequado Para** | Casos de uso corporativos ou de grande escala com vários formulários | Pequenos formulários, protótipos ou chamadas de API únicos |

## Configuração da integração da API

A captura de tela abaixo exibe a janela de configuração da integração de API:

![Configuração de Integração de API](/help/forms/assets/api-integration-configuration.png)

### Opções de configuração de chave

**Configuração de Integração de API**

* **Importar de cURL**: configure a integração da API colando um comando cURL pronto, em vez de inserir manualmente detalhes como URL da API, método HTTP, cabeçalhos e parâmetros.
* **Nome para Exibição**: nome personalizado para o serviço de API.
* **URL da API**: Ponto de extremidade do serviço de API.
* **Selecionar método HTTP**: o método de solicitação HTTP usado para chamar a API.
* **Tipo de conteúdo**: define o formato de solicitação e resposta.
* **Criptografia necessária**: (opcional) garante que dados confidenciais sejam criptografados durante a transmissão.
* **Executar no Cliente**: quando habilitado, a chamada à API é feita do cliente (navegador) em vez do servidor.

**Tipo de autenticação**

* **Opções**: nenhuma, Básica, Chave de API, OAuth 2.0.

**Parâmetros de entrada**

* **Carregar JSON para Entrada**: carregue um arquivo JSON de amostra para preencher automaticamente os mapeamentos de entrada.
   * **Nome**: nome do parâmetro de entrada exigido pela API.
   * **Tipo**: tipo de dados da entrada (Cadeia de caracteres, Número, Booleano, etc.).
   * **Em**: Local do parâmetro (Consulta, Cabeçalho ou Corpo).
   * **Valor Padrão**: valor pré-preenchido se não fornecido pelo usuário.
   * **Adicionar**: opção para adicionar mais parâmetros de entrada.

**Parâmetros de saída**

* **Carregar JSON para Saída**: carregue uma resposta de API de exemplo para gerar mapeamentos automaticamente.
   * **Nome**: nome do parâmetro de saída da resposta da API.
   * **Tipo**: tipo de dados esperado do parâmetro de saída (Cadeia de caracteres, Número, etc.).
   * **Em**: define onde o valor mapeado é esperado.
   * **Adicionar/Excluir**: adicione novos mapeamentos ou remova os existentes.

## Caso de uso: Preencher campos do país em um formulário de solicitação de visto

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**Cenário**: uma agência governamental fornece um Formulário de Solicitação de Visto online com os seguintes campos:

1. Nome completo (Texto)
2. Data de nascimento (Data)
3. País de cidadania (lista suspensa)
4. Número do Passaporte (Texto)
5. País de emissão do passaporte (suspenso)
6. País de destino (suspenso)
7. Data prevista de chegada (Data)

Em vez de manter uma lista estática de países, o formulário busca dinamicamente informações de países (continente, capital, códigos ISO Alpha etc.) usando a **API getcountryname**:

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

Isso garante que os candidatos sempre vejam uma lista atualizada e precisa de países enquanto preenchem o formulário.

### Implementação usando a integração de API no Editor de regras

É possível integrar uma API sem criar um modelo de dados de formulário clicando no botão **Criar integração de API** no Editor de regras.

![Criar Integração de API](/help/forms/assets/create-api-integration.png)

Um serviço de API chamado **getcountryname** está configurado na **Configuração de Integração de API** no Editor de Regras:

![Configuração de Ponto de Extremidade rest de API](/help/forms/assets/api-restendpoint.png)

* **URL do Ponto de Extremidade da API** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **Método HTTP** → GET
* **Tipo de conteúdo** → JSON
* **Entrada** → `username` passado como parâmetro de consulta (`aemforms`).
* **Saída** → Campos de resposta como `continent`, `capital`, `countrynames`, `isoAlpha3` e `languages` são mapeados para campos de formulário.

No **Formulário de Solicitação de Visto**, os três campos suspensos, **País de Cidadania**, **País de Emissão de Passaporte** e **País de Destino**, estão vinculados à ação **Invocar Serviço**.

Quando o formulário é carregado, o **Invoke Service** busca a lista de países da API. A resposta é mapeada para preencher automaticamente as opções suspensas.

Por exemplo, quando o usuário abre **País de cidadania**, a lista de países é exibida dinamicamente na resposta da API.

![invocar-serviço-api-integração](/help/forms/assets/invoke-service-api-integration.png)

![Saída de integração de API](/help/forms/assets/api-integration-output.png)

Da mesma forma, o **País de Emissão de Passaporte** e o **País de Destino** usam a mesma chamada de API, garantindo dados consistentes e atualizados em todos os três campos.

>
>
> Você pode [recuperar valores de propriedade de uma matriz JSON invocando uma API e usando uma função personalizada](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array). Essa abordagem permite extrair valores e vinculá-los diretamente aos campos de formulário.

## Implementação do mecanismo de repetição para falhas de API

Quando uma solicitação de API falha, geralmente é útil repetir a solicitação antes de relatar um erro ao usuário. Você pode implementar um mecanismo de pesquisa e tentativa gravando o código personalizado no arquivo **function.js**.

O exemplo a seguir demonstra como lidar com falhas de API com até duas tentativas de repetição e retrocesso exponencial entre tentativas:

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

No código acima, a função **retryHandler** gerencia solicitações de API com tentativas automáticas em caso de falha. Ele executa uma função de solicitação (requestFn) e tenta a solicitação até duas vezes, adicionando metadados para cada tentativa.

## Perguntas frequentes

* **Preciso criar um Modelo de Dados de Formulário para integrar uma API no Adaptive Forms?**\
  Não. Com o Editor de Regras Visuais, você pode integrar APIs diretamente usando a opção **Criar Integração de API** sem criar um Modelo de Dados de Formulário. Essa abordagem é mais adequada para casos de uso leves ou específicos de formulários.

* **É possível proteger chamadas de API feitas pelo Editor de Regras?**\
  Sim. A Configuração de Integração de API fornece opções de autenticação, como **Básico, Chave de API e OAuth 2.0**. Você também pode habilitar a opção **Criptografia necessária** para garantir que os dados confidenciais sejam transmitidos com segurança.
