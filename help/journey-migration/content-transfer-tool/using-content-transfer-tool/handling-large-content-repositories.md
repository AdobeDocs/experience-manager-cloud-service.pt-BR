---
title: Lidar com grandes repositórios de conteúdo
description: Esta seção descreve a manipulação de grandes repositórios de conteúdo
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
feature: Migration
role: Admin
source-git-commit: b729c07c78519cd9b6536a0dd142aa8ed01d2a22
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 7%

---

# Lidar com grandes repositórios de conteúdo {#handling-large-content-repositories}

## Visão geral {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Lidar com grandes repositórios de conteúdo"
>abstract="Para acelerar significativamente as fases de extração e ingestão da atividade de transferência de conteúdo e mover conteúdo para o AEM as a Cloud Service, a Ferramenta de Transferência de Conteúdo (CTT) pode usar o AzCopy como uma etapa opcional de pré-cópia. Depois que essa etapa prévia for configurada, na fase de extração, o AzCopy copiará blobs do Amazon S3 ou do Armazenamento de blobs do Azure para o armazenamento de blobs do conjunto de migração. Na fase de ingestão, o AzCopy copia os blobs do armazenamento de blobs do conjunto de migração para o armazenamento de blobs do AEM as a Cloud Service de destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR#setting-up-pre-copy-step" text="Introdução ao AzCopy como etapa de pré-cópia"

A cópia de muitos blobs com a Ferramenta de transferência de conteúdo (CTT) pode levar vários dias.
Para acelerar as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service, a CTT pode usar o [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como etapa opcional de pré-cópia. Essa etapa de pré-cópia pode ser usada quando a instância do AEM de origem é configurada para usar um armazenamento de dados do Amazon S3, do Azure Blob Storage ou do File Data Store. A etapa de pré-cópia é mais eficaz para a primeira extração e assimilação completas. No entanto, o uso da pré-cópia para os complementos subsequentes não é recomendado (se o tamanho do complemento for inferior a 200 GB), pois pode adicionar tempo a todo o processo. Depois que essa pré-etapa for configurada, na fase de extração, o AzCopy copia blobs do Amazon S3, do Armazenamento de blobs do Azure ou do Armazenamento de dados do arquivo para o armazenamento de blobs do conjunto de migração. Na fase de ingestão, o AzCopy copia os blobs do armazenamento de blobs do conjunto de migração para o armazenamento de blobs do AEM as a Cloud Service de destino.

## Considerações importantes antes de começar {#important-considerations}

Siga a seção abaixo para entender as considerações importantes antes de iniciar:

* A partir da versão 2.0.16 da CTT, a configuração da pré-cópia é feita automaticamente quando o pacote é instalado. Além disso, se o tamanho do conjunto de migração for maior que 200 GB, o processo de extração usará automaticamente o recurso de pré-cópia. O arquivo azcopy.config é criado no diretório crx-quickstart/cloud-migration/. Não é necessário fazer manualmente a configuração da pré-cópia se você estiver usando a versão 2.0.16 ou posterior da CTT.

* A versão do Source AEM deve ser 6.3 - 6.5.

* O armazenamento de dados do Source AEM está configurado para usar o Amazon S3 ou o Armazenamento de blobs do Azure. Para obter mais detalhes, consulte [Configurando armazenamentos de nós e armazenamentos de dados no AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* Cada conjunto de migração copia todo o armazenamento de dados, de modo que apenas um único conjunto de migração deve ser usado.

* Você precisa de acesso para instalar o [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) na instância (ou VM) que executa a instância do AEM de origem.

* A Coleta de Lixo do Armazenamento de Dados foi executada nos últimos sete dias na origem. Para obter mais detalhes, consulte [Coleta de lixo do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### Considerações adicionais se a instância do AEM de origem estiver configurada para usar um Armazenamento de dados Amazon S3 ou Azure Blob {#additional-considerations-amazons3-azure}

* Há um custo associado à transferência de dados do Amazon S3 e do Armazenamento de Blobs do Azure. O custo de transferência é relativo à quantidade total de dados no seu contêiner de armazenamento existente (seja referenciado no AEM ou não). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Armazenamento Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obter mais detalhes.

* Você precisa de um par de chave de acesso e chave secreta para o bucket existente do Amazon S3 de origem, ou um URI SAS para o contêiner existente do Armazenamento de Blobs do Azure de origem (o acesso somente leitura está correto).

### Considerações adicionais se a instância do AEM de origem estiver configurada para usar o Armazenamento de dados de arquivo {#additional-considerations-aem-instance-filedatastore}

* O sistema local deve ter espaço livre estritamente maior que o tamanho 1/256 do armazenamento de dados de origem. Por exemplo, se o tamanho do armazenamento de dados for de 3 terabytes, deverá existir espaço livre maior que 11,72 GB na pasta `crx-quickstart/cloud-migration` na origem para que o AzCopy funcione. No mínimo, o sistema de origem deve ter 1 GB de espaço livre. O espaço livre pode ser obtido usando o comando `df -h` em instâncias do Linux® e o comando dir nas instâncias do Windows.

* Cada vez que a extração é executada com o AzCopy ativado, todo o armazenamento de dados do arquivo é nivelado e copiado para o contêiner de migração na nuvem. Se o conjunto de migração for menor que o tamanho do armazenamento de dados, a extração do AzCopy não será a abordagem ideal.

* Depois que o AzCopy for usado para copiar o armazenamento de dados existente, desative-o para extrações delta ou complementares.

## Configuração do para usar o AzCopy como uma etapa de pré-cópia {#setting-up-pre-copy-step}

>[!NOTE]
>A partir da versão 2.0.16 da CTT, a configuração da pré-cópia é feita automaticamente quando o pacote é instalado. Além disso, se o tamanho do conjunto de migração for maior que 200 GB, o processo de extração usará automaticamente o recurso de pré-cópia. O arquivo azcopy.config é criado no diretório crx-quickstart/cloud-migration/. Se você quiser atualizar a configuração do arquivo manualmente, revise as seções abaixo.

Siga esta seção para saber como configurar o para usar o AzCopy como uma etapa de pré-cópia com a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service:

### &#x200B;0. Determine o tamanho total de todo o conteúdo no armazenamento de dados {#determine-total-size}

É importante determinar o tamanho total do armazenamento de dados por dois motivos:

* Se o AEM de origem estiver configurado para usar o Armazenamento de dados do arquivo, o sistema local deve ter espaço livre estritamente maior que o tamanho 1/256 do armazenamento de dados de origem.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage}

Na página de propriedades do contêiner existente no portal do Azure, use o botão **Calcular tamanho** para determinar o tamanho de todo o conteúdo do contêiner. Por exemplo:

![imagem](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Armazenamento de dados Amazon S3 {#amazon-data}

Você pode usar a guia Métricas do container para determinar o tamanho de todo o conteúdo no container. Por exemplo:


![imagem](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Armazenamento de dados do arquivo {#file-data-store-determine-size}

* Para sistemas Mac, UNIX®, execute o comando du no diretório do armazenamento de dados para obter seu tamanho:
  `du -sh [path to datastore on the instance]`. Por exemplo, se o armazenamento de dados estiver em `/mnt/author/crx-quickstart/repository/datastore`, o comando a seguir lhe dará seu tamanho: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* No Windows, use o comando dir no diretório do armazenamento de dados para obter seu tamanho:
  `dir /a/s [location of datastore]`.

### &#x200B;1. Instalar o AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) é uma ferramenta de linha de comando fornecida pela Microsoft® que deve estar disponível na instância de origem para habilitar este recurso.

Resumindo, você deseja baixar o binário x86-64 do Linux® na [página de documentos do AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e descompactá-lo em um local como /usr/bin.

>[!IMPORTANT]
>Anote onde você colocou o binário, pois é necessário o caminho completo para ele em uma etapa posterior.

### &#x200B;2. Instale a versão da Ferramenta de transferência de conteúdo (CTT) com suporte ao AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>A versão mais recente da CTT deve ser usada.

O suporte do AzCopy para Amazon S3, Armazenamento Azure Blob e Armazenamento de dados de arquivo está incluído na versão mais recente da CTT.
Você pode baixar a versão mais recente da CTT no portal [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).
Observe que somente as versões 2.0.0 e posteriores são compatíveis, e é aconselhável usar a versão mais recente.

### &#x200B;3. Configurar um arquivo azcopy.config {#configure-azcopy-config-file}

Na instância do AEM de origem, em `crx-quickstart/cloud-migration`, crie um arquivo chamado `azcopy.config`.

>[!NOTE]
>O conteúdo desse arquivo de configuração é diferente dependendo se a instância do AEM de origem usa um armazenamento de dados do Azure ou do Amazon S3 ou um armazenamento de dados do Arquivo.

#### Armazenamento de dados do Azure Blob {#azure-blob-storage-data}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar o azCopyPath e o azureSas corretos para sua instância).

>[!NOTE]
>
> Se você não quiser conceder acesso de gravação ao contêiner de armazenamento de blobs existente, poderá gerar um novo URI SAS que tenha somente permissões de Leitura e Lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Armazenamento de dados Amazon S3 {#amazon-sdata-store}

Seu arquivo azcopy.config deve incluir as seguintes propriedades (certifique-se de usar os valores corretos para sua instância).

>[!NOTE]
>
> Se a instância usar Funções IAM para permitir que o AEM acesse S3, será necessário criar uma política e um usuário com as ações ListBucket e GetObject ativadas para o bucket S3. Depois de configurada, use a chave de acesso e a chave secreta deste usuário.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Armazenamento de dados do arquivo {#file-data-store-azcopy-config}

O arquivo `azcopy.config` deve conter a propriedade azCopyPath e uma propriedade repository.home opcional que aponta para o local do armazenamento de dados do arquivo. Use os valores corretos para sua instância.
Armazenamento de dados do arquivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

A propriedade azCopyPath deve conter o caminho completo do local em que a ferramenta de linha de comando azCopy está instalada na instância de origem do AEM. Se a propriedade azCopyPath estiver ausente, a etapa de pré-cópia do blob não será executada.

Se a propriedade `repository.home` estiver ausente em azcopy.config, o local de armazenamento de dados padrão `/mnt/crx/author/crx-quickstart/repository/datastore` será usado para executar a pré-cópia.

### &#x200B;4. Extrair com o AzCopy {#extracting-azcopy}

Com o arquivo de configuração acima em vigor, a fase de pré-cópia do AzCopy é executada como parte de cada extração subsequente. Para impedir a execução, você pode renomear ou remover este arquivo.

>[!NOTE]
>Se o AzCopy não estiver configurado corretamente, você verá a seguinte mensagem nos logs:
>&#x200B;>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie uma extração da interface da CTT. Consulte [Introdução à ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) e o [processo de extração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obter mais detalhes.

1. Confirme se a seguinte linha está impressa no log de extração:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Parabéns! Essa entrada de log significa que sua configuração foi considerada válida e que o AzCopy está copiando todos os blobs do container de origem para o container de migração.

As entradas de log do AzCopy aparecem no log de extração e recebem o prefixo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pré-cópia do AzCopy]

>[!CAUTION]
>
> Durante os primeiros minutos de uma extração, observe os logs de extração atentamente para verificar se há algum sinal de um problema. Como exemplo, veja o que seria registrado se o contêiner do Azure de origem não fosse encontrado:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason > github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Se houver um problema com o AzCopy, a extração falhará imediatamente e os logs de extração conterão detalhes sobre a falha.

Todos os blobs copiados antes do erro são ignorados automaticamente pelo AzCopy nas execuções subsequentes e não precisam ser copiados novamente.

>[!TIP]
>Uma assimilação agora pode ser agendada para iniciar automaticamente imediatamente após uma extração ser bem-sucedida. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obter mais informações.

>[!TIP]
>Se a transferência de blob com o AzCopy progrediu por um tempo, mas falhou somente para alguns blobs, execute novamente a extração com as opções de Pré-cópia e Substituir container de preparo desmarcadas. Isso migrará somente os blobs restantes que não foram transferidos anteriormente.

#### Para Armazenamento de Dados de Arquivo {#file-data-store-extract}

Quando o AzCopy estiver em execução para o arquivo de origem dataStore, você deverá ver mensagens como essas nos registros, indicando que as pastas estão sendo processadas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### &#x200B;5. Assimilar com AzCopy {#ingesting-azcopy}

Consulte [Assimilando conteúdo no destino](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obter informações gerais sobre como assimilar conteúdo no destino a partir do Cloud Acceleration Manager (CAM), incluindo instruções sobre como usar ou não o AzCopy (pré-cópia) na caixa de diálogo &quot;Nova assimilação&quot;.

Para aproveitar o AzCopy durante a assimilação, o Adobe exige que você esteja em uma versão do AEM as a Cloud Service que seja, pelo menos, a versão 2021.6.5561.

Consulte a lista &quot;Tarefas de assimilação&quot; na Cloud Acceleration Manager e os registros da assimilação para que você possa ver o progresso. As entradas de log relacionadas ao
As tarefas bem-sucedidas do AzCopy são exibidas da seguinte maneira (considerando algumas diferenças). A verificação dos registros ocasionalmente pode alertá-lo de problemas
logo no início e ajudá-lo a encontrar uma solução rápida para qualquer problema.

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination does not have full folder support
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

Agora você aprendeu a lidar com grandes repositórios de conteúdo para acelerar as fases de extração e assimilação da atividade de transferência de conteúdo e mover o conteúdo para o AEM as a Cloud Service. Agora você está pronto para aprender o Processo de extração usando a ferramenta Transferência de conteúdo. Consulte [Extração de conteúdo do Source na Ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para que você possa aprender a extrair seu conjunto de migração da Ferramenta de transferência de conteúdo.
