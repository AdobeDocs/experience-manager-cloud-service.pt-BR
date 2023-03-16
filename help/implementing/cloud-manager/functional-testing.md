---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cd0b40ffa54eac0d7488b23329c4d2666c992da7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 67%

---


# Teste funcional {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código."

Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao [processo de implantação do AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantir a qualidade e a confiabilidade do seu código.

## Visão geral {#overview}

Existem três tipos diferentes de testes funcionais no AEM as a Cloud Service.

* [Teste funcional do produto](#product-functional-testing)
* [Teste funcional personalizado](#custom-functional-testing)
* [Testes de interface do usuário personalizados](#custom-ui-testing)

Para todos os testes funcionais, os resultados detalhados dos testes podem ser baixados como um arquivo `.zip` usando o botão **Baixar log de compilação** na tela de visão geral da compilação como parte do [processo de implantação.](/help/implementing/cloud-manager/deploy-code.md)

Esses logs não incluem os logs do processo de tempo de execução real do AEM. Para acessá-los, consulte o documento [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

Tanto os testes funcionais do produto quanto os testes funcionais personalizados de amostra se baseiam nos [Clientes de teste do AEM.](https://github.com/adobe/aem-testing-clients)

### Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (ITs) com funcionalidade principal no AEM, como tarefas de autoria e replicação. Esses testes são mantidos pela Adobe e têm como objetivo impedir a implantação de alterações no código de aplicativo personalizado, caso interrompa as funcionalidades principais.

* [Pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): Os testes funcionais do produto são executados automaticamente sempre que você implanta o novo código no Cloud Manager e não podem ser ignorados.
* [Pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): Os testes funcionais do produto podem ser opcionalmente selecionados para serem executados sempre que você executar o pipeline de não produção.

Os testes funcionais do produto são mantidos como um projeto de código aberto. Consulte os [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub para obter detalhes.

### Teste funcional personalizado {#custom-functional-testing}

Embora o teste funcional do produto seja definido pela Adobe, você pode criar seu próprio teste de qualidade para o seu aplicativo. Isso será executado como um teste funcional personalizado como parte do [pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) ou opcionalmente [pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para garantir a qualidade do seu aplicativo.

O teste funcional personalizado é executado tanto para implantações de código personalizadas quanto para atualizações de push, o que torna especialmente importante gravar bons testes funcionais que impeçam AEM alterações de código de quebrar seu código de aplicativo. A etapa de teste funcional personalizado está sempre presente e não pode ser ignorada.

### Testes de interface do usuário personalizados {#custom-ui-testing}

Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium compactados em uma imagem Docker, a fim de permitir uma ampla variedade de idiomas e estruturas, como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia desenvolvida na Selenium.

Consulte o documento [Testes de interface do usuário personalizados](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais detalhes.

## Introdução a testes funcionais {#getting-started-functional-tests}

Após a criação de um novo repositório de código no Cloud Manager, um `it.tests` é criada automaticamente com casos de teste de amostra.

>[!NOTE]
>
>Se o repositório foi criado antes da criação automática do Cloud Manager `it.tests` , você também pode gerar a versão mais recente usando o [AEM Arquétipo de projeto.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

Depois de ter o conteúdo da `it.tests` use-a como base para seus próprios testes e, em seguida:

1. [Desenvolva seus casos de teste.](#writing-functional-tests)
1. [Execute os testes localmente.](#local-test-execution)
1. Confirme seu código no repositório do Cloud Manager e execute um pipeline do Cloud Manager.

## Gravação de testes funcionais personalizados {#writing-functional-tests}

As mesmas ferramentas que a Adobe usa para gravar testes funcionais do produto podem ser usadas para gravar seus testes funcionais personalizados. Use os [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub como exemplo para gravar seus testes.

O código do teste funcional personalizado é o código Java localizado na pasta `it.tests` do seu projeto. Ele deve produzir um único JAR com todos os testes funcionais. Se a compilação produzir mais de um JAR de teste, o JAR selecionado será não determinístico. Se produzir zero JAR de teste, a etapa de teste será aprovada por padrão. [Consulte o Arquétipo de Projetos AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para ver exemplos de testes.

Os testes são executados em uma infraestrutura de teste mantida pela Adobe, incluindo pelo menos duas instâncias de autoria, duas instâncias de publicação e uma configuração de dispatcher. Portanto, os testes funcionais personalizados são executados em relação a toda a pilha do AEM.

### Estrutura dos testes funcionais {#functional-tests-structure}

Os testes funcionais personalizados devem ser empacotados como um arquivo JAR separado produzido pela mesma compilação Maven que os artefatos a serem implantados no AEM. Geralmente, é um módulo Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente é criado usando o `maven-assembly-plugin` com o descritor `jar-with-dependencies`.

Além disso, o JAR deve ter a o cabeçalho de manifesto `Cloud-Manager-TestType` definido como `integration-test`.

O código a seguir é um exemplo de configuração de `maven-assembly-plugin`.

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

Por exemplo, uma classe chamada `com.myco.tests.aem.it.ExampleIT` seria executada, mas uma chamada `com.myco.tests.aem.it.ExampleTest` não.

Além disso, para excluir o código de teste da verificação de abrangência da verificação de código, o código de teste deve estar abaixo de um pacote chamado `it` (o filtro de exclusão de abrangência é `**/it/**/*.java`).

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes `aem-testing-clients`. Os desenvolvedores são altamente incentivados a usar essa biblioteca e seguir suas práticas recomendadas.

Consulte o [`aem-testing-clients` repositório GitHub](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

>[!TIP]
>
>[Assista a este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) sobre como você pode usar testes funcionais personalizados para melhorar a confiança nos seus pipelines de CI/CD.

### Execução local de testes {#local-test-execution}

Antes de ativar testes funcionais em um pipeline do Cloud Manager, é recomendável executar os testes funcionais localmente usando o [AEM SDK as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) ou uma instância real AEM as a Cloud Service.

#### Pré-requisitos {#prerequisites}

Os testes no Cloud Manager serão executados com um usuário administrador técnico.

Para executar os testes funcionais a partir de sua máquina local, crie um usuário com permissões de administrador para obter o mesmo comportamento.

#### Executando em um IDE {#running-in-an-ide}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de IDEs Java mainstream como Eclipse, IntelliJ e NetBeans. Como os testes funcionais do produto e os testes funcionais personalizados se baseiam na mesma tecnologia, ambos podem ser executados localmente copiando os testes de produto aos seus testes personalizados.

No entanto, ao executá-los, será necessário definir uma variedade de propriedades do sistema esperadas pela biblioteca `aem-testing-clients` (e os Clientes de teste Sling subjacentes).

As propriedades do sistema são mostradas a seguir.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### Execução de todos os testes usando Maven {#using-maven}

1. Abra um shell e navegue até o `it.tests` no seu repositório.

1. Execute o seguinte comando fornecendo os parâmetros necessários para iniciar os testes usando Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
