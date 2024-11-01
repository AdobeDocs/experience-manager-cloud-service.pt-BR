---
title: Ambiente de compilação do Cloud Manager
description: Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f5f7830ac6d7f5b65203b12bb1775e64379c7d14
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 58%

---


# Criar ambiente {#build-environment}

Saiba mais sobre o ambiente de compilação do Cloud Manager e como ele cria e testa seu código.

## Detalhes do ambiente de compilação {#build-environment-details}

O Cloud Manager compila e testa seu código usando um ambiente de compilação especializado.

* O ambiente de compilação se baseia em Linux e é derivado do Ubuntu 22.04.
* O Apache Maven 3.9.4 está instalado.
   * A Adobe recomenda [atualizar os repositórios Maven para usar HTTPS em vez de HTTP](#https-maven).
* As versões do Java instaladas são Oracle JDK 11.0.22 e Oracle JDK 8u401.
* **IMPORTANTE**: por padrão, a variável de ambiente `JAVA_HOME` está definida como `/usr/lib/jvm/jdk1.8.0_401`, que contém o JDK de Oracle 8u401. *_Este padrão deve ser substituído para Projetos na Nuvem AEM para usar o JDK 11_*. Consulte a seção [Definindo a versão do JDK Maven](#alternate-maven-jdk-version) para obter mais detalhes.
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

O processo de compilação do Cloud Manager usa o JDK do Oracle 8 para compilar projetos por padrão, mas os clientes do AEM Cloud Service devem definir a versão do JDK de execução do Maven como `11`.

#### Definir a versão do JDK Maven {#alternate-maven-jdk-version}

A Adobe recomenda que você defina a versão do JDK para toda a execução do Maven para `11` em um arquivo `.cloudmanager/java-version`.

Para fazer isso, crie um arquivo chamado `.cloudmanager/java-version` na ramificação do repositório Git usada pelo pipeline. Edite o arquivo de forma que ele contenha apenas o texto, `11`. Embora a Cloud Manager também aceite o valor `8`, essa versão não é mais suportada para projetos AEM Cloud Service. Qualquer outro valor será ignorado. Quando `11` é especificado, o Oracle 11 é usado e a variável de ambiente `JAVA_HOME` é definida como `/usr/lib/jvm/jdk-11.0.22`.

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
