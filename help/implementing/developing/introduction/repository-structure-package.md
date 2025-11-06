---
title: Pacote de estrutura do repositório de projetos do AEM
description: Os projetos Maven no Adobe Experience Manager as a Cloud Service exigem uma definição de Subpacote de estrutura do repositório, cujo único objetivo é definir as raízes do repositório JCR em que os subpacotes de código do projeto são implantados.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# Pacote de estrutura do repositório de projetos do AEM

Os projetos Maven para Adobe Experience Manager as a Cloud Service exigem uma definição de subpacote de estrutura de repositório cujo único objetivo é definir as raízes do repositório JCR em que os subpacotes de código do projeto são implantados. Esse método garante que a instalação de pacotes no Experience Manager as a Cloud Service seja ordenada automaticamente pelas dependências de recurso JCR. Dependências ausentes podem levar a cenários em que subestruturas seriam instaladas antes de suas estruturas principais e, portanto, seriam removidas inesperadamente, interrompendo a implantação.

Se o pacote de código for implantado em um local **não coberto** pelo pacote de código, quaisquer recursos ancestrais (recursos JCR mais próximos à raiz JCR) deverão ser enumerados no pacote de estrutura do repositório. Esse processo é necessário para estabelecer essas dependências.

![Pacote de Estrutura do Repositório](./assets/repository-structure-packages.png)

O pacote de estrutura do repositório define o estado comum esperado de `/apps` que o validador de pacote usa para determinar as áreas &quot;seguras contra possíveis conflitos&quot;, pois são raízes padrão.

Os caminhos mais típicos a serem incluídos no pacote de estrutura do repositório são:

+ `/apps` que é um nó fornecido pelo sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...` e `/apps/sling/...` que fornecem sobreposições comuns para `/libs`.
+ `/apps/settings` que é o caminho raiz da configuração com reconhecimento de contexto compartilhado

Este subpacote **não tem** conteúdo e é composto apenas por um `pom.xml` definindo as raízes de filtro.

## Criação do pacote de estrutura do repositório

Para criar um pacote de estrutura de repositório para seu projeto Maven, crie um subprojeto Maven vazio, com o seguinte `pom.xml`, atualizando os metadados do projeto para estarem em conformidade com seu projeto Maven principal.

Atualize o `<filters>` para incluir todas as raízes de caminho de repositório JCR nas quais seus pacotes de código foram implantados.

Certifique-se de adicionar este novo subprojeto Maven à lista de projetos pai `<modules>`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
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
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlay structure, at each level here.

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

Para usar o pacote de estrutura do repositório, faça referência a ele por meio de todos os projetos Maven de pacote de código (os subpacotes que são implantados em `/apps`) por meio da configuração `<repositoryStructurePackage>` dos plug-ins Maven do pacote de conteúdo FileVault.

No `ui.apps/pom.xml` e em qualquer outro pacote de código `pom.xml`s, adicione uma referência à configuração do pacote de estrutura do repositório do projeto (#repository-structure-package) ao plug-in Maven do pacote FileVault.

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

Um caso de uso menos comum e mais complexo é o suporte à implantação de vários pacotes de código que são instalados nas mesmas áreas do repositório JCR.

Por exemplo:

+ O pacote de código A é implantado em `/apps/a`
+ O pacote de código B é implantado em `/apps/a/b`

Se uma dependência no nível do pacote não for estabelecida do pacote de código B no pacote de código A, o pacote de código B poderá implantar primeiro em `/apps/a`. Se for seguido pelo pacote de código A, que é implantado em `/apps/a`, o resultado será uma remoção do `/apps/a/b` instalado anteriormente.

Neste caso:

+ O pacote de código A deve definir um `<repositoryStructurePackage>` no pacote de estrutura do repositório do projeto (que deve ter um filtro para `/apps`).
+ O pacote de código B deve definir um `<repositoryStructurePackage>` no pacote de código A, pois o pacote de código B é implantado no espaço compartilhado pelo pacote de código A.

## Erros e depuração

Se os pacotes de estrutura do repositório não estiverem configurados corretamente, um erro será relatado na compilação Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Este erro indica que o pacote de códigos de quebra não tem um `<repositoryStructurePackage>` que lista `/apps/some/path` em sua lista de filtros.

## Recursos adicionais

+ [Plug-in Maven do Pacote de Conteúdo do FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
