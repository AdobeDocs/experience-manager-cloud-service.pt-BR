---
title: Encaminhamento de logs para o AEM as a Cloud Service
description: Saiba mais sobre como encaminhar logs para fornecedores de registro no AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Developer
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 1%

---

# Encaminhamento de logs {#log-forwarding}

>[!NOTE]
>
>O encaminhamento de logs agora é configurado no modo de autoatendimento, diferente do método herdado, que exigiu o envio de um tíquete de Suporte da Adobe. Consulte a seção [Migrando](#legacy-migration) se o encaminhamento de logs tiver sido configurado pela Adobe.

Os clientes com uma licença de com um fornecedor de registro em log ou que hospedam um produto de registro em log podem ter registros do AEM (incluindo Apache/Dispatcher) e registros CDN encaminhados ao destino de registro associado. O AEM as a Cloud Service oferece suporte aos seguintes destinos de registro:

<table>
  <tbody>
    <tr>
      <th>Tecnologia de registro</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td>Sim</td>
      <td>Sim</td>
      <td style="background-color: #ffb3b3;">Futuro</td>
    </tr>
    <tr>
      <td>Armazenamento Azure Blob</td>
      <td>Sim</td>
      <td>Sim</td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>Sim</td>
      <td>Sim</td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td>Sim</td>
      <td>Sim</td>
      <td style="background-color: #ffb3b3;">Futuro</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>Sim</td>
      <td>Sim</td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>Sim</td>
      <td>Sim</td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td>Sim</td>
      <td>Sim</td>
      <td style="background-color: #ffb3b3;">Futuro</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>Sim</td>
      <td>Sim</td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>Lógica Sumo</td>
      <td>Sim</td>
      <td>Sim</td>
      <td style="background-color: #ffb3b3;">Futuro</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> Para as futuras Tecnologias de Log da CDN planejadas para o futuro, envie um email para [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para registrar o interesse.

O encaminhamento de logs é configurado de maneira automatizada declarando uma configuração no Git e pode ser implantado por meio de pipelines de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção. O arquivo de configuração pode ser implantado em RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido) usando ferramentas de linha de comando.

Há uma opção para que os registros do AEM e Apache/Dispatcher sejam roteados por meio da infraestrutura de rede avançada da AEM, como IP de saída dedicado.

Observe que a largura de banda da rede associada aos registros enviados ao destino de registro é considerada parte do uso de E/S da rede da organização.

## Como este artigo está organizado {#how-organized}

Este artigo está organizado da seguinte maneira:

* Configuração - comum para todos os destinos de registro
* Transporte e rede avançada - considere a configuração da rede antes de criar a configuração de registro
* Configurações de destino de registro - cada destino tem um formato um pouco diferente
* Formatos de Entrada de Log - informações sobre os formatos de entrada de log
* Migração do encaminhamento de log herdado - como migrar do encaminhamento de log previamente configurado pela Adobe para a abordagem de autoatendimento

## Configurar {#setup}

1. Crie um arquivo chamado `logForwarding.yaml`. Ele deve conter metadados, conforme descrito no artigo [Pipeline de Configuração](/help/operations/config-pipeline.md#common-syntax) (**kind** deve ser definido como `LogForwarding` e a versão definida como &quot;1&quot;), com uma configuração semelhante à seguinte (usamos o Splunk como exemplo).

   ```yaml
   kind: "LogForwarding"
   version: "1"
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada *config* ou similar, conforme descrito em [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure).

1. Para tipos de ambiente diferentes de RDE (que usa ferramentas de linha de comando), crie um pipeline de configuração de implantação direcionada no Cloud Manager, conforme referenciado por [esta seção](/help/operations/config-pipeline.md#creating-and-managing); observe que os pipelines de Empilhamento completo e de Camada da Web não implantam o arquivo de configuração.

1. Implante a configuração.

Os tokens na configuração (como `${{SPLUNK_TOKEN}}`) representam segredos que não devem ser armazenados no Git. Em vez disso, declare-as como [Variáveis de ambiente secreto](/help/operations/config-pipeline.md#secret-env-vars) do Cloud Manager. Selecione **Todos** como o valor suspenso do campo Serviço aplicado, para que os logs possam ser encaminhados para os níveis de criação, publicação e visualização.

É possível definir valores diferentes entre logs CDN e logs AEM (incluindo Apache/Dispatcher), incluindo um bloco **cdn** e/ou **aem** adicional após o bloco **padrão**, em que as propriedades podem substituir as definidas no bloco **padrão**; somente a propriedade habilitada é necessária. Um possível caso de uso poderia ser o uso de um índice do Splunk diferente para logs CDN, como ilustra o exemplo abaixo.

```yaml
   kind: "LogForwarding"
   version: "1"
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

```yaml
   kind: "LogForwarding"
   version: "1"
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

## Transporte e rede avançada {#transport-advancednetworking}

Algumas organizações escolhem restringir qual tráfego pode ser recebido pelos destinos de registro, outras podem exigir o uso de portas diferentes de HTTPS (443).  Nesse caso, a [Rede Avançada](/help/security/configuring-advanced-networking.md) precisará ser configurada antes da implantação da configuração de encaminhamento de log.

Use a tabela abaixo para ver quais são os requisitos para a configuração avançada de rede e registro com base no fato de você estar usando ou não a porta 443 e se você precisa ou não que seus registros apareçam a partir de um endereço IP fixo.

<table>
  <tbody>
    <tr>
      <th>Porta de destino</th>
      <th>Requisito para que os registros apareçam do IP fixo?</th>
      <th>Redes avançadas necessárias</th>
      <th>Definição de Porta LogForwarding.yaml Necessária</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS (443)</td>
      <td>Não</td>
      <td>Não</td>
      <td>Não</td>
    </tr>
    <tr>
      <td>Sim</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Saída Dedicada</a></td>
      <td>Não</td>
    <tr>
    <tr>
      <td rowspan="2">Porta não padrão (por exemplo, 8088)</td>
      <td>Não</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">Saída flexível</a></td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>Sim</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Saída Dedicada</a></td>
      <td>Sim</td>
  </tbody>
</table>

>[!NOTE]
>O fato de seus registros serem exibidos a partir de um único endereço IP é determinado pela sua escolha de configuração avançada de rede.  A saída dedicada deve ser usada para facilitar isso.
>
> A configuração avançada de rede é um [processo de duas etapas](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) que requer ativação no nível do programa e do ambiente.

Para logs AEM (incluindo Apache/Dispatcher), se você tiver configurado a [Rede Avançada](/help/security/configuring-advanced-networking.md), poderá usar a propriedade `aem.advancedNetworking` para encaminhá-los de um endereço IP de saída dedicado ou através de uma VPN.

O exemplo abaixo mostra como configurar o registro em uma porta HTTPS padrão com rede avançada.

```yaml
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

Para logs CDN, você pode adicionar os endereços IP à lista de permissões, conforme descrito em [Documentação do Fastly - Lista de IP Públicos](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se essa lista de endereços IP compartilhados for muito grande, considere enviar tráfego para um servidor https ou Azure Blob Store (que não seja da Adobe), em que a lógica possa ser gravada para enviar os logouts de um IP conhecido para seu destino final.

>[!NOTE]
>
>Não é possível que os logs CDN apareçam a partir do mesmo endereço IP que os logs do AEM aparecem. Isso ocorre porque os logs são enviados diretamente do Fastly e não pelo AEM Cloud Service.
>
>Por esse motivo, não é possível usar o encaminhamento de logs com configurações VPN avançadas de rede.

## Configuração de destino de registro {#logging-destinations}

As configurações para os destinos de registro compatíveis estão listadas abaixo, juntamente com considerações específicas.

### Amazon S3 {#amazons3}

O encaminhamento de logs para o Amazon S3 é compatível com logs do AEM e do Dispatcher. Os logs CDN ainda não são compatíveis.

>[!NOTE]
>
>Registros gravados em S3 periodicamente, a cada 10 minutos para cada tipo de arquivo de registro.  Isso pode resultar em um atraso inicial para que os logs sejam gravados em S3 quando o recurso for alternado.  [Mais informações sobre este comportamento](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs).

```yaml
kind: "LogForwarding"
version: "1"
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

Para usar o S3 Log Forwarder, será necessário pré-configurar um usuário do AWS IAM com política apropriada para acessar seu bucket do S3.  Consulte [Documentação de Usuário do AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) para saber como criar credenciais de usuário do IAM.

A política IAM deve permitir que o usuário use `s3:putObject`.  Por exemplo:

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

Consulte a [Documentação da política de bucket do AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html) para obter mais informações sobre como implementar o.

>[!NOTE]
>O suporte ao Log de CDN para o AWS S3 está planejado para o futuro. Envie um email para [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para registrar interesse.

### Armazenamento Azure Blob {#azureblob}

```yaml
kind: "LogForwarding"
version: "1"
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

Se os registros pararem de ser entregues depois de antes funcionarem corretamente, verifique se o token SAS configurado ainda é válido, pois pode ter expirado.

#### Logs CDN do Armazenamento de Blobs do Azure {#azureblob-cdn}

Cada um dos servidores de log distribuídos globalmente produzirá um novo arquivo a cada poucos segundos, na pasta `aemcdn`. Depois de criado, o arquivo não será mais anexado ao. O formato do nome do arquivo é AAAA-MM-DDThh:mm:ss.sss-uniqueid.log. Por exemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Como exemplo, em algum momento:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

E 30 segundos depois:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Cada arquivo contém várias entradas de log json, cada uma em uma linha separada. Os formatos de entrada de log estão descritos em [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md), e cada entrada de log também inclui as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

#### Logs do AEM do Armazenamento de Azure Blob {#azureblob-aem}

Os logs do AEM (incluindo o Apache/Dispatcher) aparecem abaixo de uma pasta com a seguinte convenção de nomenclatura:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

Em cada pasta, um único arquivo será criado e anexado a. Os clientes são responsáveis pelo processamento e gerenciamento desse arquivo, de modo que ele não fique muito grande.

Consulte os formatos de entrada de log em [Log para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). As entradas de log também incluirão as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

### Datadog {#datadog}

```yaml
kind: "LogForwarding"
version: "1"
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

#### Considerações

* Crie uma Chave de API sem nenhuma integração com um provedor de nuvem específico.
* A propriedade das tags é opcional
* Para logs AEM, a marca de origem do Datadog está definida como uma das seguintes opções: `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` ou `aemhttpderror`
* Para logs CDN, a marca de origem do Datadog está definida como `aemcdn`
* A etiqueta de serviço do Datadog está definida como `adobeaemcloud`, mas você pode substituí-la na seção de etiquetas
* Se o pipeline de assimilação usar tags Datadog para determinar o índice apropriado para logs de encaminhamento, verifique se essas tags estão configuradas corretamente no arquivo YAML de encaminhamento de logs. As tags ausentes podem impedir a assimilação de logs bem-sucedida se o pipeline depender delas.

### Elasticsearch e OpenSearch {#elastic}

```yaml
kind: "LogForwarding"
version: "1"
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

#### Considerações

* por padrão, a porta é 443. Opcionalmente, ele pode ser substituído por uma propriedade chamada `port`
* Para credenciais, certifique-se de usar as credenciais de implantação, em vez das credenciais de conta. Estas são as credenciais geradas em uma tela que pode se parecer com esta imagem:

![Credenciais de implantação elástica](/help/implementing/developing/introduction/assets/ec-creds.png)

* Para logs AEM, `index` está definido como um de `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` ou `aemhttpderror`
* A propriedade opcional do pipeline deve ser definida como o nome do pipeline de assimilação do Elasticsearch ou OpenSearch, que pode ser configurado para rotear a entrada de log para o índice apropriado. O tipo de Processador do pipeline deve ser definido como *script* e a linguagem de script deve ser definida como *indolor*. Este é um exemplo de trecho de script para rotear entradas de log em um índice, como aemaccess_dev_26_06_2024:

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
kind: "LogForwarding"
version: "1"
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### Considerações

* A cadeia de caracteres da URL deve incluir **https://** ou a validação falhará.
* O URL pode incluir uma porta. Por exemplo, `https://example.com:8443/aem_logs/aem`. Se nenhuma porta for incluída na string do URL, a porta 443 (a porta HTTPS padrão) será considerada.

#### Logs HTTPS CDN {#https-cdn}

As solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com o formato de entrada de log descrito em [Logon para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

Também existe uma propriedade chamada `sourcetype`, que é definida como o valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar a primeira entrada de log CDN, o servidor HTTP deve concluir com êxito um desafio único: uma solicitação enviada para o caminho ``/.well-known/fastly/logging/challenge`` deve responder com um asterisco ``*`` no corpo e código de status 200.

#### Logs HTTPS do AEM {#https-aem}

Para logs do AEM (incluindo apache/dispatcher), as solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com os vários formatos de entrada de log, conforme descrito em [Logs para o AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

Também há uma propriedade chamada `Source-Type`, que é definida como um destes valores:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### API de log do New Relic {#newrelic-https}

O encaminhamento de logs para o New Relic aproveita a API HTTPS do New Relic para assimilação.  Atualmente, ele só é compatível com logs do AEM e do Dispatcher; os logs CDN ainda não são compatíveis.

```yaml
  kind: "LogForwarding"
  version: "1"
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>O encaminhamento de logs para a New Relic só está disponível para contas da New Relic de propriedade do cliente.
>
>O suporte ao Log de CDN para a API de Log do New Relic está planejado para o futuro. Envie um email para [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para registrar interesse.
>
>O New Relic fornece endpoints específicos da região com base no local em que sua conta do New Relic é provisionada.  Consulte a [documentação do New Relic](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint) para obter mais informações.

### API de log do Dynatrace {#dynatrace-https}

O encaminhamento de logs para o Dynatrace aproveita a API HTTPS do Dynatrace para assimilação.  Atualmente, ele só é compatível com logs do AEM e do Dispatcher; os logs CDN ainda não são compatíveis.

O atributo de escopo &quot;Logs de assimilação&quot; é necessário para o token.

```yaml
  kind: "LogForwarding"
  version: "1"
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>O suporte ao Log de CDN para a API de Log do Dynatrace está planejado para o futuro. Envie um email para [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para registrar interesse.

### Splunk {#splunk}

```yaml
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
```

#### Considerações

* A porta padrão é 443. Opcionalmente, ele pode ser substituído por uma propriedade chamada `port`.
* Dependendo do log específico, o campo sourcetype terá um dos seguintes valores: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Incluir na lista de permissões Se os IPs necessários tiverem sido migrados e os registros ainda não estiverem sendo entregues, verifique se não há regras de firewall impondo a validação do token de Splunk. O Fastly executa uma etapa de validação inicial na qual um token do Splunk inválido é enviado intencionalmente. Se o firewall estiver definido para encerrar conexões com tokens inválidos do Splunk, o processo de validação falhará, impedindo que o Fastly entregue logs para a instância do Splunk.

>[!NOTE]
>
> [Ao migrar](#legacy-migration) do encaminhamento de logs herdado para este modelo de autoatendimento, os valores do campo `sourcetype` enviados para o índice do Splunk podem ter sido alterados, portanto, ajuste-os adequadamente.

### Lógica Sumo {#sumologic}

O encaminhamento de logs para o Sumo Logic é compatível com logs do AEM e do Dispatcher; os logs CDN ainda não são compatíveis.

Ao configurar a Lógica de sumô para assimilação de dados, você verá um &quot;Endereço Source HTTP&quot; que fornece o host, o URI do receptor e a chave privada em uma única string.  Por exemplo:

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

Você precisará copiar a última seção da URL (sem a `/` anterior) e adicioná-la como uma [Variável de ambiente secreto do CloudManager](/help/operations/config-pipeline.md#secret-env-vars), conforme descrito na seção [Configuração](#setup) acima, e depois referenciar essa variável na sua configuração.  Um exemplo é fornecido abaixo.

```yaml
kind: "LogForwarding"
version: "1"
data:
  sumoLogic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
>O suporte ao Log de CDN para SumoLogic está planejado para o futuro. Envie um email para [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para registrar interesse.
>
> Você precisará de uma assinatura Sumo Logic Enterprise para aproveitar a funcionalidade do campo &quot;índice&quot;.  As assinaturas não empresariais terão seus logs roteados para a partição `sumologic_default` como padrão.  Consulte a [Documentação de Particionamento Lógico de Resumo](https://help.sumologic.com/docs/search/optimize-search-partitions/) para obter mais informações.

## Formatos de entrada de log {#log-formats}

Consulte [Logs do AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) para obter o formato de cada respectivo tipo de log (logs CDN e logs do AEM, incluindo o Apache/Dispatcher).

Como os registros de vários programas e ambientes podem ser encaminhados para o mesmo destino de registro, além da saída descrita no artigo de registro, as seguintes propriedades serão incluídas em cada entrada de registro:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Como exemplo, as propriedades podem ter os seguintes valores:

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Migrando do Encaminhamento de Log Herdado {#legacy-migration}

Antes de a configuração do encaminhamento de logs ser obtida por meio de um modelo de autoatendimento, os clientes eram solicitados a abrir tíquetes de suporte, onde a Adobe iniciaria a integração.

Os clientes que foram configurados dessa maneira pela Adobe são bem-vindos para se adaptarem ao modelo de autoatendimento de sua conveniência. Há vários motivos para fazer essa transição:

* Um novo ambiente (por exemplo, um novo ambiente de desenvolvimento ou RDE) foi provisionado.
* Alterações nas credenciais ou no ponto de extremidade existente do Splunk.
* A Adobe configurou o encaminhamento de logs antes que os logs CDN estivessem disponíveis e você gostaria de receber logs CDN.
* Uma decisão consciente de se adaptar proativamente ao modelo de autoatendimento para que sua organização tenha o conhecimento mesmo antes de uma alteração sensível ao tempo ser necessária.

Quando estiver pronto para migrar, basta configurar o arquivo YAML conforme descrito nas seções anteriores. Use o pipeline de configuração do Cloud Manager para implantar em cada um dos ambientes em que a configuração deve ser aplicada.

Recomenda-se, mas não é necessário, que uma configuração seja implantada em todos os ambientes para que todos estejam sob controle de autoatendimento. Caso contrário, você pode esquecer quais ambientes foram configurados pelo Adobe e quais foram configurados de maneira automatizada.

>[!NOTE]
>
>Os valores do campo `sourcetype` enviados para o índice do Splunk podem ter sido alterados, portanto, ajuste de acordo.
>
>Quando o encaminhamento de logs é implantado em um ambiente previamente configurado pelo suporte da Adobe, você pode receber logs duplicados por até algumas horas. Isso acabará sendo resolvido automaticamente.
