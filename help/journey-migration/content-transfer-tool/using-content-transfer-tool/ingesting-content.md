---
title: Assimilar conteúdo no Cloud Service
description: Saiba como usar o Cloud Acceleration Manager para assimilar conteúdo do seu conjunto de migração em uma instância do Cloud Service de destino.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 7%

---

# Assimilar conteúdo no Cloud Service {#ingesting-content}

## Processo de assimilação no Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Assimilação de conteúdo"
>abstract="Assimilação refere-se à assimilação de conteúdo do conjunto de migração na instância de destino do Cloud Service. A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=pt-BR#top-up-extraction-process" text="Extração complementar"

Siga as etapas abaixo para assimilar seu conjunto de migração usando o Cloud Acceleration Manager:

1. Acesse o Cloud Acceleration Manager. Clique no cartão do projeto e no cartão Transferência de conteúdo. Navegue até **Tarefas de assimilação** e clique em **Nova assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise a lista de verificação de assimilação e verifique se todas as etapas foram concluídas. Essas etapas são necessárias para garantir uma assimilação bem-sucedida. Vá para a página **Próxima** etapa somente se a lista de verificação estiver concluída.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Forneça as informações necessárias para criar uma assimilação.

   * **Conjunto de migração:** Selecione o conjunto de migração que contém os dados extraídos como Origem.
      * Os conjuntos de migração expirarão após um período prolongado de inatividade, de modo que é esperado que a assimilação ocorra relativamente logo após a extração ter sido realizada. Revisão [Expiração do conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   >[!TIP]
   > Se a extração estiver em execução no momento, a caixa de diálogo indicará. Depois que a extração for concluída com sucesso, a assimilação será iniciada automaticamente. Se a extração falhar ou for interrompida, o trabalho de assimilação será rescindido.

   * **Destino:** Selecione o ambiente de destino. É nesse ambiente que o conteúdo do conjunto de migração é assimilado.
      * As assimilações não são compatíveis com um destino de RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) e não aparecem como uma possível escolha de destino, mesmo que o usuário tenha acesso a ele.
      * Embora um conjunto de migração possa ser assimilado em vários destinos simultaneamente, um destino pode ser o destino de apenas um em execução ou aguardando assimilação por vez.

   * **Camada:** Selecione a camada. (Autor/Publicação).
      * Se a origem foi `Author`, é recomendável assimilá-lo na `Author` no target. Da mesma forma, se a origem foi `Publish`, o target deve ser `Publish` também.

   >[!NOTE]
   > Se a camada de destino for `Author`, a instância do autor é encerrada durante a duração da assimilação e fica indisponível para os usuários (por exemplo, autores ou qualquer pessoa que esteja executando a manutenção). O motivo é proteger o sistema e evitar quaisquer alterações que possam ser perdidas ou causar um conflito de assimilação. Confirme se sua equipe está ciente desse fato. Observe também que o ambiente parece hibernado durante a assimilação do autor.

   * **Apagar:** Escolha o `Wipe` value
      * A variável **Limpar** define o ponto inicial do destino da assimilação. Se **Limpar** estiver ativado, o destino, incluindo todo o conteúdo, será redefinido para a versão do AEM especificada no Cloud Manager. Se não estiver ativado, o destino mantém o conteúdo atual como ponto de partida.
      * Observe que essa opção não **NOT** afetam como a assimilação do conteúdo será realizada. A assimilação sempre usa uma estratégia de substituição de conteúdo e _não_ uma estratégia de mesclagem de conteúdo para que, em ambos **Limpar** e **Não-apagamento** nos casos, a assimilação de um conjunto de migração substituirá o conteúdo no mesmo caminho no destino. Por exemplo, se o conjunto de migração contiver `/content/page1` e o destino já contém `/content/page1/product1`, a assimilação removerá toda a `page1` caminho e suas subpáginas, incluindo `product1`e substitua-o pelo conteúdo no conjunto de migração. Isso significa que é necessário fazer um planejamento cuidadoso ao executar um **Não-apagamento** assimilação para um destino que contém qualquer conteúdo que deve ser mantido.

   >[!IMPORTANT]
   > Se a configuração **Limpar** estiver ativado para a assimilação, ele redefinirá todo o repositório existente, incluindo as permissões do usuário na instância do Cloud Service de destino. Essa redefinição também é verdadeira para um usuário administrador adicionado à variável **administradores** e esse usuário deverá ser adicionado ao grupo de administradores novamente para iniciar uma assimilação.

   * **Pré-cópia:** Escolha o `Pre-copy` value
      * Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a assimilação. Consulte [Assimilar com AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.
      * Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar `Author` ingestão primeiro sozinha. Isso acelera o `Publish` assimilação quando executada mais tarde.

   >[!IMPORTANT]
   > Você pode iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino. Se não conseguir iniciar uma assimilação, consulte [Não foi possível iniciar a assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obter mais detalhes.

1. Clique em **Assimilar**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Em seguida, é possível monitorar a assimilação na exibição de lista dos Trabalhos de assimilação e usar o menu de ação da assimilação para exibir as durações e registrar o progresso da assimilação.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Clique em **i)** botão na linha para obter mais informações sobre o trabalho de assimilação. É possível ver a duração de cada etapa da assimilação quando ela está em execução ou concluída clicando em **..** e clicando em **Exibir durações**. As informações da extração também são mostradas para perceber o que está sendo assimilado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Ingestão complementar {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingestão complementar"
>abstract="Use o recurso completar para mover o conteúdo modificado desde a atividade de transferência de conteúdo anterior. Após a conclusão da ingestão, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, seja resolvendo os problemas relatados ou entrando em contato com o Atendimento ao cliente da Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="Exibir logs"

A ferramenta Transferência de conteúdo tem um recurso que permite a extração de conteúdo diferencial executando uma *complementar* do conjunto de migração. Isso permite que o conjunto de migração seja modificado para incluir somente o conteúdo que foi alterado desde a extração anterior, sem precisar extrair todo o conteúdo novamente.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira assimilação, poderá ignorar a pré-cópia para assimilações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB). O motivo é que isso pode adicionar tempo a todo o processo.

Para assimilar conteúdo diferencial depois que algumas assimilações forem concluídas, execute um [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)e, em seguida, use o método de assimilação com a variável **Limpar** opção **desabilitado**. Leia as **Limpar** acima para evitar a perda de conteúdo que já está no destino.

Comece criando uma tarefa de assimilação e verifique se **Limpar** está desativado durante a assimilação, conforme mostrado abaixo:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolução de problemas {#troubleshooting}

### O CAM não consegue recuperar o token de migração {#cam-unable-to-retrieve-the-migration-token}

A recuperação automática do token de migração pode falhar por diferentes motivos, incluindo você [configuração de uma lista de permissões IP via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) no ambiente Cloud Service de destino. Nesses cenários, você verá a seguinte caixa de diálogo ao tentar iniciar uma assimilação:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupere o token de migração manualmente clicando no link &quot;Obter token&quot; na caixa de diálogo. Outra guia é aberta exibindo o token. Em seguida, você pode copiar o token e colá-lo na **Entrada do token de migração** campo. Agora, você pode começar a assimilação.

>[!NOTE]
>
>O token está disponível para usuários que pertencem ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino.

### Não foi possível iniciar a assimilação {#unable-to-start-ingestion}

Você pode iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores do AEM** grupo no serviço de autor do Cloud Service de destino. Se você não pertence ao grupo de administradores do AEM, você vê um erro como mostrado abaixo ao tentar iniciar uma assimilação. Você pode pedir ao administrador para adicioná-lo ao local **Administradores do AEM** ou solicite o token propriamente dito, que você pode colar na **Entrada do token de migração** campo.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Não é possível acessar o serviço de migração {#unable-to-reach-migration-service}

Depois que uma assimilação é solicitada, uma mensagem como a seguinte pode ser apresentada ao usuário: &quot;O serviço de migração no ambiente de destino está inacessível. Em caso afirmativo, tente novamente mais tarde ou entre em contato com o suporte do Adobe.&quot;

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Esta mensagem indica que o Cloud Acceleration Manager não conseguiu acessar o serviço de migração do ambiente de destino para iniciar a assimilação. Essa situação pode ocorrer por vários motivos.

>[!NOTE]
> 
> O campo &quot;Token de migração&quot; é exibido porque, em alguns casos, a recuperação desse token é o que realmente não é permitido. Ao permitir que seja fornecido manualmente, ele pode permitir que o usuário inicie a assimilação rapidamente, sem nenhuma ajuda adicional. Se o token for fornecido e a mensagem ainda for exibida, a recuperação do token não foi o problema.

* O AEM as a Cloud Service mantém o estado do ambiente e, ocasionalmente, deve reiniciar o serviço de migração por vários motivos normais. Se esse serviço estiver sendo reiniciado, ele não poderá ser acessado, mas estará disponível no futuro.
* É possível que outro processo esteja sendo executado na instância. Por exemplo, se [Atualizações de versão do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) estiver aplicando uma atualização, o sistema poderá estar ocupado e o serviço de migração poderá ficar indisponível regularmente. Quando esse processo estiver concluído, o início da assimilação poderá ser tentado novamente.
* Se um [A Inclui na lista de permissões IP foi aplicada](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) Por meio do Cloud Manager, ele impede que o Cloud Acceleration Manager chegue ao serviço de migração. Um endereço IP não pode ser adicionado para assimilações porque seu endereço é dinâmico. Atualmente, a única solução é desativar a lista de permissões IP enquanto a assimilação está em execução.
* Pode haver outros motivos que precisem de investigação. Se a assimilação continuar a falhar, entre em contato com o Atendimento ao cliente da Adobe.

### Atualizações e assimilações de versão do AEM

[Atualizações de versão do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) são automaticamente aplicados a ambientes para mantê-los atualizados com a versão mais recente do AEM as a Cloud Service. Se a atualização for acionada quando uma assimilação for executada, poderá causar resultados imprevisíveis, incluindo a corrupção do ambiente.

Se as &quot;Atualizações de versão do AEM&quot; estiverem integradas no programa de destino, o processo de assimilação tentará desativar sua fila antes de ser iniciado. Quando a assimilação for concluída, o estado do atualizador da versão retornará para como estava antes de as assimilações serem iniciadas.

>[!NOTE]
>
> Não é mais necessário registrar um tíquete de suporte para desativar a opção &quot;Atualizações de versão do AEM&quot;.

Se &quot;Atualizações de versão do AEM&quot; estiver ativo (ou seja, as atualizações estão em execução ou estão na fila para execução), a assimilação não será iniciada e a interface do usuário apresentará a seguinte mensagem. Quando as atualizações estiverem concluídas, a assimilação poderá ser iniciada. O Cloud Manager pode ser usado para ver o estado atual dos pipelines do programa.

>[!NOTE]
>
> &quot;Atualizações de versão do AEM&quot; é executado no pipeline do ambiente e aguardará até que o pipeline esteja limpo. Se as atualizações forem enfileiradas por mais tempo do que o esperado, verifique se um fluxo de trabalho personalizado não tem o pipeline bloqueado involuntariamente.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Falha na assimilação complementar devido à violação de restrição de exclusividade

Uma causa comum de [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) a falha é um conflito nas ids do nó. Para identificar esse erro, baixe o log de assimilação usando a interface do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: propriedade violada de restrição de exclusividade [jcr:uuid] com valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nó no AEM deve ter um uuid exclusivo. Esse erro indica que um nó que está sendo assimilado tem a mesma uuid que existe em outro lugar em um caminho diferente na instância de destino.
Essa situação pode ocorrer se um nó for movido na origem entre uma extração e uma extração subsequente [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Também pode acontecer se um nó no destino for movido entre uma assimilação e uma assimilação complementar subsequente.

Este conflito deve ser resolvido manualmente. Alguém familiarizado com o conteúdo deve decidir qual dos dois nós deve ser excluído, tendo em mente outro conteúdo que faça referência a ele. A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo.

### Falha na assimilação complementar devido à não exclusão do nó referenciado

Outra causa comum de uma [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) falha é um conflito de versão para um determinado nó na instância de destino. Para identificar esse erro, baixe o log de assimilação usando a interface do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001: não é possível excluir o nó referenciado: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Isso pode acontecer se um nó no destino for modificado entre uma assimilação e uma subsequente **Não-apagamento** assimilação, de modo que uma nova versão tenha sido criada. Se o conjunto de migração foi extraído com a opção &quot;incluir versões&quot; ativada, pode ocorrer um conflito, pois o destino agora tem uma versão mais recente que está sendo referenciada pelo histórico de versões e outro conteúdo. O processo de assimilação não poderá excluir o nó de versão incorreto porque ele está sendo referenciado.

A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo. Ou criar um pequeno conjunto de migração do nó incorreto, mas com a opção &quot;incluir versões&quot; desativada.

As práticas recomendadas indicam que, se uma **Não-apagamento** a assimilação deve ser executada usando um conjunto de migração que inclua versões (ou seja, extraído com &quot;incluir versões&quot;=true). é fundamental que o conteúdo no destino seja modificado o mínimo possível, até que a jornada de migração seja concluída. Caso contrário, esses conflitos poderão ocorrer.

### Assimilação cancelada

Uma assimilação criada com uma extração em execução como seu conjunto de migração de origem aguardará pacientemente até que a extração seja bem-sucedida e, nesse momento, iniciará normalmente. Se a extração falhar ou for interrompida, a assimilação e seu trabalho de indexação não serão iniciados, mas serão rescindidos. Nesse caso, verifique a extração para determinar por que ela falhou, corrija o problema e comece a extrair novamente. Uma vez que a extração fixa estiver em execução, uma nova assimilação pode ser programada.

## O que vem a seguir {#whats-next}

Quando a assimilação for bem-sucedida, a indexação do AEM será iniciada automaticamente. Consulte [Indexação após a migração do conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) para obter mais informações.

Depois de concluir a assimilação de conteúdo no Cloud Service, você pode visualizar os registros de cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) para saber mais.
