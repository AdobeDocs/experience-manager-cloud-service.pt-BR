---
title: Configuração de redes avançadas para o AEM as a Cloud Service
description: Saiba como configurar recursos avançados de rede, como VPN ou um endereço IP de saída flexível ou dedicado para o AEM as a Cloud Service
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: 7d74772bf716e4a818633a18fa17412db5a47199
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configuração de redes avançadas para o AEM as a Cloud Service {#configuring-advanced-networking}

Este artigo tem como objetivo apresentar a você os diferentes recursos avançados de rede no AEM as a Cloud Service, incluindo o provisionamento de autoatendimento de VPN, portas não padrão e endereços IP de saída dedicados.

>[!INFO]
>
>Você também pode encontrar uma série de artigos projetados para orientá-lo em cada uma das opções avançadas de rede neste [local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=pt-BR).

## Visão geral {#overview}

O AEM as a Cloud Service oferece vários tipos de recursos avançados de rede que podem ser configurados por clientes usando as APIs do Cloud Manager. Dentre elas:

* [Saída flexível da porta](#flexible-port-egress) - configure o AEM as a Cloud Service para permitir tráfego de saída em portas não padrão
* [Endereço IP de saída dedicado](#dedicated-egress-IP-address) - configure o tráfego do AEM as a Cloud Service para se originar de um IP exclusivo
* [VPN (Virtual Private Network)](#vpn) - tráfego seguro entre a infraestrutura de um cliente e o AEM as a Cloud Service, para clientes com tecnologia VPN

Este artigo descreve cada uma dessas opções em detalhes, incluindo como elas podem ser configuradas. Como estratégia de configuração geral, o endpoint da API `/networkInfrastructures` é chamado no nível do programa para declarar o tipo desejado de rede avançada, seguido de uma chamada para o endpoint `/advancedNetworking` para cada ambiente para habilitar a infraestrutura e configurar parâmetros específicos do ambiente. Consulte os endpoints apropriados na documentação da API do Cloud Manager para cada sintaxe formal, bem como exemplos de solicitações e respostas.

Um programa pode provisionar uma única variação avançada em rede. Ao decidir entre a saída de porta flexível e o endereço IP de saída dedicado, é recomendável escolher a saída de porta flexível se um endereço IP específico não for necessário, pois a Adobe pode otimizar o desempenho do tráfego de saída da porta flexível.

>[!INFO]
>
>A rede avançada não está disponível para o programa sandbox.
>Além disso, os ambientes devem ser atualizados para o AEM versão 5958 ou superior.

>[!NOTE]
>
>Os clientes já provisionados com a tecnologia de saída dedicada herdada que precisam configurar uma dessas opções não devem fazê-lo, pois a conectividade do site pode ser afetada. Entre em contato com o Suporte da Adobe para obter assistência.

## Saída flexível da porta {#flexible-port-egress}

Esse recurso avançado de rede permite configurar o AEM as a Cloud Service para direcionar o tráfego de saída por portas diferentes da HTTP (porta 80) e HTTPS (porta 443), que são abertas por padrão.

### Considerações {#flexible-port-egress-considerations}

Saída de porta flexível é a opção recomendada se você não precisar de VPN e não precisar de um endereço IP de saída dedicado, pois o tráfego que não depende de um egresso dedicado pode alcançar um rendimento mais alto.

### Configuração {#configuring-flexible-port-egress-provision}

Uma vez por programa, o endpoint `/program/<programId>/networkInfrastructures` POST é chamado, passando o valor de `flexiblePortEgress` para o parâmetro e região `kind`. O endpoint responde com a `network_id`, bem como com outras informações, incluindo o status. O conjunto completo de parâmetros e a sintaxe exata, bem como informações importantes, como quais parâmetros não poderão ser alterados posteriormente, [podem ser referenciados nos documentos da API.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

Uma vez chamada, normalmente leva aproximadamente 15 minutos para a infraestrutura de rede ser provisionada. Uma chamada para o [endpoint da infraestrutura de rede GET](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) do Cloud Manager mostraria o status de &quot;pronto&quot;.

Se a configuração de saída de porta flexível com escopo de programa estiver pronta, o endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve ser chamado por ambiente para permitir a operação em rede no nível do ambiente e declarar, opcionalmente, quaisquer regras de encaminhamento de portas. Os parâmetros são configuráveis por ambiente para oferecer flexibilidade.

As regras de encaminhamento de porta devem ser declaradas para qualquer porta de destino além da 80/443, mas somente se não estiverem usando o protocolo http ou https por especificar o conjunto de hosts de destino (nomes ou IP, com portas). Para cada host de destino, os clientes devem mapear a porta de destino pretendida para uma porta de 30000 a 30999.

A API deve responder em apenas alguns segundos, indicando um status de atualização e, após cerca de 10 minutos, o método `GET` do endpoint deve indicar que a rede avançada está ativada.

### Atualizações {#updating-flexible-port-egress-provision}

A configuração do nível de programa pode ser atualizada chamando o endpoint `PUT /api/program/<program_id>/network/<network_id>` e terá efeito em alguns minutos.

>[!NOTE]
>
> O parâmetro &quot;kind&quot; (`flexiblePortEgress`, `dedicatedEgressIP` ou `VPN`) não pode ser modificado. Entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.

As regras de encaminhamento de porta por ambiente podem ser atualizadas chamando novamente o endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, certificando-se de incluir o conjunto completo de parâmetros de configuração, em vez de um subconjunto.

### Desativar a saída de porta flexível {#disabling-flexible-port-egress-provision}

Para **desabilitar** a saída de porta flexível de um ambiente específico, chame `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Para obter mais informações sobre as APIs, consulte a [Documentação da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Roteamento de tráfego {#flexible-port-egress-traffic-routing}

Para o tráfego http ou https fluindo para portas que não sejam a 80 ou a 443, um proxy deve ser configurado usando as seguintes variáveis de ambiente de host e porta:

* para HTTP: `AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` (padrão para `proxy.tunnel:3128` em versões AEM &lt; 6094)
* para HTTPS: `AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` (padrão para `proxy.tunnel:3128` em versões AEM &lt; 6094)

Por exemplo, este é um exemplo de código para enviar uma solicitação para o `www.example.com:8443`:

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Ao usar bibliotecas de rede Java não padrão, configure proxies usando as propriedades acima para todo o tráfego.

O tráfego não http/s com destinos por meio de portas declaradas no parâmetro `portForwards` deve fazer referência a uma propriedade chamada `AEM_PROXY_HOST`, juntamente com a porta mapeada. Por exemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

A tabela abaixo descreve o roteamento de tráfego:

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de destino</th>
    <th>Porta </th>
    <th>Conexão</th>
    <th>Exemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo http ou https</b></td>
    <td>Tráfego http/s padrão</td>
    <td>80 ou 443</td>
    <td>Permitido</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Tráfego não padrão (em outras portas fora a 80 ou 443) por proxy http configurado, usando a variável de ambiente a seguir e o número da porta do proxy. Não declare a porta de destino no parâmetro portForwards da chamada da API do Cloud Manager:<br><ul>
     <li>AEM_PROXY_HOST (padrão para `proxy.tunnel` em versões AEM &lt; 6094)</li>
     <li>AEM_HTTPS_PROXY_PORT (padrão para a porta 3128 em versões AEM &lt; 6094)</li>
    </ul>
    <td>Exceto portas 80 ou 443</td>
    <td>Permitido</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>Tráfego não padrão (em outras portas fora das portas 80 ou 443) não usando proxy http</td>
    <td>Exceto portas 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não https</b></td>
    <td>O cliente se conecta à variável de ambiente <code>AEM_PROXY_HOST</code> usando um <code>portOrig</code> declarado no parâmetro da API <code>portForwards</code>.</td>
    <td>Qualquer</td>
    <td>Permitido</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Todo o resto</td>
    <td>Qualquer</td>
    <td>Bloqueado</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Configuração do Apache/Dispatcher**

A diretiva `mod_proxy` da camada do AEM Cloud Service Apache/Dispatcher pode ser configurada usando as propriedades descritas acima.

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Endereço IP de saída dedicado {#dedicated-egress-IP-address}

>[!NOTE]
>
>Se um IP de saída dedicado tiver sido provisionado a você antes da versão de setembro de 2021 (06/10/21), consulte [Clientes com endereço de saída dedicado herdado](#legacy-dedicated-egress-address-customers).

### Benefícios {#benefits}

Esse endereço IP dedicado pode melhorar a segurança ao ser integrado a fornecedores SaaS (como um fornecedor de CRM) ou outras integrações fora do AEM as a Cloud Service que oferecem uma lista de permissões de endereços IP. Adicionar o endereço IP dedicado à lista de permissões garante que somente o tráfego do AEM Cloud Service do cliente possa fluir para o serviço externo. Além do tráfego de qualquer outro IP permitido.

Sem o recurso de endereço IP dedicado habilitado, o tráfego proveniente do AEM as a Cloud Service flui por meio de um conjunto de IPs compartilhados com outros clientes.

### Configuração {#configuring-dedicated-egress-provision}

>[!INFO]
>
>O recurso de encaminhamento do Splunk não é possível em um endereço IP de saída dedicado.

A configuração do endereço IP de saída dedicado é idêntica à [saída de porta flexível](#configuring-flexible-port-egress-provision).

A principal diferença é que o tráfego sempre sairá de um IP dedicado e único. Para localizar esse IP, use um resolvedor de DNS para identificar o endereço IP associado a `p{PROGRAM_ID}.external.adobeaemcloud.com`. Não é esperado que o endereço IP mude, mas se precisar mudar no futuro, será fornecida uma notificação com antecedência.

Além das regras de roteamento compatíveis com egressos flexíveis da porta no endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, o endereço IP de saída dedicado suporta um parâmetro `nonProxyHosts`. Isso permite declarar um conjunto de hosts que devem rotear por um intervalo de endereços IPs compartilhados em vez do IP dedicado, o que pode ser útil, pois a criação de tráfego por meio de IPs compartilhados pode ser otimizada ainda mais. Os URLs `nonProxyHost` podem seguir os padrões `example.com` ou `*.example.com`, em que o curinga é compatível somente no início do domínio.

Ao decidir entre saída de porta flexível e endereço IP de saída dedicado, os clientes devem escolher saída de porta flexível se um endereço IP específico não for necessário, pois a Adobe pode otimizar o desempenho do tráfego de saída de porta flexível.

### Desativar o endereço IP de saída dedicado {#disabling-dedicated-egress-IP-address}

Para **desativar** o endereço IP de saída dedicado de um ambiente específico, chame `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Para obter mais informações sobre as APIs, consulte a [Documentação da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Roteamento de tráfego {#dedcated-egress-ip-traffic-routing}

O tráfego http ou https passará por um proxy pré-configurado, desde que use propriedades padrão do sistema Java para configurações de proxy.

O tráfego não http/s com destinos por meio de portas declaradas no parâmetro `portForwards` deve fazer referência a uma propriedade chamada `AEM_PROXY_HOST`, juntamente com a porta mapeada. Por exemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de destino</th>
    <th>Porta </th>
    <th>Conexão</th>
    <th>Exemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo http ou https</b></td>
    <td>Tráfego para serviços do Azure ou da Adobe</td>
    <td>Qualquer</td>
    <td>Por meio dos IPs de cluster compartilhados (não o IP dedicado)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente ao parâmetro <code>nonProxyHosts</code></td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente ao parâmetro <code>nonProxyHosts</code></td>
    <td>Exceto portas 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Por meio da configuração de proxy http, configurada por padrão para tráfego http/s usando a biblioteca HTTP Java padrão do cliente</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca HTTP Java padrão do cliente ou se uma biblioteca Java que ignora a configuração do proxy padrão for usada)</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca HTTP Java padrão do cliente ou se uma biblioteca Java que ignora a configuração do proxy padrão for usada)</td>
    <td>Exceto portas 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não https</b></td>
    <td>O cliente se conecta à variável env <code>AEM_PROXY_HOST</code> usando uma <code>portOrig</code> declarada no parâmetro de API <code>portForwards</code></td>
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

## Uso de recursos {#feature-usage}

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

Um exemplo usando o Apache HttpClient, que requer chamadas explícitas ao
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) ou o uso de
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

O mesmo IP dedicado é aplicado a todos os programas de um cliente em sua Organização Adobe e para todos os ambientes em cada um de seus programas. Isso se aplica aos serviços de autor e de publicação.

### Considerações sobre depuração {#debugging-considerations}

Para validar se o tráfego está saindo no endereço IP dedicado esperado, verifique os logs no serviço de destino, se disponível. Caso contrário, pode ser útil chamar um serviço de depuração como [https://ifconfig.me/IP](https://ifconfig.me/IP), que retornará o endereço IP de chamada.

## Clientes de endereço de saída dedicado herdado {#legacy-dedicated-egress-address-customers}

Se você tiver sido provisionado com um IP de saída dedicado antes de 30/09/2021, seu recurso de IP de saída dedicado só será compatível com portas HTTP e HTTPS.
Isso inclui HTTP/1.1 e HTTP/2 quando há criptografia. Além disso, um endpoint de saída dedicado pode conversar com qualquer público-alvo somente por HTTP/HTTPS nas portas 80/443, respectivamente.

## VPN (Virtual Private Network) {#vpn}

A VPN permite a conexão com uma infraestrutura local ou data center do autor, publicação ou pré-visualização. Por exemplo, para os meios de acessar um banco de dados.

Também permite a Conexão com fornecedores SaaS, como um fornecedor CRM que oferece suporte a VPN ou à conexão de uma rede corporativa ao autor, pré-visuzliação ou publicação do AEM as a Cloud Service.

A maioria dos dispositivos VPN com tecnologia IPSec é compatível. Consulte a lista de dispositivos [nesta página](https://docs.microsoft.com/pt-br/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), com base nas informações da coluna **instruções de configuração RouteBased**. Configure o dispositivo conforme descrito na tabela.

### Considerações gerais {#general-vpn-considerations}

* Suporte limitado a uma única conexão VPN
* O recurso de encaminhamento do Splunk não é possível em uma conexão VPN.

### Criação {#vpn-creation}

Uma vez por programa, o endpoint POST `/program/<programId>/networkInfrastructures` é chamado, transmitindo uma carga de informações de configuração incluindo: o valor de &quot;vpn&quot; para o parâmetro `kind`, região, espaço de endereço (lista de CIDRs - observe que isso não pode ser modificado posteriormente), resolvedores de DNS (para resolver nomes na rede do cliente) e informações de conexão VPN, como configuração de gateway, chave VPN compartilhada e política de segurança de IP. O endpoint responde com `network_id`, bem como através de outras informações, incluindo o status. O conjunto completo de parâmetros e a sintaxe exata devem ser referenciados na [documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Uma vez chamada, a infraestrutura de rede, normalmente, levará de 45 a 60 minutos para ser provisionada. O método GET da API pode ser chamado para retornar o status atual, que em dado momento inverterá de `creating` para `ready`. Consulte a documentação da API para todos os estados.

Se a configuração de VPN com escopo de programa estiver pronta, o endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve ser chamado por ambiente para habilitar a rede no nível do ambiente e declarar quaisquer regras de encaminhamento de porta. Os parâmetros são configuráveis por ambiente para oferecer flexibilidade.

Consulte a [documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) para obter mais informações.

As regras de encaminhamento de portas devem ser declaradas para qualquer tráfego TCP de protocolo não http/s, roteado através da VPN, especificando o conjunto de hosts de destino (nomes ou IP e com portas). Para cada host de destino, os clientes devem mapear a porta de destino pretendida para uma porta de 30000 a 30999, em que os valores sejam exclusivos nos ambientes no programa. Os clientes também podem listar um conjunto de url no parâmetro `nonProxyHosts`, que declara o URL para o qual o tráfego deve ignorar o roteamento VPN, seguindo através de um intervalo de IP compartilhado. Os padrões seguidos são os de `example.com` ou `*.example.com`, em que o curinga é compatível somente no início do domínio.

A API deve responder em apenas alguns segundos, indicando um status de `updating` e após cerca de 10 minutos, uma chamada para o endpoint de GET do ambiente do Cloud Manager mostraria um status de `ready`, indicando que a atualização do ambiente foi aplicada.

Observe que mesmo se não houver regras de roteamento de tráfego de ambiente (hosts ou ignoradas), `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` ainda deve ser chamado, apenas com uma carga vazia.

### Atualização da VPN {#updating-the-vpn}

A configuração de VPN no nível do programa pode ser atualizada chamando o endpoint `PUT /api/program/<program_id>/network/<network_id>`.

Observe que o espaço de endereço não pode ser alterado após o provisionamento de VPN inicial. Se isso for necessário, entre em contato com o suporte ao cliente. Além disso, o parâmetro `kind` (`flexiblePortEgress`, `dedicatedEgressIP` ou `VPN`) não pode ser modificado. Entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.

As regras de roteamento por ambiente podem ser atualizadas chamando novamente o endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, certificando-se de incluir o conjunto completo de parâmetros de configuração, em vez de um subconjunto. As atualizações de ambiente normalmente levam de 5 a 10 minutos para serem aplicadas.

### Desativar a VPN {#disabling-the-vpn}

Para desativar a VPN para um ambiente específico, chame `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Mais detalhes na [Documentação da API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Roteamento de tráfego {#vpn-traffic-routing}

A tabela abaixo descreve o roteamento de tráfego.

<table>
<thead>
  <tr>
    <th>Tráfego</th>
    <th>Condição de destino</th>
    <th>Porta </th>
    <th>Conexão</th>
    <th>Exemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo http ou https</b></td>
    <td>Tráfego para serviços do Azure ou da Adobe</td>
    <td>Qualquer</td>
    <td>Por meio dos IPs de cluster compartilhados (não o IP dedicado)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente ao parâmetro <code>nonProxyHosts</code></td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host correspondente ao parâmetro <code>nonProxyHosts</code></td>
    <td>Exceto portas 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP cair no intervalo <i>Endereço de gateway de VPN</i> e por meio da configuração de proxy http (configurada por padrão para tráfego http/s usando a biblioteca Java padrão do cliente HTTP)</td>
    <td>Qualquer</td>
    <td>Através da VPN</td>
    <td><code>10.0.0.1:443</code>Também pode ser um nome de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP não cair no intervalo <i>de endereço de gateway de VPN</i> e por meio da configuração de proxy http (configurada por padrão para tráfego http/s usando a biblioteca Java padrão do cliente HTTP)</td>
    <td>Qualquer</td>
    <td>Por meio do IP de saída dedicado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca Java padrão do cliente HTTP ou se estiver usando a biblioteca Java que ignora a configuração de proxy padrão)
</td>
    <td>80 ou 443</td>
    <td>Por meio dos IPs de cluster compartilhados</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora a configuração do proxy http (por exemplo, se for removido explicitamente da biblioteca Java padrão do cliente HTTP ou se estiver usando a biblioteca Java que ignora a configuração de proxy padrão)</td>
    <td>Exceto portas 80 ou 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Não http ou não https</b></td>
    <td>Se o IP cai no intervalo de <i>espaço de endereço do gateway de VPN</i> e o cliente se conecta à <code>AEM_PROXY_HOST</code> variável env usando uma <code>portOrig</code> declarada no parâmetro <code>portForwards</code> de API</td>
    <td>Qualquer</td>
    <td>Através da VPN</td>
    <td><code>10.0.0.1:3306</code>Também pode ser um nome de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se o IP não cair no intervalo de <i>espaço de endereço do gateway de VPN</i> e o cliente se conectar à <code>AEM_PROXY_HOST</code> variável env usando uma <code>portOrig</code> declarada no parâmetro <code>portForwards</code> de API</td>
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

### Domínios úteis para configuração {#vpn-useful-domains-for-configuration}

O diagrama abaixo fornece uma representação visual de um conjunto de domínios e IPs associados que são úteis para configuração e desenvolvimento. A tabela abaixo do diagrama descreve esses domínios e IPs.

![Configuração de domínio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Padrão de domínio</th>
    <th>Significado de saída (do AEM)</th>
    <th>Significado de entrada (no AEM)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Endereço IP de saída dedicado para o tráfego flui para a Internet e não para redes privadas </td>
    <td>As conexões da VPN seriam exibidas na CDN como provenientes desse IP. Para permitir que somente conexões da VPN entrem no AEM, configure o Cloud Manager para permitir somente esse IP e bloquear todo o resto. Consulte a seção "Restringir ingresso em conexões VPN" para obter mais detalhes.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/A</td>
    <td>O IP do gateway de VPN no lado do AEM. A equipe de engenharia de rede de um cliente pode usar isso para permitir somente conexões VPN, de um endereço IP específico, ao respectivo gateway de VPN. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}.inner.adobeaemcloud.net</code></td>
    <td>O IP do tráfego vindo do lado AEM da VPN para o lado do cliente. Isso pode ser incluído na lista de permissões na configuração do cliente para garantir que as conexões só possam ser feitas a partir do AEM.</td>
    <td>Se o cliente quiser permitir o acesso por VPN ao AEM, ele deverá configurar as entradas de DNS CNAME para mapear seu domínio personalizado e/ou <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> e/ou <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> para isso.</td>
  </tr>
</tbody>
</table>

### Restringir VPN a conexões de entrada {#restrict-vpn-to-ingress-connections}

Se você quiser permitir somente o acesso VPN ao AEM, as listas de permissões do ambiente poderão ser configuradas no Cloud Manager para que somente o IP definido por `p{PROGRAM_ID}.external.adobeaemcloud.com` tenha permissão para se comunicar com o ambiente. Isso pode ser feito da mesma forma que qualquer outra lista de permissões baseada em IP no Cloud Manager.

Se as regras tiverem de ser baseadas em caminho, use as diretivas http padrão no nível do dispatcher para negar ou permitir determinados IPs. Isso deve garantir que os caminhos desejados também não sejam armazenados em cache na CDN, para que a solicitação sempre chegue à origem.

**Exemplo De Configuração Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Excluir a infraestrutura de rede de um programa {#deleting-network-infrastructure}

Para **excluir** a infraestrutura de rede de um programa, chame `DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`.

>[!NOTE]
>
> Isso só excluirá a infraestrutura se todos os ambientes tiverem suas redes avançadas desativadas.

## Transição entre tipos avançados de rede {#transitioning-between-advanced-networking-types}

É possível migrar entre tipos avançados de rede seguindo o procedimento abaixo:

* desativar a rede avançada em todos os ambientes
* excluir a infraestrutura de rede avançada
* recriar as infraestruturas de rede avançadas com os valores corretos
* reativar a rede avançada no nível do ambiente

>[!WARNING]
>
> Esse procedimento resultará em um tempo de inatividade dos serviços de rede avançada durante o período de exclusão e recriação

Se o tempo de inatividade causar um impacto significativo nos negócios, entre em contato com o suporte ao cliente para obter assistência, descrevendo o que já foi criado e o motivo da alteração.

## Configuração avançada de rede para regiões de publicação adicionais {#advanced-networking-configuration-for-additional-publish-regions}

Quando uma região adicional é adicionada a um ambiente que já tem rede avançada configurada, o tráfego da região de publicação adicional que corresponde às regras de rede avançadas será roteado por padrão pela região primária. No entanto, se a região primária se tornar indisponível, o tráfego de rede avançado será descartado se a rede avançada não tiver sido habilitada na região adicional. Se você quiser otimizar a latência e aumentar a disponibilidade caso uma das regiões sofra uma interrupção, será necessário ativar a rede avançada para a(s) região(ões) de publicação adicional(is). Dois cenários diferentes são descritos nas seções a seguir.

>[!NOTE]
>
>Todas as regiões compartilham a mesma [configuração de rede avançada do ambiente](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration), portanto, não é possível rotear o tráfego para destinos diferentes com base na região de onde o tráfego está saindo.

### Endereços IP de saída dedicados {#additional-publish-regions-dedicated-egress}

#### Rede avançada já habilitada na região principal {#already-enabled}

Se uma configuração avançada de rede já estiver ativada na região principal, siga estas etapas:

1. Se você tiver bloqueado sua infraestrutura de modo que o endereço IP do AEM dedicado seja incluído na lista de permissões, é recomendável desativar temporariamente todas as regras de negação nessa infraestrutura. Se isso não for feito, haverá um curto período em que as solicitações dos endereços IP da nova região serão negadas pela sua própria infraestrutura. Observe que isso não é necessário se você tiver bloqueado sua infraestrutura por meio do FQDN (Fully Qualified Domain Name, Nome de domínio totalmente qualificado), (`p1234.external.adobeaemcloud.com`, por exemplo), já que todas as regiões AEM geram tráfego de rede avançado do mesmo FQDN
1. Crie a infraestrutura de rede com escopo de programa para a região secundária por meio de uma chamada de POST para a API Criar infraestrutura de rede do Cloud Manager, conforme descrito na documentação avançada de rede. A única diferença na configuração JSON do payload em relação à região principal será a propriedade region
1. Se sua infraestrutura precisar ser bloqueada por IP para permitir o tráfego de AEM, adicione os IPs correspondentes `p1234.external.adobeaemcloud.com`. Deve haver um por região.

#### Rede avançada ainda não configurada em nenhuma região {#not-yet-configured}

O procedimento é basicamente semelhante às instruções anteriores. No entanto, se o ambiente de produção ainda não tiver sido habilitado para redes avançadas, haverá uma oportunidade de testar a configuração, primeiro habilitando-a em um ambiente de preparo:

1. Criar uma infraestrutura de rede para todas as regiões por meio de uma chamada de POST para a [Criar API de infraestrutura de rede do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Network-infrastructure/operation/createNetworkInfrastructure). A única diferença na configuração JSON do payload em relação à região principal será a propriedade region.
1. Para o ambiente de preparo, habilite e configure a rede avançada com escopo de ambiente executando `PUT api/program/{programId}/environment/{environmentId}/advancedNetworking`. Para obter mais informações, consulte a documentação da API [aqui](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration/operation/enableEnvironmentAdvancedNetworkingConfiguration)
1. Se necessário, bloqueie a infraestrutura externa, de preferência por FQDN (por exemplo, `p1234.external.adobeaemcloud.com`). Caso contrário, você pode fazer isso por endereço IP
1. Se o ambiente de preparo funcionar conforme o esperado, habilite e configure a configuração de rede avançada com escopo de ambiente para produção.

#### VPN {#vpn-regions}

O procedimento é quase idêntico às instruções dos endereços IP de saída dedicados. A única diferença é que, além de a propriedade region ser configurada de forma diferente da região principal, a variável `connections.gateway` O campo pode, opcionalmente, ser configurado para rotear para um terminal VPN diferente operado por sua organização, talvez geograficamente mais próximo da nova região.
