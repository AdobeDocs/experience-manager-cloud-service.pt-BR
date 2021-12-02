---
title: Teste funcional - Cloud Services
description: Teste funcional - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 02db915e114c2af8329eaddbb868045944a3574d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Teste funcional {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Os ensaios funcionais são classificados em três tipos: Teste funcional do produto, teste funcional personalizado e teste de interface personalizada"

Os ensaios funcionais são classificados em três tipos:


* [Teste funcional do produto](#product-functional-testing)
* [Teste funcional personalizado](#custom-functional-testing)
* [Teste de interface personalizada](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)

## Teste funcional do produto {#product-functional-testing}

Os Testes funcionais de produto são um conjunto de testes de integração HTTP (TIs) estáveis sobre a funcionalidade principal em AEM (por exemplo, criação e replicação) que impedem a implantação de alterações do cliente em seu código de aplicativo, caso quebre essa funcionalidade principal.

Os testes funcionais do produto são executados automaticamente sempre que um cliente implanta o novo código no Cloud Manager e não pode ser ignorado.

Consulte [Testes funcionais de produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) para os ensaios de amostras.

## Teste funcional personalizado {#custom-functional-testing}

A etapa Custom Functional testing no pipeline está sempre presente e não pode ser ignorada.

A build deve produzir zero ou um JARs de teste. Se produzir JARs de teste zero, a etapa de teste será aprovada por padrão. Se a build produzir mais de um JARs de teste, o JAR selecionado é não determinístico.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. Esses registros não incluem os registros do processo de tempo de execução AEM real - eles podem ser acessados usando a funcionalidade de Download ou Registros finais. Consulte [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.


## Gravação de testes funcionais {#writing-functional-tests}

Os testes funcionais escritos pelo cliente devem ser embalados como um arquivo JAR separado produzido pela mesma compilação Maven que os artefatos a serem implantados em AEM. Geralmente, seria um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente seria criado usando o maven-assembly-plugin usando o descritor jar-com-dependências.

Além disso, o JAR deve ter o cabeçalho do manifesto Cloud-Manager-TestType definido como integration-test. No futuro, espera-se que valores de cabeçalho adicionais sejam suportados. Um exemplo de configuração para o maven-assembly-plugin é:

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

Além disso, para excluir o código de teste da verificação de cobertura da verificação de código, o código de teste deve estar abaixo de um pacote chamado `it` (o filtro de exclusão de cobertura é `**/it/**/*.java`).

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes aem-testing-clients. Os desenvolvedores são altamente incentivados a usar essa biblioteca e seguir suas práticas recomendadas. Consulte [Link Git](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

## Execução de Teste Local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de IDEs Java mainstream como Eclipse, IntelliJ, NetBeans e assim por diante.

No entanto, ao executar esses testes, será necessário definir uma variedade de propriedades do sistema esperadas pelos clientes-teste do aem (e os clientes de teste do Sling subjacentes).

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
