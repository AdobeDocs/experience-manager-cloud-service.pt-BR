---
title: Teste de interface do usuário
description: Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos personalizados.
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: ht
source-wordcount: '1338'
ht-degree: 100%

---


# Teste de interface do usuário {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Teste de interface do usuário"
>abstract="Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos. Os testes de interface do usuário são testes baseados em Selenium, compactados em uma imagem do Docker, para permitir uma variedade de opções de linguagens e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium)."

Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos.

## Visão geral {#custom-ui-testing}

O AEM fornece um conjunto integrado de [quality gates (portais de qualidade) do Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantir atualizações tranquilas para aplicativos personalizados. Em especial, os portais de teste de TI já promovem a criação e a automação de testes personalizados usando as APIs do AEM.

Os testes de interface do usuário são testes baseados em Selenium, compactados em uma imagem do Docker, para permitir uma variedade de opções de linguagens e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). Além disso, um projeto de testes de interface do usuário pode ser facilmente gerado usando o [Arquétipo de Projetos AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR)

Os testes de interface do usuário são executados como parte de um quality gate (portal de qualidade) específico para cada pipeline do Cloud Manager com uma etapa [dedicada de **Teste de interface do usuário personalizado**.](/help/implementing/cloud-manager/deploy-code.md) Quaisquer testes de interface do usuário, incluindo regressão e novas funcionalidades, permitem que erros sejam detectados e relatados.

Diferentemente dos testes funcionais personalizados, que são testes HTTP escritos em Java, os testes de interface do usuário podem ser uma imagem do Docker com testes escritos em qualquer idioma, desde que sigam as convenções definidas na seção [Compilação de testes de interface do usuário.](#building-ui-tests)

>[!TIP]
>
>A Adobe recomenda seguir a estrutura e a linguagem (JavaScript e WDIO) fornecidas no [Arquétipo de Projetos AEM.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### Adesão do cliente {#customer-opt-in}

Para que o Cloud Manager compile e execute seus testes de interface do usuário, é necessário aderir a esse recurso adicionando um arquivo ao repositório.

* O nome do arquivo deve ser `testing.properties`.
* O conteúdo do arquivo deve ser `ui-tests.version=1`.
* O arquivo deve estar sob o submódulo maven para testes de interface do usuário ao lado do arquivo `pom.xml` do submódulo de testes de interface do usuário.
* O arquivo deve estar na raiz do arquivo de compilação `tar.gz`.

A compilação dos testes de interface do usuário será ignorada se esse arquivo não estiver presente.

Para incluir um arquivo `testing.properties` no artefato de compilação, adicione a instrução `include` no arquivo `assembly-ui-test-docker-context.xml`.

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
>Se o seu projeto não incluir essa linha, será necessário editar o arquivo para aderir ao teste de interface do usuário.
>
>O arquivo pode conter uma linha aconselhando a não editá-la. Isso se deve ao fato de ele ter sido introduzido em seu projeto antes da adesão ao teste de interface do usuário e que os clientes não devem editar o arquivo. Pode ser ignorado com segurança.

## Compilação de testes de interface do usuário {#building-ui-tests}

Um projeto Maven gera um contexto de compilação do Docker. Este contexto de compilação do Docker descreve como criar uma imagem do Docker contendo testes de interface do usuário, que o Cloud Manager usa para gerar uma imagem do Docker contendo os testes de interface do usuário reais.

Esta seção descreve as etapas necessárias para adicionar um projeto de testes de interface do usuário ao seu repositório.

>[!TIP]
>
>O [Arquétipo de Projetos AEM](https://github.com/adobe/aem-project-archetype) pode gerar um projeto de testes de interface do usuário para que você não tenha requisitos especiais quanto à linguagem de programação.

### Gerar um contexto de compilação do Docker {#generate-docker-build-context}

Para gerar um contexto de compilação do Docker, você precisará de um módulo Maven que:

* Produza um arquivo que contenha um `Dockerfile` e qualquer outro arquivo necessário para criar a imagem do Docker em seus testes.
* Marque o arquivo com o classificador `ui-test-docker-context`.

A maneira mais simples de fazer isso é configurar o [Plug-in de compilação do Maven](https://maven.apache.org/plugins/maven-assembly-plugin/) para criar o arquivo de contexto de compilação do Docker e atribuir o classificador correto a ele.

Você pode compilar testes de interface do usuário com diferentes tecnologias e estruturas, mas esta seção presume que o projeto seja apresentado de uma maneira semelhante à descrita a seguir.

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

O arquivo `pom.xml` controla a compilação Maven. Adicione uma execução ao Plug-in de compilação do Maven semelhante ao mostrado a seguir.

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

Esta execução instrui o Plug-in de compilação Maven a criar um arquivo com base nas instruções contidas em `assembly-ui-test-docker-context.xml`, chamado de **descritor de compilação** no jargão do plug-in. O descritor de compilação lista todos os arquivos que devem fazer parte do arquivamento.

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

O descritor de compilação instrui o plug-in a criar um arquivamento do tipo `.tar.gz` e atribuir o classificador `ui-test-docker-context` a ele. Além disso, ele lista os arquivos que devem ser incluídos no arquivamento, incluindo os descritos a seguir.

* Um `Dockerfile`, obrigatório para criar a imagem do Docker
* O script `wait-for-grid.sh`, cujos objetivos são descritos abaixo
* Os testes reais de interface do usuário, implementados por um projeto Node.js na pasta `test-module`

O descritor de compilação também exclui alguns arquivos que podem ser gerados durante a execução local dos testes de interface do usuário. Isso garante que um arquivo menor seja gerado, e consequentemente, resulta em compilações mais rápidas.

O arquivamento que contém o contexto de compilação do Docker é selecionado automaticamente pelo Cloud Manager, que criará a imagem do Docker contendo seus testes durante os pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes de interface do usuário em seu aplicativo.

A compilação deve produzir zero ou um arquivamento. Se produzir zero arquivamento, a etapa de teste será aprovada por padrão. Se a compilação produzir mais de um arquivamento, o arquivamento selecionado será não determinístico.

## Gravação de testes da interface do usuário {#writing-ui-tests}

Esta seção descreve as convenções que a imagem do Docker que contém seus testes de interface do usuário deve seguir. A imagem do Docker é criada a partir do contexto de compilação do Docker descrito na seção anterior.

### Variáveis de ambiente {#environment-variables}

As variáveis de ambiente a seguir serão passadas para a imagem do Docker no tempo de execução.

| Variável | Exemplos | Descrição |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | A URL do servidor Selenium |
| `SELENIUM_BROWSER` | `chrome` | A implementação do navegador usada pelo servidor Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | A URL da instância do autor do AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | O nome de usuário para fazer logon na instância de autoria do AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | A senha para fazer logon na instância de autoria do AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | A URL da instância de publicação do AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | O nome de usuário para fazer logon na instância de publicação do AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | A senha para fazer logon na instância de publicação do AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | O caminho onde o relatório XML dos resultados do teste deve ser salvo |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | A URL onde o arquivo deve ser carregado para torná-lo acessível ao Selenium |

### Aguardar o Selenium estar pronto {#waiting-for-selenium}

Antes de os testes começarem, é responsabilidade da imagem do Docker garantir que o servidor Selenium esteja funcionando. Aguardar o serviço Selenium é um processo de duas etapas.

1. Leia a URL do serviço Selenium na variável de ambiente `SELENIUM_BASE_URL`.
1. Consulte em intervalos regulares o [endpoint de status](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API do Selenium.

Quando o endpoint de status do Selenium responder com uma resposta positiva, os testes poderão ser iniciados.

### Gerar relatórios de teste {#generate-test-reports}

A imagem do Docker deve gerar relatórios de teste no formato XML JUnit e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato XML JUnit é um formato amplamente usado para relatar resultados de testes. Se a imagem do Docker usar Java e Maven, os módulos de teste padrão, como o [Plug-in Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) e o [Plug-in Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) poderão gerar os relatórios imediatamente.

Se a imagem do Docker for implementada com outras linguagens de programação ou executores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

### Fazer upload de arquivos {#upload-files}

Os testes às vezes devem carregar arquivos no aplicativo que está sendo testado. Para manter a implantação do Selenium flexível em relação aos testes, não é possível fazer upload de um ativo diretamente no Selenium. Em vez disso, o upload de um arquivo exige as etapas descritas a seguir.

1. Faça upload do arquivo na URL especificado pela variável de ambiente `UPLOAD_URL`.
   * O upload deve ser realizado em uma solicitação POST com um formulário multipart.
   * O formulário multipart deve ter um único campo de arquivo.
   * É equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar essa solicitação HTTP.
1. Se o upload for bem-sucedido, a solicitação retornará uma resposta `200 OK` do tipo `text/plain`.
   * O conteúdo da resposta é um identificador de arquivo opaco.
   * Você pode usar esse identificador no lugar de um caminho de arquivo em um elemento `<input>` para testar os uploads de arquivo em seu aplicativo.
