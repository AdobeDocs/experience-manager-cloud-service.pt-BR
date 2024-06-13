---
title: Encaminhamento de logs para AEM as a Cloud Service
description: Saiba mais sobre como encaminhar logs para o Splunk e outros fornecedores de registro no AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e007f2e3713d334787446305872020367169e6a2
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Encaminhamento de logs {#log-forwarding}

>[!NOTE]
>
>Esse recurso ainda não foi lançado e alguns destinos de registro podem não estar disponíveis no momento do lançamento. Enquanto isso, você pode abrir um tíquete de suporte para encaminhar logs para **Splunk**, conforme descrito na seção [artigo de registro](/help/implementing/developing/introduction/logging.md).

Os clientes que têm uma licença para um fornecedor de registro ou hospedam um produto de registro em log podem ter registros AEM (incluindo Apache/Dispatcher) e registros CDN encaminhados aos destinos de registro associados. O AEM as a Cloud Service é compatível com os seguintes destinos de registro:

* Armazenamento Azure Blob
* DataDog
* Elasticsearch ou OpenSearch
* HTTPS
* Splunk

O encaminhamento de logs é configurado de maneira automatizada declarando uma configuração no Git e implantando-a por meio do Pipeline de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção em programas de produção (não sandbox).

Há uma opção para que os registros do AEM e do Apache/Dispatcher sejam roteados por meio de infraestruturas de rede avançadas do AEM, como IP de saída dedicado.

Observe que a largura de banda da rede associada aos registros enviados ao destino de registro é considerada parte do uso de E/S da rede da organização.


## Como este artigo está organizado {#how-organized}

Este artigo está organizado da seguinte maneira:

* Configuração - comum para todos os destinos de registro
* Configurações de destino de registro - cada destino tem um formato um pouco diferente
* Formatos de Entrada de Log - informações sobre os formatos de entrada de log
* Rede avançada - envio de logs do AEM e do Apache/Dispatcher por meio de uma saída dedicada ou por meio de uma VPN


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

   A variável **tipo** O parâmetro deve ser definido como `LogForwarding` a versão deve ser definida como a versão do schema, que é 1.

   Os tokens na configuração (como `${{SPLUNK_TOKEN}}`) representam segredos, que não devem ser armazenados no Git. Em vez disso, declare-os como Cloud Manager  [Variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md) do tipo **segredo**. Selecione **Todos** como o valor suspenso do campo Serviço aplicado, os logs podem ser encaminhados para os níveis de criação, publicação e visualização.

   É possível definir valores diferentes entre os logs CDN e logs AEM (incluindo o Apache/Dispatcher), incluindo um **cdn** e/ou **aem** bloco após o **padrão** bloco, em que as propriedades podem substituir as definidas no **padrão** bloco; somente a propriedade enabled é necessária. Um possível caso de uso poderia ser o uso de um índice do Splunk diferente para logs CDN, como ilustra o exemplo abaixo.

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

   Outro cenário é desativar o encaminhamento dos logs CDN ou AEM (incluindo o Apache/Dispatcher). Por exemplo, para encaminhar apenas os logs CDN, é possível configurar o seguinte:

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

1. Para tipos de ambiente diferentes de RDE (que não é compatível no momento), crie um pipeline de configuração de implantação direcionada no Cloud Manager.

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

![Configuração do token SAS do Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Logs CDN do Armazenamento de Blobs do Azure {#azureblob-cdn}

Cada um dos servidores de registro distribuídos globalmente produzirá um novo arquivo a cada poucos segundos, no `aemcdn` pasta. Depois de criado, o arquivo não será mais anexado ao. O formato do nome do arquivo é AAAA-MM-DDThh:mm:ss.sss-uniqueid.log. Por exemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

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

Cada arquivo contém várias entradas de log json, cada uma em uma linha separada. Os formatos de entrada de log estão descritos no [artigo de registro](/help/implementing/developing/introduction/logging.md), e cada entrada de log também inclui as propriedades adicionais mencionadas na variável [Formatos de entrada de log](#log-format) abaixo.

#### Logs AEM do Armazenamento Azure Blob {#azureblob-aem}

Os logs de AEM (incluindo o Apache/Dispatcher) aparecem abaixo de uma pasta com a seguinte convenção de nomenclatura:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

Em cada pasta, um único arquivo será criado e anexado a. Os clientes são responsáveis pelo processamento e gerenciamento desse arquivo, de modo que ele não fique muito grande.

Consulte os formatos de entrada de log no [artigo de registro](/help/implementing/developing/introduction/logging.md). As entradas de log também incluirão as propriedades adicionais mencionadas na variável [Formatos de entrada de log](#log-formats) abaixo.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

Considerações:

* Crie uma Chave de API sem nenhuma integração com um provedor de nuvem específico.


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
```

Considerações:

* Para credenciais, certifique-se de usar as credenciais de implantação, em vez das credenciais de conta. Estas são as credenciais geradas em uma tela que pode se parecer com esta imagem:

![Credenciais de implantação elástica](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### Logs HTTPS CDN {#https-cdn}

As solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com o formato de entrada de log descrito na [artigo de registro](/help/implementing/developing/introduction/logging.md#cdn-log). As propriedades adicionais são mencionadas na [Formatos de entrada de log](#log-formats) abaixo.

Também há uma propriedade chamada `sourcetype`, que é definido como o valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar a primeira entrada de log CDN, o servidor HTTP deve concluir com êxito um desafio único: uma solicitação enviada ao caminho ``wellknownpath`` deve responder com ``*``.


#### Logs AEM HTTPS {#https-aem}

Para logs do AEM (incluindo o Apache/Dispatcher), as solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com os vários formatos de entrada de log, conforme descrito na [artigo de registro](/help/implementing/developing/introduction/logging.md). As propriedades adicionais são mencionadas na [Formatos de entrada de log](#log-format) abaixo.

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

Consulte as [artigo de registro](/help/implementing/developing/introduction/logging.md) para o formato de cada tipo de log respectivo (logs CDN e logs AEM, incluindo Apache/Dispatcher).

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

Para o log CDN, é possível adicionar os endereços IP à lista de permissões, conforme descrito em [este artigo](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se essa lista de endereços IP compartilhados for muito grande, considere enviar tráfego para um Azure Blob Store (não Adobe) em que a lógica possa ser gravada para enviar os logouts de um IP dedicado para seu destino final.

Para logs AEM (incluindo Apache/Dispatcher), é possível configurar o encaminhamento de logs para passar [rede avançada](/help/security/configuring-advanced-networking.md). Veja os padrões dos três tipos avançados de rede abaixo, que usam uma `port` juntamente com o parâmetro `host` parâmetro.

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
