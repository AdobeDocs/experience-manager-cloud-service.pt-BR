---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: Diretrizes de desenvolvimento do AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: a3d940765796e6a4d8e16d8fe31343074358ebc3
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 1%

---


# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

O código sendo executado em AEM como um Cloud Service deve estar ciente do fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida em qualquer momento.

Durante a atualização do AEM como um Cloud Service, haverá instâncias com o código novo e antigo sendo executado em paralelo. Portanto, o código antigo não deve quebrar com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se houver a necessidade de identificar o principal no cluster, a API de descoberta Apache Sling pode ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas persistido no repositório. Caso contrário, esse estado pode ser perdido se uma instância for interrompida.

## Estado no sistema de arquivos {#state-on-the-filesystem}

O sistema de arquivos da instância não deve ser usado em AEM como Cloud Service. O disco é efêmero e será descartado quando as instâncias forem recicladas. A utilização limitada do sistema de arquivos para armazenamentos temporários relacionados com o processamento de pedidos únicos é possível, mas não deve ser abusada para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso de recursos e ser executado em limitações de disco.

Como exemplo, onde o uso do sistema de arquivos não é suportado, a camada de publicação deve garantir que todos os dados que precisam ser persistentes sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Da mesma forma, com tudo o que está a acontecer de forma assíncrona, como atuar sobre eventos de observação, não se pode garantir que seja executado localmente, pelo que tem de ser utilizado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recursos Sling. No momento em que uma alteração ocorre, a instância pode ser retirada e substituída por uma instância diferente. Outras instâncias na topologia que estão ativas no momento poderão reagir a esse evento. No entanto, neste caso, este não será um evento local e pode até não haver um líder ativo no caso de uma eleição de líder em curso quando o evento for emitido.

## Tarefas em segundo plano e trabalhos de longa execução {#background-tasks-and-long-running-jobs}

O código executado como tarefas em segundo plano deve supor que a instância em que está sendo executado pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e a maior parte das importações retomável. Isso significa que, se o código for executado novamente, ele não deve ser start do início novamente, mas sim do ponto em que parou. Embora este não seja um requisito novo para esse tipo de código, em AEM como Cloud Service é mais provável que ocorra uma derrubada de instância.

Para minimizar os problemas, devem ser evitados trabalhos de longa duração, se possível, e eles devem ser retomados no mínimo. Para executar esses trabalhos, use os Trabalhos Sling, que têm uma garantia pelo menos uma vez e, portanto, se forem interrompidos, serão executados novamente o mais rápido possível. Mas eles provavelmente não deveriam start desde o início novamente. Para agendar esses trabalhos, é melhor usar o scheduler [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) como novamente a execução pelo menos uma vez.

O Scheduler Sling Commons não deve ser usado para agendamento, pois a execução não pode ser garantida. É mais provável que seja agendada.

Da mesma forma, com tudo o que está a acontecer de forma assíncrona, como atuar sobre eventos de observação (quer seja, eventos de JCR ou eventos de recursos de Sling), não se pode garantir que seja executado e, portanto, deve ser usado com cuidado. Isso já é válido para implantações AEM no presente.

## Conexões HTTP de Saída {#outgoing-http-connections}

É altamente recomendável que todas as conexões HTTP de saída definam tempos limite de conexão e leitura razoáveis. Para códigos que não aplicam esses tempos limite, instâncias AEM executadas em AEM como Cloud Service, imporão um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões usadas pelas seguintes bibliotecas Java populares:

O Adobe recomenda o uso da biblioteca do Apache HttpComponents Client 4.x ](https://hc.apache.org/httpcomponents-client-ga/) fornecida para fazer conexões HTTP.[

As alternativas que são conhecidas por funcionarem, mas que podem exigir que a dependência seja fornecida por você mesmo, são:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLe/ou  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (fornecido pela AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/) (Não fornecido pela AEM)

## Nenhuma personalização de interface clássica {#no-classic-ui-customizations}

AEM como Cloud Service só suporta a interface de usuário de toque para código de cliente de terceiros. A interface clássica não está disponível para personalização.

## Evitar Binários Nativos {#avoid-native-binaries}

O código não poderá baixar binários em tempo de execução nem modificá-los. Por exemplo, ele não poderá desempacotar arquivos `jar` ou `tar`.

## Nenhum vínculo de transmissão por AEM como Cloud Service {#no-streaming-binaries}

Os binários devem ser acessados por meio do CDN, que disponibilizará binários fora dos principais serviços de AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, o que aciona o download de um binário no disco efêmero do serviço AEM.

## Nenhum agente de replicação reverso {#no-reverse-replication-agents}

A replicação reversa de Publicar para Autor não é suportada em AEM como Cloud Service. Se tal estratégia for necessária, você poderá usar um armazenamento de persistência externo que seja compartilhado entre o farm de instâncias de Publicação e, potencialmente, o cluster Autor.

## Os agentes de replicação encaminhados podem precisar ser portados {#forward-replication-agents}

O conteúdo é replicado de Autor para Publicar por meio de um mecanismo de sub-publicação. Não há suporte para agentes de replicação personalizados.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de registros são gravadas em arquivos locais na pasta `/crx-quickstart/logs`.

Em ambientes da Cloud, os desenvolvedores podem baixar os logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuração do nível de log**

Para alterar os níveis de log dos ambientes do Cloud, a configuração de Sling Logging OSGI deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e depois enviá-las para um AEM como uma instância Cloud Service. Para obter mais informações sobre como fazer isso, consulte [Implantação para AEM como Cloud Service](/help/implementing/deploying/overview.md).

**Ativando o nível de log DEBUG**

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas.
Para ativar o nível de log DEBUG, defina a variável

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

propriedade para depurar. Não deixe o log no nível de log DEBUG mais tempo do que o necessário, pois ele gera muitos logs.
Uma linha no arquivo de depuração geralmente é start com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | A ação falhou. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Info | A ação foi bem sucedida. |

### Thread Dumps {#thread-dumps}

Os despejos de processos em ambientes da Cloud são coletados de forma contínua, mas não podem ser baixados de maneira automática no momento. Enquanto isso, entre em contato com AEM suporte se os despejos por thread forem necessários para depurar um problema, especificando a janela de hora exata.

## CRX/DE Lite e Developer Console {#crxde-lite-and-developer-console}

### Desenvolvimento local {#local-development}

Para o desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e ao Console da Web AEM (`/system/console`).

Observe que no desenvolvimento local (usando o recurso de início rápido pronto para nuvem), `/apps` e `/libs` podem ser gravados diretamente, o que é diferente dos ambientes da nuvem nos quais as pastas de nível superior são imutáveis.

### AEM como ferramentas de desenvolvimento de Cloud Service {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar a lista CRXDE no ambiente de desenvolvimento da camada do autor, mas não no estágio ou na produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Um conjunto de ferramentas para depurar AEM como ambientes de desenvolvedor de Cloud Service no Developer Console para ambientes dev, stage e production. O url pode ser determinado ajustando-se as urls do serviço Autor ou Publicação da seguinte maneira:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Gerenciador de nuvem pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Como ilustrado abaixo, as informações de status disponíveis incluem o estado de pacotes, componentes, configurações OSGI, índices de carvalho, serviços OSGI e trabalhos Sling.

![Console de desenvolvedor 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como ilustrado abaixo, os desenvolvedores podem resolver dependências de pacote e servlets:

![Console de desenvolvedor 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de desenvolvedor 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explorar Query:

![Console de desenvolvedor 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas regulares, o acesso ao Console do desenvolvedor é definido pelo &quot;Gerenciador de nuvem - Função do desenvolvedor&quot; no Admin Console, enquanto para programas de caixa de proteção, o Console do desenvolvedor está disponível para qualquer usuário com um perfil de produto que fornece acesso ao AEM como um Cloud Service. Para todos os programas, &quot;Gerenciador de nuvem - Função do desenvolvedor&quot; é necessário para os despejos de status e os usuários também devem ser definidos no Perfil Usuários AEM ou Administradores AEM nos serviços de autor e publicação para que os dados de despejo de status sejam visualizações de ambos os serviços. Para obter mais informações sobre como configurar permissões de usuário, consulte [Documentação do Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).


### AEM Serviço de armazenamento temporário e produção {#aem-staging-and-production-service}

Os clientes não terão acesso à ferramenta para desenvolvedores para ambientes de preparo e produção.

### Monitoramento de desempenho {#performance-monitoring}

O Adobe monitora o desempenho do aplicativo e toma medidas para resolver se a deterioração é observada. No momento, as métricas do aplicativo não podem ser observadas.

## Endereço IP de saída dedicado {#dedicated-egress-ip-address}

Mediante solicitação, o AEM como Cloud Service fornecerá um endereço IP estático e dedicado para HTTP (porta 80) e HTTPS (porta 443) de saída programado no código Java.

### Benefícios {#benefits}

Esse endereço IP dedicado pode melhorar a segurança ao integrar-se com fornecedores SaaS (como um fornecedor de CRM) ou outras integrações fora do AEM como uma Cloud Service que oferta uma lista de permissões de endereços IP. Ao adicionar o endereço IP dedicado à lista de permissões, ele garante que somente o tráfego do Cloud Service do cliente AEM possa fluir para o serviço externo. Além do tráfego de outros IPs permitidos.

Sem o recurso de endereço IP dedicado ativado, o tráfego que sai do AEM como Cloud Service continua por meio de um conjunto de IPs compartilhados com outros clientes.

### Configuração {#configuration}

Para ativar um endereço IP dedicado, envie uma solicitação ao Suporte ao cliente, que fornecerá as informações do endereço IP. A solicitação deve especificar cada ambiente e solicitações adicionais devem ser feitas se novos ambientes precisarem do recurso após a solicitação inicial. Ambientes de programa Sandbox não são suportados.

### Uso de recursos {#feature-usage}

O recurso é compatível com código Java ou bibliotecas que resultam em tráfego externo, desde que usem propriedades padrão do sistema Java para configurações de proxy. Na prática, isso deveria incluir a maioria das bibliotecas comuns.

Abaixo está uma amostra de código:

```
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

O mesmo IP dedicado é aplicado a todos os programas de um cliente em sua Organização de Adobe e a todos os ambientes em cada um dos programas. Isso se aplica tanto aos serviços de autor quanto aos serviços de publicação.

Somente as portas HTTP e HTTPS são suportadas. Isso inclui HTTP/1.1, bem como HTTP/2 quando criptografado.

### Considerações sobre depuração {#debugging-considerations}

Para validar se o tráfego está de fato saindo no endereço IP dedicado esperado, verifique os logs no serviço de destino, se disponível. Caso contrário, pode ser útil chamar um serviço de depuração como [https://ifconfig.me/ip](https://ifconfig.me/ip), que retornará o endereço IP de chamada.

## Enviando email {#sending-email}

AEM como Cloud Service requer que o correio externo seja criptografado. As seções abaixo descrevem como solicitar, configurar e enviar emails.

### Solicitando acesso {#requesting-access}

Por padrão, o email de saída está desativado. Para ativá-lo, envie um ticket de suporte com:

1. O nome de domínio totalmente qualificado para o servidor de email (por exemplo `smtp.sendgrid.net`)
1. A porta a ser usada. Deve ser a porta 465 se for suportada pelo servidor de correio; caso contrário, a porta 587. Observe que a porta 587 só pode ser usada se o servidor de email exigir e aplicar o TLS nessa porta
1. A ID do programa e a ID do ambiente dos ambientes dos quais eles gostariam de enviar emails
1. Se o acesso SMTP é necessário para o autor, publicação ou ambos.

### Enviando emails {#sending-emails}

O serviço OSGI [Day CQ Mail Service](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) deve ser usado e os emails devem ser enviados para o servidor de correio indicado na solicitação de suporte, em vez de diretamente para os recipient.

AEM CS requer que o correio seja enviado pela porta 465. Se um servidor de correio não suportar a porta 465, a porta 587 poderá ser usada, desde que a opção TLS esteja ativada.

>[!NOTE]
>
>Observe que o Adobe não oferece suporte para o agrupamento SMTP em um endereço IP exclusivo.

### Configuração {#email-configuration}

Os emails no AEM devem ser enviados usando o serviço OSGi do [Day CQ Mail Service](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte [AEM documentação 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html) para obter detalhes sobre como configurar as configurações de email. Para AEM como Cloud Service, os seguintes ajustes devem ser feitos no serviço `com.day.cq.mailer.DefaultMailService OSGI`:

Se a porta 465 tiver sido solicitada:

* definir `smtp.port` como `465`
* definir `smtp.ssl` como `true`

Se a porta 587 tiver sido solicitada (somente permitida se o servidor de email não suportar a porta 465):

* definir `smtp.port` como `587`
* definir `smtp.ssl` como `false`

A propriedade `smtp.starttls` será automaticamente definida AEM como Cloud Service no tempo de execução para um valor apropriado. Isso será `false` para a porta 465 e `true` para a porta 587. Isso independentemente dos valores `smtp.starttls` definidos na configuração do OSGI.