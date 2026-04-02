---
title: Teste de Conectividade de Rede
description: Use o teste de conectividade de rede no Cloud Manager para validar a configuração de rede avançada e VPN do caminho de saída do seu programa antes de habilitar a rede em ambientes.
feature: Security
role: Admin
source-git-commit: b29b3a980a0bc1c619fb23c52acda79fae9bf945
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 1%

---


# Teste de Conectividade de Rede {#network-connectivity-test}

O **Teste de Conectividade de Rede** é uma ferramenta de diagnóstico da Cloud Manager que permite validar a configuração de Rede Avançada e VPN antes de habilitar a Rede Avançada em seus ambientes e antes de você ativar. Use-o para verificar se os hosts e as portas que o AEM deve alcançar, incluindo endpoints internos ou privados, podem ser acessados pelo mesmo caminho de conectividade que a Rede avançada usará.

O teste é executado da **infraestrutura de proxy de saída** que pertence à configuração Avançada de Rede do seu programa, não de um pod Autor ou Publicação. Ele usa o mesmo caminho de rede de saída que a AEM usa quando a Rede avançada está ativa. Este design é especialmente útil para cenários de **VPN**: você pode confirmar a resolução de DNS, o roteamento de rede, as regras de firewall e a disponibilidade de serviço para sistemas privados ou locais antes de entrar em funcionamento.

Para obter informações sobre o provisionamento de VPN, IP de saída dedicado ou saída de porta flexível, consulte [Configurando a Rede Avançada para o AEM as a Cloud Service](/help/security/configuring-advanced-networking.md).

>[!IMPORTANT]
>
>Um teste de conectividade bem-sucedido comprova que o caminho de rede do Advanced Networking pode alcançar seu público-alvo. Seu código de aplicativo ainda deve ser configurado para usar o proxy de rede avançada quando necessário (por exemplo, variáveis de ambiente relacionadas ao proxy e encaminhamento de portas). Se o código ignorar o proxy, talvez você não veja o tráfego do caminho de saída esperado mesmo quando o teste for aprovado.

## Quando usar esta ferramenta {#when-to-use}

* Depois que a **Rede Avançada** é criada no nível do **programa** e **antes** ou ao habilitá-la em **ambientes**.
* Para validar a conectividade da **VPN** com sistemas locais ou privados que você opera (por exemplo, nomes de host internos ou endereços IP privados).
* Para restringir os problemas de DNS em relação aos problemas de firewall ou roteamento quando um serviço não responde conforme esperado.

>[!NOTE]
>
>Essa ferramenta é para programas que usam rede avançada (VPN, IP de saída dedicado ou saída de porta flexível). Não é um teste de uso geral da conectividade padrão do AEM sem a rede avançada.

## Pré-requisitos {#prerequisites}

* Um programa do Cloud Manager.
* A infraestrutura de Rede Avançada já foi criada para o programa (consulte [Configurando Rede Avançada](/help/security/configuring-advanced-networking.md)).

## Como executar um teste {#how-to-run-a-test}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e abra sua organização e programa.
1. Abra a guia **Ambientes** do programa. Na barra lateral esquerda, selecione **Infraestrutura de Rede**.

1. Na página **Infraestrutura de Rede**, localize sua infraestrutura na tabela. Selecione uma linha para abrir a experiência de teste ou abra o menu de ações de linha (![ícone Adobe Spectrum Small More para o menu de ações de linha de reticências horizontais](assets/ellipsis.svg)) e escolha **Testar**.

   ![Área Ambientes do programa Cloud Manager com a tabela Infraestrutura de Rede, linhas de infraestrutura e o menu de ações de linhas usado para iniciar o Teste de Conectividade de Rede](assets/network-connectivity-test-cloud-manager-open-test-from-infrastructure-list.png)

1. A caixa de diálogo **Teste de Rede** é aberta. Insira o **Host** e a **Porta**, selecione **Teste** e examine a resolução DNS, a porta aberta, a conectividade HTTP e a acessibilidade na área de resultados. Ações opcionais como **Copiar para a área de transferência** e histórico de testes recentes aparecem na caixa de diálogo. Consulte [Entendendo os Resultados](#understanding-results) para saber como interpretar cada seção.

   ![Caixa de diálogo Teste de Conectividade de Rede da Cloud Manager com campos Host e Porta, ação de Teste e resultados para resolução DNS, abertura de porta, conectividade HTTP e acessibilidade](assets/network-connectivity-test-cloud-manager-results-dialog.png)

### Campos de entrada {#input-fields}

| Texto | Descrição | Exemplos |
| --- | --- | --- |
| **Host** | O nome do host ou endereço IP do serviço que o AEM deve alcançar. | `internal-api.example.com`, `10.0.1.50` |
| **Porta** | Porta TCP no host de destino (1-65535). Valores comuns podem aparecer em uma lista de atalhos (por exemplo, 80, 443, 587, 22). | `443` |

### Etapas {#test-steps}

1. Insira **Host** e **Porta**.
1. Selecione **Testar**. Os resultados geralmente aparecem em alguns segundos.
1. Opcional: Use **Copiar para a área de transferência** para capturar o resultado JSON completo (útil para casos de suporte).
1. Testes recentes podem ser listados para execuções rápidas.

## Noções básicas dos resultados {#understanding-results}

A ferramenta relata várias dimensões. Juntos, eles descrevem se o público-alvo pode ser acessado a partir da rede avançada e como as verificações com reconhecimento de HTTP se comportaram.

### Resolução de DNS {#dns-resolution}

| Resultado | Significado |
| --- | --- |
| `ips: ["10.0.1.50"]` | Resolução de DNS bem-sucedida. O nome do host resolveu para o(s) endereço(s) IP listado(s) usando os resolvedores associados à sua configuração avançada de rede. |
| `error: "DNS resolution error: ..."` | Falha na resolução de DNS. Os servidores DNS configurados não puderam resolver o nome do host (nome incorreto, resolvedor não acessível, registro ausente e causas semelhantes). |

>[!NOTE]
>
>Se você inserir um **IP numérico** em vez de um nome de host, a resolução DNS será ignorada para esse valor e o IP será usado diretamente.

### Porta aberta {#port-open}

| Resultado | Significado |
| --- | --- |
| `Yes` / true | Conexão TCP bem-sucedida — a porta está aberta e aceitando conexões. |
| `No` / falso | A porta está fechada, filtrada por um firewall ou o host está inacessível. |

### Conectividade HTTP {#http-connectivity}

Tentativa de solicitação HTTP/HTTPS em **a cada porta**. A ferramenta sempre tenta **HTTPS** primeiro e depois retorna para **HTTP**. Se nenhum dos dois funcionar, o resultado será mapeado para uma mensagem de **erro** curta e legível (consulte a tabela abaixo).

**Saídas com Êxito**

| Saída | Significado |
| --- | --- |
| `protocol: "https"`, `status_code: 200`, `reason: "200 OK"` | Conexão HTTPS bem-sucedida. |
| `protocol: "http"`, `status_code: 301`, `reason: "301 Moved Permanently"` | Conexão HTTP bem-sucedida; o serviço está sendo redirecionado (normalmente para HTTPS). Isso é normal. |

**Saídas de Erro Classificadas**

| Erro | Nota | Significado |
| --- | --- | --- |
| `"Not an HTTP/HTTPS service"` | `"The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."` | A porta está aberta, mas o serviço não fala HTTP. Isso é esperado para bancos de dados, SFTP, TCP personalizado e serviços semelhantes. |
| `"Connection refused"` | `"The port is not accepting connections. Verify the service is running and listening on this port."` | Nada está escutando nesta porta. |
| `"Connection timed out"` | `"The connection timed out. Check firewall rules and network routing."` | Um problema de firewall ou roteamento está impedindo a conexão. |
| `"No IPs resolved for host"` | — | Falha na resolução de DNS; não é possível testar o HTTP. |

>[!NOTE]
>
>Qualquer código de status HTTP do serviço de destino (por exemplo, `200`, `301`, `302`, `403`, `404` ou `500`) é um **sinal de sucesso** para conectividade, significa que o **caminho de rede** funciona. O código de status reflete a resposta do próprio serviço, não a integridade geral da rede. Para serviços não HTTP, a ferramenta indica **Não é um serviço HTTP/HTTPS**; use **Porta aberta** e **Acessabilidade** como indicadores confiáveis para esses serviços.

### Alcance {#reachability}

| Resultado | Significado |
| --- | --- |
| **Acessível** | O host e a porta de destino podem ser acessados na infraestrutura avançada de rede. A configuração de rede está correta. |
| **Inacessível: Porta não acessível** | O DNS foi resolvido com êxito, mas o TCP na porta não foi bem-sucedido. Isso geralmente é um problema de firewall ou roteamento. |
| **Inacessível: falha na resolução de DNS** | Não foi possível resolver o nome do host com a sua configuração. Isso é uma indicação de um problema de configuração de DNS. |

### Vários resolvedores de DNS {#multiple-dns-resolvers}

Se sua infraestrutura de Rede Avançada definir **mais de um resolvedor de DNS**:

* Quando **todos os resolvedores retornam resultados idênticos**, você vê um resultado **único consolidado** rotulado `default`.
* Quando os resolvedores retornam **resultados diferentes**, cada resultado do resolvedor é mostrado **separadamente** (rotulado `resolver_1`, `resolver_2` e assim por diante), **com o IP do resolvedor**, para que você possa ver qual servidor DNS está causando a inconsistência.

## Resolução de problemas {#troubleshooting}

Os cenários a seguir combinam o que você provavelmente verá na ferramenta com etapas para restringir a causa. Para obter o JSON **Copiar para a área de transferência** completo, que ilustra as mesmas situações, consulte [Exemplos de Saídas](#example-outputs).

### Falha na resolução de DNS {#dns-failed}

#### Saída

O nome de host não foi resolvido usando as configurações de DNS de rede avançada, portanto, a ferramenta não pode testar a porta. Na exibição de resultados, a **resolução DNS** mostra uma cadeia de caracteres de erro, e a **Capacidade de alcance** relata que o DNS falhou:

```
DNS Resolution: error: "DNS resolution error: ..."
Reachability: "Unreachable: DNS resolution failed"
```

#### Recomendações

1. **Verifique se o nome do host está correto**—verifique se há erros de digitação e se você está usando a **zona DNS** pretendida (a zona errada é um erro comum).
1. Verifique se **seus resolvedores de DNS**—aqueles configurados na infraestrutura de rede—estão **acessíveis a partir do intervalo CIDR de Rede Avançada** (o mesmo espaço de endereço que a ferramenta e o AEM usam para verificações de saída). Se você depende de DNS privado, esses servidores devem ser acessíveis através do túnel VPN ou dentro do espaço de endereço de rede que o roteamento expõe à Rede avançada.
1. **Verifique se os servidores DNS configurados podem resolver o nome do host** — A Rede Avançada usa **somente** os resolvedores definidos na configuração da infraestrutura de rede, **não** DNS público (por exemplo, `8.8.8.8`). Se o DNS interno não tiver registro para esse nome de host, a resolução falhará.
1. **Para configurações VPN:** Confirme se os endereços IP do servidor DNS estão no espaço de endereço VPN (o CIDR da rede remota para o qual o túnel foi criado). Os resolvedores em uma sub-rede que não é roteada pelo túnel VPN não podem ser acessados pela rede avançada.

### O DNS funciona, mas a porta não está acessível {#dns-ok-port-blocked}

#### Saída

A ferramenta pode resolver o host, mas o TCP na porta não é bem-sucedido. Um resumo geralmente tem esta aparência:

```
DNS Resolution: ips: ["10.0.1.50"]
Port Open: No
Reachability: "Unreachable: Port not accessible"
```

#### Recomendações

1. **Revisar regras de firewall e de lista de permissões no serviço de destino**—o tráfego de entrada do intervalo CIDR da infraestrutura Avançada de Rede (e os endereços IP de saída que a AEM usa) deve ser permitido. Se você usa uma VPN, inclua CIDRs de rede remota conforme exigido pelo design.
1. **Verifique se o serviço está em execução** e **escutando no host e na porta** que você inseriu no teste.
1. **Para configurações de VPN:** Confirme se o túnel está ativo, se o roteamento atinge a sub-rede de destino e se o endereço de destino se encontra no espaço de endereço de rede remoto transportado pela VPN.
1. Em sua infraestrutura, analise os **NSGs (grupos de segurança de rede), regras de segurança ou equivalente** que podem bloquear a porta entre a Rede Avançada e o destino.
1. **Confirme o número da porta**—verifique se o processo está realmente escutando na porta que você está testando.

### O teste mostra que é possível acessar, mas o AEM não se conecta {#reachable-but-aem-fails}

#### Saída

A própria verificação de conectividade foi bem-sucedida. Um resumo condensado geralmente tem esta aparência:

```
Port Open: Yes
Reachability: "Reachable"
```

Esse resultado significa que o caminho da rede avançada para o host e a porta que você testou está aberto. Isso não garante que o tráfego do aplicativo AEM esteja usando esse caminho: quando seu código é executado, os logs de serviço ainda podem não mostrar nenhuma solicitação do IP de saída esperado.

#### Recomendações

1. **O código do aplicativo deve ser configurado para usar o proxy**. O teste de conectividade comprova que o caminho de rede funciona, mas o AEM deve rotear explicitamente as solicitações por meio do **proxy de rede avançada** (por exemplo, por meio da variável de ambiente **`AEM_PROXY_HOST`**). Se o código fizer conexões diretas sem o proxy, o tráfego não passará pela infraestrutura avançada de rede.
1. **Revisar configurações de proxy em seus clientes HTTP** - Os clientes HTTP devem usar a mesma configuração de proxy (`AEM_PROXY_HOST` e encaminhamento de porta, quando aplicável).
1. **Verifique a configuração de encaminhamento de porta** para Rede Avançada no nível **ambiente**: em `portForwards`, cada entrada deve mapear **`portOrig`** para **`portDest`** no **host de destino** direito. **`portOrig`** é a **porta à qual o código de aplicativo do AEM se conecta** quando abre a conexão de saída por meio do proxy. **`portDest`** é a **porta real no serviço de destino** onde o processo remoto está escutando. O **host de destino** é o **nome do host ou endereço desse serviço** conforme usado no encaminhamento. Todos os três devem corresponder ao modo como o aplicativo é gravado para conexão.
1. **Verificar`nonProxyHosts`**. Se o host de destino estiver listado lá, as solicitações **ignorarão o proxy** para esse host e não seguirão o caminho de Rede Avançada validado.

### HTTP mostra um erro, mas a porta está aberta {#http-error-port-open}

#### Saída

TCP bem-sucedido, mas o teste HTTP/HTTPS ainda relata uma falha. Um resumo geralmente tem esta aparência:

```
Port Open: Yes
HTTP Connectivity: error: "Connection error: ..." or "Both HTTPS and HTTP failed. ..."
Reachability: "Reachable"
```

#### Recomendações

1. **O serviço pode não falar HTTP ou HTTPS** — por exemplo, TCP bruto, gRPC ou outro protocolo. A investigação HTTP pode falhar enquanto `Port open: Yes` e `Reachability: Reachable` ainda confirmam que o caminho de rede funciona. Use esses campos como a fonte da verdade para serviços não HTTP.
1. **Investigar configuração de TLS e certificado**. Se o HTTPS falhar, mas o HTTP for bem-sucedido (às vezes indicado por uma observação como `HTTPS failed, HTTP succeeded`), o serviço pode ter problemas de certificado ou pode oferecer HTTP somente nessa porta.

### Tempo limite da solicitação {#timeout}

#### Saída

```json
{ "error": "Request timeout" }
```

#### Recomendações

1. **Permitir tempo de resposta do serviço**—a verificação usa um tempo limite de 5 segundos. Alvos que respondem mais lentamente do que isso expirarão mesmo quando estiverem de outra forma saudáveis.
1. **Conta para latência de rede**. Em conexões VPN, a alta latência ou um túnel não íntegro podem ultrapassar o limite; revise o status e o roteamento do túnel.
1. **Executar o teste novamente**. Falhas de rede únicas podem produzir um tempo limite que não se repete.

## Exemplo de saídas {#example-outputs}

### Teste HTTPS bem-sucedido (por exemplo, API interna na porta 443) {#example-output-successful-https}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "protocol": "https",
        "status_code": 200,
        "reason": "200 OK"
      },
      "reachability": "Reachable"
    }
  ]
}
```

### Teste de Serviço Não HTTP Bem-sucedido (por exemplo, Banco de Dados na Porta 5432) {#example-output-successful-non-http}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "error": "Not an HTTP/HTTPS service",
        "note": "The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."
      },
      "reachability": "Reachable"
    }
  ]
}
```

>[!NOTE]
>
>O erro HTTP é esperado para serviços não HTTP. **Abertura de Porta: true** e **Acessabilidade: Acessível** confirme se o caminho de rede funciona.

### Falha de Resolução de DNS {#example-output-dns-resolution-failure}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "error": "DNS resolution error: dial udp 10.0.0.2:53: i/o timeout"
      },
      "port_open": false,
      "http_connectivity": {
        "error": "DNS resolution failed"
      },
      "reachability": "Unreachable: DNS resolution failed"
    }
  ]
}
```

### Porta Não Acessível (Firewall / Serviço Inativo) {#example-output-port-not-accessible}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": false,
      "http_connectivity": {
        "error": "Connection error: dial tcp 10.0.1.50:443: i/o timeout"
      },
      "reachability": "Unreachable: Port not accessible"
    }
  ]
}
```

## Observações importantes {#important-notes}

### O que este teste não faz {#what-this-test-does-not-do}

* O teste não é executado de dentro de um autor do AEM ou pod de publicação. Ela é executada a partir de **infraestrutura de proxy de saída**. Isso valida a camada de rede e não a configuração de proxy no nível do aplicativo no código.
* Isso não valida as configurações de proxy do aplicativo AEM. Mesmo quando o resultado é `Reachable`, o código AEM ainda deve ser configurado para usar o proxy.
* Ela não valida a configuração de encaminhamento de portas no nível do ambiente por si só. Testa a conectividade bruta do caminho da infraestrutura.
* Ele não envia cargas personalizadas. Testes HTTP emitem uma solicitação básica de `GET` para `/`.

### Tempo de resposta {#response-time}

* **Típica:** cerca de 2 a 3 segundos.
* **Máximo:** tempo limite de aproximadamente cinco segundos.
* **Todos os resolvedores de DNS** e verificações de conectividade são executados em paralelo.

### Serviços HTTP vs. não HTTP {#http-vs-non-http-services}

A ferramenta tenta uma conexão HTTP/HTTPS em cada porta. Para serviços não HTTP (por exemplo, PostgreSQL na porta 5432, MySQL em 3306, SFTP em 22, Redis em 6379), a verificação HTTP pode falhar com um erro de conexão; isso é esperado. Conte com `Port open` e `Reachability` para confirmar a conectividade desses serviços.

## Informações relacionadas {#related-information}

* [Configuração de redes avançadas para o AEM as a Cloud Service](/help/security/configuring-advanced-networking.md)
* [Tutoriais avançados de rede no Experience League](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/advanced-networking)
