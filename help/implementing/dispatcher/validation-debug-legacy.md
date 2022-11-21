---
title: Validação e depuração usando ferramentas do Dispatcher (herdadas)
description: Validação e depuração usando ferramentas do Dispatcher (herdadas)
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
source-git-commit: 687323031ecfd179a1875033411b8398a3d1d74b
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 1%

---

# Validação e depuração usando ferramentas do Dispatcher (herdadas)  {#Dispatcher-tools-legacy}

## Introdução {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obter mais informações sobre o Dispatcher na nuvem e como baixar as Ferramentas do Dispatcher, consulte a [Dispatcher na nuvem](/help/implementing/dispatcher/disp-overview.md) página.

As seções a seguir descrevem a estrutura do arquivo do modo herdado, a validação local, a depuração e como migrar do modo herdado para o modo herdado [modo flexível](/help/implementing/dispatcher/validation-debug.md).

Este artigo parte do princípio que a configuração do dispatcher do seu projeto não inclui o arquivo opt-in/USE_SOURCES_DIRECTLY. Como resultado, ele tem limitações sobre o número e o tamanho de arquivos, como:

* um único arquivo de reescrita que deve ser usado em vez de arquivos específicos do site.
* a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1MB.

A partir da versão 2021.7.0 do Cloud Manager, os novos programas do Cloud Manager geram estruturas de projeto maven com AEM arquétipo 28 e superior, que inclui o arquivo acima.

É **altamente recomendado** que você migre do modo herdado para o modo flexível, conforme descrito na seção migração [Migração do modo herdado para o modo flexível](#migrating-flexible). Usar o modo flexível também faz com que o SDK e o tempo de execução validem e implantem a configuração de uma maneira aprimorada.

## Estrutura do arquivo {#legacy-mode-file-structure}

A estrutura da subpasta do Dispatcher do projeto (no modo herdado) é a seguinte:

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
    │   ├── marketing_query_parameters.any
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

Você pode ter um ou mais desses arquivos. Eles contêm `<VirtualHost>` entradas que correspondem aos nomes de host e permitem que o Apache gerencie cada tráfego de domínio com regras diferentes. Os arquivos são criados na `available_vhosts` e habilitado com um link simbólico no `enabled_vhosts` diretório. No `.vhost` arquivos, outros arquivos como regravações e variáveis serão incluídos.

* `conf.d/rewrites/rewrite.rules`

Este arquivo está incluído de dentro de seu `.vhost` arquivos. Ele tem um conjunto de regras de reescrita para `mod_rewrite`.

>[!NOTE]
>
>Atualmente, um único arquivo de reescrita deve ser usado em vez de arquivos específicos do site. Como regra, a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1MB.

* `conf.d/variables/custom.vars`

Este arquivo está incluído de dentro de seu `.vhost` arquivos. Você pode adicionar definições para variáveis do Apache neste local.

* `conf.d/variables/global.vars`

Este arquivo é incluído de dentro da variável `dispatcher_vhost.conf` arquivo. Você pode alterar seu Dispatcher e reescrever o nível de log neste arquivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Você pode ter um ou mais desses arquivos e eles contêm farms para corresponder aos nomes de host e permitir que o módulo Dispatcher manipule cada farm com regras diferentes. Os arquivos são criados na `available_farms` e habilitado com um link simbólico no `enabled_farms` diretório. No `.farm` arquivos, outros arquivos como filtros, regras de cache e outros serão incluídos.

* `conf.dispatcher.d/cache/rules.any`

Este arquivo está incluído de dentro de seu `.farm` arquivos. Especifica preferências de armazenamento em cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este arquivo está incluído de dentro de seu `.farm` arquivos. Especifica quais cabeçalhos de solicitação devem ser encaminhados ao backend.

* `conf.dispatcher.d/filters/filters.any`

Este arquivo está incluído de dentro de seu `.farm` arquivos. Ele tem um conjunto de regras que alteram o tráfego que deve ser filtrado e não para o back-end.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este arquivo está incluído de dentro de seu `.farm` arquivos. Ela tem uma lista de nomes de host ou caminhos de URI a serem correspondidos pela correspondência glob. Isso determina qual back-end usar para servir uma solicitação.

Os arquivos acima fazem referência aos arquivos de configuração imutáveis listados abaixo. As alterações nos arquivos imutáveis não serão processadas pelo Dispatchers em ambientes Cloud.

**Arquivos de configuração imutáveis**

Esses arquivos fazem parte da estrutura básica e impõem padrões e práticas recomendadas. Os arquivos são considerados imutáveis porque modificá-los ou excluí-los localmente não terá impacto na implantação, pois não serão transferidos para a instância do Cloud.

É recomendável que os arquivos acima façam referência aos arquivos imutáveis listados abaixo, seguidos de quaisquer instruções ou substituições adicionais. Quando a configuração do Dispatcher é implantada em um ambiente de nuvem, a versão mais recente dos arquivos imutáveis será usada, independentemente da versão usada no desenvolvimento local.

* `conf.d/available_vhosts/default.vhost`

Contém um host virtual de amostra. Para seu próprio host virtual, crie uma cópia desse arquivo, personalize-o, vá para `conf.d/enabled_vhosts` e crie um link simbólico para sua cópia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte da estrutura base, usada para ilustrar como os hosts virtuais e as variáveis globais são incluídos.

* `conf.d/rewrites/default_rewrite.rules`

Regras padrão de reescrita adequadas para um projeto padrão. Se você precisar de personalização, modifique `rewrite.rules`. Na personalização, ainda é possível incluir as regras padrão primeiro, se elas atenderem às suas necessidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contém uma amostra de farm do Dispatcher. Para o seu próprio farm, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_farms` e crie um link simbólico para sua cópia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte da estrutura base é gerada na inicialização. Você está **obrigatório** para incluir esse arquivo em cada farm definido, na variável `cache/allowedClients` seção.

* `conf.dispatcher.d/cache/default_rules.any`

Regras de cache padrão adequadas para um projeto padrão. Se você precisar de personalização, modifique `conf.dispatcher.d/cache/rules.any`. Na personalização, ainda é possível incluir as regras padrão primeiro, se elas atenderem às suas necessidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Cabeçalhos de solicitação padrão para encaminhar ao backend, adequados para um projeto padrão. Se você precisar de personalização, modifique `clientheaders.any`. Na personalização, você ainda pode incluir os cabeçalhos de solicitação padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/dispatcher.any`

Parte da estrutura base, usada para ilustrar como os farms do Dispatcher são incluídos.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros padrão adequados para um projeto padrão. Se você precisar de personalização, modifique `filters.any`. Na personalização, você ainda pode incluir os filtros padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/renders/default_renders.any`

Parte da estrutura base, esse arquivo é gerado na inicialização. Você está **obrigatório** para incluir esse arquivo em cada farm definido, na variável `renders` seção.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globalização de host padrão adequada para um projeto padrão. Se você precisar de personalização, modifique `virtualhosts.any`. Na personalização, você não deve incluir a globalização de host padrão, pois ela corresponde **each** solicitação recebida.

## Módulos Apache Suportados {#apache-modules}

Consulte [Módulos Apache Suportados](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validação local {#local-validation-legacy-mode}

>[!NOTE]
>As seções abaixo incluem comandos usando as versões Mac ou Linux do SDK, mas o SDK do Windows também pode ser usado de maneira semelhante.

Use o `validate.sh` como mostrado abaixo:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv found in deployment folder: /tmp/dispatcher_validation_1625150390 - using files listed there
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

...

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

O script faz o seguinte:

1. Ele executa o validador. Se a configuração não for válida, o script falhará.
2. Ele executa a variável `httpd -t` para testar se a sintaxe está correta, de modo que o apache httpd possa ser iniciado. Se bem-sucedida, a configuração deve estar pronta para implantação.
3. Verifica se o subconjunto dos arquivos de configuração do SDK do Dispatcher, que devem ser imutáveis, conforme descrito no [Seção Estrutura do arquivo](##legacy-mode-file-structure), não foi modificada. Esta é uma nova verificação, introduzida com AEM versão v2021.1.4738 do SDK, que também inclui a versão 2.0.36 das Ferramentas do Dispatcher. Antes dessa atualização, os clientes podem ter presumido incorretamente que quaisquer modificações do SDK local desses arquivos imutáveis também seriam aplicadas ao ambiente do Cloud.

Durante uma implantação do Cloud Manager, a variável `httpd -t` a verificação de sintaxe também será executada e todos os erros serão incluídos no Cloud Manager `Build Images step failure` log.

### Fase 1 {#first-phase}

Se uma diretiva não for incluir na lista de permissões, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Além disso, ele verifica ainda mais todos os arquivos com padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe uma regra de filtro que use permite via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes.
* Nenhum recurso administrativo é exposto. Por exemplo, acesso a caminhos como `/crx/de or /system/console`.

Observe que a ferramenta de validação relata apenas o uso proibido das diretivas Apache que não foram incluir na lista de permissões. Ele não relata problemas sintáticos ou semânticos com a configuração do Apache, pois essas informações só estão disponíveis para os módulos Apache em um ambiente em execução.

Apresentamos abaixo as técnicas de solução de problemas para depurar erros comuns de validação que são gerados pela ferramenta:

**não é possível localizar um `conf.dispatcher.d` subpasta no arquivo**

Seu arquivo deve conter as pastas `conf.d` e `conf.dispatcher.d`. Observe que você **não deve**
usar o prefixo `etc/httpd` em seu arquivo.

**não é possível localizar nenhum farm em`conf.dispatcher.d/enabled_farms`**

Os farms ativados devem estar localizados na subpasta mencionada.

**arquivo incluído (..) deve ser nomeado como: ...**

Há duas seções na configuração do farm que **must** incluir um arquivo específico: `/renders` e `/allowedClients` no `/cache` seção. Essas seções devem ter a seguinte aparência:

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

Há quatro seções na configuração do farm em que você pode incluir seu próprio arquivo: `/clientheaders`, `filters`, `/rules` em `/cache` seção e `/virtualhosts`. Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Seção | Incluir nome de arquivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Como alternativa, você pode incluir a variável **default** versão desses arquivos, cujos nomes são anexados à palavra `default_`, por exemplo, `../filters/default_filters.any`.

**inclua instrução em (..), fora de qualquer local conhecido: ...**

Além das seis seções mencionadas nos parágrafos acima, você não tem permissão para usar o `$include` , por exemplo, o seguinte geraria esse erro:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**clientes/renderizadores permitidos não são incluídos de: ...**

Esse erro é gerado quando você não especifica uma inclusão para `/renders` e `/allowedClients` no `/cache` seção. Consulte a
**arquivo incluído (..) deve ser nomeado como: ...** para obter mais informações.

**o filtro não deve usar o padrão glob para permitir solicitações**

Não é seguro permitir solicitações com um `/glob` regra de estilo, que é correspondida com a linha de solicitação completa, por exemplo,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrução destina-se a permitir pedidos para `css` arquivos, mas também permite que solicitações **any** recurso seguido pela sequência de consulta `?a=.css`. Por conseguinte, é proibido utilizar esses filtros (ver também CVE-2016-0957).

**o arquivo incluído (...) não corresponde a nenhum arquivo conhecido**

Há dois tipos de arquivos na configuração de host virtual do Apache que podem ser especificados como inclui: regravações e variáveis.
Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Tipo | Incluir nome de arquivo |
|-----------|---------------------------------|
| Regravações | `conf.d/rewrites/rewrite.rules` |
| Variáveis | `conf.d/variables/custom.vars` |

>[!TIP]
>
>Para incluir mais arquivos de maneira muito menos limitada, você pode querer alternar para o modo de configuração flexível do dispatcher. Consulte o documento [Validação e depuração usando ferramentas do Dispatcher](/help/implementing/dispatcher/validation-debug.md) para obter mais detalhes sobre o modo flexível.

Como alternativa, você pode incluir a variável **default** versão das regras de regravação, cujo nome é `conf.d/rewrites/default_rewrite.rules`.
Observe que não há uma versão padrão dos arquivos de variáveis.

**Foi detectado um layout de configuração obsoleto, habilitando o modo de compatibilidade**

Essa mensagem indica que sua configuração tem o layout obsoleto da versão 1, contendo uma configuração completa do Apache e arquivos com `ams_` prefixos. Embora isso ainda seja compatível com versões anteriores, você deve alternar para o novo layout.

Observe que a primeira fase também pode ser **executar separadamente**, em vez do invólucro `validate.sh` script.

Quando correr contra seu artefato maven ou seu `dispatcher/src` subdiretório, reportará falhas de validação:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

No Windows, o validador do dispatcher faz distinção entre maiúsculas e minúsculas. Dessa forma, poderá ocorrer uma falha na validação da configuração se você não respeitar a capitalização do caminho em que a configuração reside, por exemplo:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite este erro copiando e colando o caminho do Windows Explorer e, em seguida, no prompt de comando usando um `cd` nesse caminho.

### Fase 2 {#second-phase}

Essa fase verifica a sintaxe do apache iniciando o Docker em uma imagem. O Docker deve ser instalado localmente, mas observe que não é necessário que o AEM esteja em execução.

>[!NOTE]
>Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Isso é um pré-requisito para executar e depurar o Dispatcher em um computador local.

Essa fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório de saída, necessário para o próximo comando `bin/docker_run.sh out host.docker.internal:4503 8080`.

Durante uma implantação do Cloud Manager, a variável `httpd -t` a verificação de sintaxe também será executada e todos os erros serão incluídos no log de falha da etapa Criar imagens do Cloud Manager.

### Fase 3 {#third-phase}

Se houver uma falha nessa fase, isso implica que o Adobe alterou um ou mais arquivos imutáveis e você deve substituir os arquivos imutáveis correspondentes pela nova versão entregue na `src` diretório do SDK. A amostra de log abaixo ilustra esse problema:

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

Essa fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório de saída, necessário para o próximo comando `bin/docker_immutability_check.sh out`.

## Depuração da configuração do Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Observe que você pode executar o apache dispatcher localmente usando `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Como dito anteriormente, o Docker deve ser instalado localmente e não é necessário que AEM esteja em execução. Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Isso é um pré-requisito para executar e depurar o Dispatcher em um computador local.

A estratégia a seguir pode ser usada para aumentar a saída de log do módulo Dispatcher e ver os resultados da `RewriteRule` avaliação em ambientes locais e de nuvem.

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

Atualmente, a mesma configuração do Dispatcher é aplicada a todos os ambientes AEM as a Cloud Service. O tempo de execução terá uma variável de ambiente `ENVIRONMENT_TYPE` que contém o modo de execução atual (dev, stage ou prod), bem como um definido. A definição pode ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` ou `ENVIRONMENT_PROD`. Na configuração do Apache, a variável pode ser usada diretamente em uma expressão. Como alternativa, a definição pode ser usada para criar lógica:

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

Ao testar sua configuração localmente, você pode simular diferentes tipos de ambiente transmitindo a variável `DISP_RUN_MODE` para `docker_run.sh` script diretamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

O modo de execução padrão ao não transmitir um valor para DISP_RUN_MODE é &quot;dev&quot;.
Para obter uma lista completa de opções e variáveis disponíveis, execute o script `docker_run.sh` sem argumentos.

## Visualização da configuração do Dispatcher em uso pelo seu contêiner Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Com configurações específicas do ambiente, pode ser difícil determinar a aparência real da configuração do Dispatcher. Depois de ter iniciado o contêiner do docker com `docker_run.sh` Pode ser objeto de dumping do seguinte modo:

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

## Migração do modo herdado para o modo flexível {#migrating-flexible}

Com a versão 2021.7.0 do Cloud Manager, os novos programas do Cloud Manager geram estruturas de projeto maven com AEM arquétipo 28 ou superior, que inclui o arquivo **opt-in/USE_SOURCES_DIRECTLY**. Isso remove as limitações anteriores do modo herdado em torno do número e do tamanho dos arquivos, fazendo também com que o SDK e o tempo de execução validem e implantem a configuração de maneira aprimorada. Se a configuração do dispatcher não tiver esse arquivo, é altamente recomendável migrar. Use os métodos descritos no [modo flexível](/help/implementing/dispatcher/validation-debug.md#migrating) página.
