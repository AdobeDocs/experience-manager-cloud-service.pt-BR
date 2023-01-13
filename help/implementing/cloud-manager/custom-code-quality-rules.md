---
title: Regras de qualidade do código personalizado
description: Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do teste de qualidade do código. Elas são baseadas nas práticas recomendadas da engenharia da Adobe Experience Manager.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 2935338b847f7e852dfd31c93a61e737e8a3ec80
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 44%

---

# Regras de qualidade do código personalizado {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regras de qualidade do código personalizado"
>abstract="Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do teste de qualidade do código. Elas são baseadas nas práticas recomendadas da engenharia da Adobe Experience Manager."

Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do [teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md). Elas são baseadas nas práticas recomendadas da Experience Manager Engineering.

>[!NOTE]
>
>As amostras de código fornecidas aqui são apenas para fins ilustrativos. Consulte a [Documentação de conceitos](https://docs.sonarqube.org/latest/) do SonarQube para saber mais sobre os conceitos e as regras de qualidade do SonarQube.

## Regras SonarQube {#sonarqube-rules}

A seção a seguir especifica as regras do SonarQube executadas pelo Cloud Manager.

### Não utilize funções potencialmente perigosas {#do-not-use-potentially-dangerous-functions}

* **Chave**: CQRules:CWE-676
* **Tipo**: Vulnerabilidade
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Os métodos `Thread.stop()` e `Thread.interrupt()` O pode gerar problemas de difícil reprodução e, às vezes, vulnerabilidades de segurança. A utilização deve ser rigorosamente monitorizada e validada. Em geral, a transmissão de mensagens é uma forma mais segura de atingir objetivos semelhantes.

#### Código não compatível {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Código compatível {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### Não use strings de formato que possam ser controladas externamente {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Chave**: CQRules:CWE-134
* **Tipo**: Vulnerabilidade
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

O uso de uma string de formatação de uma fonte externa (como um parâmetro de solicitação ou conteúdo gerado pelo usuário) pode expor um aplicativo a ataques de negação de serviço. Há casos em que uma string de formatação pode ser controlada externamente, mas isso somente é permitido de fontes confiáveis.

#### Código não compatível {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### As solicitações HTTP devem sempre ter soquete e tempo limite de conexão {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Chave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.6.0

Ao executar solicitações HTTP de dentro de um aplicativo Experience Manager, é essencial garantir que os tempos limite adequados sejam configurados para evitar o consumo desnecessário de encadeamento. Infelizmente, o comportamento padrão do cliente HTTP padrão do Java™ (`java.net.HttpUrlConnection`) e o cliente Apache HTTP Components usado com frequência é o de nunca expirar, portanto, os tempos limite devem ser definidos explicitamente. Além disso, como prática recomendada, esses tempos limite não devem ultrapassar 60 segundos.

#### Código não compatível {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Código compatível {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Sempre fechar objetos ResourceResolver {#resourceresolver-objects-should-always-be-closed}

* **Chave**: CQRules:CQBP-72
* **Tipo**: Code Smell
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

`ResourceResolver` objetos obtidos do `ResourceResolverFactory` consomem recursos do sistema. Embora existam medidas em vigor para recuperar esses recursos quando um `ResourceResolver` não estiver mais em uso, é mais eficiente fechar explicitamente todos os objetos `ResourceResolver` abertos chamando o método `close()`.

Um equívoco relativamente comum é que `ResourceResolver` os objetos criados usando uma sessão JCR existente não devem ser explicitamente fechados ou que isso feche a sessão JCR subjacente. Não é isso o que ocorre. Independentemente de como um `ResourceResolver` foi aberto, ele deve ser fechado quando não estiver mais em uso. Como `ResourceResolver` implementa a interface `Closeable`, também é possível usar a sintaxe `try-with-resources` em vez de chamar explicitamente `close()`.

#### Código não compatível {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Código compatível {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Não use caminhos de servlet Sling para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Chave**: CQRules:CQBP-75
* **Tipo**: Code Smell
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Conforme descrito na [Documentação do Sling](https://sling.apache.org/documentation/the-sling-engine/servlets.html), não é recomendado vincular servlets por caminhos. Os servlets vinculados a caminhos não podem usar os controles de acesso JCR padrão e, como resultado disso, exigem maior rigor de segurança. Em vez de usar servlets vinculados a caminhos, é recomendado criar nós no repositório e registrar os servlets por tipo de recurso.

#### Código não compatível {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### As exceções capturadas devem ser registradas ou lançadas, não {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Chave**: CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Em geral, uma exceção deve ser registrada exatamente uma vez. O múltiplo registro de exceções pode causar confusão, pois não deixa claro quantas vezes uma exceção ocorreu. O padrão mais comum que leva a isso é o registro e o descarte de uma exceção capturada.

#### Código não compatível {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Código compatível {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Evite instruções de log imediatamente seguidas por uma instrução de lançamento {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Chave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Outro padrão comum a ser evitado é registrar uma mensagem e imediatamente depois lançar uma exceção. Essa prática geralmente indica que a mensagem de exceção acaba duplicada em arquivos de log.

#### Código não compatível {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Código compatível {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Evite fazer logon no INFO ao manipular solicitações de GET ou HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Chave**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Tipo**: Code Smell
* **Severidade**: Baixa

Em geral, o nível de log INFO deve ser usado para demarcar ações importantes e, por padrão, o Experience Manager está configurado para fazer logon no nível INFO ou superior. Os métodos GET e HEAD devem ser operações somente leitura e, portanto, não constituem ações importantes. Fazer logon no nível da INFO em resposta a solicitações de GET ou de HEAD provavelmente gera um ruído significativo de log, dificultando a identificação de informações úteis em arquivos de log. Ao manipular solicitações GET ou HEAD, o registro deverá estar nos níveis AVISO ou ERRO quando algo der errado ou nos níveis DEPURAÇÃO ou RASTREAMENTO, se informações mais detalhadas de solução de problemas forem necessárias.

>[!NOTE]
>
>Isso não se aplica a `access.log`-digite o log para cada solicitação.

#### Código não compatível {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Código compatível {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Não use Exception.getMessage() como o primeiro parâmetro de uma instrução de log {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Chave**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como prática recomendada, as mensagens de log devem fornecer informações contextuais sobre onde ocorreu uma exceção no aplicativo. Embora o contexto também possa ser determinado usando rastreamentos de pilha, em geral a mensagem de log será mais fácil de ler e entender. Como resultado disso, ao registrar uma exceção, não é uma prática recomendada usar a mensagem da exceção como a mensagem de registro. A mensagem de exceção contém o que deu errado, enquanto a mensagem de log deve ser usada para informar a um leitor de log o que o aplicativo estava fazendo quando a exceção aconteceu. A mensagem de exceção ainda está registrada. Ao especificar sua própria mensagem, os logs são mais fáceis de entender.

#### Código não compatível {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Código compatível {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### O logon em blocos de captura deve estar no nível AVISO ou ERRO {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Chave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como o nome sugere, as exceções do Java™ devem sempre ser usadas em circunstâncias excepcionais. Como resultado disso, quando uma exceção é capturada, é importante garantir que as mensagens de log sejam registradas no nível apropriado, seja WARN ou ERROR. Isso garante que elas sejam exibidas corretamente nos logs.

#### Código não compatível {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Código compatível {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Não imprimir rastreamentos de pilha no console {#do-not-print-stack-traces-to-the-console}

* **Chave**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como mencionado, o contexto é essencial para entender as mensagens de log. Usando `Exception.printStackTrace()` faz com que somente o rastreamento de pilha seja enviado para o fluxo de erro padrão, perdendo todo o contexto. Além disso, em um aplicativo de vários processos como o Experience Manager, se várias exceções forem impressas em paralelo usando esse método, seus rastreamentos de pilha poderão se sobrepor, o que gera uma confusão significativa. As exceções devem ser registradas somente por meio da estrutura de registro.

#### Código não compatível {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Código compatível {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Não saída para saída padrão ou erro padrão {#do-not-output-to-standard-output-or-standard-error}

* **Chave**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

O Experience Manager de logon deve ser sempre feito por meio da estrutura de log (SLF4J). A saída diretamente para a saída padrão ou fluxos de erro padrão perde as informações estruturais e contextuais fornecidas pela estrutura de registro. Às vezes, pode causar problemas de desempenho.

#### Código não compatível {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Código compatível {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Evite caminhos /apps e /libs codificados {#avoid-hardcoded-apps-and-libs-paths}

* **Chave**: CQRules:CQBP-71
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Em geral, caminhos que começam com `/libs` e `/apps` não devem ser codificados, pois se referem a caminhos que normalmente são armazenados como caminhos relativos ao caminho de pesquisa Sling, que está definido como `/libs,/apps` por padrão. O uso do caminho absoluto pode introduzir defeitos sutis que só apareceriam posteriormente no ciclo de vida do projeto.

#### Código não compatível {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Código compatível {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Não use o Sling scheduler {#sonarqube-sling-scheduler}

* **Chave**: CQRules:AMSCORE-554
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Não use o Sling Scheduler para tarefas que exigem uma execução garantida. Os trabalhos agendados no Sling têm execução garantida e são mais adequados para ambientes clusterizados e não clusterizados.

Consulte [Evento do Apache Sling e Manuseio de Trabalho](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) para saber mais sobre como os Sling Jobs são tratados em ambientes em cluster.

### Não use APIs obsoletas do Experience Manager {#sonarqube-aem-deprecated}

* **Chave**: AMSCORE-553
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A superfície da API do Experience Manager está sob revisão constante para identificar APIs para as quais o uso é desencorajado e, portanto, considerado obsoleto.

Geralmente, essas APIs são descontinuadas usando o Java™ padrão `@Deprecated` anotação e, como tal, como identificada por `squid:CallToDeprecatedMethod`.

No entanto, há casos em que uma API é descontinuada no contexto do Experience Manager, mas pode não ser descontinuada em outros contextos. Esta regra identifica essa segunda classe.


## Regras de conteúdo OakPAL {#oakpal-rules}

A seção a seguir especifica as verificações do OakPAL executadas pelo Cloud Manager.

>[!NOTE]
>
>O OakPAL é uma estrutura que valida pacotes de conteúdo usando um repositório Oak autônomo. Ele foi desenvolvido por um Experience Manager Partner e vencedor do prêmio Experience Manager Rockstar North America 2019.

### As APIs de produto anotadas com @ProviderType não devem ser implementadas ou estendidas por clientes {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Chave**: CQBP-84
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.7.0

A API do Experience Manager contém interfaces e classes do Java™ que devem ser usadas apenas — mas não implementadas — pelo código personalizado. Por exemplo, a interface `com.day.cq.wcm.api.Page` deve ser implementado somente por Experience Manager.

Quando novos métodos são adicionados a essas interfaces, esses métodos adicionais não afetam o código existente que usa essas interfaces. Como resultado, a adição de novos métodos a essas interfaces é considerada compatível com versões anteriores. No entanto, se o código personalizado implementa uma dessas interfaces, ele apresenta um risco de compatibilidade com versões anteriores para o cliente.

Interfaces e classes — conforme implementadas pelo Experience Manager — são anotadas com `org.osgi.annotation.versioning.ProviderType` ou, às vezes, uma anotação herdada semelhante `aQute.bnd.annotation.ProviderType`. Esta regra identifica os casos em que essa interface é implementada ou em que uma classe é estendida por código personalizado.

#### Código não compatível {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Os índices personalizados do Lucene Oak devem ter uma configuração Tika {#oakpal-indextikanode}

* **Chave**: IndexTikaNode
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.8.0

Vários índices prontos para uso do Experience Manager Oak incluem uma configuração Tika e as personalizações desses índices devem incluir uma configuração Tika. Essa regra verifica as personalizações de `damAssetLucene` `lucene` e `graphqlConfig` indexa e gera um problema se o nó `tika` estiver ausente ou se o nó `tika` não tiver um nó filho chamado `config.xml`.

Consulte a [documentação de indexação](/help/operations/indexing.md#preparing-the-new-index-definition) para obter mais informações sobre como personalizar as definições de índice.

#### Código não compatível {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### Código compatível {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Os índices personalizados do Lucene Oak não devem ser síncronos {#oakpal-indexasync}

* **Chave**: IndexAsyncProperty
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.8.0

Os índices Oak do tipo `lucene` sempre devem ser indexados de forma assíncrona. Caso contrário, poderá ocorrer instabilidade no sistema. Mais informações sobre a estrutura dos índices do Lucene podem ser encontradas no [Documentação do Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### Código não compatível {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

#### Código compatível {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Os índices personalizados do DAM Asset Lucene Oak são estruturados corretamente  {#oakpal-damAssetLucene-sanity-check}

* **Chave**: IndexDamAssetLucene
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.6.0

Para que a pesquisa de ativos funcione corretamente no Experience Manager Assets, as personalizações da variável `damAssetLucene` O índice Oak deve seguir um conjunto de diretrizes específicas a esse índice. Essa regra verifica se a definição do índice deve ter uma propriedade de vários valores chamada `tags`, que contém o valor `visualSimilaritySearch`.

#### Código não compatível {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      + tika
        + config.xml
```

#### Código compatível {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Os pacotes do cliente não devem criar ou modificar nós em /libs {#oakpal-customer-package}

* **Chave**: BannedPath
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2019.6.0

Há muito que a melhor prática é que `/libs` a árvore de conteúdo no repositório de conteúdo do Experience Manager deve ser considerada somente leitura pelos clientes. A modificação dos nós e propriedades em `/libs` cria riscos significativos para atualizações importantes e secundárias. Modificações em `/libs` devem ser realizadas por Adobe através de canais oficiais.

### Os pacotes não devem conter configurações OSGi duplicadas {#oakpal-package-osgi}

* **Chave**: DuplicateOsgiConfigurations
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Um problema comum que ocorre em projetos complexos é quando um mesmo componente OSGi é configurado várias vezes. Esse problema cria uma ambiguidade sobre qual configuração é aplicável. Essa regra é &quot;sensível ao modo de execução&quot; na medida em que identifica problemas em que o mesmo componente é configurado várias vezes no mesmo modo de execução ou combinação de modos de execução.

>[!NOTE]
>
>Essa regra gera problemas em que a mesma configuração, no mesmo caminho, é definida em vários pacotes, incluindo casos em que o mesmo pacote é duplicado na lista geral de pacotes incorporados.
>
>Por exemplo, se a build produzir pacotes nomeados `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all` em que `com.myco:com.myco.all` incorporar `com.myco:com.myco.ui.apps`, depois todas as configurações em `com.myco:com.myco.ui.apps` são relatadas como duplicatas.
>
>Em geral, esse é um caso em que não se deve seguir as [Diretrizes de estrutura de pacotes de conteúdo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Neste exemplo específico, o pacote `com.myco:com.myco.ui.apps` não inclui a propriedade `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Código não compatível {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Código compatível {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### As pastas de configuração e instalação devem conter apenas nós OSGi {#oakpal-config-install}

* **Chave**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Por motivos de segurança, caminhos que contêm `/config/` e `/install/` são legíveis apenas por usuários administrativos no Experience Manager e devem ser usadas apenas para configuração OSGi e pacotes OSGi. Colocar outros tipos de conteúdo em caminhos que contêm esses segmentos resultará em uma variação incontrolável e não intencional do comportamento do aplicativo entre usuários administrativos e não administrativos.

Um problema comum é o uso de nós chamados `config` nas caixas de diálogo de componente ou ao especificar a configuração do editor rich text para edição em linha. Para resolver esse problema, o nó incorreto deve ser renomeado para um nome compatível. Para a configuração do editor de rich text, use o `configPath` na `cq:inplaceEditing` para especificar o novo local.

#### Código não compatível {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Código compatível {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Os pacotes não devem sobrepor-se {#oakpal-no-overlap}

* **Chave**: PackageOverlaps
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Semelhante à regra [Pacotes não devem conter configurações OSGi duplicadas](#oakpal-package-osgi), esse é um problema comum em projetos complexos, em que o mesmo caminho de nó é gravado por vários pacotes de conteúdo separados. Embora seja possível usar as dependências do pacote de conteúdo para garantir um resultado consistente, é melhor evitar qualquer sobreposição.

### O modo de criação padrão não deve ser a interface clássica {#oakpal-default-authoring}

* **Chave**: ClassicUIAuthoringMode
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A configuração do OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` define o modo de criação padrão no Experience Manager. Porque [a interface do usuário clássica foi descontinuada desde o Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=pt-BR), um problema agora é levantado quando o modo de criação padrão é configurado para a interface do usuário clássica.

### Os componentes com caixas de diálogo devem ter caixas de diálogo da interface de toque {#oakpal-components-dialogs}

* **Chave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Os componentes do Experience Manager que têm uma caixa de diálogo da interface clássica devem sempre ter uma caixa de diálogo da interface de toque correspondente. Ambos fornecem uma experiência de criação ideal e são compatíveis com o modelo de implantação do Cloud Service, onde a interface do usuário clássica não é compatível. Essa regra verifica os seguintes cenários:

* Um componente com uma caixa de diálogo da interface do usuário clássica (ou seja, um nó secundário `dialog`) deve ter uma caixa de diálogo da interface do usuário de toque correspondente (ou seja, um nó secundário `cq:dialog`).
* Um componente com uma caixa de diálogo de design da interface do usuário clássica (ou seja, um nó `design_dialog`) deve ter uma caixa de diálogo de design da interface do usuário de toque correspondente (ou seja, um nó secundário `cq:design_dialog`).
* Um componente com uma caixa de diálogo da interface do usuário clássica e uma caixa de diálogo de design da interface do usuário clássica deve ter uma caixa de diálogo da interface do usuário sensível ao toque correspondente e uma caixa de diálogo de design da interface do usuário sensível ao toque correspondente.

A documentação das Ferramentas de Modernização do Experience Manager fornece documentação e ferramentas para converter componentes da interface clássica para a interface do usuário de toque. Consulte [a documentação das Ferramentas de Modernização do Experience Manager](https://opensource.adobe.com/aem-modernize-tools/) para obter mais detalhes.

### Os pacotes não devem misturar conteúdos mutáveis e imutáveis {#oakpal-packages-immutable}

* **Chave**: ImmutableMutableMixedPackage
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Para ser compatível com o modelo de implantação do Cloud Service, os pacotes de conteúdo individuais devem conter conteúdo para as áreas imutáveis do repositório (`/apps` e `/libs`) ou a área mutável (tudo não está em `/apps` ou `/libs`), mas não ambos. Por exemplo, um pacote que inclui ambos `/apps/myco/components/text` e `/etc/clientlibs/myco` não é compatível com o Cloud Service e faz com que um problema seja relatado.

>[!NOTE]
>
>A regra [Pacotes de clientes não devem criar ou modificar nós em /libs](#oakpal-customer-package) sempre se aplica.

Consulte [Estrutura do projeto Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md) para obter mais detalhes.

### Não use agentes de replicação inversa {#oakpal-reverse-replication}

* **Chave**: ReverseReplication
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

O suporte para replicação inversa não está disponível em implantações de Cloud Service, conforme descrito como parte do Experience Manager as a Cloud Service [notas de versão.](/help/release-notes/aem-cloud-changes.md#replication-agents)

Os clientes que usam replicação reversa devem entrar em contato com a Adobe para obter soluções alternativas.

### Os recursos contidos nas bibliotecas de clientes habilitadas por proxy devem estar em uma pasta chamada recursos {#oakpal-resources-proxy}

* **Chave**: ClientlibProxyResource
* **Tipo**: Erro
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

As bibliotecas de clientes do Experience Manager podem conter recursos estáticos, como imagens e fontes. Conforme descrito no documento [Uso de pré-processadores,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) ao usar bibliotecas de clientes por proxy, esses recursos estáticos devem estar contidos em uma pasta secundária chamada `resources` para serem efetivamente referenciados nas instâncias de publicação.

#### Código não compatível {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Código compatível {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Uso de processos de fluxo de trabalho incompatíveis com o Cloud Service {#oakpal-usage-cloud-service}

* **Chave**: CloudServiceIncompatibleWorkflowProcess
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2021.2.0

Com a mudança para microsserviços de ativos para processamento de ativos no Experience Manager as a Cloud Service, vários processos de fluxo de trabalho que foram usados nas versões local e AMS do Experience Manager se tornaram incompatíveis ou desnecessários.

A ferramenta de migração no [Repositório GitHub do Experience Manager as a Cloud Service Assets](https://github.com/adobe/aem-cloud-migration) O pode ser usado para atualizar modelos de fluxo de trabalho durante a migração para o Experience Manager as a Cloud Service.

### O uso de modelos estáticos é desincentivado em favor de modelos editáveis {#oakpal-static-template}

* **Chave**: StaticTemplateUsage
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Embora o uso de modelos estáticos seja historicamente comum em projetos do Experience Manager, o Adobe recomenda modelos editáveis porque eles fornecem mais flexibilidade e oferecem suporte a recursos adicionais não presentes em modelos estáticos. Mais informações podem ser encontradas no documento [Modelos de página.](/help/implementing/developing/components/templates.md)

A migração de modelos estáticos para editáveis pode ser amplamente automatizada usando o [Ferramentas de Modernização do Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### O uso de componentes de base herdados não é recomendado {#oakpal-usage-legacy}

* **Chave**: LegacyFoundationComponentUsage
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Os componentes básicos herdados (ou seja, os componentes em `/libs/foundation`) foram [obsoleto para várias versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=pt-BR) a favor dos componentes principais. O uso dos componentes básicos como base para os componentes personalizados (seja por sobreposição ou herança) não é recomendado e deve ser convertido para os componentes principais correspondentes.

Essa conversão pode ser facilitada pela [Ferramentas de Modernização do Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### Usar somente os nomes e a ordem do modo de execução suportados {#oakpal-supported-runmodes}

* **Chave**: SupportedRunmode
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service impõe uma política de nomeação estrita para nomes de modo de execução e uma ordem estrita para esses modos de execução. A lista de modos de execução suportados pode ser encontrada no documento [Implantação no Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) e qualquer desvio a isso é identificado como um problema.

### Os nós de definição do índice de pesquisa personalizado devem ser filhos diretos de /oak:index {#oakpal-custom-search}

* **Chave**: OakIndexLocation
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Experience Manager as a Cloud Service requer definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) ser nós filhos diretos de `/oak:index`. Os índices em outros locais devem ser movidos para serem compatíveis com o Experience Manager as a Cloud Service. Mais informações sobre índices de pesquisa podem ser encontradas no documento [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós de definição de índice de pesquisa personalizada devem ter um compatVersion de 2 {#oakpal-custom-search-compatVersion}

* **Chave**: IndexCompatVersion
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Experience Manager as a Cloud Service requer definições de índice de pesquisa personalizadas (como nós do tipo `oak:QueryIndexDefinition`) deve ter o `compatVersion` propriedade definida como `2`. Nenhum outro valor é suportado pelo Experience Manager as a Cloud Service. Mais informações sobre índices de pesquisa podem ser encontradas em [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós descendentes dos nós de definição de índice de pesquisa personalizados devem ser do tipo nt:unstructured {#oakpal-descendent-nodes}

* **Chave**: IndexDescendantNodeType
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Difícil de solucionar problemas pode ocorrer quando um nó de definição de índice de pesquisa personalizado tem nós filho não ordenados. Para evitar essa situação, é recomendável que todos os nós descendentes de um `oak:QueryIndexDefinition` nó ser do tipo `nt:unstructured`.

### Os nós de definição de índice de pesquisa personalizada devem conter um nó filho denominado indexRules que tenha filhos {#oakpal-custom-search-index}

* **Chave**: IndexRulesNode
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Um nó de definição de índice de pesquisa personalizada corretamente definido deve conter um nó secundário chamado `indexRules` que, por sua vez, deve ter pelo menos um secundário. Mais informações podem ser encontradas na [documentação do Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Os nós de definição de índice de pesquisa personalizada devem seguir as convenções de nomenclatura {#oakpal-custom-search-definitions}

* **Chave**: IndexName
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Experience Manager as a Cloud Service requer definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) deve ser nomeado de acordo com um padrão específico descrito no documento [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós de definição de índice de pesquisa personalizada devem usar o tipo de índice Lucene  {#oakpal-index-type-lucene}

* **Chave**: IndexType
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: Versão 2021.2.0 (tipo e severidade alterados em 2021.8.0)

Experience Manager as a Cloud Service requer definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) têm um `type` com o valor definido como `lucene`. A indexação usando tipos de índice herdados deve ser atualizada antes da migração para o Experience Manager as a Cloud Service. Consulte [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição de índice de pesquisa personalizada não devem conter uma propriedade chamada seed {#oakpal-property-name-seed}

* **Chave**: IndexSeedProperty
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service proíbe definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) de conter uma propriedade chamada `seed`. A indexação usando essa propriedade deve ser atualizada antes da migração para o Experience Manager as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição de índice de pesquisa personalizada não devem conter uma propriedade chamada reindex {#oakpal-reindex-property}

* **Chave**: IndexReindexProperty
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service proíbe definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) de conter uma propriedade chamada `reindex`. A indexação usando essa propriedade deve ser atualizada antes da migração para o Experience Manager as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.
