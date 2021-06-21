---
title: Dispatcher na nuvem
description: 'Dispatcher na nuvem '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: cf42e530136d5eb8afe7204ae0af1353b1f31cbd
workflow-type: tm+mt
source-wordcount: '4247'
ht-degree: 6%

---

# Dispatcher na nuvem {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher na nuvem"
>abstract="Esta seção descreve como estruturar o AEM como um Cloud Service Apache e configurações do Dispatcher, bem como como como validá-lo e executá-lo localmente antes de implantá-lo em ambientes do Cloud. Também descreve a depuração em ambientes do Cloud."

## Configuração e teste do Apache e Dispatcher {#apache-and-dispatcher-configuration-and-testing}

Esta seção descreve como estruturar o AEM como um Cloud Service Apache e configurações do Dispatcher, bem como como como validá-lo e executá-lo localmente antes de implantá-lo em ambientes do Cloud. Também descreve a depuração em ambientes do Cloud. Para obter informações adicionais sobre o Dispatcher, consulte a [AEM documentação do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR).

>[!NOTE]
>Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Isso é um pré-requisito para executar e depurar o Dispatcher em um computador local. As seções abaixo incluem comandos usando as versões Mac ou Linux do SDK, mas o SDK do Windows pode ser usado de maneira semelhante.

## Ferramentas do Dispatcher {#dispatcher-sdk}

As Ferramentas do Dispatcher fazem parte do AEM geral como um Cloud Service SDK e fornecem:

* Uma estrutura de arquivo baunilha contendo os arquivos de configuração a serem incluídos em um projeto maven para o Dispatcher.
* Ferramentas para clientes validarem se a configuração do Dispatcher inclui apenas AEM como diretivas suportadas pelo Cloud Service.        Além disso, a ferramenta também valida que a sintaxe está correta para que o apache possa ser iniciado com êxito.
* Uma imagem Docker que exibe o Dispatcher localmente.

## Download e extração das ferramentas {#extracting-the-sdk}

As Ferramentas do Dispatcher, parte do [AEM como um Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), podem ser baixadas de um arquivo zip no portal [Distribuição de software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Qualquer nova configuração disponível nessa nova versão das Ferramentas do Dispatcher pode ser usada para implantar em ambientes do Cloud que executam essa versão de AEM na Cloud ou posterior.

Descompacte o SDK, que agrupa as Ferramentas do Dispatcher para macOS, Linux e Windows.

**Para macOS/Linux**, torne o artefato da ferramenta Dispatcher executável e execute-o. Ele extrairá automaticamente os arquivos das Ferramentas do Dispatcher sob o diretório em que você o armazenou (onde `version` é a versão das Ferramentas do Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**No Windows**, extraia o arquivo zip Dispatcher Tool.

## Estrutura de arquivo {#file-structure}

A estrutura da subpasta do Dispatcher do projeto é descrita abaixo e deve ser copiada para a pasta do Dispatcher do projeto maven:

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

Abaixo está uma explicação de arquivos notáveis que podem ser modificados:

**Arquivos personalizáveis**

Os arquivos a seguir são personalizáveis e serão transferidos para sua instância do Cloud na implantação:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Você pode ter um ou mais desses arquivos. Eles contêm `<VirtualHost>` entradas que correspondem aos nomes de host e permitem que o Apache manipule cada tráfego de domínio com regras diferentes. Os arquivos são criados no diretório `available_vhosts` e ativados com um link simbólico no diretório `enabled_vhosts`. Nos arquivos `.vhost`, outros arquivos como regravações e variáveis serão incluídos.

* `conf.d/rewrites/rewrite.rules`

Este arquivo é incluído de dentro de seus arquivos `.vhost`. Ele tem um conjunto de regras de regravação para `mod_rewrite`.

>[!NOTE]
>
>Atualmente, um único arquivo de reescrita deve ser usado em vez de arquivos específicos do site. Como regra, a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1MB.

* `conf.d/variables/custom.vars`

Este arquivo é incluído de dentro de seus arquivos `.vhost`. Você pode adicionar definições para variáveis do Apache neste local.

* `conf.d/variables/global.vars`

Este arquivo está incluído de dentro do arquivo `dispatcher_vhost.conf`. Você pode alterar seu Dispatcher e reescrever o nível de log neste arquivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Você pode ter um ou mais desses arquivos e eles contêm farms para corresponder aos nomes de host e permitir que o módulo Dispatcher manipule cada farm com regras diferentes. Os arquivos são criados no diretório `available_farms` e ativados com um link simbólico no diretório `enabled_farms`. Nos arquivos `.farm`, outros arquivos como filtros, regras de cache e outros serão incluídos.

* `conf.dispatcher.d/cache/rules.any`

Este arquivo é incluído de dentro de seus arquivos `.farm`. Especifica preferências de armazenamento em cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este arquivo é incluído de dentro de seus arquivos `.farm`. Especifica quais cabeçalhos de solicitação devem ser encaminhados ao backend.

* `conf.dispatcher.d/filters/filters.any`

Este arquivo é incluído de dentro de seus arquivos `.farm`. Ele tem um conjunto de regras que alteram o tráfego que deve ser filtrado e não para o back-end.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este arquivo é incluído de dentro de seus arquivos `.farm`. Ela tem uma lista de nomes de host ou caminhos de URI a serem correspondidos pela correspondência glob. Isso determina qual back-end usar para servir uma solicitação.

Os arquivos acima fazem referência aos arquivos de configuração imutáveis listados abaixo. As alterações nos arquivos imutáveis não serão processadas pelo Dispatchers em ambientes Cloud.

**Arquivos de configuração imutáveis**

Esses arquivos fazem parte da estrutura básica e impõem padrões e práticas recomendadas. Os arquivos são considerados imutáveis porque modificá-los ou excluí-los localmente não terá impacto na implantação, pois não serão transferidos para a instância do Cloud.

É recomendável que os arquivos acima façam referência aos arquivos imutáveis listados abaixo, seguidos de quaisquer instruções ou substituições adicionais. Quando a configuração do Dispatcher é implantada em um ambiente de nuvem, a versão mais recente dos arquivos imutáveis será usada, independentemente da versão usada no desenvolvimento local.

* `conf.d/available_vhosts/default.vhost`

Contém um host virtual de amostra. Para seu próprio host virtual, crie uma cópia desse arquivo, personalize-o, vá para `conf.d/enabled_vhosts` e crie um link simbólico para sua cópia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte da estrutura base, usada para ilustrar como os hosts virtuais e as variáveis globais são incluídos.

* `conf.d/rewrites/default_rewrite.rules`

Regras padrão de reescrita adequadas para um projeto padrão. Se precisar de personalização, modifique `rewrite.rules`. Na personalização, ainda é possível incluir as regras padrão primeiro, se elas atenderem às suas necessidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contém uma amostra de farm do Dispatcher. Para seu próprio farm, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_farms` e crie um link simbólico para sua cópia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte da estrutura base é gerada na inicialização. Você é **necessário** para incluir esse arquivo em cada farm definido, na seção `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Regras de cache padrão adequadas para um projeto padrão. Se precisar de personalização, modifique `conf.dispatcher.d/cache/rules.any`. Na personalização, ainda é possível incluir as regras padrão primeiro, se elas atenderem às suas necessidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Cabeçalhos de solicitação padrão para encaminhar ao backend, adequados para um projeto padrão. Se precisar de personalização, modifique `clientheaders.any`. Na personalização, você ainda pode incluir os cabeçalhos de solicitação padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/dispatcher.any`

Parte da estrutura base, usada para ilustrar como os farms do Dispatcher são incluídos.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros padrão adequados para um projeto padrão. Se precisar de personalização, modifique `filters.any`. Na personalização, você ainda pode incluir os filtros padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/renders/default_renders.any`

Parte da estrutura base, esse arquivo é gerado na inicialização. Você é **necessário** para incluir esse arquivo em cada farm definido, na seção `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globalização de host padrão adequada para um projeto padrão. Se precisar de personalização, modifique `virtualhosts.any`. Na personalização, você não deve incluir a globalização de host padrão, pois ela corresponde a **cada** solicitação recebida.

>[!NOTE]
>
>O AEM como um arquétipo de maven Cloud Service gerará a mesma estrutura de arquivo de configuração do Dispatcher.

As seções abaixo descrevem como validar a configuração localmente para que possa passar a porta de qualidade associada no Cloud Manager ao implantar uma versão interna.

## Validação local de diretivas compatíveis na configuração do Dispatcher {#local-validation-of-dispatcher-configuration}

A ferramenta de validação está disponível no SDK em `bin/validator` como um binário do Mac OS, Linux ou Windows, permitindo que os clientes executem a mesma validação que o Cloud Manager executará ao criar e implantar uma versão.

É invocado como: `validator full [-d folder] [-w allowlist] zip-file | src folder`

A ferramenta valida que a configuração do Dispatcher está usando as diretivas apropriadas compatíveis com o AEM as a Cloud Service, digitalizando todos os arquivos com o padrão `conf.d/enabled_vhosts/*.vhost`.

No Windows, o validador do dispatcher faz distinção entre maiúsculas e minúsculas. Dessa forma, poderá ocorrer uma falha na validação da configuração se você não respeitar a capitalização do caminho em que a configuração reside, por exemplo:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite esse erro copiando e colando o caminho do Windows Explorer e, em seguida, no prompt de comando usando um comando `cd` nesse caminho.

As diretivas permitidas nos arquivos de configuração do Apache podem ser listadas executando o comando de  lista de permissões do validador:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

A tabela abaixo mostra os módulos apache suportados:

| Nome do módulo | Página de referência |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
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
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

Os clientes não podem adicionar módulos arbitrários, no entanto, módulos adicionais podem ser considerados para inclusão futura no produto. Os clientes podem encontrar a lista de diretivas disponíveis para uma determinada versão do Dispatcher executando o comando de  lista de permissões do validador no SDK, conforme descrito acima.

A  lista de permissões contém uma lista de diretivas Apache que são permitidas em uma configuração de cliente. Se uma diretiva não for incluir na lista de permissões, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Se nenhuma  lista de permissões for fornecida na linha de comando (que é a forma como ela deve ser invocada), a ferramenta usará uma  de lista de permissões padrão que o Cloud Manager usará para validação antes de implantar em ambientes do Cloud.

Além disso, ele verifica todos os arquivos com o padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe uma regra de filtro que use o permite via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes)
* Nenhum recurso administrativo é exposto. Por exemplo, acesso a caminhos como `/crx/de or /system/console`.

Quando executado em seu artefato maven ou subdiretório `dispatcher/src`, ele reportará falhas de validação:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Observe que a ferramenta de validação relata apenas o uso proibido das diretivas Apache que não foram incluir na lista de permissões. Ele não relata problemas sintáticos ou semânticos com a configuração do Apache, pois essas informações só estão disponíveis para os módulos Apache em um ambiente em execução.

Apresentamos abaixo as técnicas de solução de problemas para depurar erros comuns de validação que são gerados pela ferramenta:

**não é possível localizar uma  `conf.dispatcher.d` subpasta no arquivo**

Seu arquivo deve conter as pastas `conf.d` e `conf.dispatcher.d`. Observe que você **não deve**
usar o prefixo `etc/httpd` em seu arquivo.

**não é possível localizar nenhum farm em`conf.dispatcher.d/enabled_farms`**

Os farms ativados devem estar localizados na subpasta mencionada.

**arquivo incluído (..) deve ser nomeado como: ...**

Há duas seções na configuração do farm que **devem** incluir um
arquivo específico: `/renders` e `/allowedClients` na seção `/cache`. Esses
As seções devem ter a seguinte aparência:

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

Há quatro seções na configuração do farm em que você pode incluir seu próprio arquivo: `/clientheaders`, `filters`, `/rules` na seção `/cache` e `/virtualhosts`. Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Seção | Incluir nome de arquivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Como alternativa, inclua a versão **padrão** desses arquivos, cujos nomes são anexados à palavra `default_`, por exemplo, `../filters/default_filters.any`.

**inclua instrução em (..), fora de qualquer local conhecido: ...**

Além das seis seções mencionadas nos parágrafos acima, você não é permitido
para usar a instrução `$include`, por exemplo, o seguinte geraria este erro:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**clientes/renderizadores permitidos não são incluídos de: ...**

Esse erro é gerado quando você não especifica uma inclusão para `/renders` e `/allowedClients` na seção `/cache`. Consulte a
**arquivo incluído (...) deve ser nomeado como: ...** para obter mais informações.

**o filtro não deve usar o padrão glob para permitir solicitações**

Não é seguro permitir solicitações com uma regra de estilo `/glob`, que é correspondida com a linha de solicitação completa, por exemplo

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Essa instrução destina-se a permitir solicitações para arquivos `css`, mas também permite solicitações para **qualquer** recurso seguido pela sequência de consulta `?a=.css`. Por conseguinte, é proibido utilizar esses filtros (ver também CVE-2016-0957).

**o arquivo incluído (...) não corresponde a nenhum arquivo conhecido**

Há dois tipos de arquivos na configuração de host virtual do Apache que podem ser especificados como inclui: regravações e variáveis.
Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Tipo | Incluir nome de arquivo |
|-----------|---------------------------------|
| Regravações | `conf.d/rewrites/rewrite.rules` |
| Variáveis | `conf.d/variables/custom.vars` |

Como alternativa, você pode incluir a versão **padrão** das regras de regravação, cujo nome é `conf.d/rewrites/default_rewrite.rules`.
Observe que não há uma versão padrão dos arquivos de variáveis.

**Foi detectado um layout de configuração obsoleto, habilitando o modo de compatibilidade**

Essa mensagem indica que sua configuração tem o layout obsoleto da versão 1, contendo um relatório completo
Configuração do Apache e arquivos com prefixos `ams_`. Embora isso ainda seja compatível com versões anteriores
, você deve alternar para o novo layout.

## Validação local da sintaxe de configuração do Dispatcher para que o apache httpd possa iniciar {#local-validation}

Depois de estabelecer que a configuração do módulo Dispatcher inclui apenas diretivas compatíveis, você deve verificar se a sintaxe está correta para que o apache possa ser iniciado. Para testar isso, o docker deve ser instalado localmente. E observe que não é necessário AEM estar funcionando.

Use o script `validate.sh` conforme mostrado abaixo:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

O script faz o seguinte:

1. Ele executa o validador da seção anterior para garantir que apenas as diretivas compatíveis sejam incluídas. Se a configuração não for válida, o script falhará.
2. Ela executa `httpd -t command` para testar se a sintaxe está correta, de forma que o apache httpd possa ser iniciado. Se bem-sucedida, a configuração deve estar pronta para implantação.
3. Verifica se o subconjunto dos arquivos de configuração do SDK do Dispatcher, que devem ser imutáveis conforme descrito na seção [File structure](#file-structure), não foi modificado. Esta é uma nova verificação, introduzida com AEM versão v2021.1.4738 do SDK, que também inclui a versão 2.0.36 das Ferramentas do Dispatcher. Antes dessa atualização, os clientes podem ter presumido incorretamente que quaisquer modificações do SDK local desses arquivos imutáveis também seriam aplicadas ao ambiente do Cloud.

Durante uma implantação do Cloud Manager, a verificação `httpd -t syntax` também será executada e todos os erros serão incluídos no log `Build Images step failure` do Cloud Manager.

## Testar a configuração do Apache e Dispatcher localmente {#testing-apache-and-dispatcher-configuration-locally}

Também é possível testar a configuração do Apache e Dispatcher localmente. Requer que o docker seja instalado localmente e sua configuração passe na validação conforme descrito acima.

Execute a ferramenta validador (observe que é diferente do `validator.sh` mencionado anteriormente), usando o parâmetro `-d` que gera uma pasta com todos os arquivos de configuração do Dispatcher. Em seguida, execute o script `docker_run.sh`, transmitindo essa pasta como um argumento. Fornecendo o número da porta (aqui: 8080) para expor o endpoint do Dispatcher, um container do Docker é iniciado, executando o Dispatcher com sua configuração.

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

Isso inicia o Dispatcher em um contêiner com seu back-end apontando para uma instância de AEM em execução no computador local do Mac OS na porta 4503.

## Depuração da configuração do Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

A estratégia a seguir pode ser usada para aumentar a saída de log do módulo Dispatcher e ver os resultados da avaliação `RewriteRule` em ambientes locais e de nuvem.

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

Ao executar o Dispatcher localmente, os logs são impressos diretamente na saída do terminal. Na maioria das vezes, você deseja que esses logs estejam em DEBUG, o que pode ser feito transmitindo o nível de Depuração como parâmetro ao executar o Docker. Por exemplo: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Os logs para ambientes de nuvem são expostos por meio do serviço de registro disponível no Cloud Manager.

## Diferentes configurações do Dispatcher por ambiente {#different-dispatcher-configurations-per-environment}

Atualmente, a mesma configuração do Dispatcher é aplicada a todos os AEM como ambientes Cloud Service. O tempo de execução terá uma variável de ambiente `ENVIRONMENT_TYPE` que contém o modo de execução atual (dev, stage ou prod), bem como uma definição. A definição pode ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` ou `ENVIRONMENT_PROD`. Na configuração do Apache, a variável pode ser usada diretamente em uma expressão. Como alternativa, a definição pode ser usada para criar lógica:

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

Na configuração do Dispatcher, a mesma variável de ambiente está disponível. Se for necessária mais lógica, defina as variáveis conforme mostrado no exemplo acima e use-as na seção Configuração do Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Ao testar sua configuração localmente, você pode simular diferentes tipos de ambiente transmitindo a variável `DISP_RUN_MODE` para o script `docker_run.sh` diretamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

O modo de execução padrão ao não transmitir um valor para DISP_RUN_MODE é &quot;dev&quot;.
Para obter uma lista completa de opções e variáveis disponíveis, execute o script `docker_run.sh` sem argumentos.

## Visualização da configuração do Dispatcher em uso pelo seu contêiner do Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Com configurações específicas do ambiente, pode ser difícil determinar a aparência real da configuração do Dispatcher. Depois de iniciar o contêiner do docker com `docker_run.sh`, ele pode ser descartado da seguinte maneira:

* Determine a ID do contêiner do docker em uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Execute a seguinte linha de comando com essa ID de contêiner:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Principais diferenças entre o AMS Dispatcher e o AEM como Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Conforme descrito na página de referência acima, a configuração do Apache e Dispatcher no AEM como um Cloud Service é bastante semelhante à do AMS. As principais diferenças são:

* No AEM como um Cloud Service, algumas diretivas Apache podem não ser usadas (por exemplo `Listen` ou `LogLevel`)
* No AEM como um Cloud Service, somente algumas partes da configuração do Dispatcher podem ser colocadas em arquivos de inclusão e sua nomenclatura é importante. Por exemplo, as regras de filtro que você deseja reutilizar em hosts diferentes devem ser colocadas em um arquivo chamado `filters/filters.any`. Consulte a página de referência para obter mais informações.
* No AEM como um Cloud Service, há validação extra para não permitir regras de filtro gravadas usando `/glob` para evitar problemas de segurança. Como `deny *` será usado em vez de `allow *` (que não pode ser usado), os clientes se beneficiarão de executar o Dispatcher localmente e de fazer tentativa e erro, observando os logs para saber exatamente quais caminhos os filtros do Dispatcher estão bloqueando para que eles possam ser adicionados.

## Diretrizes para migrar a configuração do dispatcher do AMS para o AEM como um Cloud Service

A estrutura de configuração do Dispatcher tem diferenças entre o Managed Services e o AEM como Cloud Service. Apresentado abaixo, é um guia passo a passo sobre como migrar da configuração do AMS Dispatcher versão 2 para o AEM como Cloud Service.

## Como converter um AMS em uma configuração de Dispatcher do AEM as a Cloud Service

A seção a seguir fornece instruções passo a passo sobre como converter uma configuração do AMS. Ele parte do princípio
que você tem um arquivo com uma estrutura semelhante à descrita em [Configuração do Dispatcher do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrair o arquivo morto e remover um eventual prefixo

Extraia o arquivo morto para uma pasta e verifique se as subpastas imediatas começam com `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. Caso contrário, mova-os para cima na hierarquia.

### Livrar-se de subpastas e arquivos não utilizados

Remova as subpastas `conf` e `conf.modules.d`, bem como os arquivos correspondentes a `conf.d/*.conf`.

### Livrar-se de todos os hosts virtuais que não sejam de publicação

Remova qualquer arquivo de host virtual em `conf.d/enabled_vhosts` que tenha `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos de host virtual em `conf.d/available_vhosts` que não estejam
vinculada ao também pode ser removida.

### Remova ou comente seções de host virtual que não se refiram à porta 80

Se você ainda tiver seções nos arquivos de host virtual que se referem exclusivamente a outras portas além da porta 80, por exemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```

remova-as ou comente-as. As instruções nessas seções não serão processadas, mas, se você as mantiver por perto, ainda poderá editá-las sem efeito, o que é confuso.

### Verificar regravações

Entre no diretório `conf.d/rewrites`.

Remova qualquer arquivo chamado `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e lembre-se de
remova as instruções `Include` nos arquivos de host virtual que fazem referência a elas.

Se `conf.d/rewrites` agora contiver um único arquivo, ele deverá ser renomeado para `rewrite.rules` e não
esqueça de adaptar também as instruções `Include` referentes a esse arquivo nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos de host virtual, seu conteúdo deverá ser
copiada para a instrução `Include` referenciando-a nos arquivos de host virtual.

### Verificar variáveis

Entre no diretório `conf.d/variables`.

Remova qualquer arquivo chamado `ams_default.vars` e lembre-se de remover as instruções `Include` no virtual
os arquivos host que fazem referência a eles.

Se `conf.d/variables` agora contiver um único arquivo, ele deverá ser renomeado para `custom.vars` e não
esqueça de adaptar também as instruções `Include` referentes a esse arquivo nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos de host virtual, seu conteúdo deverá ser
copiada para a instrução `Include` referenciando-a nos arquivos de host virtual.

### Remover listas de permissões

Remova a pasta `conf.d/whitelists` e remova as instruções `Include` nos arquivos de host virtual referentes a
algum arquivo nessa subpasta.

### Substituir qualquer variável que não esteja mais disponível

Em todos os arquivos de host virtual:

Renomeie `PUBLISH_DOCROOT` para `DOCROOT`
Remova as seções que fazem referência às variáveis chamadas `DISP_ID`, `PUBLISH_FORCE_SSL` ou `PUBLISH_WHITELIST_ENABLED`

### Verificar o estado executando o validador

Execute o validador do Dispatcher no seu diretório, com o subcomando `httpd`:

```
$ validator httpd .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente.

Se você vir diretivas Apache que não estão incluir na lista de permissões, remova-as.

### Livrar-se de todos os farms não publicados

Remova qualquer arquivo do farm em `conf.dispatcher.d/enabled_farms` que tenha `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos farm em `conf.dispatcher.d/available_farms` que não estão
vinculada ao também pode ser removida.

### Renomear arquivos de farm

Todos os farms em `conf.d/enabled_farms` devem ser renomeados para corresponder ao padrão `*.farm`, portanto, por exemplo, um
O arquivo do farm chamado `customerX_farm.any` deve ser renomeado para `customerX.farm`.

### Verificar cache

Entre no diretório `conf.dispatcher.d/cache`.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/cache` agora estiver vazio, copie o arquivo `conf.dispatcher.d/cache/rules.any`
da configuração padrão do Dispatcher para essa pasta. O Dispatcher padrão
a configuração pode ser encontrada na pasta `src` deste SDK. Não se esqueça de adaptar a
`$include` instruções referentes aos arquivos de regra `ams_*_cache.any` nos arquivos do farm
também.

Se, em vez disso, `conf.dispatcher.d/cache` agora contiver um único arquivo com o sufixo `_cache.any`,
ele deve ser renomeado para `rules.any` e não se esqueça de adaptar as instruções `$include`
fazer referência a esse arquivo também nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Remova qualquer arquivo que tenha o sufixo `_invalidate_allowed.any`.

Copie o arquivo `conf.dispatcher.d/cache/default_invalidate_any` do padrão
AEM na configuração do Cloud Dispatcher para esse local.

Em cada arquivo do farm, remova qualquer conteúdo da seção `cache/allowedClients` e substitua-o
com:

```
$include "../cache/default_invalidate.any"
```

### Verificar cabeçalhos do cliente

Entre no diretório `conf.dispatcher.d/clientheaders`.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/clientheaders` agora contiver um único arquivo com o sufixo `_clientheaders.any`,
ele deve ser renomeado para `clientheaders.any` e não se esqueça de adaptar as instruções `$include`
fazer referência a esse arquivo também nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copie o arquivo `conf.dispatcher/clientheaders/default_clientheaders.any` do padrão
AEM como uma configuração do Dispatcher do Cloud Service para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de clientheader com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

pela instrução:

```
$include "../clientheaders/default_clientheaders.any"
```

### Verificar filtro

Entre no diretório `conf.dispatcher.d/filters`.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/filters` agora contiver um único arquivo, ele deverá ser renomeado para
`filters.any` e não se esqueça de adaptar as instruções `$include` referentes a isso
nos arquivos farm também.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copie o arquivo `conf.dispatcher/filters/default_filters.any` do padrão
AEM como uma configuração do Dispatcher do Cloud Service para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

pela instrução:

```
$include "../filters/default_filters.any"
```

### Verificar renderizadores

Entre no diretório `conf.dispatcher.d/renders`.

Remova todos os arquivos nessa pasta.

Copie o arquivo `conf.dispatcher.d/renders/default_renders.any` do padrão
AEM como uma configuração do Dispatcher do Cloud Service para esse local.

Em cada arquivo do farm, remova qualquer conteúdo da seção `renders` e substitua-o
com:

```
$include "../renders/default_renders.any"
```

### Verifique virtualhosts

Renomeie o diretório `conf.dispatcher.d/vhosts` para `conf.dispatcher.d/virtualhosts` e entre nele.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/virtualhosts` agora contiver um único arquivo, ele deverá ser renomeado para
`virtualhosts.any` e não se esqueça de adaptar as instruções `$include` referentes a isso
nos arquivos farm também.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copie o arquivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` do padrão
AEM como uma configuração do Dispatcher do Cloud Service para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

pela instrução:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Verificar o estado executando o validador

Execute o AEM como um Cloud Service Dispatcher validator no seu diretório, com o subcomando `dispatcher`:

```
$ validator dispatcher .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente.

Se você vir erros relacionados à variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

Para todos os outros erros, consulte a seção de solução de problemas da documentação da ferramenta de validação.

### Teste sua configuração com uma implantação local (requer a instalação do Docker)

Usando o script `docker_run.sh` no AEM como um Cloud Service Dispatcher Tools, você pode testar se
sua configuração não contém nenhum outro erro que apareceria apenas em
implantação:

### Etapa 1: Gerar informações de implantação com o validador

```
validator full -d out .
```

Isso valida a configuração completa e gera informações de implantação em `out`

### Etapa 2: Inicie o Dispatcher em uma imagem do docker com essas informações de implantação

Com o servidor de publicação de AEM em execução no computador macOS, ouvindo na porta 4503,
você pode executar o Dispatcher na frente desse servidor da seguinte maneira:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Isso iniciará o contêiner e exporá o Apache na porta local 8080.

### Usar sua nova configuração do Dispatcher

Parabéns! Se o validador não relatar mais nenhum problema e a variável
o contêiner do docker é iniciado sem falhas ou avisos, você é
pronto para mover sua configuração para um subdiretório `dispatcher/src`
do seu repositório Git.

**Os clientes que estiverem usando a configuração do AMS Dispatcher versão 1 devem entrar em contato com o suporte ao cliente para ajudá-los a migrar da versão 1 para a versão 2, de modo que as instruções acima possam ser seguidas.**
