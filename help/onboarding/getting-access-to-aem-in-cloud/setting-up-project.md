---
title: Detalhes da configuração do projeto
description: Detalhes da configuração do projeto - Cloud Services
translation-type: tm+mt
source-git-commit: 17971405c174e2559879335ade437c5fec2868a3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 7%

---


# Configuração do projeto {#project-setup-details}

## Modificando Detalhes de Configuração do Projeto {#modifying-project-setup-details}

Para ser criado e implantado com êxito com o Cloud Manager, os projetos AEM existentes precisam seguir algumas regras básicas:

* Os projetos devem ser construídos com o Apache Maven.
* Deve haver um arquivo *pom.xml* na raiz do repositório Git. Esse arquivo *pom.xml* pode fazer referência a quantos submódulos (que por sua vez podem ter outros submódulos etc.) conforme necessário.

* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seus arquivos *pom.xml* . O acesso a repositórios [de artefatos protegidos por](#password-protected-maven-repositories) senha é suportado quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Os pacotes de conteúdo implantáveis são detectados ao verificar se há arquivos *zip* do pacote de conteúdo contidos em um diretório chamado *público alvo*. Qualquer número de submódulos pode produzir pacotes de conteúdo.

* Os artefatos do Dispatcher que podem ser implantados são descobertos pela varredura de arquivos *zip* (novamente, contidos em um diretório chamado *público alvo*) que têm diretórios chamados *conf* e *conf.d*.

* Se houver mais de um pacote de conteúdo, a ordem de implantações de pacote não é garantida. Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para definir a ordem. Os pacotes podem ser [ignorados](#skipping-content-packages) da implantação.


## Ativar Perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de compilação ao ser executado no Gerenciador de nuvem em vez de quando é executado em estações de trabalho de desenvolvedor. Nesses casos, os Perfis [](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) Maven podem ser usados para definir como a compilação deve ser diferente em ambientes diferentes, incluindo o Cloud Manager.

A ativação de um Perfil Maven dentro do ambiente de compilação do Cloud Manager deve ser feita procurando a variável de ambiente CM_BUILD descrita acima. Por outro lado, um perfil destinado a ser usado somente fora do ambiente de criação do Gerenciador de nuvem deve ser feito procurando pela ausência dessa variável.

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

>[!NOTE]
>Os artefatos de um repositório Maven protegido por senha devem ser usados com muito cuidado, pois o código implantado por esse mecanismo não é executado atualmente pelos portões de qualidade do Cloud Manager. Portanto, deve ser utilizado apenas em casos raros e para códigos não ligados à AEM. Recomenda-se também implantar as fontes Java e todo o código fonte do projeto junto com o binário.

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

### Implantação de fontes {#deploying-sources}

É uma boa prática implantar as fontes Java junto com o binário em um repositório Maven.

Configure o plug-in maven-source em seu projeto:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### Implantação de fontes de projeto {#deploying-project-sources}

É uma boa prática implantar toda a fonte do projeto junto com o binário em um repositório Maven - isso permite reconstruir o artefato exato.

Configure o plug-in maven-assembly em seu projeto:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

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
