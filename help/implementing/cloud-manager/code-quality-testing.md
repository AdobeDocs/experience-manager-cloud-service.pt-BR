---
title: Teste de qualidade do código - Cloud Services
description: Teste de qualidade do código - Cloud Services
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: 64023bbdccd8d173b15e3984d0af5bb59a2c1447
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Teste de qualidade do código {#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Teste de qualidade do código"
>abstract="O Teste de qualidade do código avalia a qualidade do código de seu aplicativo. É o objetivo principal de um pipeline somente de qualidade de código e é executado imediatamente após a etapa de build em todos os pipelines de não produção e produção."

O Teste de qualidade do código avalia a qualidade do código de seu aplicativo. É o objetivo principal de um pipeline somente de qualidade de código e é executado imediatamente após a etapa de build em todos os pipelines de não produção e produção.

Consulte [Configuração do pipeline de CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para saber mais sobre diferentes tipos de pipelines.

## Noções básicas sobre regras de qualidade de código {#understanding-code-quality-rules}

Em Teste de qualidade do código, o código-fonte é digitalizado para garantir que atenda a determinados critérios de qualidade. Atualmente, isto é implementado através de uma combinação de SonarQube e exame de nível de pacote de conteúdo usando OakPAL. Há mais de 100 regras que combinam regras Java genéricas e regras específicas de AEM. Algumas das regras específicas do AEM são criadas com base nas práticas recomendadas AEM engenharia e são chamadas de [Regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>Você pode baixar a lista completa de regras [aqui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

**Porta de três níveis**

Há uma estrutura de três níveis nesta etapa de teste de qualidade de código para os problemas identificados:

* **Crítico**: Esses são problemas identificados pela porta que causam uma falha imediata do pipeline.

* **Importante**: Esses são problemas identificados pela porta que fazem com que o pipeline entre em um estado pausado. Um gerente de implantação, gerente de projeto ou proprietário de negócios pode substituir os problemas, caso o pipeline continue, ou pode aceitar os problemas, caso o pipeline pare com uma falha.

* **Informações**: Esses são problemas identificados pela porta, que são fornecidos apenas para fins informativos e não têm impacto na execução do pipeline

Os resultados desta etapa são fornecidos como *Ratings*.

A tabela a seguir resume as classificações e os limiares de falha para cada uma das categorias Crítica, Importante e Informações:

| Nome | Definição | Categoria | Limite de Falhas |
|--- |--- |--- |--- |
| Classificação de segurança | A = 0 Vulnerabilidade <br/>B = pelo menos 1 Menor Vulnerabilidade<br/> C = pelo menos 1 Maior Vulnerabilidade <br/>D = pelo menos 1 Vulnerabilidade Crítica <br/>E = pelo menos 1 Vulnerabilidade do Bloqueador | Crítico | &lt; B |
| Classificação da confiabilidade | A = 0 Bug <br/>B = pelo menos 1 Bug Menor <br/>C = pelo menos 1 Bug Major <br/>D = pelo menos 1 Bug Crítico E = pelo menos 1 Bug Bloqueador | Importante | &lt; C |
| Classificação da capacidade de manutenção | O custo excepcional da correção para cheiros de código é: <br/><ul><li>&lt;> </li><li>entre 6 e 10%, a classificação é de </li><li>entre 11 e 20% a classificação é de C </li><li>entre 21 e 50%, a classificação é de D</li><li>qualquer coisa acima de 50% é um E</li></ul> | Importante | &lt; A |
| Cobertura | Uma combinação da cobertura da linha de ensaio da unidade e da cobertura da condição utilizando esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>em que: CT = condições que foram avaliadas como &#39;true&#39; pelo menos uma vez durante a execução de testes de unidade <br/>CF = condições que foram avaliadas como &#39;false&#39; pelo menos uma vez durante a execução de testes de unidade <br/>LC = linhas cobertas = linhas_to_cover - linhas_não cobertas <br/><br/> B = número total de condições <br/>EL = número total de linhas executáveis (lines_to_cover) | Importante | &lt; 50% |
| Testes de Unidade Ignorados | Número de testes de unidade ignorados. | Informações | > 1 |
| Problemas em aberto | Tipos de problemas gerais - Vulnerabilidades, Erros e Cheiros de código | Informações | > 0 |
| Linhas Duplicadas | Número de linhas envolvidas em blocos duplicados. <br/>Para que um bloco de código seja considerado como duplicado:  <br/><ul><li>**Projetos não Java:**</li><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem ser distribuídos pelo menos em: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras línguas</li><li>**Projetos Java:**</li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas, independentemente do número de tokens e linhas.</li></ul> <br/>As diferenças no recuo, bem como nos literais de string são ignoradas ao detectar duplicações. | Informações | > 1% |
| Compatibilidade Cloud Service | Número de problemas de compatibilidade de Cloud Service identificados. | Informações | > 0 |

>[!NOTE]
>
>Consulte [Definições de métrica](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obter definições mais detalhadas.


>[!NOTE]
>
>Para saber mais sobre as regras de qualidade do código personalizado executadas pelo [!UICONTROL Cloud Manager], consulte [Regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identifica incorretamente questões que não são realmente problemáticas. Isso é chamado de *falso positivo*.

Nesses casos, o código-fonte pode ser anotado com a anotação Java padrão `@SuppressWarnings` especificando a ID da regra como o atributo de anotação. Por exemplo, um problema comum é que a regra SonarQube para detectar senhas codificadas pode ser agressiva sobre como uma senha codificada é identificada.

Para observar um exemplo específico, esse código seria bastante comum em um projeto AEM que tem código para se conectar a algum serviço externo:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube aumentará a Vulnerabilidade do Bloqueador. Após revisar o código, você identifica que isso não é uma vulnerabilidade e pode anotar com a ID de regra apropriada.

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
>Embora seja uma prática recomendada tornar a anotação `@SuppressWarnings` o mais específica possível, ou seja, anotar apenas a declaração ou bloco específico que causa o problema, é possível anotar em nível de classe.

>[!NOTE]
>Embora não haja uma etapa explícita de Teste de segurança, ainda há regras de qualidade de código relacionadas à segurança avaliadas durante a etapa de qualidade do código. Consulte [Visão geral de segurança para AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) para saber mais sobre segurança no Cloud Service.
