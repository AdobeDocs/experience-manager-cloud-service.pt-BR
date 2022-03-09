---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação as a Cloud Service AEM para garantir a qualidade e confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---


# Teste funcional {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação as a Cloud Service AEM para garantir a qualidade e confiabilidade do seu código."

Saiba mais sobre os três diferentes tipos de testes funcionais incorporados ao [AEM processo de implantação as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantir a qualidade e confiabilidade do seu código.

## Visão geral {#overview}

Existem três tipos diferentes de testes funcionais em AEM as a Cloud Service.

* [Teste funcional do produto](#product-functional-testing)
* [Teste funcional personalizado](#custom-functional-testing)
* [Teste de interface personalizada](#custom-ui-testing)

Para todos os testes funcionais, os resultados detalhados dos testes podem ser baixados como uma `.zip` usando o **Baixar log de criação** na tela de visão geral da criação como parte do [processo de implantação.](/help/implementing/cloud-manager/deploy-code.md) Esses logs não incluem os logs do processo de tempo de execução AEM real. Para acessar esses logs, consulte o documento [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

## Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (TIs) de funcionalidade principal em AEM como tarefas de criação e replicação. Esses testes impedem que as alterações do cliente no código de aplicativo personalizado sejam implantadas se quebrar a funcionalidade principal.

Os testes funcionais do produto são executados automaticamente sempre que você implanta o novo código no Cloud Manager e não podem ser ignorados.

Consulte [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub para testes de amostra.

## Teste funcional personalizado {#custom-functional-testing}

A etapa de teste funcional personalizada no pipeline está sempre presente e não pode ser ignorada.

A build deve produzir zero ou um JARs de teste. Se produzir JARs de teste zero, a etapa de teste será aprovada por padrão. Se a build produzir mais de um JARs de teste, o JAR selecionado é não determinístico.

### Gravação de testes funcionais {#writing-functional-tests}

Os testes funcionais personalizados devem ser embalados como um arquivo JAR separado produzido pela mesma compilação Maven que os artefatos a serem implantados no AEM. Geralmente, seria um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente seria criado usando o `maven-assembly-plugin` usando o `jar-with-dependencies` descritor.

Além disso, o JAR deve ter a variável `Cloud-Manager-TestType` cabeçalho do manifesto definido como `integration-test`. No futuro, espera-se que valores de cabeçalho adicionais sejam suportados.

Este é um exemplo de configuração para a variável `maven-assembly-plugin`.

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

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela `aem-testing-clients` biblioteca de teste. Os desenvolvedores são altamente incentivados a usar essa biblioteca e seguir suas práticas recomendadas.

Consulte a [`aem-testing-clients` GitHub repo](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

## Teste de interface personalizada {#custom-ui-testing}

O teste da interface personalizada é um recurso opcional que permite criar e executar automaticamente testes da interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium).

Consulte o documento [Teste de interface personalizada](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais informações.

## Execução de Teste Local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de IDEs Java mainstream como Eclipse, IntelliJ, NetBeans e assim por diante.

No entanto, ao executar esses testes, será necessário definir uma variedade de propriedades do sistema esperadas pela `aem-testing-clients` (e os Clientes de teste Sling subjacentes).

As propriedades do sistema são as seguintes.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
