---
title: 'Pacote de estrutura do repositório de projetos do AEM  '
description: A Adobe Experience Manager como um projeto do Cloud Service Maven requer uma definição do Subpacote da Estrutura do Repositório cujo único objetivo é definir as raízes do repositório do JCR nas quais os subpacotes de Código do projeto são implantados.
translation-type: tm+mt
source-git-commit: a6820eab30f2b318d62d2504cb17c12081a320a3
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---


# Pacote de estrutura do repositório de projetos do AEM

Os projetos Maven para Adobe Experience Manager como Cloud Service exigem uma definição de subpacote de estrutura de repositório cujo único objetivo é definir as raízes do repositório JCR nas quais os subpacotes de código do projeto são implantados. Isso garante que a instalação de pacotes no Experience Manager como Cloud Service seja automaticamente ordenada pelas dependências de recursos do JCR. As dependências em falta podem levar a cenários em que as subestruturas seriam instaladas antes das suas estruturas principais e, por conseguinte, seriam removidas inesperadamente, quebrando a implantação.

Se o pacote de código for implantado em um local **não coberto** pelo pacote de código, quaisquer recursos ancestrais (recursos JCR mais próximos à raiz JCR) deverão ser enumerados no pacote de estrutura do repositório para estabelecer essas dependências.

![Pacote de estrutura do repositório](./assets/repository-structure-packages.png)

O pacote de estrutura do repositório define o estado comum esperado do `/apps` qual o validador de pacote usa para determinar as áreas &quot;seguras de possíveis conflitos&quot;, já que elas são raízes padrão.

Os caminhos mais típicos a serem incluídos no pacote de estrutura do repositório são:

+ `/apps` que é um nó fornecido pelo sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`e `/apps/sling/...` que fornecem sobreposições comuns para `/libs`.
+ `/apps/settings` que é o caminho raiz de configuração compartilhado com reconhecimento de contexto

Observe que esse subpacote **não tem** nenhum conteúdo e é composto apenas por uma `pom.xml` definição das raízes do filtro.

## Criação do pacote de estrutura do repositório

Para criar um pacote de estrutura de repositório para seu projeto Maven, crie um novo subprojeto Maven vazio, com o seguinte `pom.xml`, atualizando os metadados do projeto para que eles estejam em conformidade com seu projeto Maven pai.

Atualize o para incluir todas as raízes de caminho do repositório JCR nas quais seus pacotes de código são implantados. `<filters>`

Certifique-se de adicionar esse novo subprojeto Maven à `<modules>` lista de projetos pai.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Referência ao pacote de estrutura do repositório

Para usar o pacote de estrutura do repositório, consulte-o por meio de todos os pacotes de código (os subpacotes que implantam em `/apps`) projetos Maven por meio da configuração de plug-ins Maven do pacote de conteúdo FileVault `<repositoryStructurePackage>` .

No `ui.apps/pom.xml`, e em qualquer outro pacote `pom.xml`de códigos, adicione uma referência à configuração do pacote de estrutura de repositório (#repository-structure-package) do projeto ao plug-in FileVault package Maven.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## Caso de uso do pacote de vários códigos

Um caso de uso menos comum e mais complexo é suportar a implantação de vários pacotes de código que são instalados nas mesmas áreas do repositório JCR.

Por exemplo:

+ Pacote de código A implementa em `/apps/a`
+ O pacote de código B é implantado em `/apps/a/b`

Se uma dependência de nível de pacote não for estabelecida a partir do pacote de código B no pacote de código A, o pacote de código B pode ser implantado primeiro em `/apps/a`, seguido pelo pacote de código B, que é implantado em `/apps/a`, resultando na remoção do pacote instalado anteriormente `/apps/a/b`.

Neste caso:

+ O pacote de código A deve definir um `<repositoryStructurePackage>` no pacote de estrutura de repositório do projeto (que deve ter um filtro para `/apps`).
+ O pacote de código B deve definir um `<repositoryStructurePackage>` no pacote de código A, pois o pacote de código B é implantado no espaço compartilhado pelo pacote de código A.

## Erros e depuração

Se os pacotes de estrutura do repositório não estiverem configurados corretamente, um erro será reportado na compilação Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Isso indica que o pacote de código de quebra não tem uma lista `<repositoryStructurePackage>` que  `/apps/some/path` na lista do filtro.

## Recursos adicionais

+ [Plug-in FileVault Content Package Maven](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
