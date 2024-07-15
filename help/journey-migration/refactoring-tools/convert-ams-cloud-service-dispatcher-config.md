---
title: Converter um AMS em uma configuração de Dispatcher do Adobe Experience Manager as a Cloud Service
description: Converter um AMS em uma configuração de Dispatcher do Adobe Experience Manager as a Cloud Service
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 37%

---


# Converter um AMS em uma configuração de Dispatcher do Adobe Experience Manager (AEM) as a Cloud Service

## Introdução {#introduction}

Esta seção fornece instruções passo a passo sobre como converter uma configuração do AMS.

>[!NOTE]
>Ele pressupõe que você tenha um arquivo com uma estrutura semelhante à descrita em [Gerenciar suas configurações de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/dispatcher-configurations.html).

## Etapas para converter um AMS em uma configuração de Dispatcher do AEM as a Cloud Service

1. **Extrair o arquivo morto e remover um eventual prefixo**

   Extraia o arquivo morto para uma pasta e verifique se as subpastas imediatas começam com conf, conf.d, conf.dispatcher.d e conf.modules.d. Caso contrário, mova-os para cima na hierarquia.

1. **Livrar-se de subpastas e arquivos não utilizados**

   Remova as subpastas conf e conf.modules.d, e os arquivos conf.d/*.conf correspondentes.

1. **Livrar-se de todos os hosts virtuais que não sejam de publicação**

1. **Remova qualquer arquivo de host virtual**

   Em conf.d/enabled_vhosts que tenha author, unhealthy, health, lc ou flush no nome. Todos os arquivos de host virtual em conf.d/available_vhosts que não estejam vinculados também podem ser removidos.

1. Remova ou comente seções de host virtual que não se refiram à porta 80

   Se você ainda tiver seções nos arquivos de host virtual que se referem exclusivamente a outras portas além da porta 80, por exemplo,

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
remova-as ou comente-as. As instruções nessas seções não são processadas, mas, se você as mantiver por perto, ainda poderá editá-las sem efeito, o que é confuso.

1. **Verificar regravações**

   * Entre no diretório conf.d/rewrites.

   * Remova qualquer arquivo chamado base_rewrite.rules e xforwarded_forcessl_rewrite.rules e lembre-se de remover as instruções Include nos arquivos do host virtual que fazem referência a elas.

   * Se o arquivo conf.d/rewrites agora contiver um único arquivo, ele deverá ser renomeado para rewrite.rules, e não se esqueça de adaptar também as instruções Include referentes a esse arquivo nos arquivos de host virtual.

   * Se, no entanto, a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a instrução Include que fazem referência a eles nos arquivos do host virtual.

1. **Verificar variáveis**

   1. Entre no diretório conf.d/variables.

   1. Remova qualquer arquivo denominado ams_default.vars e lembre-se de remover as instruções Include nos arquivos do host virtual que fazem referência a elas.

   1. Se o arquivo conf.d/variables agora contiver um único arquivo, ele deverá ser renomeado para custom.vars, e não se esqueça de adaptar também as instruções Include referentes a esse arquivo nos arquivos de host virtual.

   1. Se, no entanto, a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a instrução Include que fazem referência a eles nos arquivos do host virtual.

1. **Remover listas de permissões**

   Remova a pasta conf.d/whitelists e remova as instruções Include nos arquivos de host virtual referentes a algum arquivo nessa subpasta.

1. **Substituir qualquer variável que não esteja mais disponível**

   Em todos os arquivos de host virtual:

   Renomeie PUBLISH_DOCROOT para DOCROOT
Remova as seções que fazem referência às variáveis denominadas DISP_ID, PUBLISH_FORCE_SSL ou PUBLISH_WHITELIST_ENABLED

1. **Verificar o estado executando o validador**

   Execute o validador do Dispatcher em seu diretório, com o subcomando httpd:

   `$ validator httpd`
Se você encontrar erros sobre a falta de arquivos &quot;include&quot;, verifique se os renomeou corretamente.

   Se você vir diretivas Apache que não estão na lista de permissões, remova-as.

1. **Livrar-se de todos os farms não publicados**

   Remova qualquer arquivo de farm em conf.dispatcher.d/enabled_farms que tenha author, unhealthy, health, lc ou flush no nome. Todos os arquivos do farm em conf.dispatcher.d/available_farms que não estejam vinculados também podem ser removidos.

1. **Renomear arquivos de farm**

   Todos os farms em conf.dispatcher.d/enabled_farms devem ser renomeados para corresponder ao padrão *.farm. Por exemplo, renomeie `customerX_farm.any` como `customerX.farm`.

1. **Verificar cache**

   Entre no diretório conf.dispatcher.d/cache.

   Remova qualquer arquivo prefixado com `ams_`.

   Se conf.dispatcher.d/cache agora estiver vazio, copie o arquivo `conf.dispatcher.d/cache/rules.any` da configuração padrão do Dispatcher para essa pasta. A configuração padrão do Dispatcher pode ser encontrada na pasta src desse SDK. Não se esqueça de adaptar também as instruções $include referentes aos arquivos de regras `ams_*_cache.any` nos arquivos de farm.

   Se, em vez disso, conf.dispatcher.d/cache agora contiver um único arquivo com o sufixo `_cache.any`, ele deverá ser renomeado para `rules.any`. Lembre-se de adaptar também as instruções $include referentes a esse arquivo nos arquivos do farm.

   Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a instrução $include que fazem referência a eles nos arquivos do farm.

   Remova qualquer arquivo que tenha o sufixo `_invalidate_allowed.any`.

   Copie o arquivo conf.dispatcher.d/cache/default_invalidate_any da configuração padrão do Dispatcher para esse local.

   Em cada arquivo do farm, remova qualquer conteúdo da seção cache/allowedClients e substitua-o por:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Verificar cabeçalhos do cliente**

   Entre no diretório conf.dispatcher.d/clientheaders.

   Remova qualquer arquivo prefixado com `ams_`.

   Se conf.dispatcher.d/clientheaders contiver um único arquivo com o sufixo `_clientheaders.any`, renomeie-o para `clientheaders.any`. Lembre-se de adaptar também as instruções $include referentes a esse arquivo nos arquivos do farm.

   Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a instrução $include que fazem referência a eles nos arquivos do farm.

   Copie o arquivo `conf.dispatcher/clientheaders/default_clientheaders.any` da configuração padrão do Dispatcher para esse local.

   Em cada arquivo do farm, substitua qualquer instrução &quot;include&quot; `clientheader` que apareça da seguinte maneira:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   pela instrução:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Verificar filtro**

   * Entre no diretório conf.dispatcher.d/filters.

   * Remova qualquer arquivo prefixado com `ams_`.

   * Se conf.dispatcher.d/filters agora contiver um único arquivo, renomeie-o para `filters.any`. Lembre-se de adaptar também as instruções $include referentes a esse arquivo nos arquivos do farm.

   * Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a instrução $include que fazem referência a eles nos arquivos do farm.

   * Copie o arquivo `conf.dispatcher/filters/default_filters.any` da configuração padrão do Dispatcher para esse local.

   * Em cada arquivo do farm, substitua qualquer instrução &quot;include&quot; de filtro que apareça da seguinte maneira:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
pela instrução:

     `$include "../filters/default_filters.any"`

1. **Verificar renderizadores**

   * Entre no diretório conf.dispatcher.d/renders.

   * Remova todos os arquivos nessa pasta.

   * Copie o arquivo `conf.dispatcher.d/renders/default_renders.any` da configuração padrão do Dispatcher para esse local.

   * Em cada arquivo do farm, remova qualquer conteúdo da seção renders e substitua-o por:

     `$include "../renders/default_renders.any"`

1. **Verifique virtualhosts**

   * Renomeie o diretório `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e entre nele.

   * Remova qualquer arquivo prefixado com `ams_`.

   * Se conf.dispatcher.d/virtualhosts agora contiver um único arquivo, renomeie-o para `virtualhosts.any`. Lembre-se de adaptar também as instruções $include referentes a esse arquivo nos arquivos do farm.

   * Se, no entanto, a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a instrução $include que fazem referência a eles nos arquivos do farm.

   * Copie o arquivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` da configuração padrão do Dispatcher para esse local.

   * Em cada arquivo do farm, substitua qualquer instrução &quot;include&quot; de filtro que apareça da seguinte maneira:

     `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
pela instrução:

     `$include "../virtualhosts/default_virtualhosts.any"`


1. **Verificar o estado executando o validador**

   * Execute o validador do Dispatcher em seu diretório, com o subcomando Dispatcher:

     `$ validator dispatcher`

   * Se você encontrar erros sobre a falta de arquivos &quot;include&quot;, verifique se os renomeou corretamente.

   * Se você vir erros relacionados à variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

   * Para todos os outros erros, consulte a seção de solução de problemas da documentação da ferramenta de validação.

## Testar sua configuração com uma implantação local {#testing-config-local-deployment}

>[!IMPORTANT]
>
>O teste da sua configuração com uma implantação local requer a instalação do Docker.

Usando o script `docker_run.sh` no SDK do Dispatcher, você pode testar se a sua configuração não contém nenhum outro erro que apareceria apenas na implantação:

1. Gerar informações de implantação com o validador.

   `validator full -d out`
Valida a configuração completa e gera informações de implantação em out.

1. Inicie o Dispatcher em uma imagem do docker com essas informações de implantação.

   Com o servidor de publicação AEM em execução no computador macOS, ouvindo na porta 4503, você pode executar o Dispatcher na frente desse servidor, da seguinte maneira:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Inicia o container e expõe o Apache na porta local 8080.

## Usar sua nova configuração do Dispatcher {#using-dispatcher-config}

Se o validador não relatar mais nenhum problema, e o contêiner do docker for inicializado sem falhas ou avisos, você estará pronto para mover sua configuração para o anúncio `ispatcher/src` subdiretório d do seu repositório Git.