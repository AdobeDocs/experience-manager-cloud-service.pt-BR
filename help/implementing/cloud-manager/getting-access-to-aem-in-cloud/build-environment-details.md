---
title: Ambiente de criação
description: Saiba mais sobre o ambiente de criação do Cloud Manager e como ele cria e testa seu código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: b327af40a003b055b8e44688e1b84ac15a8c8439
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Ambiente de criação {#build-environment}

Saiba mais sobre o ambiente de criação do Cloud Manager e como ele cria e testa seu código.

## Detalhes do ambiente de criação {#build-environment-details}

O Cloud Manager cria e testa seu código usando um ambiente de criação especializado.

* O ambiente de build é baseado em Linux, derivado do Ubuntu 18.04.
* O Apache Maven 3.6.0 está instalado.
* As versões do Java instaladas são Oracle JDK 8u202 e Oracle JDK 11.0.2.
* Por padrão, a variável `JAVA_HOME` variável de ambiente está definida como `/usr/lib/jvm/jdk1.8.0_202`  que contém o Oracle JDK 8u202. Consulte [Versão alternativa do JDK de execução do Maven](#alternate-maven-jdk-version) para obter mais detalhes.
* Há alguns pacotes de sistema adicionais instalados que são necessários.

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* Outros pacotes podem ser instalados no momento da criação, conforme descrito na seção [Instalação de pacotes de sistema adicionais.](#installing-additional-system-packages)
* Cada construção é feita em um ambiente primitivo; o contêiner de criação não mantém nenhum estado entre as execuções.
* Maven é sempre executado com os três comandos a seguir.

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* O Maven é configurado em um nível de sistema com um `settings.xml` arquivo , que inclui automaticamente o repositório de artefatos do Adobe público usando um perfil chamado `adobe-public`. (Consulte [Repositório Adobe Public Maven](https://repo1.maven.org/) para obter mais detalhes).

>[!NOTE]
>
>Embora o Cloud Manager não defina uma versão específica do `jacoco-maven-plugin`, a versão usada deve ser pelo menos `0.7.5.201505241946`.

### Uso de uma versão específica do Java {#using-java-support}

Por padrão, os projetos são criados pelo processo de build do Cloud Manager usando o JDK do Oracle 8. Os clientes que desejam usar um JDK alternativo têm duas opções.

* [Use correntes de ferramentas Maven.](#maven-toolchains)
* [Selecione uma versão alternativa do JDK para todo o processo de execução Maven.](#alternate-maven-jdk-version)

#### Cadeias de ferramentas Maven {#maven-toolchains}

O [Plug-in de Cadeias de Ferramentas Maven](https://maven.apache.org/plugins/maven-toolchains-plugin/) O permite que os projetos selecionem um JDK específico (ou cadeia de ferramentas) a ser usado no contexto de plug-ins Maven com reconhecimento de cadeias de ferramentas. Isso é feito no `pom.xml` especificando um fornecedor e o valor da versão.

```xml
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
```

Isso fará com que todos os plug-ins Maven com reconhecimento de cadeias de ferramentas usem o Oracle JDK, versão 11.

Ao usar esse método, o próprio Maven ainda é executado usando o JDK padrão (Oracle 8) e o `JAVA_HOME`  variável de ambiente não é alterada. Portanto, verificar ou aplicar a versão do Java por meio de plug-ins como o Plugin Apache Maven enforcer não funciona e esses plug-ins não devem ser usados.

As combinações de fornecedor/versão disponíveis no momento são:

| Fornecedor | Versão |
|---|---|
| `oracle` | `1.8` |
| `oracle` | `1.11` |
| `oracle` | `11` |
| `sun` | `1.8` |
| `sun` | `1.11` |
| `sun` | `11` |

>[!NOTE]
>
>A partir de abril de 2022, o JDK do Oracle será o JDK padrão para o desenvolvimento e a operação de aplicativos AEM. O processo de criação do Cloud Manager mudará automaticamente para o uso do JDK do Oracle, mesmo se uma opção alternativa for explicitamente selecionada na cadeia de ferramentas Maven. Consulte as notas de versão de abril, uma vez publicadas, para obter mais detalhes.

#### Versão alternativa do JDK de execução do Maven {#alternate-maven-jdk-version}

Também é possível selecionar o Java 8 ou Java 11 como o JDK para toda a execução do Maven. Diferentemente das opções de cadeias de ferramentas, isso altera o JDK usado para todos os plug-ins, a menos que a configuração de cadeias de ferramentas também esteja definida, caso em que a configuração de cadeias de ferramentas ainda será aplicada para plug-ins Maven com reconhecimento de cadeias de ferramentas. Como resultado, verifique e implemente a versão do Java usando o [Plug-in do Apache Maven enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funcionará.

Para fazer isso, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório git usada pelo pipeline. Esse arquivo pode ter o conteúdo 11 ou 8. Qualquer outro valor é ignorado. Se 11 for especificado, será utilizado o Oracle 11 e a variável `JAVA_HOME` variável de ambiente está definida como `/usr/lib/jvm/jdk-11.0.2`. Se 8 for especificado, o Oracle 8 será usado e a variável `JAVA_HOME` variável de ambiente está definida como `/usr/lib/jvm/jdk1.8.0_202`.

## Variáveis de ambiente {#environment-variables}

### Variáveis de ambiente padrão {#standard-environ-variables}

Você pode achar necessário variar o processo de build com base nas informações sobre o programa ou pipeline.

Por exemplo, se a minificação do JavaScript em tempo de criação estiver sendo feita por meio de uma ferramenta como o gulp, pode haver o desejo de usar um nível de minificação diferente ao criar um ambiente de desenvolvimento, em vez de criar para preparo e produção.

Para ser compatível com isso, o Cloud Manager adiciona essas variáveis de ambiente padrão ao contêiner de criação para cada execução.

| Nome da variável | Definição |
|---|---|
| `CM_BUILD` | Sempre defina como `true` |
| `BRANCH` | A ramificação configurada para a execução |
| `CM_PIPELINE_ID` | O identificador de pipeline numérico |
| `CM_PIPELINE_NAME` | O nome do pipeline |
| `CM_PROGRAM_ID` | O identificador numérico do programa |
| `CM_PROGRAM_NAME` | O nome do programa |
| `ARTIFACTS_VERSION` | Para um pipeline de estágio ou produção, a versão sintética gerada pelo Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | A versão de lançamento |

### Variáveis de pipeline {#pipeline-variables}

Seu processo de build pode depender de variáveis de configuração específicas que seriam inadequadas para colocar no repositório Git ou talvez seja necessário variá-las entre as execuções de pipeline que usam a mesma ramificação.

O Cloud Manager permite que essas variáveis sejam configuradas por meio da API do Cloud Manager ou da CLI do Cloud Manager por pipeline. As variáveis podem ser armazenadas como texto simples ou criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas no ambiente de criação como uma variável de ambiente que pode ser referenciada de dentro da variável `pom.xml` arquivo ou outros scripts de criação.

Esse comando da CLI define uma variável.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Esse comando lista variáveis.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Os nomes de variáveis devem observar as seguintes convenções.

* As variáveis podem conter somente caracteres alfanuméricos e o sublinhado (`_`).
* Os nomes devem estar em maiúsculas.
* Há um limite de 200 variáveis por pipeline.
* Cada nome deve ter menos de 100 caracteres.
* Cada `string` O valor da variável deve ter menos de 2048 caracteres.
* Cada `secretString` O valor da variável de tipo deve ter menos de 500 caracteres.

Quando usado dentro de um Maven `pom.xml` normalmente é útil mapear essas variáveis para propriedades do Maven usando uma sintaxe semelhante a esta.

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

Algumas builds exigem pacotes de sistema adicionais para serem instalados para funcionarem completamente. Por exemplo, uma build pode invocar um script Python ou Ruby e precisará ter um interpretador de idioma adequado instalado. Isso pode ser feito chamando a função [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) em seu `pom.xml` para invocar APT. Essa execução geralmente deve ser encapsulada em um perfil Maven específico do Cloud Manager. Este exemplo instala Python.

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

Essa mesma técnica pode ser usada para instalar pacotes específicos do idioma, por exemplo, usando `gem` para RubyGems ou `pip` Python Packages.

>[!NOTE]
>
>Instalar um pacote de sistema dessa maneira não o instala no ambiente de tempo de execução usado para executar o Adobe Experience Manager. Se precisar de um pacote de sistema instalado no ambiente AEM, entre em contato com o representante do Adobe.
