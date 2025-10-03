---
title: Introdução à ferramenta de transferência de conteúdo
description: Saiba como começar a usar a ferramenta Transferência de conteúdo
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 14%

---


# Introdução à ferramenta de transferência de conteúdo {#getting-started-content-transfer-tool}


## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Download"
>abstract="A ferramenta de transferência de conteúdo pode ser baixado como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM). Baixe a versão mais recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR" text="Notas de versão"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribuição de software"

A ferramenta de transferência de conteúdo pode ser baixado como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md) na sua instância de origem do Adobe Experience Manager (AEM). Baixe a versão mais recente. Para obter mais detalhes sobre a versão mais recente, consulte as [Notas de versão](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

Somente a versão 2.0.0 e superior é compatível, e é aconselhável usar a versão mais recente.

>[!NOTE]
>Baixe a ferramenta de transferência de conteúdo no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividade de ambiente do Source {#source-environment-connectivity}

>[!NOTE]
>
>Um erro de conexão também poderá ocorrer se um conjunto de migração tiver sido excluído do Cloud Acceleration Manager.

A instância do AEM de origem pode estar sendo executada por trás de um firewall, em que só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para executar uma extração com êxito, os seguintes endpoints precisam estar acessíveis na instância que está executando o AEM:

* O serviço de armazenamento de blobs do Azure: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Se a extração falhar devido ao seguinte erro: &quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: falha na criação do caminho PKIX: sun.security.provider.certpath.SunCertPathBuilderException: não é possível localizar o caminho de certificação válido para o destino solicitado&quot;, isso poderá ser resolvido com a importação do certificado CA relevante.

### Habilitar o registro SSL {#enable-ssl-logging}

Às vezes, pode ser difícil entender os problemas de conexão SSL/TLS. Para solucionar problemas de conexão durante um processo de extração, você pode ativar o registro SSL por meio do Console do sistema do ambiente AEM de origem seguindo estas etapas:

1. Navegue até o Console da Web do Adobe Experience Manager na sua instância de origem, indo até **Ferramentas > Operações > Console da Web** ou diretamente para a URL em *https://serveraddress:serverport/system/console/configMgr*
1. Pesquisar por **Configuração do serviço de extração da ferramenta de transferência de conteúdo**
1. Use o botão de ícone de lápis para editar seus valores de configuração
1. Habilite a configuração **Habilitar log ssl para extração** e pressione **Salvar**:

   ![imagem](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>
>Esse sinalizador é apenas para depurar problemas de SSL. Verifique se o sinalizador está desativado antes de executar a extração, pois pode exigir uma grande quantidade de espaço em disco. Isso poderia preencher a capacidade da unidade e causar falha no processo de extração.

## Execução da ferramenta de transferência de conteúdo {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Execução da ferramenta de transferência de conteúdo"
>abstract="Saiba como usar a ferramenta de transferência de conteúdo para migrar o conteúdo para o AEM as a Cloud Service (Autor/Publicação)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte a demonstração"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=pt-BR#migration" text="Tutorial: utilização da ferramenta de transferência de conteúdo"

A seção a seguir se aplica à nova versão da ferramenta Transferência de conteúdo. Siga esta seção para saber como usar a ferramenta Transferência de conteúdo para migrar conteúdo para o AEM as a Cloud Service:

### Fase de configuração da extração {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Fase de configuração da extração"
>abstract="Saiba como criar e gerenciar um conjunto de migração e como copiar a chave de extração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=pt-BR#migration" text="Tutorial: utilização da ferramenta de transferência de conteúdo"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Faça logon no Cloud Acceleration Manager (CAM) e clique no projeto CAM criado anteriormente para avaliar sua prontidão para migrar para o AEM as a Cloud Service. Se você ainda não criou um projeto CAM, consulte Criação e gerenciamento de um projeto no CAM.

1. Clique no cartão **Transferência de conteúdo** para abrir a exibição da Lista de conjuntos de migração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Crie um Conjunto de migração clicando em **Criar conjunto de migração**.

   >[!NOTE]
   >
   >No máximo 10 conjuntos de migração, incluindo conjuntos expirados, podem ser criados por projeto no Cloud Acceleration Manager.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   A caixa de diálogo a seguir é apresentada. Observe que um conjunto de migração expirará após um período prolongado de inatividade. Depois que avisos forem exibidos no cartão do projeto e as linhas da tabela de trabalhos de migração por um período, o conjunto de migração expirará e seus dados não estarão mais disponíveis. Revise a [Expiração do Conjunto de Migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   Durante a criação do conjunto de migração, você pode escolher a região geográfica na qual os dados temporários da migração serão armazenados.  É recomendável escolher a região mais próxima do ambiente de nuvem de destino para garantir o desempenho ideal durante as assimilações.  A região não pode ser alterada após a criação do conjunto de migração. Para usar uma região diferente, será necessário criar um novo conjunto de migração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >O nome deve seguir as mesmas convenções de um nó AEM; portanto, não pode conter nenhum destes caracteres: `. / : [ ] | * < > ^ ? { } % # `, nem símbolos ou emojis incomuns.

1. Agora você deve ver sua lista de migração na exibição de lista. Selecione o símbolo de três pontos (**...**) para abrir o menu suspenso e selecione **Copiar chave de extração**. Essa chave é necessária durante a fase de Extração. Copie essa chave de Extração.

   >[!NOTE]
   >
   >A chave de extração permite que o ambiente do AEM de origem se conecte com segurança ao conjunto de migração. Trate essa chave com o mesmo cuidado com que você usaria uma senha e nunca a compartilhe em uma mídia não segura, como email.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Preencher o conjunto de migração {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Preencher conjunto de migração"
>abstract="Depois de criar um conjunto de migração, ele deve ser preenchido com o conteúdo da instância de origem que será movido para o ambiente do AEM as a Cloud Service. Para fazer isso, a Ferramenta de Transferência de Conteúdo precisa estar instalada na instância de origem."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=pt-BR" text="Extrair conteúdo"

Para preencher o conjunto de migração criado no Cloud Acceleration Manager, instale a versão mais recente da ferramenta Transferência de conteúdo na instância de origem do Adobe Experience Manager (AEM). Para saber como preencher o conjunto de migração, siga esta seção.

1. Depois de instalar a versão mais recente da ferramenta Transferência de conteúdo na sua instância do Adobe Experience Manager de origem, vá para **Operações - Migração de conteúdo**

1. Clique em **Criar Conjunto de Migração**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Cole a chave de extração que foi copiada do CAM anteriormente no campo de entrada Chave de extração do formulário **Criar conjunto de migração**. Depois disso, os campos Nome do conjunto de migração e Nome do projeto do Cloud Acceleration Manager (CAM) serão preenchidos automaticamente. Eles devem corresponder ao nome do Conjunto de migração no CAM e ao nome do projeto CAM que você criou. Agora é possível adicionar caminhos de conteúdo. Depois de adicionar caminhos de conteúdo, salve o conjunto de migração. Você pode executar a extração com as versões incluídas ou excluídas.

   >[!NOTE]
   >
   >Verifique se a chave de extração é válida e se não está próxima de sua expiração. Você pode obter essas informações na caixa de diálogo **Criar conjunto de migração** depois de colar a chave de extração. Se você receber um erro de conexão, consulte [Conectividade do ambiente Source](#source-environment-connectivity) para obter mais informações.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. Em seguida, selecione os seguintes Parâmetros para criar um Conjunto de Migração:

   1. **Incluir versão**: selecione conforme necessário. Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

      ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, desative a limpeza de versões devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão habilitada e estiver executando atualizações complementares em um conjunto de migração, você deve executar a assimilação como `wipe=true`.

      >[!NOTE]
      >A partir da versão CTT (3.0.24), novos recursos foram incluídos na ferramenta Transferência de conteúdo, aprimorando o processo de inclusão e exclusão de caminhos. Anteriormente, os caminhos precisavam ser selecionados um por um, o que era tedioso e demorado. Agora, os usuários podem incluir caminhos diretamente da interface do usuário ou fazer upload de um arquivo CSV de acordo com suas preferências.  O arquivo CSV deve ter um caminho por linha e sem vírgulas.

   1. **Caminhos a serem incluídos**: use o navegador de caminhos para selecionar os caminhos que precisam ser migrados. O seletor de caminhos aceita a entrada digitando ou selecionando. Os usuários podem selecionar apenas uma opção para incluir caminhos: na interface ou fazendo upload de um arquivo CSV.
      >[!IMPORTANT]
      >Os seguintes caminhos estão restritos ao criar um conjunto de migração:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (alguns caminhos `/etc` podem ser selecionados na CTT)

      ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. Somente a seleção de caminho é permitida e pelo menos um caminho deve estar presente.Se nenhum caminho for selecionado, ocorrerá um erro no servidor.

         ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. Ao usar a **opção de carregamento CSV**, o arquivo CSV deve conter caminhos válidos.

         ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. Para voltar para o seletor de caminho, os usuários precisam atualizar a página e começar novamente.

      1. Se **caminhos inválidos** forem encontrados no CSV carregado, uma caixa de diálogo separada exibirá os caminhos inválidos.

         ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. Os usuários devem corrigir o arquivo CSV e carregá-lo novamente ou atualizar a interface do usuário para selecionar caminhos por meio do seletor de caminhos.

   1. **Caminhos a serem excluídos**: um novo recurso permite que os usuários excluam caminhos específicos se eles não os desejarem incluir. Por exemplo, se o caminho na seção de inclusão for /content/dam, os usuários poderão excluir caminhos como /content/dam/catalogs.

      ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. Clique em **Salvar** depois de preencher todos os campos na tela de detalhes **Criar conjunto de migração**.

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

* Determine se há espaço em disco suficiente no subdiretório `crx-quickstart` para concluir a extração com êxito.
* Determine se o tamanho do conjunto de migração se enquadra nos limites do produto compatível e evite assimilações de conteúdo com falha.

Siga as etapas abaixo para executar uma verificação de tamanho:

1. Selecione um conjunto de migração e clique em **Verificar tamanho**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Isso abre a caixa de diálogo **Verificar Tamanho**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. Clique em **Verificar Tamanho** para iniciar o processo. Você retornará para a exibição da lista de conjuntos de migração e verá uma mensagem indicando que **Verificar Tamanho** está em execução.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Após a conclusão do processo **Verificar Tamanho**, o status será alterado para **CONCLUÍDO**. Selecione o mesmo conjunto de migração e clique em **Verificar tamanho** para ver os resultados. Veja abaixo um exemplo dos resultados **Verificar Tamanho** sem avisos.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. Se os resultados da **Verificação de Tamanho** indicarem que há espaço em disco insuficiente, ou o conjunto de migração excede os limites do produto, ou ambos, um status de **AVISO** será exibido.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## O que vem a seguir {#whats-next}

Depois de aprender a criar um conjunto de migração, você estará pronto para aprender sobre os processos de extração e assimilação na ferramenta Transferência de conteúdo. Antes de aprender esses processos, você deve revisar [Lidar com grandes repositórios de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo e mover o conteúdo para o AEM as a Cloud Service.
