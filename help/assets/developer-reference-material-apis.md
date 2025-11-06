---
title: Referências de desenvolvedor para  [!DNL Assets]
description: O conteúdo de referências de desenvolvedor e APIs do [!DNL Assets] permite gerenciar ativos, incluindo arquivos binários, metadados, representações, comentários e informações [!DNL Content Fragments].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets] casos de uso de desenvolvedores, APIs e material de referência {#assets-cloud-service-apis}

O artigo contém recomendações, materiais de referência e recursos para desenvolvedores do [!DNL Assets] as a [!DNL Cloud Service]. Ele inclui um novo módulo de upload de ativos, referência de API e informações sobre o suporte fornecido em workflows de pós-processamento.

## [!DNL Experience Manager Assets] APIs e operações {#use-cases-and-apis}

O [!DNL Assets] as a [!DNL Cloud Service] fornece várias APIs para interagir programaticamente com ativos digitais. Cada API é compatível com casos de uso específicos, conforme mencionado na tabela abaixo. A interface de usuário [!DNL Assets], o aplicativo de desktop [!DNL Experience Manager] e o [!DNL Adobe Asset Link] oferecem suporte a todas ou algumas das operações.

>[!CAUTION]
>
>Algumas APIs continuam a existir, mas não são ativamente compatíveis (indicadas com um ×). Na medida do possível, não use essas APIs.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| × | Não suportado. Não use. |
| - | Não disponível |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | APIs Java [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | [Serviço de computação do ativo](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binário original** |  |  |  |  |  |  |
| Criar original | ✓ | × | - | × | × | - |
| Ler original | - | × | ✓ | ✓ | ✓ | - |
| Atualizar original | ✓ | × | ✓ | × | × | - |
| Excluir original | - | ✓ | - | ✓ | ✓ | - |
| Copiar original | - | ✓ | - | ✓ | ✓ | - |
| Mover original | - | ✓ | - | ✓ | ✓ | - |
| **Metadados** |  |  |  |  |  |  |
| Criar metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Ler metadados | - | ✓ | - | ✓ | ✓ | - |
| Atualizar metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Excluir metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Copiar metadados | - | ✓ | - | ✓ | ✓ | - |
| Mover metadados | - | ✓ | - | ✓ | ✓ | - |
| **Fragmentos de conteúdo (CF)** |  |  |  |  |  |  |
| Criar CF | - | ✓ | - | ✓ | - | - |
| Ler CF | - | ✓ | - | ✓ | - | ✓ |
| Atualizar CF | - | ✓ | - | ✓ | - | - |
| Excluir CF | - | ✓ | - | ✓ | - | - |
| Copiar CF | - | ✓ | - | ✓ | - | - |
| Mover CF | - | ✓ | - | ✓ | - | - |
| **Versões** |  |  |  |  |  |  |
| Criar versão | ✓ | ✓ | - | - | - | - |
| Versão de leitura | - | ✓ | - | - | - | - |
| Excluir versão | - | ✓ | - | - | - | - |
| **Pastas** |  |  |  |  |  |  |
| Criar pasta | ✓ | ✓ | - | ✓ | - | - |
| Ler pasta | - | ✓ | - | ✓ | - | - |
| Excluir pasta | ✓ | ✓ | - | ✓ | - | - |
| Copiar pasta | ✓ | ✓ | - | ✓ | - | - |
| Mover pasta | ✓ | ✓ | - | ✓ | - | - |

## Upload de ativo {#asset-upload}

No [!DNL Experience Manager] as a [!DNL Cloud Service], você pode carregar os ativos diretamente no armazenamento na nuvem usando a API HTTP. As etapas para fazer upload de um arquivo binário estão abaixo. Execute essas etapas em um aplicativo externo e não no JVM do [!DNL Experience Manager].

1. [Enviar uma solicitação HTTP](#initiate-upload). Ele informa à implantação do [!DNL Experience Manage]r sua intenção de carregar um novo binário.
1. [PUT o conteúdo do binário](#upload-binary) para um ou mais URIs fornecidos pela solicitação de iniciação.
1. [Enviar uma solicitação HTTP](#complete-upload) para informar ao servidor que o conteúdo do binário foi carregado com êxito.

![Visão geral do protocolo de carregamento binário direto](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>Execute as etapas acima em um aplicativo externo e não na JVM [!DNL Experience Manager].

A abordagem oferece uma manipulação escalável e mais eficiente de uploads de ativos. As diferenças em comparação ao [!DNL Experience Manager] 6.5 são:

* Os binários não passam pelo [!DNL Experience Manager], que agora simplesmente coordena o processo de carregamento com o armazenamento em nuvem binário configurado para a implantação.
* O armazenamento na nuvem binário funciona com uma rede de entrega de conteúdo (CDN) ou uma rede Edge. Um CDN seleciona um endpoint de upload mais próximo de um cliente. Quando os dados percorrem uma distância menor até um terminal próximo, o desempenho do upload e a experiência do usuário melhoram, especialmente para equipes distribuídas geograficamente.

>[!NOTE]
>
>Consulte o código de cliente para implementar esta abordagem na [biblioteca aem-upload](https://github.com/adobe/aem-upload) de código aberto.
>
>[!IMPORTANT]
>
>Em determinadas circunstâncias, as alterações podem não se propagar totalmente entre as solicitações para o Experience Manager, devido à natureza consistente do armazenamento no Cloud Service. Isso faz com que 404 respostas iniciem ou concluam chamadas de upload porque as criações de pasta necessárias não são propagadas. Os clientes devem esperar respostas 404 e lidar com elas implementando uma nova tentativa com uma estratégia de retirada.

### Iniciar upload {#initiate-upload}

Envie uma solicitação POST HTTP para a pasta desejada. Os Assets são criados ou atualizados nesta pasta. Inclua o seletor `.initiateUpload.json` para indicar que a solicitação é para iniciar o carregamento de um arquivo binário. Por exemplo, o caminho para a pasta onde o ativo deve ser criado é `/assets/folder`. A solicitação POST é `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

O tipo de conteúdo do corpo da solicitação deve ser de dados de formulário `application/x-www-form-urlencoded`, contendo os seguintes campos:

* `(string) fileName`: Obrigatório. O nome do ativo como ele aparece em [!DNL Experience Manager].
* `(number) fileSize`: Obrigatório. O tamanho do arquivo, em bytes, do ativo que está sendo carregado.

Uma única solicitação pode ser usada para iniciar uploads para vários binários, desde que cada binário contenha os campos obrigatórios. Se for bem-sucedida, a solicitação responderá com um código de status `201` e um corpo contendo dados JSON no seguinte formato:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (cadeia de caracteres): Chame este URI quando o binário terminar de carregar. O URI pode ser um URI absoluto ou relativo, e os clientes devem ser capazes de lidar com ambos. Ou seja, o valor pode ser `"https://[aem_server]:[port]/content/dam.completeUpload.json"` ou `"/content/dam.completeUpload.json"` Consulte [concluir o carregamento](#complete-upload).
* `folderPath` (cadeia de caracteres): Caminho completo para a pasta na qual o binário é carregado.
* `(files)` (matriz): uma lista de elementos cujo comprimento e ordem correspondem ao comprimento e à ordem da lista de informações binárias fornecidas na solicitação de inicialização.
* `fileName` (cadeia de caracteres): o nome do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `mimeType` (cadeia de caracteres): o tipo mime do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `uploadToken` (cadeia de caracteres): um token de carregamento para o binário correspondente. Esse valor deve ser incluído na solicitação completa.
* `uploadURIs` (matriz): uma lista de cadeias de caracteres cujos valores são URIs completos para os quais o conteúdo binário deve ser carregado (consulte [Carregar binário](#upload-binary)).
* `minPartSize` (número): O comprimento mínimo, em bytes, dos dados que podem ser fornecidos a qualquer um dos `uploadURIs`, se houver mais de um URI.
* `maxPartSize` (número): O comprimento máximo, em bytes, dos dados que podem ser fornecidos a qualquer um dos `uploadURIs`, se houver mais de um URI.

### Carregar binário {#upload-binary}

A saída de iniciar um upload inclui um ou mais valores de URI de upload. Se mais de um URI for fornecido, o cliente poderá dividir o binário em partes e fazer solicitações PUT de cada parte para os URIs de upload fornecidos, em ordem. Se você optar por dividir o binário em partes, siga as seguintes diretrizes:

* Cada parte, com exceção da última, deve ter um tamanho maior ou igual a `minPartSize`.
* Cada parte deve ter um tamanho menor ou igual a `maxPartSize`.
* Se o tamanho do binário exceder `maxPartSize`, divida o binário em partes para carregá-lo.
* Você não precisa usar todos os URIs.

Se o tamanho do binário for menor ou igual a `maxPartSize`, você poderá carregar todo o binário em um único URI de carregamento. Se mais de um URI de upload for fornecido, use o primeiro e ignore o restante. Você não precisa usar todos os URIs.

Os nós de borda CDN ajudam a acelerar o upload solicitado de binários.

A maneira mais fácil de fazer isso é usar o valor de `maxPartSize` como tamanho da peça. O contrato da API garante que haja URIs de upload suficientes para carregar seu binário se você usar esse valor como tamanho da peça. Para fazer isso, divida o binário em partes do tamanho `maxPartSize`, usando um URI para cada parte, em ordem. A parte final pode ser de qualquer tamanho menor ou igual a `maxPartSize`. Por exemplo, suponha que o tamanho total do binário seja 20.000 bytes, o `minPartSize` seja 5.000 bytes, `maxPartSize` seja 8.000 bytes e o número de URIs de upload seja 5. Execute as seguintes etapas:

* Carregue os primeiros 8.000 bytes do binário usando o primeiro URI de upload.
* Carregue os segundos 8.000 bytes do binário usando o segundo URI de upload.
* Carregue os últimos 4.000 bytes do binário usando o terceiro URI de upload. Como esta é a parte final, ela não precisa ser maior que `minPartSize`.
* Não é necessário usar os dois últimos URIs de upload. Você pode ignorá-los.

Um erro comum é calcular o tamanho da parte com base no número de URIs de upload fornecidos pela API. O contrato de API não garante que essa abordagem funcione e pode na verdade resultar em tamanhos de partes que estão fora do intervalo entre `minPartSize` e `maxPartSize`. Isso pode resultar em falhas binárias de upload.

Novamente, a maneira mais fácil e segura é simplesmente usar partes com tamanho igual a `maxPartSize`.

Se o carregamento for bem-sucedido, o servidor responderá a cada solicitação com um código de status `201`.

>[!NOTE]
>
>Para obter mais informações sobre o algoritmo de carregamento, consulte a [documentação oficial sobre recursos](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) e a [documentação sobre API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) no projeto Apache Jackrabbit Oak.

### Carregamento completo {#complete-upload}

Depois que todas as partes de um arquivo binário forem carregadas, envie uma solicitação HTTP POST para o URI completo fornecido pelos dados de iniciação. O tipo de conteúdo do corpo da solicitação deve ser `application/x-www-form-urlencoded` dados de formulário, contendo os seguintes campos.

| Campos | Tipo | Obrigatório ou não | Descrição |
|---|---|---|---|
| `fileName` | String | Obrigatório | O nome do ativo, conforme fornecido pelos dados de iniciação. |
| `mimeType` | String | Obrigatório | O tipo de conteúdo HTTP do binário, como foi fornecido pelos dados de iniciação. |
| `uploadToken` | String | Obrigatório | Token de upload para o binário, conforme fornecido pelos dados de iniciação. |
| `createVersion` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, [!DNL Experience Manager] cria uma nova versão do ativo. |
| `versionLabel` | String | Opcional | Se uma nova versão for criada, o rótulo associado à nova versão de um ativo. |
| `versionComment` | String | Opcional | Se uma nova versão for criada, os comentários associados à versão. |
| `replace` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, [!DNL Experience Manager] exclui o ativo e o recria. |
| `uploadDuration` | Número | Opcional | O tempo total, em milissegundos, pelo qual o arquivo será carregado em sua totalidade. Se especificada, a duração do upload é incluída nos arquivos de log do sistema para análise da taxa de transferência. |
| `fileSize` | Número | Opcional | O tamanho, em bytes, do arquivo. Se especificado, o tamanho do arquivo é incluído nos arquivos de log do sistema para análise de taxa de transferência. |

>[!NOTE]
>
>Se o ativo existir e `createVersion` ou `replace` não for especificado, [!DNL Experience Manager] atualizará a versão atual do ativo com o novo binário.

Assim como no processo inicial, os dados completos da solicitação podem conter informações de mais de um arquivo.

O processo de carregar um binário não é concluído até que o URL completo seja chamado para o arquivo. Um ativo é processado após a conclusão do processo de upload. O processamento não é iniciado mesmo se o arquivo binário do ativo for carregado completamente, mas o processo de upload não for concluído. Se o carregamento for bem-sucedido, o servidor responderá com um código de status `200`.

### Exemplo de script de shell para carregar ativos ao AEM as a Cloud Service {#upload-assets-shell-script}

O processo de carregamento em várias etapas para acesso binário direto no AEM as a Cloud Service está ilustrado no seguinte exemplo de shell-script `aem-upload.sh`:

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### Biblioteca de upload de código aberto {#open-source-upload-library}

Para saber mais sobre os algoritmos de upload ou criar seus próprios scripts e ferramentas de upload, o Adobe fornece bibliotecas e ferramentas de código aberto:

* [Biblioteca de upload do aem de código aberto](https://github.com/adobe/aem-upload).
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
>A biblioteca aem-upload e a ferramenta de linha de comando usam a [biblioteca node-httptransfer](https://github.com/adobe/node-httptransfer/)

### APIs de upload de ativos obsoletos {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

O novo método de carregamento só tem suporte para [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. As APIs do [!DNL Adobe Experience Manager] 6.5 estão obsoletas. Os métodos relacionados a fazer upload ou atualizar ativos ou representações (qualquer upload binário) foram descontinuados nas seguintes APIs:

* [API HTTP do Experience Manager Assets](mac-api-assets.md)
* API Java `AssetManager`, como `AssetManager.createAsset(..)`, `AssetManager.createAssetForBinary(..)`, `AssetManager.getAssetForBinary(..)`, `AssetManager.removeAssetForBinary(..)`, `AssetManager.createOrUpdateAsset(..)`, `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [Biblioteca de upload do aem de código aberto](https://github.com/adobe/aem-upload).
>* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).
>* [Documentação do Apache Jackrabbit Oak para carregamento direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## Fluxos de trabalho de processamento e pós-processamento de ativos {#post-processing-workflows}

Em [!DNL Experience Manager], o processamento de ativos é baseado na configuração **[!UICONTROL Processando Perfis]** que usa [microsserviços de ativos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). O processamento não requer extensões de desenvolvedor.

Para configuração de fluxo de trabalho de pós-processamento, use os fluxos de trabalho padrão com extensões com etapas personalizadas.

## Suporte a etapas de fluxo de trabalho no fluxo de trabalho de pós-processamento {#post-processing-workflows-steps}

Se você atualizar de uma versão anterior do [!DNL Experience Manager], poderá usar os microsserviços de ativos para processar ativos. Os microsserviços de ativos nativos em nuvem são mais simples de configurar e usar. Algumas etapas de fluxo de trabalho usadas no fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] na versão anterior não são compatíveis. Para obter mais informações sobre classes suportadas, consulte a [Referência da API Java ou Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Os seguintes modelos de fluxo de trabalho técnico são substituídos por microsserviços de ativos ou o suporte não está disponível:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
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
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).