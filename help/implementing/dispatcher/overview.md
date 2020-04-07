---
title: Dispatcher na nuvem
description: 'Dispatcher na nuvem '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Dispatcher na nuvem {#Dispatcher-in-the-cloud}

## Configuração e teste do Apache e do Dispatcher {#apache-and-dispatcher-configuration-and-testing}

Esta seção descreve como estruturar o AEM como um Apache de serviço em nuvem e configurações do Dispatcher, bem como como como validá-lo e executá-lo localmente antes de implantá-lo em ambientes em nuvem. Também descreve a depuração em ambientes da Cloud. Para obter informações adicionais sobre o Dispatcher, consulte a documentação [do Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)AEM.

>[!NOTE]
>Os usuários do Windows precisarão usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Este é um pré-requisito para executar e depurar o Dispatcher em um computador local. As seções abaixo incluem comandos usando as versões Mac ou Linux do SDK, mas o SDK do Windows pode ser usado de maneira semelhante.

## Ferramentas do Dispatcher {#dispatcher-sdk}

As Ferramentas do Dispatcher fazem parte do AEM geral como um SDK de serviço em nuvem e fornecem:

* Uma estrutura de arquivos baunilha contendo os arquivos de configuração a serem incluídos em um projeto maven para o dispatcher;
* Ferramentas para que os clientes validem uma configuração do dispatcher localmente;
* Uma imagem do Docker que exibe o dispatcher localmente.

## Download e extração das ferramentas {#extracting-the-sdk}

As Ferramentas do Dispatcher podem ser baixadas de um arquivo zip no portal de distribuição [de](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) software. Observe que o acesso às listagens do SDK é limitado àquelas com os serviços gerenciados do AEM ou o AEM como ambientes de serviço em nuvem. Qualquer nova configuração disponível na nova versão das Ferramentas do dispatcher pode ser usada para implantar em ambientes da Cloud que executam essa versão do AEM na Cloud ou posterior.

**Para macOS e Linux**, baixe o script de shell para uma pasta em seu computador, torne-o executável e execute-o. Ele extrairá automaticamente os arquivos das Ferramentas do Dispatcher abaixo do diretório no qual você os armazenou (onde `version` é a versão das Ferramentas do dispatcher).

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**No Windows**, baixe o arquivo zip e extraia-o.

## Estrutura do arquivo {#file-structure}

A estrutura da subpasta dispatcher do projeto está descrita abaixo e deve ser copiada para a pasta do despachante do projeto maven:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

Abaixo está uma explicação de arquivos importantes que podem ser modificados:

**Arquivos personalizáveis**

Os arquivos a seguir são personalizáveis e serão transferidos para a instância da Cloud na implantação:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Você pode ter um ou mais desses arquivos. Elas contêm `<VirtualHost>` entradas que correspondem aos nomes de host e permitem que o Apache gerencie cada tráfego de domínio com regras diferentes. Os arquivos são criados no `available_vhosts` diretório e ativados com um link simbólico no `enabled_vhosts` diretório. Nos `.vhost` arquivos, outros arquivos, como regravações e variáveis, serão incluídos.

* `conf.d/rewrites/rewrite.rules`

Este arquivo é incluído de dentro de seus `.vhost` arquivos. Ele tem um conjunto de regras de regravação para `mod_rewrite`.

>[!NOTE]
>
>No momento, um único arquivo de regravação deve ser usado em vez de arquivos específicos do site. Esse tamanho de arquivo deve ser inferior a 1 MB.

* `conf.d/variables/custom.vars`

Este arquivo é incluído de dentro de seus `.vhost` arquivos. Você pode colocar definições para variáveis do Apache neste local.

* `conf.d/variables/global.vars`

Este arquivo é incluído de dentro do `dispatcher_vhost.conf` arquivo. Você pode alterar o nível do despachante e regravar o log neste arquivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Você pode ter um ou mais desses arquivos e eles contêm farm para corresponder aos nomes de host e permitir que o módulo do dispatcher manipule cada farm com regras diferentes. Os arquivos são criados no `available_farms` diretório e ativados com um link simbólico no `enabled_farms` diretório. Nos `.farm` arquivos, outros arquivos, como filtros, regras de cache e outros, serão incluídos.

* `conf.dispatcher.d/cache/rules.any`

Este arquivo é incluído de dentro de seus `.farm` arquivos. Especifica preferências de cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este arquivo é incluído de dentro de seus `.farm` arquivos. Especifica quais cabeçalhos de solicitação devem ser encaminhados ao backend.

* `conf.dispatcher.d/filters/filters.any`

Este arquivo é incluído de dentro de seus `.farm` arquivos. Ele tem um conjunto de regras que mudam qual tráfego deve ser filtrado e não chegar ao backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este arquivo é incluído de dentro de seus `.farm` arquivos. Ele tem uma lista de nomes de host ou caminhos de URI que devem ser correspondidos por correspondências de localizações. Isso determina qual backend usar para servir uma solicitação.

Os arquivos acima fazem referência aos arquivos de configuração imutáveis listados abaixo. As alterações nos arquivos imutáveis não serão processadas pelos despachantes nos ambientes da Cloud.

**Arquivos de configuração imutáveis**

Esses arquivos fazem parte da estrutura básica e aplicam padrões e práticas recomendadas. Os arquivos são considerados imutáveis porque modificá-los ou excluí-los localmente não afetarão sua implantação, pois não serão transferidos para a instância da Cloud.

É recomendável que os arquivos acima façam referência aos arquivos imutáveis listados abaixo, seguidos de declarações ou substituições adicionais. Quando a configuração do dispatcher for implantada em um ambiente de nuvem, a versão mais recente dos arquivos imutáveis será usada, independentemente da versão usada no desenvolvimento local.

* `conf.d/available_vhosts/default.vhost`

Contém um host virtual de amostra. Para seu próprio host virtual, crie uma cópia desse arquivo, personalize-o, vá até `conf.d/enabled_vhosts` e crie um link simbólico para sua cópia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte da estrutura base, usada para ilustrar como seus hosts virtuais e variáveis globais são incluídos.

* `conf.d/rewrites/default_rewrite.rules`

Regras padrão de regravação adequadas para um projeto padrão. Se você precisar de personalização, modifique `rewrite.rules`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas se ajustarem às suas necessidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contém um farm de despachantes de amostra. Para o seu próprio farm, crie uma cópia deste arquivo, personalize-o, acesse `conf.d/enabled_farms` e crie um link simbólico para sua cópia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte da estrutura básica é gerada na inicialização. É **necessário** incluir esse arquivo em cada farm definido, na `cache/allowedClients` seção.

* `conf.dispatcher.d/cache/default_rules.any`

Regras de cache padrão adequadas para um projeto padrão. Se você precisar de personalização, modifique `conf.dispatcher.d/cache/rules.any`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas se ajustarem às suas necessidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Cabeçalhos de solicitação padrão para encaminhar ao backend, adequados para um projeto padrão. Se você precisar de personalização, modifique `clientheaders.any`. Na personalização, você ainda pode incluir os cabeçalhos de solicitação padrão primeiro, se eles se ajustarem às suas necessidades.

* `conf.dispatcher.d/dispatcher.any`

Parte da estrutura básica, usada para ilustrar como as fazendas de despachantes estão incluídas.

* `conf.dispatcher.d/filters/default_filters.any`

filtros padrão adequados para um projeto padrão. Se você precisar de personalização, modifique `filters.any`. Na personalização, você ainda pode incluir os filtros padrão primeiro, se eles se ajustarem às suas necessidades.

* `conf.dispatcher.d/renders/default_renders.any`

Parte da estrutura base, esse arquivo é gerado na inicialização. É **necessário** incluir esse arquivo em cada farm definido, na `renders` seção.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globalização de host padrão adequada para um projeto padrão. Se você precisar de personalização, modifique `virtualhosts.any`. Na personalização, você não deve incluir a globalização padrão do host, pois ela corresponde a **cada** solicitação recebida.

>[!NOTE]
>O AEM como um arquétipo maven do serviço em nuvem gerará a mesma estrutura de arquivos de configuração do dispatcher.

As seções abaixo descrevem como validar a configuração localmente para que ela possa passar pela porta de qualidade associada no Cloud Manager ao implantar uma versão interna.

## Validação local da configuração do Dispatcher {#local-validation-of-dispatcher-configuration}

A ferramenta de validação está disponível no SDK `bin/validator` como um binário Mac OS, Linux ou Windows, permitindo que os clientes executem a mesma validação que o Cloud Manager executará ao criar e implantar uma versão.

É invocado como: `validator full [-d folder] [-w whitelist] zip-file | src folder`

A ferramenta valida a configuração do Apache e do dispatcher. Ele verifica todos os arquivos com padrão `conf.d/enabled_vhosts/*.vhost` e verifica se somente as diretivas da lista de permissões são usadas. As diretivas permitidas nos arquivos de configuração do Apache podem ser listadas executando o comando da lista de permissões do validador:

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
  <Directory>
  ...
  
```

A tabela abaixo mostra os módulos de cache suportados:

| Nome do módulo | Página de referência |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

Os clientes não podem adicionar módulos arbitrários, no entanto, módulos adicionais podem ser considerados para inclusão no produto no futuro. Os clientes podem encontrar a lista de diretivas disponíveis para uma determinada versão do Dispatcher executando a &quot;lista de permissões do validador&quot; no SDK, conforme descrito na documentação das Ferramentas do Dispatcher.

A lista de permissões contém uma lista de diretivas do Apache que são permitidas em uma configuração do cliente. Se uma diretiva não estiver na lista de permissões, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Se nenhuma lista de permissões for fornecida na linha de comando (que é a forma como deve ser chamada), a ferramenta usará uma lista de permissões padrão que o Gerenciador de nuvem usará para validação antes de implantar nos ambientes da Cloud.

Além disso, verifica ainda mais todos os arquivos com padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe uma regra de filtro que use permitido via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes)
* Nenhum recurso administrativo é exposto. Por exemplo, acesso a caminhos como `/crx/de or /system/console`.

Quando executado em seu artefato maven ou em seu `dispatcher/src` subdiretório, ele reportará falhas de validação:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
 conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
 conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Observe que a ferramenta de validação relata somente o uso proibido das diretivas Apache que não foram incluídas na lista de permissões. Ele não relata problemas sintáticos ou semânticos com a configuração do Apache, pois essas informações só estão disponíveis para os módulos do Apache em um ambiente em execução.

Quando nenhuma falha de validação for relatada, sua configuração estará pronta para implantação.

Abaixo estão apresentadas técnicas de solução de problemas para depurar erros comuns de validação que são exibidos pela ferramenta:

**não é possível localizar uma`conf.dispatcher.d`subpasta no arquivo**

Seu arquivo deve conter as pastas `conf.d` e `conf.dispatcher.d`. Observe que você **não deve**
usar o prefixo `etc/httpd` em seu arquivo.

**não foi possível localizar nenhum farm em`conf.dispatcher.d/enabled_farms`**

Seus farm habilitados devem estar localizados na subpasta mencionada.

**o arquivo incluído (...) deve ser nomeado: ...**

Há duas seções na configuração do farm que **devem** incluir um arquivo específico: `/renders` e `/allowedClients` na `/cache` seção. Essas seções devem ter a seguinte aparência:

```
/renders {
    $include "../renders/default_renders.any"
}
```

e:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**arquivo incluído no local desconhecido: ...**

Há quatro seções na configuração do farm nas quais você pode incluir seu próprio arquivo: `/clientheaders`, `filters`, `/rules` na `/cache` seção e `/virtualhosts`. Os arquivos incluídos precisam ser nomeados da seguinte forma:

| Seção | Incluir nome de arquivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Como alternativa, inclua a versão **padrão** desses arquivos, cujos nomes são anexados à palavra `default_`, por exemplo, `../filters/default_filters.any`.

**inclua a declaração em (...), fora de qualquer local conhecido: ...**

Além das seis seções mencionadas nos parágrafos acima, você não tem permissão para usar a `$include` declaração, por exemplo, o seguinte geraria este erro:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**clientes/renderizadores permitidos não são incluídos de: ...**

Esse erro é gerado quando você não especifica uma inclusão para `/renders` e `/allowedClients` na `/cache` seção. Consulte o nome do **arquivo incluído (...): ...** para obter mais informações.

**o filtro não deve usar o padrão de bloqueio para permitir solicitações**

Não é seguro permitir solicitações com uma regra de `/glob` estilo, que corresponde à linha de solicitação completa, por exemplo,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrução destina-se a permitir solicitações para `css` arquivos, mas também permite solicitações para **qualquer** recurso seguido pela string de query `?a=.css`. Por conseguinte, é proibido utilizar tais filtros (ver também CVE-2016-0957).

**o arquivo incluído (...) não corresponde a nenhum arquivo conhecido**

Há dois tipos de arquivos na configuração do host virtual Apache que podem ser especificados como inclui: regravações e variáveis.
Os arquivos incluídos precisam ser nomeados da seguinte forma:

| Tipo | Incluir nome de arquivo |
|-----------|---------------------------------|
| Substitui | `conf.d/rewrites/rewrite.rules` |
| Variáveis | `conf.d/variables/custom.vars` |

Como alternativa, você pode incluir a versão **padrão** das regras de regravação, cujo nome é `conf.d/rewrites/default_rewrite.rules`.
Observe que não há uma versão padrão dos arquivos de variáveis.

**Foi detectado um layout de configuração obsoleto, habilitando o modo de compatibilidade**

Esta mensagem indica que sua configuração tem o layout obsoleto da versão 1, contendo uma configuração completa do Apache e arquivos com `ams_` prefixos. Embora isso ainda seja compatível com compatibilidade retroativa, você deve alternar para o novo layout.

## Teste da configuração do Apache e do Dispatcher localmente {#testing-apache-and-dispatcher-configuration-locally}

Também é possível testar a configuração do Apache e do Dispatcher localmente. Ele requer que o Docker seja instalado localmente e sua configuração passe na validação conforme descrito acima.

Ao usar o parâmetro &quot;`-d`&quot;, o validador gera uma pasta com todos os arquivos de configuração necessários para o dispatcher.

Em seguida, o `docker_run.sh` script pode apontar para essa pasta, iniciando o container com sua configuração.

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

Isso start o dispatcher em um container com seu backend apontando para uma instância do AEM em execução em sua máquina local do Mac OS na porta 4503.

## Depuração da configuração do Apache e do Dispatcher {#debugging-apache-and-dispatcher-configuration}

A estratégia a seguir pode ser usada para aumentar a saída do log para o módulo do dispatcher e ver o resultado da `RewriteRule` avaliação em ambientes locais e em nuvem.

Os níveis de log desses módulos são definidos pelas variáveis `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Eles podem ser definidos no arquivo `conf.d/variables/global.vars`. A sua parte relevante é a seguinte:

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

Ao executar o Dispatcher localmente, os registros também são impressos diretamente na saída do terminal. Na maioria das vezes, esses registros devem estar em DEBUG, o que pode ser feito transmitindo o nível de Depuração como parâmetro ao executar o Docker. Por exemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

Os registros de ambientes na nuvem serão expostos por meio do serviço de registro disponível no Cloud Manager.

## Diferentes configurações do Dispatcher por ambiente {#different-dispatcher-configurations-per-environment}

No momento, a mesma configuração do despachante é aplicada a todo o AEM como ambientes do serviço em nuvem. O tempo de execução terá uma variável de ambiente `ENVIRONMENT_TYPE` que contém o modo de execução atual (dev, stage ou prod), bem como uma definição. A definição pode ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` ou `ENVIRONMENT_PROD`. Na configuração do Apache, a variável pode ser usada diretamente em uma expressão. Como alternativa, a definição pode ser usada para construir lógica:

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

Na configuração do Dispatcher, a mesma variável de ambiente está disponível. Se for necessária mais lógica, defina as variáveis como mostrado no exemplo acima e use-as na seção de configuração do Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Ao testar sua configuração localmente, você pode simular diferentes tipos de ambientes transmitindo a variável `DISP_RUN_MODE` para o `docker_run.sh` script diretamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

O modo de execução padrão quando não é transmitido um valor para DISP_RUN_MODE é &quot;dev&quot;.
Para obter uma lista completa de opções e variáveis disponíveis, execute o script `docker_run.sh` sem argumentos.

## Exibição da configuração do Dispatcher em uso pelo seu container Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Com configurações específicas do ambiente, pode ser difícil determinar a aparência real da configuração do Dispatcher. Depois de ter iniciado o container do seu estivador com `docker_run.sh` ele, ele pode ser despejado da seguinte forma:

* Determine a ID do container do docker em uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Execute a seguinte linha de comando com essa ID de container:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Principais diferenças entre o AMS Dispatcher e o AEM como um serviço em nuvem {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Conforme descrito na página de referência acima, a configuração do Apache e do Dispatcher no AEM como um serviço em nuvem é muito semelhante à do AMS. As principais diferenças são:

* No AEM como um serviço em nuvem, algumas diretivas do Apache não podem ser usadas (por exemplo `Listen` ou `LogLevel`)
* No AEM como um serviço em nuvem, somente algumas partes da configuração do Dispatcher podem ser colocadas em arquivos de inclusão e sua nomeação é importante. Por exemplo, regras de filtragem que você deseja reutilizar em diferentes hosts devem ser colocadas em um arquivo chamado `filters/filters.any`. Consulte a página de referência para obter mais informações.
* No AEM como um serviço de nuvem há validação extra para proibir regras de filtro gravadas usando `/glob` o para evitar problemas de segurança. Como `deny *` serão usados em vez de `allow *` (que não podem ser usados), os clientes se beneficiarão com a execução local do Dispatcher e com erros, observando os registros para saber exatamente quais caminhos os filtros do Dispatcher estão bloqueando para que eles possam ser adicionados.

## Diretrizes para migrar a configuração do dispatcher do AMS para o AEM como um serviço em nuvem

A estrutura de configuração do dispatcher tem diferenças entre os Serviços gerenciados e o AEM como um Serviço em nuvem. Apresentado abaixo, é um guia passo a passo sobre como migrar da configuração do AMS Dispatcher versão 2 para o AEM como um serviço em nuvem.

## Como converter um AMS em um AEM como uma configuração de despachante de serviço da Cloud

A seção a seguir fornece instruções passo a passo sobre como converter uma configuração do AMS. Pressupõe que você tenha um arquivo com uma estrutura semelhante à descrita na configuração do dispatcher do [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extraia o arquivo e remova um prefixo final

Extraia o arquivo para uma pasta e certifique-se de que as subpastas imediatas estejam em start com `conf`, `conf.d``conf.dispatcher.d` e `conf.modules.d`. Se não, mova-os para cima na hierarquia.

### Livre-se de subpastas e arquivos não usados

Remova subpastas `conf` e `conf.modules.d`arquivos correspondentes `conf.d/*.conf`.

### Livre-se de todos os hosts virtuais que não sejam de publicação

Remova qualquer arquivo de host virtual em `conf.d/enabled_vhosts` que tenha `author`, `unhealthy``health`,`lc` ou `flush` em seu nome. Todos os arquivos de host virtual em `conf.d/available_vhosts` que não estão vinculados também podem ser removidos.

### Remova ou comente seções de host virtual que não se referem à porta 80

Se você ainda tiver seções nos arquivos do host virtual que se referem exclusivamente a outras portas que não a porta 80, por exemplo

```
<VirtualHost *:443>
...
</VirtualHost>
```

remova ou comente-os. As declarações nessas seções não serão processadas, mas se você as mantiver por perto, você ainda poderá editá-las sem nenhum efeito, o que é confuso.

### Verificar regravações

Enter directory `conf.d/rewrites`.

Remova qualquer arquivo nomeado `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e lembre-se de remover `Include` instruções nos arquivos de host virtual que se referem a elas.

Se `conf.d/rewrites` agora contiver um único arquivo, ele deverá ser renomeado para `rewrite.rules` e não se esqueça de adaptar as `Include` declarações referentes a esse arquivo também nos arquivos do host virtual.

No entanto, se a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a `Include` declaração referente a eles nos arquivos do host virtual.

### Verificar variáveis

Enter directory `conf.d/variables`.

Remova qualquer arquivo nomeado `ams_default.vars` e lembre-se de remover `Include` declarações nos arquivos do host virtual que se referem a elas.

Se `conf.d/variables` agora contiver um único arquivo, ele deverá ser renomeado para `custom.vars` e não se esqueça de adaptar as `Include` declarações referentes a esse arquivo também nos arquivos do host virtual.

No entanto, se a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a `Include` declaração referente a eles nos arquivos do host virtual.

### Remover listas de permissões

Remova a pasta `conf.d/whitelists` e remova `Include` as instruções nos arquivos do host virtual que fazem referência a algum arquivo dessa subpasta.

### Substituir qualquer variável que não esteja mais disponível

Em todos os arquivos de host virtual:

Renomear `PUBLISH_DOCROOT` para `DOCROOT`Remover seções que façam referência a variáveis nomeadas `DISP_ID`, `PUBLISH_FORCE_SSL` ou `PUBLISH_WHITELIST_ENABLED`

### Verifique seu estado executando o validador

Execute o validador do dispatcher no diretório, com o `httpd` subcomando:

```
$ validator httpd .
```

Se você vir erros sobre arquivos include ausentes, verifique se você renomeou esses arquivos corretamente.

Se você vir diretivas Apache que não estão na lista de permissões, remova-as.

### Eliminar todos os farm que não são publicados

Remova qualquer arquivo de farm em `conf.dispatcher.d/enabled_farms` que tenha `author`, `unhealthy`, `health`ou`lc` `flush` em seu nome. Todos os arquivos de farm nos `conf.dispatcher.d/available_farms` quais não há vínculo também podem ser removidos.

### Renomear arquivos do farm

Todas as explorações agrícolas em `conf.d/enabled_farms` devem ser renomeadas para corresponder ao padrão `*.farm`, portanto, por exemplo, o arquivo de uma exploração chamado `customerX_farm.any` deve ser renomeado `customerX.farm`.

### Verificar cache

Enter directory `conf.dispatcher.d/cache`.

Remova qualquer arquivo prefixo `ams_`.

Se agora `conf.dispatcher.d/cache` estiver vazio, copie o arquivo `conf.dispatcher.d/cache/rules.any`da configuração padrão do dispatcher para esta pasta. A configuração padrão do dispatcherches pode ser encontrada na pasta `src` deste SDK. Não se esqueça de adaptar as`$include` `ams_*_cache.any` declarações referentes aos arquivos de regras nos arquivos do farm também.

Se, em vez disso, `conf.dispatcher.d/cache` agora contiver um único arquivo com sufixo `_cache.any`, ele deverá ser renomeado para `rules.any` e não se esqueça de adaptar as `$include` declarações referentes a esse arquivo também nos arquivos do farm.

No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a `$include` declaração que os referencia nos arquivos do farm.

Remova qualquer arquivo que tenha o sufixo `_invalidate_allowed.any`.

Copie o arquivo `conf.dispatcher.d/cache/default_invalidate_any` do defaultAEM na configuração do despachante do Cloud para esse local.

Em cada arquivo de farm, remova qualquer conteúdo na `cache/allowedClients` seção e substitua-o por:

```
$include "../cache/default_invalidate.any"
```

### Verificar cabeçalhos do cliente

Enter directory `conf.dispatcher.d/clientheaders`.

Remova qualquer arquivo prefixo `ams_`.

Se `conf.dispatcher.d/clientheaders` agora contiver um único arquivo com sufixo `_clientheaders.any`, ele deverá ser renomeado para `clientheaders.any` e não se esqueça de adaptar as `$include` declarações referentes a esse arquivo também nos arquivos do farm.

No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a `$include` declaração que os referencia nos arquivos do farm.

Copie o arquivo `conf.dispatcher/clientheaders/default_clientheaders.any` da configuração padrão do AEM como um despachante do serviço de nuvem para esse local.

Em cada arquivo de farm, substitua todas as instruções de inclusão do cliente que tenham a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

com a declaração:

```
$include "../clientheaders/default_clientheaders.any"
```

### Verificar filtro

Enter directory `conf.dispatcher.d/filters`.

Remova qualquer arquivo prefixo `ams_`.

Se `conf.dispatcher.d/filters` agora contiver um único arquivo, ele deverá ser renomeado`filters.any` e não se esqueça de adaptar as `$include` declarações referentes a esse arquivo também nos arquivos do farm.

No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a `$include` declaração que os referencia nos arquivos do farm.

Copie o arquivo `conf.dispatcher/filters/default_filters.any` da configuração padrão do AEM como um despachante do serviço de nuvem para esse local.

Em cada arquivo de farm, substitua todas as instruções de inclusão de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

com a declaração:

```
$include "../filters/default_filters.any"
```

### Verificar renderizações

Enter directory `conf.dispatcher.d/renders`.

Remova todos os arquivos dessa pasta.

Copie o arquivo `conf.dispatcher.d/renders/default_renders.any` da configuração padrão do AEM como um despachante do serviço de nuvem para esse local.

Em cada arquivo de farm, remova qualquer conteúdo na `renders` seção e substitua-o por:

```
$include "../renders/default_renders.any"
```

### Verificar hosts virtuais

Renomeie o diretório `conf.dispatcher.d/vhosts` para `conf.dispatcher.d/virtualhosts` e insira-o.

Remova qualquer arquivo prefixo `ams_`.

Se `conf.dispatcher.d/virtualhosts` agora contiver um único arquivo, ele deverá ser renomeado`virtualhosts.any` e não se esqueça de adaptar as `$include` declarações referentes a esse arquivo também nos arquivos do farm.

No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a `$include` declaração que os referencia nos arquivos do farm.

Copie o arquivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` da configuração padrão do AEM como um despachante do serviço de nuvem para esse local.

Em cada arquivo de farm, substitua todas as instruções de inclusão de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

com a declaração:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Verifique seu estado executando o validador

Execute o AEM como um validador de despachante do serviço em nuvem no diretório, com o `dispatcher` subcomando:

```
$ validator dispatcher .
```

Se você vir erros sobre arquivos include ausentes, verifique se você renomeou esses arquivos corretamente.

Se você vir erros referentes a variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

Para cada outro erro, consulte a seção Solução de problemas da documentação da ferramenta do evalidator.

### Teste sua configuração com uma implantação local (requer a instalação do Docker)

Usando o script `docker_run.sh` no AEM como uma ferramenta de despacho de serviços em nuvem, é possível testar se a configuração não contém nenhum outro erro que apareça somente na implantação:

### Etapa 1: Gerar informações de implantação com o validador

```
validator full -d out .
```

Isso valida a configuração completa e gera informações de implantação em `out`

### Etapa 2: Start do despachante em uma imagem do docker com essas informações de implantação

Com o servidor de publicação de AEM em execução no computador macOS, ouvindo na porta 4503, você pode executar o start do despachante na frente desse servidor da seguinte forma:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Isso start o container e expõe o Apache na porta local 8080.

### Usar a nova configuração do dispatcher

Parabéns! Se o validador não relatar mais nenhum problema e o container do docker for start sem falhas ou avisos, você estará pronto para mover sua configuração para um `dispatcher/src` subdiretório do repositório git.

**Os clientes que estão usando a configuração do AMS Dispatcher versão 1 devem entrar em contato com o suporte ao cliente para ajudá-los a migrar da versão 1 para a versão 2 para que as instruções acima possam ser seguidas.**
