---
title: Configuração do projeto
description: Saiba como os projetos do AEM são compilados no Maven e os padrões que você deve observar ao criar seu próprio projeto.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '1404'
ht-degree: 100%

---

# Configuração do projeto {#project-setup}

Saiba como os projetos do AEM são compilados no Maven e os padrões que você deve observar ao criar seu próprio projeto.

## Detalhes de configuração do projeto {#project-setup-details}

Para criar e implantar com sucesso com o Cloud Manager, os projetos do AEM precisam seguir as seguintes diretrizes:

* Os projetos devem ser compilados usando [Apache Maven.](https://maven.apache.org)
* Deve haver um arquivo `pom.xml` na raiz do repositório Git. Esse arquivo `pom.xml` pode fazer referência a tantos submódulos (que, por sua vez, podem ter outros submódulos, e assim por diante) quanto forem necessários.
* Você pode adicionar referências a repositórios de artefatos Maven adicionais em seus arquivos `pom.xml`.
   * O acesso a [repositórios de artefatos protegidos por senha](#password-protected-maven-repositories) é suportado quando configurado. No entanto, o acesso a repositórios de artefatos protegidos pela rede não é suportado.
* Pacotes de conteúdo implantáveis são descobertos ao verificar os arquivos de pacote de conteúdo `.zip`, que estão contidos em um diretório chamado `target`.
   * Qualquer número de submódulos pode produzir pacotes de conteúdo.
* Os artefatos implantáveis do dispatcher são detectados ao verificar os arquivos `.zip` (também contidos no diretório chamado `target`), que têm diretórios chamados `conf` e `conf.d`.
* Se houver mais de um pacote de conteúdo, a ordem das implantações não será garantida.
   * Se uma ordem específica for necessária, as dependências do pacote de conteúdo poderão ser usadas para defini-la.
* Os pacotes podem ser [ignorados](#skipping-content-packages) durante a implantação.

## Ativação de perfis Maven no Cloud Manager {#activating-maven-profiles-in-cloud-manager}

Em alguns casos limitados, pode ser necessário variar um pouco o processo de compilação ao executá-lo no Cloud Manager, em vez de executá-lo em estações de trabalho de desenvolvedor. Nesses casos, [Perfis Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) podem ser usados para definir como a compilação deve ser diferente em diferentes ambientes, incluindo no Cloud Manager.

A ativação de um perfil do Maven no ambiente de criação do Cloud Manager deve ser feita procurando a `CM_BUILD`[variável de ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Da mesma forma, um perfil para uso somente fora do ambiente de criação do Cloud Manager deve ser feito verificando a ausência dessa variável.

Por exemplo, se você quiser gerar uma mensagem simples apenas quando a compilação for executada no Cloud Manager, você faria isso.

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

Além disso, se você quiser gerar uma mensagem simples apenas quando a compilação for executada fora do Cloud Manager, você faria isso.

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
>
>Os artefatos de um repositório Maven protegido por senha devem ser usados com muito cuidado, pois o código implantado por meio desse mecanismo não é executado atualmente em todas as [regras de qualidade do código](/help/implementing/cloud-manager/custom-code-quality-rules.md) implementadas nos quality gates (portais de qualidade) do Cloud Manager. Por isso, somente devem ser usados em casos raros e para código não vinculado ao AEM. É aconselhável implantar também as fonte Java e todo o código-fonte do projeto junto com o binário.

Para usar um repositório do Maven protegido por senha no Cloud Manager:

1. Especifique a senha (e, opcionalmente, o nome de usuário) como uma [variável de pipeline](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) de segredo.
1. Em seguida, faça referência a esse segredo dentro de um arquivo chamado `.cloudmanager/maven/settings.xml` no repositório Git, que segue o esquema [Arquivo de configurações Maven](https://maven.apache.org/settings.html).

Quando o processo de compilação do Cloud Manager é iniciado:

* O elemento `<servers>` neste arquivo será mesclado ao arquivo padrão `settings.xml` fornecido pelo Cloud Manager.
   * IDs de servidor que começam com `adobe` e `cloud-manager` são considerados reservados e não devem ser usados por servidores personalizados.
   * IDs de servidor que não correspondem a um desses prefixos ou ao ID padrão `central` nunca serão espelhados pelo Cloud Manager.
* Com esse arquivo em vigor, o ID do servidor seria referenciado de dentro de um elemento `<repository>` e/ou `<pluginRepository>` dentro do arquivo `pom.xml`.
* Geralmente, esses elementos `<repository>` e/ou `<pluginRepository>` ficam contidos dentro de um [Perfil específico do Cloud Manager](#activating-maven-profiles-in-cloud-manager), embora isso não seja estritamente necessário.

Como exemplo, digamos que o repositório esteja em `https://repository.myco.com/maven2`, o nome de usuário que o Cloud Manager deve usar é `cloudmanager` e a senha é `secretword`. Você seguiria as etapas a seguir.

1. Defina a senha como um segredo no pipeline.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Faça referência a isso no arquivo `.cloudmanager/maven/settings.xml`.

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

1. Por fim, faça referência ao ID do servidor dentro do arquivo `pom.xml`:

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

É uma boa prática implantar as fontes Java juntamente com o binário em um repositório Maven.

Para fazer isso, configure maven-source-plugin em seu projeto.

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

É uma boa prática implantar toda a fonte do projeto juntamente com o binário em um repositório Maven. Assim, será possível recompilar o artefato exato.

Para fazer isso, configure maven-assembly-plugin em seu projeto.

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

## Omissão de pacotes de conteúdo {#skipping-content-packages}

No Cloud Manager, as compilações podem produzir qualquer número de pacotes de conteúdo. Por uma variedade de motivos, pode ser desejável produzir um pacote de conteúdo, mas não implantá-lo. Um exemplo pode ser a criação de pacotes de conteúdo usados apenas para teste ou que são reempacotados em outra etapa do processo de criação. Ou seja, um subpacote de outro pacote.

Para acomodar esses cenários, o Cloud Manager procurará por uma propriedade chamada `cloudManagerTarget` nas propriedades dos pacotes de conteúdo criados. Se essa propriedade estiver definida como `none`, o pacote será ignorado e não será implantado.

O mecanismo para definir essa propriedade depende da forma como a compilação produz o pacote de conteúdo. Por exemplo, com `filevault-maven-plugin`, você configuraria o plug-in conforme descrito a seguir.

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

## Reutilização de artefato de compilação {#build-artifact-reuse}

Em muitos casos, um mesmo código é implantado em vários ambientes do AEM. Sempre que possível, o Cloud Manager evitará reconstruir a base de código quando detectar que a mesma Git Commit é usada em várias execuções de pipeline de pilha completa.

Quando uma execução é iniciada, a confirmação HEAD atual para o pipeline de ramificação é extraída. O hash de confirmação fica visível na interface do usuário e por meio da API. Quando a etapa de compilação for concluída com sucesso, os artefatos resultantes serão armazenados com base nesse hash de confirmação e poderão ser reutilizados em execuções de pipeline subsequentes.

Os pacotes serão reutilizados nos pipelines, se estiverem no mesmo programa. Ao procurar pacotes que possam ser reutilizados, o AEM ignora ramificações e reutiliza artefatos entre ramificações.

Quando ocorre uma reutilização, as etapas de compilação e qualidade do código são efetivamente substituídas pelos resultados da execução original. O arquivo de log da etapa de compilação listará os artefatos e as informações de execução que foram usadas originalmente para criá-los.

Veja a seguir um exemplo do log gerado.

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

1. A execução do Pipeline 1 primeiro criará os pacotes normalmente.
1. Em seguida, a execução do Pipeline 2 reutilizará os pacotes criados pelo Pipeline 1.

#### Exemplo 2 {#example-2}

Considere que seu programa tem duas ramificações:

* Ramificação `foo`
* Ramificação `bar`

Ambas as ramificações têm a mesma ID de confirmação.

1. Um pipeline de desenvolvimento compila e executa `foo`.
1. Posteriormente, um pipeline de produção compila e executa `bar`.

Nesse caso, o artefato de `foo` será reutilizado para o pipeline de produção desde que o mesmo hash de confirmação seja identificado.

### Recusa {#opting-out}

Se desejado, o comportamento de reutilização pode ser desativado para pipelines específicos, definindo a variável de pipeline `CM_DISABLE_BUILD_REUSE` como `true`. Se essa variável estiver definida, o hash de confirmação ainda será extraído e os artefatos resultantes serão armazenados para uso posterior, mas os artefatos armazenados anteriormente não serão reutilizados. Para entender esse comportamento, considere o cenário a seguir.

1. Um novo pipeline é criado.
1. O pipeline é executado (execução nº 1) e a confirmação HEAD atual é `becdddb`. A execução é bem-sucedida e os artefatos resultantes são armazenados.
1. A variável `CM_DISABLE_BUILD_REUSE` está definida.
1. O pipeline é executado novamente sem alterar o código. Embora haja artefatos armazenados associados a `becdddb`, eles não serão reutilizados devido à variável `CM_DISABLE_BUILD_REUSE`.
1. O código é alterado e o pipeline é executado. A confirmação HEAD agora é `f6ac5e6`. A execução é bem-sucedida e os artefatos resultantes são armazenados.
1. A variável `CM_DISABLE_BUILD_REUSE` é excluída.
1. O pipeline é executado novamente sem alterar o código. Como há artefatos armazenados associados a `f6ac5e6`, esses artefatos são reutilizados.

### Avisos {#caveats}

* Os artefatos de compilação não são reutilizados em diferentes programas, independentemente de o hash de confirmação ser idêntico.
* Os artefatos de compilação são reutilizados em um mesmo programa, mesmo que a ramificação e/ou o pipeline sejam diferentes.
* O [Manuseio de versão Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) substitui a versão do projeto somente nos pipelines de produção. Portanto, se a mesmo confirmação for usada em uma execução de implantação de desenvolvimento e em uma execução de pipeline de produção e o pipeline de implantação de desenvolvimento for executado primeiro, as versões serão implantadas no preparo e na produção sem serem alteradas. No entanto, uma tag ainda será criada nesse caso.
* Se a recuperação dos artefatos armazenados não for bem-sucedida, a etapa de criação será executada como se nenhum artefato tivesse sido armazenado.
* Variáveis de pipeline diferentes de `CM_DISABLE_BUILD_REUSE` não são consideradas quando o Cloud Manager decide reutilizar artefatos de build criados anteriormente.
