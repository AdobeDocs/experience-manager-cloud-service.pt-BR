---
title: Lidar com grandes repositórios de conteúdo
description: Esta seção descreve o tratamento de repositórios de conteúdo grande
exl-id: 2eca7fa6-fb34-4b08-b3ec-4e9211e94275
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 1%

---

# Lidar com grandes repositórios de conteúdo {#handling-large-content-repositories}

## Visão geral {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Lidar com grandes repositórios de conteúdo"
>abstract="Para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service, a CTT pode aproveitar o AzCopy como uma etapa opcional de pré-cópia. Depois que essa pré-etapa é configurada, na fase de extração, o AzCopy copia blobs do Amazon S3 ou do Armazenamento Azure Blob para o armazenamento de blobs do conjunto de migração. Na fase de assimilação, o AzCopy copia blobs do armazenamento de blobs do conjunto de migração para o destino AEM armazenamento de blobs as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="Introdução ao AzCopy como uma etapa de pré-cópia"

A cópia de um grande número de blobs com a ferramenta Transferência de conteúdo (CTT) pode levar vários dias.
Para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service, a CTT pode aproveitar o [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como uma etapa opcional de pré-cópia. Essa etapa de pré-cópia pode ser usada quando a instância de AEM de origem está configurada para usar um armazenamento de dados Amazon S3 ou Azure Blob Storage.  Depois que essa pré-etapa é configurada, na fase de extração, o AzCopy copia blobs do Amazon S3 ou do Armazenamento Azure Blob para o armazenamento de blobs do conjunto de migração. Na fase de assimilação, o AzCopy copia blobs do armazenamento de blobs do conjunto de migração para o destino AEM armazenamento de blobs as a Cloud Service.

>[!NOTE]
> Essa funcionalidade foi introduzida na versão 1.5.4 do CTT.

## Considerações importantes antes de começar {#important-considerations}

Siga a seção abaixo para entender as considerações importantes antes de começar:

* A versão do AEM de origem precisa ser 6.3 - 6.5
* O armazenamento de dados de AEM de origem está configurado para usar o Amazon S3 ou o Armazenamento Azure Blob. Para obter mais detalhes, consulte [Configuração de armazenamentos de nó e armazenamentos de dados em AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).
* O armazenamento de dados inteiro será copiado durante a extração. Como há um custo associado à transferência de dados do Amazon S3 e do Armazenamento Azure Blob, o custo de transferência será relativo à quantidade total de dados no contêiner de armazenamento (referenciado em AEM ou não). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Armazenamento Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obter mais detalhes.
* Cada conjunto de migração copiará todo o armazenamento de dados, de modo que apenas um único conjunto de migração deverá ser usado.
* Você precisará de acesso para instalar [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) na instância (ou VM) que está executando a instância de origem AEM.
* Você precisará de um par de chaves de acesso e secretas para o bucket Amazon S3 de origem ou um URI SAS para o contêiner de armazenamento Azure Blob de origem (o acesso somente leitura está correto).
* A coleta de lixo do armazenamento de dados foi executada nos 7 dias anteriores na fonte. Para obter mais detalhes, consulte [Coleta de lixo do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).
* A maioria dos dados na instância de origem será incluída na migração.

## Configuração para usar o AzCopy como uma etapa de pré-cópia {#setting-up-pre-copy-step}

Siga esta seção para saber como configurar o AzCopy como uma etapa de pré-cópia com a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service:

### 0. Determine o tamanho total de todo o conteúdo no armazenamento de dados {#determine-total-size}

#### Armazenamento de dados do Azure Blob {#azure-blob-storage}

Na página de propriedades do contêiner no portal do Azure, use o botão **Calculate size** para determinar o tamanho de todo o conteúdo no contêiner. Por exemplo:

![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Armazenamento de dados do Amazon S3 {#amazon-data}

Você pode usar a guia Métricas do contêiner para determinar o tamanho de todo o conteúdo do contêiner. Por exemplo:


![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. Instale o AzCopy {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) O AzCopy é uma ferramenta de linha de comando fornecida pelo Microsoft que precisa estar disponível na instância de origem para habilitar esse recurso.

Resumindo, você provavelmente fará o download do binário x86-64 Linux da [página de documentos AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e o desmarcará para um local como /usr/bin. Anote onde colocou o binário, pois precisará do caminho completo para ele em uma etapa posterior.

### 2. Instale uma versão da ferramenta Transferência de conteúdo (CTT) com suporte ao AzCopy {#install-ctt-azcopy-support}

O suporte para AzCopy está incluído na versão CTT 1.5.4. Você pode baixar a versão mais recente da CTT no portal [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

### 3. Configurar um arquivo azcopy.config {#configure-azcopy-config-file}

Na instância do AEM de origem, em `crx-quickstart/cloud-migration`, crie um novo arquivo chamado azcopy.config .

O conteúdo desse arquivo de configuração será diferente, dependendo se a instância de AEM de origem usa um armazenamento de dados do Azure ou Amazon S3.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage-data}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar o azCopyPath e o azureSas corretos para sua instância).

>[!NOTE]
>
> Se preferir não conceder acesso de gravação ao contêiner de armazenamento de blob, você pode gerar um novo URI SAS que tenha somente permissões de Leitura e Lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Armazenamento de dados do Amazon S3 {#amazon-sdata-store}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar os valores corretos para sua instância).

>[!NOTE]
>
> Se a instância usar Funções do IAM para permitir que o AEM acesse S3, será necessário criar uma política e um usuário com as ações ListBucket e GetObject ativadas para o bucket S3. Depois de configurada, use a chave de acesso e a chave secreta deste usuário.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

### 4. Extrair com AzCopy {#extracting-azcopy}

Com o arquivo de configuração acima em vigor, a fase de pré-cópia do AzCopy será executada como parte de cada extração subsequente. Para evitar que ele seja executado, é possível renomear esse arquivo ou removê-lo.

1. Inicie uma extração da interface do usuário da CTT. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) e [Processo de extração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) para obter mais detalhes.

1. Confirme se a seguinte linha está impressa no log de extração:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Parabéns! Essa entrada de log significa que sua configuração foi considerada válida e que o AzCopy está copiando atualmente todos os blobs do contêiner de origem para o contêiner de migração.

As entradas de log do AzCopy serão exibidas no log de extração e terão o prefixo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pré-cópia]

>[!CAUTION]
>
> Durante os primeiros minutos de uma extração, observe os logs de extração cuidadosamente para verificar se há sinais de um problema. Como exemplo, aqui está o que seria registrado se o contêiner do Azure de origem não pudesse ser encontrado:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

No caso de um problema com o AzCopy, a extração falhará imediatamente, e os logs de extração conterão detalhes sobre a falha.

Quaisquer blobs copiados antes do erro serão ignorados automaticamente pelo AzCopy em execuções subsequentes e não precisarão ser copiados novamente.

### 5. Assimilar com o AzCopy {#ingesting-azcopy}

Com o lançamento da ferramenta Transferência de conteúdo 1.5.4, adicionamos suporte ao AzCopy à assimilação de autor.

>[!NOTE]
>A recomendação é executar a assimilação do autor primeiro sozinho. Isso irá acelerar a assimilação de Publicação quando for executada mais tarde.

Para aproveitar o AzCopy durante a assimilação, precisamos que você esteja em uma versão AEM as a Cloud Service que tenha pelo menos a versão 2021.6.5561.

Inicie a assimilação do autor da interface do usuário da CTT. Consulte o [Processo de assimilação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) para obter mais detalhes.
As entradas de log do AzCopy serão exibidas no log de assimilação. Eles terão esta aparência:

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## O que vem a seguir {#whats-next}

Depois de aprender a lidar com repositórios de conteúdo grande para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service, agora você está pronto para aprender o Processo de extração na ferramenta Transferência de conteúdo. Consulte [Extraindo conteúdo da origem na ferramenta Transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para saber como extrair o conjunto de migração da ferramenta Transferência de conteúdo.