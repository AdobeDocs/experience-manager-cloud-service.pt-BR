---
title: Detalhes da configuração do projeto
description: Detalhes da configuração do projeto - Cloud Services
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 596a7a41dac617e2fb57ba2e4891a2b4dce31fad
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 7%

---

# Configurar o projeto {#project-setup-details}

## Modificando Detalhes de Configuração do Projeto {#modifying-project-setup-details}

Para serem criados e implantados com êxito com o Cloud Manager, os projetos de AEM existentes precisam seguir algumas regras básicas:

* Os projetos devem ser criados usando o Apache Maven.
* Deve haver um arquivo *pom.xml* na raiz do repositório Git. Este arquivo *pom.xml* pode fazer referência a quantos submódulos (que, por sua vez, podem ter outros submódulos etc.) conforme necessário.

* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seus arquivos *pom.xml*. O acesso a [repositórios de artefatos protegidos por senha](#password-protected-maven-repositories) é suportado quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Pacotes de conteúdo implantáveis são descobertos pela varredura de arquivos *zip* do pacote de conteúdo que estão contidos em um diretório chamado *target*. Qualquer número de submódulos pode produzir pacotes de conteúdo.

* Os artefatos do Dispatcher que podem ser implantados são descobertos pela varredura para arquivos *zip* (novamente, contidos em um diretório chamado *target*) que têm diretórios nomeados *conf* e *conf.d*.

* Se houver mais de um pacote de conteúdo, a ordem de implantações de pacote não será garantida. Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para definir a ordem. Os pacotes podem ser [ignorados](#skipping-content-packages) da implantação.


## Ativar perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de build ao executar no Cloud Manager, em vez de quando ele é executado em estações de trabalho de desenvolvedor. Nesses casos, [Perfis Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) podem ser usados para definir como a build deve ser diferente em ambientes diferentes, incluindo o Cloud Manager.

A ativação de um Perfil Maven no ambiente de build do Cloud Manager deve ser feita procurando a variável de ambiente CM_BUILD descrita acima. Por outro lado, um perfil destinado a ser usado somente fora do ambiente de build do Cloud Manager deve ser feito procurando a ausência dessa variável.

Por exemplo, se você quiser gerar uma mensagem simples apenas quando a build for executada no Cloud Manager, faça o seguinte:

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

E se você quiser gerar uma mensagem simples somente quando a build for executada fora do Cloud Manager, faça o seguinte:

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

## Suporte a Repositório Maven protegido por senha {#password-protected-maven-repositories}

>[!NOTE]
>Os artefatos de um repositório Maven protegido por senha devem ser usados com muito cuidado, pois o código implantado por meio desse mecanismo atualmente não é executado pelos Portas de qualidade do Cloud Manager. Por conseguinte, só deve ser utilizado em casos raros e para código não vinculado à AEM. É recomendável também implantar as fontes Java, bem como todo o código-fonte do projeto junto com o binário.

Para usar um repositório Maven protegido por senha do Cloud Manager, especifique a senha (e, opcionalmente, o nome de usuário) como uma Variável de pipeline secreta e, em seguida, faça referência a esse segredo dentro de um arquivo chamado `.cloudmanager/maven/settings.xml` no repositório Git. Esse arquivo segue o esquema [Arquivo de configurações Maven](https://maven.apache.org/settings.html). Quando o processo de build do Cloud Manager for iniciado, o elemento `<servers>` nesse arquivo será mesclado ao arquivo `settings.xml` padrão fornecido pelo Cloud Manager. As IDs de servidor que começam com `adobe` e `cloud-manager` são consideradas reservadas e não devem ser usadas por servidores personalizados. As IDs de servidor **que não** correspondem a um desses prefixos ou a ID padrão `central` nunca serão espelhadas pelo Cloud Manager. Com esse arquivo no lugar, a ID do servidor seria referenciada de dentro de um elemento `<repository>` e/ou `<pluginRepository>` dentro do arquivo `pom.xml`. Geralmente, esses elementos `<repository>` e/ou `<pluginRepository>` ficariam contidos em um [perfil específico do Cloud Manager](#activating-maven-profiles-in-cloud-manager), embora isso não seja estritamente necessário.

Como exemplo, digamos que o repositório esteja em https://repository.myco.com/maven2, o nome de usuário que o Cloud Manager deve usar é `cloudmanager` e a senha é `secretword`.

Primeiro, defina a senha como um segredo no pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Em seguida, faça referência a isso no arquivo `.cloudmanager/maven/settings.xml`:

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

E finalmente referencie a id do servidor dentro do arquivo `pom.xml`:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
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
    </profile>
</profiles>
```

### Implantação de fontes {#deploying-sources}

É uma boa prática implantar as fontes Java junto com o binário em um repositório Maven.

Configure o maven-source-plugin no seu projeto:

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

### Implantar fontes de projeto {#deploying-project-sources}

É uma boa prática implantar toda a fonte do projeto junto com o binário em um repositório Maven, o que permite reconstruir o artefato exato.

Configure o maven-assembly-plugin em seu projeto:

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

No Cloud Manager, as builds podem produzir qualquer número de pacotes de conteúdo.
Por uma variedade de motivos, pode ser desejável produzir um pacote de conteúdo, mas não implantá-lo. Isso pode ser útil, por exemplo, ao criar pacotes de conteúdo usados apenas para teste ou que serão reembalados por outra etapa no processo de criação, ou seja, como um subpacote de outro pacote.

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

Com o content-package-maven-plugin, ele é semelhante:

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
