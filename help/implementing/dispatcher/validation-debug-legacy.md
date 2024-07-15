---
title: Validação e depuração usando ferramentas do Dispatcher (herdadas)
description: Validação e depuração usando ferramentas do Dispatcher (herdadas)
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2337'
ht-degree: 1%

---

# Validação e depuração usando ferramentas do Dispatcher (herdadas)  {#Dispatcher-tools-legacy}

## Introdução {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obter mais informações sobre o Dispatcher na nuvem e como baixar as ferramentas do Dispatcher, consulte a página [Dispatcher na nuvem](/help/implementing/dispatcher/disp-overview.md).

As seções a seguir descrevem a estrutura do arquivo do modo herdado, a validação local, a depuração e como migrar do modo herdado para o [modo flexível](/help/implementing/dispatcher/validation-debug.md).

Este artigo presume que a configuração do Dispatcher do seu projeto não inclui o arquivo opt-in/USE_SOURCES_DIRECTLY. Como resultado, há limitações no número e no tamanho dos arquivos, como:

* um único arquivo de regravação que deve ser usado em vez de arquivos específicos do site.
* a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1 MB.

A partir da versão 2021.7.0 do Cloud Manager, novos programas do Cloud Manager geram estruturas de projeto maven com AEM arquétipo 28 e superior, que inclui o arquivo mencionado anteriormente.

É **altamente recomendável** migrar do modo herdado para o modo flexível, conforme descrito na seção de migração [Migrando do modo herdado para o modo flexível](#migrating-flexible). Usar o modo flexível também faz com que o SDK e o tempo de execução validem e implantem a configuração de maneira aprimorada.

## Estrutura de arquivo {#legacy-mode-file-structure}

A estrutura da subpasta Dispatcher do projeto (no modo herdado) é a seguinte:

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

Veja abaixo uma explicação dos arquivos notáveis que podem ser modificados:

**Arquivos Personalizáveis**

Os seguintes arquivos são personalizáveis e são transferidos para sua instância da Cloud na implantação:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Você pode ter um ou mais desses arquivos. Eles contêm `<VirtualHost>` entradas que correspondem a nomes de host e permitem que o Apache manipule cada tráfego de domínio com regras diferentes. Os arquivos são criados no diretório `available_vhosts` e habilitados com um link simbólico no diretório `enabled_vhosts`. A partir dos arquivos `.vhost`, outros arquivos, como regravações e variáveis, são incluídos.

* `conf.d/rewrites/rewrite.rules`

Este arquivo está incluído dentro de seus arquivos do `.vhost`. Ele tem um conjunto de regras de regravação para `mod_rewrite`.

>[!NOTE]
>
>Atualmente, um único arquivo de regravação deve ser usado, em vez de arquivos específicos do site. Como regra, a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1 MB.

* `conf.d/variables/custom.vars`

Este arquivo está incluído dentro de seus arquivos do `.vhost`. Você pode adicionar definições para variáveis do Apache neste local.

* `conf.d/variables/global.vars`

Este arquivo está incluído dentro do arquivo `dispatcher_vhost.conf`. Você pode alterar o Dispatcher e regravar o nível de log nesse arquivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Você pode ter um ou mais desses arquivos, que contêm farms para corresponder a nomes de host e permitem que o módulo Dispatcher manipule cada farm com regras diferentes. Os arquivos são criados no diretório `available_farms` e habilitados com um link simbólico no diretório `enabled_farms`. A partir dos arquivos `.farm`, outros arquivos, como filtros, regras de cache e outros, são incluídos.

* `conf.dispatcher.d/cache/rules.any`

Este arquivo está incluído dentro de seus arquivos do `.farm`. Especifica as preferências de armazenamento em cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este arquivo está incluído dentro de seus arquivos do `.farm`. Especifica quais cabeçalhos de solicitação devem ser encaminhados para o backend.

* `conf.dispatcher.d/filters/filters.any`

Este arquivo está incluído dentro de seus arquivos do `.farm`. Ele tem um conjunto de regras que alteram qual tráfego deve ser filtrado e não chega ao back-end.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este arquivo está incluído dentro de seus arquivos do `.farm`. Ela tem uma lista de nomes de host ou caminhos URI a serem correspondidos pela correspondência glob. Essa correspondência determina qual backend usar para atender a uma solicitação.

Os arquivos acima fazem referência aos arquivos de configuração imutáveis listados abaixo. As alterações nos arquivos imutáveis não são processadas pelos Dispatchers em ambientes na Nuvem.

**Arquivos de Configuração Imutáveis**

Esses arquivos fazem parte da estrutura básica e aplicam padrões e práticas recomendadas. Os arquivos são considerados imutáveis porque modificá-los ou excluí-los localmente não tem impacto na implantação, pois não são transferidos para a instância da Cloud.

Recomenda-se que os arquivos acima façam referência aos arquivos imutáveis listados abaixo, seguidos de quaisquer instruções ou substituições adicionais. Quando a configuração do Dispatcher é implantada em um ambiente de nuvem, a versão mais recente dos arquivos imutáveis é usada, independentemente da versão usada no desenvolvimento local.

* `conf.d/available_vhosts/default.vhost`

Contém uma amostra de host virtual. Para seu próprio host virtual, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_vhosts` e crie um link simbólico para sua cópia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte da estrutura básica, usada para ilustrar como os hosts virtuais e as variáveis globais são incluídos.

* `conf.d/rewrites/default_rewrite.rules`

Regras padrão para regravação adequadas para um projeto padrão. Se precisar de personalização, edite `rewrite.rules`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas forem necessárias.

* `conf.dispatcher.d/available_farms/default.farm`

Contém um exemplo de farm do Dispatcher. Para seu próprio farm, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_farms` e crie um link simbólico para sua cópia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte da estrutura base é gerada na inicialização. É **necessário** incluir este arquivo em cada farm definido, na seção `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Regras de cache padrão adequadas para um projeto padrão. Se precisar de personalização, modifique `conf.dispatcher.d/cache/rules.any`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas forem necessárias.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Cabeçalhos de solicitação padrão para encaminhar para o backend, adequado para um projeto padrão. Se precisar de personalização, modifique `clientheaders.any`. Na personalização, você ainda pode incluir os cabeçalhos de solicitação padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/dispatcher.any`

Parte da estrutura base, usada para ilustrar como seus farms da Dispatcher são incluídos.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros padrão adequados para um projeto padrão. Se precisar de personalização, modifique `filters.any`. Na personalização, ainda é possível incluir os filtros padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/renders/default_renders.any`

Parte da estrutura base, esse arquivo é gerado na inicialização. É **necessário** incluir este arquivo em cada farm definido, na seção `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

O recurso de curinga de host padrão é adequado para um projeto padrão. Se precisar de personalização, modifique `virtualhosts.any`. Na sua personalização, você não deve incluir o recurso de curinga do host padrão, pois ele corresponde a **a cada** solicitação recebida.

## Módulos Apache compatíveis {#apache-modules}

Consulte [Módulos Apache Suportados](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validação local {#local-validation-legacy-mode}

>[!NOTE]
>As seções abaixo incluem comandos que usam as versões Mac ou Linux® do SDK, mas o SDK do Windows também pode ser usado de maneira semelhante.

Use o script `validate.sh` como mostrado abaixo:

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
2. Ele executa o comando `httpd -t` para testar se a sintaxe está correta, de modo que o Apache httpd possa ser iniciado. Se for bem-sucedida, a configuração deve estar pronta para implantação.
3. Verifica se o subconjunto dos arquivos de configuração do SDK do Dispatcher, que devem ser imutáveis, conforme descrito na [seção Estrutura de arquivos](##legacy-mode-file-structure), não foi editado. Essa verificação é uma novidade e foi introduzida com o SDK do AEM versão v2021.1.4738, que também inclui as Ferramentas do Dispatcher versão 2.0.36. Antes dessa atualização, os clientes podiam ter presumido incorretamente que qualquer modificação local do SDK desses arquivos imutáveis também seria aplicada ao ambiente da nuvem.

Durante uma implantação do Cloud Manager, a verificação de sintaxe `httpd -t` também é executada e todos os erros são incluídos no log `Build Images step failure` do Cloud Manager.

### Fase 1 {#first-phase}

Incluir na lista de permissões Se uma diretiva não for alterada, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Além disso, ele verifica ainda mais todos os arquivos com o padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe nenhuma regra de filtro que use permissões via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes.
* Nenhum recurso de administrador está exposto. Por exemplo, acesso a caminhos como `/crx/de or /system/console`.

Incluir na lista de permissões A ferramenta de validação relata apenas o uso proibido de diretivas Apache que não foram alteradas. Ele não relata problemas sintáticos ou semânticos com a configuração do Apache, pois essas informações só estão disponíveis para módulos Apache em um ambiente de execução.

Abaixo estão apresentadas técnicas de solução de problemas para depurar erros comuns de validação gerados pela ferramenta:

**Não é possível localizar uma subpasta `conf.dispatcher.d` no arquivo morto**

Seu arquivo deve conter as pastas `conf.d` e `conf.dispatcher.d`. Observe que você **não deve**
usar o prefixo `etc/httpd` em seu arquivo.

**Não é possível localizar nenhum farm em`conf.dispatcher.d/enabled_farms`**

Seus farms ativados devem estar na subpasta mencionada.

**O arquivo incluído (...) deve ser nomeado como: ...**

Há duas seções na configuração do farm que **deve** incluir uma
arquivo específico: `/renders` e `/allowedClients` na seção `/cache`. Esses
As seções devem ter a seguinte aparência:

```
/renders {
    $include "../renders/default_renders.any"
}
```

E:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**Arquivo incluído em local desconhecido: ...**

Há quatro seções na configuração do farm onde você pode incluir seu próprio arquivo: `/clientheaders`, `filters`, `/rules` na seção `/cache` e `/virtualhosts`. Os arquivos incluídos devem ser nomeados da seguinte maneira:

| Seção | Incluir nome do arquivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Como alternativa, você pode incluir a versão **padrão** desses arquivos, cujos nomes são anexados com a palavra `default_`, por exemplo, `../filters/default_filters.any`.

**Incluir instrução em (...), fora de qualquer local conhecido: ...**

Além das seis seções mencionadas nos parágrafos acima, você não está autorizado a
para usar a instrução `$include`, por exemplo, o seguinte geraria este erro:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Os clientes/renderizadores permitidos não estão incluídos de: ...**

Este erro é gerado quando você não especifica um &quot;include&quot; para `/renders` e `/allowedClients` na seção `/cache`. Consulte a
**o arquivo incluído (...) deve ser nomeado como: ...** seção para obter mais informações.

**O filtro não deve usar o padrão glob para permitir solicitações**

Não é seguro permitir solicitações com uma regra de estilo `/glob`, que corresponde à linha de solicitação completa, por exemplo,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrução destina-se a permitir solicitações para `css` arquivos, mas também permite solicitações para **qualquer** recurso seguido pela sequência de consulta `?a=.css`. Portanto, é proibido usar esses filtros (consulte também CVE-2016-0957).

**O arquivo incluído (...) não corresponde a nenhum arquivo conhecido**

Há dois tipos de arquivos na configuração do host virtual Apache que podem ser especificados como inclusões: regravações e variáveis.
Os arquivos incluídos devem ser nomeados da seguinte maneira:

| Tipo | Incluir nome do arquivo |
|-----------|---------------------------------|
| Substitui | `conf.d/rewrites/rewrite.rules` |
| Variáveis | `conf.d/variables/custom.vars` |

>[!TIP]
>
>Para poder incluir mais arquivos de uma maneira muito menos limitada, talvez você queira mudar para o modo de configuração flexível do Dispatcher. Consulte [Validação e depuração usando ferramentas do Dispatcher](/help/implementing/dispatcher/validation-debug.md) para obter mais detalhes sobre o modo flexível.

Como alternativa, você pode incluir a versão **padrão** das regras de regravação, cujo nome é `conf.d/rewrites/default_rewrite.rules`.
Observe que não há versão padrão dos arquivos de variáveis.

**Layout de configuração obsoleto detectado, habilitando o modo de compatibilidade**

Esta mensagem indica que sua configuração tem o layout obsoleto versão 1, contendo um
Configuração do Apache e arquivos com `ams_` prefixos. Embora essa configuração ainda seja suportada para versões anteriores,
compatibilidade, você deve mudar para o novo layout.

A primeira fase também pode ser **executada separadamente**, em vez do script wrapper `validate.sh`.

Quando executado em relação ao artefato maven ou ao subdiretório `dispatcher/src`, ele relata falhas de validação:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

No Windows, o validador do Dispatcher diferencia maiúsculas de minúsculas. Dessa forma, poderá ocorrer uma falha ao validar a configuração se você não respeitar as letras maiúsculas do caminho no qual a configuração reside, por exemplo:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite este erro copiando e colando o caminho do Windows Explorer e, em seguida, no prompt de comando usando um comando `cd` nesse caminho.

### Fase 2 {#second-phase}

Essa fase verifica a sintaxe do Apache iniciando o Docker em uma imagem. O Docker deve ser instalado localmente, mas observe que não é necessário que o AEM esteja em execução.

>[!NOTE]
>Os usuários do Windows devem usar o Windows 10 Professional ou outras distribuições que suportem o Docker. Esse pré-requisito é necessário para executar e depurar o Dispatcher em um computador local.

Esta fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório &quot;out&quot; necessário para o próximo comando `bin/docker_run.sh out host.docker.internal:4503 8080`.

Durante uma implantação do Cloud Manager, a verificação de sintaxe `httpd -t` é executada e todos os erros são incluídos no log de falha da etapa Imagens do Cloud Manager Build.

### Fase 3 {#third-phase}

Se houver uma falha nessa fase, isso implica que o Adobe alterou um ou mais arquivos imutáveis. Nesse caso, você deve substituir os arquivos imutáveis correspondentes pela nova versão entregue no diretório `src` do SDK. O exemplo de log a seguir ilustra esse problema:

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

Esta fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório &quot;out&quot;, necessário para o próximo comando `bin/docker_immutability_check.sh out`.

## Depuração da configuração do Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Você pode executar o Apache Dispatcher localmente usando o `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Conforme dito anteriormente, o Docker deve ser instalado localmente e não é necessário que o AEM esteja em execução. Os usuários do Windows devem usar o Windows 10 Professional ou outras distribuições que suportem o Docker. Esse pré-requisito é necessário para executar e depurar o Dispatcher em um computador local.

A estratégia a seguir pode ser usada para aumentar a saída de log do módulo Dispatcher e ver os resultados da avaliação de `RewriteRule` em ambientes locais e de nuvem.

Os níveis de log desses módulos são definidos pelas variáveis `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Eles podem ser definidos no arquivo `conf.d/variables/global.vars`. A sua parte relevante é a seguinte:

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

Ao executar o Dispatcher localmente, os logs são impressos diretamente na saída do terminal. Na maioria das vezes, você deseja que esses registros estejam em DEBUG, o que pode ser feito passando o nível de Depuração como um parâmetro ao executar o Docker. Por exemplo: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Os logs para ambientes de nuvem são expostos por meio do serviço de log disponível no Cloud Manager.

## Diferentes configurações do Dispatcher por ambiente {#different-dispatcher-configurations-per-environment}

Atualmente, a mesma configuração do Dispatcher é aplicada a todos os ambientes no AEM as a Cloud Service. O tempo de execução tem uma variável de ambiente `ENVIRONMENT_TYPE` que contém o modo de execução atual (dev, stag ou prod) e uma definição. A definição pode ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` ou `ENVIRONMENT_PROD`. Na configuração do Apache, a variável pode ser usada diretamente em uma expressão. Como alternativa, a definição pode ser usada para criar lógica:

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

Na configuração do Dispatcher, a mesma variável de ambiente está disponível. Se mais lógica for necessária, defina as variáveis conforme mostrado no exemplo acima e use-as na seção de configuração do Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Ao testar sua configuração localmente, você pode simular tipos de ambientes diferentes passando a variável `DISP_RUN_MODE` diretamente para o script `docker_run.sh`:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

O modo de execução padrão ao não transmitir um valor para DISP_RUN_MODE é &quot;dev&quot;.
Para obter uma lista completa das opções e variáveis disponíveis, execute o script `docker_run.sh` sem argumentos.

## Exibição da configuração do Dispatcher em uso pelo seu contêiner Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Com configurações específicas do ambiente, pode ser difícil determinar a aparência da configuração real do Dispatcher. Depois de iniciar o contêiner do docker com `docker_run.sh`, ele pode ser descarregado da seguinte maneira:

* Determine a ID do contêiner de docker em uso:

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

Com a versão 2021.7.0 do Cloud Manager, novos programas do Cloud Manager geram estruturas de projeto maven com AEM arquétipo 28 ou superior, que inclui o arquivo **opt-in/USE_SOURCES_DIRECTLY**. As limitações anteriores do modo herdado em relação ao número e ao tamanho dos arquivos são removidas, fazendo com que o SDK e o tempo de execução validem e implantem a configuração de maneira aprimorada. Se a configuração do Dispatcher não tiver esse arquivo, é altamente recomendável migrar. Use os métodos descritos na página [modo flexível](/help/implementing/dispatcher/validation-debug.md#migrating).
