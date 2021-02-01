---
title: Usar a ferramenta Transferência de conteúdo
description: Usar a ferramenta Transferência de conteúdo
translation-type: tm+mt
source-git-commit: b4bc29dbea7a765ff41752d4b680cbbc3df51a0b
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 64%

---


# Usar a ferramenta Transferência de conteúdo {#using-content-transfer-tool}

## Considerações importantes sobre o uso da ferramenta Transferência de conteúdo {#pre-reqs}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e o JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para o AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java precisa ser configurado no ambiente AEM para que o comando `java` possa ser executado pelo usuário que start AEM.

* A Ferramenta de transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Arquivo Data Store, S3 Data Store, Compartilhado S3 Data Store e Azure Blob Store Data Store.

* Se estiver usando um *Ambiente Sandbox*, verifique se o ambiente está atualizado e atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para usar a Ferramenta de transferência de conteúdo, você precisará ser um usuário administrador na instância de origem e pertencer ao grupo de administradores de AEM local na instância de Cloud Service para a qual você está transferindo conteúdo. Os usuários sem privilégios não poderão recuperar o token de acesso para usar a ferramenta Transferência de conteúdo.

* O token de acesso pode expirar periodicamente após um período de tempo específico ou após o ambiente ser atualizado. Se o token de acesso tiver expirado, você não poderá se conectar à instância Cloud Service e terá que recuperar o novo token de acesso. O ícone de status associado a um conjunto de migração existente será alterado para uma nuvem vermelha e exibirá uma mensagem ao passar o mouse sobre ele.

* Os Usuários e grupos transferidos pela Ferramenta de transferência de conteúdo são apenas aqueles que são exigidos pelo conteúdo para atender às permissões. O processo *Extração* copia todo o `/home` para o conjunto de migração e o processo *Ingestão* copia todos os usuários e grupos referenciados nas ACLs de conteúdo migrado. Para mapear automaticamente os usuários e grupos existentes para suas IDs IMS, consulte [Usando a ferramenta de mapeamento do usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* Depois de concluir a fase *Extração* do processo de transferência de conteúdo e antes de iniciar as instâncias *Fase de ingestão* para ingerir conteúdo no seu AEM como Cloud Service *Palco* ou *Produção*, terá de registrar um ticket de suporte para notificar o Adobe da sua intenção de executar *Ingestão* para que o Adobe possa garantir que não ocorram interrupções durante o processo *Ingestão*. Você precisará registrar o ticket de suporte uma semana antes da data de *ingestão* planejada. Depois que você enviar o ticket de suporte, a equipe de suporte fornecerá orientações sobre as próximas etapas.
   * Registre um ticket de suporte com os seguintes detalhes:
      * Data exata e hora estimada (com seu fuso horário) quando você planeja start a fase *ingestão*.
      * Tipo de ambiente (Estágio ou Produção) no qual você planeja assimilar dados.
      * ID do programa.

* A *Fase de assimilação* do autor diminuirá a implantação do autor inteiro. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão. Certifique-se também de que nenhum pipeline do Cloud Manager seja executado enquanto você estiver executando a fase *Ingestão*.


## Disponibilidade {#availability}

A Ferramenta de transferência de conteúdo pode ser baixada como um arquivo zip do Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Transferência de conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. O console abaixo é exibido quando você cria o primeiro conjunto de migração. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/01-migration-set-overview.png)

   >[!NOTE]
   >Se você tiver conjuntos de migração existentes, o console exibirá a lista dos conjuntos de migração existentes com seu status atual.

1. Preencha os campos na tela **Detalhes do conjunto de migração de conteúdo**, conforme descrito abaixo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/02-migration-set-creation.png)


   1. **Nome**: insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração do Cloud Service**: insira a URL do autor do AEM as a Cloud Service.

      >[!NOTE]
      >Você pode criar e manter no máximo quatro conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Preparação*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso usando o botão **Abrir token de acesso**. É necessário garantir que você pertença ao grupo de administradores AEM na instância do Cloud Service do público alvo.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário.

      1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminho aceita entrada digitando ou por seleção.

         >[!IMPORTANT]
         >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Clique em **Salvar** depois de preencher todos os campos na tela de detalhes do **Conjunto de migração de conteúdo**.

1. Você visualizará seu conjunto de migração na página *Visão geral*.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Todos os conjuntos de migração existentes nessa tela serão exibidos na página *Visão geral* com suas informações de status atuais. Podem ver alguns destes ícones descritos abaixo.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * Uma *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração na página de visão geral e clique em **Propriedades** para visualização ou editar as propriedades desse conjunto de migração. Ao editar as propriedades, não é possível alterar o nome do container ou o URL do serviço.



### Processo de extração na transferência de conteúdo {#extraction-process}

Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Extrair** para iniciar a extração. A caixa de diálogo **extração do conjunto de migração** é exibida e clique em **Extrair** para start da fase de extração.

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

#### Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a extração complementar. Clique em **Extrair** para iniciar a extração complementar. A caixa de diálogo **Extração do conjunto de migração** é exibida.

   >[!IMPORTANT]
   >
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >
   >![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### Processo de assimilação na transferência de conteúdo {#ingestion-process}

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Assimilar** para iniciar a extração. A caixa de diálogo **Assimilação do conjunto de migração** é exibida. Clique em **Ingest** para start da fase de ingestão. Para fins de demonstração, a opção **Assimilar conteúdo na instância do autor** do autor está desativada. É possível assimilar conteúdo para Autor e Publicação ao mesmo tempo.

   >[!IMPORTANT]
   >Quando a opção **Limpar o conteúdo existente na instância da Cloud antes da ingestão** estiver ativada, ela excluirá todo o repositório existente e criará um novo repositório no qual assimilar o conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de público alvo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/12-content-ingestion.png)

1. Quando a ingestão estiver concluída, o status no campo **PUBLISH INGESTION** será atualizado para **FINISHED**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### Ingestão complementar {#top-up-ingestion-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de assimilação estiver concluído, você poderá usar o conteúdo delta por meio do método de ingestão complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a assimilação complementar. Clique em **Assimilar** para iniciar a extração complementar. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   >[!IMPORTANT]
   >
   >Você deve desativar a opção **Limpar o conteúdo existente na instância do Cloud antes da ingestão**, para evitar a exclusão do conteúdo existente da atividade de ingestão anterior.
   >
   >![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/16-topup-ingestion.png)

### Visualização de logs para um conjunto de migração {#viewing-logs-migration-set}

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

## Resolução de Problemas{#troubleshooting}

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


