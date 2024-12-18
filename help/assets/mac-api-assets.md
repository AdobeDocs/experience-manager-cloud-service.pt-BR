---
title: API HTTP de ativos
description: Criar, ler, atualizar, excluir, gerenciar ativos digitais usando a API HTTP em [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 4cec40947f1b50dd627321cabfbe43033a224f8b
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 3%

---

# API HTTP [!DNL Adobe Experience Manager Assets] {#assets-http-api}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

## Visão geral {#overview}

A API HTTP do [!DNL Assets] permite operações create-read-update-delete (CRUD) em ativos digitais, incluindo metadados, representações e comentários, juntamente com conteúdo estruturado usando [!DNL Experience Manager] Fragmentos de conteúdo. Ele é exposto em `/api/assets` e é implementado como REST API. Inclui [suporte para Fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
> Uma implementação OpenAPI modernizada da API de gerenciamento de fragmento de conteúdo está disponível. Para obter a documentação completa, consulte [API de gerenciamento de fragmento de conteúdo](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). É recomendável usar a nova implementação da OpenAPI. O uso existente da API HTTP do Assets para fragmentos de conteúdo deve ser migrado para a nova OpenAPI de gerenciamento de fragmento de conteúdo.

Para acessar a API:

1. Abra o documento de serviço de API em `https://[hostname]:[port]/api.json`.
1. Siga o link do serviço [!DNL Assets] que leva a `https://[hostname]:[server]/api/assets.json`.

A resposta da API é um arquivo JSON para alguns tipos MIME e um código de resposta para todos os tipos MIME. A resposta JSON é opcional e pode não estar disponível, por exemplo, para arquivos PDF. Contar com o código de resposta para análise ou ações adicionais.

>[!NOTE]
>
>Todas as chamadas de API relacionadas ao carregamento ou atualização de ativos ou binários em geral (como representações) estão obsoletas para [!DNL Experience Manager] como uma implantação do [!DNL Cloud Service]. Para carregar binários, use as [APIs de carregamento binário direto](developer-reference-material-apis.md#asset-upload).

## Fragmentos de conteúdo {#content-fragments}

Um [Fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md) é um tipo especial de ativo. Ele pode ser usado para acessar dados estruturados, como textos, números, datas, entre outros. Como há várias diferenças para `standard` ativos (como imagens ou documentos), algumas regras adicionais se aplicam à manipulação de Fragmentos de conteúdo.

Para obter mais informações, consulte [Suporte a fragmentos de conteúdo na [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Consulte [APIs de AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) para obter uma visão geral das várias APIs disponíveis e uma comparação de alguns dos conceitos envolvidos.
>
>As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.

## Modelo de dados {#data-model}

A API HTTP do [!DNL Assets] expõe dois elementos principais, pastas e ativos (para ativos padrão). Além disso, ele expõe elementos mais detalhados para os modelos de dados personalizados que descrevem o conteúdo estruturado em Fragmentos de conteúdo. Consulte [Modelos de dados de fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obter mais informações.

>[!NOTE]
>
>As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.

### Pastas {#folders}

As pastas são como diretórios, como nos sistemas de arquivos tradicionais. A pasta pode conter apenas ativos, apenas pastas ou pastas e ativos. As pastas têm os seguintes componentes:

**Entidades**: as entidades de uma pasta são seus elementos secundários, que podem ser pastas e ativos.

**Propriedades**:

* `name` é o nome da pasta. É o mesmo que o último segmento no caminho do URL sem a extensão.
* `title` é um título opcional da pasta que pode ser exibido em vez do seu nome.

>[!NOTE]
>
>Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` foi substituído pelo prefixo `dc`. Portanto, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

**Links** As pastas expõem três links:

* `self`: Vincular a si mesmo.
* `parent`: Vincular à pasta pai.
* `thumbnail`: (Opcional) link para uma imagem em miniatura da pasta.

### Ativos {#assets}

Em [!DNL Experience Manager] um ativo contém os seguintes elementos:

* As propriedades e os metadados do ativo.
* O upload original do arquivo binário do ativo.
* Várias representações conforme configurado. Essas podem ser imagens de diferentes tamanhos, vídeos de diferentes codificações ou páginas extraídas de arquivos PDF ou [!DNL Adobe InDesign].
* Comentários opcionais.

Para obter informações sobre elementos nos Fragmentos de conteúdo, consulte [Suporte a Fragmentos de conteúdo na API HTTP do Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.

Em [!DNL Experience Manager] uma pasta tem os seguintes componentes:

* Entidades: os filhos dos ativos são suas representações.
* Propriedades.
* Links.

## Recursos disponíveis {#available-features}

A API HTTP [!DNL Assets] inclui os seguintes recursos:

* [Recuperar uma listagem de pastas](#retrieve-a-folder-listing).
* [Criar uma pasta](#create-a-folder).
* [Criar um ativo (desaprovado)](#create-an-asset)
* [Atualizar binário de ativo (desaprovado)](#update-asset-binary).
* [Atualizar metadados de ativos](#update-asset-metadata).
* [Criar uma representação de ativo](#create-an-asset-rendition).
* [Atualize uma representação de ativo](#update-an-asset-rendition).
* [Criar um comentário de ativo](#create-an-asset-comment).
* [Copiar uma pasta ou um ativo](#copy-a-folder-or-asset).
* [Mover uma pasta ou um ativo](#move-a-folder-or-asset).
* [Excluir uma pasta, ativo ou representação](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar a leitura, os exemplos a seguir omitem as notações cURL completas. A notação correlaciona-se com [Resty](https://github.com/micha/resty), que é um wrapper de scripts para cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperar uma listagem de pastas {#retrieve-a-folder-listing}

Recupera uma representação Sirene de uma pasta existente e de suas entidades filhas (subpastas ou ativos).

**Solicitação**: `GET /api/assets/myFolder.json`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - êxito.
* 404 - NÃO ENCONTRADO - a pasta não existe ou não está acessível.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

**Resposta**: a classe da entidade retornada é um ativo ou uma pasta. As propriedades das entidades contidas são um subconjunto do conjunto completo de propriedades de cada entidade. Para obter uma representação completa da entidade, os clientes devem recuperar o conteúdo da URL apontada pelo link com um `rel` de `self`.

## Criar uma pasta {#create-a-folder}

Cria um `sling`: `OrderedFolder` no caminho fornecido. Se `*` for fornecido em vez de um nome de nó, o servlet usará o nome do parâmetro como o nome do nó. A solicitação aceita uma das seguintes opções:

* Uma representação de Sirene da nova pasta
* Um conjunto de pares nome-valor, codificados como `application/www-form-urlencoded` ou `multipart`/ `form`- `data`. Eles são úteis para criar uma pasta diretamente de um formulário HTML.

Além disso, as propriedades da pasta podem ser especificadas como parâmetros de consulta de URL.

Uma chamada de API falhará com um código de resposta `500` se o nó pai do caminho fornecido não existir. Uma chamada retornará um código de resposta `409` se a pasta existir.

**Parâmetros**: `name` é o nome da pasta.

**Solicitação**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - na criação bem-sucedida.
* 409 - CONFLITO - se a pasta existir.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Criar um ativo {#create-an-asset}

Consulte [carregamento de ativo](developer-reference-material-apis.md) para obter informações sobre como criar um ativo. Não é possível criar um ativo usando a API HTTP.

## Atualizar um binário de ativo {#update-asset-binary}

Consulte [upload de ativos](developer-reference-material-apis.md) para obter informações sobre como atualizar binários de ativos. Não é possível atualizar um binário de ativo usando a API HTTP.

## Atualizar metadados de um ativo {#update-asset-metadata}

Atualiza as propriedades dos metadados do Ativo. Se você atualizar qualquer propriedade no namespace `dc:`, a API atualizará a mesma propriedade no namespace `jcr`. A API não sincroniza as propriedades nos dois namespaces.

**Solicitação**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se o Ativo foi atualizado com êxito.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Criar uma representação de ativo {#create-an-asset-rendition}

Criar uma representação para um ativo. Se o nome do parâmetro de solicitação não for fornecido, o nome do arquivo será usado como nome de representação.

**Parâmetros**: os parâmetros são `name` para o nome da representação e `file` como uma referência de arquivo.

**Solicitação**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de resposta**

* 201 - CRIADO - se a Representação foi criada com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Atualizar uma representação de ativo {#update-an-asset-rendition}

As atualizações substituem uma representação de ativo pelos novos dados binários.

**Solicitação**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se a Representação foi atualizada com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Adicionar um comentário em um ativo {#create-an-asset-comment}

**Parâmetros**: os parâmetros são `message` para o corpo da mensagem do comentário e `annotationData` para os dados de Anotação no formato JSON.

**Solicitação**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se o Comentário foi criado com sucesso.
* 404 - NÃO ENCONTRADO - se o ativo não puder ser encontrado ou acessado no URI fornecido.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Copiar uma pasta ou um ativo {#copy-a-folder-or-asset}

Copia uma pasta ou ativo disponível no caminho fornecido para um novo destino.

**Solicitar Cabeçalhos**: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para o qual copiar o recurso.
* `X-Depth` - `infinity` ou `0`. Usar `0` copia somente o recurso e suas propriedades, não seus filhos.
* `X-Overwrite` - Use `F` para impedir a substituição de um ativo no destino existente.

**Solicitação**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo foi copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo foi copiado para um destino existente.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Mover uma pasta ou um ativo {#move-a-folder-or-asset}

Move uma pasta ou ativo no caminho determinado para um novo destino.

**Solicitar Cabeçalhos**: Os parâmetros são:

* `X-Destination` - um novo URI de destino dentro do escopo da solução de API para o qual copiar o recurso.
* `X-Depth` - `infinity` ou `0`. Usar `0` copia somente o recurso e suas propriedades, não seus filhos.
* `X-Overwrite` - Use `T` para forçar a exclusão de um recurso existente ou `F` para impedir a substituição de um recurso existente.

**Solicitação**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos de resposta**: os códigos de resposta são:

* 201 - CRIADO - se a pasta/ativo foi copiado para um destino não existente.
* 204 - SEM CONTEÚDO - se a pasta/ativo foi copiado para um destino existente.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se um cabeçalho de solicitação estiver ausente.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Excluir uma pasta, um ativo ou uma representação {#delete-a-folder-asset-or-rendition}

Exclui um recurso (-tree) no caminho fornecido.

**Solicitação**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos de resposta**: os códigos de resposta são:

* 200 - OK - se a pasta foi excluída com sucesso.
* 412 - FALHA NA PRÉ-CONDIÇÃO - se a coleção raiz não puder ser encontrada ou acessada.
* 500 - ERRO INTERNO DO SERVIDOR - se algo der errado.

## Dicas, práticas recomendadas e limitações {#tips-limitations}

* Após o [!UICONTROL Tempo Desativado], um ativo e suas representações não estarão disponíveis por meio da interface da Web do [!DNL Assets] e da API HTTP. A API retorna a mensagem de erro 404 se o [!UICONTROL Momento da ativação] estiver no futuro ou o [!UICONTROL Momento da desativação] estiver no passado.

* A API HTTP do Assets não retorna os metadados completos. Os namespaces são codificados e somente esses namespaces são retornados. Para obter metadados completos, consulte o caminho do ativo `/jcr_content/metadata.json`.

* Algumas propriedades da pasta ou do ativo são mapeadas para um prefixo diferente quando atualizadas usando APIs. O prefixo `jcr` de `jcr:title`, `jcr:description` e `jcr:language` foi substituído pelo prefixo `dc`. Portanto, no JSON retornado, `dc:title` e `dc:description` contêm os valores de `jcr:title` e `jcr:description`, respectivamente.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publish Assets para AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documentos de referência do desenvolvedor para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
