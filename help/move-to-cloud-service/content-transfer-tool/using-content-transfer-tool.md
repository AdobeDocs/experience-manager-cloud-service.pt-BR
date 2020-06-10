---
title: Uso da ferramenta de transferência de conteúdo
description: Uso da ferramenta de transferência de conteúdo
translation-type: tm+mt
source-git-commit: f2a6b67e3673bf6dfeb63d445074f6d1e05971cf
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 1%

---


# Uso da ferramenta de transferência de conteúdo {#using-content-transfer-tool}

## Considerações importantes sobre o uso da ferramenta de transferência de conteúdo {#pre-reqs}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a Ferramenta de transferência de conteúdo é AEM 6.3 + e JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para o AEM 6.5 para usar a Ferramenta de transferência de conteúdo.

* Se você estiver usando um Ambiente ** Sandbox , certifique-se de que seu ambiente foi atualizado para a versão de 10 de junho de 2020 ou posterior. Se você estiver usando um Ambiente *de* produção, ele será atualizado automaticamente.

* Para usar a Ferramenta de transferência de conteúdo, você precisará ser um usuário administrador na instância de origem e pertencer ao grupo de administradores do AEM na instância do Serviço de nuvem para a qual você está transferindo conteúdo. Os usuários sem privilégios não poderão recuperar o token de acesso para usar a Ferramenta de transferência de conteúdo.

* Durante a fase de extração, a Ferramenta de transferência de conteúdo é executada em uma instância de origem AEM ativa.

* A Fase *de* ingestão do autor diminuirá a implantação do autor inteiro. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão.

## Disponibilidade {#availability}

A Ferramenta de transferência de conteúdo pode ser baixada como um arquivo zip (Content Transfer Tool v1.0.0) do portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe a Ferramenta de transferência de conteúdo do Portal [de distribuição de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)software.

## Execução da ferramenta de transferência de conteúdo {#running-tool}

Siga esta seção para saber como usar a Ferramenta de transferência de conteúdo para migrar o conteúdo para o AEM como um serviço em nuvem (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Transferência **** de conteúdo.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Clique em **Criar conjunto** de migração para criar um novo conjunto de migração. Os detalhes **do Conjunto de migrações** de conteúdo são exibidos.

   >[!NOTE]
   >Você visualização os conjuntos de migração existentes nesta tela com seu status atual.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Preencha os campos na tela de detalhes **do Conjunto de migrações de** conteúdo, conforme descrito abaixo.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Nome**: Insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração** do serviço em nuvem: Insira o AEM de destino como um URL do autor do serviço em nuvem.

      >[!NOTE]
      >Você pode criar e manter no máximo quatro conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Estágio*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: Insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso da instância do autor navegando até `/libs/granite/migration/token.json`. O token de acesso é recuperado da instância do autor do Serviço em nuvem.

   1. **Parâmetros**: Selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: Selecione conforme necessário.

      1. **Caminhos a serem incluídos**: Use o navegador de caminho para selecionar os caminhos que precisam ser migrados.

         >[!IMPORTANT]
         >Os seguintes caminhos são restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Clique em **Salvar** depois de preencher todos os campos na tela de detalhes **do Conjunto de migrações** de conteúdo.

1. Você visualização seu conjunto de migração na página *Visão geral* .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Todos os conjuntos de migração existentes nessa tela são exibidos na página *Visão geral* com suas informações de status e status atuais.

   * Uma nuvem ** vermelha indica que não é possível concluir o processo de extração.
   * Uma nuvem ** verde indica que você pode concluir o processo de extração.
   * Um ícone ** amarelo indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração na página de visão geral e clique em **Propriedades** para visualização ou editar as propriedades do conjunto de migração.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Processo de Extração na transferência de conteúdo {#extraction-process}

Siga as etapas abaixo para extrair seu conjunto de migração da Ferramenta de transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Extrair** para extração do start.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. A caixa de diálogo extração **Conjunto de** Migração é exibida e clique em **Extrair** para concluir a fase de extração.

   >[!NOTE]
   >Você tem a opção de substituir o container temporário durante a fase de extração.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. O campo **EXTRAÇÃO** agora exibe o status **EXECUÇÃO** do processo de extração em andamento.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **FINALIZADO** e um ícone de nuvem verde ** estável será exibido abaixo do campo **INFO** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Será necessário atualizar a página para visualização do status atualizado.
   >Quando a fase de extração é iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Então, se uma extração for parada, você precisa esperar um minuto para que a fechadura seja liberada antes de iniciar a extração novamente.

#### Extração superior {#top-up-extraction-process}

A Ferramenta de transferência de conteúdo tem um recurso que oferece suporte ao conteúdo diferencial de complementos, onde é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial de conteúdo, é recomendável fazer atualizações frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar em funcionamento no Cloud Service.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração superior. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual deseja executar a extração de cima.

1. Clique em **Extrair** para start da extração superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. A caixa de diálogo extração **Conjunto de** Migrações é exibida.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir container de preparo durante a extração** .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Processo de ingestão na transferência de conteúdo {#ingestion-process}

Siga as etapas abaixo para assimilar seu conjunto de migração da Ferramenta de transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Ingressar** na extração do start.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. A caixa de diálogo de ingestão **do Conjunto de** Migração é exibida.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   Para fins de demonstração, a opção **Ingressar conteúdo na instância** do autor está desativada. É possível ingerir conteúdo para Autor e Publicar ao mesmo tempo.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Clique em **Ingest** para concluir a fase de ingestão.

1. Quando a ingestão estiver concluída, o status no campo **AUTHOR INGESTION** será atualizado para **FINISHED** e um ícone de nuvem verde estável será exibido abaixo de **INFO**.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Será necessário atualizar a página para visualização do status atualizado.

#### Ingestão Superior para Cima {#top-up-ingestion-process}

A Ferramenta de transferência de conteúdo tem um recurso que oferece suporte ao conteúdo diferencial *adicional* , onde é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial de conteúdo, é recomendável fazer atualizações frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar em funcionamento no Cloud Service.

Quando o processo de ingestão estiver concluído, você poderá usar o conteúdo delta, usando o método de ingestão topo a topo. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual deseja executar a ingestão de cima.

1. Clique em **Ingest** para start da extração superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. A caixa de diálogo **Migração Definir ingestão** é exibida.

   >[!NOTE]
   >Você deve desativar a opção *Limpar* , para evitar que o conteúdo existente seja excluído da atividade de ingestão anterior.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Exibindo Registros para um Conjunto de Migrações {#viewing-logs-migration-set}

Você pode visualização logs para um conjunto de migração existente na página *Visão geral* .
Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração que deseja excluir e clique em Log **de** Visualizações na barra de ações.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. A caixa de diálogo **Logs** é exibida. Clique em Logs **de** Extração para visualização dos registros em uma nova guia.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)Or,

   Você também pode visualização logs para seu conjunto de migração na tela *Visão geral* . Selecione o conjunto de migração e clique no status no campo **EXTRAÇÃO** . Nesse caso, clique em **CONCLUÍDO** para fazer a visualização dos registros em uma nova guia.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### Excluindo um Conjunto de Migrações {#deleting-migration-set}

Você pode excluir o conjunto de migração da página *Visão geral* .
Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração que deseja excluir e clique em **Excluir** na barra de ações.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Clique em **Excluir** da caixa de diálogo **Excluir conjunto** de migração para confirmar a exclusão.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Resolução de Problemas{#troubleshooting}

### IDs de blob ausentes {#missing-blobs}

Se houver IDs de blob ausentes reportadas, como mencionado abaixo, então é necessário executar uma verificação de consistência no repositório existente e restaurar os blobs ausentes.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

O seguinte comando é executado

>[!NOTE]
> `--verbose` o sinalizador é necessário para relatar os caminhos do nó de onde os blobs são referenciados.

**Para repositórios AEM 6.5 (Oak 1.8 e inferior)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositórios com Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obter mais detalhes.

Os arquivos criados no *OUT_DIR* especificado acima para fins de consistência podem ser verificados quanto aos caminhos que faltam binários e à ação apropriada tomada como restaurar a partir de um backup, excluir os caminhos, reindexar e assim por diante.

### Comportamento da interface {#ui-behavior}

Como usuário, você pode ver as seguintes alterações de comportamento na interface do usuário para a ferramenta de transferência de conteúdo:

* O usuário cria um conjunto de migração para um URL do autor (Desenvolvimento/Fase/Produção) e executa com êxito a extração e a ingestão.

* Em seguida, o usuário cria um novo conjunto de migração para o mesmo URL do autor e executa extração e ingestão no novo conjunto de migração. A interface do usuário mostra que o status de ingestão do primeiro conjunto de migração muda para **FALHA** e nenhum registro está disponível.

* Isso não significa que a ingestão do primeiro conjunto de migração falhou. Esse comportamento é visto porque quando um novo trabalho de ingestão é iniciado, ele exclui o trabalho de ingestão anterior. Portanto, o status das alterações no primeiro conjunto de migração deve ser ignorado.

* Os ícones na interface do usuário da Ferramenta de transferência de conteúdo podem parecer diferentes das capturas de tela mostradas neste guia ou podem não aparecer, dependendo da versão da instância do AEM de origem.


