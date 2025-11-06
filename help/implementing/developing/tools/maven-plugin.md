---
title: Plug-in Maven do pacote de conteúdo do Adobe
description: Usar o plug-in Maven do pacote de conteúdo para implantar aplicativos do AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---

# Plug-in Maven do pacote de conteúdo do Adobe {#adobe-content-package-maven-plugin}

Use o plug-in Maven do pacote de conteúdo do Adobe para integrar tarefas de implantação e gerenciamento de pacotes em seus projetos Maven.

A implantação dos pacotes construídos no AEM é realizada pelo plug-in Maven do Pacote de conteúdo do Adobe e permite a automação das tarefas normalmente realizadas usando o [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) do AEM

* Crie novos pacotes a partir de arquivos no sistema de arquivos.
* Instalar e desinstalar pacotes no AEM.
* Crie pacotes que já estão definidos no AEM.
* Obtenha uma lista de pacotes instalados no AEM.
* Remover um pacote do AEM.

Este documento detalha como usar o Maven para gerenciar essas tarefas. No entanto, também é importante entender [como os projetos da AEM e seus pacotes estão estruturados](#aem-project-structure).

>[!NOTE]
>
>Use sempre as versões mais recentes disponíveis desses plug-ins.

>[!NOTE]
>
>A **criação** do pacote agora pertence ao [Plug-in Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/).
>
>Este artigo descreve a **implantação** dos pacotes construídos para o AEM conforme executado pelo plug-in Maven do pacote de conteúdo do Adobe.

## Pacotes e a estrutura do projeto AEM {#aem-project-structure}

A AEM as a Cloud Service segue as práticas recomendadas mais recentes para o gerenciamento de pacotes e a estrutura do projeto, conforme implementado pelo Arquétipo de projeto mais recente da AEM.

>[!TIP]
>
>Consulte o artigo [Estrutura de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) na documentação do AEM as a Cloud Service e da documentação do [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR). Ambos são totalmente compatíveis com o AEM 6.5.

## Obter o plug-in Maven do pacote de conteúdo {#obtaining-the-content-package-maven-plugin}

O plug-in está disponível no [Repositório Central Maven](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public).

## Metas e parâmetros do plug-in Maven do pacote de conteúdo

Para usar o Plug-in Maven do pacote de conteúdo, adicione o seguinte elemento de plug-in dentro do elemento de build do seu arquivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para permitir que o Maven baixe o plug-in, use o perfil fornecido na seção [Obtendo o plug-in Maven do pacote de conteúdo](#obtaining-the-content-package-maven-plugin) nesta página.

## Metas do plug-in Maven do pacote de conteúdo {#goals-of-the-content-package-maven-plugin}

As metas e os parâmetros de meta fornecidos pelo plug-in do Pacote de conteúdo são descritos nas seções a seguir. Os parâmetros descritos na seção Parâmetros Comuns podem ser usados para a maioria das metas. Os parâmetros que se aplicam a uma meta são descritos na seção para essa meta.

### Prefixo do plug-in {#plugin-prefix}

O prefixo do plug-in é `content-package`. Use esse prefixo para executar uma meta a partir da linha de comando, como no exemplo a seguir:

```shell
mvn content-package:build
```

### Prefixo do parâmetro {#parameter-prefix}

A menos que seja observado o contrário, as metas e os parâmetros do plug-in usam o prefixo `vault`, como no exemplo a seguir:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Metas que usam proxies para o AEM usam a primeira configuração de proxy válida encontrada nas configurações Maven. Se nenhuma configuração de proxy for encontrada, nenhum proxy será usado. Consulte o parâmetro `useProxy` na seção [Parâmetros Comuns](#common-parameters).

### Parâmetros comuns {#common-parameters}

Os parâmetros na tabela a seguir são comuns a todas as metas, exceto quando anotados na coluna **Metas**.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição | Metas |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Não | `false` | Um valor de `true` causa falha na compilação quando ocorre um erro. Um valor de `false` faz com que a compilação ignore o erro. | Todas as metas exceto `package` |
| `name` | `String` | `build`: Sim, `install`: Não, `rm`: Sim | `build`: Nenhum padrão, `install`: O valor da propriedade `artifactId` do projeto Maven | O nome do pacote no qual agir | Todas as metas exceto `ls` |
| `password` | `String` | Sim | `admin` | A senha usada para autenticação com o AEM | Todas as metas exceto `package` |
| `serverId` | `String` | Não | A ID do servidor da qual recuperar o nome de usuário e a senha para autenticação | Todas as metas exceto `package` |
| `targetURL` | `String` | Sim | `http://localhost:4502/crx/packmgr/service.jsp` | O URL da API de serviço HTTP do gerenciador de pacotes do AEM | Todas as metas exceto `package` |
| `timeout` | `int` | Não | `5` | O tempo limite da conexão para comunicação com o serviço do gerenciador de pacotes, em segundos | Todas as metas exceto `package` |
| `useProxy` | `boolean` | Não | `true` | Um valor de `true` faz com que o Maven use a primeira configuração de proxy ativa encontrada para solicitações de proxy para o Gerenciador de pacotes. | Todas as metas exceto `package` |
| `userId` | `String` | Sim | `admin` | O nome de usuário a ser autenticado com o AEM | Todas as metas exceto `package` |
| `verbose` | `boolean` | Não | `false` | Habilita ou desabilita o log detalhado | Todas as metas exceto `package` |

### build {#build}

Cria um pacote de conteúdo que já está definido em uma instância do AEM.

>[!NOTE]
>
>Essa meta não precisa ser executada em um projeto Maven.

#### Parâmetros {#parameters}

Todos os parâmetros da meta de compilação estão descritos na seção [Parâmetros Comuns](#common-parameters).

### instalar {#install}

Instala um pacote no repositório. A execução dessa meta não requer um projeto Maven. A meta está vinculada à fase `install` do ciclo de vida da compilação Maven.

#### Parâmetros {#parameters-1}

Além dos parâmetros a seguir, consulte as descrições na seção [Parâmetros Comuns](#common-parameters).

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `artifact` | `String` | Não | O valor da propriedade `artifactId` do projeto Maven | Uma cadeia de caracteres do formulário `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Não | Nenhum | A ID do artefato a ser instalado |
| `groupId` | `String` | Não | Nenhum | O `groupId` do artefato a ser instalado |
| `install` | `boolean` | Não | `true` | Determina se o pacote deve ser descompactado automaticamente quando carregado |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Não | O valor da variável de sistema `localRepository` | O repositório Maven local que não pode ser configurado usando a configuração do plug-in, pois a propriedade do sistema é sempre usada |
| `packageFile` | `java.io.File` | Não | O artefato principal definido para o projeto Maven | O nome do arquivo de pacote a ser instalado |
| `packaging` | `String` | Não | `zip` | O tipo de pacote do artefato a ser instalado |
| `pomRemoteRepositories` | `java.util.List` | Sim | O valor da propriedade `remoteArtifactRepositories` que é definida para o projeto Maven | Este valor não pode ser configurado usando a configuração de plug-in e deve ser especificado no projeto. |
| `project` | `org.apache.maven.project.MavenProject` | Sim | O projeto para o qual o plug-in está configurado | O projeto Maven que está implícito porque o projeto contém a configuração do plug-in |
| `repositoryId` (POM), `repoID` (linha de comando) | `String` | Não | `temp` | A ID do repositório do qual o artefato é recuperado |
| `repositoryUrl` (POM), `repoURL` (linha de comando) | `String` | Não | Nenhum | O URL do repositório do qual o artefato é recuperado |
| version | String | Não | Nenhum | A versão do artefato a ser instalado |

### ls {#ls}

Lista os pacotes implantados no [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md).

#### Parâmetros {#parameters-2}

Todos os parâmetros da meta ls estão descritos na seção [Parâmetros Comuns](#common-parameters).

### rm {#rm}

Remove um pacote do [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md).

#### Parâmetros {#parameters-3}

Todos os parâmetros da meta rm estão descritos na seção [Parâmetros Comuns](#common-parameters).

### desinstalar {#uninstall}

Desinstala um pacote. O pacote permanece no servidor no estado desinstalado.

#### Parâmetros {#parameters-4}

Todos os parâmetros da meta de desinstalação estão descritos na seção [Parâmetros Comuns](#common-parameters).


### ajuda {#help}

#### Parâmetros {#parameters-6}

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `detail` | `boolean` | Não | `false` | Determina se devem ser exibidas todas as propriedades definíveis para cada meta |
| `goal` | `String` | Não | Nenhum | Esses parâmetros definem o nome da meta para a qual mostrar ajuda. Se nenhum valor for especificado, a ajuda para todas as metas será exibida. |
| `indentSize` | `int` | Não | `2` | O número de espaços a serem usados para o recuo de cada nível (deve ser positivo se definido) |
| `lineLength` | `int` | Não | `80` | O comprimento máximo de uma linha de exibição (deve ser positivo se definido) |

## Inclusão de uma imagem em miniatura ou arquivo de propriedades no pacote {#including-a-thumbnail-image-or-properties-file-in-the-package}

Substitua os arquivos de configuração de pacote padrão para personalizar as propriedades do pacote. Por exemplo, inclua uma imagem em miniatura para distinguir o pacote no [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md).

Os arquivos de origem podem estar localizados em qualquer lugar do sistema de arquivos. No arquivo POM, defina os recursos de compilação para copiar os arquivos de origem no `target/vault-work/META-INF` para inclusão no pacote.

O código POM a seguir adiciona os arquivos da pasta `META-INF` da origem do projeto ao pacote:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

O código POM a seguir adiciona apenas uma imagem em miniatura ao pacote. A imagem em miniatura deve se chamar `thumbnail.png` e deve estar localizada na pasta `META-INF/vault/definition` do pacote. Neste exemplo, o arquivo de origem está localizado na pasta `/src/main/content/META-INF/vault/definition` do projeto:

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

## Uso do Arquétipo de Projetos AEM para Gerar Projetos AEM {#using-archetypes}

O Arquétipo de projeto do AEM mais recente implementa a estrutura do pacote de práticas recomendadas para implementações locais e do AMS e é recomendado para todos os projetos do AEM.

>[!TIP]
>
>Consulte o artigo [Estrutura de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) na documentação do AEM as a Cloud Service e da documentação do [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR). Ambos são totalmente compatíveis com o AEM 6.5.
