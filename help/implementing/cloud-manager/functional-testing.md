---
title: Functional Testing - Cloud Services
description: Functional Testing - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 778fa187df675eada645c73911e6f02e8a112753
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Teste funcional {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Functional Testing"
>abstract="Os ensaios funcionais são classificados em três tipos: Teste funcional do produto, teste funcional personalizado e teste de interface personalizada"

Os ensaios funcionais são classificados em três tipos:


* Teste funcional do produto
* Teste funcional personalizado
* Teste de interface personalizada

## Teste funcional do produto {#product-functional-testing}

Product Functional Tests are a set of stable HTTP integration tests (ITs) around core functionality in AEM (for example, authoring and replication) that prevent customer changes to their application code from being deployed if it breaks this core functionality.

Product Functional Tests run automatically whenever a customer deploys new code to Cloud Manager and cannot be skipped.

Consulte [Testes funcionais de produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) para os ensaios de amostras.

## Custom Functional Testing {#custom-functional-testing}

The Custom Functional testing step in the pipeline is always present and cannot be skipped.

A build deve produzir zero ou um JARs de teste. Se produzir JARs de teste zero, a etapa de teste será aprovada por padrão. If the build produces more than one test JARs, which JAR is selected is non-deterministic.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. These logs do not include the logs of the actual AEM runtime process – those can be accessed using the regular Download or Tail Logs functionality. Consulte [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.


## Writing Functional Tests {#writing-functional-tests}

Customer-written functional tests must be packaged as a separate JAR file produced by the same Maven build as the artifacts to be deployed to AEM. Geralmente, seria um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente seria criado usando o maven-assembly-plugin usando o descritor jar-com-dependências.

In addition, the JAR must have the Cloud-Manager-TestType manifest header set to integration-test. In the future, it is expected that additional header values will be supported. Um exemplo de configuração para o maven-assembly-plugin é:

```java
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
```

Neste arquivo JAR, os nomes de classe dos testes reais a serem executados devem terminar em `IT`.

Por exemplo, uma classe chamada `com.myco.tests.aem.it.ExampleIT` seria executada, mas uma classe chamada `com.myco.tests.aem.it.ExampleTest` não.

Furthermore, to exclude test code from the coverage check of the code scanning, the test code must be below a package named `it` (the coverage exclusion filter is `**/it/**/*.java`).

The test classes need to be normal JUnit tests. The test infrastructure is designed and configured to be compatible with the conventions used by the aem-testing-clients test library. Developers are strongly encouraged to use this library and follow its best practices. Consulte [Link Git](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

## Execução de Teste Local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de IDEs Java mainstream como Eclipse, IntelliJ, NetBeans e assim por diante.

However, when running these tests, it will be necessary to set a variety of system properties expected by the aem-testing-clients (and the underlying Sling Testing Clients).

The system properties are as follows:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
