---
title: Detalhes da configuração do projeto
description: Detalhes da configuração do projeto - Cloud Services
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 4219c8ce30a0f1cd44bbf8e8de46d6be28a1ddf3
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 5%

---

# Configurar o projeto {#project-setup-details}

## Modificando Detalhes de Configuração do Projeto {#modifying-project-setup-details}

Para serem criados e implantados com êxito com o Cloud Manager, os projetos de AEM existentes precisam seguir algumas regras básicas:

* Os projetos devem ser criados usando o Apache Maven.
* Deve haver um *pom.xml* na raiz do repositório Git. Essa *pom.xml* arquivo pode se referir a quantos submódulos (que por sua vez podem ter outros submódulos etc.) conforme necessário.

* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seu *pom.xml* arquivos. Acesso ao [repositórios de artefatos protegidos por senha](#password-protected-maven-repositories) é compatível quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Pacotes de conteúdo implantáveis são descobertos pela varredura do pacote de conteúdo *zip* arquivos contidos em um diretório chamado *target*. Qualquer número de submódulos pode produzir pacotes de conteúdo.

* Os artefatos do Dispatcher que podem ser implantados são descobertos ao verificar *zip* arquivos (novamente, contidos em um diretório chamado *target*) que têm diretórios nomeados *conf* e *conf.d*.

* Se houver mais de um pacote de conteúdo, a ordem de implantações de pacote não será garantida. Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para definir a ordem. As embalagens podem ser [ignorado](#skipping-content-packages) da implantação.


## Ativar perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de build ao executar no Cloud Manager, em vez de quando ele é executado em estações de trabalho de desenvolvedor. Para estes casos, [Perfis Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) O pode ser usado para definir como a build deve ser diferente em diferentes ambientes, incluindo o Cloud Manager.

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
>Para testar esse perfil em uma estação de trabalho de desenvolvedor, você pode habilitá-lo na linha de comando (com `-PcmBuild`) ou no ambiente de desenvolvimento integrado (IDE).

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
>Os artefatos de um repositório Maven protegido por senha devem ser usados com muito cuidado, pois o código implantado por meio desse mecanismo atualmente não é executado por todas as regras de qualidade implementadas nos Portos de qualidade do Cloud Manager. Por conseguinte, só deve ser utilizado em casos raros e para código não vinculado à AEM. É recomendável também implantar as fontes Java, bem como todo o código-fonte do projeto junto com o binário.

Para usar um repositório Maven protegido por senha do Cloud Manager, especifique a senha (e, opcionalmente, o nome de usuário) como uma Variável de pipeline secreta e, em seguida, faça referência a esse segredo dentro de um arquivo chamado `.cloudmanager/maven/settings.xml` no repositório git. Esse arquivo segue o [Arquivo de configurações Maven](https://maven.apache.org/settings.html) esquema. Quando o processo de build do Cloud Manager é iniciado, a variável `<servers>` o elemento neste arquivo será mesclado ao padrão `settings.xml` arquivo fornecido pelo Cloud Manager. IDs de servidor que começam com `adobe` e `cloud-manager` são consideradas reservadas e não devem ser usadas por servidores personalizados. IDs de servidor **not** correspondendo a um desses prefixos ou a ID padrão `central` O nunca será espelhado pelo Cloud Manager. Com esse arquivo em vigor, a ID do servidor seria referenciada de dentro de um `<repository>` e/ou `<pluginRepository>` dentro do `pom.xml` arquivo. Geralmente, estes `<repository>` e/ou `<pluginRepository>` elementos ficariam contidos dentro de um [Perfil específico do Cloud Manager](#activating-maven-profiles-in-cloud-manager), embora isso não seja estritamente necessário.

Como exemplo, digamos que o repositório esteja em https://repository.myco.com/maven2, o nome de usuário que o Cloud Manager deve usar é `cloudmanager` e a senha é `secretword`.

Primeiro, defina a senha como um segredo no pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Em seguida, faça referência a isso no `.cloudmanager/maven/settings.xml` arquivo:

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

E finalmente referencie a ID do servidor dentro da `pom.xml` arquivo:

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

## Reutilização de artefato de construção {#build-artifact-reuse}

Em muitos casos, o mesmo código é implantado em vários ambientes AEM. Sempre que possível, o Cloud Manager evitará reconstruir a base de código quando detectar que a mesma confirmação de git é usada em várias execuções de pipeline de pilha completa.

Quando uma execução é iniciada, a confirmação de HEAD atual para o pipeline da ramificação é extraída. O hash de confirmação é visível na interface do usuário e por meio da API. Quando a etapa de build for concluída com êxito, os artefatos resultantes serão armazenados com base nesse hash de confirmação e poderão ser reutilizados em execuções de pipeline subsequentes. Quando ocorre uma reutilização, as etapas de criação e qualidade do código são efetivamente substituídas pelos resultados da execução original. O arquivo de log da etapa de build listará os artefatos e as informações de execução que foram usadas originalmente para criá-los.

Veja a seguir um exemplo dessa saída de log.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

O log da etapa de qualidade do código conterá informações semelhantes.

### Recusar {#opting-out}

Se desejar, o comportamento de reutilização pode ser desativado para pipelines específicos, definindo a variável de pipeline `CM_DISABLE_BUILD_REUSE` para `true`. Se essa variável for definida, o hash de confirmação ainda será extraído e os artefatos resultantes serão armazenados para uso posterior, mas todos os artefatos armazenados anteriormente não serão reutilizados. Para entender esse comportamento, considere o seguinte cenário.

1. Um novo pipeline é criado.
1. O pipeline é executado (execução nº 1) e a confirmação de HEAD atual é `becdddb`. A execução é bem-sucedida e os artefatos resultantes são armazenados.
1. O `CM_DISABLE_BUILD_REUSE` estiver definida.
1. O pipeline é executado novamente sem alterar o código. Embora haja artefatos armazenados associados a `becdddb`, não serão reutilizados devido ao `CM_DISABLE_BUILD_REUSE` variável.
1. O código é alterado e o pipeline é executado. A confirmação de HEAD é agora `f6ac5e6`. A execução é bem-sucedida e os artefatos resultantes são armazenados.
1. O `CM_DISABLE_BUILD_REUSE` é excluída.
1. O pipeline é executado novamente sem alterar o código. Como há artefatos armazenados associados a `f6ac5e6`, esses artefatos são reutilizados.

### Avisos {#caveats}

* [Manuseio de versão Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) substitua a versão do projeto somente em pipelines de produção. Portanto, se a mesma confirmação for usada em uma execução de implantação de desenvolvimento e em uma execução de pipeline de produção e o pipeline de implantação de desenvolvimento for executado primeiro, as versões serão implantadas no estágio e na produção sem serem alteradas. No entanto, uma tag ainda será criada nesse caso.
* Se a recuperação dos artefatos armazenados não for bem-sucedida, a etapa de build será executada como se nenhum artefato tivesse sido armazenado.
* Variáveis de pipeline diferentes de `CM_DISABLE_BUILD_REUSE` não são considerados quando o Cloud Manager decide reutilizar artefatos de build criados anteriormente.
