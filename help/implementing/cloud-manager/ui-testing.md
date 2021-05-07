---
title: Teste da interface do usuário - Cloud Services
description: Teste da interface do usuário - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Teste da interface do usuário {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Teste da interface do usuário"
>abstract="Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). A imagem Docker pode ser criada com ferramentas padrão, mas deve respeitar certas convenções durante a execução. Ao executar a imagem Docker, um servidor Selenium é automaticamente provisionado. As convenções de tempo de execução descritas abaixo permitem que o código de teste acesse o servidor Selenium e as instâncias de AEM em teste."

Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). A imagem Docker pode ser criada com ferramentas padrão, mas deve respeitar certas convenções durante a execução. Ao executar a imagem Docker, um servidor Selenium é automaticamente provisionado. As convenções de tempo de execução descritas abaixo permitem que o código de teste acesse o servidor Selenium e as instâncias de AEM em teste.

>[!NOTE]
> Os pipelines de preparo e produção criados antes de 10 de fevereiro de 2021 precisam ser atualizados para usar os testes da interface do usuário, conforme descrito nesta página.
> Consulte [Configuração do pipeline de CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para obter informações sobre a configuração do pipeline.

## Criação de testes da interface do usuário {#building-ui-tests}

Os testes da interface do usuário são criados a partir de um contexto de compilação Docker gerado por um projeto Maven. O Cloud Manager usa o contexto de compilação do Docker para gerar uma imagem do Docker que contém os testes reais da interface do usuário. Em resumo, um projeto Maven gera um contexto de compilação Docker, e o contexto de compilação Docker descreve como criar uma imagem Docker contendo os testes da interface do usuário.

Esta seção passa pelas etapas necessárias para adicionar um projeto de Testes de interface ao seu repositório. Se você tiver pressa ou não tiver requisitos especiais para a linguagem de programação, o [AEM Arquétipo de Projeto](https://github.com/adobe/aem-project-archetype) poderá gerar um projeto de Testes de IU para você.

### Gerar um contexto de compilação do Docker {#generate-docker-build-context}

Para gerar um contexto de compilação do Docker, você precisa de um módulo Maven que:

- Produz um arquivo que contém um `Dockerfile` e qualquer outro arquivo necessário para criar a imagem do Docker com seus testes.
- Marca o arquivo com o classificador `ui-test-docker-context`.

A maneira mais simples de fazer isso é configurar o [Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/) para criar o arquivo de contexto da compilação do Docker e atribuir o classificador correto a ele.

Você pode criar testes de interface do usuário com diferentes tecnologias e estruturas, mas esta seção presume que o projeto foi apresentado de uma maneira semelhante ao seguinte.

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

O arquivo `pom.xml` cuida da build Maven. Adicione uma execução ao Plug-in Maven Assembly semelhante ao seguinte.

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

Essa execução instrui o Plug-in de Montagem Maven a criar um arquivo com base nas instruções contidas em `assembly-ui-test-docker-context.xml`, chamado de &quot;descritor de montagem&quot; no jargão do plug-in. O descritor de assembly lista todos os arquivos que devem fazer parte do arquivo.

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

- Um `Dockerfile`, obrigatório para criar a imagem Docker.
- O script `wait-for-grid.sh`, cujas finalidades são descritas abaixo.
- Os testes da interface do usuário real, implementados por um projeto Node.js na pasta `test-module`.

O descritor de conjunto também exclui alguns arquivos que podem ser gerados durante a execução local dos testes da interface do usuário. Isso garante um arquivo menor e builds mais rápidas.

O arquivo que contém o contexto de compilação do Docker é automaticamente selecionado pelo Cloud Manager, que criará a imagem do Docker que contém seus testes durante seus pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes da interface de usuário em seu aplicativo.

## Gravando testes de interface do usuário {#writing-ui-tests}

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

### Aguardando que o Selenium esteja pronto {#waiting-for-selenium}

Antes de os testes começarem, é responsabilidade da imagem do Docker garantir que o servidor Selenium esteja funcionando. Aguardar o serviço Selenium é um processo de duas etapas:

1. Leia o URL do serviço Selenium da variável de ambiente `SELENIUM_BASE_URL`.
2. Pesquisa em intervalo regular para o [status endpoint](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API Selenium.

Quando o endpoint de status do Selenium responde com uma resposta positiva, os testes podem finalmente começar.

### Gerar os relatórios de teste {#generate-test-reports}

A imagem Docker deve gerar relatórios de teste no formato JUnit XML e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato JUnit XML é um formato amplo para relatar os resultados dos testes. Se a imagem do Docker usar Java e Maven, o [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) e o [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/). Se a imagem do Docker for implementada com outras linguagens de programação ou corredores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

### Upload de arquivos (#upload-files)

Os testes às vezes devem carregar arquivos no aplicativo em teste. Para manter a implantação do Selenium em relação aos testes flexível, não é possível fazer upload direto de um ativo para o Selenium. Em vez disso, o upload de um arquivo passa por algumas etapas intermediárias:

1. Carregue o arquivo no URL especificado pela variável de ambiente `UPLOAD_URL`. O upload deve ser executado em uma solicitação de POST com um formulário multipart. O formulário multipart deve ter um único campo de arquivo. Isso é equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar tal solicitação HTTP.
2. Se o upload for bem-sucedido, a solicitação retornará uma resposta `200 OK` do tipo `text/plain`. O conteúdo da resposta é um identificador de arquivo opaco. Você pode usar esse identificador no lugar de um caminho de arquivo em um elemento `<input>` para testar os uploads de arquivo em seu aplicativo.
