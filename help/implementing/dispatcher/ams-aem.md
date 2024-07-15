---
title: Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service
description: Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# Migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Principais diferenças entre o AMS Dispatcher e o AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

A configuração do Apache e do Dispatcher no AEM as a Cloud Service é bastante semelhante à do AMS. As principais diferenças são:

* No AEM as a Cloud Service, algumas diretivas do Apache não podem ser usadas (por exemplo, `Listen` ou `LogLevel`)
* No AEM as a Cloud Service, somente algumas partes da configuração do Dispatcher podem ser colocadas em arquivos de inclusão e seus nomes são importantes. Por exemplo, as regras de filtro que você deseja reutilizar em diferentes hosts devem ser colocadas em um arquivo chamado `filters/filters.any`. Consulte a página de referência do para obter mais informações.
* No AEM as a Cloud Service há validação extra para não permitir regras de filtro gravadas com o uso de `/glob` para evitar problemas de segurança. Como o `deny *` é usado em vez do `allow *` (que não pode ser usado), os clientes se beneficiam da execução local do Dispatcher e da realização de tentativas e erros, examinando os logs para saber exatamente quais caminhos os filtros do Dispatcher estão bloqueando para que eles possam ser adicionados.
* No AEM as a Cloud Service, é altamente recomendável [optar por usar o modo de origem flexível da configuração do dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug), por exemplo, usar pipelines de configuração no nível da Web ou ter mais flexibilidade no número e na estrutura de arquivos de configuração.

## Diretrizes para migrar a configuração do dispatcher do AMS para o AEM as a Cloud Service

A estrutura de configuração do Dispatcher tem diferenças entre o Managed Services e o AEM as a Cloud Service. Apresentado abaixo, é apresentado um guia passo a passo sobre como migrar da configuração 2 do AMS Dispatcher para o AEM as a Cloud Service.

## Como converter um AMS em uma configuração de Dispatcher do AEM as a Cloud Service

A seção a seguir fornece instruções passo a passo sobre como converter uma configuração do AMS. Ele pressupõe
que você tem um arquivo morto com uma estrutura semelhante à descrita em [configuração do Cloud Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrair o arquivo morto e remover um eventual prefixo

Extraia o arquivo morto para uma pasta e verifique se as subpastas imediatas começam com `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. Caso contrário, mova-os para cima na hierarquia.

### Livrar-se de subpastas e arquivos não utilizados

Remover subpastas `conf` e `conf.modules.d` e arquivos correspondentes a `conf.d/*.conf`.

### Livrar-se de todos os hosts virtuais que não sejam de publicação

Remova qualquer arquivo de host virtual em `conf.d/enabled_vhosts` que tenha `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos de host virtual em `conf.d/available_vhosts` que não estão
vinculado ao também pode ser removido.

### Remova ou comente seções de host virtual que não se refiram à porta 80

Se você ainda tiver seções nos arquivos de host virtual que se referem exclusivamente a outras portas além da porta 80, por exemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```

remova-as ou comente-as. As instruções nessas seções não serão processadas, mas se você
mantenha-os por perto, você ainda pode acabar editando-os sem efeito, o que é confuso.

### Verificar regravações

Entre no diretório `conf.d/rewrites`.

Remova qualquer arquivo chamado `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e lembre-se de:
remova as instruções `Include` nos arquivos de host virtual que fazem referência a elas.

Se `conf.d/rewrites` agora contiver um único arquivo, ele deverá ser renomeado para `rewrite.rules` e não
esqueça de adaptar também as instruções `Include` que fazem referência a esse arquivo nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser
copiado para a instrução `Include` que faz referência a eles nos arquivos de host virtual.

### Verificar variáveis

Entre no diretório `conf.d/variables`.

Remova qualquer arquivo chamado `ams_default.vars` e lembre-se de remover as instruções `Include` na pasta virtual
arquivos de host referentes a eles.

Se `conf.d/variables` agora contiver um único arquivo, ele deverá ser renomeado para `custom.vars` e não
esqueça de adaptar também as instruções `Include` que fazem referência a esse arquivo nos arquivos de host virtual.

Se, no entanto, a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser
copiado para a instrução `Include` que faz referência a eles nos arquivos de host virtual.

### Remover listas de permissões

Remova a pasta `conf.d/whitelists` e remova as instruções `Include` nos arquivos de host virtual referentes a
algum arquivo nessa subpasta.

### Substituir qualquer variável que não esteja mais disponível

Em todos os arquivos de host virtual:

Renomear `PUBLISH_DOCROOT` para `DOCROOT`
Remover seções que fazem referência às variáveis chamadas `DISP_ID`, `PUBLISH_FORCE_SSL` ou `PUBLISH_WHITELIST_ENABLED`

### Verificar o estado executando o validador

Execute o validador do Dispatcher em seu diretório, com o subcomando `httpd`:

```
$ validator httpd .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente
arquivos.

Incluir na lista de permissões Se você vir diretivas do Apache que não são, remova-as.

### Livrar-se de todos os farms não publicados

Remova qualquer arquivo de farm em `conf.dispatcher.d/enabled_farms` que tenha `author`, `unhealthy`, `health`,
`lc` ou `flush` em seu nome. Todos os arquivos do farm em `conf.dispatcher.d/available_farms` que não estão
vinculado ao também pode ser removido.

### Renomear arquivos do farm

Todos os farms em `conf.dispatcher.d/enabled_farms` devem ser renomeados para corresponder ao padrão `*.farm`, por exemplo, um
o arquivo de farm chamado `customerX_farm.any` deve ser renomeado `customerX.farm`.

### Verificar cache

Entre no diretório `conf.dispatcher.d/cache`.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/cache` estiver vazio agora, copie o arquivo `conf.dispatcher.d/cache/rules.any`
da configuração padrão do Dispatcher para essa pasta. O Dispatcher padrão
A configuração do pode ser encontrada na pasta `src` deste SDK. Não se esqueça de adaptar o
`$include` instruções referentes aos arquivos de regras `ams_*_cache.any` nos arquivos de farm
também.

Se, em vez disso, `conf.dispatcher.d/cache` agora contiver um único arquivo com o sufixo `_cache.any`,
ele deve ser renomeado para `rules.any` e não se esqueça de adaptar as instruções `$include`
que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Remova qualquer arquivo que tenha o sufixo `_invalidate_allowed.any`.

Copiar o arquivo `conf.dispatcher.d/cache/default_invalidate_any` do padrão
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
que fazem referência a esse arquivo nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/clientheaders/default_clientheaders.any` do padrão
AEM as a Cloud Service Dispatcher para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de clienteheader com a seguinte aparência:

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
`filters.any` e não se esqueça de adaptar as instruções `$include` que fazem referência a isso
nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/filters/default_filters.any` do padrão
AEM as a Cloud Service Dispatcher para esse local.

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

Copiar o arquivo `conf.dispatcher.d/renders/default_renders.any` do padrão
AEM as a Cloud Service Dispatcher para esse local.

Em cada arquivo do farm, remova qualquer conteúdo da seção `renders` e substitua-o
com:

```
$include "../renders/default_renders.any"
```

### Verificar virtualhosts

Renomeie o diretório `conf.dispatcher.d/vhosts` como `conf.dispatcher.d/virtualhosts` e entre nele.

Remova qualquer arquivo prefixado com `ams_`.

Se `conf.dispatcher.d/virtualhosts` agora contiver um único arquivo, ele deverá ser renomeado para
`virtualhosts.any` e não se esqueça de adaptar as instruções `$include` que fazem referência a isso
nos arquivos do farm.

Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo
deve ser copiado para a instrução `$include` que faz referência a eles nos arquivos do farm.

Copiar o arquivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` do padrão
AEM as a Cloud Service Dispatcher para esse local.

Em cada arquivo do farm, substitua qualquer instrução include de filtro com a seguinte aparência:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

pela instrução:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Verificar o estado executando o validador

Execute o AEM as a Cloud Service Dispatcher validator em seu diretório, com o subcomando `dispatcher`:

```
$ validator dispatcher .
```

Se você encontrar erros sobre a falta de arquivos de inclusão, verifique se os renomeou corretamente
arquivos.

Se você vir erros relacionados à variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

Para todos os outros erros, consulte a seção Solução de problemas do
documentação da ferramenta validadora.

### Testar sua configuração com uma implantação local (requer instalação do Docker)

Usando o script `docker_run.sh` nas Ferramentas do AEM as a Cloud Service Dispatcher, você pode testar isso
sua configuração não contém nenhum outro erro que apareceria apenas no
implantação:

### Etapa 1: Gerar informações de implantação com o validador

```
validator full -d out .
```

Isso valida a configuração completa e gera informações de implantação em `out`

### Etapa 2: iniciar o Dispatcher em uma imagem do docker com essas informações de implantação

Com o servidor de publicação AEM em execução no computador macOS, ouvindo na porta 4503,
você pode executar iniciar o Dispatcher na frente desse servidor da seguinte maneira:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Isso iniciará o contêiner e exporá o Apache na porta local 8080.

### Usar sua nova configuração do Dispatcher

Parabéns! Se o validador não relatar mais nenhum problema e a variável
contêiner docker é inicializado sem falhas ou avisos, você está
pronto para mover sua configuração para um subdiretório `dispatcher/src`
do seu repositório Git.

**Os clientes que usam a configuração 1 do AMS Dispatcher devem entrar em contato com o suporte ao cliente para ajudá-los a migrar da versão 1 para a versão 2, de modo que as instruções acima possam ser seguidas.**
