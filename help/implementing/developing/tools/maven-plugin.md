---
title: Plug-in Maven do pacote de conteúdo do Adobe
description: Usar o plug-in Maven do pacote de conteúdo para implantar aplicativos AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 6%

---

# Plug-in Maven do pacote de conteúdo do Adobe {#adobe-content-package-maven-plugin}

Use o plug-in Adobe Content Package Maven para integrar tarefas de implantação e gerenciamento de pacotes em seus projetos Maven.

A implantação dos pacotes construídos no AEM é realizada pelo plug-in Adobe Content Package Maven e permite a automação das tarefas normalmente realizadas usando o AEM [Gerenciador de pacotes:](/help/implementing/developing/tools/package-manager.md)

* Crie novos pacotes a partir de arquivos no sistema de arquivos.
* Instale e desinstale pacotes no AEM.
* Criar pacotes que já estão definidos no AEM.
* Obtenha uma lista de pacotes que estão instalados no AEM.
* Remover um pacote do AEM.

Este documento detalha como usar o Maven para gerenciar essas tarefas. No entanto, também é importante compreender [como os projetos AEM e seus pacotes são estruturados.](#aem-project-structure)

>[!NOTE]
>
>Pacote **criação** agora é de propriedade da [Plug-in Apache Jackrabbit FileVault Package Maven.](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>
>* A variável `content-package-maven-plugin` O não é mais compatível com pacotes da versão 1.0.2.
>* Este artigo descreve as **implantação** dos pacotes construídos para o AEM é executado pelo plug-in Adobe Content Package Maven.

## Pacotes e a estrutura do projeto AEM {#aem-project-structure}

O AEM as a Cloud Service segue as práticas recomendadas mais recentes para o gerenciamento de pacotes e a estrutura do projeto, conforme implementado pelo Arquétipo de projeto AEM mais recente.

>[!TIP]
>
>Consulte a [Estrutura de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) artigo na documentação do AEM as a Cloud Service e na [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) documentação. Ambos são totalmente compatíveis com AEM 6.5.

## Obter o plug-in Maven do pacote de conteúdo {#obtaining-the-content-package-maven-plugin}

O plug-in está disponível no [Repositório central Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

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

Para permitir que o Maven baixe o plug-in, use o perfil fornecido na [Obter o plug-in Maven do pacote de conteúdo](#obtaining-the-content-package-maven-plugin) nesta página.

## Metas do plug-in Maven do pacote de conteúdo {#goals-of-the-content-package-maven-plugin}

As metas e os parâmetros de meta fornecidos pelo plug-in do Pacote de conteúdo são descritos nas seções a seguir. Os parâmetros descritos na seção Parâmetros Comuns podem ser usados para a maioria das metas. Os parâmetros que se aplicam a uma meta são descritos na seção para essa meta.

### Prefixo do plug-in {#plugin-prefix}

O prefixo do plug-in é `content-package`. Use esse prefixo para executar uma meta a partir da linha de comando, como no exemplo a seguir:

```shell
mvn content-package:build
```

### Prefixo do parâmetro {#parameter-prefix}

A menos que indicado de outra forma, as metas e os parâmetros do plug-in usam o `vault` como no exemplo a seguir:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Metas que usam proxies para AEM usam a primeira configuração de proxy válida encontrada nas configurações Maven. Se nenhuma configuração de proxy for encontrada, nenhum proxy será usado. Consulte a `useProxy` parâmetro no [Parâmetros comuns](#common-parameters) seção.

### Parâmetros comuns {#common-parameters}

Os parâmetros na tabela a seguir são comuns a todas as metas, exceto quando anotados na variável **Metas** coluna.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição | Metas |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Não | `false` | Um valor de `true` causa falha na criação quando ocorre um erro. Um valor de `false` faz com que a build ignore o erro. | Todas as metas exceto `package` |
| `name` | `String` | `build`: Sim, `install`: Não, `rm`: Sim | `build`: Sem padrão, `install`: o valor de `artifactId` propriedade do projeto Maven | O nome do pacote no qual agir | Todas as metas exceto `ls` |
| `password` | `String` | Sim | `admin` | A senha usada para autenticação com AEM | Todas as metas exceto `package` |
| `serverId` | `String` | Não | A ID do servidor da qual recuperar o nome de usuário e a senha para autenticação | Todas as metas exceto `package` |
| `targetURL` | `String` | Sim | `http://localhost:4502/crx/packmgr/service.jsp` | O URL da API de serviço HTTP do gerenciador de pacotes AEM | Todas as metas exceto `package` |
| `timeout` | `int` | Não | `5` | O tempo limite da conexão para comunicação com o serviço do gerenciador de pacotes, em segundos | Todas as metas exceto `package` |
| `useProxy` | `boolean` | Não | `true` | Um valor de `true` faz com que o Maven use a primeira configuração de proxy ativa encontrada para solicitações de proxy para o Gerenciador de pacotes. | Todas as metas exceto `package` |
| `userId` | `String` | Sim | `admin` | O nome de usuário a ser autenticado com AEM | Todas as metas exceto `package` |
| `verbose` | `boolean` | Não | `false` | Habilita ou desabilita o log detalhado | Todas as metas exceto `package` |

### build {#build}

Cria um pacote de conteúdo que já está definido em uma instância do AEM.

>[!NOTE]
>
>Essa meta não precisa ser executada em um projeto Maven.

#### Parâmetros {#parameters}

Todos os parâmetros da meta de build estão descritos no [Parâmetros comuns](#common-parameters) seção.

### instalar {#install}

Instala um pacote no repositório. A execução dessa meta não requer um projeto Maven. A meta está vinculada à variável `install` fase do ciclo de vida de compilação Maven.

#### Parâmetros {#parameters-1}

Além dos parâmetros a seguir, consulte as descrições nas [Parâmetros comuns](#common-parameters) seção.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `artifact` | `String` | Não | O valor de `artifactId` propriedade do projeto Maven | Uma cadeia de caracteres do formulário `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Não | Nenhum | A ID do artefato a ser instalado |
| `groupId` | `String` | Não | Nenhum | A variável `groupId` do artefato a ser instalado |
| `install` | `boolean` | Não | `true` | Determina se o pacote deve ser descompactado automaticamente quando carregado |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Não | O valor de `localRepository` variável de sistema | O repositório Maven local que não pode ser configurado usando a configuração do plug-in, pois a propriedade do sistema é sempre usada |
| `packageFile` | `java.io.File` | Não | O artefato principal definido para o projeto Maven | O nome do arquivo de pacote a ser instalado |
| `packaging` | `String` | Não | `zip` | O tipo de pacote do artefato a ser instalado |
| `pomRemoteRepositories` | `java.util.List` | Sim | O valor de `remoteArtifactRepositories` propriedade definida para o projeto Maven | Este valor não pode ser configurado usando a configuração de plug-in e deve ser especificado no projeto. |
| `project` | `org.apache.maven.project.MavenProject` | Sim | O projeto para o qual o plug-in está configurado | O projeto Maven que está implícito porque o projeto contém a configuração do plug-in |
| `repositoryId` (POM), `repoID` (linha de comando) | `String` | Não | `temp` | A ID do repositório do qual o artefato é recuperado |
| `repositoryUrl` (POM), `repoURL` (linha de comando) | `String` | Não | Nenhum | O URL do repositório do qual o artefato é recuperado |
| version | String | Não | Nenhum | A versão do artefato a ser instalado |

### ls {#ls}

Lista os pacotes implantados em [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md).

#### Parâmetros {#parameters-2}

Todos os parâmetros da meta ls estão descritos no [Parâmetros comuns](#common-parameters) seção.

### rm {#rm}

Remove um pacote de [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md).

#### Parâmetros {#parameters-3}

Todos os parâmetros da meta do rm estão descritos na [Parâmetros comuns](#common-parameters) seção.

### desinstalar {#uninstall}

Desinstala um pacote. O pacote permanece no servidor no estado desinstalado.

#### Parâmetros {#parameters-4}

Todos os parâmetros da meta de desinstalação estão descritos no [Parâmetros comuns](#common-parameters) seção.

### pacote {#package}

Cria um pacote de conteúdo. A configuração padrão da meta do pacote inclui o conteúdo do diretório onde os arquivos compilados são salvos. A execução da meta do pacote exige que a fase de compilação tenha sido concluída. A meta do pacote é vinculada à fase do pacote do ciclo de vida de compilação Maven.

#### Parâmetros {#parameters-5}

Além dos parâmetros a seguir, consulte a descrição da variável `name` parâmetro no [Parâmetros comuns](#common-parameters) seção.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | Não | Nenhum | A configuração de arquivamento a ser usada |
| `builtContentDirectory` | `java.io.File` | Sim | O valor do diretório de saída da compilação Maven | O diretório que contém o conteúdo a ser incluído no pacote |
| `dependencies` | `java.util.List` | Não | Nenhum |  |
| `embeddedTarget` | `java.lang.String` | Não | Nenhum |  |
| `embeddeds` | `java.util.List` | Não | Nenhum |  |
| `failOnMissingEmbed` | `boolean` | Sim | `false` | Um valor de `true` causa falha na criação quando um artefato incorporado não é encontrado nas dependências do projeto. Um valor de `false` faz com que a build ignore esses erros. |
| `filterSource` | `java.io.File` | Não | Nenhum | Esse parâmetro define um arquivo que especifica a origem do filtro do espaço de trabalho. Os filtros especificados na configuração e inseridos por meio de incorporados ou subpacotes são mesclados com o conteúdo do arquivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | Não | Nenhum | Esse parâmetro contém elementos de filtro que definem o conteúdo do pacote. Quando executados, os filtros são incluídos na variável `filter.xml` arquivo. Consulte a [Utilização de filtros](#using-filters) abaixo. |
| `finalName` | `java.lang.String` | Sim | A variável `finalName` definido no projeto Maven (fase de compilação) | O nome do arquivo ZIP do pacote gerado, sem a variável `.zip` extensão de arquivo |
| `group` | `java.lang.String` | Sim | A variável `groupID` definido no projeto Maven | A variável `groupId` do pacote de conteúdo gerado que faz parte do caminho de instalação de destino do pacote de conteúdo |
| `outputDirectory` | `java.io.File` | Sim | O diretório de build definido no projeto Maven | O diretório local onde o pacote de conteúdo é salvo |
| `prefix` | `java.lang.String` | Não | Nenhum |  |
| `project` | `org.apache.maven.project.MavenProject` | Sim | Nenhum | O projeto Maven |
| `properties` | `java.util.Map` | Não | Nenhum | Esses parâmetros definem propriedades adicionais que podem ser definidas na variável `properties.xml` arquivo. Essas propriedades não podem substituir as seguintes propriedades predefinidas: `group` (use `group` parâmetro a definir), `name` (use `name` parâmetro a definir), `version` (use `version` parâmetro a definir), `description` (definido a partir da descrição do projeto), `groupId` (`groupId` do descritor de projeto Maven), `artifactId` (`artifactId` do descritor de projeto Maven), `dependencies` (use `dependencies` parâmetro a definir), `createdBy` (o valor da variável `user.name` propriedade do sistema), `created` (a hora atual do sistema), `requiresRoot` (use `requiresRoot` parâmetro a definir), `packagePath` (gerado automaticamente a partir do grupo e do nome do pacote) |
| `requiresRoot` | `boolean` | Sim | falso | Define se o pacote requer raiz. Torna-se o `requiresRoot` propriedade do `properties.xml` arquivo. |
| `subPackages` | `java.util.List` | Não | Nenhum |  |
| `version` | `java.lang.String` | Sim | A versão definida no projeto Maven | A versão do pacote de conteúdo |
| `workDirectory` | `java.io.File` | Sim | O diretório definido no projeto Maven (fase de compilação) | O diretório que contém o conteúdo a ser incluído no pacote |

#### Utilização de filtros {#using-filters}

Use o elemento filters para definir o conteúdo do pacote. Os filtros são adicionados à variável `workspaceFilter` elemento na `META-INF/vault/filter.xml` do pacote.

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

A variável `mode` element define como o conteúdo é o repositório é afetado quando o pacote é importado. Os seguintes valores podem ser usados:

* **Mesclar:** O conteúdo do pacote que ainda não está no repositório é adicionado. O conteúdo que está no pacote e no repositório permanece inalterado. Nenhum conteúdo é removido do repositório.
* **Substituir:** O conteúdo do pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo é removido do repositório quando não existe no pacote.
* **Atualizar:** O conteúdo do pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote.

Quando o filtro não contém `mode` elemento, o valor padrão de `replace` é usada.

### Ajuda com o  {#help}

#### Parâmetros {#parameters-6}

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `detail` | `boolean` | Não | `false` | Determina se devem ser exibidas todas as propriedades definíveis para cada meta |
| `goal` | `String` | Não | Nenhum | Esses parâmetros definem o nome da meta para a qual mostrar ajuda. Se nenhum valor for especificado, a ajuda para todas as metas será exibida. |
| `indentSize` | `int` | Não | `2` | O número de espaços a serem usados para o recuo de cada nível (deve ser positivo se definido) |
| `lineLength` | `int` | Não | `80` | O comprimento máximo de uma linha de exibição (deve ser positivo se definido) |

## Inclusão de uma imagem em miniatura ou arquivo de propriedades no pacote {#including-a-thumbnail-image-or-properties-file-in-the-package}

Substitua os arquivos de configuração de pacote padrão para personalizar as propriedades do pacote. Por exemplo, inclua uma imagem em miniatura para distinguir o pacote em [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md).

Os arquivos de origem podem estar localizados em qualquer lugar do sistema de arquivos. No arquivo POM, defina os recursos de build para copiar os arquivos de origem para o `target/vault-work/META-INF` para inclusão no pacote.

O código POM a seguir adiciona os arquivos na variável `META-INF` pasta da origem do projeto para o pacote:

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

O código POM a seguir adiciona apenas uma imagem em miniatura ao pacote. A imagem em miniatura deve ser nomeada `thumbnail.png`e devem estar localizados no `META-INF/vault/definition` pasta do pacote. Neste exemplo, o arquivo de origem está localizado no `/src/main/content/META-INF/vault/definition` pasta do projeto:

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

## Uso do Arquétipo de Projeto AEM para Gerar Projetos AEM {#using-archetypes}

O Arquétipo de projeto AEM mais recente implementa a estrutura do pacote de práticas recomendadas para implementações locais e AMS e é recomendado para todos os projetos AEM.

>[!TIP]
>
>Consulte a [Estrutura de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) artigo na documentação do AEM as a Cloud Service e na [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) documentação. Ambos são totalmente compatíveis com AEM 6.5.
