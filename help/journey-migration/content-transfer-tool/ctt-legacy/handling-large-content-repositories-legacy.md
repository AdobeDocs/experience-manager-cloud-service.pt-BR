---
title: Lidar com grandes repositórios de conteúdo (herdados)
description: Esta seção descreve a manipulação de grandes repositórios de conteúdo
hide: true
hidefromtoc: true
exl-id: 19021f40-d0a5-4e0c-a213-c421338cedeb
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 2%

---

# Lidar com grandes repositórios de conteúdo (herdados) {#handling-large-content-repositories}

## Visão geral {#overview}

A cópia de um grande número de blobs com a Ferramenta de transferência de conteúdo (CTT) pode levar vários dias.
Para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service, a CTT pode aproveitar [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como uma etapa opcional de pré-cópia. Essa etapa de pré-cópia pode ser usada quando a instância do AEM de origem é configurada para usar um armazenamento de dados Amazon S3, Azure Blob Storage ou File Data Store. Depois que essa pré-etapa for configurada, na fase de extração, o AzCopy copia blobs do Amazon S3, do Armazenamento de blobs do Azure ou do Armazenamento de dados do arquivo para o armazenamento de blobs do conjunto de migração. Na fase de assimilação, o AzCopy copia blobs do armazenamento de blob do conjunto de migração para o armazenamento de blob do AEM de destino as a Cloud Service.

>[!NOTE]
> Essa funcionalidade foi introduzida na versão 1.5.4 da CTT.

## Considerações importantes antes de começar {#important-considerations}

Siga a seção abaixo para entender as considerações importantes antes de iniciar:

* A versão do AEM de origem precisa ser 6.3 - 6.5.

* O armazenamento de dados do AEM de origem é configurado para usar o Amazon S3 ou o Armazenamento de Blobs do Azure. Para obter mais detalhes, consulte [Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* Cada conjunto de migração copiará todo o armazenamento de dados, de modo que somente um único conjunto de migração deve ser usado.

* Você precisará de acesso para instalar o [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) na instância (ou VM) que executa a instância do AEM de origem.

* A Coleta de Lixo do Armazenamento de Dados foi executada nos 7 dias anteriores na origem. Para obter mais detalhes, consulte [Coleta de lixo do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).


### Considerações adicionais se a instância do AEM de origem estiver configurada para usar um armazenamento de dados Amazon S3 ou Azure Blob {#additional-considerations-amazons3-azure}

* Como há um custo associado à transferência de dados do Amazon S3 e do Armazenamento de blobs do Azure, o custo de transferência será relativo à quantidade total de dados no contêiner de armazenamento (seja referenciado no AEM ou não). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Armazenamento Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obter mais detalhes.

* Você precisará de um par de chave de acesso e chave secreta para o bucket do Amazon S3 de origem ou de um URI SAS para o contêiner do Armazenamento de Blobs do Azure de origem (o acesso somente leitura está correto).

### Considerações adicionais se a instância AEM de origem estiver configurada para usar o Armazenamento de dados de arquivo {#additional-considerations-aem-instance-filedatastore}

* O sistema local deve ter espaço livre estritamente maior que o tamanho 1/256 do armazenamento de dados de origem. Por exemplo, se o tamanho do armazenamento de dados for de 3 TB, deverá existir espaço livre maior que 11,72 GB no `crx-quickstart/cloud-migration` na origem para que o AzCopy funcione. No mínimo, o sistema de origem deve ter 1 GB de espaço livre. O espaço livre pode ser obtido usando `df -h` comando nas instâncias do Linux e comando dir nas instâncias do Windows.

* Cada vez que a extração é executada com o AzCopy ativado, todo o armazenamento de dados do arquivo é nivelado e copiado para o contêiner de migração na nuvem. Se o conjunto de migração for significativamente menor que o tamanho do armazenamento de dados, a extração do AzCopy não será a abordagem ideal.

* Depois que o AzCopy for usado para copiar o armazenamento de dados, desative-o para extrações delta ou complementares.

## Configuração do para usar o AzCopy como uma etapa de pré-cópia {#setting-up-pre-copy-step}

Siga esta seção para saber como configurar o para usar o AzCopy como uma etapa de pré-cópia com a Ferramenta de transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service:

### 0. Determine o tamanho total de todo o conteúdo no armazenamento de dados {#determine-total-size}

É importante determinar o tamanho total do armazenamento de dados por dois motivos:

* Se o AEM de origem estiver configurado para usar o Armazenamento de dados do arquivo, o sistema local deve ter espaço livre estritamente maior que o tamanho 1/256 do armazenamento de dados de origem.

* Conhecer o tamanho total do armazenamento de dados ajudará a estimar os tempos de extração e assimilação. Use o [Calculador de ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) para obter uma estimativa dos tempos de extração e assimilação.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage}

Na página de propriedades do container no portal do Azure, use o **Calcular tamanho** botão para determinar o tamanho de todo o conteúdo no container. Por exemplo:

![imagem](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Armazenamento de dados Amazon S3 {#amazon-data}

Você pode usar a guia Métricas do container para determinar o tamanho de todo o conteúdo no container. Por exemplo:


![imagem](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Armazenamento de dados do arquivo {#file-data-store-determine-size}

* Para sistemas mac, UNIX, execute o comando du no diretório do armazenamento de dados para obter seu tamanho:
   `du -sh [path to datastore on the instance]`. Por exemplo, se o armazenamento de dados estiver localizado em `/mnt/author/crx-quickstart/repository/datastore`, o comando a seguir fornecerá o tamanho: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* No Windows, use o comando dir no diretório do armazenamento de dados para obter seu tamanho:
   `dir /a/s [location of datastore]`.

### 1. Instalar o AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) é uma ferramenta de linha de comando fornecida pelo Microsoft que precisa estar disponível na instância de origem para habilitar esse recurso.

Em resumo, você provavelmente desejará fazer o download do binário x86-64 do Linux a partir do [Página de documentos do AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e remova-o do tar para um local como /usr/bin.

>[!IMPORTANT]
>Anote onde você colocou o binário, pois precisará do caminho completo para ele em uma etapa posterior.

### 2. Instale uma versão da Ferramenta de transferência de conteúdo (CTT) com suporte ao AzCopy {#install-ctt-azcopy-support}

O suporte do AzCopy para Amazon S3 e Armazenamento Azure Blob está incluído na versão CTT 1.5.4.
O suporte para o File Data Store está incluído na versão CTT 1.7.2. Você pode baixar a versão mais recente da CTT no [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.


### 3. Configurar um arquivo azcopy.config {#configure-azcopy-config-file}

Na instância do AEM de origem, em `crx-quickstart/cloud-migration`, crie um novo arquivo chamado `azcopy.config`.

>[!NOTE]
>O conteúdo desse arquivo de configuração será diferente se a instância do AEM de origem usar um armazenamento de dados do Azure ou do Amazon S3 ou um armazenamento de dados do arquivo.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage-data}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar o azCopyPath e o azureSas corretos para sua instância).

>[!NOTE]
>
> Se você preferir não conceder acesso de gravação ao contêiner de armazenamento de blobs, poderá gerar um novo URI SAS que tem somente permissões de Leitura e Lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Armazenamento de dados Amazon S3 {#amazon-sdata-store}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar os valores corretos para sua instância).

>[!NOTE]
>
> Se sua instância usar Funções IAM para permitir que o AEM acesse S3, será necessário criar uma política e um usuário com as ações ListBucket e GetObject ativadas para o bucket S3. Depois de configurada, use a chave de acesso e a chave secreta deste usuário.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Armazenamento de dados do arquivo {#file-data-store-azcopy-config}

Seu `azcopy.config` o arquivo deve conter a propriedade azcopyPath e uma propriedade repository.home opcional que aponta para o local do armazenamento de dados do arquivo. Use os valores corretos para sua instância.
Armazenamento de dados do arquivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

A propriedade azcopyPath deve conter o caminho completo do local em que a ferramenta de linha de comando azCopy está instalada na instância AEM de origem. Se a propriedade azCopyPath estiver ausente, a etapa de pré-cópia do blob não será executada.

Se `repository.home` a propriedade está ausente em azcopy.config, em seguida, o local do armazenamento de dados padrão `/mnt/crx/author/crx-quickstart/repository/datastore` será usado para executar a pré-cópia.

### 4. Extrair com o AzCopy {#extracting-azcopy}

Com o arquivo de configuração acima em vigor, a fase de pré-cópia do AzCopy será executada como parte de cada extração subsequente. Para impedir a execução, você pode renomear ou remover este arquivo.

>[!NOTE]
>Se o AzCopy não estiver configurado corretamente, você verá esta mensagem nos logs:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie uma extração da interface da CTT. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) e a variável [Processo de extração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=pt-BR) para obter mais detalhes.

1. Confirme se a seguinte linha está impressa no log de extração:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Parabéns! Essa entrada de log significa que sua configuração foi considerada válida e que o AzCopy está copiando todos os blobs do container de origem para o container de migração no momento.

As entradas de log do AzCopy aparecerão no log de extração e terão o prefixo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pré-cópia do AzCopy]

>[!CAUTION]
>
> Durante os primeiros minutos de uma extração, observe os logs de extração atentamente para verificar se há algum sinal de um problema. Como exemplo, veja o que seria registrado se o contêiner do Azure de origem não fosse encontrado:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Caso ocorra um problema com o AzCopy, a extração falhará imediatamente e os logs de extração conterão detalhes sobre a falha.

Quaisquer blobs copiados antes do erro serão ignorados automaticamente pelo AzCopy nas execuções subsequentes e não precisarão ser copiados novamente.

#### Para Armazenamento de Dados de Arquivo {#file-data-store-extract}

Quando o AzCopy estiver em execução para o arquivo de origem dataStore, você deverá ver mensagens como essas nos registros, indicando que as pastas estão sendo processadas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Assimilar com AzCopy {#ingesting-azcopy}

Com o lançamento da Ferramenta de transferência de conteúdo 1.5.4, adicionamos o suporte ao AzCopy à assimilação do autor.

>[!NOTE]
>A recomendação é executar a Assimilação do autor primeiro sozinho. Isso irá acelerar a Assimilação de publicação quando for executado posteriormente.

Para aproveitar o AzCopy durante a assimilação, é necessário estar em uma versão as a Cloud Service do AEM que seja, pelo menos, a versão 2021.6.5561.

Comece a assimilação do autor da interface da CTT. Consulte a [Processo de assimilação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=pt-BR) para obter mais detalhes.
As entradas de log do AzCopy aparecerão no log de assimilação. Eles serão assim:

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

## Desativar AzCopy {#disable-azcopy}

Para desativar o AzCopy, renomeie ou exclua o `azcopy.config` arquivo.

Por exemplo, a extração do azcopy pode ser desativada com: `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## O que vem a seguir {#whats-next}

Depois de aprender a lidar com grandes repositórios de conteúdo para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service, agora você está pronto para aprender o processo de extração na ferramenta Transferência de conteúdo. Consulte [Extração de conteúdo da origem na ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para saber como extrair seu conjunto de migração da ferramenta Transferência de conteúdo.
