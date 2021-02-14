---
title: API HTTP de ativos
description: Crie, leia, atualize, exclua, gerencie ativos digitais usando a API HTTP em [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: f1fa095c7c89be89ed02ebdf14dcc0a4b9f542b1
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] API HTTP  {#assets-http-api}

## Visão geral {#overview}

A API HTTP [!DNL Assets] permite operações de criação-leitura-atualização-exclusão (CRUD) em ativos digitais, incluindo metadados, renderizações e comentários, juntamente com conteúdo estruturado usando [!DNL Experience Manager] Fragmentos de conteúdo. Ele é exposto em `/api/assets` e é implementado como REST API. Inclui [suporte para Fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md).

Para acessar a API:

1. Abra o documento de serviço da API em `https://[hostname]:[port]/api.json`.
1. Siga o link de serviço [!DNL Assets] que leva a `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Confie no código de resposta para obter mais análises ou ações.

Depois do [!UICONTROL Tempo desligado], um ativo e suas representações não estão disponíveis por meio da interface da Web [!DNL Assets] e por meio da API HTTP. A API retornará uma mensagem de erro 404 se [!UICONTROL On Time] estiver no futuro ou [!UICONTROL Off Time] estiver no passado.

>[!NOTE]
>
>Todas as chamadas de API relacionadas ao upload ou atualização de ativos ou binários em geral (como execuções) estão obsoletas para AEM como uma implantação [!DNL Cloud Service]. Para fazer upload de binários, use [APIs de upload binário direto](developer-reference-material-apis.md#asset-upload-technical).

## Fragmentos de conteúdo {#content-fragments}

Um [Fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) é um tipo especial de ativo. Pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças entre os ativos `standard` (como imagens ou documentos), algumas regras adicionais se aplicam ao manuseio de Fragmentos de conteúdo.

Para obter mais informações, consulte [Suporte a fragmentos de conteúdo na  [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

## Modelo de dados {#data-model}

A API HTTP [!DNL Assets] expõe dois elementos principais, pastas e ativos (para ativos padrão). Além disso, expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado em Fragmentos de conteúdo. Consulte [Modelos de dados do fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obter mais informações.

### Pastas {#folders}

As pastas são como diretórios em sistemas de arquivos tradicionais. São container para outras pastas ou asserções. As pastas têm os seguintes componentes:

**Entidades**: As entidades de uma pasta são seus elementos filho, que podem ser pastas e ativos.

**Propriedades**:

* `name` é o nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão.
* `title` é um título opcional da pasta que pode ser exibido em vez de seu nome.

>[!NOTE]
>
>Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` são substituídos pelo prefixo `dc`. Assim, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

**** LinksFolders expõe três links:

* `self`: Vincule-se a si mesmo.
* `parent`: Link para a pasta pai.
* `thumbnail`: (Opcional) link para uma imagem em miniatura da pasta.

### Assets {#assets}

Em [!DNL Experience Manager] um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo.
* Várias representações, como a representação original (que é o ativo carregado originalmente), uma miniatura e várias outras representações. As representações adicionais podem ser imagens de tamanhos diferentes, codificações de vídeo diferentes ou páginas extraídas de arquivos PDF ou Adobe InDesign.
* Comentários opcionais.

Para obter informações sobre elementos em Fragmentos de conteúdo, consulte [Suporte a fragmentos de conteúdo na API HTTP do Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

Em [!DNL Experience Manager] uma pasta tem os seguintes componentes:

* Entidades: Os filhos dos ativos são suas representações.
* Propriedades.
* Links.

## Recursos disponíveis {#available-features}

A API HTTP [!DNL Assets] inclui os seguintes recursos:

* [Recuperar uma lista](#retrieve-a-folder-listing) de pastas.
* [Criar uma pasta](#create-a-folder).
* [Criar um ativo (obsoleto)](#create-an-asset)
* [Atualizar o binário do ativo (obsoleto)](#update-asset-binary).
* [Atualize os metadados](#update-asset-metadata) do ativo.
* [Crie uma representação](#create-an-asset-rendition) de ativo.
* [Atualizar uma representação](#update-an-asset-rendition) de ativo.
* [Crie um comentário](#create-an-asset-comment) de ativo.
* [Copie uma pasta ou um ativo](#copy-a-folder-or-asset).
* [Mova uma pasta ou um ativo](#move-a-folder-or-asset).
* [Exclua uma pasta, ativo ou representação](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar a leitura, os seguintes exemplos omitem a notação cURL completa. Na verdade, a notação correlaciona-se com [Resty](https://github.com/micha/resty), que é um invólucro de script para `cURL`.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperar uma lista de pastas {#retrieve-a-folder-listing}

Recupera uma representação Siren de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitação**:  `GET /api/assets/myFolder.json`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - sucesso.
* 404 - NOT FOUND - a pasta não existe ou não está acessível.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

**Resposta**: A classe da entidade retornada é um ativo ou uma pasta. As propriedades de entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo do URL apontado pelo link com um `rel` de `self`.

## Crie uma pasta {#create-a-folder}

Cria um novo `sling`: `OrderedFolder` no caminho especificado. Se um `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como nome de nó. Aceitos como dados de solicitação é uma representação Siren da nova pasta ou um conjunto de pares nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, úteis para criar uma pasta diretamente de um formulário HTML. Além disso, as propriedades da pasta podem ser especificadas como parâmetros de query de URL.

Uma chamada de API falha com um código de resposta `500` se o nó pai do caminho fornecido não existir. Uma chamada retornará um código de resposta `409` se a pasta já existir.

**Parâmetros**:  `name` é o nome da pasta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - sobre criação bem sucedida.
* 409 - CONFLICT - se a pasta já existir.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Criar um ativo {#create-an-asset}

Consulte [upload de ativos](developer-reference-material-apis.md) para obter informações sobre como criar um ativo. Não é possível criar um ativo usando a API HTTP.

## Atualizar um binário de ativo {#update-asset-binary}

Consulte [upload de ativos](developer-reference-material-apis.md) para obter informações sobre como atualizar binários de ativos. Não é possível atualizar um binário de ativo usando a API HTTP.

## Atualizar metadados de um ativo {#update-asset-metadata}

Atualiza as propriedades de metadados do ativo. Se você atualizar qualquer propriedade na namespace `dc:`, a API atualizará a mesma propriedade na namespace `jcr`. A API não sincroniza as propriedades nas duas namespaces.

**Solicitação**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Asset (Ativo) tiver sido atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Criar uma representação de ativo {#create-an-asset-rendition}

Crie uma nova representação de ativo para um ativo. Se o nome do parâmetro de solicitação não for fornecido, o nome do arquivo será usado como nome de execução.

**Parâmetros**: Os parâmetros são  `name` para o nome da representação e  `file` como uma referência de arquivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de resposta**

* 201 - CREATED - se a Renderização tiver sido criada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem respectivamente uma representação de ativo pelos novos dados binários.

**Solicitação**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Renderização tiver sido atualizada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Adicionar um comentário em um ativo {#create-an-asset-comment}

Cria um novo comentário de ativo.

**Parâmetros**: Os parâmetros são  `message` para o corpo da mensagem do comentário e  `annotationData` para os dados de anotação no formato JSON.

**Solicitação**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se Comentário tiver sido criado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo disponível no caminho fornecido para um novo destino.

**Cabeçalhos** de solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para copiar o recurso.
* `X-Depth` - quer  `infinity` quer  `0`. Usar `0` copia somente o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use  `F` para evitar a substituição de um ativo no destino existente.

**Solicitação**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo tiver sido copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo tiver sido copiado para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou um ativo no caminho fornecido para um novo destino.

**Cabeçalhos** de solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para copiar o recurso.
* `X-Depth` - quer  `infinity` quer  `0`. Usar `0` copia somente o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use  `T` para forçar a exclusão de um recurso existente ou  `F` para evitar a substituição de um recurso existente.

**Solicitação**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo tiver sido copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo tiver sido copiado para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho fornecido.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se a pasta tiver sido excluída com êxito.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO DE SERVIDOR INTERNO - se algo der errado.

>[!MORELIKETHIS]
>
>* [Documentos de referência do desenvolvedor para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

