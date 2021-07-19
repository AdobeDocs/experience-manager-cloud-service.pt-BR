---
title: Detalhes do ambiente de criação
description: Detalhes do ambiente de criação - Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Compreensão do ambiente de criação {#understanding-build-environment}

## Detalhes do ambiente de criação {#build-environment-details}

O Cloud Manager cria e testa seu código usando um ambiente de criação especializado. Esse ambiente tem os seguintes atributos:

* O ambiente de build é baseado em Linux, derivado do Ubuntu 18.04.
* O Apache Maven 3.6.0 está instalado.
* As versões do Java instaladas são Oracle JDK 8u202 e 11.0.2.
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

### Uso do suporte ao Java 11 {#using-java-support}

O Cloud Manager agora é compatível com a criação de projetos de clientes com o Java 8 e o Java 11. Por padrão, os projetos são criados usando o Java 8.

Os clientes que desejam usar o Java 11 em seus projetos podem fazer isso usando o [Apache Maven Toolchain Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/).

Para fazer isso, no arquivo pom.xml, adicione uma entrada `<plugin>` que tenha a seguinte aparência:

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

>[!NOTE]
>Os valores de fornecedor suportados são `oracle` e `sun`e os valores de versão suportados são `1.8`, `1.11` e `11`.

>[!NOTE]
>A build do projeto do Cloud Manager ainda está usando o Java 8 para chamar o Maven, portanto, verificar ou impor a versão do Java configurada no plug-in da cadeia de ferramentas por meio de plug-ins como o [Plugin Apache Maven enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) não funciona e esses plug-ins não devem ser usados.

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
