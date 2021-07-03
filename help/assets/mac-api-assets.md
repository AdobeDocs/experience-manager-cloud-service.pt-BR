---
title: API HTTP de ativos
description: Crie, leia, atualize, exclua, gerencie ativos digitais usando a API HTTP em [!DNL Experience Manager Assets].
contentOwner: AG
feature: APIs HTTP de ativos, APIs
role: Developer,Architect,Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] API HTTP {#assets-http-api}

## Visão geral {#overview}

A API HTTP [!DNL Assets] permite criar-ler-atualizar-excluir (CRUD) operações em ativos digitais, incluindo metadados, representações e comentários, juntamente com conteúdo estruturado usando [!DNL Experience Manager] Fragmentos de conteúdo. Ele é exposto em `/api/assets` e é implementado como REST API. Ele inclui [suporte para Fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md).

Para acessar a API:

1. Abra o documento do serviço de API em `https://[hostname]:[port]/api.json`.
1. Siga o link do serviço [!DNL Assets] que leva a `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Confie no código de resposta para mais análises ou ações.

>[!NOTE]
>
>Todas as chamadas de API relacionadas ao upload ou atualização de ativos ou binários em geral (como representações) estão obsoletas para [!DNL Experience Manager] como uma implantação [!DNL Cloud Service]. Para fazer upload de binários, use [APIs de upload binário direto](developer-reference-material-apis.md#asset-upload).

## Fragmentos de conteúdo {#content-fragments}

Um [Fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) é um tipo especial de ativo. Ele pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças nos ativos `standard` (como imagens ou documentos), algumas regras adicionais se aplicam ao manuseio dos Fragmentos de conteúdo.

Para obter mais informações, consulte [Suporte a fragmentos de conteúdo na  [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

## Modelo de dados {#data-model}

A API HTTP [!DNL Assets] expõe dois elementos, pastas e ativos principais (para ativos padrão). Além disso, expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado nos Fragmentos de conteúdo. Consulte [Modelos de dados do fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obter mais informações.

### Pastas {#folders}

As pastas são como diretórios nos sistemas de arquivos tradicionais. A pasta pode conter apenas ativos, apenas pastas ou pastas e ativos. As pastas têm os seguintes componentes:

**Entidades**: As entidades de uma pasta são seus elementos filho, que podem ser pastas e ativos.

**Propriedades**:

* `name` é o nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão.
* `title` é um título opcional da pasta que pode ser exibido em vez de seu nome.

>[!NOTE]
>
>Algumas propriedades de pasta ou ativo são mapeadas para um prefixo diferente. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` são substituídos pelo prefixo `dc`. Portanto, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

**** LinksFolders expõe três links:

* `self`: Vincular a si mesmo.
* `parent`: Link para a pasta principal.
* `thumbnail`: (Opcional) link para uma imagem em miniatura de pasta.

### Ativos {#assets}

Em [!DNL Experience Manager] um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo.
* Ficheiro binário originalmente carregado do ativo.
* Várias representações, conforme configurado. Essas podem ser imagens de diferentes tamanhos, vídeos de diferentes codificações ou páginas extraídas de arquivos PDF ou [!DNL Adobe InDesign].
* Comentários opcionais.

Para obter informações sobre elementos nos Fragmentos de conteúdo, consulte [Suporte a fragmentos de conteúdo na API HTTP do Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

Em [!DNL Experience Manager] uma pasta tem os seguintes componentes:

* Entidades: Os filhos dos ativos são suas representações.
* Propriedades.
* Links.

## Recursos disponíveis {#available-features}

A API HTTP [!DNL Assets] inclui os seguintes recursos:

* [Recupere uma lista de pastas](#retrieve-a-folder-listing).
* [Criar uma pasta](#create-a-folder).
* [Criar um ativo (obsoleto)](#create-an-asset)
* [Atualizar binário de ativo (obsoleto)](#update-asset-binary).
* [Atualizar metadados](#update-asset-metadata) do ativo.
* [Criar uma representação de ativo](#create-an-asset-rendition).
* [Atualizar uma representação de ativo](#update-an-asset-rendition).
* [Crie um comentário](#create-an-asset-comment) de ativo.
* [Copie uma pasta ou um ativo](#copy-a-folder-or-asset).
* [Mova uma pasta ou um ativo](#move-a-folder-or-asset).
* [Excluir uma pasta, ativo ou representação](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar a legibilidade, os exemplos a seguir omitem as anotações completas de cURL. A notação correlaciona-se com [Resty](https://github.com/micha/resty), que é um wrapper de scripts para cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperar uma listagem de pastas {#retrieve-a-folder-listing}

Recupera uma representação Siren de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitação**:  `GET /api/assets/myFolder.json`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - sucesso.
* 404 - NÃO ENCONTRADO - a pasta não existe ou não está acessível.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

**Resposta**: A classe da entidade retornada é um ativo ou uma pasta. As propriedades das entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo do URL apontado pelo link com um `rel` de `self`.

## Crie uma pasta  {#create-a-folder}

Cria um `sling`: `OrderedFolder` no caminho especificado. Se `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como nome do nó. A solicitação aceita um dos seguintes procedimentos:

* Uma representação Siren da nova pasta
* Um conjunto de pares de nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`. Eles são úteis para criar uma pasta diretamente de um formulário HTML.

Além disso, as propriedades da pasta podem ser especificadas como parâmetros de consulta de URL.

Uma chamada de API falha com um código de resposta `500` se o nó pai do caminho fornecido não existir. Uma chamada retorna um código de resposta `409` se a pasta existir.

**Parâmetros**:  `name` é o nome da pasta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - na criação bem-sucedida.
* 409 - CONFLICT - if folder exists.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Criar um ativo {#create-an-asset}

Consulte [upload de ativo](developer-reference-material-apis.md) para obter informações sobre como criar um ativo. Não é possível criar um ativo usando a API HTTP.

## Atualizar um binário de ativo {#update-asset-binary}

Consulte [upload de ativo](developer-reference-material-apis.md) para obter informações sobre como atualizar binários de ativos. Não é possível atualizar um binário de ativo usando a API HTTP.

## Atualizar metadados de um ativo {#update-asset-metadata}

Atualiza as propriedades de metadados do ativo. Se você atualizar qualquer propriedade no namespace `dc:`, a API atualizará a mesma propriedade no namespace `jcr`. A API não sincroniza as propriedades nos dois namespaces.

**Solicitação**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se Ativo tiver sido atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Criar uma representação de ativo {#create-an-asset-rendition}

Crie uma representação para um ativo. Se o nome do parâmetro da solicitação não for fornecido, o nome do arquivo será usado como nome da representação.

**Parâmetros**: Os parâmetros são  `name` para o nome da representação e  `file` como uma referência de arquivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de resposta**

* 201 - CREATED - se a Representação tiver sido criada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem, respectivamente, uma representação de ativo pelos novos dados binários.

**Solicitação**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se a Representação tiver sido atualizada com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Adicionar um comentário em um ativo {#create-an-asset-comment}

**Parâmetros**: Os parâmetros são  `message` para o corpo da mensagem do comentário e  `annotationData` para os dados de anotação no formato JSON.

**Solicitação**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CRIADO - se o Comentário tiver sido criado com êxito.
* 404 - NÃO ENCONTRADO - se o Ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo disponível no caminho fornecido para um novo destino.

**Cabeçalhos** da solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino no escopo da solução de API para copiar o recurso.
* `X-Depth` -  `infinity` ou  `0`. Usar `0` copia somente o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use  `F` para impedir a substituição de um ativo no destino existente.

**Solicitação**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CREATED - se a pasta/ativo tiver sido copiada para um destino não existente.
* 204 - NO CONTENT - se a pasta/ativo tiver sido copiada para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou um ativo no caminho especificado para um novo destino.

**Cabeçalhos** da solicitação: Os parâmetros são:

* `X-Destination` - um novo URI de destino no escopo da solução de API para copiar o recurso.
* `X-Depth` -  `infinity` ou  `0`. Usar `0` copia somente o recurso e suas propriedades, e não seus filhos.
* `X-Overwrite` - Use  `T` para excluir forçosamente um recurso existente ou  `F` para evitar a substituição de um recurso existente.

**Solicitação**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos** de resposta: Os códigos de resposta são:

* 201 - CREATED - se a pasta/ativo tiver sido copiada para um destino não existente.
* 204 - NO CONTENT - se a pasta/ativo tiver sido copiada para um destino existente.
* 412 - PRECONDITION FAILED - se um cabeçalho de solicitação estiver ausente.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho fornecido.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos** de resposta: Os códigos de resposta são:

* 200 - OK - se a pasta tiver sido excluída com êxito.
* 412 - PRECONDITION FAILED - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - INTERNAL SERVER ERROR - se algo der errado.

## Dicas, práticas recomendadas e limitações {#tips-limitations}

* Após o [!UICONTROL Tempo desligado], um ativo e suas representações não estarão disponíveis por meio da interface da Web [!DNL Assets] e por meio da API HTTP. A API retornará uma mensagem de erro 404 se o [!UICONTROL Tempo ligado] estiver no futuro ou [!UICONTROL Tempo desligado] estiver no passado.

* A API HTTP de ativos não retorna os metadados completos. Os namespaces são codificados e somente esses namespaces são retornados. Para obter metadados completos, consulte o caminho do ativo `/jcr_content/metadata.json`.

* Algumas propriedades de pasta ou ativo são mapeadas para um prefixo diferente quando atualizadas usando APIs. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` são substituídos pelo prefixo `dc`. Portanto, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

>[!MORELIKETHIS]
>
>* [Documentos de referência do desenvolvedor para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

