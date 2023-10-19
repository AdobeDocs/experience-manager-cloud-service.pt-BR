---
title: Testes funcionais do Java&trade
description: Saiba como preparar testes funcionais do Java&trade para o AEM as a Cloud Service
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
source-git-commit: 0109cea1be85e647fb6c04dde4714b162bdc75a5
workflow-type: ht
source-wordcount: '844'
ht-degree: 100%

---

# Teste funcional de Java™

Saiba como preparar testes funcionais de Java™ para o AEM as a Cloud Service

## Introdução aos testes funcionais {#getting-started-functional-tests}

Após a criação de um novo repositório de código no Cloud Manager, uma pasta chamada `it.tests` é criada automaticamente com exemplos de casos de teste.

>[!NOTE]
>
>Se o repositório foi criado antes do Cloud Manager criar automaticamente as pastas `it.tests`, você também poderá gerar a versão mais recente usando o [Arquétipo de projeto do AEM.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

Depois de obter o conteúdo da pasta `it.tests`, você poderá usá-la como base para os seus próprios testes e, em seguida:

1. [Desenvolver os seus casos de teste.](#writing-functional-tests)
1. [Executar os testes localmente.](#local-test-execution)
1. Confirmar seu código no repositório do Cloud Manager e executar um pipeline do Cloud Manager.

## Gravação de testes funcionais personalizados {#writing-functional-tests}

As mesmas ferramentas que a Adobe usa para gravar testes funcionais do produto podem ser usadas para gravar seus testes funcionais personalizados. Use os [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub como exemplo para gravar seus testes.

O código do teste funcional personalizado é o código Java™ localizado na pasta `it.tests` do projeto. Ele deve produzir um único JAR com todos os testes funcionais. Se a compilação produzir mais de um JAR de teste, o JAR selecionado será não determinístico. Se produzir zero JAR de teste, a etapa de teste será aprovada por padrão. [Consulte o Arquétipo de Projetos AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para ver exemplos de testes.

Os testes são executados na infraestrutura de testes mantida pela Adobe, incluindo pelo menos duas instâncias de autor, duas instâncias de publicação e uma configuração do Dispatcher. Essa configuração significa que seus testes funcionais personalizados são executados em toda a pilha do AEM.

### Estrutura de testes funcionais {#functional-tests-structure}

Os testes funcionais personalizados precisam ser compactados como um arquivo JAR separado produzido pela mesma build do Maven que os artefatos a serem implantados no AEM. Em geral, essa build seria um módulo do Maven separado. O arquivo JAR resultante deve conter todas as dependências necessárias e geralmente é criado usando o `maven-assembly-plugin` com o descritor `jar-with-dependencies`.

Além disso, o JAR deve ter a o cabeçalho de manifesto `Cloud-Manager-TestType` definido como `integration-test`.

O código a seguir é um exemplo de configuração de `maven-assembly-plugin`.

```XML
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
</build>
```

Neste arquivo JAR, os nomes de classe dos testes reais a serem executados devem terminar em `IT`.

Por exemplo, uma classe chamada `com.myco.tests.aem.it.ExampleIT` seria executada, mas uma chamada `com.myco.tests.aem.it.ExampleTest` não.

Além disso, para excluir o código de teste da verificação de abrangência da verificação de código, o código de teste deve estar abaixo de um pacote chamado `it` (o filtro de exclusão de abrangência é `**/it/**/*.java`).

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes `aem-testing-clients`. Os desenvolvedores são incentivados a usar essa biblioteca e a seguir suas práticas recomendadas.

Consulte [`aem-testing-clients`repositório do GitHub](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

>[!TIP]
>
>[Assista a este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) sobre como usar testes funcionais personalizados para melhorar a confiança nos seus pipelines de CI/CD.

### Pré-requisitos {#prerequisites}

1. Os testes no Cloud Manager são executados usando um usuário administrador técnico.

>[!NOTE]
>
>Para executar os testes funcionais no computador local, crie um usuário com permissões de administrador para alcançar o mesmo comportamento.

1. A infraestrutura em container com escopo para testes funcionais apresenta os seguintes limites:


| Tipo | Valor | Descrição |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | Quantidade de tempo de CPU reservado por execução de teste |
| Memória | 0.5 Gi | Quantidade de memória alocada para o teste, valor em gibibytes |
| Tempo limite | 30 min | A duração após a qual o teste é encerrado. |
| Duração recomendada | 15 min | A Adobe recomenda preparar os testes para não demorar mais do que esse tempo. |

>[!NOTE]
>
> Caso precise de mais recursos, crie um chamado no Atendimento ao cliente e descreva seu caso de uso. A equipe da Adobe analisará sua solicitação e fornecerá a assistência apropriada.


### Execução local de testes {#local-test-execution}

Antes de ativar testes funcionais em um pipeline do Cloud Manager, é recomendável executar os testes funcionais localmente usando o [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) ou uma instância real do AEM as a Cloud Service.

#### Executando em um IDE {#running-in-an-ide}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir dos principais IDEs Java™, como Eclipse, IntelliJ, e NetBeans. Como os testes funcionais do produto e os testes funcionais personalizados se baseiam na mesma tecnologia, ambos podem ser executados localmente copiando os testes de produto aos seus testes personalizados.

No entanto, ao executá-los, será necessário definir uma variedade de propriedades do sistema esperadas pela biblioteca `aem-testing-clients` (e os Clientes de teste do Sling subjacentes).

As propriedades do sistema são mostradas a seguir.

| Propriedade | Descrição | Exemplo |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | quantidade de instâncias para corresponder ao serviços na nuvem deve ser definida como `2` | `2` |
| `sling.it.instance.url.1` | deve ser definido como o URL do autor | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | o modo de execução da primeira instância, deve ser definido como `author` | `author` |
| `sling.it.instance.adminUser.1` | deve ser definido como o usuário administrador do autor. | `admin` |
| `sling.it.instance.adminPassword.1` | deve ser definido como a senha do administrador do autor. |                         |
| `sling.it.instance.url.2` | deve ser definido como o URL de publicação | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | o modo de execução da segunda instância, deve ser definido como `publish` | `publish` |
| `sling.it.instance.adminUser.2` | deve ser definido como usuário administrador de publicação. | `admin` |
| `sling.it.instance.adminPassword.2` | deve ser definido como senha do administrador de publicação. |                         |



#### Execução de todos os testes usando Maven {#using-maven}

1. Abra um shell e navegue até a pasta `it.tests` no seu repositório.

1. Execute o seguinte comando fornecendo os parâmetros necessários para iniciar os testes usando o Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
