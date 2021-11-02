---
title: Plug-in Adobe Content Package Maven
description: Use o plug-in Content Package Maven para implantar aplicativos AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 5%

---

# Plug-in Adobe Content Package Maven {#adobe-content-package-maven-plugin}

Use o plug-in Adobe Content Package Maven para integrar tarefas de implantação e gerenciamento de pacotes aos seus projetos Maven.

A implantação dos pacotes construídos no AEM é realizada pelo plug-in Adobe Content Package Maven e permite a automação de tarefas normalmente executadas usando AEM [Gerenciador de pacotes:](/help/implementing/developing/tools/package-manager.md)

* Crie novos pacotes a partir de arquivos no sistema de arquivos.
* Instale e desinstale pacotes no AEM.
* Crie pacotes que já estão definidos no AEM.
* Obtenha uma lista de pacotes instalados no AEM.
* Remova um pacote do AEM.

Este documento detalha como usar o Maven para gerenciar essas tarefas. No entanto, também é importante compreender [a forma como AEM projetos e respectivos pacotes são estruturados.](#aem-project-structure)

>[!NOTE]
>
>A criação do pacote agora é de propriedade do [Plug-in Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/). A implantação dos pacotes construídos no AEM é executada pelo plugin Adobe Content Package Maven, conforme descrito aqui.

## Pacotes e a estrutura AEM do projeto {#aem-project-structure}

AEM as a Cloud Service segue as práticas recomendadas mais recentes para o gerenciamento de pacotes e a estrutura do projeto, conforme implementado pelo Arquétipo de projeto AEM mais recente.

>[!TIP]
>
>Para obter mais detalhes, consulte o [Estrutura do projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) artigo na documentação as a Cloud Service do AEM, bem como o [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentação. Ambos são totalmente compatíveis com o AEM 6.5.

## Obter o plug-in Content Package Maven {#obtaining-the-content-package-maven-plugin}

O plug-in está disponível no [Repositório Central Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Metas e parâmetros do plug-in do Maven para pacote de conteúdo

Para usar o plug-in Content Package Maven , adicione o seguinte elemento de plug-in dentro do elemento build do seu arquivo POM:

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

Para permitir que o Maven baixe o plug-in, use o perfil fornecido no [Obter o plug-in Content Package Maven](#obtaining-the-content-package-maven-plugin) nesta página.

## Metas do plug-in do Content Package Maven {#goals-of-the-content-package-maven-plugin}

As metas e os parâmetros de meta fornecidos pelo plug-in Pacote de conteúdo são descritos nas seções a seguir. Os parâmetros descritos na seção Parâmetros comuns podem ser usados para a maioria das metas. Os parâmetros que se aplicam a uma meta são descritos na seção para essa meta.

### Prefixo do plug-in {#plugin-prefix}

O prefixo do plug-in é `content-package`. Use esse prefixo para executar uma meta da linha de comando, como no exemplo a seguir:

```shell
mvn content-package:build
```

### Prefixo do parâmetro {#parameter-prefix}

Salvo indicação em contrário, as metas e os parâmetros do plug-in usam a variável `vault` como no exemplo a seguir:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Metas que usam proxies para AEM usam a primeira configuração de proxy válida encontrada nas configurações de Maven. Se nenhuma configuração de proxy for encontrada, nenhum proxy será usado. Consulte a `useProxy` no [Parâmetros comuns](#common-parameters) seção.

### Parâmetros comuns {#common-parameters}

Os parâmetros na tabela a seguir são comuns a todas as metas, exceto quando anotados na variável **Metas** coluna.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição | Metas |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Não | `false` | Um valor de `true` causa falha na criação quando ocorre um erro. Um valor de `false` faz com que a build ignore o erro. | Todas as metas exceto `package` |
| `name` | `String` | `build`: Sim, `install`: Não, `rm`: Sim | `build`: Sem padrão, `install`: O valor da variável `artifactId` propriedade do projeto Maven | O nome do pacote no qual agir | Todas as metas exceto `ls` |
| `password` | `String` | Sim | `admin` | A senha usada para autenticação com AEM | Todas as metas exceto `package` |
| `serverId` | `String` | Não | A ID do servidor da qual recuperar o nome de usuário e a senha para autenticação | Todas as metas exceto `package` |
| `targetURL` | `String` | Sim | `http://localhost:4502/crx/packmgr/service.jsp` | O URL da API do serviço HTTP do gerenciador de pacotes de AEM | Todas as metas exceto `package` |
| `timeout` | `int` | Não | `5` | O tempo limite da conexão para comunicação com o serviço gerenciador de pacotes, em segundos | Todas as metas exceto `package` |
| `useProxy` | `boolean` | Não | `true` | Um valor de `true` O faz com que o Maven use a primeira configuração de proxy ativa encontrada para que as solicitações de proxy sejam feitas no Gerenciador de Pacotes. | Todas as metas exceto `package` |
| `userId` | `String` | Sim | `admin` | O nome de usuário com o qual autenticar AEM | Todas as metas exceto `package` |
| `verbose` | `boolean` | Não | `false` | Ativa ou desativa o registro detalhado | Todas as metas exceto `package` |

### build {#build}

Cria um pacote de conteúdo que já está definido em uma instância de AEM.

>[!NOTE]
>
>Essa meta não precisa ser executada em um projeto Maven.

#### Parâmetros {#parameters}

Todos os parâmetros para a meta de build são descritos na seção [Parâmetros comuns](#common-parameters) seção.

### instalar {#install}

Instala um pacote no repositório. A execução dessa meta não requer um projeto Maven. A meta é vinculada à variável `install` fase do ciclo de vida de compilação Maven.

#### Parâmetros {#parameters-1}

Além dos parâmetros a seguir, consulte as descrições no [Parâmetros comuns](#common-parameters) seção.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|---|
| `artifact` | `String` | Não | O valor da variável `artifactId` propriedade do projeto Maven | Uma string do formulário `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Não | Nenhum | A ID do artefato a ser instalado |
| `groupId` | `String` | Não | Nenhum | O `groupId` do artefato a ser instalado |
| `install` | `boolean` | Não | `true` | Determina se o pacote deve ser descompactado automaticamente quando carregado |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Não | O valor da variável `localRepository` variável do sistema | O repositório Maven local que não pode ser configurado usando a configuração do plug-in, pois a propriedade do sistema é sempre usada |
| `packageFile` | `java.io.File` | Não | O artefato principal definido para o projeto Maven | O nome do arquivo de pacote a ser instalado |
| `packaging` | `String` | Não | `zip` | O tipo de empacotamento do artefato a ser instalado |
| `pomRemoteRepositories` | `java.util.List` | Sim | O valor da variável `remoteArtifactRepositories` propriedade definida para o projeto Maven | Esse valor não pode ser configurado usando a configuração do plug-in e deve ser especificado no projeto. |
| `project` | `org.apache.maven.project.MavenProject` | Sim | O projeto para o qual o plug-in está configurado | O projeto Maven que está implícito porque o projeto contém a configuração do plug-in |
| `repositoryId` (POM), `repoID` (linha de comando) | `String` | Não | `temp` | A ID do repositório do qual o artefato é recuperado |
| `repositoryUrl` (POM), `repoURL` (linha de comando) | `String` | Não | Nenhum | O URL do repositório do qual o artefato é recuperado |
| version | Sequência de caracteres | Não | Nenhum | A versão do artefato a ser instalada |

### ls {#ls}

Lista os pacotes implantados em [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)

#### Parâmetros {#parameters-2}

Todos os parâmetros da meta de ls são descritos na seção [Parâmetros comuns](#common-parameters) seção.

### rm {#rm}

Remove um pacote de [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)

#### Parâmetros {#parameters-3}

Todos os parâmetros da meta de rm são descritos na seção [Parâmetros comuns](#common-parameters) seção.

### desinstalar {#uninstall}

Desinstala um pacote. O pacote permanece no servidor no estado desinstalado.

#### Parâmetros {#parameters-4}

Todos os parâmetros da meta de desinstalação estão descritos na seção [Parâmetros comuns](#common-parameters) seção.

### pacote {#package}

Cria um pacote de conteúdo. A configuração padrão do objetivo do pacote inclui o conteúdo do diretório em que os arquivos compilados são salvos. A execução da meta do pacote requer que a fase de compilação tenha sido concluída. A meta do pacote é vinculada à fase do pacote do ciclo de vida da compilação Maven.

#### Parâmetros {#parameters-5}

Além dos parâmetros a seguir, consulte a descrição do `name` no [Parâmetros comuns](#common-parameters) seção.

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | Não | Nenhum | A configuração de arquivamento a ser usada |
| `builtContentDirectory` | `java.io.File` | Sim | O valor do diretório de saída da compilação Maven | O diretório que contém o conteúdo a ser incluído no pacote |
| `dependencies` | `java.util.List` | Não | Nenhum |  |
| `embeddedTarget` | `java.lang.String` | Não | Nenhum |  |
| `embeddeds` | `java.util.List` | Não | Nenhum |  |
| `failOnMissingEmbed` | `boolean` | Sim | `false` | Um valor de `true` causa a falha da criação quando um artefato incorporado não é encontrado nas dependências do projeto. Um valor de `false` faz com que a build ignore esses erros. |
| `filterSource` | `java.io.File` | Não | Nenhum | Esse parâmetro define um arquivo que especifica a origem do filtro do espaço de trabalho. Os filtros especificados na configuração e inseridos por meio de bordas ou subpacotes são unidos ao conteúdo do arquivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | Não | Nenhum | Esse parâmetro contém elementos de filtro que definem o conteúdo do pacote. Quando executados, os filtros são incluídos na variável `filter.xml` arquivo. Consulte a [Uso de filtros](#using-filters) abaixo. |
| `finalName` | `java.lang.String` | Sim | O `finalName` definido no projeto Maven (fase de criação) | O nome do arquivo ZIP do pacote gerado, sem o `.zip` extensão de arquivo |
| `group` | `java.lang.String` | Sim | O `groupID` definido no projeto Maven | O `groupId` do pacote de conteúdo gerado que faz parte do caminho de instalação de destino do pacote de conteúdo |
| `outputDirectory` | `java.io.File` | Sim | O diretório de build definido no projeto Maven | O diretório local onde o pacote de conteúdo é salvo |
| `prefix` | `java.lang.String` | Não | Nenhum |  |
| `project` | `org.apache.maven.project.MavenProject` | Sim | Nenhum | O projeto Maven |
| `properties` | `java.util.Map` | Não | Nenhum | Esses parâmetros definem propriedades adicionais que podem ser definidas na variável `properties.xml` arquivo. Essas propriedades não podem substituir as seguintes propriedades predefinidas: `group` (use `group` parâmetro para definir), `name` (use `name` parâmetro para definir), `version` (use `version` parâmetro para definir), `description` (definido na descrição do projeto), `groupId` (`groupId` do descritor do projeto Maven), `artifactId` (`artifactId` do descritor do projeto Maven), `dependencies` (use `dependencies` parâmetro para definir), `createdBy` (o valor da variável `user.name` propriedade do sistema), `created` (hora atual do sistema), `requiresRoot` (use `requiresRoot` parâmetro para definir), `packagePath` (gerado automaticamente pelo grupo e pelo nome do pacote) |
| `requiresRoot` | `boolean` | Sim | falso | Define se o pacote requer raiz. Isso se tornará o `requiresRoot` da `properties.xml` arquivo. |
| `subPackages` | `java.util.List` | Não | Nenhum |  |
| `version` | `java.lang.String` | Sim | A versão definida no projeto Maven | A versão do pacote de conteúdo |
| `workDirectory` | `java.io.File` | Sim | O diretório definido no projeto Maven (fase de compilação) | O diretório que contém o conteúdo a ser incluído no pacote |

#### Uso de filtros {#using-filters}

Use o elemento filters para definir o conteúdo do pacote. Os filtros são adicionados ao `workspaceFilter` no `META-INF/vault/filter.xml` do pacote.

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

O `mode` O elemento define como o conteúdo é afetado pelo repositório quando o pacote é importado. Os seguintes valores podem ser usados:

* **Mesclar:** O conteúdo no pacote que ainda não está no repositório é adicionado. O conteúdo que está no pacote e no repositório não é alterado. Nenhum conteúdo é removido do repositório.
* **Substituir:** O conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo é removido do repositório quando não existe no pacote.
* **Atualização:** O conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo existente é removido do repositório.

Quando o filtro contiver `mode` elemento, o valor padrão de `replace` é usada.

### ajuda {#help}

#### Parâmetros {#parameters-6}

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| `detail` | `boolean` | Não | `false` | Determina se todas as propriedades configuráveis devem ser exibidas para cada meta |
| `goal` | `String` | Não | Nenhum | Esses parâmetros definem o nome da meta para a qual será exibida a ajuda. Se nenhum valor for especificado, a ajuda para todas as metas será exibida. |
| `indentSize` | `int` | Não | `2` | O número de espaços a serem usados para o recuo de cada nível (deve ser positivo, se definido) |
| `lineLength` | `int` | Não | `80` | O comprimento máximo de uma linha de exibição (deve ser positivo, se definido) |

## Inclusão de uma imagem em miniatura ou de um arquivo de propriedades no pacote {#including-a-thumbnail-image-or-properties-file-in-the-package}

Substitua os arquivos de configuração padrão do pacote para personalizar as propriedades do pacote. Por exemplo, inclua uma imagem em miniatura para distinguir o pacote em [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)

Os arquivos de origem podem estar localizados em qualquer lugar no seu sistema de arquivos. No arquivo POM, defina os recursos de criação para copiar os arquivos de origem para o `target/vault-work/META-INF` para inclusão na embalagem.

O seguinte código POM adiciona os arquivos no `META-INF` pasta da origem do projeto para o pacote:

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

O código POM a seguir adiciona apenas uma imagem em miniatura ao pacote. A imagem em miniatura deve ser nomeada `thumbnail.png`e devem estar localizados na variável `META-INF/vault/definition` pasta do pacote. Neste exemplo, o arquivo de origem está localizado na variável `/src/main/content/META-INF/vault/definition` pasta do projeto:

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

## Usar o Arquétipo de projeto AEM para gerar projetos AEM {#using-archetypes}

O AEM Project Archetype mais recente implementa a estrutura de pacotes de práticas recomendadas para implementações locais e do AMS e é recomendado para todos os projetos AEM.

>[!TIP]
>
>Para obter mais detalhes, consulte o [Estrutura do projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) artigo na documentação as a Cloud Service do AEM, bem como o [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentação. Ambos são totalmente compatíveis com o AEM 6.5.
