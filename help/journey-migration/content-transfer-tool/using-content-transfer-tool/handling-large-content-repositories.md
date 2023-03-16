---
title: Lidar com grandes repositórios de conteúdo
description: Esta seção descreve o tratamento de repositórios de conteúdo grande
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: cf09c7774b633ae2cf1c5b28fee2bd8191d80bb3
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 8%

---

# Lidar com grandes repositórios de conteúdo {#handling-large-content-repositories}

## Visão geral {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Lidar com grandes repositórios de conteúdo"
>abstract="Para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service, a CTT pode aproveitar o AzCopy como uma etapa opcional de pré-cópia. Depois que essa etapa prévia for configurada, na fase de extração, o AzCopy copiará blobs do Amazon S3 ou do Armazenamento do Azure Blob para o armazenamento de blobs do conjunto de migração. Na fase de assimilação, o AzCopy copia os blobs do armazenamento de blobs do conjunto de migração para o armazenamento de blobs do AEM as a Cloud Service de destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR#setting-up-pre-copy-step" text="Introdução ao AzCopy como uma etapa de pré-cópia"

A cópia de um grande número de blobs com a ferramenta Transferência de conteúdo (CTT) pode levar vários dias.
Para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service, a CTT pode aproveitar [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como uma etapa opcional de pré-cópia. Essa etapa de pré-cópia pode ser usada quando a instância de AEM de origem está configurada para usar um armazenamento de dados Amazon S3, Armazenamento de dados Azure Blob ou Armazenamento de dados de arquivo. A etapa de pré-cópia é mais eficaz para a primeira extração e ingestão completas. No entanto, não é recomendado usar a pré-cópia para atualizações adicionais subsequentes (se o tamanho adicional for menor que 200 GB), pois isso pode adicionar tempo a todo o processo. Depois que essa pré-etapa é configurada, na fase de extração, o AzCopy copia blobs do Amazon S3, do Armazenamento Azure Blob ou do Armazenamento de dados do Arquivo para o armazenamento de blobs do conjunto de migração. Na fase de assimilação, o AzCopy copia os blobs do armazenamento de blobs do conjunto de migração para o armazenamento de blobs do AEM as a Cloud Service de destino.

## Considerações importantes antes de começar {#important-considerations}

Siga a seção abaixo para entender as considerações importantes antes de começar:

* A partir da versão 2.0.16 da CTT, a configuração da pré-cópia será feita automaticamente quando o pacote for instalado. Além disso, se o tamanho do conjunto de migração for maior que 200 GB, o processo de extração utilizará automaticamente o recurso de pré-cópia. O arquivo azcopy.config é criado no diretório crx-quickstart/cloud-migration/ . Você não precisa fazer manualmente a configuração de pré-cópia se estiver usando a versão 2.0.16 ou posterior da CTT.

* A versão de AEM de origem precisa ser 6.3 - 6.5.

* O armazenamento de dados de AEM de origem está configurado para usar o Amazon S3 ou o Armazenamento Azure Blob. Para obter mais detalhes, consulte [Configuração de armazenamentos de nó e armazenamentos de dados no AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* Cada conjunto de migração copiará todo o armazenamento de dados, de modo que apenas um único conjunto de migração deverá ser usado.

* Você precisará de acesso para instalar o [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) na instância (ou VM) que está executando a instância de AEM de origem.

* A coleta de lixo do armazenamento de dados foi executada nos 7 dias anteriores na fonte. Para obter mais detalhes, consulte [Coleta de lixo do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### Considerações adicionais se a instância de AEM de origem estiver configurada para usar um armazenamento de dados Amazon S3 ou Azure Blob {#additional-considerations-amazons3-azure}

* Como há um custo associado à transferência de dados do Amazon S3 e do Armazenamento Azure Blob, o custo de transferência será relativo à quantidade total de dados no contêiner de armazenamento existente (referenciado em AEM ou não). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Armazenamento Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obter mais detalhes.

* Você precisará de um par de chaves de acesso e secretas para o bucket Amazon S3 de origem existente ou de um URI SAS para o contêiner de armazenamento Azure Blob de origem existente (o acesso somente leitura está correto).

### Considerações adicionais se a instância de AEM de origem estiver configurada para usar o File Data Store {#additional-considerations-aem-instance-filedatastore}

* O sistema local deve ter espaço livre estritamente maior que 1/256 do armazenamento de dados de origem. Por exemplo, se o tamanho do armazenamento de dados for de 3 TB, deverá existir espaço livre maior que 11,72 GB no `crx-quickstart/cloud-migration` pasta na origem do AzCopy para funcionar. No mínimo, o sistema de origem deve ter 1 GB de espaço livre. O espaço livre pode ser obtido usando `df -h` em instâncias Linux e comando dir nas instâncias do Windows.

* Toda vez que a extração é executada com o AzCopy ativado, o armazenamento de dados de arquivo inteiro é nivelado e copiado para o contêiner de migração de nuvem. Se o seu conjunto de migração for significativamente menor do que o tamanho do seu armazenamento de dados, a extração do AzCopy não será a abordagem ideal.

* Depois que o AzCopy for usado para copiar sobre o armazenamento de dados existente, desative-o para extrações delta ou adicionais.

## Configuração para usar o AzCopy como uma etapa de pré-cópia {#setting-up-pre-copy-step}

>[!NOTE]
>A partir da versão 2.0.16 da CTT, a configuração da pré-cópia será feita automaticamente quando o pacote for instalado. Além disso, se o tamanho do conjunto de migração for maior que 200 GB, o processo de extração utilizará automaticamente o recurso de pré-cópia. O arquivo azcopy.config é criado no diretório crx-quickstart/cloud-migration/ . Se quiser atualizar a configuração do arquivo manualmente, reveja as seções abaixo.

Siga esta seção para saber como configurar o AzCopy como uma etapa de pré-cópia com a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service:

### 0. Determine o tamanho total de todo o conteúdo no armazenamento de dados {#determine-total-size}

É importante determinar o tamanho total do armazenamento de dados por dois motivos:

* Se a AEM de origem estiver configurada para usar o File data store, o sistema local deverá ter espaço livre estritamente maior que 1/256 do tamanho do armazenamento de dados de origem.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage}

Na página de propriedades do contêiner existente no portal do Azure, use o **Calcular tamanho** para determinar o tamanho de todo o conteúdo no container. Por exemplo:

![imagem](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Armazenamento de dados do Amazon S3 {#amazon-data}

Você pode usar a guia Métricas do contêiner para determinar o tamanho de todo o conteúdo do contêiner. Por exemplo:


![imagem](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Armazenamento de dados do arquivo {#file-data-store-determine-size}

* Para mac, sistemas UNIX, execute o comando du no diretório do armazenamento de dados para obter seu tamanho:
   `du -sh [path to datastore on the instance]`. Por exemplo, se o armazenamento de dados estiver localizado em `/mnt/author/crx-quickstart/repository/datastore`, o seguinte comando obterá o tamanho: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* No Windows, use o comando dir no diretório do armazenamento de dados para obter o tamanho:
   `dir /a/s [location of datastore]`.

### 1. Instale o AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) é uma ferramenta de linha de comando fornecida pelo Microsoft que precisa estar disponível na instância de origem para habilitar esse recurso.

Em resumo, você provavelmente fará o download do binário x86-64 do Linux na [Página de documentos do AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e desmarque-o em um local como /usr/bin.

>[!IMPORTANT]
>Anote onde colocou o binário, pois precisará do caminho completo para ele em uma etapa posterior.

### 2. Instale a versão da Ferramenta de transferência de conteúdo (CTT) com o suporte ao AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>A versão mais recente da CTT deve ser usada.

O suporte do AzCopy para Amazon S3, Armazenamento Azure Blob e Armazenamento de dados de arquivo está incluído na versão mais recente do CTT.
Você pode baixar a versão mais recente da CTT no [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.
Observe que somente as versões 2.0.0 e superior serão compatíveis e é aconselhável usar a versão mais recente.

### 3. Configurar um arquivo azcopy.config {#configure-azcopy-config-file}

Na instância do AEM de origem, em `crx-quickstart/cloud-migration`, crie um novo arquivo chamado `azcopy.config`.

>[!NOTE]
>O conteúdo desse arquivo de configuração será diferente, dependendo se a instância de AEM de origem usa um armazenamento de dados ou um armazenamento de dados do Azure ou Amazon S3.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage-data}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar o azCopyPath e o azureSas corretos para sua instância).

>[!NOTE]
>
> Se preferir não conceder acesso de gravação ao contêiner de armazenamento de blob existente, você poderá gerar um novo URI SAS que tenha somente permissões de Leitura e Lista.

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

#### Armazenamento de dados do arquivo {#file-data-store-azcopy-config}

Seu `azcopy.config` O arquivo deve conter a propriedade azCopyPath e uma propriedade repository.home opcional que aponte para o local do armazenamento de dados do arquivo. Use os valores corretos para sua instância.
Armazenamento de dados do arquivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

A propriedade azCopyPath deve conter o caminho completo do local onde a ferramenta de linha de comando azCopy está instalada na instância de AEM de origem. Se a propriedade azCopyPath estiver ausente, a etapa de pré-cópia do blob não será executada.

If `repository.home` A propriedade está ausente do azcopy.config, em seguida, o local padrão do armazenamento de dados `/mnt/crx/author/crx-quickstart/repository/datastore` será usada para executar a pré-cópia.

### 4. Extrair com AzCopy {#extracting-azcopy}

Com o arquivo de configuração acima em vigor, a fase de pré-cópia do AzCopy será executada como parte de cada extração subsequente. Para evitar que ele seja executado, é possível renomear esse arquivo ou removê-lo.

>[!NOTE]
>Se o AzCopy não estiver configurado corretamente, você verá esta mensagem nos logs:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie uma extração da interface do usuário da CTT. Consulte [Introdução à ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) e [Processo de extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obter mais detalhes.

1. Confirme se a seguinte linha está impressa no log de extração:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Parabéns! Essa entrada de log significa que sua configuração foi considerada válida e que o AzCopy está copiando atualmente todos os blobs do contêiner de origem para o contêiner de migração.

As entradas de log do AzCopy serão exibidas no log de extração e terão o prefixo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pré-cópia do AzCopy]

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

#### Para armazenamento de dados de arquivo {#file-data-store-extract}

Quando o AzCopy está em execução para o arquivo de origem dataStore, você deve ver mensagens como essas nos logs indicando que as pastas estão sendo processadas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Assimilar com o AzCopy {#ingesting-azcopy}

Consulte [Inserção de conteúdo ao Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
para obter informações gerais sobre como assimilar conteúdo no target pelo Cloud Acceleration Manager (CAM), incluindo instruções sobre como usar ou não o AzCopy (pré-cópia), na caixa de diálogo &quot;Nova assimilação&quot;.

Para aproveitar o AzCopy durante a assimilação, precisamos que você esteja em uma versão AEM as a Cloud Service que tenha pelo menos a versão 2021.6.5561.

Consulte a lista &quot;Tarefas de assimilação&quot; no Cloud Acceleration Manager e os registros da assimilação para ver o progresso.  As entradas de log relacionadas às tarefas bem-sucedidas do AzCopy serão exibidas da seguinte maneira (permitindo algumas diferenças). Verificar os registros ocasionalmente pode alertá-lo para problemas antecipadamente e ajudá-lo a encontrar uma solução rápida para qualquer problema.

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

Depois de aprender a lidar com repositórios de conteúdo grande para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para AEM as a Cloud Service, agora você está pronto para aprender o Processo de extração usando a ferramenta Transferência de conteúdo. Consulte [Extrair conteúdo da origem na ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para saber como extrair seu conjunto de migração da ferramenta Transferência de conteúdo.
