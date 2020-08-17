---
title: AEM Application Project - Cloud Service
description: AEM Application Project - Cloud Service
translation-type: tm+mt
source-git-commit: 2a89c8039f3d2135d8944822d3a4381142bbdb75
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 9%

---


# Criação de um projeto de aplicativo AEM {#aem-application-project}

## Usando o Assistente para Criar um Projeto de Aplicativo AEM {#using-wizard-to-create-an-aem-application-project}

Para ajudar a iniciar novos clientes, o Cloud Manager agora pode criar um projeto de AEM mínimo como ponto de partida. Esse processo se baseia no [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).


Siga as etapas abaixo para criar um projeto de aplicativo AEM no Cloud Manager:

1. Quando você fizer logon no Cloud Manager e a configuração básica do programa for concluída, uma chamada especial para o cartão de ação será exibida na tela **Visão geral** se o repositório estiver vazio.

   ![](assets/create-wizard1.png)

1. Clique em **Criar** para navegar até a tela **Criar uma ramificação e projeto**.

   ![](assets/create-wizard2.png)

1. O bloco Criação **do projeto em andamento** é exibido na tela Visão geral *do* Programa.

   ![](assets/create-wizard3.png)

1. Quando a criação do programa for concluída, o bloco **Adicionar ambiente** aparecerá na página *Visão geral do programa*.
   ![](assets/create-wizard4.png)

   Consulte [Gerenciamento de Ambientes](/help/implementing/cloud-manager/manage-environments.md) para saber como adicionar ou gerenciar ambientes.

## Configuração do projeto {#setting-up-your-project}

### Modificando Detalhes de Configuração do Projeto {#modifying-project-setup-details}

Para ser criado e implantado com êxito com o Cloud Manager, os projetos AEM existentes precisam seguir algumas regras básicas:

* Os projetos devem ser construídos com o Apache Maven.
* Deve haver um arquivo *pom.xml* na raiz do repositório Git. Esse arquivo *pom.xml* pode fazer referência a quantos submódulos (que por sua vez podem ter outros submódulos etc.) conforme necessário.

* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seus arquivos *pom.xml* . O acesso a repositórios [de artefatos protegidos por](#password-protected-maven-repositories) senha é suportado quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Os pacotes de conteúdo implantáveis são detectados ao verificar se há arquivos *zip* do pacote de conteúdo contidos em um diretório chamado *público alvo*. Qualquer número de submódulos pode produzir pacotes de conteúdo.

* Os artefatos do Dispatcher que podem ser implantados são descobertos pela varredura de arquivos *zip* (novamente, contidos em um diretório chamado *público alvo*) que têm diretórios chamados *conf* e *conf.d*.

* Se houver mais de um pacote de conteúdo, a ordem de implantações de pacote não é garantida. Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para definir a ordem. Os pacotes podem ser [ignorados](#skipping-content-packages) da implantação.


## Criar detalhes do Ambiente {#build-environment-details}

O Cloud Manager cria e testa seu código usando um ambiente de compilação especializado. Esse ambiente tem os seguintes atributos:

* O ambiente build é baseado no Linux, derivado do Ubuntu 18.04.
* O Apache Maven 3.6.0 está instalado.
* As versões do Java instaladas são o Oracle JDK 8u202 e 11.0.2.
* Existem outros pacotes de sistema instalados que são necessários:

   * bzip2
   * descompactar
   * libpng
   * imagemagick
   * gráfico

* Outros pacotes podem ser instalados no momento da criação, conforme descrito [abaixo](#installing-additional-system-packages).
* Cada obra é feita com um ambiente intocado; o container build não mantém nenhum estado entre as execuções.
* Maven é sempre executado com o comando: *mvn —batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent package*
* O Maven é configurado no nível do sistema com um arquivo settings.xml que inclui automaticamente o repositório público do **Artefato** de Adobe. (Consulte o Repositório [Adobe Public Maven](https://repo.adobe.com/) para obter mais detalhes).

>[!NOTE]
>Embora o Gerenciador de nuvem não defina uma versão específica do `jacoco-maven-plugin`, a versão usada deve ser pelo menos `0.7.5.201505241946`.

### Uso do suporte ao Java 11 {#using-java-support}

O Cloud Manager agora é compatível com a criação de projetos de clientes com Java 8 e Java 11. Por padrão, os projetos são criados usando o Java 8. Os clientes que desejam usar o Java 11 em seus projetos podem fazer isso usando o plug-in Maven Toolchain.

Para fazer isso, no arquivo pom.xml, adicione uma `<plugin>` entrada com a seguinte aparência:

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
>Os valores de fornecedor suportados são `oracle` e `sun`.
>Os valores de versão suportados são `1.8`, `1.11`e `11`.

## Variáveis de ambiente {#environment-variables}

### Variáveis de Ambiente padrão {#standard-environ-variables}

Em alguns casos, os clientes acham necessário variar o processo de criação com base nas informações sobre o programa ou pipeline.

Por exemplo, se a miniificação do JavaScript em tempo de criação estiver sendo feita, por meio de uma ferramenta como gulp, pode haver um desejo de usar um nível de miniificação diferente ao criar um ambiente dev em vez de construir para o palco e a produção.

Para suportar isso, o Cloud Manager adiciona essas variáveis de ambiente padrão ao container build para cada execução.

| **Nome da variável** | **Definição** |
|---|---|
| CM_BUILD | Sempre definido como &quot;true&quot; |
| RAMIFICAÇÃO | A ramificação configurada para a execução |
| CM_PIPELINE_ID | O identificador de pipeline numérico |
| CM_PIPELINE_NAME | O nome do pipeline |
| CM_PROGRAMA_ID | O identificador de programa numérico |
| CM_PROGRAMA_NAME | O nome do programa |
| ARTIFTS_VERSION | Para um pipeline de estágio ou produção, a versão sintética gerada pelo Cloud Manager |
| CM_AEM_PRODUCT_VERSION | O nome da versão |

### Variáveis de pipeline {#pipeline-variables}

Em alguns casos, o processo de compilação de um cliente pode depender de variáveis de configuração específicas que não seriam adequadas para serem colocadas no repositório Git ou que precisariam variar entre execuções de pipeline usando a mesma ramificação.

O Cloud Manager permite que essas variáveis sejam configuradas por meio da API do Cloud Manager ou da CLI do Cloud Manager por pipeline. As variáveis podem ser armazenadas como texto sem formatação ou como criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas dentro do ambiente build como uma variável de ambiente que pode ser referenciada dentro do `pom.xml` arquivo ou de outros scripts de compilação.

Para definir uma variável usando a CLI, execute um comando como:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

As variáveis atuais podem ser listadas:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

Os nomes de variáveis podem conter somente caracteres alfanuméricos e sublinhado (_). Por convenção, os nomes devem ser todos maiúsculos. Há um limite de 200 variáveis por pipeline, cada nome deve ter menos de 100 caracteres e cada valor deve ter menos de 2048 caracteres.

Quando usado em um `Maven pom.xml` arquivo, é útil mapear essas variáveis para as propriedades do Maven usando uma sintaxe semelhante a esta:

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


## Ativar Perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de compilação ao ser executado no Gerenciador de nuvem em vez de quando é executado em estações de trabalho de desenvolvedor. Nesses casos, os Perfis [](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) Maven podem ser usados para definir como a compilação deve ser diferente em ambientes diferentes, incluindo o Cloud Manager.

A ativação de um Perfil Maven dentro do ambiente de compilação do Cloud Manager deve ser feita procurando a variável de ambiente CM_BUILD descrita acima. Em contrapartida, um perfil destinado a ser usado somente fora do ambiente de criação do Cloud Manager deve ser feito procurando o absentido dessa variável.

Por exemplo, se você quiser enviar uma mensagem simples somente quando a compilação for executada dentro do Cloud Manager, você deve fazer o seguinte:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Para testar esse perfil em uma estação de trabalho de desenvolvedor, você pode ativá-lo na linha de comando (com `-PcmBuild`) ou no Ambiente de desenvolvimento integrado (IDE).

E se você quiser enviar uma mensagem simples somente quando a criação for executada fora do Gerenciador de nuvem, você deve fazer o seguinte:

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## Suporte ao repositório Maven protegido por senha {#password-protected-maven-repositories}

Para usar um repositório Maven protegido por senha do Gerenciador de nuvem, especifique a senha (e, opcionalmente, o nome de usuário) como uma Variável [secreta do](#pipeline-variables) Pipeline e faça referência a esse segredo em um arquivo chamado `.cloudmanager/maven/settings.xml` no repositório git. Esse arquivo segue o [schema de Arquivo](https://maven.apache.org/settings.html) de Configurações Maven. Quando os start de processo de criação do Gerenciador de nuvem, o `<servers>` elemento nesse arquivo será mesclado no arquivo padrão `settings.xml` fornecido pelo Gerenciador de nuvem. As IDs de servidor que começam com `adobe` e `cloud-manager` são consideradas reservadas e não devem ser usadas por servidores personalizados. As IDs de servidor **que não** correspondem a um desses prefixos ou a ID padrão nunca `central` serão espelhadas pelo Gerenciador de nuvem. Com esse arquivo no lugar, a ID do servidor seria referenciada de dentro de um `<repository>` e/ou `<pluginRepository>` elemento dentro do `pom.xml` arquivo. Geralmente, esses `<repository>` e/ou `<pluginRepository>` elementos estariam contidos em um perfil [específico do](#activating-maven-profiles-in-cloud-manager)Cloud Manager, embora isso não seja estritamente necessário.

Por exemplo, digamos que o repositório esteja em https://repository.myco.com/maven2, o usuário que o Gerenciador da Cloud deve usar é `cloudmanager` e a senha é `secretword`.

Primeiro, defina a senha como um segredo no pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Em seguida, consulte-o no `.cloudmanager/maven/settings.xml` arquivo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

Por fim, consulte a ID do servidor dentro do `pom.xml` arquivo:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

## Instalação de pacotes adicionais do sistema {#installing-additional-system-packages}

Algumas compilações exigem a instalação de pacotes adicionais do sistema para funcionar totalmente. Por exemplo, uma compilação pode chamar um script Python ou ruby e, como resultado, precisa ter um interpretador de idioma apropriado instalado. Isso pode ser feito chamando o plug-in [exec-maven](https://www.mojohaus.org/exec-maven-plugin/) para chamar a APT. Essa execução geralmente deve estar envolvida em um perfil Maven específico do Cloud Manager. Por exemplo, para instalar o python:

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

Essa mesma técnica pode ser usada para instalar pacotes específicos de idioma, ou seja, usar `gem` para RubyGems ou `pip` para pacotes Python.

>[!NOTE]
>
>Instalar um pacote do sistema desta maneira **não** o instala no ambiente de tempo de execução usado para executar o Adobe Experience Manager. Se precisar de um pacote do sistema instalado no ambiente AEM, entre em contato com o representante do Adobe.

## Ignorando pacotes de conteúdo {#skipping-content-packages}

No Cloud Manager, as compilações podem produzir qualquer número de pacotes de conteúdo.
Por vários motivos, pode ser desejável produzir um pacote de conteúdo, mas não implantá-lo. Isso pode ser útil, por exemplo, ao criar pacotes de conteúdo usados apenas para teste ou que serão reempacotados por outra etapa do processo de compilação, ou seja, como um subpacote de outro pacote.

Para acomodar esses cenários, o Cloud Manager procurará uma propriedade chamada ***cloudManagerTarget*** nas propriedades dos pacotes de conteúdo incorporados. Se essa propriedade estiver definida como Nenhum, o pacote será ignorado e não implantado. O mecanismo para definir essa propriedade depende da forma como a compilação está produzindo o pacote de conteúdo. Por exemplo, no plugin filevault-maven, você o configuraria da seguinte maneira:

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

Com o plug-in content-package-maven-é semelhante:

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## Recursos adicionais {#additional-resources}

Consulte as seções abaixo para saber como usar o Cloud Manager no Cloud Service:

* [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md)
* [Configure seu Pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md)
* [Implantação do código](/help/implementing/cloud-manager/deploy-code.md)
* [Noções básicas dos resultados de teste](/help/implementing/developing/introduction/understand-test-results.md)