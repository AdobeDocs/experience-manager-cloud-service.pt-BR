---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: Diretrizes de desenvolvimento do AEM as a Cloud Service
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '2375'
ht-degree: 1%

---

# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

O código em execução AEM as a Cloud Service deve estar ciente do fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida em qualquer momento.

Durante a atualização do AEM as a Cloud Service, haverá instâncias com o código antigo e o novo sendo executado simultaneamente. Portanto, o código antigo não deve ser quebrado com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se houver a necessidade de identificar o principal no cluster, a API Apache Sling Discovery poderá ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas persistido no repositório. Caso contrário, esse estado poderá ser perdido se uma instância for interrompida.

## Estado do sistema de arquivos {#state-on-the-filesystem}

O sistema de arquivos da instância não deve ser usado AEM as a Cloud Service. O disco é efêmero e será descartado quando as instâncias forem recicladas. A utilização limitada do sistema de arquivos para armazenamento temporário relacionado ao processamento de pedidos únicos é possível, mas não deve ser utilizada abusivamente para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso de recursos e encontrar limitações de disco.

Como exemplo, onde o uso do sistema de arquivos não é compatível, a camada Publicar deve garantir que todos os dados que precisam ser persistentes sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Da mesma forma, com tudo o que está acontecendo de forma assíncrona como atuar em eventos de observação, não se pode garantir que seja executado localmente e, portanto, deve ser usado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recurso Sling. No momento em que uma alteração ocorre, a instância pode ser removida e substituída por uma instância diferente. Outras instâncias na topologia que estão ativas nesse momento poderão reagir a esse evento. No entanto, neste caso, não se trata de um evento local e pode até não haver um líder ativo no caso de uma eleição de líder em curso, quando o evento é emitido.

## Tarefas em Segundo Plano e Trabalhos de Longa Execução {#background-tasks-and-long-running-jobs}

O código executado como uma tarefa em segundo plano deve supor que a instância em execução pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e a maioria das importações deve ser retomada. Isso significa que, se o código for executado novamente, ele não deverá começar do início novamente, mas antes próximo de onde parou. Embora esse não seja um novo requisito para esse tipo de código, em AEM as a Cloud Service é mais provável que ocorra uma interrupção da instância.

Para minimizar os problemas, os empregos de longa duração devem ser evitados, se possível, e devem ser retomadas no mínimo. Para executar esses trabalhos, use os Trabalhos do Sling, que têm uma garantia pelo menos uma vez e, portanto, se forem interrompidos, serão executados novamente o mais rápido possível. Mas, provavelmente, não deveriam recomeçar desde o início. Para agendar essas tarefas, é melhor usar o agendador [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) assim que isso for novamente a execução pelo menos uma vez.

O Sling Commons Scheduler não deve ser usado para agendamento, pois a execução não pode ser garantida. É muito mais provável que seja agendado.

Da mesma forma, com tudo o que está acontecendo de forma assíncrona, como agir em eventos de observação (sejam eventos JCR ou eventos de recurso Sling), não pode ser garantido que seja executado e, portanto, deve ser usado com cuidado. Isso já é verdadeiro para implantações AEM no presente.

## Conexões HTTP de saída {#outgoing-http-connections}

É altamente recomendável que todas as conexões HTTP de saída definam conexões razoáveis e tempos limite de leitura. Para código que não aplica esses tempos limite, as instâncias AEM executadas em AEM as a Cloud Service impõem um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões usadas pelas seguintes bibliotecas Java populares:

O Adobe recomenda o uso da biblioteca [Apache HttpComponents Client 4.x ](https://hc.apache.org/httpcomponents-client-ga/) fornecida para fazer conexões HTTP.

As alternativas que são conhecidas por funcionar, mas que podem exigir que você mesmo forneça a dependência, são:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/or  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html)  (Fornecido por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (não recomendado, pois está desatualizado e substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/)  (Não fornecido pelo AEM)

## Nenhuma personalização da interface clássica {#no-classic-ui-customizations}

AEM as a Cloud Service suporta apenas a interface do usuário de toque para código de cliente de terceiros. A interface do usuário clássica não está disponível para personalização.

## Evitar binários Nativos {#avoid-native-binaries}

O código não poderá baixar binários no tempo de execução nem modificá-los. Por exemplo, ele não poderá descompactar os arquivos `jar` ou `tar`.

## Nenhum binário de transmissão por meio AEM as a Cloud Service {#no-streaming-binaries}

Os binários devem ser acessados por meio da CDN, que fornecerá binários fora dos principais serviços de AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, o que aciona o download de um binário no disco efêmero do serviço de AEM.

## Sem agentes de replicação inversa {#no-reverse-replication-agents}

A replicação inversa de Publicar para autor não é compatível com AEM as a Cloud Service. Se tal estratégia for necessária, você poderá usar um armazenamento de persistência externo compartilhado entre o farm de instâncias de Publicação e, potencialmente, o cluster Autor.

## Os agentes de replicação de encaminhamento podem precisar ser transferidos {#forward-replication-agents}

O conteúdo é replicado de Autor para Publicação por meio de um mecanismo de sub-rede. Não há suporte para agentes de replicação personalizados.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de logs são gravadas em arquivos locais na pasta `/crx-quickstart/logs` .

Em ambientes do Cloud, os desenvolvedores podem baixar logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Definir o nível de log**

Para alterar os níveis de log de ambientes do Cloud, a configuração OSGI do Sling Logging deve ser modificada, seguida por uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar logs detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e depois enviá-las para uma instância AEM as a Cloud Service. Para obter mais informações sobre como fazer isso, consulte [Implantação para AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Ativando o Nível de Log DEBUG**

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas.
Para ativar o nível de log DEBUG, defina a variável

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

propriedade a ser depurada. Não deixe o log no nível de log DEBUG por mais tempo do que o necessário, pois ele gera muitos logs.
Uma linha no arquivo de depuração geralmente começa com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | A ação falhou. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Info | A ação foi bem sucedida. |

### Despejos de encadeamento {#thread-dumps}

Os despejos de encadeamento em ambientes do Cloud são coletados continuamente, mas não podem ser baixados de maneira automatizada no momento. Enquanto isso, entre em contato com AEM suporte se os despejos de encadeamento forem necessários para depurar um problema, especificando a janela de tempo exata.

## CRX/DE Lite e Console do desenvolvedor {#crxde-lite-and-developer-console}

### Desenvolvimento local {#local-development}

Para desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e ao Console da Web AEM (`/system/console`).

Observe que, no desenvolvimento local (usando o SDK), `/apps` e `/libs` podem ser gravadas diretamente, o que é diferente dos ambientes do Cloud, onde essas pastas de nível superior são imutáveis.

### AEM ferramentas de desenvolvimento as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar o CRXDE lite no ambiente de desenvolvimento do nível de criação, mas não no ambiente de preparo ou produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Um conjunto de ferramentas para depurar AEM ambientes de desenvolvedor as a Cloud Service está disponível no Console do desenvolvedor para ambientes de desenvolvimento, preparo e produção. O url pode ser determinado ajustando os urls do serviço de Autor ou Publicação da seguinte maneira:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Cloud Manager pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Conforme ilustrado abaixo, as informações de status disponíveis incluem o estado de pacotes, componentes, configurações OSGI, índices de oak, serviços OSGI e tarefas Sling.

![Console de desenvolvimento 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Conforme ilustrado abaixo, os desenvolvedores podem resolver dependências de pacote e servlets:

![Console de desenvolvimento 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de desenvolvimento 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explicar Consulta:

![Console de desenvolvimento 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas de Produção, o acesso ao Console do Desenvolvedor é definido pela &quot;Função do Desenvolvedor - Cloud Manager&quot; no Admin Console, enquanto para programas de sandbox, o Console do Desenvolvedor está disponível para qualquer usuário com um perfil de produto que dá acesso a AEM as a Cloud Service. Para todos os programas, &quot;Cloud Manager - Função do desenvolvedor&quot; é necessário para despejos de status e os usuários também devem ser definidos no Perfil de produto Usuários AEM ou Administradores AEM nos serviços de criação e publicação, para visualizar os dados de despejo de status de ambos os serviços. Para obter mais informações sobre como configurar permissões de usuário, consulte [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Serviço de preparo e produção de AEM {#aem-staging-and-production-service}

Os clientes não terão acesso às ferramentas do desenvolvedor para ambientes de preparo e produção.

### Monitoramento de desempenho {#performance-monitoring}

O Adobe monitora o desempenho do aplicativo e toma medidas para corrigir se a deterioração é observada. No momento, as métricas do aplicativo não podem ser observadas.

## Endereço IP de saída dedicado {#dedicated-egress-ip-address}

Mediante solicitação, AEM as a Cloud Service fornecerá um endereço IP estático e dedicado para HTTP (porta 80) e HTTPS (porta 443) tráfego externo programado no código Java.

### Benefícios {#benefits}

Esse endereço IP dedicado pode melhorar a segurança ao integrar fornecedores SaaS (como um fornecedor de CRM) ou outras integrações fora AEM as a Cloud Service que oferecem uma lista de permissões de endereços IP. Ao adicionar o endereço IP dedicado à  de lista de permissões, isso garante que somente o tráfego da AEM Cloud Service do cliente poderá fluir para o serviço externo. Além do tráfego de qualquer outro IP permitido.

Sem o recurso de endereço IP dedicado habilitado, o tráfego proveniente AEM fluxos as a Cloud Service por meio de um conjunto de IPs compartilhados com outros clientes.

### Configuração {#configuration}

Para ativar um endereço IP dedicado, envie uma solicitação ao Suporte ao cliente, que fornecerá as informações do endereço IP. A solicitação deve especificar cada ambiente e solicitações adicionais devem ser feitas se novos ambientes precisarem do recurso após a solicitação inicial. Os ambientes de programa de sandbox não são compatíveis.

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
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) ou use
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

Somente as portas HTTP e HTTPS são compatíveis. Isso inclui HTTP/1.1, bem como HTTP/2 quando criptografado.

### Considerações sobre depuração {#debugging-considerations}

Para validar se o tráfego está de saída no endereço IP dedicado esperado, verifique os logs no serviço de destino, se disponível. Caso contrário, pode ser útil chamar um serviço de depuração como [https://ifconfig.me/ip](https://ifconfig.me/ip), que retornará o endereço IP de chamada.

## Envio de email {#sending-email}

AEM as a Cloud Service requer que o email de saída seja criptografado. As seções abaixo descrevem como solicitar, configurar e enviar emails.

>[!NOTE]
>
>O serviço de email pode ser configurado com suporte a OAuth2. Para obter mais informações, consulte [Suporte OAuth2 para o serviço de email](/help/security/oauth2-support-for-mail-service.md).

### Solicitar acesso {#requesting-access}

Por padrão, o email de saída é desativado. Para ativá-lo, envie um tíquete de suporte com:

1. O nome de domínio totalmente qualificado para o servidor de email (por exemplo `smtp.sendgrid.net`)
1. A porta a ser usada. Ela deve ser a porta 465 se for suportada pelo servidor de e-mail; caso contrário, a porta 587. Observe que a porta 587 só poderá ser usada se o servidor de email exigir e aplicar o TLS nessa porta
1. A ID do programa e a ID do ambiente para os ambientes dos quais eles gostariam de enviar emails
1. Se o acesso SMTP é necessário para criar, publicar ou ambos.

### Envio de emails {#sending-emails}

O [Day CQ Mail Service OSGI service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) deve ser usado e os emails devem ser enviados ao servidor de email indicado na solicitação de suporte, em vez de diretamente aos recipients.

AEM CS requer que o correio seja enviado através da porta 465. Se um servidor de email não suportar a porta 465, a porta 587 poderá ser usada, desde que a opção TLS esteja habilitada.

>[!NOTE]
>
>Observe que o Adobe não suporta egresso SMTP sobre um endereço IP dedicado exclusivo.

### Configuração {#email-configuration}

Os emails no AEM devem ser enviados usando o [Day CQ Mail Service OSGi service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte a documentação do [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obter detalhes sobre a configuração das configurações de email. Para AEM as a Cloud Service, os seguintes ajustes devem ser feitos no serviço `com.day.cq.mailer.DefaultMailService OSGI`:

Se a porta 465 tiver sido solicitada:

* defina `smtp.port` para `465`
* defina `smtp.ssl` para `true`

Se a porta 587 tiver sido solicitada (somente permitida se o servidor de e-mail não suportar a porta 465):

* defina `smtp.port` para `587`
* defina `smtp.ssl` para `false`

A propriedade `smtp.starttls` será automaticamente definida por AEM as a Cloud Service em tempo de execução para um valor apropriado. Portanto, se `smtp.tls` estiver definido como true, `smtp.startls` será ignorado. Se `smtp.ssl` for definido como falso, `smtp.starttls` será definido como verdadeiro. Isso ocorre independentemente dos valores `smtp.starttls` definidos na configuração OSGI.

## [!DNL Assets] diretrizes de desenvolvimento e casos de uso {#use-cases-assets}

Para saber mais sobre casos de uso de desenvolvimento, recomendações e materiais de referência do Assets as a Cloud Service, consulte [Referência do desenvolvedor do Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
