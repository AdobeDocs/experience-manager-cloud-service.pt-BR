---
title: Encaminhamento de logs para AEM as a Cloud Service
description: Saiba mais sobre como encaminhar logs para o Splunk e outros fornecedores de registro no AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Encaminhamento de logs {#log-forwarding}

>[!NOTE]
>
>Esse recurso ainda não foi lançado e alguns destinos de registro podem não estar disponíveis no momento do lançamento. Enquanto isso, você pode abrir um tíquete de suporte para encaminhar logs para **Splunk**, conforme descrito na seção [artigo de registro](/help/implementing/developing/introduction/logging.md).

Os clientes que têm uma licença para um fornecedor de registro ou hospedam um produto de registro podem ter registros de AEM, Apache/Dispatcher e CDN encaminhados para os destinos de registro associados. O AEM as a Cloud Service é compatível com os seguintes destinos de registro:

* Armazenamento Azure Blob
* DataDog
* Elasticsearch ou OpenSearch
* HTTPS
* Splunk

O encaminhamento de logs é configurado de maneira automatizada declarando uma configuração no Git e implantando-a por meio do Pipeline de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção em programas de produção (não sandbox).

Observe que a largura de banda da rede associada aos registros enviados ao destino de registro é considerada parte do uso de E/S da rede da organização.


## Como este artigo está organizado {#how-organized}

Este artigo está organizado da seguinte maneira:

* Configuração - comum para todos os destinos de registro
* Configurações de destino de registro - cada destino tem um formato um pouco diferente
* Rede avançada - envio de logs do AEM e do Apache/Dispatcher por meio de uma saída dedicada ou por meio de uma VPN


## Configurar {#setup}

1. Crie a seguinte estrutura de pasta e arquivo na pasta de nível superior em seu projeto no Git:

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml deve conter metadados e uma configuração semelhante ao seguinte formato (usamos o Splunk como exemplo).

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

   A variável **tipo** deve ser definido como LogForwarding a versão deve ser definida como a versão do schema, que é 1.

   Os tokens na configuração (como `${{SPLUNK_TOKEN}}`) representam segredos, que não devem ser armazenados no Git. Em vez disso, declare-os como Cloud Manager  [Variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md) do tipo **segredo**. Selecione **Todos** como o valor suspenso do campo Serviço aplicado, os logs podem ser encaminhados para os níveis de criação, publicação e visualização.

   É possível definir valores diferentes entre os logs cdn e todo o resto (logs AEM e apache), incluindo um **cdn** e/ou **aem** bloco após o **padrão** bloco, em que as propriedades podem substituir as definidas no **padrão** bloco; somente a propriedade enabled é necessária. Um possível caso de uso poderia ser o uso de um índice do Splunk diferente para logs CDN, como ilustra o exemplo abaixo.

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

   Outro cenário é desabilitar o encaminhamento dos logs CDN ou tudo o mais (logs AEM e Apache). Por exemplo, para encaminhar apenas os logs CDN, é possível configurar o seguinte:

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

* Serviços permitidos: o blob deve ser selecionado
* Recursos permitidos: o objeto deve ser selecionado
* Permissões permitidas: Gravar, Adicionar, Criar devem ser selecionadas
* Uma data/hora de início e expiração válidas.

Esta é uma captura de tela de um exemplo de configuração de token SAS:

![Configuração do token SAS do Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)


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

## Rede avançada {#advanced-networking}

Se você tiver requisitos organizacionais para bloquear o tráfego para o destino de registro, poderá configurar o encaminhamento de registros para passar pelo [rede avançada](/help/security/configuring-advanced-networking.md). Veja os padrões dos três tipos avançados de rede abaixo, que usam uma `port` juntamente com o parâmetro `host` parâmetro.

### Saída flexível da porta {#flex-port}

Se o tráfego de log for para uma porta diferente da 443 (por exemplo, 8443 abaixo), configure a rede avançada da seguinte maneira:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
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
      host: "proxy.tunnel"
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
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

Se o tráfego de log precisar passar por uma VPN, configure a rede avançada da seguinte maneira:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
