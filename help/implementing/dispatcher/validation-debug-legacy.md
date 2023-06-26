---
title: Validação e depuração usando ferramentas do Dispatcher (herdado)
description: Validação e depuração usando ferramentas do Dispatcher (herdado)
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 1%

---

# Validação e depuração usando ferramentas do Dispatcher (herdado)  {#Dispatcher-tools-legacy}

## Introdução {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obter mais informações sobre o Dispatcher na nuvem e como baixar as Ferramentas do Dispatcher, consulte o [Dispatcher na nuvem](/help/implementing/dispatcher/disp-overview.md) página.

As seções a seguir descrevem a estrutura do arquivo do modo herdado, a validação local, a depuração e como migrar do modo herdado para o [modo flexível](/help/implementing/dispatcher/validation-debug.md).

Este artigo presume que a configuração do dispatcher do projeto não inclui o arquivo opt-in/USE_SOURCES_DIRECTLY. Como resultado, há limitações no número e no tamanho dos arquivos, como:

* um único arquivo de regravação que deve ser usado em vez de arquivos específicos do site.
* a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1 MB.

A partir da versão 2021.7.0 do Cloud Manager, novos programas do Cloud Manager geram estruturas de projeto maven com arquétipo AEM 28 e superior, que inclui o arquivo mencionado acima.

É necessário **altamente recomendado** que você migre do modo herdado para o modo flexível, conforme descrito na seção migração [Migração do modo herdado para o modo flexível](#migrating-flexible). Usar o modo flexível também faz com que o SDK e o tempo de execução validem e implantem a configuração de maneira aprimorada.

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

**Arquivos personalizáveis**

Os seguintes arquivos são personalizáveis e serão transferidos para a sua instância da Cloud na implantação:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Você pode ter um ou mais desses arquivos. Eles contêm `<VirtualHost>` entradas que correspondem a nomes de host e permitem que o Apache manipule cada tráfego de domínio com regras diferentes. Os arquivos são criados no `available_vhosts` e habilitado com um link simbólico na variável `enabled_vhosts` diretório. No `.vhost` arquivos, outros arquivos como regravações e variáveis são incluídos.

* `conf.d/rewrites/rewrite.rules`

Esse arquivo é incluído de dentro do seu `.vhost` arquivos. Ele tem um conjunto de regras de regravação para `mod_rewrite`.

>[!NOTE]
>
>Atualmente, um único arquivo de regravação deve ser usado, em vez de arquivos específicos do site. Como regra, a soma do conteúdo dos arquivos personalizáveis deve ser inferior a 1 MB.

* `conf.d/variables/custom.vars`

Esse arquivo é incluído de dentro do seu `.vhost` arquivos. Você pode adicionar definições para variáveis do Apache neste local.

* `conf.d/variables/global.vars`

Esse arquivo está incluído de dentro do `dispatcher_vhost.conf` arquivo. Você pode alterar o Dispatcher e regravar o nível de log nesse arquivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Você pode ter um ou mais desses arquivos, que contêm farms para corresponder a nomes de host e permitem que o módulo Dispatcher manipule cada farm com regras diferentes. Os arquivos são criados no `available_farms` e habilitado com um link simbólico na variável `enabled_farms` diretório. No `.farm` arquivos, outros arquivos como filtros, regras de cache e outros são incluídos.

* `conf.dispatcher.d/cache/rules.any`

Esse arquivo é incluído de dentro do seu `.farm` arquivos. Especifica as preferências de armazenamento em cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Esse arquivo é incluído de dentro do seu `.farm` arquivos. Especifica quais cabeçalhos de solicitação devem ser encaminhados para o backend.

* `conf.dispatcher.d/filters/filters.any`

Esse arquivo é incluído de dentro do seu `.farm` arquivos. Ele tem um conjunto de regras que alteram qual tráfego deve ser filtrado e não chega ao back-end.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Esse arquivo é incluído de dentro do seu `.farm` arquivos. Ela tem uma lista de nomes de host ou caminhos URI a serem correspondidos pela correspondência glob. Isso determina qual back-end usar para atender a uma solicitação.

Os arquivos acima fazem referência aos arquivos de configuração imutáveis listados abaixo. As alterações nos arquivos imutáveis não serão processadas pelos Dispatchers em ambientes na Nuvem.

**Arquivos de configuração imutáveis**

Esses arquivos fazem parte da estrutura básica e aplicam padrões e práticas recomendadas. Os arquivos são considerados imutáveis porque modificá-los ou excluí-los localmente não terá impacto na implantação, pois não serão transferidos para a instância da Nuvem.

Recomenda-se que os arquivos acima façam referência aos arquivos imutáveis listados abaixo, seguidos de quaisquer instruções ou substituições adicionais. Quando a configuração do Dispatcher é implantada em um ambiente de nuvem, a versão mais recente dos arquivos imutáveis é usada, independentemente da versão usada no desenvolvimento local.

* `conf.d/available_vhosts/default.vhost`

Contém uma amostra de host virtual. Para seu próprio host virtual, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_vhosts` e criar um link simbólico para sua cópia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte da estrutura básica, usada para ilustrar como os hosts virtuais e as variáveis globais são incluídos.

* `conf.d/rewrites/default_rewrite.rules`

Regras de regravação padrão adequadas para um projeto padrão. Se precisar de personalização, modifique `rewrite.rules`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas forem necessárias.

* `conf.dispatcher.d/available_farms/default.farm`

Contém um exemplo de farm do Dispatcher. Para seu próprio farm, crie uma cópia deste arquivo, personalize-o, vá para `conf.d/enabled_farms` e criar um link simbólico para sua cópia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte da estrutura base é gerada na inicialização. Você está **obrigatório** para incluir esse arquivo em cada farm definido, na variável `cache/allowedClients` seção.

* `conf.dispatcher.d/cache/default_rules.any`

Regras de cache padrão adequadas para um projeto padrão. Se precisar de personalização, modifique `conf.dispatcher.d/cache/rules.any`. Na personalização, você ainda pode incluir as regras padrão primeiro, se elas forem necessárias.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Cabeçalhos de solicitação padrão para encaminhar para o backend, adequado para um projeto padrão. Se precisar de personalização, modifique `clientheaders.any`. Na personalização, você ainda pode incluir os cabeçalhos de solicitação padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/dispatcher.any`

Parte da estrutura base, usada para ilustrar como seus farms do Dispatcher são incluídos.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros padrão adequados para um projeto padrão. Se precisar de personalização, modifique `filters.any`. Na personalização, ainda é possível incluir os filtros padrão primeiro, se eles atenderem às suas necessidades.

* `conf.dispatcher.d/renders/default_renders.any`

Parte da estrutura base, esse arquivo é gerado na inicialização. Você está **obrigatório** para incluir esse arquivo em cada farm definido, na variável `renders` seção.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

O recurso de curinga de host padrão é adequado para um projeto padrão. Se precisar de personalização, modifique `virtualhosts.any`. Na personalização, não inclua o recurso de curinga do host padrão, pois ele corresponde **a cada** solicitação de entrada.

## Módulos Apache compatíveis {#apache-modules}

Consulte [Módulos compatíveis do Apache](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validação local {#local-validation-legacy-mode}

>[!NOTE]
>As seções abaixo incluem comandos que usam as versões Mac ou Linux do SDK, mas o SDK do Windows também pode ser usado de maneira semelhante.

Use o `validate.sh` conforme mostrado abaixo:

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
2. Ele executa o `httpd -t` para testar se a sintaxe está correta, de modo que o apache httpd possa ser iniciado. Se for bem-sucedida, a configuração deve estar pronta para implantação.
3. Verifica se o subconjunto dos arquivos de configuração do SDK do Dispatcher, que devem ser imutáveis, conforme descrito na seção [Seção de estrutura de arquivo](##legacy-mode-file-structure), não foi modificado. Esta é uma nova verificação, introduzida com o SDK AEM versão v2021.1.4738 que também inclui as Ferramentas do Dispatcher versão 2.0.36. Antes dessa atualização, os clientes podiam ter presumido incorretamente que qualquer modificação local do SDK desses arquivos imutáveis também seria aplicada ao ambiente da nuvem.

Durante uma implantação do Cloud Manager, a variável `httpd -t` a verificação de sintaxe também é executada e todos os erros são incluídos no Cloud Manager `Build Images step failure` registro.

### Fase 1 {#first-phase}

Incluir na lista de permissões Se uma diretiva não for alterada, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Além disso, ele verifica ainda mais todos os arquivos com padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe nenhuma regra de filtro que use permissões via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes.
* Nenhum recurso de administrador está exposto. Por exemplo, o acesso a caminhos como `/crx/de or /system/console`.

Incluir na lista de permissões Observe que a ferramenta de validação relata apenas o uso proibido de diretivas Apache que não foram migradas. Ele não relata problemas sintáticos ou semânticos com a configuração do Apache, pois essas informações só estão disponíveis para módulos Apache em um ambiente de execução.

Abaixo estão apresentadas técnicas de solução de problemas para depurar erros comuns de validação gerados pela ferramenta:

**não é possível localizar um `conf.dispatcher.d` subpasta no arquivo**

Seu arquivo deve conter as pastas `conf.d` e `conf.dispatcher.d`. Observe que você **não deve**
usar o prefixo `etc/httpd` em seu arquivo.

**não foi possível encontrar farm em`conf.dispatcher.d/enabled_farms`**

Seus farms ativados devem estar localizados na subpasta mencionada.

**arquivo incluído (...) deve ser nomeado: ...**

Há duas seções na configuração do farm que **deve** incluir um arquivo específico: `/renders` e `/allowedClients` no `/cache` seção. Essas seções devem ter a seguinte aparência:

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

**arquivo incluído em local desconhecido: ...**

Há quatro seções na configuração do farm, nas quais você pode incluir seu próprio arquivo: `/clientheaders`, `filters`, `/rules` in `/cache` seção e `/virtualhosts`. Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Seção | Incluir nome do arquivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Como alternativa, inclua a variável **padrão** versão desses arquivos, cujos nomes são anexados à palavra `default_`, por exemplo, `../filters/default_filters.any`.

**incluir instrução em (...), fora de qualquer local conhecido: ...**

Além das seis seções mencionadas nos parágrafos acima, você não está autorizado a usar o `$include` Por exemplo, o seguinte geraria esse erro:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**os clientes/renderizadores permitidos não estão incluídos de: ...**

Esse erro é gerado quando você não especifica uma inclusão para `/renders` e `/allowedClients` no `/cache` seção. Consulte a
**arquivo incluído (...) deve ser nomeado: ...** para obter mais informações.

**o filtro não deve usar o padrão glob para permitir solicitações**

Não é seguro permitir solicitações com um `/glob` regra de estilo, que corresponde à linha de solicitação completa, por exemplo,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta declaração destina-se a permitir `css` arquivos, mas também permite que solicitações para **qualquer** recurso seguido pela sequência de consulta `?a=.css`. Portanto, é proibido usar esses filtros (consulte também CVE-2016-0957).

**arquivo incluído (...) não corresponde a nenhum arquivo conhecido**

Há dois tipos de arquivos na configuração do host virtual Apache que podem ser especificados como inclusões: regravações e variáveis.
Os arquivos incluídos precisam ser nomeados da seguinte maneira:

| Tipo | Incluir nome do arquivo |
|-----------|---------------------------------|
| Substitui | `conf.d/rewrites/rewrite.rules` |
| Variáveis | `conf.d/variables/custom.vars` |

>[!TIP]
>
>Para poder incluir mais arquivos de maneira muito menos limitada, talvez você queira alternar para o modo de configuração flexível do dispatcher. Consulte o documento [Validação e depuração usando ferramentas do Dispatcher](/help/implementing/dispatcher/validation-debug.md) para obter mais detalhes sobre o modo flexível.

Como alternativa, inclua a variável **padrão** versão das regras de regravação, cujo nome é `conf.d/rewrites/default_rewrite.rules`.
Observe que não há versão padrão dos arquivos de variáveis.

**Layout de configuração obsoleto detectado, ativando o modo de compatibilidade**

Esta mensagem indica que sua configuração tem o layout obsoleto versão 1, contendo uma configuração completa do Apache e arquivos com `ams_` prefixos. Embora isso ainda seja suportado para compatibilidade com versões anteriores, você deve alternar para o novo layout.

Observe que a primeira fase também pode ser **executar separadamente**, em vez do invólucro `validate.sh` script.

Quando executado contra seu artefato maven ou seu `dispatcher/src` subdiretório, ele relatará falhas de validação:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

No Windows, o validador do dispatcher diferencia maiúsculas de minúsculas. Dessa forma, poderá ocorrer uma falha ao validar a configuração se você não respeitar as letras maiúsculas do caminho no qual a configuração reside, por exemplo:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite este erro copiando e colando o caminho do Windows Explorer e, em seguida, no prompt de comando usando uma `cd` nesse caminho.

### Fase 2 {#second-phase}

Essa fase verifica a sintaxe do Apache iniciando o Docker em uma imagem. O Docker deve ser instalado localmente, mas observe que não é necessário que o AEM esteja em execução.

>[!NOTE]
>Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições que suportem o Docker. Esse é um pré-requisito para executar e depurar o Dispatcher em um computador local.

Essa fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório out, necessário para o comando next `bin/docker_run.sh out host.docker.internal:4503 8080`.

Durante uma implantação do Cloud Manager, a variável `httpd -t` a verificação de sintaxe é executada e todos os erros são incluídos no log de falha da etapa Imagens de compilação do Cloud Manager.

### Fase 3 {#third-phase}

Se houver uma falha nessa fase, isso implica que o Adobe alterou um ou mais arquivos imutáveis e você deve substituir os arquivos imutáveis correspondentes pela nova versão entregue no `src` do SDK. A amostra de log abaixo ilustra esse problema:

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

Essa fase também pode ser executada independentemente por meio de `validator full -d out src/dispatcher`, que gera um diretório out, necessário para o comando next `bin/docker_immutability_check.sh out`.

## Depuração da configuração do Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Observe que é possível executar o Apache Dispatcher localmente usando `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Conforme dito anteriormente, o Docker deve ser instalado localmente e não é necessário que o AEM esteja em execução. Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições que suportem o Docker. Esse é um pré-requisito para executar e depurar o Dispatcher em um computador local.

A estratégia a seguir pode ser usada para aumentar a saída de log do módulo Dispatcher e ver os resultados do `RewriteRule` avaliação em ambientes locais e de nuvem.

Os níveis de log desses módulos são definidos pelas variáveis `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Elas podem ser definidas no arquivo `conf.d/variables/global.vars`. A sua parte relevante é a seguinte:

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

Os logs de ambientes da nuvem são expostos por meio do serviço de log disponível no Cloud Manager.

## Diferentes configurações do Dispatcher por ambiente {#different-dispatcher-configurations-per-environment}

Atualmente, a mesma configuração do Dispatcher é aplicada a todos os ambientes as a Cloud Service AEM. O tempo de execução terá uma variável de ambiente `ENVIRONMENT_TYPE` que contém o modo de execução atual (dev, stage ou prod), bem como uma definição. A definição pode ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` ou `ENVIRONMENT_PROD`. Na configuração do Apache, a variável pode ser usada diretamente em uma expressão. Como alternativa, a definição pode ser usada para criar lógica:

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

Na configuração do Dispatcher, a mesma variável de ambiente está disponível. Se mais lógica for necessária, defina as variáveis conforme mostrado no exemplo acima e use-as na seção Configuração do Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Ao testar sua configuração localmente, você pode simular diferentes tipos de ambiente transmitindo a variável `DISP_RUN_MODE` para o `docker_run.sh` script diretamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

O modo de execução padrão ao não transmitir um valor para DISP_RUN_MODE é &quot;dev&quot;.
Para obter uma lista completa das opções e variáveis disponíveis, execute o script `docker_run.sh` sem argumentos.

## Exibição da configuração do Dispatcher em uso pelo contêiner do Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Com configurações específicas de ambiente, pode ser difícil determinar como é a configuração real do Dispatcher. Depois de iniciar o contêiner do docker com `docker_run.sh` pode ser objeto de dumping do seguinte modo:

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

Com a versão 2021.7.0 do Cloud Manager, novos programas do Cloud Manager geram estruturas de projeto maven com arquétipo AEM 28 ou superior, que inclui o arquivo **opt-in/USE_SOURCES_DIRECTLY**. Isso remove as limitações anteriores do modo herdado em relação ao número e ao tamanho dos arquivos, fazendo com que o SDK e o tempo de execução validem e implantem a configuração de maneira aprimorada. Se a configuração do dispatcher não tiver esse arquivo, é altamente recomendável migrar. Use os métodos descritos na seção [modo flexível](/help/implementing/dispatcher/validation-debug.md#migrating) página.
