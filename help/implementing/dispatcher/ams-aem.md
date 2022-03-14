---
title: Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service
description: Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 17%

---

# Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Principais diferenças entre o AMS Dispatcher e o AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

A configuração do Apache e Dispatcher AEM as a Cloud Service é bastante semelhante à do AMS. As principais diferenças são:

* Em AEM as a Cloud Service, algumas diretivas Apache podem não ser usadas (por exemplo, `Listen` ou `LogLevel`)
* Em AEM as a Cloud Service, somente algumas partes da configuração do Dispatcher podem ser colocadas em arquivos de inclusão e sua nomenclatura é importante. Por exemplo, as regras de filtro que você deseja reutilizar em hosts diferentes devem ser colocadas em um arquivo chamado `filters/filters.any`. Consulte a página de referência para obter mais informações.
* Em AEM as a Cloud Service, há validação extra para não permitir regras de filtro gravadas usando `/glob` para evitar problemas de segurança. Since `deny *` será usada em vez de `allow *` (que não pode ser usado), os clientes se beneficiarão com a execução do Dispatcher localmente e com a realização de testes e erros, observando os logs para saber exatamente quais caminhos os filtros do Dispatcher estão bloqueando para que eles possam ser adicionados.

## Diretrizes para migrar a configuração do dispatcher do AMS para o AEM as a Cloud Service

A estrutura de configuração do Dispatcher tem diferenças entre o Managed Services e AEM as a Cloud Service. Apresentado abaixo, é um guia passo a passo sobre como migrar da configuração do AMS Dispatcher versão 2 para AEM as a Cloud Service.

## Como converter um AMS em uma configuração de Dispatcher do AEM as a Cloud Service

A seção a seguir fornece instruções passo a passo sobre como converter uma configuração do AMS. Ele pressupõe que você tenha um arquivo com uma estrutura semelhante à descrita em [Configuração do Dispatcher do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrair o arquivo morto e remover um eventual prefixo

Extraia o arquivo morto para uma pasta e verifique se as subpastas imediatas começam com `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. Caso contrário, mova-os para cima na hierarquia.

### Livrar-se de subpastas e arquivos não utilizados

Remover subpastas `conf` e `conf.modules.d`, bem como a correspondência de arquivos `conf.d/*.conf`.

### Livrar-se de todos os hosts virtuais que não sejam de publicação

Remova qualquer arquivo de host virtual em `conf.d/enabled_vhosts` que `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos de host virtual em `conf.d/available_vhosts` que não estão vinculadas a também podem ser removidas.

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

Remova qualquer arquivo nomeado `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e lembre-se de remover `Include` nos arquivos de host virtual que fazem referência a eles.

If `conf.d/rewrites` agora contém um único arquivo, ele deve ser renomeado para `rewrite.rules` e não se esqueça de adaptar a `Include` instruções referentes a esse arquivo também nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos de host virtual, seu conteúdo deverá ser copiado para o `Include` instrução referenciando-os nos arquivos de host virtual.

### Verificar variáveis

Entre no diretório `conf.d/variables`.

Remova qualquer arquivo nomeado `ams_default.vars` e lembre-se de remover `Include` nos arquivos de host virtual que fazem referência a eles.

If `conf.d/variables` agora contém um único arquivo, ele deve ser renomeado para `custom.vars` e não se esqueça de adaptar a `Include` instruções referentes a esse arquivo também nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos de host virtual, seu conteúdo deverá ser copiado para o `Include` instrução referenciando-os nos arquivos de host virtual.

### Remover listas de permissões

Remover a pasta `conf.d/whitelists` e remover `Include` instruções nos arquivos de host virtual referentes a algum arquivo nessa subpasta.

### Substituir qualquer variável que não esteja mais disponível

Em todos os arquivos de host virtual:

Renomear `PUBLISH_DOCROOT` para `DOCROOT`
Remova as seções que fazem referência às variáveis nomeadas `DISP_ID`, `PUBLISH_FORCE_SSL` ou `PUBLISH_WHITELIST_ENABLED`

### Verificar o estado executando o validador

Execute o validador do Dispatcher no seu diretório, com o `httpd` subcomando:

```
$ validator httpd .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente.

Se você vir diretivas Apache que não estão incluir na lista de permissões, remova-as.

### Livrar-se de todos os farms não publicados

Remova qualquer arquivo do farm em `conf.dispatcher.d/enabled_farms` que `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos farm em `conf.dispatcher.d/available_farms` que não estão vinculadas a também podem ser removidas.

### Renomear arquivos de farm

Todas as explorações agrícolas `conf.d/enabled_farms` deve ser renomeado para corresponder ao padrão `*.farm`, por exemplo, um arquivo farm chamado `customerX_farm.any` deve ser renomeado `customerX.farm`.

### Verificar cache

Entre no diretório `conf.dispatcher.d/cache`.

Remova qualquer arquivo prefixado com `ams_`.

If `conf.dispatcher.d/cache` agora está vazio, copiar o arquivo `conf.dispatcher.d/cache/rules.any`
da configuração padrão do Dispatcher para essa pasta. A configuração padrão do Dispatcher pode ser encontrada na pasta `src` deste SDK. Não se esqueça de adaptar a
`$include` declarações que se referem à `ams_*_cache.any` arquivos de regras nos arquivos farm também.

Em vez disso `conf.dispatcher.d/cache` agora contém um único arquivo com sufixo `_cache.any`, ele deve ser renomeado para `rules.any` e não se esqueça de adaptar a `$include` também as instruções que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para o `$include` declaração referenciando-os nos arquivos do farm.

Remova qualquer arquivo que tenha o sufixo `_invalidate_allowed.any`.

Copiar o arquivo `conf.dispatcher.d/cache/default_invalidate_any` do AEM padrão na configuração do Cloud Dispatcher para esse local.

Em cada arquivo do farm, remova qualquer conteúdo do `cache/allowedClients` e substitua-a por:

```
$include "../cache/default_invalidate.any"
```

### Verificar cabeçalhos do cliente

Entre no diretório `conf.dispatcher.d/clientheaders`.

Remova qualquer arquivo prefixado com `ams_`.

If `conf.dispatcher.d/clientheaders` agora contém um único arquivo com sufixo `_clientheaders.any`, ele deve ser renomeado para `clientheaders.any` e não se esqueça de adaptar a `$include` também as instruções que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para o `$include` declaração referenciando-os nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/clientheaders/default_clientheaders.any` da configuração padrão AEM as a Cloud Service Dispatcher para esse local.

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

If `conf.dispatcher.d/filters` agora contém um único arquivo para o qual ele deve ser renomeado
`filters.any` e não se esqueça de adaptar a `$include` também as instruções que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para o `$include` declaração referenciando-os nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/filters/default_filters.any` da configuração padrão AEM as a Cloud Service Dispatcher para esse local.

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

Copiar o arquivo `conf.dispatcher.d/renders/default_renders.any` da configuração padrão AEM as a Cloud Service Dispatcher para esse local.

Em cada arquivo do farm, remova qualquer conteúdo do `renders` e substitua-a por:

```
$include "../renders/default_renders.any"
```

### Verifique virtualhosts

Renomeie o diretório `conf.dispatcher.d/vhosts` para `conf.dispatcher.d/virtualhosts` e insira-o.

Remova qualquer arquivo prefixado com `ams_`.

If `conf.dispatcher.d/virtualhosts` agora contém um único arquivo para o qual ele deve ser renomeado
`virtualhosts.any` e não se esqueça de adaptar a `$include` também as instruções que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para o `$include` declaração referenciando-os nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` da configuração padrão AEM as a Cloud Service Dispatcher para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

pela instrução:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Verificar o estado executando o validador

Execute o AEM validador as a Cloud Service do Dispatcher no seu diretório, com o `dispatcher` subcomando:

```
$ validator dispatcher .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente.

Se você vir erros relacionados à variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

Para todos os outros erros, consulte a seção de solução de problemas da documentação da ferramenta de validação.

### Teste sua configuração com uma implantação local (requer a instalação do Docker)

Uso do script `docker_run.sh` nas AEM ferramentas as a Cloud Service do Dispatcher, você pode testar se a sua configuração não contém nenhum outro erro que apareceria apenas na implantação:

### Etapa 1: Gerar informações de implantação com o validador

```
validator full -d out .
```

Isso valida a configuração completa e gera informações de implantação em `out`

### Etapa 2: Inicie o Dispatcher em uma imagem do docker com essas informações de implantação

Com seu servidor de publicação de AEM em execução no computador macOS, ouvindo na porta 4503, você pode executar o Dispatcher na frente desse servidor da seguinte maneira:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Isso iniciará o contêiner e exporá o Apache na porta local 8080.

### Usar sua nova configuração do Dispatcher

Parabéns! Se o validador não relatar mais nenhum problema e o contêiner do docker for inicializado sem falhas ou avisos, você estará pronto para mover sua configuração para um `dispatcher/src` subdiretório do seu repositório Git.

**Os clientes que estiverem usando a configuração do AMS Dispatcher versão 1 devem entrar em contato com o suporte ao cliente para ajudá-los a migrar da versão 1 para a versão 2, de modo que as instruções acima possam ser seguidas.**
