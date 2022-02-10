---
title: Teste de qualidade do código
description: Saiba como o teste de qualidade de código de pipelines funciona e como ele pode melhorar a qualidade de suas implantações.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: ca3c1f255b8441a8d376a55a5353d58848384b8b
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 2%

---

# Teste de qualidade do código {#code-quality-testing}

Saiba como o teste de qualidade de código de pipelines funciona e como ele pode melhorar a qualidade de suas implantações.

>[!CONTEXTUALHELP]
>
>id="aemcloud_nonbpa_codequalitytests"
>title="Code Quality Testing"
>abstract="Code quality testing evaluates your application code based on a set of quality rules. It is the primary purpose of a code-quality only pipeline and is executed immediately following the build step in all production and non-production pipelines."

## Introdução {#introduction}

O teste de qualidade do código avalia o código do aplicativo com base em um conjunto de regras de qualidade. É o objetivo principal de um pipeline somente de qualidade de código e é executado imediatamente após a etapa de build em todos os pipelines de produção e não produção.

Consulte o documento [Configurar seu pipeline de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para saber mais sobre diferentes tipos de pipelines.

## Regras de qualidade do código {#understanding-code-quality-rules}

O teste de qualidade do código verifica o código-fonte para garantir que ele atenda a determinados critérios de qualidade. Esta é implementada por uma combinação de SonarQube e exame ao nível do pacote de conteúdo usando OakPAL. Há mais de 100 regras, combinando regras genéricas do Java e regras específicas de AEM. Algumas das regras específicas do AEM são criadas com base nas práticas recomendadas da engenharia AEM e são chamadas de [regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
Você pode baixar a lista completa de regras [com este link.](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### Classificações de três níveis {#three-tiered-gate}

Os problemas identificados por testes de qualidade do código são atribuídos a uma de três categorias.

* **Crítico** - São questões que causam uma falha imediata do pipeline.

* **Importante** - Esses são problemas que fazem com que o pipeline entre no estado pausado. Um gerente de implantação, gerente de projeto ou proprietário de negócios pode substituir os problemas, caso o pipeline continue, ou pode aceitar os problemas, caso o pipeline pare com uma falha.

* **Informações** - Trata-se de questões que são fornecidas exclusivamente para fins informativos e não têm impacto na execução do pipeline

Os resultados desta etapa são fornecidos como **Classificações**.

A tabela a seguir resume as notações e os limiares de falha para cada uma das categorias críticas, importantes e informativas.

| Nome | Definição | Categoria | Limite de Falhas |
|--- |--- |--- |--- |
| Classificação de segurança | A = Sem vulnerabilidades <br/>B = Pelo menos 1 vulnerabilidade menor<br/> C = Pelo menos 1 grande vulnerabilidade <br/>D = Pelo menos 1 vulnerabilidade crítica <br/>E = Pelo menos 1 vulnerabilidade do bloqueador | Crítico | &lt; B |
| Classificação da confiabilidade | A = Sem bugs <br/>B = Pelo menos 1 erro secundário <br/>C = Pelo menos 1 grande erro <br/>D = Pelo menos 1 bug crítico<br>E = Pelo menos 1 bug do bloqueador | Crítico | &lt; D |
| Classificação da capacidade de manutenção | Definido pelo custo de remediação pendente do código como uma porcentagem do tempo que já passou para o aplicativo<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | Importante | &lt; A |
| Cobertura | Definida por uma combinação de cobertura da linha de ensaio unitária e cobertura da condição utilizando a fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Condições que foram avaliadas como `true` pelo menos uma vez durante a execução dos ensaios da unidade</li><li>`CF` = Condições que foram avaliadas como `false` pelo menos uma vez durante a execução dos ensaios da unidade</li><li>`LC` = Linhas cobertas = lines_to_cover - linhas_não cobertas</li><li>`B` = número total de condições</li><li>`EL` = número total de linhas executáveis (lines_to_cover)</li></ul> | Importante | &lt; 50% |
| Testes de Unidade Ignorados | Número de testes de unidade ignorados | Informações | > 1 |
| Problemas em aberto | Tipos de problemas gerais - Vulnerabilidades, Erros e Cheiros de código | Informações | > 0 |
| Linhas Duplicadas | Definido como o número de linhas envolvidas em blocos duplicados. Um bloco de código é considerado duplicado nas condições a seguir.<br>Projetos não Java:<ul><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem ser distribuídos pelo menos: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras línguas</li></ul>Projetos Java:<ul></li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas independentemente do número de tokens e linhas.</li></ul>As diferenças no recuo, bem como nos literais de string são ignoradas ao detectar duplicatas. | Informações | > 1% |
| Compatibilidade Cloud Service | Número de problemas de compatibilidade do serviço em nuvem identificados | Informações | > 0 |

>[!NOTE]
Consulte [Definições de métrica da SonarQube](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obter definições mais detalhadas.

>[!NOTE]
Para saber mais sobre as regras de qualidade do código personalizado executadas pelo [!UICONTROL Cloud Manager]consulte o documento [Regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identifica incorretamente questões que não são realmente problemáticas. Isso é chamado de **falso positivo**.

Nesses casos, o código-fonte pode ser anotado com o Java padrão `@SuppressWarnings` anotação especificando a ID da regra como o atributo de anotação. Por exemplo, um falso positivo comum é que a regra SonarQube para detectar senhas codificadas pode ser agressiva sobre como uma senha codificada é identificada.

O código a seguir é bastante comum em um projeto AEM, que tem código para se conectar a algum serviço externo.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube levantará uma vulnerabilidade do bloqueador. Mas, depois de revisar o código, você reconhece que isso não é uma vulnerabilidade e pode anotar o código com a ID de regra apropriada.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

No entanto, se o código fosse realmente este:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Em seguida, a solução correta é remover a senha codificada.

>[!NOTE]
Embora seja uma prática recomendada fazer a variável `@SuppressWarnings` anotação o mais específica possível, ou seja, anote apenas a declaração ou bloco específico que causa o problema, é possível anotar em nível de classe.

>[!NOTE]
Embora não haja uma etapa explícita de teste de segurança, há regras de qualidade de código relacionadas à segurança avaliadas durante a etapa de qualidade do código. Consulte o documento [Visão geral de segurança para AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) para saber mais sobre segurança no Cloud Service.

## Otimização da digitalização do pacote de conteúdo {#content-package-scanning-optimization}

Como parte do processo de análise de qualidade, o Cloud Manager realiza a análise dos pacotes de conteúdo produzidos pela compilação Maven. O Cloud Manager oferece otimizações para acelerar esse processo, que são eficazes quando determinadas restrições de empacotamento são observadas. Mais importante é a otimização executada para projetos que geram um único pacote de conteúdo, geralmente chamado de pacote &quot;tudo&quot;, que contém vários outros pacotes de conteúdo produzidos pela build, que são marcados como ignorados. Quando o Cloud Manager detecta esse cenário, em vez de descompactar o pacote &quot;todos&quot;, os pacotes de conteúdo individuais são digitalizados diretamente e classificados com base nas dependências. Por exemplo, considere a seguinte saída de build.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (pacote de conteúdo)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

Se os únicos itens dentro de `myco-all-1.0.0-SNAPSHOT.zip` são os dois pacotes de conteúdo ignorados, então os dois pacotes incorporados serão digitalizados no lugar do pacote de conteúdo &quot;todos&quot;.

Para projetos que produzem dezenas de pacotes incorporados, essa otimização economiza mais de 10 minutos por execução de pipeline.

Um caso especial pode ocorrer quando o pacote de conteúdo &quot;todos&quot; contiver uma combinação de pacotes de conteúdo ignorados e pacotes OSGi. Por exemplo, se `myco-all-1.0.0-SNAPSHOT.zip` continha os dois pacotes incorporados mencionados anteriormente, bem como um ou mais pacotes OSGi, então um novo pacote de conteúdo mínimo é construído apenas com os pacotes OSGi. Este pacote é sempre nomeado `cloudmanager-synthetic-jar-package` e os pacotes contidos são colocados em `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
* Essa otimização não afeta os pacotes implantados no AEM.
* Como a correspondência entre os pacotes de conteúdo incorporados e os pacotes de conteúdo ignorado se baseia em nomes de arquivo, essa otimização não pode ser executada se vários pacotes de conteúdo ignorados tiverem exatamente o mesmo nome de arquivo ou se o nome do arquivo for alterado durante a incorporação.

