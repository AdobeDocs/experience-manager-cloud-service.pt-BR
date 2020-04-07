---
title: Pesquisa e indexação de conteúdo
description: 'Pesquisa e indexação de conteúdo '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Pesquisa e indexação de conteúdo {#indexing}

## Alterações no AEM como um serviço em nuvem {#changes-in-aem-as-a-cloud-service}

Com o AEM como um serviço em nuvem, a Adobe está mudando de um modelo centralizado em instâncias do AEM para uma visualização baseada em serviços com Container n-x do AEM, conduzidos por dutos CI/CD no Gerenciador de nuvem. Em vez de configurar e manter Índices em instâncias de AEM únicas, a configuração de Índice deve ser especificada antes de uma implantação. As mudanças de configuração na produção estão quebrando claramente as políticas de CI/CD. O mesmo se aplica às alterações de índice, pois isso pode afetar a estabilidade e o desempenho do sistema se não for especificado, testado e indexado novamente antes de trazê-los para a produção.

Veja abaixo uma lista das principais alterações em relação ao AEM 6.5 e versões anteriores:

1. Os usuários não terão acesso ao Gerenciador de índice de uma única instância do AEM para depurar, configurar ou manter a indexação. É usado apenas para desenvolvimento local e implantações locais.

1. Os usuários não alterarão Índices em uma única instância do AEM, nem precisarão se preocupar com verificações de consistência ou reindexação.

1. Em geral, as alterações de índice são iniciadas antes de entrar na produção, a fim de não contornar os gateways de qualidade nos pipelines CI/CD do Cloud Manager e não afetar os KPIs de Negócios na produção.

1. Todas as métricas relacionadas, incluindo o desempenho da pesquisa na produção, estarão disponíveis para clientes em tempo de execução para fornecer a visualização holística nos tópicos de Pesquisa e Indexação.

1. Os clientes poderão configurar alertas de acordo com suas necessidades.

1. Os SREs monitoram a saúde do sistema 24 horas por dia, 7 dias por semana, e tomarão medidas se necessário e o mais cedo possível.

1. A configuração do índice é alterada por meio de implantações. As alterações de definição de índice são configuradas como outras alterações de conteúdo.

1. Em um alto nível no AEM como um serviço em nuvem, com a introdução do modelo [de implantação](#index-management-using-blue-green-deployments) Blue-Green, dois conjuntos de índices existirão: um conjunto para a versão antiga (azul) e um conjunto para a nova versão (verde).

<!-- The version of the index that is used is configured using flags in the index definitions via the `useIfExist` flag. An index may be used in only one version of the application (for example only blue or only green), or in both versions. Detailed documentation is available at [Index Management using Blue-Green Deployments](#index-management-using-blue-green-deployments). -->

1. Os clientes podem ver se o trabalho de indexação foi concluído na página de criação do Cloud Manager e receberão uma notificação quando a nova versão estiver pronta para receber tráfego.

1. Limitações: no momento, o gerenciamento de índice no AEM como um serviço de nuvem é compatível somente com índices do tipo lucene.

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings. 

AS NOTE: the above is internal for now.

-->

## Como usar {#how-to-use}

A definição de índices pode incluir os 3 casos de uso:

1. Adicionando uma nova definição de índice de cliente
1. Atualização de uma definição de índice existente. Isso significa adicionar uma nova versão de uma definição de índice existente
1. Remoção de um índice existente redundante ou obsoleto.

Para ambos os pontos 1 e 2 acima, é necessário criar uma nova definição de índice como parte da sua base de código personalizada na programação de lançamento do Cloud Manager. Para obter mais informações, consulte a documentação [Implantação](/help/implementing/deploying/overview.md)no AEM como um serviço em nuvem.

### Preparação da nova definição de índice {#preparing-the-new-index-definition}

É necessário preparar um novo pacote de definição de índice que contenha a definição de índice real, seguindo este padrão de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

O que então precisa de ir para baixo `ui.apps/src/main/content/jcr_root`. As pastas de sub-raiz não são suportadas a partir de agora.

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

O pacote da amostra acima é construído como `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

### Implantação de definições de índice {#deploying-index-definitions}

> [!NOTE]
>
> Há um problema conhecido com o Plug-in do pacote Jackrabbit Filevault Maven versão **1.1.0** que não permite que você adicione `oak:index` aos módulos do `<packageType>application</packageType>`. Para contornar esse problema, use a versão **1.0.4**.

As definições de índice agora são marcadas como personalizadas e com controle de versão:

* A própria definição do índice (por exemplo `/oak:index/ntBaseLucene-custom-1`)

Portanto, para implantar um índice, a definição (`/oak:index/definitionname`) do índice precisa ser fornecida por meio `ui.apps` do processo de implantação Git e do Cloud Manager.

Depois que a nova definição de índice é adicionada, o novo aplicativo precisa ser implantado pelo Cloud Manager. Após a implantação, dois trabalhos são iniciados, responsáveis por adicionar (e mesclar, se necessário) as definições de índice ao MongoDB e ao Azure Segment Store para autor e publicação, respectivamente. Os repositórios subjacentes estão sendo indexados novamente com as novas definições de índice, antes da mudança Blue-Green.

## Gerenciamento de índice usando implantações Blue-Green {#index-management-using-blue-green-deployments}

### O que é Gerenciamento de índice {#what-is-index-management}

O gerenciamento de índice trata de adicionar, remover e alterar índices. A alteração da *definição* de um índice é rápida, mas a aplicação da alteração (muitas vezes chamada de &quot;criação de um índice&quot; ou, para índices existentes, &quot;reindexação&quot;) requer tempo. Não é instantâneo: o repositório deve ser verificado para que os dados sejam indexados.

### O que é a implantação do Blue-Green {#what-is-blue-green-deployment}

A implantação Blue-Green pode reduzir o tempo de inatividade. Também permite upgrades sem tempo de inatividade e reversões rápidas. A versão antiga do aplicativo (azul) é executada ao mesmo tempo que a nova versão do aplicativo (verde).

### Áreas somente leitura e leitura/gravação {#read-only-and-read-write-areas}

Determinadas áreas do repositório (partes somente leitura do repositório) podem ser diferentes na versão antiga (azul) e na nova (verde) do aplicativo. As áreas somente leitura do repositório normalmente são &quot;`/app`&quot; e &quot;`/libs`&quot;. No exemplo a seguir, itálico é usado para marcar áreas somente leitura, enquanto negrito é usado para áreas de leitura e gravação.

* **/**
* */apps (somente leitura)*
* **/content**
* */libs (somente leitura)*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

As áreas de leitura e gravação do repositório são compartilhadas entre todas as versões do aplicativo, enquanto para cada versão do aplicativo há um conjunto específico de `/apps` e `/libs`.

### Gerenciamento de índice sem implantação em verde azul {#index-management-without-blue-green-deployment}

Durante o desenvolvimento ou ao usar instalações locais, os índices podem ser adicionados, removidos ou alterados em tempo de execução. Os índices são usados assim que estão disponíveis. Se um índice ainda não deve ser usado na versão antiga do aplicativo, o índice normalmente é criado durante um tempo de inatividade programado. O mesmo ocorre ao remover um índice ou alterar um índice existente. Ao remover um índice, ele fica indisponível assim que é removido.

### Gerenciamento De Índice Com Implantação Blue-Green {#index-management-with-blue-green-deployment}

Com implantações azul-esverdeadas, não há tempo de inatividade. No entanto, para o gerenciamento de índice, isso requer que os índices sejam usados apenas por determinadas versões do aplicativo. Por exemplo, ao adicionar um índice na versão 2 do aplicativo, você não gostaria que ele fosse usado pela versão 1 do aplicativo. O inverso é o caso quando um índice é removido: um índice removido na versão 2 ainda é necessário na versão 1. Ao alterar uma definição de índice, desejamos que a versão antiga do índice seja usada apenas para a versão 1 e que a nova versão do índice seja usada apenas para a versão 2.

A tabela a seguir mostra 5 definições de índice: index `cqPageLucene` é usado em ambas as versões enquanto index `damAssetLucene-custom-1` é usado somente na versão 2.


> [!NOTE]
> `<indexName>-custom-<customerVersionNumber>` é necessário para que o AEM como um serviço em nuvem marque isso como uma substituição para um índice existente.

| Índice | Índice predefinido | Usar na versão 1 | Usar na versão 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sim | Sim | Não |
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Não | Sim |
| /oak:index/acmeProduct-custom-1 | Não | Sim | Não |
| /oak:index/acmeProduct-custom-2 | Não | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Sim |

O número da versão é incrementado sempre que o índice é alterado. Para evitar que os nomes de índice personalizados colidam com os nomes de índice do próprio produto, os índices personalizados, bem como as alterações nos índices prontos para uso, precisam terminar com `-custom-<number>`.

### Alterações nos índices prontos para uso {#changes-to-out-of-the-box-indexes}

Quando a Adobe altera um índice predefinido como &quot;damAssetLucene&quot; ou &quot;cqPageLucene&quot;, um novo índice chamado `damAssetLucene-2` ou `cqPageLucene-2` é criado ou, se o índice já foi personalizado, a definição de índice personalizado é unida às alterações no índice predefinido, como mostrado abaixo. A mesclagem de alterações ocorre automaticamente. Isso significa que você não precisa fazer nada se um índice predefinido for alterado. No entanto, é possível personalizar o índice novamente mais tarde.

| Índice | Índice predefinido | Usar na versão 2 | Usar na versão 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sim (personalizado) | Sim | Não |
| /oak:index/damAssetLucene-2-custom-1 | Sim (unido automaticamente de damAssetLucene-custom-1 e damAssetLucene-2) | Não | Sim |
| /oak:index/cqPageLucene | Sim | Sim | Não |
| /oak:index/cqPageLucene-2 | Sim | Não | Sim |

### Limitações       {#limitations}

Atualmente, o gerenciamento de índice é compatível apenas com índices do tipo `lucene`.

### Removendo um índice {#removing-an-index}

Se um índice for removido em uma versão posterior do aplicativo, você poderá definir um índice vazio (um índice sem dados para indexar), com um novo nome. Por exemplo, você pode nomeá-lo `/oak:index/acmeProduct-custom-3`. Isso substitui o índice `/oak:index/acmeProduct-custom-2`. Quando `/oak:index/acmeProduct-custom-2` for removido pelo sistema, o índice vazio também `/oak:index/acmeProduct-custom-3` poderá ser removido.

### Adicionar um índice {#adding-an-index}

Para adicionar um índice chamado &quot;/oak:index/acmeProduct-custom-1&quot; a ser usado em uma nova versão do aplicativo e posterior, o índice precisa ser configurado da seguinte maneira:

`/oak:index/acmeProduct-custom-1`

Como acima, isso garante que o índice seja usado somente pela nova versão do aplicativo.

### Alteração de um índice {#changing-an-index}

Quando um índice existente é alterado, um novo índice precisa ser adicionado com a definição de índice alterada. Por exemplo, considere que o índice existente &quot;/oak:index/acmeProduct-custom-1&quot; foi alterado. O índice antigo é armazenado em `/oak:index/acmeProduct-custom-1`, e o novo índice é armazenado em `/oak:index/acmeProduct-custom-2`.

A versão antiga do aplicativo usa a seguinte configuração:

`/oak:index/acmeProduct-custom-1`

A nova versão do aplicativo usa a seguinte configuração (alterada):

`/oak:index/acmeProduct-custom-2`