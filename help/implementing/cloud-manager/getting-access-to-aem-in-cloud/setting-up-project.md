---
title: Configuração do projeto
description: Saiba como AEM projetos são criados com o Maven e os padrões que você deve observar ao criar seu próprio projeto.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 1%

---

# Configuração do projeto {#project-setup}

Saiba como AEM projetos são criados com o Maven e os padrões que você deve observar ao criar seu próprio projeto.

## Detalhes de configuração do projeto {#project-setup-details}

Para serem criados e implantados com êxito com o Cloud Manager, AEM projetos precisam seguir estas diretrizes:

* Os projetos devem ser criados usando [Apache Maven.](https://maven.apache.org)
* Deve haver um `pom.xml` na raiz do repositório git. Essa `pom.xml` arquivo pode se referir a quantos submódulos (que por sua vez podem ter outros submódulos etc.) conforme necessário.
* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seu `pom.xml` arquivos.
   * Acesso ao [repositórios de artefatos protegidos por senha](#password-protected-maven-repositories) é compatível quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Pacotes de conteúdo implantáveis são descobertos pela varredura do pacote de conteúdo `.zip` arquivos, que estão contidos em um diretório chamado `target`.
   * Qualquer número de submódulos pode produzir pacotes de conteúdo.
* Os artefatos do dispatcher implantáveis são detectados ao verificar `.zip` arquivos (também contidos no diretório chamado `target`), que têm diretórios nomeados `conf` e `conf.d`.
* Se houver mais de um pacote de conteúdo, a ordem de implantações de pacote não será garantida.
   * Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para definir a ordem.
* As embalagens podem ser [ignorado](#skipping-content-packages) durante a implantação.

## Ativar perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de build ao executar o Cloud Manager, em vez de executar o em estações de trabalho de desenvolvedor. Para estes casos, [Perfis Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) O pode ser usado para definir como a build deve ser diferente em diferentes ambientes, incluindo o Cloud Manager.

A ativação de um perfil Maven no ambiente de build do Cloud Manager deve ser feita procurando a variável `CM_BUILD` [variável de ambiente.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) Da mesma forma, um perfil destinado a ser usado somente fora do ambiente de build do Cloud Manager deve ser feito procurando a ausência dessa variável.

Por exemplo, se você quiser gerar uma mensagem simples apenas quando a build for executada no Cloud Manager, faça isso.

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

E se você quiser gerar uma mensagem simples somente quando a build for executada fora do Cloud Manager, você faria isso.

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
>
>Os artefatos de um repositório Maven protegido por senha devem ser usados com muito cuidado, pois o código implantado por meio desse mecanismo não é executado atualmente em todos os [regras de qualidade do código](/help/implementing/cloud-manager/custom-code-quality-rules.md) implementado nas portas de qualidade do Cloud Manager. Por conseguinte, só deve ser utilizado em casos raros e para código não vinculado à AEM. É recomendável também implantar as fontes Java, bem como todo o código-fonte do projeto junto com o binário.

Para usar um repositório Maven protegido por senha no Cloud Manager:

1. Especifique a senha (e, opcionalmente, o nome de usuário) como um segredo [variável de pipeline.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. Em seguida, faça referência a esse segredo dentro de um arquivo chamado `.cloudmanager/maven/settings.xml` no repositório git, que segue o [Arquivo de configurações Maven](https://maven.apache.org/settings.html) esquema.

Quando o processo de build do Cloud Manager é iniciado:

* O `<servers>` o elemento neste arquivo será mesclado ao padrão `settings.xml` arquivo fornecido pelo Cloud Manager.
   * IDs de servidor que começam com `adobe` e `cloud-manager` são consideradas reservadas e não devem ser usadas por servidores personalizados.
   * IDs de servidor que não correspondem a um desses prefixos ou a ID padrão `central` O nunca será espelhado pelo Cloud Manager.
* Com esse arquivo em vigor, a ID do servidor seria referenciada de dentro de um `<repository>` e/ou `<pluginRepository>` dentro do `pom.xml` arquivo.
* Geralmente, estes `<repository>` e/ou `<pluginRepository>` elementos ficariam contidos dentro de um [Perfil específico do Cloud Manager](#activating-maven-profiles-in-cloud-manager), embora isso não seja estritamente necessário.

Como exemplo, digamos que o repositório esteja em `https://repository.myco.com/maven2`, o nome de usuário que o Cloud Manager deve usar é `cloudmanager`e a senha é `secretword`. Você tomaria as seguintes etapas.

1. Defina a senha como um segredo no pipeline.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Faça referência a `.cloudmanager/maven/settings.xml` arquivo.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. Por fim, faça referência à ID do servidor dentro do `pom.xml` arquivo:

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

Para fazer isso, configure o maven-source-plugin em seu projeto.

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

É uma boa prática implantar toda a origem do projeto junto com o binário em um repositório Maven. Isso permite que o reconstrua o artefato exato.

Para fazer isso, configure o maven-assembly-plugin em seu projeto.

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

No Cloud Manager, as builds podem produzir qualquer número de pacotes de conteúdo. Por uma variedade de motivos, pode ser desejável produzir um pacote de conteúdo, mas não implantá-lo. Um exemplo pode ser a criação de pacotes de conteúdo usados apenas para teste ou que serão reembalados por outra etapa no processo de criação, ou seja, como um subpacote de outro pacote.

Para acomodar esses cenários, o Cloud Manager procurará uma propriedade chamada `cloudManagerTarget` nas propriedades dos pacotes de conteúdo incorporados. Se essa propriedade estiver definida como `none`, o pacote será ignorado e não implantado.

O mecanismo para definir essa propriedade depende da maneira como a build produz o pacote de conteúdo. Por exemplo, com a variável `filevault-maven-plugin` você configuraria o plug-in da seguinte maneira.

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

O `content-package-maven-plugin` tem uma configuração semelhante.

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

Quando uma execução é iniciada, a confirmação de HEAD atual para o pipeline da ramificação é extraída. O hash de confirmação é visível na interface do usuário e por meio da API. Quando a etapa de build for concluída com êxito, os artefatos resultantes serão armazenados com base nesse hash de confirmação e poderão ser reutilizados em execuções de pipeline subsequentes.

Os pacotes serão reutilizados em pipelines, se estiverem no mesmo programa. Ao procurar pacotes que possam ser reutilizados, o AEM ignora ramificações e reutiliza artefatos entre ramificações.

Quando ocorre uma reutilização, as etapas de criação e qualidade do código são efetivamente substituídas pelos resultados da execução original. O arquivo de log da etapa de build listará os artefatos e as informações de execução que foram usadas originalmente para criá-los.

Veja a seguir um exemplo dessa saída de log.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

O log da etapa de qualidade do código conterá informações semelhantes.

### Exemplos {#example-reuse}

#### Exemplo 1 {#example-1}

Considere que seu programa tem dois pipelines de desenvolvimento:

* Pipeline 1 na ramificação `foo`
* Pipeline 2 na ramificação `bar`

Ambas as ramificações estão na mesma ID de confirmação.

1. A execução do pipeline 1 primeiro criará os pacotes normalmente.
1. Em seguida, executar o Pipeline 2 reutilizará pacotes criados pelo Pipeline 1.

#### Exemplo 2 {#example-2}

Considere que seu programa tem duas ramificações:

* Ramificação `foo`
* Ramificação `bar`

Ambas as ramificações têm a mesma ID de confirmação.

1. Um pipeline de desenvolvimento cria e executa `foo`.
1. Posteriormente, um pipeline de produção cria e executa `bar`.

Nesse caso, o artefato de `foo` será reutilizado para o pipeline de produção desde que o mesmo hash de confirmação tenha sido identificado.

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

* Os artefatos da build não são reutilizados em diferentes programas, independentemente de o hash de confirmação ser idêntico.
* Os artefatos da build são reutilizados no mesmo programa mesmo se a ramificação e/ou o pipeline for diferente.
* [Manuseio de versão Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) substitui a versão do projeto somente em pipelines de produção. Portanto, se a mesma confirmação for usada em uma execução de implantação de desenvolvimento e em uma execução de pipeline de produção e o pipeline de implantação de desenvolvimento for executado primeiro, as versões serão implantadas no estágio e na produção sem serem alteradas. No entanto, uma tag ainda será criada nesse caso.
* Se a recuperação dos artefatos armazenados não for bem-sucedida, a etapa de build será executada como se nenhum artefato tivesse sido armazenado.
* Variáveis de pipeline diferentes de `CM_DISABLE_BUILD_REUSE` não são considerados quando o Cloud Manager decide reutilizar artefatos de build criados anteriormente.
