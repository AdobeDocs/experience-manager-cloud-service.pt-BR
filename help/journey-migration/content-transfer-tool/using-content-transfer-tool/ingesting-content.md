---
title: Assimilar conteúdo no Target
description: Assimilar conteúdo no Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1732'
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
>Você se lembrou de registrar um tíquete de suporte para esta assimilação? Consulte [Considerações importantes antes de usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) por essa e outras considerações para ajudar a tornar a assimilação bem-sucedida.

1. Acesse o Cloud Acceleration Manager. Clique no cartão do projeto e clique no cartão Transferência de conteúdo. Navegue até **Tarefas de assimilação** e clique em **Nova assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise a lista de verificação de assimilação e verifique se todas as etapas foram concluídas. Essas são etapas necessárias para garantir uma assimilação bem-sucedida. Vá para a página **Próxima** etapa somente se a lista de verificação estiver concluída.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Forneça as informações necessárias para criar uma nova assimilação.

   * Selecione o conjunto de migração que contém os dados extraídos como Origem.
      * Os conjuntos de migração expirarão após um período prolongado de inatividade, de modo que é esperado que a assimilação ocorra relativamente logo após a extração ter sido realizada. Revisão [Expiração do conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.
   * Selecione o ambiente de destino. É nesse ambiente que o conteúdo do conjunto de migração é assimilado. Selecione a camada. (Autor/Publicação). Os ambientes de desenvolvimento rápido não são compatíveis.

   >[!NOTE]
   >As seguintes observações se aplicam à assimilação de conteúdo:
   > Se a origem foi do Autor, é recomendável assimilá-la no nível do Autor no destino. Da mesma forma, se a origem foi Publicar, o destino também deve ser Publicar.
   > Se a camada de destino for `Author`, a instância do autor é encerrada durante a duração da assimilação e fica indisponível para os usuários (por exemplo, autores ou qualquer pessoa que esteja executando a manutenção). O motivo é proteger o sistema e evitar quaisquer alterações que possam ser perdidas ou causar um conflito de assimilação. Confirme se sua equipe está ciente desse fato. Observe também que o ambiente parece hibernado durante a assimilação do autor.
   > Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Assimilar com AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.
   > Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinha. Isso acelera a Assimilação de publicação quando executada posteriormente.
   > As assimilações não são compatíveis com um destino de RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) e não aparecem como uma possível opção de destino, mesmo que o usuário tenha acesso a ele.

   >[!IMPORTANT]
   > Os seguintes avisos importantes se aplicam à assimilação de conteúdo:
   > Você pode iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino. Se não conseguir iniciar uma assimilação, consulte [Não foi possível iniciar a assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obter mais detalhes.
   > Se a configuração **Limpar** estiver ativado antes da assimilação, ele exclui todo o repositório existente e cria um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também ocorre para um usuário administrador adicionado à variável **administradores** grupo. Você deve ser adicionado novamente ao grupo de administradores para iniciar uma assimilação.

1. Clique em **Assimilar**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Em seguida, é possível monitorar a fase de assimilação na exibição de lista dos trabalhos de assimilação e usar o menu de ação da assimilação para exibir o log à medida que a assimilação avança.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Clique em **i)** botão na linha para obter mais informações sobre o trabalho de assimilação. Você pode ver a duração de cada etapa da assimilação quando ela estiver em execução ou concluída clicando em **..** e depois em **Exibir durações**. As informações da extração também são mostradas para perceber o que está sendo assimilado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira assimilação completa, poderá ignorar a pré-cópia para as assimilações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB), pois pode adicionar tempo a todo o processo.

Quando o processo de assimilação estiver concluído, para assimilar o conteúdo delta, será necessário executar um [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) e, em seguida, use o método de assimilação complementar.

Você pode fazer isso criando um novo trabalho de assimilação e garantindo que **Limpar** O está desativado durante a fase de assimilação, conforme mostrado abaixo:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolução de problemas {#troubleshooting}

### O CAM não consegue recuperar o token de migração {#cam-unable-to-retrieve-the-migration-token}

A recuperação automática do token de migração pode falhar por diferentes motivos, incluindo você [configuração de uma lista de permissões IP via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) no ambiente Cloud Service de destino. Nesses casos, você verá a seguinte caixa de diálogo ao tentar iniciar uma assimilação:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Você precisará recuperar o token de migração manualmente clicando no link &quot;Obter token&quot; na caixa de diálogo. Isso abrirá outra guia que exibe o token. Em seguida, você pode copiar o token e colá-lo na **Entrada do token de migração** campo. Agora, você pode começar a assimilação.

>[!NOTE]
>
>O token está disponível para usuários que pertencem ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino.

### Não foi possível iniciar a assimilação {#unable-to-start-ingestion}

Você pode iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino. Se você não pertencer ao grupo de administradores do AEM, verá um erro como mostrado abaixo ao tentar iniciar uma assimilação. Você pode pedir ao administrador para adicioná-lo ao local **Administradores do AEM** ou solicite o token propriamente dito, que você pode colar na **Entrada do token de migração** campo.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Não é possível acessar o serviço de migração {#unable-to-reach-migration-service}

Depois que uma assimilação é solicitada, uma mensagem como a seguinte pode ser apresentada ao usuário: &quot;O serviço de migração no ambiente de destino está inacessível no momento. Tente novamente mais tarde ou entre em contato com o suporte de Adobe.&quot;

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Isso indica que o Cloud Acceleration Manager não conseguiu atingir o serviço de migração do ambiente de destino para iniciar a assimilação. Isso pode acontecer por várias razões.

>[!NOTE]
> 
> O campo &quot;Token de migração&quot; é exibido porque, em alguns casos, a recuperação desse token é o que realmente não é permitido. Ao permitir que seja fornecido manualmente, ele pode permitir que o usuário inicie a assimilação rapidamente, sem nenhuma ajuda adicional. Se o token for fornecido e a mensagem ainda for exibida, o problema não foi recuperar o token.

* O AEM as a Cloud Service mantém o estado do ambiente e, ocasionalmente, pode precisar reiniciar o serviço de migração por vários motivos normais. Se esse serviço estiver sendo reiniciado, ele não poderá ser acessado, mas geralmente estará disponível em breve.
* É possível que outro processo esteja sendo executado na instância. Por exemplo, se o Release Orchestrator estiver aplicando uma atualização, o sistema pode estar ocupado e o serviço de migração pode ficar indisponível regularmente. Isso e a possibilidade de corromper o estágio ou a instância de produção é o motivo pelo qual é altamente recomendável pausar as atualizações durante uma assimilação.
* Se um [A Inclui na lista de permissões IP foi aplicada](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) por meio do Cloud Manager, isso impedirá que o Cloud Acceleration Manager chegue ao serviço de migração. Um endereço IP não pode ser adicionado para assimilações porque seu endereço é muito dinâmico. Atualmente, a única solução é desativar a lista de permissões IP enquanto a assimilação está em execução.
* Pode haver outros motivos que precisem de investigação. Se a assimilação continuar a falhar, entre em contato com o Atendimento ao cliente da Adobe.

### As Atualizações Automáticas através do Release Orchestrator ainda estão habilitadas

O Release Orchestrator mantém os ambientes atualizados automaticamente ao aplicar atualizações automaticamente. Se a atualização for acionada quando uma assimilação estiver sendo executada, poderá causar resultados imprevisíveis, incluindo a corrupção do ambiente. Esse é um dos motivos pelos quais um tíquete de suporte deve ser registrado antes de iniciar uma assimilação (consulte a &quot;Observação&quot; acima), para que a desativação temporária do Release Orchestrator possa ser programada.

Se o Release Orchestrator ainda estiver em execução quando uma assimilação estiver sendo iniciada, a interface do usuário apresentará essa mensagem. Você pode optar por continuar mesmo assim, aceitando o risco, marcando o campo e pressionando o botão novamente.

>[!NOTE]
>
> O Release Orchestrator agora está sendo implantado em ambientes de desenvolvimento, portanto, as atualizações pausadas nesses ambientes também devem ser feitas.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Falha na assimilação complementar

Uma causa comum de [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) a falha é um conflito nas ids do nó. Para identificar esse erro, baixe o log de assimilação usando a interface do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: propriedade violada de restrição de exclusividade [jcr:uuid] com valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nó no AEM deve ter um uuid exclusivo. Esse erro indica que um nó que está sendo assimilado tem a mesma uuid que uma que já existe em um caminho diferente na instância de destino.
Isso pode acontecer se um nó for movido na origem entre uma extração e uma extração subsequente [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Isso também pode acontecer se um nó no público-alvo for movido entre uma assimilação e uma assimilação complementar subsequente.

Este conflito deve ser resolvido manualmente. Alguém familiarizado com o conteúdo deve decidir qual dos dois nós deve ser excluído, tendo em mente outro conteúdo que faça referência a ele. A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo.

## O que vem a seguir {#whats-next}

Depois de concluir a assimilação de conteúdo no Target, você poderá visualizar os logs de cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) para saber mais.
