---
title: Conversão de um AMS em um Adobe Experience Manager como uma configuração do Dispatcher de serviço em nuvem
description: Conversão de um AMS em um Adobe Experience Manager como uma configuração do Dispatcher de serviço em nuvem
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# Converter um AMS em um Adobe Experience Manager (AEM) como uma configuração do Dispatcher de serviço em nuvem

## Introdução {#introduction}

Esta seção fornece instruções passo a passo sobre como converter uma configuração do AMS.

>[!NOTE]
>Ele supõe que você tenha um arquivo com uma estrutura semelhante à descrita em [Gerenciar configurações](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)do Dispatcher.

## Etapas para converter um AMS em AEM como uma configuração do Dispatcher de serviço em nuvem

1. **Extraia o arquivo e remova um prefixo final**

   Extraia o arquivo para uma pasta e verifique se o start de subpastas imediatas está com conf, conf.d, conf.dispatcher.d e conf.modules.d. Se não, mova-os para cima na hierarquia.

1. **Livre-se de subpastas e arquivos não usados**

   Remova as subpastas conf e conf.modules.d, bem como os arquivos que correspondem a conf.d/*.conf.

1. **Livre-se de todos os hosts virtuais que não sejam de publicação**

1. **Remover qualquer arquivo de host virtual**

   Em conf.d/enabled_vhosts com autor, não saudável, integridade, lc ou descarregamento em seu nome. Todos os arquivos de host virtual em conf.d/available_vhosts que não estejam vinculados também podem ser removidos.

1. Remova ou comente seções de host virtual que não se referem à porta 80

   Se você ainda tiver seções nos arquivos do host virtual que se referem exclusivamente a outras portas que não a porta 80, por exemplo

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
remova ou comente-os. As declarações nessas seções não serão processadas, mas se você as mantiver por perto, você ainda poderá editá-las sem nenhum efeito, o que é confuso.

1. **Verificar regravações**

   * Insira o diretório conf.d/rewrite.

   * Remova qualquer arquivo chamado base_rewrite.rules e xencaminhou_forcessl_rewrite.rules e lembre-se de remover instruções Incluir nos arquivos de host virtual que se referem a elas.

   * Se conf.d/rewrite agora contiver um único arquivo, ele deverá ser renomeado para rewrite.rules e não se esqueça de adaptar as declarações Incluir referentes a esse arquivo também nos arquivos do host virtual.

   * No entanto, se a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a instrução Incluir que os referenciará nos arquivos do host virtual.

1. **Verificar variáveis**

   1. Insira o diretório conf.d/variables.

   1. Remova qualquer arquivo chamado ams_default.vars e lembre-se de remover instruções Incluir nos arquivos de host virtual que se referem a elas.

   1. Se conf.d/variables agora contiver um único arquivo, ele deverá ser renomeado para custom.vars e não se esqueça de adaptar as instruções Incluir referentes a esse arquivo também nos arquivos do host virtual.

   1. No entanto, se a pasta contiver vários arquivos específicos do host virtual, seu conteúdo deverá ser copiado para a instrução Incluir que os referenciará nos arquivos do host virtual.

1. **Remover listas de permissões**

   Remova a pasta conf.d/whitelists e remova as instruções Incluir nos arquivos do host virtual que fazem referência a algum arquivo dessa subpasta.

1. **Substituir qualquer variável que não esteja mais disponível**

   Em todos os arquivos de host virtual:

   Renomeie PUBLISH_DOCROOT para DOCROOTRemoção de seções referentes a variáveis chamadas DISP_ID, PUBLISH_FORCE_SSL ou PUBLISH_WHITELIST_ENABLED

1. **Verifique seu estado executando o validador**

   Execute o validador do dispatcher no diretório, com o subcomando httpd:

   `$ validator httpd`
Se você vir erros sobre arquivos include ausentes, verifique se você renomeou esses arquivos corretamente.

   Se você vir diretivas Apache que não estão na lista de permissões, remova-as.

1. **Eliminar todos os farm que não são publicados**

   Remova qualquer arquivo de farm em conf.dispatcher.d/enabled_farm que tenha autor, não saudável, integridade, lc ou liberação em seu nome. Todos os arquivos de farm em conf.dispatcher.d/available_farms que não estão vinculados também podem ser removidos.

1. **Renomear arquivos do farm**

   Todos os farm em conf.dispatcher.d/enabled_farms devem ser renomeados para corresponder ao padrão *.farm; por exemplo, um arquivo farm chamado customerX_farm.any deve ser renomeado como customerX.farm.

1. **Verificar cache**

   Insira o diretório conf.dispatcher.d/cache.

   Remova qualquer arquivo prefixo ams_.

   Se conf.dispatcher.d/cache agora estiver vazio, copie o arquivo conf.dispatcher.d/cache/rules.any da configuração padrão do dispatcher para essa pasta. A configuração padrão do dispatcher pode ser encontrada na pasta src deste SDK. Não se esqueça de adaptar as instruções $include referentes aos arquivos ams_*_cache.any nos arquivos do farm também.

   Se, em vez disso, conf.dispatcher.d/cache contiver um único arquivo com o sufixo _cache.any, ele deverá ser renomeado para rules.any e não se esqueça de adaptar as declarações $include referentes a esse arquivo também nos arquivos do farm.

   No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a declaração $include referente a eles nos arquivos do farm.

   Remova qualquer arquivo que tenha o sufixo _invalidate_allow.any.

   Copie o arquivo conf.dispatcher.d/cache/default_invalidate_any da configuração padrão do dispatcher para esse local.

   Em cada arquivo de farm, remova qualquer conteúdo na seção cache/allowClients e substitua-o por:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Verificar cabeçalhos do cliente**

   Insira o diretório conf.dispatcher.d/clientheaders.

   Remova qualquer arquivo prefixo ams_.

   Se conf.dispatcher.d/clientheaders agora contiver um único arquivo com o sufixo _clientheaders.any, ele deverá ser renomeado para clientheaders.any e não se esqueça de adaptar as declarações $include referentes a esse arquivo também nos arquivos do farm.

   No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a declaração $include referente a eles nos arquivos do farm.

   Copie o arquivo conf.dispatcher/clientheaders/default_clientheaders.any da configuração padrão do dispatcher para esse local.

   Em cada arquivo de farm, substitua todas as instruções de inclusão do cliente que tenham a seguinte aparência:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   com a declaração:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Verificar filtro**

   * Insira o diretório conf.dispatcher.d/filtros.

   * Remova qualquer arquivo prefixo ams_.

   * Se conf.dispatcher.d/filtros agora contiver um único arquivo, ele deverá ser renomeado para filtros.any e não se esqueça de adaptar as declarações $include referentes a esse arquivo também nos arquivos do farm.

   * No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a declaração $include referente a eles nos arquivos do farm.

   * Copie o arquivo conf.dispatcher/filters/default_filters.any da configuração padrão do dispatcher para esse local.

   * Em cada arquivo de farm, substitua todas as instruções de inclusão de filtro com a seguinte aparência:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`com a declaração:

      `$include "../filters/default_filters.any"`

1. **Verificar renderizações**

   * Insira o diretório conf.dispatcher.d/renders.

   * Remova todos os arquivos dessa pasta.

   * Copie o arquivo conf.dispatcher.d/renders/default_renders.any da configuração padrão do dispatcher para esse local.

   * Em cada arquivo de farm, remova qualquer conteúdo na seção de renderizações e substitua-o por:

      `$include "../renders/default_renders.any"`

1. **Verificar hosts virtuais**

   * Renomeie o diretório `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e insira-o.

   * Remova qualquer arquivo prefixo `ams_`.

   * Se conf.dispatcher.d/virtualhosts agora contiver um único arquivo, ele deverá ser renomeado para virtualhosts.any e não se esqueça de adaptar as declarações $include referentes a esse arquivo também nos arquivos do farm.

   * No entanto, se a pasta contiver vários arquivos específicos do farm com esse padrão, seu conteúdo deverá ser copiado para a declaração $include referente a eles nos arquivos do farm.

   * Copie o arquivo conf.dispatcher/virtualhosts/default_virtualhosts.any da configuração padrão do dispatcher para esse local.

   * Em cada arquivo de farm, substitua todas as instruções de inclusão de filtro com a seguinte aparência:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
com a declaração:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Verifique seu estado executando o validador**

   * Execute o validador do dispatcher no diretório, com o subcomando dispatcher:

      `$ validator dispatcher`

   * Se você vir erros sobre arquivos include ausentes, verifique se você renomeou esses arquivos corretamente.

   * Se você vir erros referentes a variável indefinida `PUBLISH_DOCROOT`, renomeie-a para `DOCROOT`.

   * Para cada outro erro, consulte a seção Solução de problemas da documentação da ferramenta validadora.

## Testar sua configuração com uma implantação local {#testing-config-local-deployment}

>[!IMPORTANT]
> O teste de sua configuração com uma implantação local requer a instalação do Docker.

Usando o script `docker_run.sh` no Dispatcher SDK, é possível testar se sua configuração não contém nenhum outro erro que apareceria somente na implantação:

1. Gerar informações de implantação com o validador

   `validator full -d out`
Isso valida a configuração completa e gera informações de implantação em

1. Start do despachante em uma imagem do docker com essas informações de implantação

   Com o servidor de publicação de AEM em execução no computador macOS, ouvindo na porta 4503, você pode executar o start do dispatcher na frente desse servidor da seguinte forma:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Isso start o container e expõe o Apache na porta local 8080.

## Usando a nova configuração do dispatcher {#using-dispatcher-config}

Se o validador não relatar mais nenhum problema e o container docker for start sem falhas ou avisos, você estará pronto para mover sua configuração para um subdiretório d`ispatcher/src` do repositório git.