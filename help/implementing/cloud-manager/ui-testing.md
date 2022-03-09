---
title: Teste da interface
description: O teste da interface personalizada é um recurso opcional que permite criar e executar automaticamente testes da interface do usuário para seus aplicativos personalizados
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: a7555507f4fb0fb231e27d7c7a6413b4ec6b94e6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 1%

---


# Teste da interface {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Teste da interface"
>abstract="O teste da interface personalizada é um recurso opcional que permite criar e executar automaticamente testes da interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium)."

O teste da interface personalizada é um recurso opcional que permite criar e executar automaticamente testes da interface do usuário para seus aplicativos.

>[!NOTE]
> Os pipelines de preparo e produção criados antes de 10 de fevereiro de 2021 precisam ser atualizados para usar os testes da interface do usuário, conforme descrito nesta página.
> Consulte [Pipelines de CI-CD no Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter informações sobre a configuração do pipeline.

## Visão geral {#custom-ui-testing}

AEM fornece um conjunto integrado de [Portas de qualidade do Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantir atualizações tranquilas para aplicativos personalizados. Em particular, o teste de TI já promove a criação e automação de testes personalizados usando APIs AEM.

Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). Além disso, um projeto de testes da interface do usuário pode ser facilmente gerado usando [o Arquétipo de projeto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Os testes da interface do usuário são executados como parte de uma porta de qualidade específica para cada pipeline do Cloud Manager com um [dedicado **Teste de interface personalizada** etapa.](/help/implementing/cloud-manager/deploy-code.md) Quaisquer testes de interface do usuário, incluindo regressão e novas funcionalidades, permitem que erros sejam detectados e relatados.

Diferentemente dos testes funcionais personalizados, que são testes HTTP escritos em Java, os testes da interface do usuário podem ser uma imagem do Docker com testes escritos em qualquer idioma, desde que sigam as convenções definidas na seção [Criação de testes da interface do usuário.](#building-ui-tests)

>[!TIP]
>
>O Adobe recomenda seguir a estrutura e a linguagem (JavaScript e WDIO) fornecidas na [AEM Arquétipo de projeto.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### Opt-in do cliente {#customer-opt-in}

Para que o Cloud Manager crie e execute seus testes de interface do usuário, é necessário aderir a esse recurso adicionando um arquivo ao repositório.

* O nome do arquivo deve ser `testing.properties`.
* O conteúdo do arquivo deve ser `ui-tests.version=1`.
* O arquivo deve estar sob o submódulo maven para testes de interface do usuário ao lado do `pom.xml` arquivo do submódulo de testes da interface do usuário.
* O arquivo deve estar na raiz da build `tar.gz` arquivo.

A build dos testes da interface do usuário será ignorada se esse arquivo não estiver presente.

Para incluir uma `testing.properties` no artefato de criação, adicione um `include` na instrução `assembly-ui-test-docker-context.xml` arquivo.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>Se o seu projeto não incluir essa linha, será necessário editar esse arquivo para aceitar o teste da interface do usuário. Se o arquivo tiver uma linha avisando para não editá-lo, ignore esse conselho.

>[!NOTE]
>
>Os pipelines de produção criados antes de 10 de fevereiro de 2021 precisarão ser atualizados para usar os testes da interface do usuário, conforme descrito nesta seção. Basicamente, isso significa que o Usuário deve editar o pipeline de Produção e clicar em **Salvar** da interface do usuário, mesmo que nenhuma alteração tenha sido feita.
>Consulte [Configuração do pipeline de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) para saber mais sobre a configuração de pipeline.

## Criação de testes da interface do usuário {#building-ui-tests}

Um projeto Maven gera um contexto de compilação Docker. Este contexto de compilação do Docker descreve como criar uma imagem Docker contendo os testes da interface do usuário, que os usuários do Cloud Manager geram uma imagem Docker contendo os testes da interface do usuário real.

Esta seção descreve as etapas necessárias para adicionar um projeto de testes de interface ao seu repositório.

>[!TIP]
>
>O [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) O pode gerar um projeto de Testes de interface do usuário para que você não tenha requisitos especiais para a linguagem de programação.

### Gerar um Contexto de Criação do Docker {#generate-docker-build-context}

Para gerar um contexto de compilação do Docker, você precisa de um módulo Maven que:

* Produz um arquivo que contém um `Dockerfile` e qualquer outro arquivo necessário para criar a imagem Docker com seus testes.
* Marca o arquivo com a variável `ui-test-docker-context` classificador.

A maneira mais simples de fazer isso é configurar a variável [Plug-in de Montagem Maven](http://maven.apache.org/plugins/maven-assembly-plugin/) para criar o arquivo de contexto de compilação do Docker e atribuir o classificador correto a ele.

Você pode criar testes de interface do usuário com diferentes tecnologias e estruturas, mas esta seção presume que o projeto foi apresentado de uma maneira semelhante ao seguinte.

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

O `pom.xml` O arquivo cuida da build Maven. Adicione uma execução ao Plug-in Maven Assembly semelhante ao seguinte.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Esta execução instrui o Plug-in de Montagem Maven a criar um arquivo com base nas instruções contidas no `assembly-ui-test-docker-context.xml`, chamada de **descritor de assembly** no jargão do plug-in. O descritor de assembly lista todos os arquivos que devem fazer parte do arquivo.

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

O descritor de assembly instrui o plug-in a criar um arquivo do tipo `.tar.gz` e atribui o `ui-test-docker-context` classificador nele. Além disso, ele lista os arquivos que devem ser incluídos no arquivo, incluindo o seguinte.

* A `Dockerfile`, obrigatório para criar a imagem Docker
* O `wait-for-grid.sh` , cujos objetivos são descritos abaixo
* Os testes reais da interface do usuário, implementados por um projeto Node.js no `test-module` pasta

O descritor de conjunto também exclui alguns arquivos que podem ser gerados durante a execução local dos testes da interface do usuário. Isso garante um arquivo menor e builds mais rápidas.

O arquivo que contém o contexto de compilação do Docker é automaticamente selecionado pelo Cloud Manager, que criará a imagem do Docker que contém seus testes durante seus pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes da interface de usuário em seu aplicativo.

A build deve produzir zero ou um arquivo. Se produzir zero arquivos, a etapa de teste passará por padrão. Se a build produzir mais de um arquivo, qual arquivo está selecionado é não determinístico.

## Gravação de testes da interface do usuário {#writing-ui-tests}

Esta seção descreve as convenções que a imagem do Docker que contém seus testes de interface de usuário devem seguir. A imagem do Docker é criada a partir do contexto de compilação do Docker descrito na seção anterior.

### Variáveis de ambiente {#environment-variables}

As variáveis de ambiente a seguir serão passadas para a imagem Docker em tempo de execução.

| Variável | Exemplos | Descrição |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | O URL do servidor Selenium |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | A implementação do navegador usada pelo servidor Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | O URL da instância do autor do AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | O nome de usuário para fazer logon na instância do autor do AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | A senha para fazer logon na instância do autor do AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | O URL da instância de publicação de AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | O nome de usuário para fazer logon na instância de publicação do AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | A senha para fazer logon na instância de publicação do AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | O caminho onde o relatório XML dos resultados do teste deve ser salvo |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | O URL onde o arquivo deve ser carregado para torná-lo acessível ao Selenium |

### Aguardando o Selenium estar pronto {#waiting-for-selenium}

Antes de os testes começarem, é responsabilidade da imagem do Docker garantir que o servidor Selenium esteja funcionando. Aguardar o serviço Selenium é um processo de duas etapas.

1. Leia o URL do serviço Selenium no `SELENIUM_BASE_URL` variável de ambiente.
1. Pesquisa em intervalos regulares para a [ponto final de status](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API do Selenium.

Quando o endpoint de status do Selenium responde com uma resposta positiva, os testes podem ser iniciados.

### Gerar relatórios de teste {#generate-test-reports}

A imagem Docker deve gerar relatórios de teste no formato JUnit XML e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato JUnit XML é um formato amplamente usado para relatar os resultados de testes. Se a imagem do Docker usar Java e Maven, a variável [Plug-in do Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) e [Plug-in Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/).

Se a imagem do Docker for implementada com outras linguagens de programação ou corredores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

### Fazer upload de arquivos {#upload-files}

Os testes às vezes devem carregar arquivos no aplicativo que está sendo testado. Para manter a implantação do Selenium flexível em relação aos testes, não é possível fazer upload direto de um ativo para o Selenium. Em vez disso, o upload de um arquivo requer as seguintes etapas.

1. Faça upload do arquivo no URL especificado pela variável `UPLOAD_URL` variável de ambiente.
   * O upload deve ser executado em uma solicitação de POST com um formulário multipart.
   * O formulário multipart deve ter um único campo de arquivo.
   * É equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar tal solicitação HTTP.
1. Se o upload for bem-sucedido, a solicitação retornará um `200 OK` resposta do tipo `text/plain`.
   * O conteúdo da resposta é um identificador de arquivo opaco.
   * Você pode usar esse identificador no lugar de um caminho de arquivo em um `<input>` elemento para testar os uploads do arquivo em seu aplicativo.
