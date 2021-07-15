---
title: Validação e depuração usando ferramentas do Dispatcher
description: Validação e depuração usando ferramentas do Dispatcher
feature: Dispatcher
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 1%

---

# Validação e depuração usando ferramentas do Dispatcher {#Dispatcher-in-the-cloud}

## Introdução {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obter mais informações sobre o Dispatcher na nuvem e como baixar as Ferramentas do Dispatcher, consulte o [Dispatcher na página Cloud](/help/implementing/dispatcher/disp-overview.md) . Se a configuração do dispatcher estiver no modo herdado, consulte a [documentação do modo herdado](/help/implementing/dispatcher/validation-debug-legacy.md).

As seções a seguir descrevem a estrutura do arquivo do modo flexível, a validação local, a depuração e a migração do modo herdado para o modo flexível.

Este artigo parte do princípio que a configuração do dispatcher do seu projeto inclui o arquivo `opt-in/USE_SOURCES_DIRECTLY`, o que faz com que o SDK e o tempo de execução validem e implantem a configuração de uma maneira aprimorada em comparação ao modo herdado, removendo limitações ao redor do número e do tamanho dos arquivos.

Dessa forma, se a configuração do dispatcher não incluir o arquivo mencionado acima, é **altamente recomendado** que você migre do modo herdado para o modo flexível, conforme descrito na seção [Migração do modo herdado para o modo flexível](#migrating).

## Estrutura do arquivo {#flexible-mode-file-structure}

A estrutura da subpasta do Dispatcher do projeto é a seguinte:

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

Abaixo está uma explicação de arquivos notáveis que podem ser modificados:

**Arquivos personalizáveis**

Os arquivos a seguir são personalizáveis e serão transferidos para sua instância do Cloud na implantação:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Você pode ter um ou mais desses arquivos. Eles contêm `<VirtualHost>` entradas que correspondem aos nomes de host e permitem que o Apache manipule cada tráfego de domínio com regras diferentes. Os arquivos são criados no diretório `available_vhosts` e ativados com um link simbólico no diretório `enabled_vhosts`. Nos arquivos `.vhost`, outros arquivos como regravações e variáveis serão incluídos.

* `conf.d/rewrites/rewrite.rules`

Este arquivo é incluído de dentro de seus arquivos `.vhost`. Ele tem um conjunto de regras de regravação para `mod_rewrite`.

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

* `opt-in/USE_SOURCES_DIRECTLY`

Esse arquivo habilita uma configuração de dispatcher mais flexível e remove limitações anteriores sobre o número e o tamanho dos arquivos. Isso também faz com que o SDK e o tempo de execução validem e implantem a configuração de uma maneira aprimorada.

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

## Módulos Apache Suportados {#apache-modules}

Consulte [Módulos Apache Suportados](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validação local {#local-validation-flexible-mode}

>[!NOTE]
>As seções abaixo incluem comandos usando as versões Mac ou Linux do SDK, mas o SDK do Windows também pode ser usado de maneira semelhante.

Use o script `validate.sh` conforme mostrado abaixo:

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
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

O script tem as três fases a seguir:

1. Ele executa o validador. Se a configuração não for válida, o script falhará.
2. Ele executa o comando `httpd -t` para testar se a sintaxe está correta, de forma que o apache httpd possa ser iniciado. Se bem-sucedida, a configuração deve estar pronta para implantação.
3. Verifica se o subconjunto dos arquivos de configuração do SDK do Dispatcher, que devem ser imutáveis conforme descrito na seção [File structure](##flexible-mode-file-structure), não foi modificado.

Durante uma implantação do Cloud Manager, a verificação da sintaxe `httpd -t` também será executada e todos os erros serão incluídos no log `Build Images step failure` do Cloud Manager.

### Fase 1 {#first-phase}

Se uma diretiva não for incluir na lista de permissões, a ferramenta registrará um erro e retornará um código de saída diferente de zero. Além disso, ele verifica todos os arquivos com o padrão `conf.dispatcher.d/enabled_farms/*.farm` e verifica se:

* Não existe uma regra de filtro que use o permite via `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obter mais detalhes.
* Nenhum recurso administrativo é exposto. Por exemplo, acesso a caminhos como `/crx/de or /system/console`.

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

Observe que a primeira fase também pode ser **executar separadamente**, em vez do script wrapper `validate.sh`.

Quando executado em seu artefato maven ou subdiretório `dispatcher/src`, ele reportará falhas de validação:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

No Windows, o validador do dispatcher faz distinção entre maiúsculas e minúsculas. Dessa forma, poderá ocorrer uma falha na validação da configuração se você não respeitar a capitalização do caminho em que a configuração reside, por exemplo:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite esse erro copiando e colando o caminho do Windows Explorer e, em seguida, no prompt de comando usando um comando `cd` nesse caminho.

### Fase 2 {#second-phase}

Essa fase verifica a sintaxe do apache iniciando o Docker em uma imagem. O Docker deve ser instalado localmente, mas observe que não é necessário que o AEM esteja em execução.

>[!NOTE]
>Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Isso é um pré-requisito para executar e depurar o Dispatcher em um computador local.

Essa fase também pode ser executada independentemente por meio de `bin/docker_run.sh src/dispatcher host.internal.docker:4503 8080`.

Durante uma implantação do Cloud Manager, a verificação da sintaxe `httpd -t` também será executada e todos os erros serão incluídos no log de falha da etapa Imagens de criação do Cloud Manager.

### Fase 3 {#third-phase}

Se houver uma falha nessa fase, isso implica que o Adobe alterou um ou mais arquivos imutáveis e você deve substituir os arquivos imutáveis correspondentes pela nova versão entregue no diretório `src` do SDK. A amostra de log abaixo ilustra esse problema:

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

Essa fase também pode ser executada independentemente por meio de `bin/docker_immutability_check.sh src/dispatcher`.

## Depuração da configuração do Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Observe que você pode executar o apache dispatcher localmente usando `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Como dito anteriormente, o Docker deve ser instalado localmente e não é necessário que AEM esteja em execução. Os usuários do Windows precisam usar o Windows 10 Professional ou outras distribuições compatíveis com o Docker. Isso é um pré-requisito para executar e depurar o Dispatcher em um computador local.

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

## Visualização da configuração do Dispatcher em uso pelo seu contêiner Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

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

## Migração do modo herdado para o modo flexível {#migrating}

Com a versão 2021.7.0 do Cloud Manager, os novos programas do Cloud Manager geram estruturas de projeto maven com [AEM arquétipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) ou superior, que inclui o arquivo **opt-in/USE_SOURCES_DIRECTLY**. Isso remove as limitações anteriores do [modo herdado](/help/implementing/dispatcher/validation-debug-legacy.md) sobre o número e o tamanho dos arquivos, fazendo também com que o SDK e o tempo de execução validem e implantem a configuração de uma maneira aprimorada. Se a configuração do dispatcher não tiver esse arquivo, é altamente recomendável migrar. Use as seguintes etapas para garantir uma transição segura:

1. **Teste local.** Usando as ferramentas mais recentes do dispatcher SDK, adicione a pasta e o arquivo  `opt-in/USE_SOURCES_DIRECTLY`. Siga as instruções de &quot;validação local&quot; neste artigo para testar se o dispatcher funciona localmente.
2. **Teste de desenvolvimento em nuvem:**
   * Confirme o arquivo `opt-in/USE_SOURCES_DIRECTLY` em uma ramificação git implantada pelo pipeline de não produção em um ambiente de desenvolvimento do Cloud.
   * Use o Cloud Manager para implantar em um ambiente de desenvolvimento do Cloud.
   * Teste completamente. É importante validar se a configuração do apache e do dispatcher se comporta conforme o esperado antes de implantar alterações em ambientes superiores. Verifique todo o comportamento relacionado à sua configuração personalizada! Registre um tíquete de suporte ao cliente se você achar que a configuração do dispatcher implantada não reflete a configuração personalizada.
3. **Implantar na produção:**
   * Confirme o arquivo `opt-in/USE_SOURCES_DIRECTLY` em uma ramificação git implantada pelo pipeline de produção nos ambientes de preparo e produção do Cloud.
   * Use o Cloud Manager para implantar no armazenamento temporário.
   * Teste completamente. É importante validar se a configuração do apache e do dispatcher se comporta conforme o esperado antes de implantar alterações em ambientes superiores. Verifique todo o comportamento relacionado à sua configuração personalizada! Registre um tíquete de suporte ao cliente se você achar que a configuração do dispatcher implantada não reflete a configuração personalizada.
   * Use o Cloud Manager para continuar a implantação na produção.
