---
title: Teste da interface do usuário - Cloud Services
description: Teste da interface do usuário - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 710f156e606902ab5548169661d4a82c8cf4f819
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 1%

---

# Teste da interface do usuário {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Teste da interface do usuário"
>abstract="Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). A imagem Docker pode ser criada com ferramentas padrão, mas deve respeitar certas convenções durante a execução. Ao executar a imagem Docker, um servidor Selenium é automaticamente provisionado. As convenções de tempo de execução descritas abaixo permitem que o código de teste acesse o servidor Selenium e as instâncias de AEM em teste."

Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). A imagem Docker pode ser criada com ferramentas padrão, mas deve respeitar certas convenções durante a execução. Ao executar a imagem Docker, um servidor Selenium é automaticamente provisionado. As convenções de tempo de execução descritas abaixo permitem que o código de teste acesse o servidor Selenium e as instâncias de AEM em teste.

>[!NOTE]
> Os pipelines de preparo e produção criados antes de 10 de fevereiro de 2021 precisam ser atualizados para usar os testes da interface do usuário, conforme descrito nesta página.
> Consulte [Pipelines de CI-CD no Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter informações sobre a configuração do pipeline.

## Teste de interface personalizada {#custom-ui-testing}

O AEM fornece aos clientes um conjunto integrado de portas de qualidade do Cloud Manager para garantir atualizações tranquilas em seus aplicativos. Em particular, os portões de teste de TI já permitem que os clientes criem e automatizem seus próprios testes que usam AEM APIs.

O recurso de teste da interface do usuário personalizada é um [recurso opcional](#customer-opt-in) que permite que nossos clientes criem e executem automaticamente testes da interface do usuário para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium). Saiba mais sobre como criar interface do usuário e gravar testes da interface do usuário a partir daqui. Além disso, um projeto de Testes de interface pode ser facilmente gerado usando o Arquétipo de projeto AEM.

Os clientes podem criar testes personalizados (via GIT) e conjunto de testes para interface do usuário. O teste da interface do usuário será executado como parte de uma porta de qualidade específica para cada pipeline do Cloud Manager com suas informações específicas de etapa e feedback. Quaisquer testes da interface do usuário, incluindo regressão e novas funcionalidades, permitirão que os erros sejam detectados e relatados no contexto do cliente.

Os testes da interface do usuário do cliente são executados automaticamente no pipeline de Produção na etapa &quot;Teste da interface personalizada&quot;.

Diferentemente do Teste Funcional Personalizado, que são testes HTTP escritos em java, os testes da interface do usuário podem ser uma imagem mais docker com testes escritos em qualquer idioma, desde que sigam as convenções definidas em [Criação de testes da interface do usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>É recomendável seguir a estrutura e o idioma *(js e wdio)* convenientemente fornecido no [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) como ponto de partida.

### Opt-in do cliente {#customer-opt-in}

Para que os testes da interface do usuário sejam criados e executados, os clientes precisam &quot;aceitar&quot; adicionando um arquivo ao repositório de código, no submódulo maven para testes da interface do usuário (ao lado do arquivo pom.xml do submódulo de testes da interface do usuário) e garantir que esse arquivo esteja na raiz da build `tar.gz` arquivo.

*Nome do arquivo*: `testing.properties`

*Conteúdo*: `ui-tests.version=1`

Se isso não estiver na build `tar.gz` , a interface do usuário testa a criação e as execuções serão ignoradas

Para adicionar `testing.properties` no artefato criado, adicione um `include` instrução em `assembly-ui-test-docker-context.xml` (no submódulo de testes da interface do usuário).

>[!NOTE]
>Se o projeto não incluir a linha, será necessário editar esse arquivo para aceitar o teste da interface do usuário. Se o arquivo tiver uma linha aconselhando a não editar, ignore esse conselho.

    &quot;
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- módulo de teste de aceitação no Cloud Manager —>
    &lt;/includes>
    [...]
    &quot;

>[!NOTE]
>Os pipelines de produção criados antes de 10 de fevereiro de 2021 precisarão ser atualizados para usar os testes da interface do usuário, conforme descrito nesta seção. Basicamente, isso significa que o Usuário deve editar o pipeline de Produção e clicar em **Salvar** da interface do usuário, mesmo que nenhuma alteração tenha sido feita.
>Consulte [Configuração do pipeline de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) para saber mais sobre a configuração de pipeline.

## Criação de testes da interface do usuário {#building-ui-tests}

Os testes da interface do usuário são criados a partir de um contexto de compilação Docker gerado por um projeto Maven. O Cloud Manager usa o contexto de compilação do Docker para gerar uma imagem do Docker que contém os testes reais da interface do usuário. Em resumo, um projeto Maven gera um contexto de compilação Docker, e o contexto de compilação Docker descreve como criar uma imagem Docker contendo os testes da interface do usuário.

Esta seção passa pelas etapas necessárias para adicionar um projeto de Testes de interface ao seu repositório. Se você tiver pressa ou não tiver requisitos especiais para a linguagem de programação, a variável [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) O pode gerar um projeto de Testes da interface do usuário para você.

### Gerar um contexto de compilação do Docker {#generate-docker-build-context}

Para gerar um contexto de compilação do Docker, você precisa de um módulo Maven que:

- Produz um arquivo que contém um `Dockerfile` e qualquer outro arquivo necessário para criar a imagem Docker com seus testes.
- Marca o arquivo com a variável `ui-test-docker-context` classificador.

A maneira mais simples de fazer isso é configurar a variável [Plug-in de Montagem Maven](http://maven.apache.org/plugins/maven-assembly-plugin/) para criar o arquivo de contexto de compilação do Docker e atribuir o classificador correto a ele.

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

Esta execução instrui o Plug-in de Montagem Maven a criar um arquivo com base nas instruções contidas no `assembly-ui-test-docker-context.xml`, chamado de &quot;descritor de conjunto&quot; no jargão do plug-in. O descritor de assembly lista todos os arquivos que devem fazer parte do arquivo.

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

O descritor de assembly instrui o plug-in a criar um arquivo do tipo `.tar.gz` e atribui o `ui-test-docker-context` classificador nele. Além disso, ele lista os arquivos que devem ser incluídos no arquivo:

- A `Dockerfile`, obrigatório para criar a imagem Docker.
- O `wait-for-grid.sh` , cujas finalidades são descritas abaixo.
- Os testes reais da interface do usuário, implementados por um projeto Node.js no `test-module` pasta.

O descritor de conjunto também exclui alguns arquivos que podem ser gerados durante a execução local dos testes da interface do usuário. Isso garante um arquivo menor e builds mais rápidas.

O arquivo que contém o contexto de compilação do Docker é automaticamente selecionado pelo Cloud Manager, que criará a imagem do Docker que contém seus testes durante seus pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes da interface de usuário em seu aplicativo.

A build deve produzir zero ou um arquivo. Se produzir zero arquivo, a etapa de teste será aprovada por padrão. Se a build produzir mais de um arquivo, qual arquivo está selecionado é não determinístico.

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

### Aguardando que o Selênio esteja pronto {#waiting-for-selenium}

Antes de os testes começarem, é responsabilidade da imagem do Docker garantir que o servidor Selenium esteja funcionando. Aguardar o serviço Selenium é um processo de duas etapas:

1. Leia o URL do serviço Selenium no `SELENIUM_BASE_URL` variável de ambiente.
2. Pesquisa em intervalos regulares para a [ponto final de status](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API do Selenium.

Quando o endpoint de status do Selenium responde com uma resposta positiva, os testes podem finalmente começar.

### Gerar os relatórios de teste {#generate-test-reports}

A imagem Docker deve gerar relatórios de teste no formato JUnit XML e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato JUnit XML é um formato amplo para relatar os resultados dos testes. Se a imagem do Docker usar Java e Maven, a variável [Plug-in do Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) e [Plug-in Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Se a imagem do Docker for implementada com outras linguagens de programação ou corredores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

### Upload de arquivos {#upload-files}

Os testes às vezes devem carregar arquivos no aplicativo em teste. Para manter a implantação do Selenium em relação aos testes flexível, não é possível fazer upload direto de um ativo para o Selenium. Em vez disso, o upload de um arquivo passa por algumas etapas intermediárias:

1. Faça upload do arquivo no URL especificado pela variável `UPLOAD_URL` variável de ambiente. O upload deve ser executado em uma solicitação de POST com um formulário multipart. O formulário multipart deve ter um único campo de arquivo. É equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar tal solicitação HTTP.
2. Se o upload for bem-sucedido, a solicitação retornará um `200 OK` resposta do tipo `text/plain`. O conteúdo da resposta é um identificador de arquivo opaco. Você pode usar esse identificador no lugar de um caminho de arquivo em um `<input>` elemento para testar os uploads do arquivo em seu aplicativo.
