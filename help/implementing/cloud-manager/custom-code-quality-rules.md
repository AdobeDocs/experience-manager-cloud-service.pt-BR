---
title: Regras de qualidade do código personalizado
description: Saiba mais sobre as regras de qualidade de código personalizadas do Cloud Manager, com base nas práticas recomendadas de engenharia do Adobe Experience Manager, para garantir um código de alta qualidade por meio de testes completos.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '4349'
ht-degree: 64%

---

# Regras de qualidade do código personalizado {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regras de qualidade do código personalizado"
>abstract="Saiba mais sobre as regras de qualidade de código personalizadas do Cloud Manager, com base nas práticas recomendadas de engenharia do Adobe Experience Manager, para garantir um código de alta qualidade por meio de testes completos."

Saiba mais sobre as regras personalizadas de qualidade do código da Cloud Manager, com base nas práticas recomendadas da engenharia da Adobe Experience Manager, para garantir código de alta qualidade por meio de testes completos. Consulte também [teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md).

As regras completas do SonarQube não estão disponíveis para download devido às informações proprietárias da Adobe. Você pode baixar a lista completa de *regras atuais* [usando este link](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx). Continue a ler este documento para obter descrições e exemplos das regras.

>[!IMPORTANT]
>
>A partir de quinta-feira, 13 de fevereiro de 2025 (Cloud Manager 2025.2.0), a qualidade de código do Cloud Manager usará uma versão atualizada do SonarQube 9.9 e uma lista atualizada de regras que você pode [baixar aqui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx).

>[!NOTE]
>
>As amostras de código fornecidas aqui são apenas para fins ilustrativos. Consulte a [Documentação de conceitos](https://docs.sonarsource.com/sonarqube/latest/) do SonarQube para saber mais sobre os conceitos e as regras de qualidade do SonarQube.

## Regras do SonarQube {#sonarqube-rules}

A seção a seguir especifica as regras do SonarQube executadas pelo Cloud Manager.

### Não usar funções potencialmente perigosas  {#do-not-use-potentially-dangerous-functions}

* **Chave**: CQRules:CWE-676
* **Tipo**: Vulnerabilidade
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Os métodos `Thread.stop()` e `Thread.interrupt()` podem gerar problemas difíceis de reproduzir e, em alguns casos, vulnerabilidades de segurança. A utilização deve ser rigorosamente monitorizada e validada. Em geral, a transmissão de mensagens é uma forma mais segura de atingir objetivos semelhantes.

#### Código não compatível  {#non-compliant-code}

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

#### Código compatível  {#compliant-code}

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

### Não use strings de formatação que possam ser controladas externamente  {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Chave**: CQRules:CWE-134
* **Tipo**: Vulnerabilidade
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Usar uma string de formatação de uma fonte externa (como um parâmetro de solicitação ou conteúdo gerado pelo usuário) pode expor um aplicativo a ataques de negação de serviço. Há casos em que uma string de formatação pode ser controlada externamente, mas isso somente é permitido de fontes confiáveis.

#### Código não compatível  {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### As solicitações HTTP devem sempre ter um tempo limite de soquete e conexão {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Chave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.6.0

Ao fazer solicitações HTTP em um aplicativo do Experience Manager, é essencial configurar tempos limite apropriados para evitar o consumo desnecessário de thread.
Por padrão, o Java™ HTTP Client (java.net.HttpUrlConnection) e o cliente Apache HTTP Components amplamente usado não impõem tempos limite, portanto, eles devem ser configurados manualmente. Como prática recomendada, os tempos limite devem ser definidos como 60 segundos ou menos.

#### Código não compatível  {#non-compliant-code-2}

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

#### Código compatível  {#compliant-code-1}

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

public void orDoThis () {
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
* **Tipo**: `Code Smell`
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Os objetos ResourceResolver obtidos de `ResourceResolverFactory` consomem recursos do sistema. Embora existam medidas em vigor para recuperar esses recursos quando um `ResourceResolver` não é mais utilizado, é mais eficiente fechar explicitamente todos os objetos `ResourceResolver` abertos chamando o método `close()`.

Um equívoco comum é que `ResourceResolver` objetos criados com uma sessão JCR existente não devem ser fechados explicitamente, ou que seu fechamento afeta a sessão JCR. Esta informação está incorreta. Um `ResourceResolver` deve ser sempre fechado quando não é mais necessário. Como `ResourceResolver` implementa a interface `Closeable`, você também pode usar a sintaxe `try-with-resources` em vez de chamar `close()` diretamente.

#### Código não compatível  {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Código compatível  {#compliant-code-2}

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

### Não use caminhos de servlet do Sling para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Chave**: CQRules:CQBP-75
* **Tipo**: `Code Smell`
* **Severidade**: Alta
* **Desde**: Versão 2018.4.0

Conforme descrito na [`Sling` documentação](https://sling.apache.org/documentation/the-sling-engine/servlets.html), vinculações de servlets por caminhos não são incentivadas. Os servlets vinculados a caminhos não podem usar os controles de acesso JCR padrão e, como resultado disso, exigem maior rigor de segurança. Em vez de usar servlets vinculados a caminhos, é recomendado criar nós no repositório e registrar os servlets por tipo de recurso.

#### Código não compatível  {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### As exceções capturadas devem ser registradas ou descartadas, mas não ambos {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Chave**: CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Em geral, uma exceção deve ser registrada exatamente uma vez. Registrar exceções várias vezes pode causar confusão. O motivo é porque não está claro quantas vezes uma exceção ocorreu. O padrão mais comum que leva a esse efeito é o registro e o descarte de uma exceção capturada.

#### Código não compatível  {#non-compliant-code-6}

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

#### Código compatível  {#compliant-code-3}

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

### Evite instruções de log seguidas imediatamente por instruções de descarte {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Chave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Outro padrão comum a ser evitado é registrar uma mensagem e imediatamente depois lançar uma exceção. Isso geralmente indica que a mensagem de exceção acabará duplicada nos arquivos de log. 

#### Código não compatível  {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Código compatível  {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Evite registrar no nível INFO ao manipular solicitações GET ou HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Chave**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Tipo**: `Code Smell`
* **Severidade**: baixa

Em geral, o nível de log INFO deve ser usado para demarcar ações importantes e, por padrão, o Experience Manager é configurado para registrar no nível INFO ou superior. Os métodos GET e HEAD devem ser operações somente leitura e, portanto, não constituem ações importantes. Registrar no nível INFO em resposta a solicitações GET ou HEAD provavelmente criará um ruído significativo de log, dificultando a identificação de informações úteis em arquivos de log. Ao manipular solicitações do GET ou do HEAD, registre nos níveis AVISO ou ERRO se algo der errado. Use os níveis DEBUG ou TRACE se forem necessárias informações detalhadas de solução de problemas.

>[!NOTE]
>
>Não se aplica ao registro do tipo `access.log` para cada solicitação.

#### Código não compatível  {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Código compatível  {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Não use Exception.getMessage() como o primeiro parâmetro de uma instrução de log  {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Chave**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como prática recomendada, as mensagens de log devem fornecer informações contextuais sobre onde ocorreu uma exceção no aplicativo. Embora o contexto também possa ser determinado pelo uso de rastros de pilha, em geral, a mensagem de log será mais fácil de ler e entender. Como resultado disso, ao registrar uma exceção, não é uma prática recomendada usar a mensagem da exceção como a mensagem de registro. A mensagem de exceção explica o que deu errado, enquanto a mensagem de log deve informar ao leitor sobre o que o aplicativo estava fazendo quando a exceção ocorreu. A mensagem de exceção ainda é registrada. Ao especificar sua própria mensagem, será mais fácil entender os logs. 

#### Código não compatível  {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Código compatível  {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Os logs em blocos de catch devem estar no nível AVISO ou ERRO {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Chave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como o nome sugere, as exceções do Java™ sempre devem ser usadas em casos excepcionais. Como resultado disso, quando uma exceção é capturada, é importante garantir que as mensagens de log sejam registradas no nível apropriado, seja WARN ou ERROR. Esse processo garante que essas mensagens sejam exibidas corretamente nos logs.

#### Código não compatível  {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Código compatível  {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Não imprimir rastros de pilha no console {#do-not-print-stack-traces-to-the-console}

* **Chave**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Como mencionado, o contexto é essencial para entender as mensagens de log. Usar `Exception.printStackTrace()` faz com que somente o rastro de pilha seja enviado para o fluxo de erro padrão, perdendo todo o contexto. Além disso, em um aplicativo multithread como o Experience Manager, se várias exceções forem impressas em paralelo usando esse método, seus rastros de pilha poderão se sobrepor, gerando bastante confusão. As exceções devem ser registradas somente por meio da estrutura de registro.

#### Código não compatível  {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Código compatível  {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Não envie para a saída padrão ou fluxo de erro padrão {#do-not-output-to-standard-output-or-standard-error}

* **Chave**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Os registros no Experience Manager sempre devem ser feitos por meio da estrutura de registro (SLF4J). Enviar diretamente para a saída padrão ou fluxos de erro padrão perde as informações estruturais e contextuais fornecidas pela estrutura de registro. Às vezes, isso pode causar problemas de desempenho.

#### Código não compatível  {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Código compatível  {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Evite caminhos de bibliotecas e aplicativos codificados {#avoid-hardcoded-apps-and-libs-paths}

* **Chave**: CQRules:CQBP-71
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2018.4.0

Caminhos que começam com `/libs` e `/apps` geralmente não devem ser codificados. Normalmente, esses caminhos são armazenados em relação ao caminho de pesquisa `Sling`, que tem como padrão `/libs,/apps`. O uso do caminho absoluto pode gerar defeitos sutis que só aparecerão posteriormente no ciclo de vida do projeto.

#### Código não compatível  {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Código compatível  {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Não use o Sling Scheduler {#sonarqube-sling-scheduler}

* **Chave**: CQRules:AMSCORE-554
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Não use o Agendador do `Sling` para tarefas que exigem execução garantida. Os processos agendados no Sling têm execução garantida e são mais adequados para ambientes clusterizados e não clusterizados.

Consulte [`Apache Sling` Evento e manuseio de trabalho](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) para saber mais sobre como os trabalhos do Sling são tratados em ambientes clusterizados.

### Não use APIs obsoletas do Experience Manager {#sonarqube-aem-deprecated}

* **Chave**: AMSCORE-553
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A superfície da API do Experience Manager está em constante revisão para identificar APIs cujo uso não é recomendado e, portanto, são consideradas obsoletas.

Geralmente, essas APIs são descontinuadas usando a anotação padrão Java™ `@Deprecated` e, sendo assim, são identificadas por `squid:CallToDeprecatedMethod`.

No entanto, há casos em que uma API é descontinuada no contexto do Experience Manager mas pode não ser descontinuada em outros contextos. Esta regra identifica essa segunda classe.

### Não use a anotação @Inject com @Optional nos Modelos Sling {#sonarqube-slingmodels-inject-optional}

* **Chave**: InjectAnnotationWithOptionalInjectionCheck
* **Tipo**: qualidade do software
* **Severidade**: baixa
* **Desde**: Versão 2023.11

O projeto `Apache Sling` não incentiva o uso da anotação `@Inject` no contexto de Modelos Sling, pois pode resultar em desempenho inadequado quando combinado com `DefaultInjectionStrategy.OPTIONAL` (no nível de campo ou de classe). Em vez disso, injeções mais específicas (como `@ValueMapValue` ou `@OsgiInjector` anotações) devem ser usadas.

Consulte a [`Apache Sling` documentação](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1) para obter mais informações sobre as anotações recomendadas e por que essa recomendação foi feita.


### Reutilizar instâncias de um HTTPClient {#sonarqube-reuse-httpclient}

* **Chave**: AEMSRE-870
* **Tipo**: qualidade do software
* **Severidade**: baixa
* **Desde**: Versão 2023.11

Os aplicativos do AEM geralmente alcançam outros aplicativos usando o protocolo HTTP, e o Apache HttpClient é uma biblioteca usada com frequência para atingir esse fim. Mas a criação desse objeto HttpClient vem com alguma sobrecarga, de modo que esses objetos devem ser reutilizados o máximo possível.

Essa regra verifica se esse objeto HttpClient não é privado em um método, mas global em um nível de classe, para que possa ser reutilizado. Nesse caso, o campo HttpClient deve ser definido no construtor da classe ou no método `activate()` (se essa classe for um componente/serviço OSGi).

Consulte o [Guia de Otimização](https://hc.apache.org/httpclient-legacy/performance.html) do HttpClient para obter algumas práticas recomendadas relacionadas ao uso do HttpClient.

#### Código não compatível  {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### Código compatível  {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## Regras de conteúdo OakPAL {#oakpal-rules}

A seção a seguir especifica as verificações do OakPAL executadas pelo Cloud Manager.

>[!NOTE]
>
>O OakPAL é uma estrutura que valida pacotes de conteúdo usando um repositório Oak autônomo. Um Parceiro da Experience Manager, que ganhou o prêmio Experience Manager Rockstar North America 2019, o desenvolveu.

### Os clientes não devem implementar ou estender APIs de produto anotadas com @ProviderType{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Chave**: CQBP-84
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2018.7.0

A API do Experience Manager contém interfaces e classes Java™, que devem ser usadas, mas não implementadas, apenas pelo código personalizado. Por exemplo, somente a Experience Manager deve implementar a interface `com.day.cq.wcm.api.Page`.

Quando novos métodos são adicionados a essas interfaces, esses métodos adicionais não afetam o código existente que usa essas interfaces. Como resultado, a adição de novos métodos a essas interfaces é considerada compatível com versões anteriores. No entanto, se o código personalizado implementa uma dessas interfaces, ele apresenta um risco de compatibilidade com versões anteriores para o cliente.

As interfaces e as classes, conforme implementadas pelo Experience Manager, são anotadas com `org.osgi.annotation.versioning.ProviderType` ou, às vezes, com a anotação herdada semelhante: `aQute.bnd.annotation.ProviderType`. Esta regra identifica casos em que o código personalizado implementa essa interface ou estende uma classe.

#### Código não compatível  {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Os índices personalizados do Lucene Oak devem ter uma configuração do Tika {#oakpal-indextikanode}

* **Chave**: IndexTikaNode
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.8.0

Vários índices do Oak prontos para uso no Experience Manager incluem uma configuração do Tika, e as personalizações desses índices devem incluir uma configuração do Tika. Essa regra verifica as personalizações do `damAssetLucene` e `lucene`, e o `graphqlConfig` indexa e gera um problema se o nó `tika` estiver ausente ou se o nó `tika` não tiver um nó filho chamado `config.xml`.

Consulte a [documentação de indexação](/help/operations/indexing.md#preparing-the-new-index-definition) para obter mais informações sobre como personalizar as definições de índice.

#### Código não compatível  {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### Código compatível  {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
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

Os índices Oak do tipo `lucene` sempre devem ser indexados de forma assíncrona. Caso contrário, poderá ocorrer instabilidade no sistema. Mais informações sobre a estrutura dos índices Lucene podem ser encontradas na [documentação do Oak](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition).

#### Código não compatível  {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### Código compatível  {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Os índices de ativo DAM personalizados do Lucene Oak estão adequadamente estruturados {#oakpal-damAssetLucene-sanity-check}

* **Chave**: IndexDamAssetLucene
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: 2021.6.0

Para que a pesquisa de ativos funcione corretamente no Experience Manager Assets, as personalizações do índice Oak `damAssetLucene` devem seguir um conjunto de diretrizes específicas desse índice. Esta regra verifica se a definição do índice deve ter uma propriedade de vários valores chamada `tags`, que contém o valor `visualSimilaritySearch`.

#### Código não compatível  {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### Código compatível  {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Os pacotes de clientes não devem criar ou modificar nós em bibliotecas {#oakpal-customer-package}

* **Chave**: BannedPath
* **Tipo**: Erro
* **Severidade**: Crítica
* **Desde**: Versão 2019.6.0

Considerar a árvore de conteúdo do `/libs` no repositório de conteúdo do Experience Manager como somente leitura pelos clientes é uma prática recomendada de longa data. A modificação dos nós e propriedades em `/libs` cria riscos significativos para atualizações importantes e secundárias. Use o Adobe, através de canais oficiais, para fazer modificações no `/libs`.

### Os pacotes não devem conter configurações de OSGi duplicadas {#oakpal-package-osgi}

* **Chave**: DuplicateOsgiConfigurations
* **Tipo**: Erro
* **Severidade**: Alta
* **Desde**: Versão 2019.6.0

Um problema comum que ocorre em projetos complexos é quando o mesmo componente OSGi é configurado várias vezes. Esse problema cria uma ambiguidade sobre qual configuração é aplicável. Essa regra age de acordo com o modo de execução, no sentido de que ela apenas identifica problemas em que o mesmo componente é configurado várias vezes no mesmo modo de execução ou combinação de modos de execução.

>[!NOTE]
>
>A regra gera problemas quando uma mesma configuração, em um mesmo caminho, é definida em vários pacotes, incluindo casos em que o mesmo pacote é duplicado na lista geral de pacotes incorporados.
>
>Por exemplo, se a compilação produzir pacotes chamados `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all`, nos quais `com.myco:com.myco.all` incorpora `com.myco:com.myco.ui.apps`, então todas as configurações em `com.myco:com.myco.ui.apps` serão relatadas como duplicadas.
>
>Geralmente, esta situação é um caso em que não se deve seguir as [Diretrizes de Estrutura do Pacote de Conteúdo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Neste exemplo, o pacote `com.myco:com.myco.ui.apps` não tem a propriedade `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Código não compatível  {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Código compatível  {#compliant-code-osgi}

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

Por motivos de segurança, os caminhos que contêm `/config/` e `/install/` só podem ser lidos por usuários administrativos no Experience Manager e devem ser usados apenas para configuração do OSGi e de pacotes do OSGi. Colocar outros tipos de conteúdo em caminhos que contêm esses segmentos faz com que o comportamento do aplicativo difira involuntariamente entre usuários administrativos e não administrativos.

Um problema comum é o uso de nós chamados `config` nas caixas de diálogo de componente ou ao especificar a configuração do editor rich text para edição em linha. Para solucionar esse problema, o nó incorreto deve ser renomeado para um nome que esteja em conformidade. Para configurar o editor de rich text, use a propriedade `configPath` do nó `cq:inplaceEditing` para especificar o novo local.

#### Código não compatível  {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Código compatível  {#compliant-code-config-install}

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

Semelhante à regra [Os pacotes não devem conter configurações OSGi duplicadas](#oakpal-package-osgi), essa situação é um problema comum em projetos complexos, em que o mesmo caminho de nó é gravado por vários pacotes de conteúdo separados. Embora seja possível usar as dependências do pacote de conteúdo para garantir um resultado consistente, é melhor evitar qualquer sobreposição.

### O modo de criação padrão não deve ser a interface clássica {#oakpal-default-authoring}

* **Chave**: ClassicUIAuthoringMode
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A configuração `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` do OSGi define o modo de criação padrão no Experience Manager. Visto que a interface clássica foi descontinuada no Experience Manager 6.4, um problema será gerado se o modo de criação padrão estiver configurado para usá-la.

### Componentes com caixas de diálogo devem ter caixas de diálogo da interface para toque {#oakpal-components-dialogs}

* **Chave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Os componentes do Experience Manager que têm uma caixa de diálogo com interface clássica sempre devem ter uma caixa de diálogo com interface de toque correspondente. Ambos oferecem uma experiência de criação ideal compatível com o modelo de implantação do Cloud Service, em que a interface clássica não é mais compatível. Essa regra verifica os seguintes cenários:

* Um componente com uma caixa de diálogo da interface do usuário clássica (ou seja, um nó filho`dialog`) deve ter uma caixa de diálogo da interface do usuário de toque correspondente (ou seja, um nó filho `cq:dialog`).
* Um componente com uma caixa de diálogo de design com interface clássica (ou seja, um nó `design_dialog`) deve ter uma caixa de diálogo de design com interface de toque correspondente (ou seja, um nó filho `cq:design_dialog`).
* Um componente com uma caixa de diálogo com interface clássica e uma caixa de diálogo de design com interface clássica deve ter uma caixa de diálogo com interface de toque e uma caixa de diálogo de design com interface de toque correspondentes.

A documentação das Ferramentas de modernização do Experience Manager fornece a documentação e as ferramentas para converter componentes da interface clássica para a interface sensível ao toque. Consulte a [documentação das Ferramentas de modernização do Experience Manager](https://opensource.adobe.com/aem-modernize-tools/) para obter mais detalhes.

### Os pacotes não devem misturar conteúdo mutável e imutável {#oakpal-packages-immutable}

* **Chave**: ImmutableMutableMixedPackage
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

Para serem compatíveis com o modelo de implantação do Cloud Service, os pacotes de conteúdo individuais devem ter conteúdo para áreas imutáveis do repositório (`/apps` e `/libs`) ou para a área mutável (tudo que não esteja em `/apps` ou `/libs`), mas não ambos. Por exemplo, um pacote que inclui `/apps/myco/components/text` e `/etc/clientlibs/myco` não é compatível com o Cloud Service e faz com que um problema seja relatado.

>[!NOTE]
>
>A regra [Pacotes de Clientes Não Devem Criar ou Modificar Nós em libs](#oakpal-customer-package) sempre se aplica.

Consulte a [Estrutura de projetos do Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md) para obter mais detalhes.

### Não usar agentes de replicação reversa {#oakpal-reverse-replication}

* **Chave**: ReverseReplication
* **Tipo**: `Code Smell`/Compatibilidade com Cloud Service
* **Severidade**: Baixa
* **Desde**: Versão 2020.5.0

A compatibilidade com a replicação reversa não está disponível em implantações do Cloud Service, conforme descrito nas [notas de versão](/help/release-notes/aem-cloud-changes.md#replication-agents) do Experience Manager as a Cloud Service.

Os clientes que usam replicação reversa devem entrar em contato com a Adobe para obter soluções alternativas.

### Os recursos contidos nas bibliotecas de clientes habilitadas por proxy devem estar em uma pasta chamada “resources” {#oakpal-resources-proxy}

* **Chave**: ClientlibProxyResource
* **Tipo**: Erro
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

As bibliotecas de cliente do Experience Manager podem conter recursos estáticos, como imagens e fontes. Conforme descrito no documento [Usando Pré-processadores](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors), ao usar bibliotecas de clientes por proxy, esses recursos estáticos devem estar contidos em uma pasta filho chamada `resources` para serem efetivamente referenciados nas instâncias de publicação.

#### Código não compatível  {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Código compatível  {#compliant-proxy-enabled}

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

Com a mudança para os microsserviços de ativos para o processamento de ativos no Adobe Experience Manager as a Cloud Service, vários processos de fluxo de trabalho usados nas versões local e AMS agora não são compatíveis. Muitos desses workflows também se tornaram desnecessários.

A ferramenta de migração do [repositório de ativos do Experience Manager as a Cloud Service no GitHub](https://github.com/adobe/aem-cloud-migration) pode ser usada para atualizar modelos de fluxo de trabalho durante a migração para o Experience Manager as a Cloud Service.

### Recomendamos o uso de modelos editáveis em vez de modelos estáticos {#oakpal-static-template}

* **Chave**: StaticTemplateUsage
* **Tipo**: `Code Smell` 
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Embora o uso de modelos estáticos seja historicamente comum em projetos do Experience Manager, a Adobe recomenda usar modelos editáveis porque eles fornecem mais flexibilidade e são compatíveis com recursos adicionais não presentes em modelos estáticos. Mais informações podem ser encontradas no documento [Modelos de página](/help/implementing/developing/components/templates.md).

A migração de modelos estáticos para editáveis pode ser amplamente automatizada usando as [Ferramentas de modernização do Experience Manager](https://opensource.adobe.com/aem-modernize-tools/).

### O uso de componentes básicos herdados não é recomendado {#oakpal-usage-legacy}

* **Chave**: LegacyFoundationComponentUsage
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Os componentes fundamentais herdados (ou seja, localizados em `/libs/foundation`) foram descontinuados em várias versões do Experience Manager para incentivar o uso dos componentes principais. O uso dos componentes básicos como base para os componentes personalizados (seja por sobreposição ou herança) não é recomendado e deve ser convertido para os componentes principais correspondentes.

[As Ferramentas de Modernização do Experience Manager](https://opensource.adobe.com/aem-modernize-tools/) podem facilitar essa conversão.

### Use apenas ordenações e nomes de modo de execução compatíveis {#oakpal-supported-runmodes}

* **Chave**: SupportedRunmode
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service utiliza uma política de nomeação rigorosa para nomes de modo de execução e uma ordenação estrita para eles. A lista de modos de execução com suporte é fundamentada no documento [Implantação no Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) e qualquer desvio em relação a essa lista é identificado como um problema.

### Os nós de definição do índice de pesquisa personalizado devem ser nós secundários diretos de `/oak:index` {#oakpal-custom-search}

* **Chave**: OakIndexLocation
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) sejam nós filhos diretos de `/oak:index`. Os índices em outros locais devem ser movidos para serem compatíveis com o Experience Manager as a Cloud Service. Mais informações sobre índices de pesquisa podem ser encontradas no documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

### Os nós de definição do índice de pesquisa personalizada devem ter uma compatVersion de 2 {#oakpal-custom-search-compatVersion}

* **Chave**: IndexCompatVersion
* **Tipo**: `Code Smell` 
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) tenham a propriedade `compatVersion` definida como `2`. O Adobe Experience Manager as a Cloud Service não é compatível com nenhum outro valor. Consulte [Pesquisa e indexação de conteúdo](/help/operations/indexing.md) para obter mais informações sobre índices de pesquisa.

### Os nós descendentes dos nós de definição do índice de pesquisa personalizado devem ser do tipo `nt:unstructured `{#oakpal-descendent-nodes}

* **Chave**: IndexDescendantNodeType
* **Tipo**: `Code Smell` 
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Problemas difíceis de solucionar podem ocorrer quando um nó de definição do índice de pesquisa personalizado possui nós filhos desordenados. Para evitar essa situação, é recomendado que todos os nós descendentes de um nó `oak:QueryIndexDefinition` sejam do tipo `nt:unstructured`.

### Os nós de definição do índice de pesquisa personalizado devem conter um nó filho denominado “indexRules” que tenha filhos {#oakpal-custom-search-index}

* **Chave**: IndexRulesNode
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

Um nó de definição de índice de pesquisa personalizada corretamente definido deve conter um nó filho chamado `indexRules`, que por sua vez deve ter pelo menos um nó filho. Para mais informações, consulte a [documentação do Oak](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Os nós de definição do índice de pesquisa personalizado devem seguir as convenções de nomeação {#oakpal-custom-search-definitions}

* **Chave**: IndexName
* **Tipo**: `Code Smell` 
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) sejam nomeadas de acordo com um padrão específico descrito no documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

### Os nós de definição do índice de pesquisa personalizado devem usar o tipo de índice Lucene {#oakpal-index-type-lucene}

* **Chave**: IndexType
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: Versão 2021.2.0 (tipo e severidade alterados em 2021.8.0)

O Experience Manager as a Cloud Service exige que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) tenham uma propriedade `type` cujo valor esteja definido como `lucene`. Uma indexação que utiliza tipos de índice herdados deve ser atualizada antes da migração para o Experience Manager as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição do índice de pesquisa personalizado não devem conter uma propriedade denominada “seed” {#oakpal-property-name-seed}

* **Chave**: IndexSeedProperty
* **Tipo**: `Code Smell`
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service proíbe que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) contenham uma propriedade chamada `seed`. Uma indexação que utiliza essa propriedade deve ser atualizada antes da migração para o Experience Manager as a Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós de definição do índice de pesquisa personalizado não devem conter uma propriedade denominada “reindex” {#oakpal-reindex-property}

* **Chave**: IndexReindexProperty
* **Tipo**: `Code Smell` 
* **Severidade**: Baixa
* **Desde**: Versão 2021.2.0

O Experience Manager as a Cloud Service proíbe que as definições do índice de pesquisa personalizado (ou seja, nós do tipo `oak:QueryIndexDefinition`) contenham uma propriedade chamada `reindex`. A indexação usando essa propriedade deve ser atualizada antes da migração para o Experience Manager as a
Cloud Service. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#how-to-use) para obter mais informações.

### Os nós Lucene de ativos DAM personalizados não devem especificar `queryPaths` {#oakpal-damAssetLucene-queryPaths}

* **Chave**: IndexDamAssetLucene
* **Tipo**: Erro
* **Severidade**: Limitante
* **Desde**: versão 2022.1.0

#### Código não compatível  {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### Código compatível  {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Se a definição do índice de pesquisa personalizado contiver `compatVersion`, ele deverá ser definido como 2 {#oakpal-compatVersion}

* **Chave**: IndexCompatVersion
* **Tipo**: `Code Smell`
* **Severidade**: Alta
* **Desde**: versão 2022.1.0


### O nó de índice que especifica `includedPaths` também deve especificar `queryPaths` com os mesmos valores {#oakpal-included-paths-without-query-paths}

* **Chave**: IndexIncludedPathsWithoutQueryPaths
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

Para índices personalizados, configure `includedPaths` e `queryPaths` com valores idênticos. Se um for especificado, o outro deverá corresponder a ele. No entanto, há um caso especial para índices de `damAssetLucene`, incluindo suas versões personalizadas. Para estes casos, forneça apenas `includedPaths`.

### O nó de índice que especifica `nodeScopeIndex` no tipo de nó genérico também deve especificar `includedPaths` e `queryPaths` {#oakpal-full-text-on-generic-node-type}

* **Chave**: IndexFulltextOnGenericType
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

Ao definir a propriedade `nodeScopeIndex` em um tipo de nó &quot;genérico&quot; como `nt:unstructured` ou `nt:base`, você também deve especificar as propriedades `includedPaths` e `queryPaths`.
O tipo de nó `nt:base` pode ser considerado &quot;genérico&quot;, pois todos os tipos de nó herdam dele. Assim, definir um `nodeScopeIndex` em `nt:base` faz com que ele indexe todos os nós no repositório. Da mesma forma, `nt:unstructured` também é considerado &quot;genérico&quot;, pois há muitos nós em repositórios desse tipo.

#### Código não compatível  {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### Código compatível  {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### A propriedade queryLimitReads do mecanismo de consulta não deve ser substituída {#oakpal-query-limit-reads}

* **Chave**: OverrideOfQueryLimitReads
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

Substituir o valor padrão pode resultar em leituras de página lentas, especialmente quando mais conteúdo é adicionado.

### Várias versões ativas do mesmo índice {#oakpal-multiple-active-versions}

* **Chave**: IndexDetectMultipleActiveVersionsOfSameIndex
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

#### Código não compatível  {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### Código compatível  {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### O nome das definições de índice totalmente personalizadas deve estar em conformidade com as diretrizes oficiais {#oakpal-fully-custom-index-name}

* **Chave**: IndexValidFullyCustomName
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

O padrão esperado para nomes de índice totalmente personalizados é: `[prefix].[indexName]-custom-[version]`. Mais informações podem ser encontradas no documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md).

### Mesma propriedade com valores analisados diferentes na mesma definição de índice {#oakpal-same-property-different-analyzed-values}

#### Código não compatível  {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### Código compatível  {#compliant-code-same-property-different-analyzed-values}

Exemplo:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Exemplo:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Se a propriedade analisada não for explicitamente definida, seu valor padrão será false.

### Propriedade das tags {#tags-property}

* **Chave**: IndexHasValidTagsProperty
* **Tipo**: `Code Smell`
* **Severidade**: baixa
* **Desde**: versão 2023.1.0

Para índices específicos, certifique-se de manter a propriedade das tags e seus valores atuais. Embora a adição de novos valores à propriedade de tags seja permitida, a exclusão de qualquer valor existente (ou da propriedade completamente) pode levar a resultados inesperados.

### Não implante nós de definição de índice no pacote de conteúdo da interface {#oakpal-ui-content-package}

* **Chave**: IndexNotUnderUIContent
* **Tipo**: melhoria
* **Severidade**: baixa
* **Desde**: versão 2024.6.0

O AEM Cloud Service proíbe que definições de índice de pesquisa personalizadas (nós do tipo `oak:QueryIndexDefinition`) sejam implantadas no pacote de conteúdo da interface.

>[!WARNING]
>
>Você deve resolver esse problema o mais rápido possível, pois ele pode causar falhas de pipeline a partir da [versão de agosto de 2024 do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### A definição de índice de texto completo personalizado do tipo damAssetLucene deve receber o prefixo correto de &#39;damAssetLucene&#39; {#oakpal-dam-asset-lucene}

* **Chave**: CustomFulltextIndexesOfTheDamAssetCheck
* **Tipo**: melhorias
* **Severidade**: baixa
* **Desde**: versão 2024.6.0

O AEM Cloud Service proíbe que definições de índice de texto completo personalizadas do tipo `damAssetLucene` sejam prefixadas com qualquer item diferente de `damAssetLucene`.

>[!WARNING]
>
>Resolva esse problema o mais rápido possível, pois pode causar falhas de pipeline a partir da [versão de agosto de 2024 do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### Nós de definição de índice não devem conter propriedades com o mesmo nome {#oakpal-index-property-name}

* **Chave**: DuplicateNameProperty
* **Tipo**: melhoria
* **Severidade**: baixa
* **Desde**: versão 2024.6.0

O AEM Cloud Service proíbe que definições de índice de pesquisa personalizadas (ou seja, nós do tipo `oak:QueryIndexDefinition`) contenham propriedades com o mesmo nome

>[!WARNING]
>
>Resolva esse problema o mais rápido possível, pois pode causar falhas de pipeline a partir da [versão de agosto de 2024 do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### A personalização de determinadas definições de índice prontas para uso é proibida {#oakpal-customizing-ootb-index}

* **Chave**: RestrictIndexCustomization
* **Tipo**: melhoria
* **Severidade**: baixa
* **Desde**: versão 2024.6.0

O AEM Cloud Service proíbe modificações não autorizadas nos seguintes índices protos para uso:

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>Resolva esse problema o mais rápido possível, pois pode causar falhas de pipeline a partir da [versão de agosto de 2024 do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### A configuração dos tokenizers em analisadores deve ser criada com o nome &quot;tokenizer&quot; {#oakpal-tokenizer}

* **Chave**: AnalyzerTokenizerConfigCheck
* **Tipo**: melhoria
* **Severidade**: baixa
* **Desde**: versão 2024.6.0

O AEM Cloud Service proíbe a criação de tokenizers com nomes incorretos em analisadores. Os tokenizadores devem ser sempre definidos como `tokenizer`.

>[!WARNING]
>
>Resolva esse problema o mais rápido possível, pois pode causar falhas de pipeline a partir da [versão de agosto de 2024 do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### A configuração das definições de indexação não deve conter espaços {#oakpal-indexing-definitions-spaces}

* **Chave**: PathSpacesCheck
* **Tipo**: melhoria
* **Severidade**: baixa
* **Desde**: versão 2024.7.0

O AEM Cloud Service proíbe a criação de definições de indexação que contenham propriedades com espaços.
