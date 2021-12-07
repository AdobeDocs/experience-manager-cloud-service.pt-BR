---
title: Configuração de redes avançadas para AEM as a Cloud Service
description: Saiba como configurar recursos avançados de rede, como VPN ou um endereço IP de saída flexível ou dedicado para AEM as a Cloud Service
source-git-commit: fa11beb1dfdd8dd2a1a5d49ece059f5894c835be
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 1%

---


# Configuração de redes avançadas para AEM as a Cloud Service {#configuring-advanced-networking}

Este artigo tem como objetivo apresentar a você os diferentes recursos avançados de rede em AEM as a Cloud Service, incluindo o provisionamento de autoatendimento de VPN, portas não padrão e endereços IP de saída dedicados.

## Visão geral {#overview}

AEM as a Cloud Service oferece vários tipos de recursos avançados de rede, que podem ser configurados por clientes usando APIs do Cloud Manager. Dentre elas:

* [Saída flexível da porta](#flexible-port-egress) - configure AEM as a Cloud Service para permitir o tráfego de saída de portas não padrão
* [Endereço IP de saída dedicado](#dedicated-egress-IP-address) - configure o tráfego de AEM as a Cloud Service para se originar de um IP exclusivo
* [VPN (Virtual Private Network)](#vpn) - tráfego seguro entre a infraestrutura de um cliente e o AEM as a Cloud Service, para clientes com tecnologia VPN

Este artigo descreve cada uma dessas opções em detalhes, incluindo como elas podem ser configuradas. Como estratégia de configuração geral, a variável `/networkInfrastructures` O endpoint da API é chamado no nível do programa para declarar o tipo desejado de rede avançada, seguido de uma chamada para a `/advancedNetworking` endpoint para cada ambiente para habilitar a infraestrutura e configurar parâmetros específicos do ambiente. Consulte os endpoints apropriados na documentação da API do Cloud Manager para cada sintaxe formal, bem como exemplos de solicitações e respostas.

Um programa pode proporcionar uma única variação avançada em rede. Ao decidir entre saída de porta flexível e endereço IP de saída dedicado, é recomendável escolher saída de porta flexível se um endereço IP específico não for necessário, pois o Adobe pode otimizar o desempenho do tráfego de saída de porta flexível.

>[!INFO]
>
>A rede avançada não está disponível para o programa sandbox.
>Além disso, os ambientes devem ser atualizados para AEM versão 5958 ou superior.

>[!NOTE]
>
>Os clientes já provisionados com a tecnologia de saída dedicada herdada que precisam configurar uma dessas opções não devem fazê-lo ou a conectividade do site pode ser afetada. Entre em contato com o Suporte do Adobe para obter assistência.

## Aumento Flexível da Porta {#flexible-port-egress}

Esse recurso avançado de rede permite configurar AEM as a Cloud Service para obter tráfego por meio de portas diferentes de HTTP (porta 80) e HTTPS (porta 443), que são abertas por padrão.

### Considerações {#flexible-port-egress-considerations}

Saída de porta flexível é a opção recomendada se você não precisar de VPN e não precisar de um endereço IP de saída dedicado, pois o tráfego que não depende de um egresso dedicado pode alcançar throughput mais alto.

### Configuração {#configuring-flexible-port-egress-provision}

Uma vez por programa, o POST `/program/<programId>/networkInfrastructures` endpoint é chamado, basta passar o valor de `flexiblePortEgress` para `kind` parâmetro e região. O endpoint responde com a variável `network_id`, bem como outras informações, incluindo o status . O conjunto completo de parâmetros e a sintaxe exata devem ser referenciados nos documentos da API.

Uma vez chamada, normalmente leva aproximadamente 15 minutos para a infraestrutura de rede ser provisionada. Uma chamada para o [ponto de extremidade do GET de infraestrutura de rede](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) mostraria um status de &quot;pronto&quot;.

Se a configuração de saída de porta flexível com escopo de programa estiver pronta, a variável `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` o endpoint deve ser chamado por ambiente para permitir a operação em rede no nível do ambiente e declarar, opcionalmente, quaisquer regras de encaminhamento de portas. Os parâmetros são configuráveis por ambiente para oferecer flexibilidade.

As regras de encaminhamento de portas devem ser declaradas para qualquer porta diferente de 80/443, especificando o conjunto de hosts de destino (nomes ou IP e com portas). Para cada host de destino, os clientes devem mapear a porta de destino pretendida para uma porta de 30000 a 30999.

A API deve responder em apenas alguns segundos, indicando um status de atualização e, após cerca de 10 minutos, o parâmetro de extremidade `GET` deve indicar que a rede avançada está ativada.

### Atualizações {#updating-flexible-port-egress-provision}

A configuração de nível de programa pode ser atualizada chamando a função `PUT /api/program/<program_id>/network/<network_id>` e entrará em vigor em alguns minutos.

>[!NOTE]
>
> O parâmetro &quot;type&quot; (`flexiblePortEgress`, `dedicatedEgressIP` ou `VPN`) não pode ser modificada. Entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.

As regras de encaminhamento de porta por ambiente podem ser atualizadas chamando novamente o `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` endpoint , certificando-se de incluir o conjunto completo de parâmetros de configuração, em vez de um subconjunto.

### Excluindo ou Desativando saída flexível de porta {#deleting-disabling-flexible-port-egress-provision}

Para **excluir** a infraestrutura de rede, envie um tíquete de suporte ao cliente, descrevendo o que foi criado e por que ele precisa ser excluído.

Para **disable** saída de porta flexível de um ambiente específico, invocar `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Para obter mais informações, consulte o [Documentação da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Roteamento de tráfego {#flexible-port-egress-traffic-routing}

O tráfego Http ou https que vai para destinos por meio das portas 80 ou 443 passará por um proxy pré-configurado, supondo que a biblioteca de rede Java padrão seja usada. Para tráfego http ou https que atravessa outras portas, um proxy deve ser configurado usando as seguintes propriedades.

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

Por exemplo, este é um exemplo de código para enviar uma solicitação para o `www.example.com:8443`:

```java
String url = "www.example.com:8443"
var proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
var proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Se estiver usando bibliotecas de rede Java não padrão, configure proxies usando as propriedades acima para todo o tráfego.

Tráfego não http/s com destinos por meio de portas declaradas no `portForwards` deve fazer referência a uma propriedade chamada `AEM_PROXY_HOST`, juntamente com a porta mapeada. Por exemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

A tabela abaixo descreve o roteamento de tráfego:

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de determinação</th>
    <th>Port</th>
    <th>Conexão</th>
    <th>Exemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http ou https</b></td>
    <td>Tráfego http/s padrão</td>
    <td>80 ou 443</td>
    <td>Permitido</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Tráfego não padrão (em outras portas fora de 80 ou 443) por proxy http configurado usando estas variáveis de ambiente:<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>Portas fora de 80 ou 443</td>
    <td>Permitido</td>
  </tr>
  <tr>
    <td></td>
    <td>Tráfego não padrão (em outras portas fora das portas 80 ou 443) não usando proxy http</td>
    <td>Portas fora de 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não-https</b></td>
    <td>O cliente se conecta ao <code>AEM_PROXY_HOST</code> variável de ambiente usando um <code>portOrig</code> declarado no <code>portForwards</code> parâmetro da API.</td>
    <td>Qualquer</td>
    <td>Permitido</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Tudo o resto</td>
    <td>Qualquer</td>
    <td>Bloqueado</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Configuração do Apache / Dispatcher**

A camada do AEM Cloud Service Apache/Dispatcher `mod_proxy` pode ser configurada usando as propriedades descritas acima.

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Endereço IP de saída dedicado {#dedicated-egress-IP-address}

>[!NOTE]
>
>Se você tiver sido provisionado com um IP de saída dedicado antes da versão de setembro de 2021 (06/10/21), consulte o [Clientes de endereço dedicado herdado](#legacy-dedicated-egress-address-customers).

### Benefícios {#benefits}

Esse endereço IP dedicado pode melhorar a segurança ao integrar fornecedores SaaS (como um fornecedor de CRM) ou outras integrações fora AEM as a Cloud Service que oferecem uma lista de permissões de endereços IP. Ao adicionar o endereço IP dedicado à  de lista de permissões, isso garante que somente o tráfego da AEM Cloud Service do cliente possa fluir para o serviço externo. Além do tráfego de qualquer outro IP permitido.

Sem o recurso de endereço IP dedicado habilitado, o tráfego proveniente AEM fluxos as a Cloud Service por meio de um conjunto de IPs compartilhados com outros clientes.

### Configuração {#configuring-dedicated-egress-provision}

>[!INFO]
>
>O recurso de encaminhamento do Splunk não é possível em um endereço IP de saída dedicado.

A configuração do endereço IP de saída dedicado é idêntica a [saída de porta flexível](#configuring-flexible-port-egress-provision).

A principal diferença é que o tráfego sempre sairá de um IP dedicado e único. Para localizar esse IP, use um resolvedor de DNS para identificar o endereço IP associado a `p{PROGRAM_ID}.external.adobeaemcloud.com`. Não é esperado que o endereço IP mude, mas se precisar mudar no futuro, será fornecida uma notificação avançada.

Além das regras de roteamento compatíveis com egressos flexíveis da porta no `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` endpoint, endereço IP de saída dedicado suporta um `nonProxyHosts` parâmetro. Isso permite declarar um conjunto de hosts que devem rotear por um intervalo de endereços IPs compartilhados em vez do IP dedicado, o que pode ser útil, pois a criação de tráfego por meio de IPs compartilhados pode ser otimizada ainda mais. O `nonProxyHost` Os URLs podem seguir os padrões de `example.com` ou `*.example.com`, em que o curinga é compatível somente no início do domínio.

Ao decidir entre saída de porta flexível e endereço IP de saída dedicado, os clientes devem escolher saída de porta flexível se um endereço IP específico não for necessário, pois o Adobe pode otimizar o desempenho do tráfego de saída de porta flexível.

### Roteamento de tráfego {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de destino</th>
    <th>Port</th>
    <th>Conexão</th>
    <th>Exemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http ou https</b></td>
    <td>Tráfego para serviços do Azure ou da Adobe</td>
    <td>Qualquer</td>
    <td>Por meio dos IPs de cluster compartilhados (não o IP dedicado)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente à <code>nonProxyHosts</code> parâmetro</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente à <code>nonProxyHosts</code> parâmetro</td>
    <td>Portas fora de 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Por meio da configuração de proxy http, configurada por padrão para tráfego http/s usando a biblioteca do cliente HTTP Java padrão</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca do cliente HTTP Java padrão ou se uma biblioteca Java que ignora a configuração do proxy padrão for usada)</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca do cliente HTTP Java padrão ou se uma biblioteca Java que ignora a configuração do proxy padrão for usada)</td>
    <td>Portas fora de 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não-https</b></td>
    <td>O cliente se conecta a <code>AEM_PROXY_HOST</code> variável env usando uma <code>portOrig</code> declarado no <code>portForwards</code> Parâmetro de API</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Qualquer outra coisa</td>
    <td></td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
</tbody>
</table>

## Clientes de endereço dedicado herdado {#legacy-dedicated-egress-address-customers}

Se você tiver sido provisionado com um IP de saída dedicado antes de 2021.09.30, seu recurso IP de saída dedicado funcionará conforme descrito abaixo.

### Uso de recursos {#feature-usage}

O recurso é compatível com código Java ou bibliotecas que resultam em tráfego de saída, desde que usem propriedades padrão do sistema Java para configurações de proxy. Na prática, isso deve incluir as bibliotecas mais comuns.

Abaixo está uma amostra de código:

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Algumas bibliotecas exigem configuração explícita para usar as propriedades padrão do sistema Java para configurações de proxy.

Um exemplo usando o Apache HttpClient, que requer chamadas explícitas para
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) ou usar
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

O mesmo IP dedicado é aplicado a todos os programas de um cliente em sua Organização do Adobe e para todos os ambientes em cada um de seus programas. Isso se aplica aos serviços de autor e publicação.

Somente as portas HTTP e HTTPS são compatíveis. Isso inclui HTTP/1.1 e HTTP/2 quando criptografado.

### Considerações sobre depuração {#debugging-considerations}

Para validar se o tráfego está de saída no endereço IP dedicado esperado, verifique os logs no serviço de destino, se disponível. Caso contrário, pode ser útil chamar um serviço de depuração como [https://ifconfig.me/IP](https://ifconfig.me/IP), que retornará o endereço IP de chamada.

## VPN (Virtual Private Network) {#vpn}

A VPN permite a conexão com uma infraestrutura local ou data center de criação, publicação ou pré-visualização. Por exemplo, para os meios de acessar um banco de dados.

Também permite a Conexão com fornecedores SaaS, como um fornecedor de CRM que oferece suporte a VPN ou a conexão de uma rede corporativa a AEM autor, pré-visualização ou publicação as a Cloud Service.

A maioria dos dispositivos VPN com tecnologia IPSec é compatível. Consulte a lista de dispositivos em [esta página](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), com base nas informações da **Instruções de configuração com base na rota** coluna. Configure o dispositivo conforme descrito na tabela.

### Considerações gerais {#general-vpn-considerations}

* Suporte limitado a uma única conexão VPN
* O recurso de encaminhamento do Splunk não é possível em uma conexão VPN.

### Criação {#vpn-creation}

Uma vez por programa, o POST `/program/<programId>/networkInfrastructures` o endpoint é chamado, transmitindo uma carga de informações de configuração incluindo: o valor de &quot;vpn&quot; para a variável `kind` parâmetro, região, espaço de endereço (lista de CIDRs - observe que isso não pode ser modificado posteriormente), resolvedores de DNS (para resolver nomes na rede do cliente) e informações de conexão VPN, como configuração de gateway, chave VPN compartilhada e política de segurança de IP. O endpoint responde com a variável `network_id`, bem como outras informações, incluindo o status . O conjunto completo de parâmetros e a sintaxe exata devem ser referenciados na variável [Documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Uma vez coletada, a infraestrutura de rede normalmente levará de 45 a 60 minutos para ser provisionada. O método GET da API pode ser chamado para retornar o status atual, que eventualmente se virará de `creating` para `ready`. Consulte a documentação da API para todos os estados.

Se a configuração de VPN com escopo de programa estiver pronta, a variável `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` o endpoint deve ser chamado por ambiente para habilitar a rede no nível do ambiente e declarar quaisquer regras de encaminhamento de porta. Os parâmetros são configuráveis por ambiente para oferecer flexibilidade.

Consulte a [Documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) para obter mais informações.

As regras de encaminhamento de portas devem ser declaradas para qualquer tráfego TCP de protocolo não http/s que deve ser roteado através da VPN especificando o conjunto de hosts de destino (nomes ou IP e com portas). Para cada host de destino, os clientes devem mapear a porta de destino pretendida para uma porta de 30000 a 30999, onde os valores devem ser exclusivos entre os ambientes do programa. Os clientes também podem listar um conjunto de url no `nonProxyHosts` , que declara o URL para o qual o tráfego deve ignorar o roteamento VPN, mas por meio de um intervalo IP compartilhado. Ele segue os padrões de `example.com` ou `*.example.com`, em que o curinga é compatível somente no início do domínio.

A API deve responder em apenas alguns segundos, indicando um status de `updating` e após cerca de 10 minutos, uma chamada para o endpoint de GET do ambiente do Cloud Manager mostraria um status de `ready`, indicando que a atualização do ambiente foi aplicada.

Observe que mesmo se não houver regras de roteamento de tráfego de ambiente (hosts ou ignoradas), `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` ainda deve ser chamado, apenas com uma carga vazia.

### Atualização da VPN {#updating-the-vpn}

A configuração de VPN no nível do programa pode ser atualizada chamando o `PUT /api/program/<program_id>/network/<network_id>` endpoint .

Observe que o espaço de endereço não pode ser alterado após o provisionamento de VPN inicial. Se isso for necessário, entre em contato com o suporte ao cliente. Além disso, a variável `kind` parâmetro (`flexiblePortEgress`, `dedicatedEgressIP` ou `VPN`) não pode ser modificada. Entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.

As regras de roteamento por ambiente podem ser atualizadas chamando novamente a função `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` endpoint , certificando-se de incluir o conjunto completo de parâmetros de configuração, em vez de um subconjunto. As atualizações de ambiente normalmente levam de 5 a 10 minutos para serem aplicadas.

### Excluindo ou desabilitando a VPN {#deleting-or-disabling-the-vpn}

Para excluir a infraestrutura de rede, envie um tíquete de suporte ao cliente, descrevendo o que foi criado e por que ele precisa ser excluído.

Para desativar a VPN para um ambiente específico, chame `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Mais detalhes na [Documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Roteamento de tráfego {#vpn-traffic-routing}

A tabela abaixo descreve o roteamento de tráfego.

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de destino</th>
    <th>Port</th>
    <th>Conexão</th>
    <th>Exemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http ou https</b></td>
    <td>Tráfego para serviços do Azure ou da Adobe</td>
    <td>Qualquer</td>
    <td>Por meio dos IPs de cluster compartilhados (não o IP dedicado)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente à <code>nonProxyHosts</code> parâmetro</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente à <code>nonProxyHosts</code> parâmetro</td>
    <td>Portas fora de 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP cair na variável <i>Endereço do gateway VPN</i> intervalo de espaço e por meio da configuração de proxy http (configurada por padrão para tráfego http/s usando a biblioteca do cliente HTTP Java padrão)</td>
    <td>Qualquer</td>
    <td>Através da VPN</td>
    <td><code>10.0.0.1:443</code>Também pode ser um nome de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP não cair na <i>Espaço de endereço do gateway VPN</i> e por meio da configuração de proxy http (configurada por padrão para tráfego http/s usando a biblioteca padrão do cliente HTTP Java)</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca do cliente HTTP Java padrão ou se estiver usando a biblioteca Java que ignora a configuração do proxy padrão)
</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca do cliente HTTP Java padrão ou se estiver usando a biblioteca Java que ignora a configuração do proxy padrão)</td>
    <td>Portas fora de 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não-https</b></td>
    <td>Se o IP cair na variável <i>Espaço de endereço do gateway VPN</i> e o cliente se conecta a <code>AEM_PROXY_HOST</code> variável env usando uma <code>portOrig</code> declarado no <code>portForwards</code> Parâmetro de API</td>
    <td>Qualquer</td>
    <td>Através da VPN</td>
    <td><code>10.0.0.1:3306</code>Também pode ser um nome de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP não cair na <i>Espaço de endereço do gateway VPN</i> o intervalo e o cliente se conecta a <code>AEM_PROXY_HOST</code> variável env usando uma <code>portOrig</code> declarado no <code>portForwards</code> Parâmetro de API</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Qualquer outra coisa</td>
    <td>Qualquer</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
</tbody>
</table>

### Domínios úteis para configuração{#vpn-useful-domains-for-configuration}

O diagrama abaixo fornece uma representação visual de um conjunto de domínios e IPs associados que são úteis para configuração e desenvolvimento. A tabela abaixo descreve esses domínios e IPs.

![Configuração de domínio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Padrão de domínio</th>
    <th>Incêndio (de AEM)</th>
    <th>Assimilação (para AEM)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Endereço IP de saída dedicado para o tráfego que vai para a Internet e não através de redes privadas </td>
    <td>As conexões da VPN mostrariam na CDN como provenientes deste IP. Para permitir somente conexões da VPN para entrar no AEM, configure o Cloud Manager para permitir somente esse IP e bloquear todo o resto. Consulte a seção "Restrict ingress to VPN connections" para obter mais detalhes.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/A</td>
    <td>O IP do gateway VPN no lado do AEM. Uma equipe de engenharia de rede de um cliente pode usar isso para permitir somente conexões VPN com o gateway VPN de um endereço IP específico. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>O IP do tráfego vindo do lado AEM da VPN para o lado do cliente. Isso pode ser incluir na lista de permissões na configuração do cliente para garantir que as conexões só possam ser feitas de AEM.</td>
    <td>Se o cliente quiser permitir somente o acesso VPN ao AEM, ele deverá configurar as entradas de DNS CNAME para mapear <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>  e/ou <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> a isto.</td>
  </tr>
</tbody>
</table>

### Restringir VPN a Conexões de Entrada {#restrict-vpn-to-ingress-connections}

Se você quiser permitir somente o acesso VPN ao AEM, as lista de permissões do ambiente poderão ser configuradas no Cloud Manager para que somente o IP definido por `p{PROGRAM_ID}.external.adobeaemcloud.com` é permitido falar com o meio ambiente. Isso pode ser feito da mesma forma que qualquer outra  de lista de permissões baseada em IP no Cloud Manager.

Se as regras tiverem de ser baseadas em caminho, use as diretivas http padrão no nível do dispatcher para negar ou permitir determinados IPs. Eles devem garantir que os caminhos desejados também não possam ser armazenados em cache na CDN, para que a solicitação sempre chegue à origem.

**Exemplo De Configuração Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Transição Entre Tipos Avançados De Rede {#transitioning-between-advanced-networking-types}

Como a variável `kind` não pode ser modificado, entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.
