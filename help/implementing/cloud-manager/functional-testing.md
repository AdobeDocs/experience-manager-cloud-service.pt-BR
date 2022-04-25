---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação as a Cloud Service AEM para garantir a qualidade e confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: f8d5b94d176dfbd5bcecf552f974dc77c5afe4e2
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

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

Para todos os testes funcionais, os resultados detalhados dos testes podem ser baixados como uma `.zip` usando o **Baixar log de criação** na tela de visão geral da criação como parte do [processo de implantação.](/help/implementing/cloud-manager/deploy-code.md)

Esses logs não incluem os logs do processo de tempo de execução AEM real. Para acessar esses logs, consulte o documento [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

Tanto os testes funcionais do produto quanto os testes funcionais personalizados da amostra são baseados no [AEM Testando clientes.](https://github.com/adobe/aem-testing-clients)

## Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (TIs) de funcionalidade principal em AEM como tarefas de criação e replicação. Esses testes são mantidos pelo Adobe e têm como objetivo impedir a implantação de alterações no código de aplicativo personalizado, caso quebre as funcionalidades principais.

Os testes funcionais do produto são executados automaticamente sempre que você implanta o novo código no Cloud Manager e não podem ser ignorados.

Os testes funcionais do produto são mantidos como um projeto de código aberto. Consulte [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub para obter detalhes.

## Teste funcional personalizado {#custom-functional-testing}

Embora o teste funcional do produto seja definido pelo Adobe, você pode criar seu próprio teste de qualidade para seu próprio aplicativo. Isso será executado como um teste funcional personalizado como parte do pipeline de produção para garantir a qualidade do seu aplicativo.

O teste funcional personalizado é executado tanto para implantações de código personalizadas quanto para atualizações de push, o que torna especialmente importante gravar bons testes funcionais que impeçam AEM alterações de código de quebrar seu código de aplicativo. A etapa de teste funcional personalizada está sempre presente e não pode ser ignorada.

### Gravação de testes funcionais personalizados {#writing-functional-tests}

As mesmas ferramentas que o Adobe usa para escrever testes funcionais de produto podem ser usadas para escrever seus testes funcionais personalizados. Use o [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub como um exemplo de como escrever seus testes.

O código para o teste funcional personalizado é o código Java localizado na variável `it.tests` pasta do seu projeto. Ele deve produzir um único JAR com todos os testes funcionais. Se a build produzir mais de um JAR de teste, o JAR selecionado é não determinístico. Se produzir JARs de teste zero, a etapa de teste será aprovada por padrão. [Consulte o Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para os ensaios de amostras.

Os testes são executados em uma infraestrutura de teste Adobe mantida, incluindo pelo menos duas instâncias de autor, duas instâncias de publicação e uma configuração de dispatcher. Isso significa que seus testes funcionais personalizados são executados em relação a toda a pilha de AEM.

Os testes funcionais personalizados devem ser embalados como um arquivo JAR separado produzido pela mesma compilação Maven que os artefatos a serem implantados no AEM. Geralmente, seria um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente seria criado usando o `maven-assembly-plugin` usando o `jar-with-dependencies` descritor.

Além disso, o JAR deve ter a variável `Cloud-Manager-TestType` cabeçalho do manifesto definido como `integration-test`.

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

>[!TIP]
>
>[Assista a este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) sobre como você pode usar testes funcionais personalizados para melhorar sua confiança nos seus pipelines de CI/CD.

## Teste de interface personalizada {#custom-ui-testing}

O teste da interface personalizada é um recurso opcional que permite criar e executar automaticamente testes da interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium).

Consulte o documento [Teste de interface personalizada](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais informações.

## Execução de Teste Local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de IDEs Java mainstream como Eclipse, IntelliJ, NetBeans e assim por diante. Como os testes funcionais do produto e os testes funcionais personalizados são baseados na mesma tecnologia, ambos podem ser executados localmente copiando os testes do produto em seus testes personalizados.

No entanto, ao executar esses testes, será necessário definir uma variedade de propriedades do sistema esperadas pela `aem-testing-clients` (e os Clientes de teste Sling subjacentes).

As propriedades do sistema são as seguintes.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
