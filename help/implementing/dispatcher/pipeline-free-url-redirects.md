---
title: Redirecionamentos de URL sem pipeline
description: Saiba como declarar redirecionamentos 301 ou 302 sem acesso aos pipelines Git ou Cloud Manager.
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: 7a543c8fe63166ef34999f23ce9b05de8e8b0e9f
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Redirecionamentos de URL sem pipeline {#pipeline-free-redirects}

Por vários motivos, as organizações reescrevem URLs de uma maneira que causa um redirecionamento 301 (ou 302), o que significa que o navegador é redirecionado para uma página diferente.

Os cenários incluem:

* Uma página do HTML removida, de modo que o usuário é direcionado a uma página substituta (às vezes, a página inicial) em vez de ver um erro `404 Page Not Found`.
* Uma página do HTML renomeada.
* Otimização de SEO.

A AEM as a Cloud Service oferece [várias abordagens](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) para implementar redirecionamentos do lado do servidor, mas a estratégia descrita neste artigo, redirecionamentos sem pipeline, é uma boa escolha quando:

* As pessoas que mantêm os redirecionamentos são usuários empresariais, que não têm o acesso necessário para confirmar alterações de arquivo no controle de origem ou a possibilidade de executar um pipeline de configuração no nível da Web do Cloud Manager.
* O número de redirecionamentos varia de alguns a dezenas de milhares.
* Você deseja a opção de uma interface de usuário, criada como um projeto personalizado ou usando o [Gerenciador do Mapa de Redirecionamento do ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) ou o [Gerenciador de Redirecionamento do ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html).

O núcleo desse recurso é a capacidade do AEM Apache/Dispatcher de carregar (ou recarregar) um ou mais arquivos de mapa de regravação que foram colocados em um local especificado no repositório de publicação (para que ele possa ser baixado na publicação do AEM). É importante mencionar que a forma como os arquivos chegam lá está fora do escopo desse recurso, mas você pode considerar um dos seguintes métodos:

* Assimilar o mapa de regravação como um ativo na interface do usuário do autor e publicá-lo.
* Instalando o [ACS Commons Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) ([pelo menos versão 6.7.0 ou superior](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), que inclui uma interface de usuário para gerenciar os mapeamentos de URL e também pode publicar o arquivo de mapa de regravação.
* Instalando o [ACS Commons Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) ([pelo menos versão 6.10.0 ou superior](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), que também inclui uma interface de usuário para gerenciar os mapeamentos de URL e pode publicar o arquivo de mapa de regravação.
* Flexibilidade total ao escrever um aplicativo personalizado. Por exemplo, uma interface de usuário ou de linha de comando para gerenciar os mapeamentos de URL ou, como alternativa, um formulário para carregar um mapa de regravação, que usa APIs do AEM para publicar o arquivo de mapa de regravação.

>[!NOTE]
> Este recurso requer o AEM versão **18311 ou superior**.

>[!NOTE]
> O uso deste recurso do Gerenciador de Mapa de Redirecionamento requer o ACS Commons versão **6.7.0 ou superior**, enquanto o uso do Gerenciador de Redirecionamento requer versão **6.10.0 ou superior**.

Para obter um guia detalhado de implementação passo a passo, consulte o tutorial [Implementando redirecionamentos de URL sem pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects).

## O mapa de regravação {#rewrite-map}

O mapa de regravação é recarregado (se alterado) pelo servidor HTTP do Apache a cada 300 segundos por padrão (o valor é configurável). O formato de arquivo deve seguir o formato de arquivo RewriteMap do mapa de valor-chave de texto simples descrito na [documentação do Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt).

Um arquivo chamado `managed-rewrite-maps.yaml` deve ser criado para especificar o local do arquivo de mapa de regravação e deve ser implantado uma vez, usando o pipeline de pilha completa do Cloud Manager ou o pipeline da camada da Web. O arquivo deve ser criado na pasta [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) da configuração do Dispatcher. Certifique-se de usar a [estrutura de arquivo do modo flexível](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure).

Você pode configurá-lo com o seguinte padrão:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

Se, por exemplo, o método escolhido para colocar o arquivo de mapa de regravação for assimilá-lo no AEM como um ativo chamado `mysite-redirectmap.txt` e depois publicá-lo, você poderá especificar uma pasta em `/content/dam`:

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

Em seguida, em um arquivo de configuração do Apache como `rewrites/rewrite.rules` ou `<yourfile>.vhost`, você deve configurar o arquivo de mapa referenciado pela propriedade de nome (`my.map` na amostra acima). Após carregado, este arquivo de mapa é salvo no armazenamento local do dispatcher no local **corrigido** `/tmp/rewrites/`.

A diretiva `RewriteMap` deve indicar que os dados são armazenados em um formato de arquivo do gerenciador de banco de dados (DBM) usando o formato `sdbm` (DBM simples), e o caminho completo do arquivo é derivado do prefixo do local de armazenamento e da propriedade name.

O restante da configuração depende do formato do `redirectmap.txt`. O formato mais simples, mostrado na amostra abaixo, é um mapeamento de um para um entre o url original e o url mapeado:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```

## Considerações {#considerations}

Lembre-se do seguinte:

* Por padrão, ao carregar um mapa de regravação, o Apache é inicializado sem esperar que os arquivos de mapa completos sejam carregados e, portanto, pode haver inconsistências temporárias até que os mapas completos sejam carregados. Essa configuração pode ser alterada para que o Apache aguarde o conteúdo completo do mapa ser carregado, mas leva mais tempo para que o Apache seja inicializado. Para alterar esse comportamento de forma que o Apache aguarde, adicione `wait:true` ao arquivo `managed-rewrite-maps.yaml`.
* Para alterar a frequência entre cargas, adicione `ttl: <integer>` ao arquivo `managed-rewrite-maps.yaml`. Por exemplo: `ttl: 120`.
* O Apache tem um limite de comprimento de 1024 para entradas únicas de RewriteMap.

## Tutoriais {#tutorials}

1. [Implementando redirecionamentos de URL sem pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects)
1. [redirecionamentos de URL](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection)
