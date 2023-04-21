---
title: Assimilar conteúdo no Target
description: Assimilar conteúdo no Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: cab182a7998be6a569cf16e4000184f7235082da
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 12%

---

# Assimilar conteúdo no Target {#ingesting-content}

## Processo de assimilação na ferramenta Transferência de conteúdo {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingestão de conteúdo"
>abstract="Ingestão refere-se à ingestão de conteúdo do conjunto de migração na instância de destino do Cloud Service. A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="Ingestão complementar"

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:

>[!NOTE]
>Lembrou-se de registrar um tíquete de suporte para esta assimilação? Consulte [Considerações importantes antes de usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) para isso e outras considerações que ajudem a tornar a ingestão bem-sucedida.

1. Vá para Cloud Acceleration Manager. Clique no cartão do projeto e clique no cartão Transferência de conteúdo . Navegar para **Trabalhos de assimilação** e clique em **Nova Assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise a lista de verificação de assimilação e verifique se todas as etapas foram concluídas. Essas são etapas necessárias para garantir uma assimilação bem-sucedida. Você poderá prosseguir para a **Próximo** somente se a lista de verificação tiver sido concluída.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Forneça as informações necessárias para criar uma nova assimilação.

   * Selecione o conjunto de migração que contém os dados extraídos como a Fonte.
      * Os Conjuntos de Migração expirarão após um longo período de inatividade, portanto, espera-se que a assimilação ocorra relativamente cedo após a extração ter sido executada. Revisão [Expiração do conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.
   * Selecione o ambiente de destino. É aqui que o conteúdo do conjunto de migração será assimilado. Selecione a camada. (Autor/Publicação). Ambientes de desenvolvimento rápido não são compatíveis.

   >[!NOTE]
   >As seguintes notas se aplicam à assimilação de conteúdo:
   > Se a origem foi Autor, é recomendável assimilá-la no nível Autor no destino. Da mesma forma, se a origem foi Publicar, o destino também deve ser Publicar.
   > Se a camada de destino for `Author`, a instância do autor será encerrada durante a assimilação e não estará disponível para os usuários (por exemplo, autores ou qualquer pessoa que faça manutenção etc.). Isto serve para proteger o sistema e impedir quaisquer alterações que possam ser perdidas ou causar um conflito de ingestão. Certifique-se de que a sua equipe esteja ciente deste fato. Observe também que o ambiente aparecerá hibernado durante a assimilação do autor.
   > Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Integração com o AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.
   > Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinho. Isso irá acelerar a assimilação de Publicação quando for executada mais tarde.
   > As sugestões não são compatíveis com um destino de RDE (Rapid Development Environment). Eles não serão exibidos como uma possível escolha de destino, mesmo se o usuário tiver acesso a ele.

   >[!IMPORTANT]
   > Os seguintes avisos importantes se aplicam à assimilação de conteúdo:
   > Você poderá iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino. Se não conseguir iniciar uma assimilação, consulte [Não é possível iniciar a assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obter mais detalhes.
   > Se a configuração **Varrer** estiver habilitado antes da assimilação, ele excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao **administradores** grupo. Você precisará ser adicionado novamente ao grupo de administradores para iniciar uma assimilação.

1. Clique em **Assimilar**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Em seguida, você pode monitorar a fase de assimilação na exibição da lista Trabalhos de assimilação e usar o menu de ação da assimilação para exibir o log conforme a assimilação avança.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Quando a assimilação estiver concluída, clique no botão (i) no canto superior direito da tela para obter mais informações sobre o trabalho de assimilação.

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Ingestão complementar {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingestão complementar"
>abstract="Use o recurso complementar para mover o conteúdo modificado desde a atividade de transferência de conteúdo anterior. Após a conclusão da ingestão, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, seja resolvendo os problemas relatados ou entrando em contato com o Atendimento ao cliente da Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="Exibir logs"

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se tiver usado a etapa de pré-cópia para a primeira assimilação completa, você pode ignorar a pré-cópia para as assimilações adicionais subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB), pois isso pode adicionar tempo ao processo inteiro.

Quando o processo de ingestão estiver concluído, para assimilar o conteúdo delta, será necessário executar uma [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) e, em seguida, use o método de ingestão complementar.

Você pode fazer isso criando um novo trabalho de assimilação e garantir que **Varrer** estiver desativado durante a fase de assimilação, conforme mostrado abaixo:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolução de problemas {#troubleshooting}

### O CAM não pode recuperar o token de migração {#cam-unable-to-retrieve-the-migration-token}

A recuperação automática do token de migração pode falhar por motivos diferentes, incluindo você [configuração de uma lista de permissões IP via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) no ambiente Cloud Service do target. Nesses cenários, você verá a seguinte caixa de diálogo ao tentar iniciar uma assimilação:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Você precisará recuperar o token de migração manualmente clicando no link &quot;Obter token&quot; na caixa de diálogo. Isso abrirá outra guia que exibe o token. Em seguida, você pode copiar o token e colá-lo no **Entrada do token de migração** campo. Agora, você deve ser capaz de iniciar a ingestão.

>[!NOTE]
>
>O token estará disponível para usuários que pertencem ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino.

### Não é possível iniciar a assimilação {#unable-to-start-ingestion}

Você poderá iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino. Se você não pertencer ao grupo de administradores AEM, verá um erro como mostrado abaixo ao tentar iniciar uma assimilação. Você pode solicitar que o administrador o adicione ao local **Administradores de AEM** ou peça o token em si, que pode ser colado no **Entrada do token de migração** campo.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Não é possível acessar o serviço de migração {#unable-to-reach-migration-service}

Depois que uma assimilação é solicitada, uma mensagem como a seguinte pode ser apresentada ao usuário: &quot;O serviço de migração no ambiente de destino está inacessível no momento. Tente novamente mais tarde ou entre em contato com o suporte ao Adobe.&quot;

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Isso indica que o Cloud Acceleration Manager não conseguiu acessar o serviço de migração do ambiente de destino para iniciar a assimilação. Isso pode acontecer por várias razões.

>[!NOTE]
> 
> O campo &quot;Token de migração&quot; é exibido porque, em alguns casos, a recuperação desse token é o que está sendo realmente proibido. Ao permitir que seja fornecido manualmente, pode permitir que o usuário inicie a ingestão rapidamente, sem qualquer ajuda adicional. Se o token for fornecido, e a mensagem ainda aparecer, a recuperação do token não foi o problema.

* AEM as a Cloud Service mantém o estado do ambiente e, ocasionalmente, pode precisar reiniciar o serviço de migração por vários motivos normais. Se esse serviço estiver sendo reiniciado, ele não poderá ser acessado, mas estará disponível em breve.
* É possível que outro processo esteja sendo executado na instância. Por exemplo, se o Orquestrador de versões estiver aplicando uma atualização, o sistema poderá estar ocupado e o serviço de migração regularmente não estará disponível. É por isso que, e a possibilidade de corromper o estágio ou a instância de produção, pausar atualizações durante uma assimilação é altamente recomendado.
* Se uma [A  de Lista de permissões de IP foi aplicada](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) por meio do Cloud Manager, isso impedirá que o Cloud Acceleration Manager chegue ao serviço de migração. Um endereço IP não pode ser adicionado para ingestões porque seu endereço é muito dinâmico. Atualmente, a única solução é desativar a lista de permissões IP enquanto a assimilação estiver em execução.
* Pode haver outras razões que precisem de investigação. Se a ingestão continuar falhando, entre em contato com o Atendimento ao Cliente do Adobe.

### Atualizações automáticas por meio do Orquestrador de versões ainda estão ativadas

O Release Orchestrator mantém os ambientes atualizados automaticamente ao aplicar atualizações automaticamente. Se a atualização for acionada quando uma assimilação estiver sendo executada, poderá causar resultados imprevisíveis, incluindo a corrupção do ambiente. Esse é um dos motivos pelos quais um tíquete de suporte deve ser registrado antes de iniciar uma assimilação (consulte &quot;Observação&quot; acima), para que a desativação temporária do Orquestrador de versões possa ser agendada.

Se o Orquestrador de versões ainda estiver em execução quando uma assimilação estiver sendo iniciada, a interface do usuário apresentará esta mensagem. Você pode optar por continuar assim mesmo, aceitando o risco, marcando o campo e pressionando o botão novamente.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Falha de assimilação complementar

Uma causa comum de um [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) falha é um conflito nas ids de nó. Para identificar esse erro, baixe o log de assimilação usando a interface do usuário do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Propriedade violada de restrição de exclusividade [jcr:uuid] com o valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nó no AEM deve ter um uuid exclusivo. Este erro indica que um nó que está sendo assimilado tem o mesmo uuid que um que já existe em um caminho diferente na instância de destino.
Isso pode acontecer se um nó for movido para a origem entre uma extração e uma [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Isso também pode acontecer se um nó no destino for movido entre uma assimilação e uma assimilação complementar subsequente.

Este conflito deve ser resolvido manualmente. Alguém familiarizado com o conteúdo deve decidir qual dos dois nós deve ser excluído, tendo em mente outro conteúdo que o referencie. A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo.

## O que vem a seguir {#whats-next}

Depois de concluir a Inserção de conteúdo no Target, você pode visualizar os logs de cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) para saber mais.
