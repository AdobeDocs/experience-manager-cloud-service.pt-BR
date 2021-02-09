---
title: Teste da interface de usuário - Cloud Services
description: Teste da interface de usuário - Cloud Services
translation-type: tm+mt
source-git-commit: ea0c9675ca03b1d247c7e5fd13e03072fb4a13ae
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# Teste da interface de usuário {#ui-testing}

Os testes da interface do usuário são testes baseados em Selenium empacotados em uma imagem da Docker para permitir uma ampla escolha em linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia desenvolvida a partir da Selenium). A imagem do Docker pode ser criada com ferramentas padrão, mas deve respeitar certas convenções durante sua execução. Ao executar a imagem do Docker, um servidor Selenium é automaticamente provisionado. As convenções de tempo de execução descritas abaixo permitem que seu código de teste acesse o servidor Selenium e as instâncias de AEM em teste.

>[!NOTE]
> Os pipeline de estágio e de produção criados antes de 10 de fevereiro de 2021 precisam ser atualizados para que os testes de interface sejam usados, conforme descrito nesta página.
> Consulte [Configurando o pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para obter informações sobre a configuração do pipeline.

## Criando testes de interface de usuário {#building-ui-tests}

Os testes de interface são criados a partir de um contexto de criação do Docker gerado por um projeto Maven. O Gerenciador de nuvem usa o contexto de compilação do Docker para gerar uma imagem do Docker que contém os testes de UI reais. Em resumo, um projeto Maven gera um contexto de criação do Docker, e o contexto de criação do Docker descreve como criar uma imagem do Docker contendo os testes da interface do usuário.

Esta seção passa pelas etapas necessárias para adicionar um projeto de Testes de interface ao seu repositório. Se você estiver com pressa ou não tiver requisitos especiais para a linguagem de programação, o [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) poderá gerar um projeto de Testes de IU para você.

### Gerar um contexto de compilação do Docker {#generate-docker-build-context}

Para gerar um contexto de compilação do Docker, você precisa de um módulo Maven que:

- Produz um arquivo que contém `Dockerfile` e todos os outros arquivos necessários para criar a imagem do Docker com seus testes.
- Marca o arquivo com o classificador `ui-test-docker-context`.

A maneira mais simples de conseguir isso é configurar o [Plug-in Maven Assembly](http://maven.apache.org/plugins/maven-assembly-plugin/) para criar o arquivo de contexto de compilação do Docker e atribuir o classificador correto a ele.

Você pode criar testes de interface de usuário com diferentes tecnologias e estruturas, mas esta seção presume que seu projeto seja apresentado de uma forma semelhante à seguinte.

```
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

O arquivo `pom.xml` cuida da compilação Maven. Adicione uma execução ao Plug-in Maven Assembly semelhante ao seguinte.

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

Essa execução instrui o Plug-in Maven Assembly a criar um arquivo com base nas instruções contidas em `assembly-ui-test-docker-context.xml`, chamado de &quot;descritor de assembly&quot; no jargão do plug-in. O descritor de assembly lista todos os arquivos que devem fazer parte do arquivo.

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

O descritor de assembly instrui o plug-in a criar um arquivo do tipo `.tar.gz` e atribui o classificador `ui-test-docker-context` a ele. Além disso, ele lista os arquivos que devem ser incluídos no arquivo:

- Um `Dockerfile`, obrigatório para criar a imagem do Docker.
- O script `wait-for-grid.sh`, cujas finalidades são descritas abaixo.
- Os testes de interface reais, implementados por um projeto Node.js na pasta `test-module`.

O descritor de assembly também exclui alguns arquivos que podem ser gerados durante a execução local dos testes da interface do usuário. Isso garante um arquivo menor e construções mais rápidas.

O arquivo que contém o contexto de compilação do Docker é automaticamente selecionado pelo Gerenciador de nuvem, que criará a imagem do Docker que contém seus testes durante seus pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes da interface de usuário em seu aplicativo.

## Gravando testes de interface de usuário {#writing-ui-tests}

Esta seção descreve as convenções que a imagem do Docker que contém seus testes de interface de usuário devem seguir. A imagem do Docker é construída a partir do contexto de compilação do Docker descrito na seção anterior.

### Variáveis de ambiente {#environment-variables}

As variáveis de ambiente a seguir serão passadas para a imagem do Docker em tempo de execução.

| Variável | Exemplos | Descrição |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | O URL do servidor Selenium |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | A implementação do navegador usada pelo servidor Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | O URL da instância do autor AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | O nome de usuário para fazer login na instância do autor AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | A senha para fazer login na instância do autor AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | O URL da instância de publicação AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | O nome de usuário para fazer login na instância de publicação AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | A senha para fazer login na instância de publicação AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | O caminho no qual o relatório XML dos resultados do teste deve ser salvo |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | O URL para o qual o arquivo deve ser carregado para torná-lo acessível ao Selenium |

### Aguardando que Selenium esteja pronto {#waiting-for-selenium}

Antes do start dos testes, é responsabilidade da imagem da Docker garantir que o servidor Selenium esteja funcionando. Esperar pelo serviço Selenium é um processo de duas etapas:

1. Leia o URL do serviço Selenium da variável de ambiente `SELENIUM_BASE_URL`.
2. Pesquisa em intervalos regulares para o [ponto de extremidade de status](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API Selenium.

Quando o terminal de status do Selenium responde com uma resposta positiva, os testes podem finalmente start.

### Gerar os relatórios de teste {#generate-test-reports}

A imagem do Docker deve gerar relatórios de teste no formato XML JUnit e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato JUnit XML é um formato difundido para o relatórios dos resultados dos testes. Se a imagem do Docker usar Java e Maven, o [Plug-in Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) e o [Plug-in Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Se a imagem do Docker for implementada com outras linguagens de programação ou corredores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

### Carregar arquivos (#upload-files)

Os testes às vezes devem carregar arquivos no aplicativo em teste. Para manter flexível a implantação da Selenium em relação aos seus testes, não é possível carregar diretamente um ativo diretamente para a Selenium. Em vez disso, o upload de um arquivo passa por algumas etapas intermediárias:

1. Carregue o arquivo no URL especificado pela variável de ambiente `UPLOAD_URL`. O upload deve ser executado em uma solicitação de POST com um formulário multiparte. O formulário multipart deve ter um único campo de arquivo. Isso equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar tal solicitação HTTP.
2. Se o upload for bem-sucedido, a solicitação retornará uma resposta `200 OK` do tipo `text/plain`. O conteúdo da resposta é um identificador de arquivo opaco. Você pode usar esse identificador no lugar de um caminho de arquivo em um elemento `<input>` para testar os uploads de arquivos no aplicativo.
