---
title: Teste funcional - Cloud Services
description: Teste funcional - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cf2e206b0ad186e0f4caa4a2ec9c34faf2078b76
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# Teste funcional {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Os ensaios funcionais são classificados em três tipos: Teste funcional do produto, teste funcional personalizado e teste de interface personalizada"

Os ensaios funcionais são classificados em três tipos:


* Teste funcional do produto
* Teste funcional personalizado
* Teste de interface personalizada

## Teste funcional do produto {#product-functional-testing}

Os Testes funcionais de produto são um conjunto de testes de integração HTTP (TIs) estáveis sobre a funcionalidade principal em AEM (por exemplo, criação e replicação) que impedem a implantação de alterações do cliente em seu código de aplicativo, caso quebre essa funcionalidade principal.

Os testes funcionais do produto são executados automaticamente sempre que um cliente implanta o novo código no Cloud Manager e não pode ser ignorado.

Consulte [Teste funcional do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) para obter amostras de teste.

## Teste funcional personalizado {#custom-functional-testing}

A etapa Custom Functional testing no pipeline está sempre presente e não pode ser ignorada.

No entanto, se nenhum JAR de teste for produzido pela build, o teste será aprovado por padrão.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. Esses registros não incluem os registros do processo de tempo de execução AEM real - eles podem ser acessados usando a funcionalidade de Download ou Registros finais. Consulte [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

## Teste de interface personalizada {#custom-ui-testing}

O AEM fornece aos clientes um conjunto integrado de portas de qualidade do Cloud Manager para garantir atualizações tranquilas em seus aplicativos. Em particular, os portões de teste de TI já permitem que os clientes criem e automatizem seus próprios testes que usam AEM APIs.

O recurso de teste da interface personalizada é um recurso opcional [Opt-in do cliente](#customer-opt-in) que permite que nossos clientes criem e executem automaticamente testes da interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). Saiba mais sobre como criar interface do usuário e gravar testes da interface do usuário a partir daqui. Além disso, um projeto de Testes de interface pode ser facilmente gerado usando o Arquétipo de projeto AEM.

Os clientes podem criar testes personalizados (via GIT) e conjunto de testes para interface do usuário. O teste da interface do usuário será executado como parte de uma porta de qualidade específica para cada pipeline do Cloud Manager com suas informações específicas de etapa e feedback. Quaisquer testes da interface do usuário, incluindo regressão e novas funcionalidades, permitirão que os erros sejam detectados e relatados no contexto do cliente.

Os testes da interface do usuário do cliente são executados automaticamente no pipeline de Produção na etapa &quot;Teste da interface personalizada&quot;.

Diferentemente do Teste Funcional Personalizado, que são testes HTTP escritos em java, os testes da interface do usuário podem ser uma imagem do docker com testes escritos em qualquer idioma, desde que sigam as convenções definidas em [Criando Testes da Interface do Usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>É recomendável seguir a estrutura e o idioma *(js e wdio)* convenientemente fornecidos no [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) como ponto de partida.

### Opt-in do cliente {#customer-opt-in}

Para que os testes da interface do usuário sejam criados e executados, os clientes precisam &quot;aceitar&quot; adicionando um arquivo ao repositório de código, no submódulo maven para testes da interface do usuário (ao lado do arquivo pom.xml do submódulo de testes da interface do usuário) e garantir que esse arquivo esteja na raiz do arquivo criado `tar.gz`.

*Nome do arquivo*: `testing.properties`

*Conteúdo*:  `ui-tests.version=1`

Se isso não estiver no arquivo `tar.gz` criado, a interface do usuário testa a criação e as execuções serão ignoradas

Para adicionar o arquivo `testing.properties` no artefato criado, adicione uma instrução `include` no arquivo `assembly-ui-test-docker-context.xml` (no submódulo de testes da interface do usuário):

    &quot;
    [..]
    &lt;includes>
    &lt;include>&lt;/include>
    &lt;include>Dockerfilewait-for-grid.&lt;/include>
    &lt;include>shtesting.properties&lt;/include> &lt;!- módulo de teste de aceitação no Cloud Manager —>
    &lt;/include>
    [...]
    &quot;

>[!NOTE]
>Os pipelines de produção criados antes de 10 de fevereiro de 2021 precisarão ser atualizados para usar os testes da interface do usuário, conforme descrito nesta seção. Essencialmente, isso significa que o Usuário deve editar o pipeline de Produção e clicar em **Salvar** na interface do usuário, mesmo que nenhuma alteração tenha sido feita.
>Consulte [Configuração do pipeline de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) para saber mais sobre a configuração do pipeline.

### Gravação de testes funcionais {#writing-functional-tests}

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

Dentro desse arquivo JAR, os nomes de classe dos testes reais a serem executados devem terminar em TI.

Por exemplo, uma classe chamada `com.myco.tests.aem.ExampleIT` seria executada, mas uma classe chamada `com.myco.tests.aem.ExampleTest` não seria executada.

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes aem-testing-clients. Os desenvolvedores são altamente incentivados a usar essa biblioteca e seguir suas práticas recomendadas. Consulte [Git Link](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

### Execução de Teste Local {#local-test-execution}

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
