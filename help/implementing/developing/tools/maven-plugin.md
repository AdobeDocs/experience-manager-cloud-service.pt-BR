---
title: Plug-in Adobe Content Package Maven
description: Use o plug-in Content Package Maven para implantar aplicativos AEM
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 7%

---


# Plug-in Adobe Content Package Maven {#adobe-content-package-maven-plugin}

Use o plug-in Adobe Content Package Maven para integrar tarefas de gerenciamento e implantação de pacotes aos projetos Maven.

A implantação dos pacotes construídos para AEM é realizada pelo plug-in Adobe Content Package Maven e permite a automação do tarefa normalmente executado usando AEM Gerenciador de pacotes:

* Crie novos pacotes a partir de arquivos no sistema de arquivos.
* Instale e desinstale pacotes no AEM.
* Crie pacotes que já estão definidos no AEM.
* Obtenha uma lista de pacotes instalados no AEM.
* Remova um pacote do AEM.

Este documento detalha como usar o Maven para gerenciar essas tarefas. No entanto, também é importante entender [como AEM projetos e seus pacotes são estruturados.](#aem-project-structure)

>[!NOTE]
>
>A criação do pacote agora pertence ao [plug-in Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/). A implantação dos pacotes construídos para AEM é realizada pelo plug-in Adobe Content Package Maven, conforme descrito aqui.

## Pacotes e a estrutura do projeto AEM {#aem-project-structure}

AEM 6.5 segue as práticas recomendadas mais recentes para o gerenciamento de pacotes e a estrutura de projetos, conforme implementado pelo último AEM do Project Archetype para implementações locais e AMS.

>[!TIP]
>
>Para obter mais detalhes, consulte o artigo [AEM Estrutura do Projeto](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) no AEM como documentação de Cloud Service, bem como a documentação [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html). Ambas são totalmente suportadas pela AEM 6.5.

## Obtenção do plug-in Content Package Maven {#obtaining-the-content-package-maven-plugin}

O plug-in está disponível no [Repositório Central Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Metas e parâmetros do plug-in do Content Package Maven

Para usar o plug-in Content Package Maven, adicione o seguinte elemento de plug-in dentro do elemento build do arquivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para permitir que o Maven baixe o plug-in, use o perfil fornecido na seção [Obtenção do plug-in Content Package Maven](#obtaining-the-content-package-maven-plugin) nesta página.

## Metas do plug-in Content Package Maven {#goals-of-the-content-package-maven-plugin}

Os parâmetros de metas e metas fornecidos pelo plug-in Pacote de conteúdo são descritos nas seções a seguir. Os parâmetros descritos na seção Parâmetros comuns podem ser usados para a maioria das metas. Os parâmetros que se aplicam a uma meta são descritos na seção para essa meta.

### Prefixo do plug-in {#plugin-prefix}

O prefixo do plug-in é `content-package`. Use esse prefixo para executar uma meta da linha de comando, como no exemplo a seguir:

```shell
mvn content-package:build
```

### Prefixo do parâmetro {#parameter-prefix}

Salvo indicação em contrário, os parâmetros e metas do plug-in usam o prefixo `vault`, como no exemplo a seguir:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

As metas que usam proxy para AEM usam a primeira configuração válida de proxy encontrada nas configurações de Maven. Se nenhuma configuração de proxy for encontrada, nenhum proxy será usado. Consulte o parâmetro `useProxy` na seção [Parâmetros Comuns](#common-parameters).

### Parâmetros comuns {#common-parameters}

Os parâmetros na tabela a seguir são comuns a todos os objetivos, exceto quando anotados na coluna **Metas**.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição | Metas |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Não | `false` | Um valor de `true` faz com que a compilação falhe quando ocorre um erro. Um valor de `false` faz com que a compilação ignore o erro. | Todos os objetivos exceto `package` |
| `name` | `String` | `build`: Sim,  `install`: Não,  `rm`: Sim | `build`: Sem padrão,  `install`: O valor da  `artifactId` propriedade do projeto Maven | O nome do pacote em que agir | Todos os objetivos exceto `ls` |
| `password` | `String` | Sim | `admin` | A senha usada para autenticação com AEM | Todos os objetivos exceto `package` |
| `serverId` | `String` | Não | A ID do servidor da qual recuperar o nome de usuário e a senha para autenticação | Todos os objetivos exceto `package` |
| `targetURL` | `String` | Sim | `http://localhost:4502/crx/packmgr/service.jsp` | O URL da API de serviço HTTP do gerenciador de pacote AEM | Todos os objetivos exceto `package` |
| `timeout` | `int` | Não | `5` | O tempo limite da conexão para comunicação com o serviço gerenciador de pacotes, em segundos | Todos os objetivos exceto `package` |
| `useProxy` | `boolean` | Não | `true` | Um valor de `true` faz com que o Maven use a primeira configuração de proxy ativa encontrada para solicitar proxy ao Gerenciador de pacotes. | Todos os objetivos exceto `package` |
| `userId` | `String` | Sim | `admin` | O nome de usuário para autenticação com AEM | Todos os objetivos exceto `package` |
| `verbose` | `boolean` | Não | `false` | Ativa ou desativa o registro detalhado | Todos os objetivos exceto `package` |

### build {#build}

Cria um pacote de conteúdo que já está definido em uma instância AEM.

>[!NOTE]
>
>Este objetivo não precisa ser executado dentro de um projeto Maven.

#### Parâmetros {#parameters}

Todos os parâmetros da meta de compilação são descritos na seção [Parâmetros Comuns](#common-parameters).

### instalar {#install}

Instala um pacote no repositório. A execução desta meta não requer um projeto Maven. A meta está vinculada à fase `install` do ciclo de vida da compilação Maven.

#### Parâmetros {#parameters-1}

Além dos parâmetros a seguir, consulte as descrições na seção [Parâmetros Comuns](#common-parameters).

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|---|
| `artifact` | `String` | Não | O valor da propriedade `artifactId` do projeto Maven | Uma string do formulário `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Não | Nenhum | A ID do artefato a ser instalado |
| `groupId` | `String` | Não | Nenhum | O `groupId` do artefato a ser instalado |
| `install` | `boolean` | Não | `true` | Determina se o pacote deve ser desempacotado automaticamente quando for carregado |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Não | O valor da variável do sistema `localRepository` | O repositório Maven local que não pode ser configurado usando a configuração do plug-in, pois a propriedade do sistema é sempre usada |
| `packageFile` | `java.io.File` | Não | O artefato principal definido para o projeto Maven | O nome do arquivo de pacote a ser instalado |
| `packaging` | `String` | Não | `zip` | O tipo de empacotamento do artefato a ser instalado |
| `pomRemoteRepositories` | `java.util.List` | Sim | O valor da propriedade `remoteArtifactRepositories` definida para o projeto Maven | Este valor não pode ser configurado usando a configuração do plug-in e deve ser especificado no projeto. |
| `project` | `org.apache.maven.project.MavenProject` | Sim | O projeto para o qual o plug-in está configurado | O projeto Maven que está implícito porque o projeto contém a configuração do plug-in |
| `repositoryId` (POM),  `repoID` (linha de comando) | `String` | Não | `temp` | A ID do repositório a partir do qual o artefato é recuperado |
| `repositoryUrl` (POM),  `repoURL` (linha de comando) | `String` | Não | Nenhum | O URL do repositório do qual o artefato é recuperado |
| version | Sequência de caracteres | Não | Nenhum | A versão do artefato a ser instalada |

### ls {#ls}

Lista os pacotes implantados no Package Manager.

#### Parâmetros {#parameters-2}

Todos os parâmetros da meta ls estão descritos na seção [Parâmetros Comuns](#common-parameters).

### rm {#rm}

Remove um pacote do Gerenciador de pacotes.

#### Parâmetros {#parameters-3}

Todos os parâmetros do objetivo rm estão descritos na seção [Parâmetros Comuns](#common-parameters).

### desinstalar {#uninstall}

Desinstala um pacote. O pacote permanece no servidor no estado desinstalado.

#### Parâmetros {#parameters-4}

Todos os parâmetros do objetivo de desinstalação estão descritos na seção [Parâmetros Comuns](#common-parameters).

### pacote {#package}

Cria um pacote de conteúdo. A configuração padrão do objetivo do pacote inclui o conteúdo do diretório em que os arquivos compilados são salvos. A execução da meta do pacote requer que a fase de compilação tenha sido concluída. A meta do pacote está vinculada à fase do pacote do ciclo de vida da construção Maven.

#### Parâmetros {#parameters-5}

Além dos seguintes parâmetros, consulte a descrição do parâmetro `name` na seção [Parâmetros Comuns](#common-parameters).

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | Não | Nenhum | A configuração do arquivo a ser usada |
| `builtContentDirectory` | `java.io.File` | Sim | O valor do diretório de saída da compilação Maven | O diretório que contém o conteúdo a ser incluído no pacote |
| `dependencies` | `java.util.List` | Não | Nenhum |  |
| `embeddedTarget` | `java.lang.String` | Não | Nenhum |  |
| `embeddeds` | `java.util.List` | Não | Nenhum |  |
| `failOnMissingEmbed` | `boolean` | Sim | `false` | Um valor de `true` faz com que a compilação falhe quando um artefato incorporado não for encontrado nas dependências do projeto. Um valor de `false` faz com que a compilação ignore esses erros. |
| `filterSource` | `java.io.File` | Não | Nenhum | Esse parâmetro define um arquivo que especifica a origem do filtro de espaço de trabalho. Os filtros especificados na configuração e inseridos por meio de bordas ou subpacotes são unidos ao conteúdo do arquivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | Não | Nenhum | Esse parâmetro contém elementos de filtro que definem o conteúdo do pacote. Quando executados, os filtros são incluídos no arquivo `filter.xml`. Consulte a seção [Usando Filtros](#using-filters) abaixo. |
| `finalName` | `java.lang.String` | Sim | O `finalName` definido no projeto Maven (fase de compilação) | O nome do arquivo ZIP do pacote gerado, sem a extensão de arquivo `.zip` |
| `group` | `java.lang.String` | Sim | O `groupID` definido no projeto Maven | O `groupId` do pacote de conteúdo gerado que faz parte do caminho de instalação do público alvo para o pacote de conteúdo |
| `outputDirectory` | `java.io.File` | Sim | O diretório build definido no projeto Maven | O diretório local onde o pacote de conteúdo é salvo |
| `prefix` | `java.lang.String` | Não | Nenhum |  |
| `project` | `org.apache.maven.project.MavenProject` | Sim | Nenhum | O projeto Maven |
| `properties` | `java.util.Map` | Não | Nenhum | Esses parâmetros definem propriedades adicionais que podem ser definidas no arquivo `properties.xml`. Essas propriedades não podem substituir as seguintes propriedades predefinidas: `group` (use o parâmetro `group` para definir), `name` (use o parâmetro `name` para definir), `version` (use o parâmetro `version` para definir), `description` (defina a partir da descrição do projeto), `groupId` (`groupId` do descritor do projeto Maven), `artifactId` (&lt;a11000/> o descritor do projeto Maven), `dependencies` (use o parâmetro `dependencies` para definir), `createdBy` (o valor da propriedade do sistema `user.name`), `created` (a hora atual do sistema), `requiresRoot` (use o parâmetro `requiresRoot` para definir), &lt;a11 8/> (gerado automaticamente pelo nome do grupo e do pacote)`artifactId``packagePath` |
| `requiresRoot` | `boolean` | Sim | falso | Define se o pacote requer raiz. Isso se tornará a propriedade `requiresRoot` do arquivo `properties.xml`. |
| `subPackages` | `java.util.List` | Não | Nenhum |  |
| `version` | `java.lang.String` | Sim | A versão definida no projeto Maven | A versão do pacote de conteúdo |
| `workDirectory` | `java.io.File` | Sim | O diretório definido no projeto Maven (fase de compilação) | O diretório que contém o conteúdo a ser incluído no pacote |

#### Usando filtros {#using-filters}

Use o elemento filtros para definir o conteúdo do pacote. Os filtros são adicionados ao elemento `workspaceFilter` no arquivo `META-INF/vault/filter.xml` do pacote.

O exemplo de filtro a seguir mostra a estrutura XML a ser usada:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### Modo de importação {#import-mode}

O elemento `mode` define como o conteúdo é o repositório é afetado quando o pacote é importado. Os seguintes valores podem ser usados:

* **Mesclar:** o conteúdo no pacote que ainda não está no repositório é adicionado. O conteúdo que está no pacote e no repositório não é alterado. Nenhum conteúdo é removido do repositório.
* **Substituir:** o conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo é removido do repositório quando não existe no pacote.
* **Atualização:** o conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo existente é removido do repositório.

Quando o filtro não contém nenhum elemento `mode`, o valor padrão de `replace` é usado.

### ajuda {#help}

#### Parâmetros {#parameters-6}

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `detail` | `boolean` | Não | `false` | Determina se todas as propriedades que podem ser definidas para cada meta devem ser exibidas |
| `goal` | `String` | Não | Nenhum | Esses parâmetros definem o nome da meta para a qual mostrar ajuda. Se nenhum valor for especificado, a ajuda para todas as metas será exibida. |
| `indentSize` | `int` | Não | `2` | O número de espaços a serem usados para o recuo de cada nível (deve ser positivo se definido) |
| `lineLength` | `int` | Não | `80` | O comprimento máximo de uma linha de exibição (deve ser positivo se definido) |

## Incluindo uma imagem em miniatura ou um arquivo de propriedades no pacote {#including-a-thumbnail-image-or-properties-file-in-the-package}

Substitua os arquivos de configuração do pacote padrão para personalizar as propriedades do pacote. Por exemplo, inclua uma imagem em miniatura para distinguir o pacote no Package Manager e no Package Share.

Os arquivos de origem podem ser localizados em qualquer lugar no seu sistema de arquivos. No arquivo POM, defina os recursos de compilação para copiar os arquivos de origem para `target/vault-work/META-INF` para inclusão no pacote.

O seguinte código POM adiciona os arquivos na pasta `META-INF` da fonte do projeto ao pacote:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

O código POM a seguir adiciona apenas uma imagem em miniatura ao pacote. A imagem em miniatura deve ser chamada de `thumbnail.png` e deve estar localizada na pasta `META-INF/vault/definition` do pacote. Neste exemplo, o arquivo de origem está localizado na pasta `/src/main/content/META-INF/vault/definition` do projeto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Usando o AEM Project Archetype para Gerar AEM Projetos {#using-archetypes}

O AEM mais recente do Project Archetype implementa a estrutura do pacote de práticas recomendadas para implementações locais e AMS e é recomendado para todos os projetos AEM.

>[!TIP]
>
>Para obter mais detalhes, consulte o artigo [AEM Estrutura do Projeto](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) no AEM como documentação de Cloud Service, bem como a documentação [AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html). Ambas são totalmente suportadas pela AEM 6.5.
