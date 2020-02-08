---
title: Regras de qualidade de código personalizado - Serviços em nuvem
description: Regras de qualidade de código personalizado - Serviços em nuvem
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# Understanding Custom Code Quality Rules {#custom-code-quality-rules}


Esta página descreve as regras de qualidade de código personalizadas executadas pelo Cloud Manager criadas com base nas práticas recomendadas da engenharia do AEM.

>[!NOTE]
>
>As amostras de código fornecidas aqui são apenas para fins ilustrativos.

## Regras do SonarQube {#sonarqube-rules}

A seção a seguir destaca as regras do SonarQube:

### Não utilize funções potencialmente perigosas {#do-not-use-potentially-dangerous-functions}

**Chave**: CQRules:CWE-676

**Tipo**: Vulnerabilidade

**Gravidade**: Major

**Desde**: Versão 2018.4.0

Os métodos ***Thread.stop()*** e ***Thread.interrupt()*** podem gerar problemas difíceis de reproduzir e, em alguns casos, vulnerabilidades de segurança. A sua utilização deve ser rigorosamente monitorizada e validada. Em geral, a transmissão de mensagens é uma forma mais segura de atingir objetivos semelhantes.

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

**Chave**: CQRules:CWE-134

**Tipo**: Vulnerabilidade

**Gravidade**: Major

**Desde**: Versão 2018.4.0

O uso de uma string de formato de uma fonte externa (como um parâmetro de solicitação ou conteúdo gerado pelo usuário) pode produzir pode expor um aplicativo a ataques de negação de serviço. Há circunstâncias em que uma string de formato pode ser controlada externamente, mas só é permitida de fontes confiáveis.

#### Código não compatível {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### As solicitações HTTP devem sempre ter tempos limite de soquete e conexão {#http-requests-should-always-have-socket-and-connect-timeouts}

**Chave**: CQRules:ConnectionTimeoutMechanism

**Tipo**: Bug

**Gravidade**: Crítico

**Desde**: Versão 2018.6.0

Ao executar solicitações HTTP de dentro de um aplicativo AEM, é essencial garantir que os tempos limite apropriados sejam configurados para evitar o consumo desnecessário de thread. Infelizmente, o comportamento padrão do cliente HTTP padrão do Java (java.net.HttpUrlConnection) e do cliente Apache HTTP Components comumente usado é nunca expirar, portanto, os tempos limite devem ser definidos explicitamente. Além disso, como prática recomendada, esses tempos limite não devem exceder 60 segundos.

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

### As APIs de produto anotadas com @ProviderType não devem ser implementadas ou estendidas pelos clientes {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**Chave**: CQBP-84, CQBP-84-dependências

**Tipo**: Bug

**Gravidade**: Crítico

**Desde**: Versão 2018.7.0

A API do AEM contém interfaces e classes Java que devem ser usadas apenas, mas não implementadas, pelo código personalizado. Por exemplo, a interface *com.day.cq.wcm.api.Page* foi projetada para ser implementada somente ***pelo*** AEM.

Quando novos métodos são adicionados a essas interfaces, esses métodos adicionais não afetam o código existente que usa essas interfaces e, como resultado, a adição de novos métodos a essas interfaces é considerada retrocompatível. No entanto, se o código personalizado ***implementa*** uma dessas interfaces, ele apresenta um risco de compatibilidade com versões anteriores para o cliente.

As interfaces (e classes) que só devem ser implementadas pelo AEM são anotadas com *org.osgi.annotation.versioning.ProviderType* (ou, em alguns casos, uma anotação herdada similar *aQute.bnd.annotation.ProviderType*). Essa regra identifica os casos em que tal interface é implementada (ou uma classe é estendida) pelo código personalizado.

#### Código não compatível {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Os objetos ResourceResolver devem ser sempre fechados {#resourceresolver-objects-should-always-be-closed}

**Chave**: CQRules:CQBP-72

**Tipo**: Cheiro de código

**Gravidade**: Major

**Desde**: Versão 2018.4.0

Os objetos ResourceResolver obtidos a partir do ResourceResolverFactory consomem recursos do sistema. Embora existam medidas para recuperar esses recursos quando um ResourceResolver não estiver mais em uso, é mais eficiente fechar explicitamente quaisquer objetos ResourceResolver abertos chamando o método close().

Um equívoco relativamente comum é que os objetos ResourceResolver criados usando uma Sessão JCR existente não devem ser explicitamente fechados ou que isso fechará a Sessão JCR subjacente. Esse não é o caso - independentemente de como um ResourceResolver é aberto, ele deve ser fechado quando não for mais usado. Como o ResourceResolver implementa a interface Fechável, também é possível usar a sintaxe try-with-resources em vez de chamar explicitamente close().

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

### Não usar caminhos de servlet Sling para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

**Chave**: CQRules:CQBP-75

**Tipo**: Cheiro de código

**Gravidade**: Major

**Desde**: Versão 2018.4.0

Conforme descrito na documentação [do](http://sling.apache.org/documentation/the-sling-engine/servlets.html)Sling, os servlets de vinculação por caminhos são desencorajados. Os servlets vinculados ao caminho não podem usar controles de acesso JCR padrão e, como resultado, exigem rigor de segurança adicional. Em vez de usar servlets vinculados a caminho, é recomendável criar nós no repositório e registrar servlets por tipo de recurso.

#### Código não compatível {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### As exceções obtidas devem ser registradas ou lançadas, mas não ambas {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Chave**: CQRules:CQBP-44—CatchAndOrThrow

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Em geral, uma exceção deve ser registrada exatamente uma vez. O registro de exceções várias vezes pode causar confusão, pois não está claro quantas vezes uma exceção ocorreu. O padrão mais comum que leva a isso é cortar e lançar uma exceção.

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

### Evite ter uma declaração de log imediatamente seguida de uma declaração de lançamento {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Chave**: CQRules:CQBP-44—ConsecutivelyLogAndThrow

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Outro padrão comum a ser evitado é registrar uma mensagem e imediatamente lançar uma exceção. Isso geralmente indica que a mensagem de exceção acabará duplicada nos arquivos de registro.

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

### Evite fazer logon em INFO ao manipular solicitações GET ou HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Chave**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Tipo**: Cheiro de código

**Gravidade**: Menor

Em geral, o nível de log INFO deve ser usado para demarcar ações importantes e, por padrão, o AEM está configurado para fazer logon no nível INFO ou acima. Os métodos GET e HEAD só devem ser operações somente leitura e, portanto, não constituem ações importantes. O registro no nível INFO em resposta às solicitações GET ou HEAD provavelmente criará um ruído significativo no registro, dificultando a identificação de informações úteis em arquivos de registro. O registro ao lidar com solicitações GET ou HEAD deve estar nos níveis de WARN ou ERROR quando algo deu errado ou nos níveis de DEBUG ou TRACE se informações mais detalhadas sobre solução de problemas forem úteis.

>[!CAUTION]
>
>Isso não se aplica ao log access.log-type para cada solicitação.

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

### Não use Exception.getMessage() como o primeiro parâmetro de uma instrução de registro {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**Chave**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Como prática recomendada, as mensagens de log devem fornecer informações contextuais sobre onde ocorreu uma exceção no aplicativo. Embora o contexto também possa ser determinado pelo uso de rastreamentos de pilha, em geral a mensagem de registro será mais fácil de ler e entender. Como resultado, ao registrar uma exceção, é uma prática ruim usar a mensagem de exceção como a mensagem de registro - a mensagem de exceção conterá o que deu errado, enquanto a mensagem de registro deve ser usada para informar ao leitor de log o que o aplicativo estava fazendo quando a exceção aconteceu. A mensagem de exceção continuará sendo registrada; ao especificar sua própria mensagem, os registros serão mais fáceis de entender.

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

### O logon em blocos catch deve estar no nível WARN ou ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Chave**: CQRules:CQBP-44—WrongLogLevelInCatchBlock

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Como o nome sugere, as exceções de Java devem ser sempre usadas em circunstâncias *excepcionais* . Como resultado, quando uma exceção é detectada, é importante garantir que as mensagens de log sejam registradas no nível apropriado - WARN ou ERROR. Isso garante que essas mensagens sejam exibidas corretamente nos registros.

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

**Chave**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Como mencionado, o contexto é crítico ao entender as mensagens de log. O uso de Exception.printStackTrace() faz com que **somente** o rastreamento da pilha seja enviado para o fluxo de erro padrão, perdendo todo o contexto. Além disso, em um aplicativo de vários processos, como o AEM, se várias exceções forem impressas usando esse método em paralelo, seus traços de pilha podem se sobrepor, o que gera confusão significativa. As exceções devem ser registradas somente pela estrutura de registro.

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

### Não produzir para Saída Padrão ou Erro Padrão {#do-not-output-to-standard-output-or-standard-error}

**Chave**: CQRules:CQBP-44—LogLevelConsolePrinters

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

O logon no AEM deve ser sempre feito por meio da estrutura de registro (SLF4J). A saída diretamente para a saída padrão ou fluxos de erro padrão perde as informações estruturais e contextuais fornecidas pela estrutura de registro e pode, em alguns casos, causar problemas de desempenho.

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

**Chave**: CQRules:CQBP-71

**Tipo**: Cheiro de código

**Gravidade**: Menor

**Desde**: Versão 2018.4.0

Em geral, os caminhos que começam com /libs e /apps não devem ser codificados, pois os caminhos aos quais se referem são mais comumente armazenados como caminhos relativos ao caminho de pesquisa Sling (que é definido como /libs,/apps por padrão). O uso do caminho absoluto pode apresentar defeitos sutis que só apareceriam posteriormente no ciclo de vida do projeto.

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


## Regras de conteúdo OakPAL {#oakpal-rules}

Encontre abaixo as verificações do OakPAL executadas pelo Cloud Manager.

>[!NOTE]
>O OakPAL é uma estrutura desenvolvida por um parceiro AEM (e vencedor do AEM Rockstar North America 2019) que valida pacotes de conteúdo usando um repositório Oak independente.

### Os pacotes do cliente não devem criar ou modificar nós em /libs {#oakpal-customer-package}

**Chave**: Caminhos Banidos

**Tipo**: Bug

**Gravidade**: Bloqueador

**Desde**: Versão 2019.6.0

É uma prática recomendada antiga que a árvore de conteúdo /libs no repositório de conteúdo do AEM seja considerada somente leitura pelos clientes. Modificar nós e propriedades em */libs* cria um risco significativo para atualizações principais e secundárias. As modificações em */libs* só devem ser feitas pela Adobe através de canais oficiais.

### Os pacotes não devem conter configurações OSGi duplicadas {#oakpal-package-osgi}

**Chave**: DuplicateOsgiConfigurations

**Tipo**: Bug

**Gravidade**: Major

**Desde**: Versão 2019.6.0

Um problema comum que ocorre em projetos complexos é onde o mesmo componente OSGi é configurado várias vezes. Isso cria uma ambiguidade sobre qual configuração será operável. Essa regra é &quot;sensível ao modo de execução&quot;, pois identificará apenas problemas em que o mesmo componente é configurado várias vezes no mesmo modo de execução (ou combinação de modos de execução).

#### Código não compatível {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Código compatível {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### As pastas Config e Install devem conter apenas nós OSGi {#oakpal-config-install}

**Chave**: ConfigAndInstallshouldOnlyContainOsgiNodes

**Tipo**: Bug

**Gravidade**: Major

**Desde**: Versão 2019.6.0

Por motivos de segurança, os caminhos que contêm */config/ e /install/* só podem ser lidos por usuários administrativos no AEM e devem ser usados apenas para configuração do OSGi e pacotes OSGi. Colocar outros tipos de conteúdo em caminhos que contêm esses segmentos resulta em comportamento de aplicativo que varia involuntariamente entre usuários administrativos e não administrativos.

Um problema comum é o uso de nós nomeados `config` nas caixas de diálogo do componente ou ao especificar a configuração do editor de rich text para edição em linha. Para resolver isso, o nó que está causando a ofensa deve ser renomeado para um nome compatível. Para a configuração do editor de Rich Text, use a `configPath` propriedade no `cq:inplaceEditing` nó para especificar o novo local.

#### Código não compatível {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Código compatível {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Os Pacotes Não Devem Sobrepor {#oakpal-no-overlap}

**Chave**: PackageOverlaps

**Tipo**: Bug

**Gravidade**: Major

**Desde**: Versão 2019.6.0

Semelhante aos *pacotes não devem conter configurações* OSGi duplicadas, esse é um problema comum em projetos complexos nos quais o mesmo caminho de nó é gravado por vários pacotes de conteúdo separados. Embora seja possível usar dependências de pacote de conteúdo para garantir um resultado consistente, é melhor evitar sobreposições completamente.