---
title: Ambiente de compilação do Cloud Manager
description: Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7b9b9f3b957b27812c4a7e8f2dbcf96d8786b73e
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 35%

---


# Criar ambiente {#build-environment}

Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.

## Detalhes do ambiente de compilação {#build-environment-details}

O Cloud Manager compila e testa seu código usando um ambiente de compilação especializado.

* O ambiente de compilação se baseia em Linux e é derivado do Ubuntu 22.04.
* O Apache Maven 3.9.4 está instalado.
   * A Adobe recomenda [atualizar os repositórios Maven para usar HTTPS em vez de HTTP](#https-maven).
* As versões do Java instaladas são Oracle JDK 11.0.22, Oracle JDK 17.0.10 e Oracle JDK 21.0.4.
* **IMPORTANTE:** por padrão, a variável de ambiente `JAVA_HOME` está definida como `/usr/lib/jvm/jdk1.8.0_401`, que contém o JDK de Oracle 8u401. ***Este padrão deve ser substituído para que os Projetos na Nuvem do AEM usem JDK 21 (preferencial), 17 ou 11***. Consulte a seção [Definindo a versão do JDK Maven](#alternate-maven-jdk-version) para obter mais detalhes.
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
>Embora o Cloud Manager não defina uma versão específica do `jacoco-maven-plugin`, a versão usada deve ser pelo menos `0.7.5.201505241946`.

## Repositórios Maven HTTPS {#https-maven}

O Cloud Manager [versão 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) iniciou uma atualização contínua do ambiente de compilação (que terminou com a versão 2023.12.0) que incluiu a atualização para o Maven 3.8.8. Uma mudança significativa introduzida no Maven 3.8.1 foi um aprimoramento de segurança destinado a reduzir possíveis vulnerabilidades. Mais especificamente, o Maven agora desabilita por padrão todos os espelhos inseguros de `http://*`, conforme descrito nas [notas de versão do Maven](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Como resultado desse aprimoramento de segurança, algumas pessoas podem enfrentar problemas durante a etapa de compilação, especialmente ao baixar artefatos de repositórios Maven que usam conexões HTTP inseguras.

Para garantir uma experiência perfeita com a versão atualizada, a Adobe recomenda atualizar os repositórios Maven para usar HTTPS em vez de HTTP. Esse ajuste se alinha à evolução contínua do setor em direção a protocolos de comunicação seguros e ajuda a manter um processo de compilação seguro e confiável.

### Usar uma versão específica do Java {#using-java-support}

O processo de compilação do Cloud Manager usa o JDK do Oracle 8 para criar projetos por padrão, mas os clientes do AEM Cloud Service devem definir a versão do JDK de execução do Maven como 21 (preferencial), 17 ou 11.

#### Definir a versão do JDK Maven {#alternate-maven-jdk-version}

O Adobe recomenda configurar a versão do JDK de execução Maven para `21` ou `17` em um arquivo `.cloudmanager/java-version`.

Para fazer isso, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório Git usada pelo pipeline. Edite o arquivo de forma que ele contenha apenas o texto `21` ou `17`. Embora a Cloud Manager também aceite o valor `8`, essa versão não é mais suportada para projetos AEM Cloud Service. Qualquer outro valor será ignorado. Quando `21` ou `17` é especificado, o Oracle Java 21 ou o Oracle Java 17 é usado e a variável de ambiente `JAVA_HOME` é definida como `/usr/lib/jvm/jdk-21` ou `/usr/lib/jvm/jdk-17`.

#### Pré-requisitos para migrar para a criação com Java 21 ou Java 17 {#prereq-for-building}

>[!NOTE]
>
>*Ao migrar seu aplicativo para uma nova versão de compilação e de tempo de execução do Java, teste completamente em ambientes de desenvolvimento e de preparo antes de implantar na produção.
>De nota especial, os seguintes recursos ainda não foram formalmente validados com o tempo de execução do Java 21: [Forms](/help/forms/home.md), [Workflows](/help/sites-cloud/authoring/workflows/overview.md), [Caixa de entrada](/help/sites-cloud/authoring/inbox.md) e [Projetos](/help/sites-cloud/authoring/projects/overview.md). Se o aplicativo depender desses recursos, garanta um teste abrangente para verificar a funcionalidade.*

##### Sobre alguns recursos de tradução {#translation-features}

Os seguintes recursos podem não funcionar corretamente ao compilar com o Java 21 ou Java 17, e o Adobe espera resolvê-los no início de 2025:

* `XLIFF` (Formato de Arquivo de Intercâmbio de Localização XML) falha ao usar a Tradução Humana.
* `I18n` (Internacionalização) não lida corretamente com idiomas locais em hebraico (`he`), indonésio (`in`) e iídiche (`yi`) devido a alterações no construtor de Localidade em versões Java mais recentes.

#### Requisitos de tempo de execução {#runtime-requirements}

O tempo de execução do Java 21 é usado para builds no Java 21, Java 17 e Java 11 a partir de fevereiro de 2025. Para garantir a compatibilidade, os seguintes ajustes são necessários.

As atualizações de biblioteca podem ser aplicadas a qualquer momento, pois permanecem compatíveis com versões Java mais antigas.

* **Versão mínima de `org.objectweb.asm`:**
Atualize o uso do `org.objectweb.asm` para a versão 9.5 ou superior para garantir o suporte para tempos de execução de JVM mais recentes.

* **Versão mínima de `org.apache.groovy`:**
Atualize o uso do `org.apache.groovy` para a versão 4.0.22 ou superior para garantir o suporte para tempos de execução de JVM mais recentes.

  Esse pacote pode ser incluído indiretamente adicionando dependências de terceiros, como o console AEM Groovy.

* **Editar um parâmetro de tempo de execução:**
Ao executar o AEM localmente com o Java 21, os scripts de início (`crx-quickstart/bin/start` ou `crx-quickstart/bin/start.bat`) falham devido ao parâmetro `MaxPermSize`. Como solução, remova `-XX:MaxPermSize=256M` do script ou defina a variável de ambiente `CQ_JVM_OPTS`, definindo-a como `-Xmx1024m -Djava.awt.headless=true`.

  O Adobe planeja resolver esse problema em uma versão futura.

>[!NOTE]
>
>Quando `.cloudmanager/java-version` está definido como `21` ou `17`, o tempo de execução do Java 21 é implantado. Em fevereiro ou março de 2025, o tempo de execução do Java 21 está planejado para implantação em todos os clientes, mesmo se o Java 11 for usado para criar seu código.

#### Requisitos de tempo de criação

Os ajustes a seguir são necessários para permitir a criação do projeto com Java 21 e Java 17. Eles podem ser atualizados a qualquer momento, pois são compatíveis com versões mais antigas do Java.

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
