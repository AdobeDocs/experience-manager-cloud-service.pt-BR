---
title: Funções do AEM Edge
description: Saiba como executar o JavaScript na camada CDN com as funções do AEM Edge para permitir personalização, segurança e experiências dinâmicas próximas ao usuário final.
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: f8000bef01d6b72fb3ac2ae81be9fc19ed1a67d1
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---


# Funções do AEM Edge {#aem-edge-functions}

>[!IMPORTANT]
>
>O AEM Edge Functions é um recurso **beta**. Os recursos e a documentação podem mudar sem aviso prévio. Para participar do programa de acesso antecipado e fornecer feedback, envie um email para [aemcs-edge-functions-feedback@adobe.com](mailto:aemcs-edge-functions-feedback@adobe.com).

O AEM Edge Functions permite executar o JavaScript na camada de CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas sem uma viagem de ida e volta à sua origem.

Casos de uso comuns incluem:

- Personalização de conteúdo com base em informações como geolocalização, tipo de dispositivo ou atributos do usuário
- Atuar como middleware entre a CDN e sua origem
- Reformatação ou agregação de respostas de APIs de terceiros antes que elas cheguem ao navegador
- Compondo e disponibilizando HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends

O AEM Edge Functions é compatível com o Java-stack do Edge Delivery Services e do AEM Cloud Service.

## Principais benefícios {#key-benefits}

| Benefício | Descrição |
|---|---|
| **Desempenho** | TTFB rápido por meio do SSR de borda que retorna o HTML totalmente renderizado. Chamadas de API de baixa latência por meio de buscas paralelas e saltos de rede otimizados. |
| **SEO / GEO** | O HTML do servidor é indexado no primeiro rastreo. O conteúdo totalmente renderizado está pronto para rastreadores de IA. |
| **Segurança** | Manter as credenciais de API no lado do servidor ocultas do JavaScript cliente. Autentique com um provedor de identidade e restrinja o acesso ao conteúdo. |
| **Personalização** | Personalize o conteúdo antes que a página seja carregada com base nos sinais de localização geográfica e do dispositivo. Execute pesquisas de público-alvo na borda para entrega direcionada. |

## Pré-requisitos {#prerequisites}

- Um ambiente do AEM as a Cloud Service
- O Perfil de Produto de Administrador do AEM na instância de autor do seu ambiente do Cloud Service, **ou** a função de Gerente de Implantação do Cloud Manager no Admin Console para sites do Edge Delivery Services
- [Node.js e npm](https://nodejs.org/)

## Configurar {#setup}

### Instalar a CLI do Adobe {#install-adobe-cli}

Instale a CLI do Adobe Developer (`aio`):

```bash
npm install -g @adobe/aio-cli
```

Instale o plug-in AEM Edge Functions:

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

Autentique e configure o plug-in para o seu ambiente:

```bash
aio login
aio aem edge-functions setup
```

O comando de configuração solicita que você faça logon e selecione o ambiente do AEM no qual deseja usar as funções do AEM Edge.

### Clonar a chapa {#boilerplate}

Copie o [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) no seu próprio repositório e instale as dependências:

```bash
npm install
```

## Crie sua primeira função {#create-your-function}

Os serviços de função do AEM Edge são declarados em um arquivo de configuração YAML e implantados por meio do pipeline de configuração do Cloud Manager.

### &#x200B;1. Definir um pipeline de configuração {#configuration-pipeline}

Antes de criar uma função de borda, verifique se existe um pipeline de configuração para o seu ambiente no Cloud Manager. Caso contrário, [crie um pipeline de configuração](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) primeiro.

>[!NOTE]
>
>Se você estiver usando um Ambiente de Desenvolvimento Rápido (RDE), é possível implantar a configuração diretamente com o `aio aem rde:install -t env-config ./config`, em vez de passar por um pipeline de configuração.

### &#x200B;2. Declarar os serviços de função da Edge {#declare-services}

Crie um arquivo chamado `edgeFunctions.yaml` no diretório de configuração:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: first-function
    - name: second-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

A configuração aceita até três serviços. As teclas de nível superior são:

| Chave | Descrição |
|---|---|
| `services` | Lista de serviços de função de borda, cada um identificado por um `name`. |
| `configs` | Pares de chave/valor expostos a todos os serviços de função de borda como variáveis de ambiente. |
| `secrets` | Pares de chave/valor que fazem referência a segredos do Cloud Manager, expostos a todos os serviços de função de borda. |

### &#x200B;3. Adicionar Regras do Seletor de Origem CDN {#cdn-routing}

As funções do Edge são invocadas pelo roteamento de tráfego CDN para elas por meio de regras do seletor de origem. Adicione o seguinte ao arquivo de configuração `cdn.yaml` (ou crie um caso ele não exista):

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-first-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-first-function
      - name: route-to-second-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-second-function
```

As regras do seletor de origem permitem rotear o tráfego para suas funções de borda com base em qualquer condição disponível no mecanismo de regras CDN, como um caminho, domínio ou cabeçalho de solicitação específico. Consulte [Seletores de Origem](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) para obter a sintaxe de regra completa.

### &#x200B;4. Implantar a configuração {#deploy-configuration}

Confirme `edgeFunctions.yaml` e `cdn.yaml` no repositório Git do Cloud Manager e acione o pipeline de configuração. Depois que o pipeline for concluído com êxito, seus pontos de extremidade de função de borda estarão disponíveis em:

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

onde `pXXXXX-eYYYYY` são as coordenadas do seu ambiente. Se um domínio personalizado estiver configurado, as funções também poderão ser acessadas nesses caminhos de domínio (por exemplo, `example.com/weather`).

## Criar e implantar o código de função do AEM Edge {#build-deploy}

### Build {#build}

Crie um pacote do código de função de borda para implantação:

```bash
aio aem edge-functions build
```

### Implantar {#deploy}

Implante o pacote criado em um serviço de função de borda nomeado. O argumento `function-name` deve corresponder ao valor `name` em `edgeFunctions.yaml`:

```bash
aio aem edge-functions deploy <function-name>
```

## Desenvolvimento local {#local-development}

### Executar localmente {#local-run}

Iniciar um servidor de desenvolvimento local em `http://127.0.0.1:7676`:

```bash
aio aem edge-functions serve
```

Consulte esta [documentação do Compute JavaScript](https://www.fastly.com/documentation/guides/compute/javascript/) para obter detalhes sobre o que o tempo de execução local suporta.

### Teste {#test}

Execute o conjunto de testes com [Mocha](https://mochajs.org/):

```bash
npm run test
```

### Depuração remota {#remote-debugging}

O Adobe Managed CDN não expõe um depurador remoto, mas expõe o fluxo de log. Siga os logs de uma função implantada para receber saída de `console.log` diretamente em seu terminal:

```bash
aio aem edge-functions tail-logs <function-name>
```

## Referência da configuração {#configuration-reference}

### Origens {#origins}

Por padrão, as funções de borda podem buscar de qualquer origem. Para restringir uma função a um conjunto definido de origens, declare-as em `origins` em `edgeFunctions.yaml`:

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

Referencie a origem nomeada em seu código de função usando a opção de busca `backend`:

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

### Configuração do serviço {#service-configuration}

Exponha variáveis de ambiente a suas funções usando a chave `configs` em `edgeFunctions.yaml`. Os valores são armazenados em um repositório de configuração chamado `config_default`:

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

Leia os valores de configuração no seu código de função:

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- O repositório de configuração é sempre nomeado como `config_default`.
>- Os nomes de chave fazem distinção entre maiúsculas e minúsculas.
>- O armazenamento de configuração é compartilhado em todos os serviços de função de borda no mesmo ambiente.

### Segredos do serviço {#service-secrets}

Segredos são referenciados, não armazenados, em `edgeFunctions.yaml`. O campo `value` deve apontar para um segredo Cloud Manager usando a sintaxe `${{SECRET_REFERENCE}}`. Primeiro defina o segredo subjacente no Cloud Manager — consulte [Variáveis Secretas do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

Recupere segredos em seu código de função usando o auxiliar `SecretStoreManager` da chapa padrão:

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- O armazenamento secreto sempre se chama `secret_default`.
>- Os nomes de chave fazem distinção entre maiúsculas e minúsculas.
>- Segredos são imutáveis uma vez criados.
>- O armazenamento secreto é compartilhado em todos os serviços de função de borda no mesmo ambiente.

### Logs {#logging}

O AEM Edge Functions é integrado ao recurso [Encaminhamento de logs do AEM](/help/implementing/developing/introduction/log-forwarding.md). Crie um arquivo `logForwarding.yaml` junto com seu `edgeFunctions.yaml`:

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Use o agente de log no código da função para gravar entradas de log estruturadas:

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>Os logs CDN — que incluem entradas de log de função do AEM Edge — podem ser baixados do Cloud Manager para ambientes Java-stack, mas não para sites do Edge Delivery Services.
>
