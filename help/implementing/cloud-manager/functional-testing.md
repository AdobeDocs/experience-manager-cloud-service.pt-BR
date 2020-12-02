---
title: Teste funcional - Cloud Services
description: Teste funcional - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# Teste funcional {#functional-testing}

Os ensaios funcionais são classificados em dois tipos:

* Teste funcional do produto
* Teste funcional personalizado

## Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (TIs) sobre a funcionalidade principal em AEM (por exemplo, criação e replicação) que impedem que as alterações do cliente em seu código de aplicativo sejam implantadas se quebrar essa funcionalidade principal.

Os testes funcionais do produto são executados automaticamente sempre que um cliente implanta um novo código no Cloud Manager e não pode ser ignorado.

Consulte [Testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) para obter exemplos de testes.

## Teste funcional personalizado {#custom-functional-testing}

A etapa de teste Funcional personalizada no pipeline está sempre presente e não pode ser ignorada.

No entanto, se nenhum JAR de teste for produzido pela compilação, o teste será aprovado por padrão.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. Esses registros não incluem os registros do processo de tempo de execução AEM real - eles podem ser acessados usando a funcionalidade normal de Download ou Logs de assinatura. Consulte [Acesso e gerenciamento de registros](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.


### Gravando testes funcionais {#writing-functional-tests}

Os testes funcionais escritos pelo cliente devem ser empacotados como um arquivo JAR separado produzido pela mesma compilação Maven que os artefatos a serem implantados no AEM. Geralmente, este seria um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente seria criado usando o plug-in maven-assembly usando o descritor jar com dependências.

Além disso, o JAR deve ter o cabeçalho do manifesto Cloud-Manager-TestType definido como integration-test. No futuro, espera-se que valores de cabeçalho adicionais sejam suportados. Um exemplo de configuração para o plug-in maven-assembly é:

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

Neste arquivo JAR, os nomes de classe dos testes reais a serem executados devem terminar na TI.

Por exemplo, uma classe chamada `com.myco.tests.aem.ExampleIT` seria executada, mas uma classe chamada `com.myco.tests.aem.ExampleTest` não seria executada.

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes aem-testing-customers. Os desenvolvedores são fortemente incentivados a usar essa biblioteca e seguir suas práticas recomendadas. Consulte [Git Link](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

### Execução de teste local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de Java IDEs comuns como Eclipse, IntelliJ, NetBeans e assim por diante.

No entanto, ao executar esses testes, será necessário definir uma variedade de propriedades do sistema esperadas pelos aem-testing-customers (e os clientes de teste Sling subjacentes).

As propriedades do sistema são as seguintes:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

