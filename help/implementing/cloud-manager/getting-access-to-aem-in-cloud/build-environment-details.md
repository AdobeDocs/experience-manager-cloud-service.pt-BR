---
title: Ambiente de compilação
description: Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 30f2eaf4d2edba13e875cd1bfe767e83a2b7f1a5
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 92%

---


# Ambiente de compilação {#build-environment}

Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.

## Detalhes do ambiente de compilação {#build-environment-details}

O Cloud Manager compila e testa seu código usando um ambiente de compilação especializado.

* O ambiente de compilação se baseia em Linux e é derivado do Ubuntu 22.04.
* O Apache Maven 3.8.8 está instalado.
   * A Adobe recomenda [atualizar os repositórios Maven para usar HTTPS em vez de HTTP.](#https-maven)
* As versões do Java instaladas são Oracle JDK 8u371 e Oracle JDK 11.0.20.
* Por padrão, a variável `JAVA_HOME` a variável de ambiente está definida como `/usr/lib/jvm/jdk1.8.0_371` que contém o JDK 8u371 do Oracle. Consulte a [Versão alternativa do JDK de execução do Maven](#alternate-maven-jdk-version) para obter mais detalhes.
* Há alguns pacotes de sistema adicionais instalados que são necessários.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Outros pacotes podem ser instalados no momento da compilação, conforme descrito na seção [Instalação de pacotes de sistema adicionais.](#installing-additional-system-packages)
* Cada compilação é feita em um ambiente primitivo; o contêiner de compilação não mantém nenhum estado entre as execuções.
* O Maven é sempre executado com os três comandos a seguir.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* O Maven é configurado em nível de sistema com um arquivo `settings.xml`, que inclui automaticamente o repositório público de artefatos da Adobe usando um perfil chamado `adobe-public`. (Consulte [Repositório público Maven da Adobe](https://repo1.maven.org/) para obter mais detalhes).

>[!NOTE]
>
>Embora o Cloud Manager não defina uma versão específica do `jacoco-maven-plugin`, a versão usada deve ser pelo menos `0.7.5.201505241946`.

## Repositórios Maven HTTPS {#https-maven}

O Cloud Manager [versão 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) iniciou uma atualização contínua do ambiente de compilação (que terminou com a versão 2023.12.0) que incluiu a atualização para o Maven 3.8.8. Uma mudança significativa introduzida no Maven 3.8.1 foi um aprimoramento de segurança destinado a reduzir possíveis vulnerabilidades. Mais especificamente, o Maven agora desabilita por padrão todas as páginas espelho inseguras de `http://*`, conforme descrito nas [notas de versão do Maven.](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)

Como resultado desse aprimoramento de segurança, algumas pessoas podem enfrentar problemas durante a etapa de compilação, especialmente ao baixar artefatos de repositórios Maven que usam conexões HTTP inseguras.

Para garantir uma experiência perfeita com a versão atualizada, a Adobe recomenda atualizar os repositórios Maven para usar HTTPS em vez de HTTP. Esse ajuste se alinha à evolução contínua do setor em direção a protocolos de comunicação seguros e ajuda a manter um processo de compilação seguro e confiável.

### Uso de uma versão específica do Java {#using-java-support}

Por padrão, os projetos são criados pelo processo de compilação do Cloud Manager usando o Oracle 8 JDK. Os clientes que desejam usar um JDK alternativo têm duas opções.

* [Usar cadeias de ferramentas Maven.](#maven-toolchains)
* [Selecionar uma versão alternativa do JDK para todo o processo de execução Maven.](#alternate-maven-jdk-version)

#### Cadeias de ferramentas Maven {#maven-toolchains}

O [Plug-in de cadeias de ferramentas Maven](https://maven.apache.org/plugins/maven-toolchains-plugin/) permite que os projetos selecionem um JDK específico (ou cadeia de ferramentas) a ser usado no contexto de plug-ins Maven com reconhecimento de cadeias de ferramentas. Isso é feito no `pom.xml` especificando um fornecedor e o valor da versão.

Este plug-in da cadeia de ferramentas pode ser adicionado como parte de um perfil, conforme mostrado abaixo.

```xml
<profile>
    <id>cm-java-11</id>
    <activation>
        <property>
            <name>env.CM_BUILD</name>
        </property>
    </activation>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-toolchains-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>toolchain</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <toolchains>
                        <jdk>
                            <version>11</version>
                            <vendor>oracle</vendor>
                        </jdk>
                    </toolchains>
                </configuration>
            </plugin>
        </plugins>
    </build>
</profile>
```

Assim, todos os plug-ins Maven com reconhecimento de cadeias de ferramentas usarão o Oracle JDK versão 11.

Ao usar esse método, o próprio Maven ainda é executado usando o JDK padrão (Oracle 8) e a variável de ambiente `JAVA_HOME` não é alterada. Portanto, a verificação ou a aplicação da versão do Java por meio de plug-ins como o Plug-in executor Apache Maven não funcionarão e tais plug-ins não deverão ser usados.

As combinações de fornecedor/versão disponíveis no momento são:

| Fornecedor | Versão |
|---|---|
| `oracle` | `8` |
| `oracle` | `11` |
| `sun` | `8` |
| `sun` | `11` |

Esta tabela se refere aos números de versão do produto. Os números de compilação ou caminhos de instalação do Java podem refletir convenções de versão antigas do Java, como 1.8 para o Java 8.

>[!NOTE]
>
>A partir de abril de 2022, o JDK do Oracle será o JDK padrão para o desenvolvimento e a operação de aplicativos do AEM. O processo de criação do Cloud Manager passa automaticamente a usar o JDK do Oracle, mesmo que uma opção alternativa esteja explicitamente selecionada na conjunto de ferramentas do Maven. Consulte as notas de versão de abril de 2022.

#### Versão alternativa do JDK de execução do Maven {#alternate-maven-jdk-version}

Também é possível selecionar o Java 8 ou Java 11 como JDK para toda a execução do Maven. Diferentemente das opções de cadeias de ferramentas, essa definição altera o JDK usado para todos os plug-ins, a menos que a configuração de cadeias de ferramentas também esteja definida, caso em que esta ainda será aplicada aos plug-ins Maven com reconhecimento de cadeias de ferramentas. Como resultado, a verificação e a implementação da versão do Java usando o [Plug-in executor Apache Maven](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funcionarão.

Para fazer isso, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório Git usada pelo pipeline. Esse arquivo pode ter o conteúdo 11 ou 8. Qualquer outro valor será ignorado. Se 11 for especificado, será usado o Oracle 11 e a variável de ambiente `JAVA_HOME` será definida como `/usr/lib/jvm/jdk-11.0.2`. Se 8 for especificado, será usado o Oracle 8 e a variável de ambiente `JAVA_HOME` será definida como `/usr/lib/jvm/jdk1.8.0_202`.

## Variáveis de ambiente {#environment-variables}

### Variáveis de ambiente padrão {#standard-environ-variables}

Você pode achar necessário variar o processo de compilação com base nas informações sobre o programa ou pipeline.

Por exemplo, se a minificação do JavaScript no tempo de compilação for feita por meio de uma ferramenta como o gulp, talvez você queira usar um nível de minificação diferente ao compilar um ambiente de desenvolvimento, em vez de ambientes de preparo e produção.

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

### Variáveis de pipeline {#pipeline-variables}

Seu processo de compilação pode depender de variáveis de configuração específicas, cuja colocação no repositório Git seria inadequada, ou talvez seja necessário variá-las entre as execuções de pipeline que usam uma mesma ramificação.

O Cloud Manager permite que essas variáveis sejam configuradas por meio da API ou da CLI do Cloud Manager com base no pipeline. As variáveis podem ser armazenadas como texto simples ou criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas no ambiente de compilação como variáveis de ambiente que podem ser referenciadas no arquivo `pom.xml` ou em outros scripts de compilação.

Esse comando da CLI define uma variável.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Esse comando lista variáveis.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Os nomes das variáveis devem observar as convenções a seguir.

* As variáveis podem conter somente caracteres alfanuméricos e sublinhado (`_`).
* Os nomes devem estar em maiúsculas.
* Há um limite de 200 variáveis por pipeline.
* Cada nome deve ter 100 caracteres ou menos.
* Cada valor de variável `string` deve ter menos de 2048 caracteres.
* Each `secretString` o valor da variável de tipo deve ter 500 caracteres ou menos.

Quando usado em um arquivo `pom.xml` do Maven, normalmente é útil mapear essas variáveis às propriedades do Maven usando uma sintaxe semelhante a esta.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## Instalação de pacotes de sistema adicionais {#installing-additional-system-packages}

Algumas compilações exigem a instalação de pacotes de sistema adicionais para funcionarem plenamente. Por exemplo, uma compilação pode invocar um script Python ou Ruby e deve ter um interpretador de linguagem apropriado instalado. Faça isso chamando [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) em seu `pom.xml` para invocar o APT. Essa execução geralmente deve ser encapsulada em um perfil Maven específico do Cloud Manager. Este exemplo instala o Python.

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
