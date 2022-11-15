---
title: Regras de qualidade do código personalizado
description: Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do teste de qualidade do código. Elas se baseiam nas práticas recomendadas pela Engenharia do AEM.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: d7509556e4ae7a377498f2de2bae57f3557522ac
workflow-type: tm+mt
source-wordcount: '3493'
ht-degree: 100%

---

# Regras de qualidade do código personalizado {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regras de qualidade do código personalizado"
>abstract="Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do teste de qualidade do código. Elas se baseiam nas práticas recomendadas pela Engenharia do AEM."

Esta página descreve as regras personalizadas de qualidade do código executadas pelo Cloud Manager como parte do [teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md). Elas se baseiam nas práticas recomendadas pela Engenharia do AEM.

>[!NOTE]
>
>As amostras de código fornecidas aqui são apenas para fins ilustrativos. Consulte a [Documentação de conceitos](https://docs.sonarqube.org/7.4/user-guide/concepts/) do SonarQube para saber mais sobre os conceitos e as regras de qualidade do SonarQube.

## Regras do SonarQube {#sonarqube-rules}

A seção a seguir especifica as regras do SonarQube executadas pelo Cloud Manager.

### Não usar funções potencialmente perigosas {#do-not-use-potentially-dangerous-functions}

* **Chave**: CQRules:CWE-676
* **Tipo**: Vulnerabilidade
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Os métodos `Thread.stop()` e `Thread.interrupt()` podem gerar problemas de difícil reprodução e, em alguns casos, vulnerabilidades de segurança. A utilização deve ser rigorosamente monitorizada e validada. Em geral, a transmissão de mensagens é uma forma mais segura de atingir objetivos semelhantes.

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

### Não usar strings de formatação que possam ser controladas externamente {#do-not-use-format-strings-which-may-be-externally-controlled}

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

### As solicitações HTTP sempre devem ter soquete e tempo limite de conexão {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Chave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.6.0

Ao executar solicitações HTTP de dentro de um aplicativo do AEM, é importante garantir que os tempos limite adequados sejam configurados para evitar o consumo desnecessário de thread. Infelizmente, o comportamento padrão do cliente HTTP padrão do Java (`java.net.HttpUrlConnection`) e o cliente Apache HTTP Components mais usado é o de nunca atingir o tempo limite, portanto, os tempos limite devem ser definidos de forma explícita. Além disso, como prática recomendada, esses tempos limite não devem ultrapassar 60 segundos.

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

### Os objetos ResourceResolver sempre devem ser fechados {#resourceresolver-objects-should-always-be-closed}

* **Chave**: CQRules:CQBP-72
* **Tipo**: Code Smell
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

`ResourceResolver` objetos obtidos do `ResourceResolverFactory` consomem recursos do sistema. Embora existam medidas em vigor para recuperar esses recursos quando um `ResourceResolver` não estiver mais em uso, é mais eficiente fechar explicitamente todos os objetos `ResourceResolver` abertos chamando o método `close()`.

Um equívoco relativamente comum é que os objetos `ResourceResolver` criados usando uma sessão JCR existente não devem ser fechados explicitamente, ou que isso encerrará a sessão JCR subjacente. Não é isso o que ocorre. Independentemente de como um `ResourceResolver` foi aberto, ele deve ser fechado quando não estiver mais em uso. Como `ResourceResolver` implementa a interface `Closeable`, também é possível usar a sintaxe `try-with-resources` em vez de chamar explicitamente `close()`.

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

### Não usar caminhos Sling Servlet para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Chave**: CQRules:CQBP-75
* **Tipo**: Code Smell
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Conforme descrito na [Documentação do Sling](http://sling.apache.org/documentation/the-sling-engine/servlets.html), não é recomendado vincular servlets por caminhos. Os servlets vinculados a caminhos não podem usar os controles de acesso JCR padrão e, como resultado disso, exigem maior rigor de segurança. Em vez de usar servlets vinculados a caminhos, é recomendado criar nós no repositório e registrar os servlets por tipo de recurso.

#### Código não compatível {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### As exceções capturadas devem ser registradas ou descartadas, não ambos {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

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

### Evitar instruções de registro seguidas por instruções de descarte {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Chave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Outro padrão comum a ser evitado é registrar uma mensagem e imediatamente depois lançar uma exceção. Isso geralmente indica que a mensagem de exceção acabará duplicada nos arquivos de log.

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

### Evitar fazer registro em INFO ao manipular solicitações GET ou HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Chave**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Tipo**: Code Smell
* **Severidade**: Baixa

Em geral, o nível de log INFO deve ser usado para demarcar ações importantes e, por padrão, o AEM é configurado para fazer logon no nível INFO ou superior. Os métodos GET e HEAD devem ser operações somente leitura e, portanto, não constituem ações importantes. Fazer logon no nível INFO em resposta a solicitações GET ou HEAD costuma gerar um ruído significativo, dificultando a identificação de informações úteis nos arquivos de log. Ao manipular solicitações GET ou HEAD, o registro deverá estar nos níveis AVISO ou ERRO quando algo der errado ou nos níveis DEPURAÇÃO ou RASTREAMENTO, se informações mais detalhadas de solução de problemas forem necessárias.

>[!NOTE]
>
>Isso não se aplica ao registro do tipo `access.log` para cada solicitação.

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

### Não usar Exception.getMessage() como o primeiro parâmetro de uma instrução de registro {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Chave**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como prática recomendada, as mensagens de log devem fornecer informações contextuais sobre onde ocorreu uma exceção no aplicativo. Embora o contexto também possa ser determinado por meio do uso de rastreamentos de pilha, a mensagem de log costuma ser mais fácil de ler e entender. Como resultado disso, ao registrar uma exceção, não é uma prática recomendada usar a mensagem da exceção como a mensagem de registro. A mensagem de exceção conterá o que deu errado, enquanto que a mensagem de registro deverá ser usada para informar a um leitor de registros o que o aplicativo estava fazendo quando a exceção ocorreu. A mensagem de exceção ainda será registrada. Ao especificar sua própria mensagem, será mais fácil entender os logs.

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

### O registro em blocos de captura deve estar no nível AVISO ou ERRO {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Chave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como o nome sugere, as exceções de Java sempre devem ser usadas em casos excepcionais. Como resultado disso, quando uma exceção é capturada, é importante garantir que as mensagens de log sejam registradas no nível apropriado, seja WARN ou ERROR. Isso garante que elas sejam exibidas corretamente nos logs.

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

Como mencionado, o contexto é essencial para entender as mensagens de log. O uso de `Exception.printStackTrace()` faz com que somente o rastreamento de pilha seja enviado para o fluxo de erro padrão, perdendo todo o contexto. Além disso, em um aplicativo com muitos segmentos como o AEM, se várias exceções forem impressas em paralelo usando esse método, seus rastreamentos de pilha poderão se sobrepor, gerando confusão significativa. As exceções devem ser registradas somente por meio da estrutura de registro.

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

### Não gerar saída para saída padrão ou erro padrão {#do-not-output-to-standard-output-or-standard-error}

* **Chave**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Os registros no AEM sempre devem ser feitos por meio da estrutura de registro (SLF4J). Ao enviar diretamente para a saída padrão ou para fluxos de erro padrão, as informações estruturais e contextuais fornecidas pela estrutura de registro eram perdidas e podiam, em alguns casos, causar problemas de desempenho.

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

### Evitar caminhos /apps e /libs codificados {#avoid-hardcoded-apps-and-libs-paths}

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

### O Sling Scheduler não deve ser usado {#sonarqube-sling-scheduler}

* **Chave**: CQRules:AMSCORE-554
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

O Sling Scheduler não deve ser usado para tarefas que exigem execução garantida. Os trabalhos agendados no Sling têm execução garantida e são mais adequados para ambientes clusterizados e não clusterizados.

Consulte o [Evento do Apache Sling e manuseio de trabalhos](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) para saber mais sobre como os trabalhos do Sling são tratados em ambientes em cluster.

### APIs obsoletas do AEM não devem ser usadas {#sonarqube-aem-deprecated}

* **Chave**: AMSCORE-553
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

As APIs do AEM estão em constante revisão para identificar quais não devem mais ser usadas e, portanto, consideradas descontinuadas.

Em muitos casos, essas APIs são descontinuadas usando a anotação Java padrão `@Deprecated` e, como tal, conforme identificado por `squid:CallToDeprecatedMethod`.

No entanto, há casos em que uma API é preterida no contexto do AEM, mas pode não ser em outros contextos. Esta regra identifica essa segunda classe.


## Regras de conteúdo OakPAL {#oakpal-rules}

A seção a seguir especifica as verificações do OakPAL executadas pelo Cloud Manager.

>[!NOTE]
>
>O OakPAL é uma estrutura que valida pacotes de conteúdo usando um repositório Oak autônomo. Ele foi desenvolvido por um parceiro do AEM e vencedor do prêmio AEM Rockstar North America 2019.

### As APIs de produto anotadas com @ProviderType não devem ser implementadas ou estendidas pelos clientes {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Chave**: CQBP-84
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.7.0

A API do AEM contém interfaces e classes do Java que devem ser usadas, mas não implementadas, apenas pelo código personalizado. Por exemplo, a interface `com.day.cq.wcm.api.Page` foi projetada para ser implementada somente pelo AEM.

Quando novos métodos são adicionados a essas interfaces, esses métodos adicionais não afetam o código existente que usa essas interfaces e, como resultado, a adição de novos métodos a essas interfaces é considerada compatível com versões anteriores. No entanto, se o código personalizado implementa uma dessas interfaces, ele apresenta um risco de compatibilidade com versões anteriores para o cliente.

As interfaces e classes que somente devem ser implementadas pelo AEM estão marcadas com `org.osgi.annotation.versioning.ProviderType` ou, em alguns casos, com uma anotação herdada semelhante `aQute.bnd.annotation.ProviderType`. Esta regra identifica os casos em que essa interface é implementada ou em que uma classe é estendida por código personalizado.

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

Vários índices Oak do AEM prontos para uso incluem uma configuração tika e as personalizações desses índices devem incluir uma configuração tika. Essa regra verifica as personalizações de `damAssetLucene` `lucene` e `graphqlConfig` indexa e gera um problema se o nó `tika` estiver ausente ou se o nó `tika` não tiver um nó filho chamado `config.xml`.

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

Os índices Oak do tipo `lucene` sempre devem ser indexados de forma assíncrona. Caso contrário, poderá ocorrer instabilidade no sistema. Mais informações sobre a estrutura dos índices Lucene podem ser encontradas na [documentação do Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

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

### Os índices DAM Asset Lucene Oak estão adequadamente estruturados  {#oakpal-damAssetLucene-sanity-check}

* **Chave**: IndexDamAssetLucene
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.6.0

Para que a pesquisa de ativos funcione corretamente no AEM Assets, as personalizações do índice Oak `damAssetLucene` devem seguir um conjunto de diretrizes específicas desse índice. Essa regra verifica se a definição do índice deve ter uma propriedade de vários valores chamada `tags`, que contém o valor `visualSimilaritySearch`.

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

### Pacotes de clientes não devem criar ou modificar nós em /libs {#oakpal-customer-package}

* **Chave**: BannedPath
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2019.6.0

Uma prática recomendada já consolidada é que a árvore de conteúdo `/libs` no repositório de conteúdo do AEM deve ser considerada somente leitura pelos clientes. A modificação dos nós e propriedades em `/libs` cria riscos significativos para atualizações importantes e secundárias. As modificações em `/libs` somente devem ser realizadas pela Adobe por meio de canais oficiais.

### Pacotes não devem conter configurações OSGi duplicadas {#oakpal-package-osgi}

* **Chave**: DuplicateOsgiConfigurations
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Um problema comum que ocorre em projetos complexos é quando um mesmo componente OSGi é configurado várias vezes. Isso cria ambiguidade sobre qual configuração deve ser aplicada. Essa regra é “sensível ao modo de execução”, pois somente identificará problemas em que o mesmo componente é configurado várias vezes no mesmo modo de execução ou combinação de modos de execução.

>[!NOTE]
>
>Essa regra gerará problemas em que uma mesma configuração, em um mesmo caminho, será definida em vários pacotes, incluindo casos em que um mesmo pacote será duplicado na lista geral de pacotes incorporados.
>
>Por exemplo, se a compilação produzir pacotes chamados `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all`, em que `com.myco:com.myco.all` incorpora `com.myco:com.myco.ui.apps`, então todas as configurações em `com.myco:com.myco.ui.apps` serão relatadas como duplicadas.
>
>Em geral, esse é um caso em que não se deve seguir as [Diretrizes de estrutura de pacotes de conteúdo.](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Neste exemplo específico, o pacote `com.myco:com.myco.ui.apps` não inclui a propriedade `<cloudManagerTarget>none</cloudManagerTarget>`.

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

Por motivos de segurança, caminhos que contêm `/config/` e `/install/` somente podem ser lidos por usuários administrativos no AEM e devem ser usados apenas para a configuração do OSGi e os pacotes do OSGi. Colocar outros tipos de conteúdo em caminhos que contêm esses segmentos resultará em uma variação incontrolável e não intencional do comportamento do aplicativo entre usuários administrativos e não administrativos.

Um problema comum é o uso de nós chamados `config` nas caixas de diálogo de componente ou ao especificar a configuração do editor rich text para edição em linha. Para resolver isso, o nó incorreto deve ser renomeado com um nome que esteja em conformidade. Para a configuração do editor rich text, use a propriedade `configPath` no nó `cq:inplaceEditing` para especificar o novo local.

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

### Os pacotes não devem se sobrepor {#oakpal-no-overlap}

* **Chave**: PackageOverlaps
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Semelhante à regra [Pacotes não devem conter configurações OSGi duplicadas](#oakpal-package-osgi), esse é um problema comum em projetos complexos, em que o mesmo caminho de nó é gravado por vários pacotes de conteúdo separados. Embora seja possível usar as dependências do pacote de conteúdo para garantir um resultado consistente, é melhor evitar qualquer sobreposição.

### O modo de autoria padrão não deve ser a interface do usuário clássica {#oakpal-default-authoring}

* **Chave**: ClassicUIAuthoringMode
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A configuração do OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` define o modo de autoria padrão no AEM. Como a [interface do usuário clássica foi descontinuada no AEM 6.4,](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=pt-BR) um problema será gerado quando o modo de criação padrão estiver configurado para usá-la.

### Os componentes com caixas de diálogo devem ter caixas de diálogo da interface do usuário sensíveis ao toque {#oakpal-components-dialogs}

* **Chave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Os componentes do AEM que têm caixas de diálogo da interface do usuário clássica sempre devem ter uma caixa de diálogo da interface do usuário sensível ao toque correspondente para fornecer uma experiência de autoria ideal e para serem compatíveis com o modelo de implantação do Cloud Service, que não inclui suporte à interface do usuário clássica. Essa regra verifica os seguintes cenários:

* Um componente com uma caixa de diálogo da interface do usuário clássica (ou seja, um nó secundário `dialog`) deve ter uma caixa de diálogo da interface do usuário de toque correspondente (ou seja, um nó secundário `cq:dialog`).
* Um componente com uma caixa de diálogo de design da interface do usuário clássica (ou seja, um nó `design_dialog`) deve ter uma caixa de diálogo de design da interface do usuário de toque correspondente (ou seja, um nó secundário `cq:design_dialog`).
* Um componente com uma caixa de diálogo da interface do usuário clássica e uma caixa de diálogo de design da interface do usuário clássica deve ter uma caixa de diálogo da interface do usuário sensível ao toque correspondente e uma caixa de diálogo de design da interface do usuário sensível ao toque correspondente.

A documentação das Ferramentas de Modernização do AEM fornece documentação e ferramentas para converter componentes da interface do usuário clássica para a interface do usuário sensível ao toque. Consulte [a documentação das Ferramentas de modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/) para obter mais detalhes.

### Pacotes não devem misturar conteúdo mutável e imutável {#oakpal-packages-immutable}

* **Chave**: ImmutableMutableMixedPackage
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Para serem compatíveis com o modelo de implantação do Cloud Service, os pacotes de conteúdo individuais devem incluir conteúdo para as áreas imutáveis do repositório (ou seja, `/apps` e `/libs`) ou para a área mutável (ou seja, tudo que não está em `/apps` ou em `/libs`), mas não ambas. Por exemplo, um pacote que inclui `/apps/myco/components/text and /etc/clientlibs/myco` não é compatível com o Cloud Service e resultará em um erro.

>[!NOTE]
>
>A regra [Pacotes de clientes não devem criar ou modificar nós em /libs](#oakpal-customer-package) sempre se aplica.

Consulte [Estrutura de projetos AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md) para obter mais detalhes.

### Agentes de replicação reversa não devem ser usados {#oakpal-reverse-replication}

* **Chave**: ReverseReplication
* **Tipo**: Compatibilidade entre Smell/Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

O suporte à replicação reversa não está disponível em implantações de Cloud Service, conforme descrito nas [notas de versão do AEM as a Cloud Service.](/help/release-notes/aem-cloud-changes.md#replication-agents)

Os clientes que usam replicação reversa devem entrar em contato com a Adobe para obter soluções alternativas.

### Os recursos contidos nas bibliotecas de clientes habilitadas por proxy devem estar em uma pasta denominada Recursos {#oakpal-resources-proxy}

* **Chave**: ClientlibProxyResource
* **Tipo**: Erro
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

As bibliotecas de clientes do AEM podem conter recursos estáticos, como imagens e fontes. Conforme descrito no documento [Uso de pré-processadores,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) ao usar bibliotecas de clientes por proxy, esses recursos estáticos devem estar contidos em uma pasta secundária chamada `resources` para serem efetivamente referenciados nas instâncias de publicação.

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

Com a mudança para os microsserviços de ativos para o processamento de ativos no AEM as a Cloud Service, vários processos de fluxo de trabalho que foram usados nas versões local e AMS do AEM se tornaram incompatíveis ou desnecessários.

A ferramenta de migração no [repositório GitHub do AEM Assets as a Cloud Service](https://github.com/adobe/aem-cloud-migration) pode ser usada para atualizar modelos de fluxo de trabalho durante a migração para o AEM as a Cloud Service.

### O uso de modelos estáticos não é recomendado em prol dos modelos editáveis {#oakpal-static-template}

* **Chave**: StaticTemplateUsage
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Embora o uso de modelos estáticos tenha sido historicamente muito comum em projetos AEM, os modelos editáveis são altamente recomendados, pois fornecem mais flexibilidade e suporte a recursos adicionais que não estão presentes nos modelos estáticos. Mais informações podem ser encontradas no documento [Modelos de página.](/help/implementing/developing/components/templates.md)

A migração de modelos estáticos para editáveis pode ser amplamente automatizada usando as [Ferramentas de modernização do AEM.](https://opensource.adobe.com/aem-modernize-tools/)

### O uso de componentes básicos herdados não é recomendado {#oakpal-usage-legacy}

* **Chave**: LegacyFoundationComponentUsage
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Os componentes básicos herdados (ou seja, os componentes em `/libs/foundation`) foram [descontinuados em várias versões do AEM](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) em prol dos componentes principais. O uso dos componentes básicos como base para os componentes personalizados (seja por sobreposição ou herança) não é recomendado e deve ser convertido para os componentes principais correspondentes.

Essa conversão pode ser facilitada pelas [Ferramentas de modernização do AEM.](https://opensource.adobe.com/aem-modernize-tools/)

### Somente nomes e classificações do modo de execução suportados devem ser usados {#oakpal-supported-runmodes}

* **Chave**: SupportedRunmode
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service impõe uma política de nomenclatura estrita para nomes de modos de execução e uma ordem estrita para esses modos de execução. A lista de modos de execução suportados pode ser encontrada no documento [Implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) e qualquer desvio em relação a isso será identificado como um problema.

### Os nós de definição do índice de pesquisa personalizado devem ser nós secundários diretos de /oak:index {#oakpal-custom-search}

* **Chave**: OakIndexLocation
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) sejam nós secundários diretos de `/oak:index`. Os índices em outros locais devem ser movidos para serem compatíveis com o AEM as a Cloud Service. Mais informações sobre índices de pesquisa podem ser encontradas no documento [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós de definição do índice de pesquisa personalizado devem ter compatVersion igual a 2 {#oakpal-custom-search-compatVersion}

* **Chave**: IndexCompatVersion
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) tenham a prioridade `compatVersion` definida como `2`. Nenhum outro valor é suportado pelo AEM as a Cloud Service. Mais informações sobre índices de pesquisa podem ser encontradas em [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós descendentes dos nós de definição do índice de pesquisa personalizado devem ser do tipo nt:unstructured {#oakpal-descendent-nodes}

* **Chave**: IndexDescendantNodeType
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Problemas difíceis de solucionar podem ocorrer quando um nó de definição do índice de pesquisa personalizado inclui nós secundários desordenados. Para evitar essa situação, é recomendado que todos os nós descendentes de um nó `oak:QueryIndexDefinition` sejam do tipo `nt:unstructured`.

### Os nós de definição do índice de pesquisa personalizado devem conter um nó secundário chamado indexRules que tenha nós secundários {#oakpal-custom-search-index}

* **Chave**: IndexRulesNode
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Um nó de definição do índice de pesquisa personalizado definido corretamente deve conter um nó secundário chamado `indexRules` que, por sua vez, deve conter pelo menos um nó secundário. Mais informações podem ser encontradas na [Documentação do Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Os nós de definição do índice de pesquisa personalizado devem seguir as convenções de nomenclatura {#oakpal-custom-search-definitions}

* **Chave**: IndexName
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) sejam nomeadas de acordo com um padrão específico descrito no documento [Pesquisa e indexação de conteúdo.](/help/operations/indexing.md)

### Os nós de definição do índice de pesquisa personalizado devem usar o tipo de índice lucene  {#oakpal-index-type-lucene}

* **Chave**: IndexType
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: Versão 2021.2.0 (tipo e severidade alterados em 2021.8.0)

O AEM as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) tenham uma propriedade `type` com valor definido como `lucene`. A indexação usando tipos de índice herdados deve ser atualizada antes da migração para o AEM as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição do índice de pesquisa personalizado não devem conter uma propriedade chamada seed {#oakpal-property-name-seed}

* **Chave**: IndexSeedProperty
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service proíbe que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) contenham uma propriedade chamada `seed`. A indexação usando esse tipo de propriedade deve ser atualizada antes da migração para o AEM as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição do índice de pesquisa personalizado não devem conter uma propriedade chamada reindex {#oakpal-reindex-property}

* **Chave**: IndexReindexProperty
* **Tipo**: Code Smell
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O AEM as a Cloud Service proíbe que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) contenham uma propriedade chamada `reindex`. A indexação usando esse tipo de propriedade deve ser atualizada antes da migração para o AEM as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.
