---
title: Teste de qualidade do código
description: Saiba como o teste de qualidade de código de pipelines funciona e como ele pode melhorar a qualidade de suas implantações.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 80%

---

# Teste de qualidade do código {#code-quality-testing}

Saiba como o teste de qualidade de código de pipelines funciona e como ele pode melhorar a qualidade de suas implantações.

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Teste de qualidade do código"
>abstract="O teste de qualidade do código avalia o código do aplicativo com base em um conjunto de regras de qualidade. É o objetivo principal de um pipeline somente de qualidade do código e é executado imediatamente após a etapa de compilação em todos os pipelines de produção e não produção."

## Introdução {#introduction}

O teste de qualidade do código avalia o código do aplicativo com base em um conjunto de regras de qualidade. É o objetivo principal de um pipeline somente de qualidade do código e é executado imediatamente após a etapa de compilação em todos os pipelines de produção e não produção.

Consulte [Configuração do pipeline de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para saber mais sobre os diferentes tipos de pipelines.

## Regras de qualidade do código {#understanding-code-quality-rules}

O teste de qualidade do código verifica o código-fonte para garantir que atenda a determinados critérios de qualidade. Uma combinação de SonarQube e exame em nível de pacote de conteúdo usando OakPAL implementa essa etapa. Há mais de 100 regras, que combinam regras Java genéricas e regras específicas do AEM. Algumas regras específicas da AEM são baseadas nas práticas recomendadas pela Engenharia da AEM e são conhecidas como [regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md).

Você pode baixar a lista completa atual de regras [usando este link](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

>[!IMPORTANT]
>
>A partir de quinta-feira, 13 de fevereiro de 2025 (Cloud Manager 2025.2.0), a qualidade de código do Cloud Manager usará uma versão atualizada do SonarQube 9.9 e uma lista atualizada de regras que você pode [baixar aqui](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx).

### Classificações de três níveis {#three-tiered-gate}

Os problemas identificados pelos testes de qualidade do código são atribuídos a uma de três categorias.

* **Crítico**: problemas que causam uma falha imediata do pipeline.

* **Importante**: problemas que causam a pausa do pipeline. Um gerente de implantação, gerente de projeto ou proprietário da empresa pode substituir os problemas, permitindo que o pipeline continue. Alternativamente, eles podem aceitar os problemas, interrompendo o pipeline com uma falha.

* **Informações** - Problemas fornecidos exclusivamente para fins informativos e que não têm impacto na execução do pipeline

>[!NOTE]
>
>Em um pipeline somente de qualidade do código, falhas importantes no portal de qualidade do código não podem ser substituídas, pois a etapa de teste de qualidade do código é a etapa final no pipeline.

### Classificações {#ratings}

Os resultados desta etapa são fornecidos como **Classificações**.

A tabela a seguir resume as classificações e os limites de falha para cada uma das categorias: crítico, importante e informativo.

| Nome | Definição | Categoria | Limite de falhas |
|--- |--- |--- |--- |
| Classificação de segurança | A = Sem vulnerabilidades <br/>B = Pelo menos 1 vulnerabilidade baixa<br/> C = Pelo menos 1 vulnerabilidade alta <br/>D = Pelo menos 1 vulnerabilidade crítica <br/>E = Pelo menos 1 vulnerabilidade limitante | Crítico | &lt; B |
| Classificação de confiabilidade | A = Sem erros <br/>B = Pelo menos 1 erro baixo <br/>C = Pelo menos 1 erro alto <br/>D = Pelo menos 1 erro crítico <br>E = Pelo menos 1 erro limitante | Crítico | &lt; D |
| Classificação da capacidade de manutenção | Definido pelo custo de remediação pendente de code smells como uma porcentagem do tempo já dispendido no aplicativo<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | Importante | &lt; A |
| Abrangência | Definida por uma combinação de abrangências da linha de teste unitária e da condição utilizando a fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Condições que foram avaliadas como `true` pelo menos uma vez durante a execução dos testes da unidade</li><li>`CF` = Condições que foram avaliadas como `false` pelo menos uma vez durante a execução dos testes da unidade</li><li>`LC` = Linhas abrangidas = lines_to_cover - uncovered_lines</li><li>`B` = número total de condições</li><li>`EL` = número total de linhas executáveis (lines_to_cover)</li></ul> | Importante | &lt; 50% |
| Testes de unidade ignorados | Número de testes de unidade ignorados | Informações | > 1 |
| Problemas em aberto | Tipos de problemas gerais - Vulnerabilidades, Erros e Code Smells | Informações | > 0 |
| Linhas duplicadas | Definido como o número de linhas envolvidas em blocos duplicados. Um bloco de código é considerado duplicado nas condições a seguir.<br>Projetos não Java:<ul><li>Deve haver pelo menos 100 tokens sucessivos e duplicados.</li><li>Esses tokens devem estar distribuídos por pelo menos: </li><li>30 linhas de código para COBOL </li><li>20 linhas de código para ABAP </li><li>10 linhas de código para outras linguagens</li></ul>Projetos Java:<ul></li><li> Deve haver pelo menos 10 declarações sucessivas e duplicadas, independentemente do número de tokens e linhas.</li></ul>As diferenças no recuo, bem como nos literais de string são ignoradas ao detectar duplicadas. | Informações | > 1% |
| Compatibilidade do Cloud Service | Número de problemas de compatibilidade do Cloud Service identificados | Informações | > 0 |

>[!NOTE]
>
>Consulte [Definições das métricas do SonarQube](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/) para obter definições mais detalhadas.

>[!NOTE]
>
>Para saber mais sobre as regras de qualidade do código personalizado executadas pelo [!UICONTROL Cloud Manager], consulte [Regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Como lidar com falsos positivos {#dealing-with-false-positives}

O processo de verificação da qualidade não é perfeito e, por vezes, identifica incorretamente problemas que não são realmente problemas. Este estado é chamado de **falso positivo**.

Nesses casos, o código-fonte pode ser anotado com a anotação Java padrão `@SuppressWarnings` especificando a ID da regra como o atributo de anotação. Por exemplo, um falso positivo comum é que a regra do SonarQube para detectar senhas codificadas pode ser rígida quanto à forma como uma senha codificada é identificada.

O código a seguir é bastante comum em um projeto AEM, que tem código para se conectar a serviços externos.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

O SonarQube gera uma vulnerabilidade de bloqueador. Porém, depois de revisar o código, é possível reconhecer que não se trata de uma vulnerabilidade e anotar o código com a ID de regra apropriada.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

No entanto, se o código fosse este:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Então, a solução correta seria remover a senha codificada.

>[!NOTE]
>
>Embora seja recomendado fazer a anotação `@SuppressWarnings` a mais específica possível — como anotar apenas a instrução ou o bloco que causa o problema — também é possível anotar no nível da classe.

>[!NOTE]
>Embora não haja uma etapa explícita de teste de segurança, há regras de qualidade do código relacionadas à segurança que são avaliadas durante a etapa de qualidade do código. Consulte a [Visão geral de segurança para o AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) para saber mais sobre segurança no Cloud Service.

## Otimização da verificação do pacote de conteúdo {#content-package-scanning-optimization}

Como parte do processo de análise de qualidade, o Cloud Manager realiza a análise dos pacotes de conteúdo produzidos pela compilação Maven. O Cloud Manager oferece otimizações para acelerar esse processo, que é eficaz quando determinadas restrições de empacotamento são observadas. A otimização mais significativa tem como alvo projetos que produzem um único pacote &quot;all&quot;, contendo vários pacotes de conteúdo da build, que são marcados como ignorados. Quando o Cloud Manager detecta esse cenário, em vez de descompactar o pacote “all”, os pacotes de conteúdo individuais são diretamente verificados e classificados com base nas dependências. Por exemplo, considere a saída de compilação a seguir.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

Se os únicos itens dentro de `myco-all-1.0.0-SNAPSHOT.zip` são os dois pacotes de conteúdo ignorados, então os dois pacotes incorporados serão verificados no lugar do pacote de conteúdo “all”.

Para projetos que produzem dezenas de pacotes incorporados, essa otimização economiza mais de 10 minutos por execução de pipeline.

Um caso especial pode ocorrer quando o pacote de conteúdo “all” contiver uma combinação de pacotes de conteúdo ignorados e pacotes OSGi. Por exemplo, se `myco-all-1.0.0-SNAPSHOT.zip` continha os dois pacotes incorporados mencionados anteriormente, bem como um ou mais pacotes OSGi, então um novo pacote de conteúdo mínimo é construído apenas com os pacotes OSGi. Esse pacote é sempre nomeado `cloudmanager-synthetic-jar-package` e os pacotes contidos são colocados em `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* Essa otimização não afeta os pacotes implantados no AEM.
>* A correspondência entre pacotes de conteúdo incorporados e pacotes de conteúdo ignorados depende dos nomes de arquivo. Essa otimização não pode ocorrer se vários pacotes ignorados compartilharem o mesmo nome de arquivo ou se o nome do arquivo for alterado durante a incorporação.
