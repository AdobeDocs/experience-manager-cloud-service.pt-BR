---
title: Dispatcher na nuvem
description: Dispatcher na nuvem
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 100%

---

# Dispatcher na nuvem {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher na nuvem"
>abstract="Esta página descreve como baixar e extrair as ferramentas do Dispatcher, os módulos de Apache compatíveis, e fornece uma visão geral de alto nível dos modos herdado e flexível."

## Introdução {#apache-and-dispatcher-configuration-and-testing}

Esta página descreve as ferramentas do Dispatcher e como baixá-las e extraí-las, os módulos de apache compatíveis e fornece uma visão geral de alto nível dos modos herdados e flexíveis. Além disso, há outras referências na validação e depuração, e na migração da configuração do Dispatcher do AMS para o AEM as a Cloud Service. <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Ferramentas do Dispatcher {#dispatcher-sdk}

As Ferramentas do Dispatcher fazem parte do SDK geral do AEM as a Cloud Service e fornecem:

* Uma estrutura de arquivo baunilha contendo os arquivos de configuração a serem incluídos em um projeto maven para o Dispatcher.
* Ferramentas para clientes validarem se a configuração do Dispatcher inclui apenas diretivas compatíveis com o AEM as a Cloud Service. Além disso, o conjunto de ferramentas também valida se a sintaxe está correta para que o Apache possa ser iniciado com êxito.
* Uma imagem d Docker que traz o Dispatcher localmente.

## Baixando e extraindo as ferramentas {#extracting-the-sdk}

As Ferramentas do Dispatcher, parte do [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), podem ser baixadas de um arquivo zip no portal de [Distribuição de softwares](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Qualquer nova configuração disponível nessa nova versão das Ferramentas do Dispatcher pode ser usada para implantar em ambientes de nuvem que executam essa versão do AEM na nuvem ou posterior.

Descompacte o SDK, que agrupa as Ferramentas do Dispatcher para macOS, Linux® e Windows.

**Para macOS/Linux**, torne o artefato da ferramenta Dispatcher executável e execute-o. Ele extrai automaticamente os arquivos das Ferramentas do Dispatcher sob o diretório em que você os armazenou (onde `version` é a versão das Ferramentas do Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Para Windows**, extraia o arquivo zip Ferramentas do Dispatcher.

## Validação e depuração usando as Ferramentas do Dispatcher {#validation-debug}

As ferramentas do Dispatcher são usadas para validar e depurar a configuração do Dispatcher do seu projeto. Saiba mais sobre como usar essas ferramentas nas páginas referenciadas abaixo, com base em se a configuração do Dispatcher do seu projeto está estruturada em modo flexível ou no modo herdado:

* **Modo flexível** - o modo recomendado e o padrão para [arquétipo 28 do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) e superior, que também é usada pelo Cloud Manager para novos ambientes criados após a versão 2021.7.0 do Cloud Manager. Os clientes podem ativar esse modo adicionando a pasta e o arquivo `opt-in/USE_SOURCES_DIRECTLY`. Ao usar esse modo mais flexível, não há limitações na estrutura de arquivos na pasta de regravações que, no modo herdado, exigia um único arquivo de `rewrite.rules`. Além disso, não há limitação no número de regras que podem ser adicionadas. Para obter detalhes sobre a estrutura de pastas e a validação local, consulte [Validação e depuração usando Ferramentas do Dispatcher](/help/implementing/dispatcher/validation-debug.md).

* **Modo herdado**: para obter detalhes sobre a estrutura de pastas e a validação local para o modo herdado de configuração do Dispatcher, consulte [Validação e depuração usando Ferramentas do Dispatcher (Herdadas)](/help/implementing/dispatcher/validation-debug-legacy.md)

Para obter mais informações sobre como migrar do modelo de configuração herdado para o mais flexível, fornecido com arquétipo 28 do AEM em diante, consulte [esta documentação](/help/implementing/dispatcher/validation-debug.md#migrating).

## Disposição do conteúdo {#content-disposition}

Para o nível de publicação, o padrão para o serviço de blobs é como um anexo. Substitua essa configuração usando o padrão [cabeçalho de disposição de conteúdo](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers/Content-Disposition) no Dispatcher.

Veja abaixo um exemplo de como a configuração deve ser:

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## Módulos Apache compatíveis {#supported-directives}

A tabela abaixo mostra os módulos Apache compatíveis:

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
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


Os clientes não podem adicionar módulos arbitrários, no entanto, módulos adicionais podem ser considerados para inclusão futura. Os clientes podem encontrar a lista de diretivas disponíveis para uma determinada versão do Dispatcher executando o comando de lista de permissões do validador no SDK.

As diretivas permitidas nos arquivos de configuração do Apache podem ser listadas executando o comando de lista de permissões do validador:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## Estrutura da pasta {#folder-structure}

A estrutura de pastas do apache e do Dispatcher do projeto será ligeiramente diferente com base em qual modo o projeto está usando, conforme descrito na seção [Validação e depuração usando as Ferramentas do Dispatcher](#validation-debug) acima.

## Migração a configuração do Dispatcher do AMS {#ams-aem}

Para obter detalhes sobre como migrar a configuração do Dispatcher do AMS para o AEM as a Cloud Service, consulte a página [Migrando a configuração do Dispatcher do AMS para o AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service.
