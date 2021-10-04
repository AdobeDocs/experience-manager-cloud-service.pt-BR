---
title: Usar a ferramenta Transferência de conteúdo
description: Usar a ferramenta Transferência de conteúdo
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: a9d3547900c84101672cd0400bb374b1a8ccda33
workflow-type: tm+mt
source-wordcount: '3104'
ht-degree: 37%

---

# Usar a ferramenta Transferência de conteúdo {#using-content-transfer-tool}

## Considerações importantes sobre o uso da ferramenta Transferência de conteúdo {#pre-reqs}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e o JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java deve ser configurado no ambiente de AEM, para que o comando `java` possa ser executado pelo usuário que inicia o AEM.

* É recomendável desinstalar versões mais antigas da ferramenta Transferência de conteúdo ao instalar a versão 1.3.0, pois houve uma mudança importante na arquitetura da ferramenta. Com a versão 1.3.0, você também deve criar novos conjuntos de migração e executar novamente a extração e a assimilação nos novos conjuntos de migração.

* A ferramenta Transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Armazenamento de dados de arquivo, Armazenamento de dados S3, Armazenamento de dados S3 compartilhado e Armazenamento de dados do Azure Blob Store.

* Se você estiver usando um *Ambiente de sandbox*, certifique-se de que ele esteja atualizado e seja atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para usar a ferramenta Transferência de conteúdo, você precisa ser um usuário administrador na instância de origem e pertencer ao grupo de AEM local **administradores** na instância do Cloud Service para a qual você está transferindo conteúdo. Os usuários sem privilégios não poderão recuperar o token de acesso para usar a ferramenta Transferência de conteúdo.

* Se a configuração **Limpar conteúdo existente na instância do Cloud antes da assimilação** estiver ativada, ela excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao grupo **administradores**. O usuário deve ser adicionado novamente ao grupo **administrators** para recuperar o token de acesso para CTT.

* O token de acesso pode expirar periodicamente após um período de tempo específico ou após a atualização do ambiente de Cloud Service. Se o token de acesso tiver expirado, você não poderá se conectar à instância do Cloud Service e precisará recuperar o novo token de acesso. O ícone de status associado a um conjunto de migração existente será alterado para uma nuvem vermelha e exibirá uma mensagem ao passar o mouse sobre ela.

* A Ferramenta de transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado enquanto assimila conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração será assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou de Publicação ou em ambos. Recomenda-se que, ao mover o conteúdo para uma instância de Produção, a CTT seja instalada na instância de Autor de origem para mover o conteúdo para a instância de Autor de destino e, de forma semelhante, instale a CTT na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Executar a ferramenta Transferência de conteúdo em uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) para obter mais detalhes.

* Os Usuários e grupos transferidos pela ferramenta Transferência de conteúdo são apenas aqueles que são exigidos pelo conteúdo para atender às permissões. O processo de *Extração* copia todo o `/home` para o conjunto de migração e o processo de *Assimilação* copia todos os usuários e grupos referenciados nas ACLs do conteúdo migrado. Para mapear automaticamente os usuários e grupos existentes para suas IDs IMS, consulte [Usar a ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* Após concluir a fase *Extração* do processo de transferência de conteúdo e antes de iniciar a *Fase de assimilação* para assimilar conteúdo em seu AEM como um Cloud Service *Stage* ou *Production* instâncias, será necessário registrar um tíquete de suporte para notificar o Adobe de sua intenção de executar *Assimilação9/> para que o Adobe possa garantir que nenhuma interrupção ocorra durante o processo* Assimilação *.* Você precisará registrar o tíquete de suporte uma semana antes da data planejada de *Assimilação*. Depois de enviar o tíquete de suporte, a equipe de suporte fornecerá orientação sobre as próximas etapas. Você pode registrar um tíquete de suporte com os seguintes detalhes:

   * Data exata e hora estimada (com seu fuso horário) quando você planeja iniciar a fase *Assimilação*.
   * Tipo de ambiente (Preparo ou Produção) no qual você planeja assimilar dados.
   * ID do programa.

* A *Fase de assimilação* do autor diminui a implantação do autor inteiro. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão. Certifique-se também de que nenhum pipeline do Cloud Manager seja executado enquanto você está executando a fase *Assimilação*.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema de AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados de índice e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se você estiver usando índices personalizados, certifique-se de configurar os índices personalizados com o nó `tika` antes de executar a ferramenta Transferência de conteúdo. Consulte [Preparando a Nova Definição de Índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações adicionais, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Download"
>abstract="A ferramenta Transferência de conteúdo pode ser baixada como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Notas de versão"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribuição de software"

A ferramenta Transferência de conteúdo pode ser baixada como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Faça o download da versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Execução da ferramenta Transferência de conteúdo"
>abstract="Saiba como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM como um Cloud Service (Autor/Publicação)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte Demonstração"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial - Uso da ferramenta Transferência de conteúdo"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação):

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> **Migração de Conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. Selecione a opção **Transferência de conteúdo** do assistente **Migração de conteúdo**.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. O console abaixo é exibido ao criar o primeiro conjunto de migração. Clique em **Criar conjunto de migração** para criar um novo conjunto de migração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >Se você tiver conjuntos de migração existentes, o console exibirá a lista de conjuntos de migração existentes com seu status atual.

   Além disso, clique em **Criar configuração de mapeamento de usuários** para acessar a [Ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).

1. Preencha os campos na tela **Criar conjunto de migração**, conforme descrito abaixo.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **Nome**: insira o nome do conjunto de migração.
      >[!NOTE]
      >Nenhum caractere especial é permitido para o nome do conjunto de migração.

   1. **Configuração do Cloud Service**: insira a URL do autor do AEM as a Cloud Service.

      >[!NOTE]
      >Você pode criar e manter no máximo dez conjuntos de migração por vez durante a atividade de transferência de conteúdo.
      >Além disso, é necessário criar uma migração separadamente para cada um dos ambientes específicos - *Preparação*, *Desenvolvimento* ou *Produção*.

   1. **Token de acesso**: insira o token de acesso.

      >[!NOTE]
      >Você pode recuperar o token de acesso usando o botão **Open access token**. Você precisa garantir que pertença ao grupo dos administradores de AEM na instância do Cloud Service de destino.

   1. **Parâmetros**: selecione os seguintes parâmetros para criar o conjunto de migração:

      1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

      1. **Incluir mapeamento de usuários e grupos** do IMS: Selecione a opção para incluir o mapeamento de usuários e grupos do IMS.
Consulte [Ferramenta de Mapeamento de Usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.

      1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminho aceita entrada digitando ou por seleção.

         >[!IMPORTANT]
         >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alguns  `/etc` caminhos podem ser selecionados no CTT)


1. Clique em **Salvar** depois de preencher todos os campos na tela de detalhes **Criar conjunto de migração**.

1. Você visualizará seu conjunto de migração na página *Visão geral*.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Todos os conjuntos de migração existentes nessa tela serão exibidos na página *Visão Geral* com suas informações de status atuais. Você pode ver alguns desses ícones descritos abaixo.

   * Uma *nuvem vermelha* indica que não é possível concluir o processo de extração.
   * Uma *nuvem verde* indica que você pode concluir o processo de extração.
   * Um *ícone amarelo* indica que você não criou o conjunto de migração existente e o específico é criado por algum outro usuário na mesma instância.

1. Selecione um conjunto de migração na página de visão geral e clique em **Propriedades** para visualização ou editar as propriedades desse conjunto de migração. Ao editar as propriedades, não é possível alterar o nome do contêiner ou o URL do serviço.


### Processo de extração na transferência de conteúdo {#extraction-process}

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

#### Extração complementar {#top-up-extraction-process}

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

### Processo de assimilação na transferência de conteúdo {#ingestion-process}

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

#### Ingestão complementar {#top-up-ingestion-process}

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
