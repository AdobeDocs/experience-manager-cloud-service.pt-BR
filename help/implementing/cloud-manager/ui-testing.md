---
title: Teste de interface do usuário
description: Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos personalizados.
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8703240a5b7b8ed751620f602470da45025f7b74
workflow-type: tm+mt
source-wordcount: '2698'
ht-degree: 74%

---


# Teste de interface do usuário {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Teste de interface do usuário"
>abstract="Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos. Os testes de interface são baseados no Selenium, compactados em uma imagem do Docker, para permitir uma variedade de opções de idiomas e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada a partir do Selenium)."

Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos.

## Visão geral {#custom-ui-testing}

O AEM fornece um conjunto integrado de [quality gates (portais de qualidade) do Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantir atualizações tranquilas para aplicativos personalizados. Em especial, os portais de teste de TI já promovem a criação e a automação de testes personalizados usando as APIs do AEM.

Os testes de interface são compactados em uma imagem do Docker para permitir uma variedade de opções de idiomas e estruturas (como Cypress, Selenium, Java e Maven, além do JavaScript). Além disso, um projeto de testes de interface do usuário pode ser facilmente gerado usando o [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/overview).

A Adobe incentiva o uso do Cypress, pois oferece recarregamento em tempo real e espera automática, o que ajuda a economizar tempo e melhorar a produtividade durante os testes. O Cypress também fornece uma sintaxe simples e intuitiva, facilitando a aprendizagem e o uso, até mesmo para aqueles que são novos em testes.

Os testes de interface são executados como parte de uma porta de qualidade específica para cada pipeline do Cloud Manager que contém uma etapa de [**Teste de interface personalizada** ](/help/implementing/cloud-manager/deploy-code.md)nos [pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) ou, opcionalmente, nos [pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Quaisquer testes de interface, incluindo regressão e novas funcionalidades, permitem que erros sejam detectados e relatados.

Diferentemente dos testes funcionais personalizados, que são testes HTTP escritos em Java, os testes de interface podem ser uma imagem do Docker com testes escritos em qualquer linguagem, desde que sigam as convenções definidas na seção [Compilação de testes de interface](#building-ui-tests).

>[!TIP]
>
>A Adobe recomenda o uso do Cypress para testes de interface, seguindo o código fornecido no [repositório de Exemplos de teste do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>A Adobe também fornece exemplos de módulos de teste de interface com base em JavaScript com WebdriverIO (consulte [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) e Java com WebDriver (consulte o [repositório de Amostras de testes do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)).

## Introdução aos testes de interface  {#get-started-ui-tests}

Esta seção descreve as etapas necessárias para a configuração dos testes de interface para execução no Cloud Manager.

1. Decida sobre a estrutura de teste que deseja usar.

   * Para o Cypress (padrão), use o código de amostra do [repositório de Amostras de Teste do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress) ou use o código de amostra gerado automaticamente na pasta `ui.tests` do seu repositório do Cloud Manager.

   * Para o Playwright, use o código de amostra do [repositório de Amostras de Teste do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).

   * Para Webdriver.IO, use o código de amostra do [repositório de Amostras de Teste de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

   * Para o Selenium WebDriver, use o código de amostra do [repositório de Amostras de Teste de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * Para outras linguagens de programação, consulte a seção [Criação de testes de interface](#building-ui-tests) deste documento para configurar o projeto de teste.

1. Certifique-se de que o teste da interface esteja ativado de acordo com a seção [Adesão do cliente](#customer-opt-in) deste documento.

1. Desenvolva seus casos de teste e [execute-os localmente](#run-ui-tests-locally).

1. Confirmar seu código no repositório do Cloud Manager e executar um pipeline do Cloud Manager.

## Compilação de testes de interface do usuário {#building-ui-tests}

Um projeto Maven gera um contexto de compilação do Docker. Este contexto de construção do Docker descreve como criar uma imagem do Docker que contenha os testes de interface, que o Cloud Manager usa para gerar uma imagem do Docker contendo os testes de interface reais.

Esta seção descreve as etapas necessárias para adicionar um projeto de testes de interface ao seu repositório.

>[!TIP]
>
>O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) pode gerar um projeto de testes de interface para você, que está em conformidade com a descrição a seguir, caso você não tenha requisitos especiais para a linguagem de programação.

### Gerar um contexto de compilação do Docker {#generate-docker-build-context}

Para gerar um contexto de construção do Docker, você precisará de um módulo Maven que:

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

O descritor de compilação instrui o plug-in a criar um arquivamento do tipo `.tar.gz` e atribuir o classificador `ui-test-docker-context` a ele. Além disso, ele lista os arquivos que devem ser incluídos no arquivamento, incluindo o seguinte:

* Um `Dockerfile`, obrigatório para criar a imagem do Docker
* O script `wait-for-grid.sh`, cujos objetivos são descritos abaixo
* Os testes reais de interface do usuário, implementados por um projeto Node.js na pasta `test-module`

O descritor de compilação também exclui alguns arquivos que podem ser gerados durante a execução local dos testes de interface do usuário. Isso garante que um arquivo menor seja gerado, e consequentemente, resulta em compilações mais rápidas.

O arquivamento que contém o contexto de compilação do Docker é selecionado automaticamente pelo Cloud Manager, que criará a imagem do Docker contendo seus testes durante os pipelines de implantação. Eventualmente, o Cloud Manager executará a imagem do Docker para executar os testes de interface do usuário em seu aplicativo.

A compilação deve produzir zero ou um arquivamento. Se produzir zero arquivamento, a etapa de teste será aprovada por padrão. Se a compilação produzir mais de um arquivamento, o arquivamento selecionado será não determinístico.

### Adesão do cliente {#customer-opt-in}

Para que o Cloud Manager compile e execute seus testes de interface, é necessário aderir a esse recurso adicionando um arquivo ao repositório.

* O nome do arquivo deve ser `testing.properties`.
* O conteúdo do arquivo deve ser `ui-tests.version=1`.
* O arquivo deve estar no submódulo Maven para testes de interface, próximo do arquivo `pom.xml` do submódulo de testes de interface.
* O arquivo deve estar na raiz do arquivo de compilação `tar.gz`.

A compilação e a execução dos testes de interface será ignorada se esse arquivo não estiver presente.

Para incluir um arquivo `testing.properties` no artefato de compilação, adicione a instrução `include` no arquivo `assembly-ui-test-docker-context.xml`.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>Se o projeto não incluir essa linha, edite o arquivo para aderir ao teste de interface do usuário.
>
>O arquivo pode conter uma linha aconselhando a não editá-la. Isso se deve ao fato de ele ter sido introduzido em seu projeto antes da adesão ao teste de interface e não havia a intenção de que os clientes editassem o arquivo. Pode ser ignorado com segurança.

Se estiver usando os exemplos fornecidos pela Adobe:

* Para a pasta `ui.tests` baseada em JavaScript, gerada com base no [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests), você pode executar o comando abaixo para adicionar a configuração necessária.

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* As amostras de teste Cypress e Java Selenium fornecidas pelo Adobe já têm o sinalizador de aceitação definido.

## Gravação de testes da interface do usuário {#writing-ui-tests}

Esta seção descreve as convenções que a imagem do Docker que contém seus testes de interface do usuário deve seguir. A imagem do Docker é criada a partir do contexto de compilação do Docker descrito na seção anterior.

### Variáveis de ambiente {#environment-variables}

As seguintes variáveis de ambiente são passadas para a imagem do Docker em tempo de execução, dependendo da estrutura.

>[!NOTE]
>
> Esses valores serão definidos automaticamente durante a execução do pipeline - não há necessidade de defini-los manualmente como variáveis de pipeline.

| Variável | Exemplos | Descrição | Estrutura de testes |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | A URL do servidor Selenium | Somente Selenium |
| `SELENIUM_BROWSER` | `chrome` | A implementação do navegador usada pelo servidor Selenium | Somente Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | O URL da instância do autor do AEM | Todos |
| `AEM_AUTHOR_USERNAME` | `admin` | O nome de usuário para fazer logon na instância de autor do AEM | Todos |
| `AEM_AUTHOR_PASSWORD` | `admin` | A senha para fazer logon na instância de autor do AEM | Todos |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | O URL da instância de publicação do AEM | Todos * |
| `AEM_PUBLISH_USERNAME` | `admin` | O nome de usuário para fazer logon na instância de publicação do AEM | Todos * |
| `AEM_PUBLISH_PASSWORD` | `admin` | A senha para fazer logon na instância de publicação do AEM | Todos * |
| `REPORTS_PATH` | `/usr/src/app/reports` | O caminho onde o relatório XML dos resultados do teste deve ser salvo | Todos |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | O URL no qual o arquivo deve ser enviado para torná-lo acessível à estrutura de teste | Todos |
| `PROXY_HOST` | `proxy-host` | O nome do host do Proxy HTTP interno a ser usado pela estrutura de teste | Todos, exceto Selenium |
| `PROXY_HTTPS_PORT` | `8071` | A porta de escuta do servidor proxy para conexões HTTPS (pode estar vazia) | Todos, exceto Selenium |
| `PROXY_HTTP_PORT` | `8070` | A porta de escuta do servidor proxy para conexões HTTP (pode estar vazia) | Todos, exceto Selenium |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | O caminho para o certificado CA a ser usado pela estrutura de testes | Todos, exceto Selenium |
| `PROXY_OBSERVABILITY_PORT` | `8081` | A porta de verificação de integridade HTTP do servidor proxy | Todos, exceto Selenium |
| `PROXY_RETRY_ATTEMPTS` | `12` | Número sugerido de tentativas ao aguardar a prontidão do servidor proxy | Todos, exceto Selenium |
| `PROXY_RETRY_DELAY` | `5` | Atraso sugerido entre tentativas de repetição ao aguardar a prontidão do servidor proxy | Todos, exceto Selenium |

`* these values will be empty if there is no publish instance`

Os exemplos de teste da Adobe fornecem funções auxiliares para acessar os parâmetros de configuração:

* Cypress: use a função padrão `Cypress.env('VARIABLE_NAME')`
* JavaScript: Consulte o módulo [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js)
* Java: consulte a classe [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java)

### Gerar relatórios de teste {#generate-test-reports}

A imagem do Docker deve gerar relatórios de teste no formato XML JUnit e salvá-los no caminho especificado pela variável de ambiente `REPORTS_PATH`. O formato XML JUnit é um formato amplamente usado para relatar resultados de testes. Se a imagem do Docker usar Java e Maven, os módulos de teste padrão, como o [Plug-in Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) e o [Plug-in Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) poderão gerar os relatórios imediatamente.

Se a imagem do Docker for implementada com outras linguagens de programação ou executores de teste, verifique a documentação das ferramentas escolhidas para saber como gerar relatórios XML JUnit.

>[!NOTE]
>
>O resultado da etapa de teste da interface é avaliado somente com base nos relatórios de teste. Certifique-se de que o relatório seja gerado adequadamente para a execução do teste.
>
>Use asserções em vez de apenas registrar um erro no STDERR ou retornar um código de saída diferente de zero, caso contrário, o pipeline de implantação poderá continuar normalmente.
>
>Se um proxy HTTP foi usado durante a execução de testes, os resultados incluirão um arquivo `request.log`.

### Pré-requisitos {#prerequisites}

* Os testes no Cloud Manager são executados usando um usuário administrador técnico.

>[!NOTE]
>
>Para executar os testes funcionais no computador local, crie um usuário com permissões de administrador para alcançar o mesmo comportamento.

* A infraestrutura em container com escopo para testes funcionais apresenta os seguintes limites:

| Tipo | Valor | Descrição |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | Quantidade de tempo de CPU reservado por execução de teste. |
| Memória | 1Gi | Quantidade de memória alocada para o teste, valor em gibibytes. |
| Tempo limite | 30 min | A duração após a qual o teste é concluído. |
| Duração recomendada | 15 min | A Adobe recomenda gravar os testes para não demorar mais do que esse tempo. |

>[!NOTE]
>
> Caso precise de mais recursos, crie um chamado no Atendimento ao cliente e descreva o caso de uso. A Adobe verificará sua solicitação e fornecerá a assistência adequada.

## Detalhes específicos do Selenium

>[!NOTE]
>
>Esta seção só se aplica quando o Selenium é a infraestrutura de teste escolhida.

### Aguardar o Selenium estar pronto {#waiting-for-selenium}

Antes de os testes começarem, é responsabilidade da imagem do Docker garantir que o servidor Selenium esteja funcionando. Aguardar o serviço Selenium é um processo de duas etapas.

1. Leia a URL do serviço Selenium na variável de ambiente `SELENIUM_BASE_URL`.
1. Consulte em intervalos regulares o [endpoint de status](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exposto pela API do Selenium.

Quando o endpoint de status do Selenium responder com uma resposta positiva, os testes poderão ser iniciados.

Os exemplos de teste de interface da Adobe lidam com isso por meio do script `wait-for-grid.sh`, que é executado na inicialização do Docker e inicia a execução do teste real somente depois que a grade está pronta.

### Capturar imagens de tela e vídeos {#capture-screenshots}

A imagem do Docker pode gerar saídas de teste adicionais (por exemplo, capturas de tela ou vídeos) e salvá-las no caminho especificado pela variável de ambiente `REPORTS_PATH`. Qualquer arquivo encontrado abaixo de `REPORTS_PATH` é incluído no arquivo de resultados de teste.

Os exemplos de teste fornecidos pela Adobe criam, por padrão, capturas de tela de qualquer teste com falha.

Você pode usar as funções auxiliares para criar capturas de tela nos testes.

* JavaScript: [comando takeScreenshot](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [comandos](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

Se um arquivo de resultados de teste for criado durante a execução de um teste de interface, você poderá baixá-lo do Cloud Manager usando o botão `Download Details` na etapa [**Testes de interface personalizados**.](/help/implementing/cloud-manager/deploy-code.md)

### Fazer upload de arquivos {#upload-files}

Os testes às vezes devem carregar arquivos no aplicativo que está sendo testado. Para manter a implantação do Selenium flexível em relação aos testes, não é possível fazer upload de um ativo diretamente no Selenium. Em vez disso, o upload de um arquivo exige as etapas descritas a seguir.

1. Faça upload do arquivo na URL especificado pela variável de ambiente `UPLOAD_URL`.
   * O upload deve ser realizado em uma solicitação POST com um formulário multipart.
   * O formulário multipart deve ter um único campo de arquivo.
   * É equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte a documentação e as bibliotecas da linguagem de programação usada na imagem do Docker para saber como executar essa solicitação HTTP.
   * Os exemplos de teste da Adobe fornecem funções auxiliares para fazer o upload de arquivos:
      * JavaScript: consulte o comando [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js).
      * Java: consulte a classe [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java).
1. Se o upload for bem-sucedido, a solicitação retornará uma resposta `200 OK` do tipo `text/plain`.
   * O conteúdo da resposta é um identificador de arquivo opaco.
   * Você pode usar esse identificador no lugar de um caminho de arquivo em um elemento `<input>` para testar os uploads de arquivo em seu aplicativo.

## Detalhes específicos do Cypress

>[!NOTE]
>
>Esta seção só se aplica quando o Cypress é a infraestrutura de ensaio escolhida.

### Configurar proxy HTTP

O ponto de entrada do contêiner Docker precisa verificar o valor da variável de ambiente `PROXY_HOST`.

Se esse valor estiver vazio, nenhuma etapa adicional será necessária e os testes deverão ser executados sem o uso do proxy HTTP.

Se não estiver vazio, o script de ponto de entrada precisa:

1. Configure uma conexão proxy HTTP para executar testes de interface. Isso pode ser feito exportando a variável de ambiente `HTTP_PROXY` que é criada usando os seguintes valores:
   * Host do proxy, que é fornecido pela variável `PROXY_HOST`
   * Porta de proxy, que é fornecida pela variável `PROXY_HTTPS_PORT` ou `PROXY_HTTP_PORT` (a variável com um valor não vazio será usada)
2. Defina o certificado CA que será usado na conexão com o proxy HTTP. Sua localização é fornecida pela variável `PROXY_CA_PATH`.
   * Isso pode ser feito exportando a variável de ambiente `NODE_EXTRA_CA_CERTS`.
3. Aguarde até que o proxy HTTP esteja pronto.
   * Para verificar a preparação, as variáveis de ambiente `PROXY_HOST`, `PROXY_OBSERVABILITY_PORT`, `PROXY_RETRY_ATTEMPTS` e `PROXY_RETRY_DELAY` podem ser usadas.
   * Você pode verificar usando uma solicitação cURL, certificando-se de instalar o cURL em seu `Dockerfile`.

Um exemplo de implementação pode ser encontrado no ponto de entrada do módulo de teste de amostra Cypress em [GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh).

## Detalhes específicos do dramaturgo

>[!NOTE]
>
> Esta seção só se aplica quando o dramaturgo é a infraestrutura de teste escolhida.

### Configurar proxy HTTP

>[!NOTE]
>
> Nos exemplos apresentados, supomos que o Chrome está sendo usado como um navegador de projeto.

Semelhante ao Cypress, os testes precisam usar o proxy HTTP se uma variável de ambiente `PROXY_HOST` não vazia for fornecida.

Para fazer isso, as seguintes modificações precisam ser feitas.

#### Dockerfile

Instalar cURL e `libnss3-tools`, que fornece `certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### Script de ponto de entrada

Inclua um script bash que, caso a variável de ambiente `PROXY_HOST` seja fornecida, faça o seguinte:

1. Exportar variáveis relacionadas ao proxy, como `HTTP_PROXY` e `NODE_EXTRA_CA_CERTS`
2. Use `certutil` para instalar o certificado de autoridade de certificação de proxy para chromium
3. Aguarde até que o proxy HTTP esteja pronto (ou saia em caso de falha).

Exemplo de implementação:

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### Configuração do dramaturgo

Modifique a configuração do playwright (por exemplo, em `playwright.config.js`) para usar um proxy caso a variável de ambiente `HTTP_PROXY` esteja definida.

Exemplo de implementação:

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

>[!NOTE]
>
> Um exemplo de implementação pode ser encontrado no Módulo de Teste de Amostra do Playwright no [GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-playwright/).


## Execução de testes locais de interface {#run-ui-tests-locally}

Antes de ativar os testes de interface em um pipeline do Cloud Manager, é recomendável executá-los localmente no [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) ou em uma instância real do AEM as a Cloud Service.

### Exemplo de teste do Cypress {#cypress-sample}

1. Abra um shell e navegue até a pasta `ui.tests/test-module` no repositório

1. Instale o Cypress e outros pré-requisitos

   ```shell
   npm install
   ```

1. Defina as variáveis de ambiente necessárias para a execução do teste

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. Execute testes com um dos comandos a seguir

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>Os arquivos de log são armazenados na pasta `target/` do repositório.
>
>Para obter detalhes, consulte [Repositório de amostras de teste do AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md).

### Exemplo de teste do JavaScript WebdriverIO {#javascript-sample}

1. Abra um shell e navegue até a pasta `ui.tests` no repositório

1. Execute o comando abaixo para iniciar os testes usando o Maven

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* Isso inicia uma instância independente do Selenium e executa os testes nela.
>* Os arquivos de log são armazenados na pasta `target/reports` do repositório.
>* Certifique-se de que sua máquina esteja executando a versão mais recente do Chrome, pois o teste baixa a versão mais recente do ChromeDriver automaticamente.
>
>Para obter detalhes, consulte [Repositório de amostras de teste do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

### Amostra de teste do dramaturgo {#playwright-sample}

1. Abra um shell e navegue até a pasta `ui.tests` no repositório

1. Execute o comando abaixo para criar uma imagem do docker usando Maven

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. Execute o comando abaixo para iniciar os testes usando o Maven

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>Os arquivos de log são armazenados na pasta `target/` do repositório.
>
>Para obter detalhes, consulte [Repositório de amostras de teste do AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).


### Exemplo de teste do Java Selenium WebDriver {#java-sample}

1. Abra um shell e navegue até a pasta `ui.tests/test-module` no repositório

1. Execute os comandos abaixo para iniciar os testes usando o Maven

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>Os arquivos de log são armazenados na pasta `target/reports` do repositório.
>
>Para obter detalhes, consulte [Repositório de amostras de teste do AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
