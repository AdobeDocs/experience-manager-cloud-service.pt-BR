---
title: Entenda seus resultados de teste - Serviços em nuvem
description: Entenda os resultados do teste - Serviços em nuvem
translation-type: tm+mt
source-git-commit: 4b79f7dd3a55e140869985faa644f7da1f62846c
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 4%

---


# Noções básicas dos resultados de teste {#understand-test-results}

As execuções de pipeline do Cloud Manager for Cloud Services oferecerão suporte à execução de testes executados em relação ao ambiente stage. Isso contrasta com os testes executados durante a etapa de criação e teste de unidade executados offline, sem acesso a nenhum ambiente AEM em execução.
Há dois tipos de testes executados neste contexto:
* Testes escritos pelo cliente
* Testes escritos pela Adobe

Ambos os tipos de testes são executados em uma infraestrutura de contêiner projetada para executar esses tipos de testes.


## Teste de qualidade de código {#code-quality-testing}

Como parte do pipeline, o código fonte é verificado para garantir que as implantações atendam a determinados critérios de qualidade. Atualmente, esta ação é implementada através de uma combinação de SonarQube e exame de nível de pacote de conteúdo utilizando OakPAL. Há mais de 100 regras que combinam regras genéricas do Java e regras específicas do AEM. A tabela a seguir resume a classificação dos critérios de teste:

| Nome | Definição | Categoria | Limite de falha |
|--- |--- |--- |--- |
| Classificação de segurança | A = 0 Vulnerabilidade <br/>B = pelo menos 1 Vulnerabilidade<br/> Menor C = pelo menos 1 Vulnerabilidade Principal <br/>D = pelo menos 1 Vulnerabilidade Crítica <br/>E = pelo menos 1 Vulnerabilidade Bloqueadora | Crítico | &lt; B |
| Classificação da confiabilidade | A = 0 Bug <br/>B = pelo menos 1 Bug Menor <br/>C = pelo menos 1 Bug Principal <br/>D = pelo menos 1 Bug Crítico E = pelo menos 1 Bug Bloqueador | Importante | &lt; C |
| Classificação da manutenção | O custo de correção excepcional para cheiros de código é: <br/><ul><li>&lt;=5% do tempo que já passou para o aplicativo, a classificação é A </li><li>entre 6 e 10%, a classificação é de </li><li>entre 11 e 20% a classificação é de C </li><li>entre 21 e 50% a classificação é um D</li><li>algo acima de 50% é um E</li></ul> | Importante | &lt; A |
| Cobertura | Uma combinação da cobertura da linha de teste da unidade e da cobertura da condição usando esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>em que: CT = condições que foram avaliadas como &#39;true&#39; pelo menos uma vez durante a execução de testes de unidade <br/>CF = condições que foram avaliadas como &#39;false&#39; pelo menos uma vez durante a execução de testes de unidade <br/>LC = linhas cobertas = lines_to_cover - uncovered_lines <br/><br/> B = número total de condições <br/>EL = número total de linhas executáveis (lines_to_cover) | Importante | &lt; 50% |
| Testes de unidade ignorados | Número de testes de unidade ignorados. | Informações | > 1 |
| Problemas em aberto | Tipos de edição geral - Vulnerabilidades, Erros e Cheiros de código | Informações | > 0 |
| Linhas Duplicadas | Número de linhas envolvidas em blocos duplicados. <br/>Para que um bloco de código seja considerado como duplicado: <br/><ul><li>**Projetos não Java:**</li><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem ser espalhados pelo menos em: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras línguas</li><li>**Projetos Java:**</li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas, independentemente do número de tokens e linhas.</li></ul> <br/>As diferenças no recuo, bem como nos literais de string, são ignoradas ao detectar duplicações. | Informações | > 1% |
| Compatibilidade do serviço em nuvem | Número de problemas identificados de Compatibilidade do serviço em nuvem. | Informações | > 0 |


>[!NOTE]
>
>Consulte Definições [de](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) métricas para obter definições mais detalhadas.

Você pode fazer download da lista de regras aqui [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx)

>[!NOTE]
>
>Para saber mais sobre as regras de qualidade de código personalizadas executadas pelo [!UICONTROL Cloud Manager], consulte Regras [de qualidade de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizadas.

### Lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identificará incorretamente questões que não são realmente problemáticas. Isso é conhecido como &quot;falso positivo&quot;.

Nesses casos, o código fonte pode ser anotado com a `@SuppressWarnings` anotação padrão Java que especifica a ID da regra como o atributo de anotação. Por exemplo, um problema comum é que a regra SonarQube para detectar senhas codificadas pode ser agressiva sobre como uma senha codificada é identificada.

Para ver um exemplo específico, esse código seria bastante comum em um projeto do AEM que tem código para se conectar a algum serviço externo:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

A SonarQube criará uma Vulnerabilidade do Bloqueador. Depois de revisar o código, você identifica que isso não é uma vulnerabilidade e pode anotar isso com a ID de regra apropriada.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

No entanto, por outro lado, se o código era realmente este:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Em seguida, a solução correta é remover a senha codificada.

>[!NOTE]
>
>Embora seja uma prática recomendada tornar a `@SuppressWarnings` anotação o mais específica possível, ou seja, anotar somente a declaração específica ou o bloco que está causando o problema, é possível fazer anotações em nível de classe.

## Gravação de testes funcionais {#writing-functional-tests}

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

Por exemplo, uma classe chamada `com.myco.tests.aem.ExampleIT` seria executada, mas uma classe chamada não `com.myco.tests.aem.ExampleTest` seria.

As classes de teste precisam ser testes JUnit normais. A infraestrutura de teste é projetada e configurada para ser compatível com as convenções usadas pela biblioteca de testes aem-testing-customers. Os desenvolvedores são fortemente incentivados a usar essa biblioteca e seguir suas práticas recomendadas. Consulte [Git Link](https://github.com/adobe/aem-testing-clients) para obter mais detalhes.

## Teste funcional personalizado {#custom-functional-test}

A etapa de teste Funcional personalizada no pipeline está sempre presente e não pode ser ignorada.

No entanto, se nenhum JAR de teste for produzido pela compilação, o teste será aprovado por padrão. Esta etapa é realizada imediatamente após a implantação do estágio.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. Esses registros não incluem os registros do processo de tempo de execução AEM real - eles podem ser acessados usando a funcionalidade normal de Download ou Logs de assinatura. Consulte [Acesso e gerenciamento de registros](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

## Execução de teste local {#local-test-execution}

Como as classes de teste são testes JUnit, elas podem ser executadas a partir de Java IDEs comuns como Eclipse, IntelliJ, NetBeans e assim por diante.

No entanto, ao executar esses testes necessariamente, será necessário definir uma variedade de propriedades do sistema esperadas pelos aem-testing-customers (e os clientes de teste Sling subjacentes).

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