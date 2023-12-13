---
title: Introdução à ferramenta Transferência de conteúdo
description: Saiba como começar a usar a ferramenta Transferência de conteúdo
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 0161477e5248267224fe6d637a192f409161f6d3
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 16%

---

# Introdução à ferramenta Transferência de conteúdo {#getting-started-content-transfer-tool}


## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Download"
>abstract="O Content Transfer Tool pode ser baixado como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Baixe a versão mais recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR" text="Notas de versão"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribuição de software"

O Content Transfer Tool pode ser baixado como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio de [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) na instância do Adobe Experience Manager (AEM) de origem. Baixe a versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

Somente a versão 2.0.0 e superior é compatível, e é aconselhável usar a versão mais recente.

>[!NOTE]
>Baixe a ferramenta Transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividade do ambiente de origem {#source-environment-connectivity}

>[!NOTE]
>
>Um erro de conexão também poderá ocorrer se um conjunto de migração tiver sido excluído do Cloud Acceleration Manager.

A instância do AEM de origem pode estar sendo executada por trás de um firewall, em que ela só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para executar uma extração com êxito, os seguintes endpoints precisam estar acessíveis na instância que está executando o AEM:

* O serviço de armazenamento de blobs do Azure: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Se a extração falhar devido ao seguinte erro: &quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: falha na criação do caminho PKIX: sun.security.provider.certpath.SunCertPathBuilderException: não é possível localizar o caminho de certificação válido para o destino solicitado&quot;, isso poderá ser resolvido com a importação do certificado CA relevante.

### Habilitar o registro SSL {#enable-ssl-logging}

Às vezes, pode ser difícil entender os problemas de conexão SSL/TLS. Para solucionar problemas de conexão durante um processo de extração, você pode ativar o registro SSL por meio do Console do sistema do ambiente AEM de origem seguindo estas etapas:

1. Navegue até o Console da Web do Adobe Experience Manager na instância de origem, acessando **Ferramentas > Operações > Console da Web** ou diretamente para o URL em *https://serveraddress:serverport/system/console/configMgr*
1. Pesquisar por **Configuração do serviço de extração da ferramenta Transferência de conteúdo**
1. Use o botão de ícone de lápis para editar seus valores de configuração
1. Ativar o **Habilitar log ssl para extração** , depois pressione **Salvar**:

   ![imagem](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>Esse sinalizador é apenas para depurar problemas de SSL. Verifique se o sinalizador está desativado antes de executar a extração, pois pode exigir uma grande quantidade de espaço em disco. Isso poderia preencher a capacidade da unidade e causar falha no processo de extração.

## Execução da ferramenta Transferência de conteúdo {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Execução do Content Transfer Tool"
>abstract="Saiba como usar o Content Transfer Tool para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte a demonstração"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Tutorial: utilização do Content Transfer Tool"

A seção a seguir se aplica à nova versão da ferramenta Transferência de conteúdo. Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service:

### Fase de configuração da extração {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Fase de configuração da extração"
>abstract="Saiba como criar e gerenciar um conjunto de migração e como copiar a chave de extração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Tutorial: utilização do Content Transfer Tool"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Faça logon no Cloud Acceleration Manager (CAM) e clique no projeto CAM criado anteriormente para avaliar sua prontidão para migrar para o AEM as a Cloud Service. Se você ainda não criou um projeto CAM, consulte Criação e gerenciamento de um projeto no CAM.

1. Clique em **Transferência de conteúdo** para abrir a exibição da Lista do conjunto de migrações.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Criar um conjunto de migração clicando em **Criar conjunto de migração**.

   >[!NOTE]
   >
   >No máximo 20 conjuntos de migração, incluindo conjuntos expirados, podem ser criados por projeto no Cloud Acceleration Manager.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   A caixa de diálogo a seguir é apresentada. Observe que um conjunto de migração expirará após um período prolongado de inatividade. Depois que avisos forem exibidos no cartão do projeto e as linhas da tabela de trabalhos de migração por um período, o conjunto de migração expirará e seus dados não estarão mais disponíveis. Revisão [Expiração do conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >O nome deve seguir as mesmas convenções de um nó AEM, portanto, não pode conter nenhum destes caracteres: . / : [ ] | *

1. Agora você deve ver sua lista de migração na exibição de lista. Selecione o símbolo de três pontos (**..**) para abrir o menu suspenso e selecionar **Copiar chave de extração**. Essa chave é necessária durante a fase de Extração. Copie essa chave de Extração.

   >[!NOTE]
   >
   >A chave de extração permite que o ambiente AEM de origem se conecte com segurança ao conjunto de migração. Trate essa chave com o mesmo cuidado com que você usaria uma senha e nunca a compartilhe em uma mídia não segura, como email.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Preencher o conjunto de migração {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Preencher conjunto de migração"
>abstract="Depois de criar um conjunto de migração, ele deve ser preenchido com o conteúdo da instância de origem que será movido para o ambiente do AEM as a Cloud Service. Para fazer isso, a Ferramenta de Transferência de Conteúdo precisa estar instalada na instância de origem."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="Extrair conteúdo"

Para preencher o conjunto de migração criado no Cloud Acceleration Manager, instale a versão mais recente da ferramenta Transferência de conteúdo na sua instância de origem do Adobe Experience Manager (AEM). Para saber como preencher o conjunto de migração, siga esta seção.

1. Depois de instalar a versão mais recente da ferramenta Transferência de conteúdo na instância do Adobe Experience Manager de origem, acesse **Operações - Migração de conteúdo**

1. Clique em **Criar conjunto de migração**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Cole a chave de extração que foi copiada do CAM anteriormente no campo de entrada Extraction key de **Criar conjunto de migração** formulário. Depois de fazer isso, os campos Nome do conjunto de migração e Nome do projeto do Cloud Acceleration Manager (CAM) são preenchidos automaticamente. Eles devem corresponder ao nome do Conjunto de migração no CAM e ao nome do projeto CAM que você criou. Agora é possível adicionar caminhos de conteúdo. Depois de adicionar caminhos de conteúdo, salve o conjunto de migração. Você pode executar a extração com as versões incluídas ou excluídas.

   >[!NOTE]
   >
   >Verifique se a chave de extração é válida e se não está próxima de sua expiração. Você pode obter essas informações no **Criar conjunto de migração** após colar a chave de extração. Se você receber um erro de conexão, consulte [Conectividade do ambiente de origem](#source-environment-connectivity) para obter mais informações.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. Em seguida, selecione os seguintes Parâmetros para criar um Conjunto de Migração:

   1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

      ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, é necessário desativar a limpeza de versão devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão ativada e estiver executando atualizações complementares em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.


   1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminhos aceita a entrada digitando ou selecionando.

      >[!IMPORTANT]
      >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (algumas `/etc` caminhos podem ser selecionados na CTT)

1. Clique em **Salvar** depois de preencher todos os campos no **Criar conjunto de migração** tela de detalhes.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Determinação do tamanho do conjunto de migração {#migration-set-size}

Depois de criar um conjunto de migração, é altamente recomendável executar uma verificação de tamanho no conjunto de migração antes de iniciar um processo de Extração.
Ao executar uma verificação de tamanho no conjunto de migração, é possível:

* Determine se há espaço em disco suficiente no `crx-quickstart` subdiretório para concluir a extração com êxito.
* Determine se o tamanho do conjunto de migração se enquadra nos limites do produto compatível e evite assimilações de conteúdo com falha.

Siga as etapas abaixo para executar uma verificação de tamanho:

1. Selecione um conjunto de migração e clique em **Verificar tamanho**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Isso abre o **Verificar tamanho** diálogo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. Clique em **Verificar tamanho** para iniciar o processo. Em seguida, você retornará à exibição da lista de conjuntos de migração e verá uma mensagem indicando que **Verificar tamanho** está em execução.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Depois **Verificar tamanho** for concluído, o status será alterado para **CONCLUÍDO**. Selecione o mesmo conjunto de migração e clique em **Verificar tamanho** para visualizar os resultados. Veja abaixo um exemplo de **Verificar tamanho** resultados sem avisos.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. Se a variável **Verificar tamanho** Os resultados indicam que há espaço em disco insuficiente ou que o conjunto de migração excede os limites do produto, ou ambos, um **AVISO** é exibido.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## O que vem a seguir {#whats-next}

Depois de aprender a criar um conjunto de migração, você estará pronto para aprender sobre os processos de extração e assimilação na ferramenta Transferência de conteúdo. Antes de aprender esses processos, você deve revisar [Lidar com grandes repositórios de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo para mover o conteúdo para o AEM as a Cloud Service.
