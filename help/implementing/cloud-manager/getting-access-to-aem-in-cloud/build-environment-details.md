---
title: Ambiente de compilação do Cloud Manager
description: Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 28%

---


# Criar ambiente {#build-environment}

Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.

>[!TIP]
>
>Este documento aborda o ambiente de compilação da Cloud Manager para o desenvolvimento de seu projeto do AEM as a Cloud Service. Para obter detalhes sobre as plataformas de cliente compatíveis com o AEM as a Cloud Service para criação de conteúdo, consulte o documento [Plataformas de Cliente Compatíveis.](/help/overview/supported-platforms.md)

## Detalhes do ambiente de compilação {#build-environment-details}

O Cloud Manager compila e testa seu código usando um ambiente de compilação especializado.

* O ambiente de compilação se baseia em Linux e é derivado do Ubuntu 22.04.
* O Apache Maven 3.9.4 está instalado.
   * A Adobe recomenda [atualizar os repositórios Maven para usar HTTPS em vez de HTTP](#https-maven).
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* As versões do Java instaladas são Oracle JDK 11.0.22, Oracle JDK 17.0.10 e Oracle JDK 21.0.4.

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **IMPORTANTE:** por padrão, a variável de ambiente `JAVA_HOME` está definida como `/usr/lib/jvm/jdk1.8.0_401`, que contém o Oracle JDK 8u401. ***Este padrão deve ser substituído para que o AEM Cloud Projects use o JDK 21 (preferencial), 17 ou 11***. Consulte a seção [Definindo a versão do JDK Maven](#alternate-maven-jdk-version) para obter mais detalhes.
* Há alguns pacotes de sistema adicionais instalados que são necessários.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* É possível instalar outros pacotes no momento da criação, conforme descrito na seção [Instalação de pacotes de sistema adicionais](#installing-additional-system-packages).
* Cada criação é executada em um ambiente limpo, com o contêiner de criação não retendo nenhum estado entre as execuções.
* O Maven é sempre executado com os três comandos a seguir.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* O Maven é configurado em nível de sistema com um arquivo `settings.xml`, que inclui automaticamente o repositório público de artefatos da Adobe usando um perfil chamado `adobe-public`. (Consulte [Repositório público Maven da Adobe](https://repo1.maven.org/) para obter mais detalhes).

>[!NOTE]
>
>O Cloud Manager não especifica uma versão específica do `jacoco-maven-plugin`, mas a versão necessária depende da versão do Java do projeto. Para o Java 8, a versão do plug-in deve ser pelo menos `0.7.5.201505241946`, enquanto as versões mais recentes do Java podem exigir uma versão mais recente.

## Repositórios Maven HTTPS {#https-maven}

O Cloud Manager [versão 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) iniciou uma atualização contínua do ambiente de compilação (que terminou com a versão 2023.12.0) que incluiu a atualização para o Maven 3.8.8. Uma mudança significativa introduzida no Maven 3.8.1 foi um aprimoramento de segurança destinado a reduzir possíveis vulnerabilidades. Mais especificamente, o Maven agora desabilita por padrão todos os espelhos inseguros de `http://*`, conforme descrito nas [notas de versão do Maven](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Como resultado desse aprimoramento de segurança, algumas pessoas podem enfrentar problemas durante a etapa de compilação, especialmente ao baixar artefatos de repositórios Maven que usam conexões HTTP inseguras.

Para garantir uma experiência perfeita com a versão atualizada, a Adobe recomenda atualizar os repositórios Maven para usar HTTPS em vez de HTTP. Esse ajuste se alinha à evolução contínua do setor em direção a protocolos de comunicação seguros e ajuda a manter um processo de compilação seguro e confiável.

<!-- OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11. -->

<!-- OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`. -->

### Usar uma versão específica do Java {#using-java-support}

O processo de compilação do Cloud Manager usa o Oracle 8 JDK para criar projetos por padrão, mas os clientes do AEM Cloud Service devem definir a versão do JDK de execução do Maven como 21 (preferencial), 17 ou 11.

#### Definir a versão do JDK Maven {#alternate-maven-jdk-version}

Para definir o JDK de execução do Maven, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório Git usada pelo pipeline. Edite o arquivo de forma que ele contenha apenas o texto `21` ou `17`. Embora a Cloud Manager também aceite o valor `8`, essa versão não é mais compatível com os projetos do AEM Cloud Service. Qualquer outro valor será ignorado. Quando `21` ou `17` é especificado, o Oracle Java 21 ou o Oracle Java 17 é usado.


#### Pré-requisitos para migrar para a criação com Java 21 ou Java 17 {#prereq-for-building}

Para construir com o Java 21 ou Java 17, o Cloud Manager agora usa o SonarQube 9.9, que é compatível com essas versões do Java. Essa alteração foi introduzida na versão 2025.1.0 do Cloud Manager. Nenhuma ação do cliente é necessária para atualizar o SonarQube. Para obter mais detalhes e entender a alteração, consulte as [Notas de versão para Cloud Manager 2025.1.0](/help/implementing/cloud-manager/release-notes/2025/2025-1-0.md).

Ao migrar seu aplicativo para uma nova versão de build e versão de tempo de execução do Java, teste completamente nos ambientes de desenvolvimento e preparo antes de implantar na produção.

A Adobe recomenda a seguinte estratégia de implantação:

1. Execute seu SDK local com o Java 21, que você pode baixar de https://experience.adobe.com/#/downloads, e implante seu aplicativo nele e valide sua funcionalidade. Verifique os registros de que não há erros, o que indica problemas com o carregamento de classe ou tecelagem de código de bytes.
1. Configure uma ramificação no repositório do Cloud Manager para usar o Java 21 como a versão do Java em tempo de compilação, configure um pipeline DEV para usar essa ramificação e execute o pipeline. Execute seus testes de validação.
1. Se estiver bom, configure seu pipeline de preparo/produção para usar o Java 21 como a versão de Java de tempo de compilação e execute o pipeline.

##### Sobre alguns recursos de tradução {#translation-features}

Os seguintes recursos podem não funcionar corretamente quando implantados no tempo de execução do Java 21, e a Adobe espera resolvê-los no início de 2025:

* `XLIFF` (Formato de Arquivo de Intercâmbio de Localização XML) falha ao usar a Tradução Humana.
* `I18n` (Internacionalização) não lida corretamente com idiomas locais em hebraico (`he`), indonésio (`in`) e iídiche (`yi`) devido a alterações no construtor de Localidade em versões Java mais recentes.

#### Requisitos de tempo de execução {#runtime-requirements}

O tempo de execução do Java 21 foi aplicado a todos os ambientes elegíveis, que são ambientes no AEM versão 17098 ou posterior que atendem aos critérios abaixo. Se um ambiente não atender aos critérios, é importante fazer ajustes para garantir desempenho, disponibilidade e segurança.

* **Versão mínima do ASM:**
Atualize o uso do pacote Java`org.objectweb.asm`, geralmente incluído nos artefatos `org.ow2.asm.*`, para a versão 9.5 ou superior para garantir o suporte para tempos de execução JVM mais recentes.

* **Versão mínima do Groovy:**
Atualize o uso dos pacotes Java `org.apache.groovy` ou `org.codehaus.groovy` para a versão 4.0.22 ou superior para garantir o suporte para tempos de execução JVM mais recentes.

  Esse pacote pode ser incluído indiretamente adicionando dependências de terceiros, como o console do AEM Groovy.

* **Versão mínima de Aries SPIFly:**
Atualize o uso do pacote Java `org.apache.aries.spifly.dynamic.bundle` para a versão 1.3.6 ou mais recente para garantir o suporte para tempos de execução JVM mais recentes.

O AEM Cloud Service SDK é compatível com o Java 21 e permite verificar a compatibilidade do seu projeto com o Java 21 antes de executar um pipeline da Cloud Manager.

* **Editar um parâmetro de tempo de execução:**
Ao executar o AEM localmente com o Java 21, os scripts de inicialização (`crx-quickstart/bin/start` ou `crx-quickstart/bin/start.bat`) falham devido ao parâmetro `MaxPermSize`. Como solução, remova `-XX:MaxPermSize=256M` do script ou defina a variável de ambiente `CQ_JVM_OPTS`, definindo-a como `-Xmx1024m -Djava.awt.headless=true`.

  Esse problema é resolvido na SDK do AEM Cloud Service versão 19149 e posterior.

>[!IMPORTANT]
>
>Se um ambiente ainda não tiver sido atualizado automaticamente para o tempo de execução do Java 21, você poderá acioná-lo criando com o Java 17 ou 21. Isso é feito configurando `.cloudmanager/java-version` como `21` ou `17`. Entre em contato com a Adobe em [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) em caso de dúvidas.

#### Requisitos de tempo de criação {#build-time-reqs}

Os ajustes a seguir são necessários para permitir a criação do projeto com Java 21 e Java 17. Eles podem ser atualizados mesmo antes de você executar o Java 21 e o Java 17, pois são compatíveis com versões Java mais antigas.

Recomenda-se que os clientes do AEM Cloud Service criem seus projetos com o Java 21 o mais rápido possível para aproveitar os novos recursos de linguagem.

* **Versão mínima de `bnd-maven-plugin`:**
Atualize o uso do `bnd-maven-plugin` para a versão 6.4.0 para garantir o suporte para tempos de execução de JVM mais recentes.

  As versões 7 ou superiores não são compatíveis com o Java 11 ou inferior, portanto, não é recomendada uma atualização para essa versão.

* **Versão mínima de `aemanalyser-maven-plugin`:**
Atualize o uso do `aemanalyser-maven-plugin` para a versão 1.6.6 ou superior para garantir o suporte para tempos de execução de JVM mais recentes.

* **Versão mínima de `maven-bundle-plugin`:**
Atualize o uso do `maven-bundle-plugin` para a versão 5.1.5 ou superior para garantir o suporte para tempos de execução de JVM mais recentes.

  As versões 6 ou superiores não são compatíveis com o Java 11 ou inferior, portanto, não é recomendada uma atualização para essa versão.

* **Atualizar dependências em `maven-scr-plugin`:**
O `maven-scr-plugin` não é diretamente compatível com Java 21 ou Java 17. No entanto, os arquivos de descritor podem ser gerados atualizando a versão de dependência do ASM na configuração do plug-in, conforme mostrado no exemplo a seguir:

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```

## Variáveis de ambiente - padrão {#environment-variables}

Você pode achar necessário variar o processo de compilação com base nas informações sobre o programa ou pipeline.

Por exemplo, se a minificação do JavaScript ocorrer no momento da criação usando uma ferramenta como o gulp, diferentes níveis de minificação poderão ser preferidos para vários ambientes. Uma build de desenvolvimento pode usar um nível de minificação mais leve em comparação ao preparo e à produção.

Para permitir isso, o Cloud Manager adiciona essas variáveis de ambiente padrão ao contêiner de compilação para cada execução.

| Nome da variável | Definição |
|---|---|
| `CM_BUILD` | Sempre definir como `true` |
| `BRANCH` | A ramificação configurada para a execução |
| `CM_PIPELINE_ID` | O identificador numérico do pipeline |
| `CM_PIPELINE_NAME` | O nome do pipeline |
| `CM_PROGRAM_ID` | O identificador numérico do programa |
| `CM_PROGRAM_NAME` | O nome do programa |
| `ARTIFACTS_VERSION` | Para um pipeline de preparo ou produção, a versão sintética gerada pelo Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | A versão de lançamento |

## Variáveis de ambiente - pipeline {#pipeline-variables}

Seu processo de compilação pode exigir variáveis de configuração específicas que não devem ser armazenadas no repositório Git. Além disso, talvez seja necessário ajustar essas variáveis entre execuções de pipeline usando a mesma ramificação.

Consulte também [Configurar variáveis de pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) para obter mais informações.

## Instalar pacotes de sistema adicionais {#installing-additional-system-packages}

Algumas compilações exigem pacotes de sistema adicionais para funcionarem plenamente. Por exemplo, uma compilação pode invocar um script Python ou Ruby e deve ter um interpretador de linguagem apropriado instalado. Este processo de instalação pode ser gerenciado chamando o [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) em seu `pom.xml` para invocar o APT. Essa execução geralmente deve ser encapsulada em um perfil Maven específico do Cloud Manager. Este exemplo instala o Python.

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Essa mesma técnica pode ser usada para instalar pacotes de linguagem específicos, por exemplo, usando `gem`para RubyGems ou `pip` para Pacotes Python.

>[!NOTE]
>
>Instalar um pacote de sistema dessa maneira não o instala no ambiente de tempo de execução usado para executar o Adobe Experience Manager. Se a instalação de um pacote de sistema no ambiente AEM for necessária, entre em contato com o representante da Adobe.

>[!TIP]
>
>Para obter detalhes sobre o ambiente de criação de front-end, consulte o [Desenvolvimento de sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
