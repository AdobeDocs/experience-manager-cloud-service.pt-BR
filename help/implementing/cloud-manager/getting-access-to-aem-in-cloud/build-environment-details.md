---
title: Detalhes do ambiente de criação
description: Detalhes do ambiente de criação - Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Compreensão do ambiente de criação {#understanding-build-environment}

## Detalhes do ambiente de criação {#build-environment-details}

O Cloud Manager cria e testa seu código usando um ambiente de criação especializado. Esse ambiente tem os seguintes atributos:

* O ambiente de build é baseado em Linux, derivado do Ubuntu 18.04.
* O Apache Maven 3.6.0 está instalado.
* As versões do Java instaladas são Oracle JDK 8u202, Azul Zulu 8u292, Oracle JDK 11.0.2 e Azul Zulu 11.0.11.
* Há alguns pacotes de sistema adicionais instalados que são necessários:

   * bzip2
   * descompactar
   * libpng
   * imagemagick
   * graficicado

* Outros pacotes podem ser instalados no momento da criação, conforme descrito [abaixo](#installing-additional-system-packages).
* Cada construção é feita em um ambiente primitivo; o contêiner de criação não mantém nenhum estado entre as execuções.
* Maven é sempre executado com os três comandos a seguir:

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* O Maven é configurado em um nível de sistema com um arquivo settings.xml que inclui automaticamente o repositório Adobe público **Artifact** usando um perfil chamado `adobe-public`. (Consulte [Repositório Maven público do Adobe](https://repo.adobe.com/) para obter mais detalhes).

>[!NOTE]
>Embora o Cloud Manager não defina uma versão específica do `jacoco-maven-plugin`, a versão usada deve ser pelo menos `0.7.5.201505241946`.

### Uso de uma versão específica do Java {#using-java-support}

Por padrão, os projetos são criados pelo processo de build do Cloud Manager usando o JDK do Oracle 8. Os clientes que desejam usar um JDK alternativo têm duas opções: As cadeias de ferramentas Maven e a seleção de uma versão alternativa do JDK para todo o processo de execução Maven.

#### Cadeias de ferramentas Maven {#maven-toolchains}

O [Plugin Maven Toolchain](https://maven.apache.org/plugins/maven-toolchains-plugin/) permite que os projetos selecionem um JDK específico (ou *toolchain*) a ser usado no contexto de plug-ins Maven com reconhecimento de cadeias de ferramentas. Isso é feito no arquivo `pom.xml` do projeto, especificando um fornecedor e o valor da versão. Uma seção de amostra no arquivo `pom.xml` é:

```
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

Ao usar esse método, o próprio Maven ainda é executado usando o JDK padrão (Oracle 8). Portanto, verificar ou aplicar a versão do Java por meio de plug-ins como o Plugin Apache Maven enforcer não funciona e esses plug-ins não devem ser usados.

As combinações de fornecedor/versão disponíveis no momento são:

* oracle 1.8
* oracle 1.11
* oracle 11
* sol 1,8
* sol 1,11
* sol 11
* azul 1.8
* azul 1.11
* azul 8

#### Versão alternativa do JDK de execução do Maven {#alternate-maven-jdk-version}

Também é possível selecionar o Azul 8 ou o Azul 11 como JDK para toda a execução do Maven. Diferentemente das opções de cadeias de ferramentas, isso altera o JDK usado para todos os plug-ins, a menos que a configuração de cadeias de ferramentas também esteja definida, caso em que a configuração de cadeias de ferramentas ainda será aplicada para plug-ins Maven com reconhecimento de cadeias de ferramentas. Como resultado, verificar e aplicar a versão do Java usando o [Plugin Apache Maven Enforcement](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funcionará.

Para fazer isso, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório Git usada pelo pipeline. Esse arquivo pode ter o conteúdo 11 ou 8. Qualquer outro valor é ignorado. Se 11 for especificado, Azul 11 será usado. Se 8 for especificado, Azul 8 será usado.

>[!NOTE]
>Em uma versão futura do Cloud Manager, atualmente estimada para outubro de 2021, o JDK padrão será alterado e o padrão será Azul 11. Os projetos que não são compatíveis com o Java 11 devem criar esse arquivo com o conteúdo 8 o mais rápido possível para garantir que não sejam afetados por esse switch.


## Variáveis de ambiente {#environment-variables}

### Variáveis de ambiente padrão {#standard-environ-variables}

Em alguns casos, os clientes acham necessário variar o processo de build com base nas informações sobre o programa ou pipeline.

Por exemplo, se a minificação do JavaScript em tempo de criação estiver sendo feita, por meio de uma ferramenta como o gulp, pode haver o desejo de usar um nível de minificação diferente ao criar um ambiente de desenvolvimento, em vez de criar para estágio e produção.

Para ser compatível com isso, o Cloud Manager adiciona essas variáveis de ambiente padrão ao contêiner de criação para cada execução.

| **Nome da variável** | **Definição** |
|---|---|
| CM_BUILD | Sempre definido como &quot;true&quot; |
| RAMIFICAÇÃO | A ramificação configurada para a execução |
| CM_PIPELINE_ID | O identificador de pipeline numérico |
| CM_PIPELINE_NAME | O nome do pipeline |
| CM_PROGRAM_ID | O identificador numérico do programa |
| CM_PROGRAM_NAME | O nome do programa |
| ARTIFATTS_VERSION | Para um pipeline de estágio ou produção, a versão sintética gerada pelo Cloud Manager |
| CM_AEM_PRODUCT_VERSION | O nome da Versão |

### Variáveis de pipeline {#pipeline-variables}

Em alguns casos, o processo de criação de um cliente pode depender de variáveis de configuração específicas que seriam inadequadas para colocar no repositório Git ou precisariam variar entre execuções de pipeline usando a mesma ramificação.

O Cloud Manager permite que essas variáveis sejam configuradas por meio da API do Cloud Manager ou da CLI do Cloud Manager por pipeline. As variáveis podem ser armazenadas como texto simples ou criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas no ambiente de criação como uma variável de ambiente que pode ser referenciada no arquivo `pom.xml` ou em outros scripts de criação.

Para definir uma variável usando a CLI, execute um comando como:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

As variáveis atuais podem ser listadas:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

Os nomes de variáveis só podem conter caracteres alfanuméricos e sublinhados (_). Por convenção, os nomes devem estar todos em maiúsculas. Existe um limite de 200 variáveis por pipeline, cada nome deve ter menos de 100 caracteres e cada valor deve ter menos de 2048 caracteres no caso de variáveis do tipo string e 500 caracteres no caso de variáveis do tipo secretString.

Quando usada dentro de um arquivo `Maven pom.xml`, normalmente é útil mapear essas variáveis para propriedades do Maven usando uma sintaxe semelhante a esta:

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

Algumas builds exigem pacotes de sistema adicionais para serem instalados para funcionarem completamente. Por exemplo, uma build pode invocar um script Python ou ruby e, como resultado, precisa ter um interpretador de idioma adequado instalado. Isso pode ser feito chamando o [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) para chamar a APT. Essa execução geralmente deve ser encapsulada em um perfil Maven específico do Cloud Manager. Por exemplo, para instalar o python:

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

Essa mesma técnica pode ser usada para instalar pacotes específicos de idioma, ou seja, usando `gem` para RubyGems ou `pip` para Pacotes de Python.

>[!NOTE]
>Instalar um pacote de sistema dessa maneira o **not** o instala no ambiente de tempo de execução usado para executar o Adobe Experience Manager. Se precisar de um pacote de sistema instalado no ambiente AEM, entre em contato com o representante do Adobe.
