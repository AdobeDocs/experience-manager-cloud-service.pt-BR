---
title: Entenda seus resultados de teste - Cloud Services
description: Entenda os resultados do teste - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 3%

---


# Noções básicas dos resultados de teste {#understand-test-results}

As execuções de pipeline do Cloud Manager para o Cloud Services oferecerão suporte à execução de testes que são executados no ambiente de preparo. Isso contrasta com os testes executados durante a etapa Build and Unit Testing, que são executados offline, sem acesso a nenhum ambiente AEM em execução.

Há três categorias amplas de testes suportadas pelo Cloud Manager para Cloud Services Pipeline:

1. [Teste de qualidade de código](#code-quality-testing)
1. [Teste funcional](#functional-testing)
1. [Teste de auditoria de conteúdo](#content-audit-testing)

Esses testes podem ser:

* Escrito pelo cliente
* Adobe
* Ferramenta de código aberto (alimentada pelo Farol do Google)

   >[!NOTE]
   > Os testes escritos pelo cliente e os testes por Adobe são executados em uma infraestrutura de contêiner projetada para executar esses tipos de testes.


## Teste de qualidade de código {#code-quality-testing}

Esta etapa avalia a qualidade do código do aplicativo. É o objetivo principal de um gasoduto de qualidade-código e é executado imediatamente após a etapa de construção em todos os gasodutos de não-produção e de produção.

Consulte [Configuração do seu pipeline](/help/implementing/cloud-manager/configure-pipeline.md) CI-CD para saber mais sobre diferentes tipos de pipeline.

### Noções básicas sobre regras de qualidade de código personalizadas {#understanding-code-quality-rules}

Em Teste de qualidade de código, o código fonte é verificado para garantir que as implantações atendam a determinados critérios de qualidade. Atualmente, esta ação é implementada através de uma combinação de SonarQube e exame de nível de pacote de conteúdo utilizando OakPAL. Há mais de 100 regras que combinam regras genéricas do Java e regras específicas do AEM. Algumas das regras específicas do AEM são criadas com base nas práticas recomendadas AEM engenharia e são chamadas de Regras [de qualidade de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizado.

Você pode baixar a lista de regras [aqui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

Os resultados desta etapa são fornecidos como *Classificação*. A tabela a seguir resume a classificação dos critérios de teste:

| Nome | Definição | Categoria | Limite de falha |
|--- |--- |--- |--- |
| Classificação de segurança | A = 0 Vulnerabilidade <br/>B = pelo menos 1 Vulnerabilidade<br/> Menor C = pelo menos 1 Vulnerabilidade Principal <br/>D = pelo menos 1 Vulnerabilidade Crítica <br/>E = pelo menos 1 Vulnerabilidade Bloqueadora | Crítico | &lt; B |
| Classificação da confiabilidade | A = 0 Bug <br/>B = pelo menos 1 Bug Menor <br/>C = pelo menos 1 Bug Principal <br/>D = pelo menos 1 Bug Crítico E = pelo menos 1 Bug Bloqueador | Importante | &lt; C |
| Classificação da manutenção | O custo de correção excepcional para cheiros de código é: <br/><ul><li>&lt;=5% do tempo que já passou para o aplicativo, a classificação é A </li><li>entre 6 e 10%, a classificação é de </li><li>entre 11 e 20% a classificação é de C </li><li>entre 21 e 50% a classificação é um D</li><li>algo acima de 50% é um E</li></ul> | Importante | &lt; A |
| Cobertura | Uma combinação da cobertura da linha de teste da unidade e da cobertura da condição usando esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>em que: CT = condições que foram avaliadas como &#39;true&#39; pelo menos uma vez durante a execução de testes de unidade <br/>CF = condições que foram avaliadas como &#39;false&#39; pelo menos uma vez durante a execução de testes de unidade <br/>LC = linhas cobertas = lines_to_cover - uncovered_lines <br/><br/> B = número total de condições <br/>EL = número total de linhas executáveis (lines_to_cover) | Importante | &lt; 50% |
| Testes de unidade ignorados | Número de testes de unidade ignorados. | Informações | > 1 |
| Problemas em aberto | Tipos de edição geral - Vulnerabilidades, Erros e Cheiros de código | Informações | > 0 |
| Linhas Duplicadas | Número de linhas envolvidas em blocos duplicados. <br/>Para que um bloco de código seja considerado como duplicado: <br/><ul><li>**Projetos não Java:**</li><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem ser espalhados pelo menos em: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras línguas</li><li>**Projetos Java:**</li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas, independentemente do número de tokens e linhas.</li></ul> <br/>As diferenças no recuo, bem como nos literais de string, são ignoradas ao detectar duplicações. | Informações | > 1% |
| Compatibilidade com Cloud Service | Número de problemas de compatibilidade de Cloud Service identificados. | Informações | > 0 |

>[!NOTE]
>
>Consulte Definições [de](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) métricas para obter definições mais detalhadas.


>[!NOTE]
>
>Para saber mais sobre as regras de qualidade de código personalizadas executadas pelo [!UICONTROL Cloud Manager], consulte Regras [de qualidade de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizadas.

### Lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identificará incorretamente questões que não são realmente problemáticas. Isso é conhecido como &quot;falso positivo&quot;.

Nesses casos, o código fonte pode ser anotado com a `@SuppressWarnings` anotação padrão Java que especifica a ID da regra como o atributo de anotação. Por exemplo, um problema comum é que a regra SonarQube para detectar senhas codificadas pode ser agressiva sobre como uma senha codificada é identificada.

Para ver um exemplo específico, esse código seria bastante comum em um projeto AEM que tem código para se conectar a algum serviço externo:

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

>[!NOTE]
>Embora não haja nenhuma etapa explícita de Teste de segurança, ainda existem regras de qualidade de código relacionadas à segurança avaliadas durante a etapa de qualidade do código. Consulte Visão geral [de segurança para obter AEM como Cloud Service](/help/security/cloud-service-security-overview.md) para saber mais sobre segurança no Cloud Service.

## Teste funcional {#functional-testing}

Os ensaios funcionais são classificados em dois tipos:

* Teste funcional do produto
* Teste funcional personalizado

### Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (TIs) sobre a funcionalidade principal em AEM (por exemplo, criação e replicação) que impedem que as alterações do cliente em seu código de aplicativo sejam implantadas se quebrar essa funcionalidade principal.

Os testes funcionais do produto são executados automaticamente sempre que um cliente implanta um novo código no Cloud Manager e não pode ser ignorado.

Consulte os testes [de funcionalidade do](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) produto para obter exemplos de testes.

### Teste funcional personalizado {#custom-functional-testing}

A etapa de teste Funcional personalizada no pipeline está sempre presente e não pode ser ignorada.

No entanto, se nenhum JAR de teste for produzido pela compilação, o teste será aprovado por padrão.

>[!NOTE]
>O botão **Baixar registro** permite acesso a um arquivo ZIP contendo os registros para o formulário detalhado de execução de teste. Esses registros não incluem os registros do processo de tempo de execução AEM real - eles podem ser acessados usando a funcionalidade normal de Download ou Logs de assinatura. Consulte [Acessar e gerenciar registros](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.


#### Gravação de testes funcionais {#writing-functional-tests}

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

#### Execução de teste local {#local-test-execution}

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


## Teste de auditoria de conteúdo {#content-audit-testing}

A auditoria de conteúdo é um recurso disponível nos pipelines de produção do Cloud Manager que é acionado pelo Lighthouse, uma ferramenta de código aberto do Google. Esse recurso é ativado em todos os pipelines de produção do Cloud Manager.

Ele valida o processo de implantação e ajuda a garantir que as alterações implantadas:

1. Atenda aos padrões básicos de desempenho, acessibilidade, práticas recomendadas, SEO (Search Engine Otimization) e PWA (Progressive Web App).

1. Não inclua regressões nessas dimensões.

A auditoria de conteúdo no Cloud Manager garante que a experiência digital dos usuários finais no site seja mantida com os mais altos padrões. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.

### Como entender os resultados da auditoria de conteúdo {#understanding-content-audit-results}

A Auditoria de conteúdo fornece resultados de testes em nível de página e agregação por meio da página de execução do pipeline de produção.

* As métricas de nível de agregação medem a pontuação média nas páginas que foram auditadas.
* As pontuações de nível de página individuais também estão disponíveis por meio da busca detalhada.
* Detalhes das pontuações estão disponíveis para ver quais são os resultados dos testes individuais, juntamente com orientações sobre como corrigir quaisquer problemas identificados durante a auditoria de conteúdo.
* Um histórico dos resultados do teste é persistente no Cloud Manager para que os clientes possam ver se as alterações que estão sendo introduzidas na execução do pipeline incluem quaisquer regressões da execução anterior.

#### Pontuações de agregação {#aggregate-scores}

Há uma pontuação de nível de agregação para cada tipo de teste (desempenho, acessibilidade, SEO, práticas recomendadas e PWA).

A pontuação do nível de agregação obtém a pontuação média das páginas que estão incluídas na execução. A alteração no nível da agregação representa a pontuação média das páginas na execução atual em comparação com a média das pontuações da execução anterior, mesmo se a coleção de páginas configuradas a serem incluídas tiver sido alterada entre as execuções.

O valor da métrica Alterar pode ser um dos seguintes:

* **Valor** positivo - as páginas melhoraram no teste selecionado desde a última execução do pipeline de produção

* **Valor** negativo - as páginas regrediram no teste selecionado desde a última execução do pipeline de produção

* **Sem alteração** - as páginas tiveram a mesma pontuação desde a última execução do pipeline de produção

* **N/D** - não havia pontuação anterior disponível para comparação

   ![](assets/content-audit-test1.png)

#### Pontuações no nível da página {#page-level-scores}

Ao analisar qualquer um dos testes, é possível visualizar uma pontuação mais detalhada no nível da página. O usuário poderá ver a pontuação das páginas individuais do teste específico junto com a alteração da hora anterior em que o teste foi executado.

Clicar nos detalhes de qualquer página individual fornecerá informações sobre os elementos da página que foram avaliados e orientações para corrigir problemas se as oportunidades de aprimoramento forem detectadas. Os detalhes dos testes e as orientações associadas são fornecidos pelo Google Lighthouse.

![](assets/page-level-scores.png)

