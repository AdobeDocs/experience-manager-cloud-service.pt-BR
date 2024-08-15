---
title: Encaminhamento de logs para o AEM as a Cloud Service
description: Saiba mais sobre como encaminhar logs para o Splunk e outros fornecedores de registro em log na AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Encaminhamento de logs {#log-forwarding}

>[!NOTE]
>
>Esse recurso ainda não foi lançado e alguns destinos de registro podem não estar disponíveis no momento do lançamento. Enquanto isso, você pode abrir um tíquete de suporte para encaminhar logs para o **Splunk**, conforme descrito em [Logon no AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md).

Os clientes que têm uma licença para um fornecedor de registro ou hospedam um produto de registro podem ter registros AEM (incluindo Apache/Dispatcher) e registros CDN encaminhados aos destinos de registro associados. O AEM as a Cloud Service oferece suporte aos seguintes destinos de registro:

* Armazenamento Azure Blob
* DataDog
* Elasticsearch ou OpenSearch
* HTTPS
* Splunk

O encaminhamento de logs é configurado de maneira automatizada declarando uma configuração no Git e implantando-a por meio do Pipeline de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção em programas de produção (não sandbox).

Há uma opção para que os registros AEM e Apache/Dispatcher sejam roteados por meio da infraestrutura de rede avançada do AEM, como IP de saída dedicado.

Observe que a largura de banda da rede associada aos registros enviados ao destino de registro é considerada parte do uso de E/S da rede da organização.


## Como este artigo está organizado {#how-organized}

Este artigo está organizado da seguinte maneira:

* Configuração - comum para todos os destinos de registro
* Configurações de destino de registro - cada destino tem um formato um pouco diferente
* Formatos de Entrada de Log - informações sobre os formatos de entrada de log
* Rede avançada - envio de registros AEM e Apache/Dispatcher por meio de uma saída dedicada ou por meio de uma VPN


## Configurar {#setup}

1. Crie a seguinte estrutura de pasta e arquivo na pasta de nível superior em seu projeto no Git:

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml` deve conter metadados e uma configuração semelhante ao seguinte formato (usamos o Splunk como exemplo).

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

   O parâmetro **kind** deve ser definido como `LogForwarding`, a versão deve ser definida como a versão do esquema, que é 1.

   Os tokens na configuração (como `${{SPLUNK_TOKEN}}`) representam segredos que não devem ser armazenados no Git. Em vez disso, declare-as como [Variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md) do Cloud Manager do tipo **segredo**. Selecione **Todos** como o valor suspenso do campo Serviço aplicado, para que os logs possam ser encaminhados para os níveis de criação, publicação e visualização.

   É possível definir valores diferentes entre logs CDN e logs AEM (incluindo Apache/Dispatcher), incluindo um bloco **cdn** e/ou **aem** adicional após o bloco **padrão**, em que as propriedades podem substituir as definidas no bloco **padrão**; somente a propriedade habilitada é necessária. Um possível caso de uso poderia ser o uso de um índice do Splunk diferente para logs CDN, como ilustra o exemplo abaixo.

   ```
      kind: "LogForwarding"
      version: "1"
      metadata:
        envTypes: ["dev"]
      data:
        splunk:
          default:
            enabled: true
            host: "splunk-host.example.com"
            token: "${{SPLUNK_TOKEN}}"
            index: "AEMaaCS"
          cdn:
            enabled: true
            token: "${{SPLUNK_TOKEN_CDN}}"
            index: "AEMaaCS_CDN"   
   ```

   Outro cenário é desabilitar o encaminhamento dos logs CDN ou dos logs AEM (incluindo o Apache/Dispatcher). Por exemplo, para encaminhar apenas os logs CDN, é possível configurar o seguinte:

   ```
      kind: "LogForwarding"
      version: "1"
      metadata:
        envTypes: ["dev"]
      data:
        splunk:
          default:
            enabled: true
            host: "splunk-host.example.com"
            token: "${{SPLUNK_TOKEN}}"
            index: "AEMaaCS"
          aem:
            enabled: false
   ```

1. Para tipos de ambiente diferentes do RDE (que não é compatível no momento), crie um pipeline de configuração de implantação direcionada no Cloud Manager; observe que os pipelines de Empilhamento completo e de Camada da Web não implantam o arquivo de configuração.

   * [Consulte configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Consulte configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Configuração de destino de registro {#logging-destinations}

As configurações para os destinos de registro compatíveis estão listadas abaixo, juntamente com considerações específicas.

### Armazenamento Azure Blob {#azureblob}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

Um token SAS deve ser usado para autenticação. Ela deve ser criada na página Shared access signature, em vez de na página Shared access token, e deve ser configurada com estas configurações:

* Serviços permitidos: o blob deve ser selecionado.
* Recursos permitidos: o objeto deve ser selecionado.
* Permissões permitidas: Gravar, Adicionar, Criar devem ser selecionadas.
* Uma data/hora de início e expiração válidas.

Esta é uma captura de tela de um exemplo de configuração de token SAS:

![Configuração de token SAS do Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Logs CDN do Armazenamento de Blobs do Azure {#azureblob-cdn}

Cada um dos servidores de log distribuídos globalmente produzirá um novo arquivo a cada poucos segundos, na pasta `aemcdn`. Depois de criado, o arquivo não será mais anexado ao. O formato do nome do arquivo é AAAA-MM-DDThh:mm:ss.sss-uniqueid.log. Por exemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Como exemplo, em algum momento:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

E 30 segundos depois:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Cada arquivo contém várias entradas de log json, cada uma em uma linha separada. Os formatos de entrada de log estão descritos em [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md), e cada entrada de log também inclui as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-format) abaixo.

#### Logs AEM do Armazenamento Azure Blob {#azureblob-aem}

Os logs de AEM (incluindo o Apache/Dispatcher) aparecem abaixo de uma pasta com a seguinte convenção de nomenclatura:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

Em cada pasta, um único arquivo será criado e anexado a. Os clientes são responsáveis pelo processamento e gerenciamento desse arquivo, de modo que ele não fique muito grande.

Consulte os formatos de entrada de log em [Log para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). As entradas de log também incluirão as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

Considerações:

* Crie uma Chave de API sem nenhuma integração com um provedor de nuvem específico.
* a propriedade tags é opcional


### Elasticsearch e OpenSearch {#elastic}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

Considerações:

* Para credenciais, certifique-se de usar as credenciais de implantação, em vez das credenciais de conta. Estas são as credenciais geradas em uma tela que pode se parecer com esta imagem:

![Credenciais de implantação elástica](/help/implementing/developing/introduction/assets/ec-creds.png)

* A propriedade opcional do pipeline deve ser definida como o nome do pipeline de assimilação de Elasticsearch ou OpenSearch, que pode ser configurado para rotear a entrada de log para o índice apropriado. O tipo de Processador do pipeline deve ser definido como *script* e a linguagem de script deve ser definida como *indolor*. Este é um exemplo de trecho de script para rotear entradas de log em um índice, como aemaccess_dev_26_06_2024:

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com:8443/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

Considerações:

* A cadeia de caracteres da URL deve incluir **https://** ou a validação falhará. Se nenhuma porta for incluída na string do URL, a porta 443 (a porta HTTPS padrão) será considerada.
* Se você quiser usar uma porta diferente de 443, forneça-a como parte do URL.

#### Logs HTTPS CDN {#https-cdn}

As solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com o formato de entrada de log descrito em [Logon para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

Também existe uma propriedade chamada `sourcetype`, que é definida como o valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar a primeira entrada de log CDN, o servidor HTTP deve concluir com êxito um desafio único: uma solicitação enviada para o caminho ``/.well-known/fastly/logging/challenge`` deve responder com um asterisco ``*`` no corpo e código de status 200.

#### Logs AEM HTTPS {#https-aem}

Para logs AEM (incluindo apache/dispatcher), as solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com os vários formatos de entrada de log, conforme descrito em [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-format) abaixo.

Também há uma propriedade chamada `sourcetype`, que é definida como um destes valores:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

### Splunk {#splunk}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## Formatos de entrada de log {#log-formats}

Consulte [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) para o formato de cada respectivo tipo de log (logs CDN e logs AEM, incluindo Apache/Dispatcher).

Como os registros de vários programas e ambientes podem ser encaminhados para o mesmo destino de registro, além da saída descrita no artigo de registro, as seguintes propriedades serão incluídas em cada entrada de registro:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Como exemplo, as propriedades podem ter os seguintes valores:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Rede avançada {#advanced-networking}

>[!NOTE]
>
>Esse recurso ainda não está pronto para os participantes iniciais.


Algumas organizações escolhem restringir qual tráfego pode ser recebido pelos destinos de registro.

Para o log CDN, você pode adicionar os endereços IP à lista de permissões, conforme descrito em [Documentação rápida - Lista de IP Públicos](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se essa lista de endereços IP compartilhados for muito grande, considere enviar tráfego para um Azure Blob Store (não Adobe) em que a lógica possa ser gravada para enviar os logouts de um IP dedicado para seu destino final.

Para logs AEM (incluindo Apache/Dispatcher), você pode configurar o encaminhamento de logs para passar pela [rede avançada](/help/security/configuring-advanced-networking.md). Consulte os padrões dos três tipos avançados de rede abaixo, que usam um parâmetro `port` opcional, juntamente com o parâmetro `host`.

### Saída flexível da porta {#flex-port}

Se o tráfego de log for para uma porta diferente da 443 (por exemplo, 8443 abaixo), configure a rede avançada da seguinte maneira:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

e configure o arquivo yaml da seguinte maneira:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "${{AEM_PROXY_HOST}}"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### IP de saída dedicado {#dedicated-egress}


Se o tráfego de log precisar vir de um IP de saída dedicado, configure redes avançadas da seguinte maneira:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

e configure o arquivo yaml da seguinte maneira:

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

Se o tráfego de log precisar passar por uma VPN, configure a rede avançada da seguinte maneira:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
