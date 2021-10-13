---
title: Usar a ferramenta Transferência de conteúdo
description: Usar a ferramenta Transferência de conteúdo
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 04494e116fcdd38622ae2d4434d7cf8e4034d5aa
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 52%

---

# Usar a ferramenta Transferência de conteúdo {#using-content-transfer-tool}

## Processo de extração na transferência de conteúdo {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extração de conteúdo"
>abstract="Extração refere-se à extração de conteúdo da instância de AEM de origem em uma área temporária chamada de conjunto de migração. Um conjunto de migração é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extração complementar"

Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Se o Amazon S3 ou o Azure Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. Para fazer isso, será necessário configurar um arquivo `azcopy.config` antes de executar a extração. Consulte [Manuseio de repositórios de conteúdo grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obter mais detalhes.

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Extrair** para iniciar a extração. A caixa de diálogo **Extração do conjunto de migração** é exibida e clique em **Extrair** para iniciar a fase de extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >Você tem a opção de substituir o containercontêiner de preparação durante a fase de extração.


1. O campo **EXTRAÇÃO** agora exibe o status **EXECUÇÃO** para indicar que a extração está em andamento.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **CONCLUÍDO**, e um ícone de nuvem *verde sólido* será exibido abaixo do campo **INFO** .

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >A interface do usuário tem um recurso de recarregamento automático que recarrega a página de visão geral a cada 30 segundos.
   >Quando a fase de extração for iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Em seguida, se uma extração for interrompida, você precisará esperar um minuto até que o bloqueio seja liberado antes de reiniciar a extração.

### Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a extração complementar. Clique em **Extrair** para iniciar a extração complementar. A caixa de diálogo **Extração do conjunto de migração** é exibida.

   >[!IMPORTANT]
   >
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >
   >![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

## Processo de assimilação na transferência de conteúdo {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Assimilação de conteúdo"
>abstract="Assimilação refere-se à assimilação de conteúdo do conjunto de migração na instância do Cloud Service de destino. A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Ingestão complementar"

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Se o Amazon S3 ou o Azure Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Gravação com AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obter mais detalhes.

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Assimilar** para iniciar a assimilação. A caixa de diálogo **Assimilação do conjunto de migração** é exibida. O conteúdo pode ser assimilado na instância do autor ou na instância de publicação de cada vez. Selecione a instância para a qual assimilar conteúdo. Clique em **Assimilar** para iniciar a fase de assimilação.

   >[!IMPORTANT]
   >Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinho. Isso irá acelerar a assimilação de Publicação quando for executada mais tarde.

   >[!IMPORTANT]
   >Quando a opção **Limpar conteúdo existente na instância do Cloud antes da assimilação** estiver ativada, ela excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao grupo **administradores**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   Além disso, clique em **Atendimento ao cliente** para registrar um tíquete, conforme mostrado na figura acima. Além disso, consulte [Considerações importantes sobre o uso da ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) para saber mais.

1. Quando a assimilação estiver concluída, o status será atualizado para **FINISHED**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

### Ingestão complementar {#top-up-ingestion-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de assimilação estiver concluído, você poderá usar o conteúdo delta por meio do método de ingestão complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a assimilação complementar. Clique em **Assimilar** para iniciar a extração complementar. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Você deve desativar a opção **Limpar conteúdo existente na instância do Cloud antes de assimilar**, para evitar que o conteúdo existente seja excluído da atividade de assimilação anterior. Além disso, clique em **Atendimento ao cliente** para registrar um tíquete, conforme mostrado na figura anterior.


### Visualização de logs para um conjunto de migração {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualização de logs"
>abstract="Após a conclusão da extração da assimilação, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o suporte ao Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Resolução de problemas"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Entrar em contato com o suporte ao Adobe"

Após a conclusão de cada etapa (extração e assimilação), verifique os logs e procure erros.  Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o suporte ao Adobe.

Você pode visualizar logs de um conjunto de migração existente na página *Visão geral*.
Siga as etapas abaixo:

1. Navegue até a página *Visão geral*, selecione o conjunto de migração que você deseja excluir e clique em **Exibir log** na barra de ações.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. A caixa de diálogo **Logs** é exibida. Clique em **Logs de extração** para visualizar os logs em uma nova guia.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Ou,

   Você também pode visualizar logs para o seu conjunto de migração na tela *Visão geral*. Selecione o conjunto de migração e clique no status do campo **EXTRAÇÃO**. Nesse caso, clique em **CONCLUÍDO** para visualizar os logs em uma nova guia.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Para rastrear os logs sem usar a interface do usuário, você pode aplicar SSH ao ambiente do AEM de origem e rastrear o conteúdo do `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Exclusão de um conjunto de migração {#deleting-migration-set}

Você pode excluir o conjunto de migração na página *Visão geral*.
Siga as etapas abaixo:

1. Navegue até a página *Visão geral*, selecione o conjunto de migração que você deseja excluir e clique em **Excluir** na barra de ações.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Clique em **Excluir** na caixa de diálogo **Excluir conjunto de migração** para confirmar a exclusão.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## Execução da ferramenta Transferência de conteúdo em uma instância de publicação {#running-ctt-on-publish}

Recomenda-se que, ao mover o conteúdo para uma instância de Publicação, a CTT seja instalada na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Siga a abordagem recomendada conforme descrito abaixo:

* Use a mesma versão da CTT usada na instância do Autor.

* Somente um único nó de publicação precisa ser migrado. Ele deve ser removido do balanceador de carga antes de iniciar a extração.

* Ao criar o conjunto de migração, use o URL do ambiente AEMaaCS de autor.

* Durante a assimilação para publicar, o nível de publicação NÃO será dimensionado para baixo (diferente do autor). Como precaução, evite quaisquer operações de gravação iniciadas pelo usuário, como:

   * Distribuição de conteúdo do autor do AEMaaCS para publicar nesse ambiente
   * Sincronização de usuários entre instâncias de publicação


## Resolução de problemas {#troubleshooting}

### IDs de blob ausentes {#missing-blobs}

Se houver IDs de blob ausentes reportados, como mencionado abaixo, será necessário executar uma verificação de consistência no repositório existente e restaurar os blobs ausentes.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

O seguinte comando é executado

>[!NOTE]
>
>O sinalizador `--verbose` é necessário para relatar os caminhos de nó de onde os Blobs são referenciados.

**Para repositórios AEM 6.5 (Oak 1.8 e inferior)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositórios com Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Jar executável do Oak](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obter mais detalhes.

Os arquivos criados no *OUT_DIR* especificado acima para fins de consistência podem ser verificados quanto a caminhos com binários ausentes e à ação apropriada a ser realizada, como restauração de um backup, exclusão dos caminhos, reindexação e assim por diante.


### Comportamento da interface do usuário {#ui-behavior}

Como usuário, você pode ver as seguintes alterações de comportamento na interface do usuário da ferramenta Transferência de conteúdo:

* Os ícones na interface do usuário da ferramenta Transferência de conteúdo podem parecer diferentes das capturas de tela mostradas neste guia ou podem não aparecer, dependendo da versão da instância do AEM de origem.
