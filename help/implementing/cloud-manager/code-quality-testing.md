---
title: Teste de qualidade de código - Cloud Services
description: Teste de qualidade de código - Cloud Services
translation-type: tm+mt
source-git-commit: ba20916bf6048cb7dff054d9c10f6e1606ae8506
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---


# Teste de qualidade de código {#code-quality-testing}

O teste de qualidade de código avalia a qualidade do código do aplicativo. É o objetivo principal de um gasoduto de qualidade-código e é executado imediatamente após a etapa de construção em todos os gasodutos de não-produção e de produção.

Consulte [Configurando seu pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para saber mais sobre diferentes tipos de pipeline.

## Como entender as regras de qualidade de código {#understanding-code-quality-rules}

Em Teste de qualidade de código, o código fonte é verificado para garantir que ele atenda a determinados critérios de qualidade. Atualmente, esta ação é implementada através de uma combinação de SonarQube e exame de nível de pacote de conteúdo utilizando OakPAL. Há mais de 100 regras que combinam regras genéricas do Java e regras específicas do AEM. Algumas das regras específicas do AEM são criadas com base nas práticas recomendadas AEM engenharia e são chamadas de [Regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>Você pode baixar a lista completa das regras [aqui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

**Porta de três níveis**

Há uma estrutura em três níveis nesta etapa de teste de qualidade de código para os problemas identificados:

* **Crítico**: Estes são problemas identificados pela porta que causam uma falha imediata do pipeline.

* **Importante**: Esses são problemas identificados pela porta que fazem com que o pipeline entre em um estado de pausa. Um gerente de implantação, gerente de projeto ou proprietário de negócios pode substituir os problemas, caso em que o pipeline continua, ou pode aceitar os problemas, caso em que o pipeline pára com uma falha.

* **Informações**: Trata-se de questões identificadas pela porta, que são fornecidas apenas para fins informativos e não têm impacto na execução do gasoduto

Os resultados desta etapa são entregues como *Classificações*.

A tabela a seguir resume as classificações e os limiares de falha para cada uma das categorias Críticas, Importantes e de Informações:

| Nome | Definição | Categoria | Limite de falha |
|--- |--- |--- |--- |
| Classificação de segurança | A = 0 Vulnerabilidade <br/>B = pelo menos 1 Menor Vulnerabilidade<br/> C = pelo menos 1 Grande Vulnerabilidade <br/>D = pelo menos 1 Vulnerabilidade Crítica <br/>E = pelo menos 1 Vulnerabilidade Bloqueadora | Crítico | &lt; B |
| Classificação da confiabilidade | A = 0 Bug <br/>B = pelo menos 1 Bug Menor <br/>C = pelo menos 1 Bug Maior <br/>D = pelo menos 1 Bug Crítico E = pelo menos 1 Bug Bloqueador | Importante | &lt; C |
| Classificação da manutenção | O custo de correção excepcional para cheiros de código é: <br/><ul><li>&lt;> </li><li>entre 6 e 10%, a classificação é de </li><li>entre 11 e 20% a classificação é de C </li><li>entre 21 e 50% a classificação é um D</li><li>algo acima de 50% é um E</li></ul> | Importante | &lt; A |
| Cobertura | Uma combinação da cobertura da linha de teste da unidade e da cobertura da condição usando esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>em que: CT = condições que foram avaliadas como &#39;true&#39; pelo menos uma vez durante a execução de testes de unidade <br/>CF = condições que foram avaliadas como &#39;false&#39; pelo menos uma vez durante a execução de testes de unidade <br/>LC = linhas cobertas = lines_to_cover - uncovered_lines <br/><br/> B = número total de condições <br/>EL = número total de linhas executáveis (lines_to_cover) | Importante | &lt; 50% |
| Testes de unidade ignorados | Número de testes de unidade ignorados. | Informações | > 1 |
| Problemas em aberto | Tipos de edição geral - Vulnerabilidades, Erros e Cheiros de código | Informações | > 0 |
| Linhas Duplicadas | Número de linhas envolvidas em blocos duplicados. <br/>Para que um bloco de código seja considerado como duplicado:  <br/><ul><li>**Projetos não Java:**</li><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem ser espalhados pelo menos em: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras línguas</li><li>**Projetos Java:**</li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas, independentemente do número de tokens e linhas.</li></ul> <br/>As diferenças no recuo, bem como nos literais de string, são ignoradas ao detectar duplicações. | Informações | > 1% |
| Compatibilidade com Cloud Service | Número de problemas de compatibilidade de Cloud Service identificados. | Informações | > 0 |

>[!NOTE]
>
>Consulte [Definições de métrica](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obter definições mais detalhadas.


>[!NOTE]
>
>Para saber mais sobre as regras de qualidade de código personalizadas executadas pelo [!UICONTROL Cloud Manager], consulte [Regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identificará incorretamente questões que não são realmente problemáticas. Isso é chamado de *falso positivo*.

Nesses casos, o código fonte pode ser anotado com a anotação padrão Java `@SuppressWarnings` especificando a ID da regra como o atributo de anotação. Por exemplo, um problema comum é que a regra SonarQube para detectar senhas codificadas pode ser agressiva sobre como uma senha codificada é identificada.

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
>Embora seja uma prática recomendada tornar a anotação `@SuppressWarnings` o mais específica possível, isto é, anotar somente a declaração ou o bloco específico que está causando o problema, é possível fazer anotações em nível de classe.

>[!NOTE]
>Embora não haja nenhuma etapa explícita de Teste de segurança, ainda existem regras de qualidade de código relacionadas à segurança avaliadas durante a etapa de qualidade do código. Consulte [Visão geral de segurança para AEM como Cloud Service](/help/security/cloud-service-security-overview.md) para saber mais sobre segurança no Cloud Service.
