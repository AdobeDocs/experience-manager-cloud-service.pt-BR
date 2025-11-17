---
title: Assimilar conteúdo no Cloud Service
description: Saiba como usar o Cloud Acceleration Manager para assimilar conteúdo do seu conjunto de migração em uma instância do Cloud Service de destino.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 7c0703d746601742a28c3c98f35e69de70f25e05
workflow-type: tm+mt
source-wordcount: '3647'
ht-degree: 11%

---

# Assimilar conteúdo no Cloud Service {#ingesting-content}

## Processo de ingestão no Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingestão de conteúdo"
>abstract="Ingestão refere-se à ingestão de conteúdo do conjunto de migração na instância de destino do Cloud Service. A ferramenta de transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content#top-up-extraction-process" text="Extração complementar"

Siga as etapas abaixo para assimilar seu conjunto de migração usando o Cloud Acceleration Manager:

1. Vá para o Cloud Acceleration Manager. Clique no cartão do projeto e no cartão Transferência de conteúdo. Navegue até **Trabalhos de assimilação** e clique em **Nova assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise a lista de verificação de assimilação e verifique se todas as etapas foram concluídas. Essas etapas são necessárias para garantir uma assimilação bem-sucedida. Vá para a etapa **Avançar** somente se a lista de verificação estiver concluída.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Forneça as informações necessárias para criar uma assimilação.

   * **Conjunto de migração:** selecione o conjunto de migração que contém os dados extraídos como o Source.
      * Os conjuntos de migração expirarão após um período prolongado de inatividade, de modo que é esperado que a assimilação ocorra relativamente logo após a extração ter sido realizada. Revise a [Expiração do Conjunto de Migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   >[!TIP]
   > Se a extração estiver em execução, a caixa de diálogo a indicará. Depois que a extração for concluída com sucesso, a assimilação será iniciada automaticamente. Se a extração falhar ou for interrompida, o trabalho de assimilação será rescindido.

   * **Destino:** selecione o ambiente de destino. É nesse ambiente que o conteúdo do conjunto de migração é assimilado.
      * As assimilações não são compatíveis com destinos do tipo RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) ou pré-visualização e não aparecem como uma possível escolha de destino, mesmo que o usuário tenha acesso a elas.
      * Embora um conjunto de migração possa ser assimilado em vários destinos simultaneamente, um destino pode ser o destino de apenas um em execução ou aguardando assimilação por vez.

   * **Camada:** Selecione a camada. (Autor/Publicação).
      * Se a origem foi `Author`, é recomendável assimilá-la na camada `Author` no destino. Da mesma forma, se a origem fosse `Publish`, o destino também deveria ser `Publish`.

   >[!NOTE]
   > Se a camada de destino for `Author`, a instância de autor será desligada durante a duração da assimilação e ficará indisponível para os usuários (por exemplo, autores ou qualquer pessoa que esteja executando a manutenção). O motivo é proteger o sistema e evitar quaisquer alterações que possam ser perdidas ou causar um conflito de assimilação. Confirme se sua equipe está ciente desse fato. Observe também que o ambiente parece hibernado durante a assimilação do autor.

   >[!NOTE]
   > Se a camada de destino for `Publish`, a instância de publicação permanecerá em execução durante a assimilação.  No entanto, se o processo de compactação estiver em execução durante a assimilação, é provável que ocorra um conflito entre os dois processos.  Por esse motivo, o processo de assimilação 1) desativa o script de compactação cronometrado, de modo que a compactação não será iniciada durante a assimilação e 2) verifica se a compactação está em execução no momento e, se estiver, aguarda a conclusão antes que a assimilação continue.  Se a assimilação de publicação estiver demorando mais do que o esperado, verifique os logs de assimilação para obter as instruções de log relacionadas.

   * **Apagar:** Escolha o valor `Wipe`
      * A opção **Apagar** define o ponto inicial de destino da assimilação. Se **Apagar** estiver habilitado, o destino, incluindo todo o seu conteúdo, será redefinido para a versão do AEM especificada no Cloud Manager. Se não estiver ativado, o destino mantém o conteúdo atual como ponto de partida.
      * Esta opção **NÃO** afeta como a assimilação de conteúdo será realizada. A assimilação sempre usa uma estratégia de substituição de conteúdo e _não_ uma estratégia de mesclagem de conteúdo, portanto, em ambos os casos **Apagar** e **Não-Apagar**, a assimilação de um conjunto de migração substituirá o conteúdo no mesmo caminho no destino. Por exemplo, se o conjunto de migração contiver `/content/page1` e o destino já contiver `/content/page1/product1`, a assimilação removerá todo o caminho `page1` e suas subpáginas, incluindo `product1`, e substituirá pelo conteúdo no conjunto de migração. Isso significa que é necessário fazer um planejamento cuidadoso ao executar uma assimilação **Não-apagada** para um destino que contenha qualquer conteúdo que deva ser mantido.
      * As assimilações que não são de limpeza são projetadas especificamente para o caso de uso de assimilação complementar. Essas assimilações devem ter uma quantidade incremental de novo conteúdo que foi alterado desde a última assimilação em um conjunto de migração existente. Executar assimilações que não são de limpeza fora desse caso de uso pode resultar em tempos de assimilação muito longos.

   >[!IMPORTANT]
   > Se a configuração **Limpar** estiver habilitada para a assimilação, ela redefinirá todo o repositório existente, incluindo as permissões de usuário na instância do Cloud Service de destino. Essa redefinição também é válida para um usuário administrador adicionado ao grupo **administradores** e esse usuário deve ser adicionado ao grupo de administradores novamente para iniciar uma assimilação.

   * **Pré-cópia:** Escolha o valor `Pre-copy`
      * Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a assimilação. Consulte [Assimilar com AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.
      * Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação `Author` sozinha. Isso acelera a assimilação de `Publish` quando executada posteriormente.

   >[!IMPORTANT]
   > Você só poderá iniciar uma assimilação no ambiente de destino se pertencer ao grupo local de **administradores do AEM** no serviço de autor do Cloud Service de destino. Se você não conseguir iniciar uma assimilação, consulte [Não foi possível iniciar a assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obter mais detalhes.

1. Depois que as opções de assimilação forem selecionadas, uma estimativa de sua duração poderá ser mostrada. Esta é uma estimativa de melhor esforço com base em dados históricos de assimilações semelhantes.

   * Esta estimativa não é calculada ou mostrada para **assimilações que não sejam de limpeza**, já que o CAM não sabe quanto conteúdo está no sistema de destino neste caso.
   * Essa estimativa só será calculada e mostrada se os valores de &quot;Verificar tamanho&quot; da extração tiverem sido coletados e estiverem disponíveis.
   * Este valor é uma estimativa e, embora calculado inteligentemente, não deve ser considerado exato. Vários fatores podem alterar a duração real.
   * Enquanto a assimilação estiver em execução, esse valor também estará disponível na caixa de diálogo de durações, acessada por meio da ação &quot;**Exibir durações**&quot; da assimilação.

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="Duração estimada da ingestão"
>abstract="Uma duração aproximada de uma ingestão específica pode ser exibida para fornecer uma noção geral de quanto tempo ela levará. Sua precisão é limitada."

![imagem](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. Clique em **Assimilar**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Em seguida, é possível monitorar a assimilação na exibição de lista dos Trabalhos de assimilação e usar o menu de ação da assimilação para exibir as durações e registrar o progresso da assimilação.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Clique no botão **(i)** na linha para obter mais informações sobre o trabalho de assimilação. Você pode ver a duração de cada etapa da assimilação quando ela estiver em execução ou concluída clicando em **...** e em **Exibir durações**. As informações da extração também são mostradas para perceber o que está sendo assimilado.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Ingestão complementar {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingestão complementar"
>abstract="Use o recurso complementar para mover o conteúdo modificado desde a atividade de transferência de conteúdo anterior. Após a conclusão da ingestão, verifique os logs em busca de erros ou avisos. Todos os erros devem ser resolvidos imediatamente, seja resolvendo os problemas relatados ou entrando em contato com o Atendimento ao cliente da Adobe."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs" text="Exibir logs"

A ferramenta Transferência de conteúdo tem um recurso que permite a extração de conteúdo diferencial executando um *complemento* do conjunto de migração. Isso permite que o conjunto de migração seja modificado para incluir somente o conteúdo que foi alterado desde a extração anterior, sem precisar extrair todo o conteúdo novamente.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira assimilação, poderá ignorar a pré-cópia para assimilações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB). O motivo é que isso pode adicionar tempo a todo o processo.

Para assimilar conteúdo diferencial depois que algumas assimilações forem concluídas, execute uma [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) e use o método de assimilação com a opção **Apagar** **desabilitada**. Leia a explicação **Apagar** acima para evitar a perda do conteúdo que já está no destino.

Comece criando uma tarefa de assimilação e verifique se **Apagar** está desativado durante a assimilação, conforme mostrado abaixo:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolução de problemas {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Solução de problemas de ingestão de conteúdo"
>abstract="Consulte os logs de ingestão e a documentação para descobrir os motivos comuns pelos quais uma ingestão pode falhar e uma maneira de corrigir o problema. Depois de corrigida, a ingestão pode ser executada novamente."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers" text="Validar transferências de conteúdo"

### O CAM não consegue recuperar o token de migração {#cam-unable-to-retrieve-the-migration-token}

A recuperação automática do token de migração pode falhar por diferentes motivos, incluindo você [configurar uma lista de permissões IP via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) no ambiente Cloud Service de destino. Nesses cenários, você verá a seguinte caixa de diálogo ao tentar iniciar uma assimilação:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupere o token de migração manualmente clicando no link &quot;Obter token&quot; na caixa de diálogo. Outra guia é aberta exibindo o token. Em seguida, você pode copiar o token e colá-lo no campo **Entrada do token de migração**. Agora, você pode começar a assimilação.

>[!NOTE]
>
>O token está disponível para usuários que pertencem ao grupo local **administradores do AEM** no serviço de autor do Cloud Service de destino.

### Não foi possível iniciar a assimilação {#unable-to-start-ingestion}

Você só poderá iniciar uma assimilação no ambiente de destino se pertencer ao grupo local de **administradores do AEM** no serviço de autor do Cloud Service de destino. Se você não pertence ao grupo de administradores do AEM, você vê um erro como mostrado abaixo ao tentar iniciar uma assimilação. Você pode pedir ao administrador para adicioná-lo aos **administradores do AEM** locais ou solicitar o token propriamente dito, que você pode colar no campo **Entrada de token de migração**.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Não é possível acessar o serviço de migração {#unable-to-reach-migration-service}

Depois que uma assimilação é solicitada, uma mensagem como a seguinte pode ser apresentada ao usuário: &quot;O serviço de migração no ambiente de destino está inacessível. Em caso afirmativo, tente novamente mais tarde ou entre em contato com o suporte da Adobe.&quot;

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Esta mensagem indica que o Cloud Acceleration Manager não conseguiu acessar o serviço de migração do ambiente de destino para iniciar a assimilação. Essa situação pode ocorrer por vários motivos.

>[!NOTE]
> 
> O campo &quot;Token de migração&quot; é exibido porque, em alguns casos, a recuperação desse token é o que realmente não é permitido. Ao permitir que seja fornecido manualmente, ele pode permitir que o usuário inicie a assimilação rapidamente, sem nenhuma ajuda adicional. Se o token for fornecido e a mensagem ainda for exibida, a recuperação do token não foi o problema.

* A AEM as a Cloud Service mantém o estado do ambiente e, ocasionalmente, deve reiniciar o serviço de migração por vários motivos normais. Se esse serviço estiver sendo reiniciado, ele não poderá ser acessado, mas estará disponível no futuro.
* É possível que outro processo esteja sendo executado na instância. Por exemplo, se as [Atualizações de versão do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) estiverem aplicando uma atualização, o sistema pode estar ocupado e o serviço de migração pode ficar indisponível regularmente. Quando esse processo estiver concluído, o início da assimilação poderá ser tentado novamente.
* Se um [Incluo na lista de permissões IP tiver sido aplicado](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) por meio do Cloud Manager, ele impedirá que o Cloud Acceleration Manager acesse o serviço de migração. Um endereço IP não pode ser adicionado para assimilações porque seu endereço é dinâmico. Atualmente, a única solução é desabilitar o incluo na lista de permissões IP durante o processo de assimilação e indexação, adicionando temporariamente 0.0.0.0/0 ao incluo na lista de permissões enquanto o processo de assimilação e indexação está em execução.
* Pode haver outros motivos que precisem de investigação. Se a assimilação ou indexação continuar a falhar, entre em contato com o Atendimento ao cliente da Adobe.

### Atualizações e assimilações de versão do AEM {#aem-version-updates-and-ingestions}

[As Atualizações de Versão do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) são aplicadas automaticamente aos ambientes para mantê-los atualizados com a versão mais recente do AEM as a Cloud Service. Se a atualização for acionada quando uma assimilação for executada, poderá causar resultados imprevisíveis, incluindo a corrupção do ambiente.

Se as &quot;Atualizações de versão do AEM&quot; estiverem integradas no programa de destino, o processo de assimilação tentará desativar sua fila antes de ser iniciado. Quando a assimilação é concluída, o estado do atualizador de versão retorna ao estado em que estava antes de as assimilações começarem.

>[!NOTE]
>
> Não é mais necessário registrar um tíquete de suporte para desativar a opção &quot;Atualizações de versão do AEM&quot;.

Se &quot;Atualizações de versão do AEM&quot; estiver ativo (ou seja, as atualizações estão em execução ou estão na fila para execução), a assimilação não será iniciada e a interface do usuário apresentará a seguinte mensagem. Quando as atualizações estiverem concluídas, a assimilação poderá ser iniciada. O Cloud Manager pode ser usado para ver o estado atual dos pipelines do programa.

>[!NOTE]
>
> &quot;Atualizações de versão do AEM&quot; é executado no pipeline do ambiente e aguarda até que o pipeline esteja limpo. Se as atualizações forem enfileiradas por mais tempo do que o esperado, verifique se um fluxo de trabalho personalizado não tem o pipeline bloqueado involuntariamente.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Falha de ingestão devido ao Ambiente de nuvem não estar no estado pronto {#ingestion-failure-due-to-cloud-environment-not-in-ready-state}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_cloud_environment_not_in_ready_state"
>title="O Ambiente de nuvem não está no estado pronto"
>abstract="Em casos raros, o ambiente de nuvem de destino pode estar enfrentando problemas inesperados, o que causará a falha da ingestão."

Em casos raros, o ambiente Cloud Service de destino da assimilação pode estar com problemas inesperados. Como resultado, a assimilação falhará, pois o ambiente não está no estado pronto esperado. Verifique o log de assimilação para revelar mais detalhes do estado de erro encontrado.

Verifique se o ambiente de criação está disponível e aguarde alguns minutos antes de tentar assimilar novamente. Se o problema persistir, entre em contato com o suporte ao cliente com o estado de erro encontrado.

### Falha na ingestão complementar devido a uma violação da restrição de exclusividade {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="Violação da restrição de exclusividade"
>abstract="Uma causa comum da falha de exclusão do conteúdo durante a ingestão é um conflito nas IDs dos nós. Somente um dos nós em conflito pode existir."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Ingestão complementar"

Uma causa comum de uma falha de [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) é um conflito nas IDs do nó. Para identificar esse erro, baixe o log de assimilação usando a interface do usuário do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Propriedade violada de restrição de exclusividade [jcr:uuid] com valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nó no AEM deve ter um uuid exclusivo. Esse erro indica que um nó que está sendo assimilado tem a mesma uuid que existe em um caminho diferente na instância de destino. Essa situação pode ocorrer por dois motivos:

* Um nó é movido na origem entre uma extração e uma [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) subsequente
   * _LEMBRAR_: para extrações complementares, o nó ainda existirá no conjunto de migração, mesmo que não exista mais na origem.
* Um nó no destino é movido entre uma assimilação e uma assimilação complementar subsequente.

Este conflito deve ser resolvido manualmente. Alguém familiarizado com o conteúdo deve decidir qual dos dois nós deve ser excluído, tendo em mente outro conteúdo que faça referência a ele. A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo.

### Falha na ingestão complementar devido à impossibilidade de excluir o nó referenciado {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="Não é possível excluir o nó referenciado"
>abstract="Uma causa comum da falha de exclusão do conteúdo durante a ingestão é um conflito de versão de um determinado nó na instância de destino. As versões do nó precisam ser corrigidas."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Ingestão complementar"

Outra causa comum de uma falha de [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) é um conflito de versão para um determinado nó na instância de destino. Para identificar esse erro, baixe o log de assimilação usando a interface do usuário do Cloud Acceleration Manager e procure uma entrada como a seguinte:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001: não é possível excluir o nó referenciado: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Isso poderá acontecer se um nó no destino for modificado entre uma assimilação e uma assimilação **Não apagável** subsequente, de modo que uma nova versão tenha sido criada. Se o conjunto de migração foi extraído com a opção &quot;incluir versões&quot; ativada, pode ocorrer um conflito, pois o destino agora tem uma versão mais recente que está sendo referenciada pelo histórico de versões e outro conteúdo. O processo de assimilação não pode excluir o nó de versão incorreto porque ele está sendo referenciado.

A solução pode exigir que a extração complementar seja feita novamente sem o nó ofensivo. Ou criar um pequeno conjunto de migração do nó incorreto, mas com a opção &quot;incluir versões&quot; desativada.

As práticas recomendadas indicam que, se uma assimilação de **Não apagável** precisar ser executada usando um conjunto de migração que inclua versões, é fundamental que o conteúdo no destino seja modificado o mínimo possível, até que a jornada de migração seja concluída. Caso contrário, esses conflitos poderão ocorrer.

### Falha na ingestão devido a valores grandes de propriedade de nó {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="Propriedade de nó grande"
>abstract="Uma causa comum de falha na ingestão é ao exceder o tamanho máximo dos valores de propriedade do nó. Siga a documentação, incluindo as relacionadas ao relatório do BPA, para corrigir essa situação."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool" text="Pré-requisitos de migração"

Os valores de propriedade do nó armazenados no MongoDB não podem exceder 16 MB. Se um valor de nó exceder o tamanho compatível, a assimilação falhará e o log conterá:

* um erro `BSONObjectTooLarge` e especificar qual nó excedeu o máximo, ou
* um erro `BsonMaximumSizeExceededException`, que indica que provavelmente há um nó contendo caracteres unicode excedendo o tamanho máximo **

Essa é uma restrição MongoDB.

Consulte a observação `Node property value in MongoDB` em [Pré-requisitos da Ferramenta de Transferência de Conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md) para obter mais informações e um link para uma ferramenta Oak que possa ajudar a encontrar todos os nós grandes. Depois que todos os nós com tamanhos grandes forem corrigidos, execute a extração e a assimilação novamente.

Para evitar possivelmente essa restrição, execute o [Analisador de Práticas Recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) na instância do AEM de origem e revise as descobertas apresentadas, especialmente o padrão [&quot;Estrutura de Repositório Sem Suporte&quot; (URS)](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/urs).

>[!NOTE]
>
>O [Analisador de Práticas Recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) versão 2.1.50+ informará sobre nós grandes que contêm caracteres unicode que excedem o tamanho máximo. Verifique se você está executando a versão mais recente. As versões do BPA anteriores à versão 2.1.50 não identificarão e relatarão esses nós grandes e precisarão ser descobertas separadamente usando a ferramenta de pré-requisito do Oak mencionada acima.

### Falha de ingestão devido a erros intermitentes inesperados {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="Erros intermitentes inesperados"
>abstract="Às vezes, erros intermitentes e inesperados do serviço downstream podem ocorrer e, infelizmente, o único recurso é simplesmente repetir a ingestão."

Às vezes, questões intermitentes inesperadas podem se prestar a assimilações fracassadas, onde infelizmente o único recurso é tentar novamente a assimilação. Investigue o log de assimilação para descobrir a causa da falha e ver se ele está alinhado a qualquer um dos erros listados abaixo, onde uma nova tentativa deve ser feita.

#### Problemas do MongoDB {#mongo-db-issues}

* `Atlas prescale timeout error` - A fase de assimilação tentará dimensionar previamente o banco de dados de nuvem de destino para um tamanho adequado que se alinhe ao tamanho do conteúdo do conjunto de migração que está sendo assimilado. Raramente, essa operação não é concluída dentro do período esperado.
* `Exhausted mongo restore retries` - As tentativas de restaurar um despejo local do conteúdo do conjunto de migração assimilado para o banco de dados de nuvem se esgotaram. Isso indica um problema geral de integridade/rede com o MongoDB, que muitas vezes se cura após alguns minutos.
* `Mongo network error` - Às vezes, estabelecer uma conexão com MongoDB pode falhar, fazendo com que o processo de assimilação saia antes e relate-o como falho. Uma simples tentativa de assimilação deve ser feita.
* `Mongo server selection error` - Este é um erro raro de tempo limite do lado do cliente mongo que pode ocorrer por vários motivos subjacentes. Uma nova tentativa provavelmente corrigirá o problema.
* `Mongo took too long to start` - Em casos extremamente raros, o MongoDB local usado no fluxo de trabalho de assimilação pode falhar ao iniciar. Uma nova tentativa provavelmente corrigirá o problema.

#### Problemas do AZCopy {#azcopy-issues}

* `AZCopy critical failure` - Em casos raros, a ferramenta AZCopy usada para executar a etapa de pré-cópia da assimilação pode falhar inesperadamente. Uma nova tentativa de assimilação deve ser tentada nesse caso.

### Ingestão cancelada {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="Ingestão cancelada"
>abstract="A extração que a ingestão aguardava não foi concluída com sucesso. A ingestão foi cancelada porque não pôde ser executada."

Uma assimilação criada com uma extração em execução, à medida que seu conjunto de migração de origem aguarda pacientemente até que a extração seja bem-sucedida, e nesse ponto começa normalmente. Se a extração falhar ou for interrompida, a assimilação e seu trabalho de indexação não serão iniciados, mas serão rescindidos. Nesse caso, verifique a extração para determinar por que ela falhou, corrija o problema e comece a extrair novamente. Uma vez que a extração fixa estiver em execução, uma nova assimilação pode ser programada.

### Falha ao iniciar espera da assimilação {#waiting-ingestion-not-started}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_waiting_ingestion_not_started"
>title="Espera da assimilação não iniciada"
>abstract="Falha ao iniciar a assimilação após aguardar a conclusão de uma extração."

Uma assimilação criada com uma extração em execução enquanto seu conjunto de migração de origem aguarda até que a extração seja bem-sucedida e, nesse ponto, a assimilação tenta iniciar normalmente. Se a assimilação não for iniciada, ela será marcada como com falha. Possíveis motivos para não iniciar são: uma Lista de permissões IP é configurada no ambiente de autor de destino; o ambiente de destino não está disponível por algum outro motivo.  Nesse caso, verifique por que a assimilação falhou ao iniciar, corrija o problema e inicie a assimilação novamente (não há necessidade de executar novamente a extração).

### O ativo excluído não está presente após executar a assimilação novamente

Em geral, não é recomendado modificar os dados do ambiente de nuvem entre as assimilações.

Quando um ativo é excluído do destino do Cloud Service usando a interface para toque do Assets, os dados do nó são excluídos, mas o blob de ativos com a imagem não é excluído imediatamente. Ele é marcado para exclusão para que não apareça mais na interface do usuário; no entanto, permanece no armazenamento de dados até que a coleta de lixo ocorra e o blob seja removido.

No cenário em que um ativo migrado anteriormente é excluído e a próxima assimilação é executada antes que o coletor de lixo conclua a exclusão do ativo, a assimilação do mesmo conjunto de migração não restaurará o ativo excluído. Quando a assimilação verifica o ambiente de nuvem para o ativo, não há dados de nó; portanto, a assimilação copiará os dados do nó para o ambiente de nuvem. No entanto, quando ele verifica o armazenamento de blob, ele vê que o blob está presente e ignora a cópia do blob. É por isso que os metadados estão presentes após a assimilação quando você observa o ativo da interface para toque, mas a imagem não está. Lembre-se de que os conjuntos de migração e a assimilação de conteúdo não foram projetados para lidar com esse caso. Eles têm como objetivo adicionar novo conteúdo ao ambiente de nuvem e não restaurar o conteúdo migrado anteriormente.

## O que vem a seguir {#whats-next}

Quando a assimilação for bem-sucedida, a indexação do AEM será iniciada automaticamente. Consulte [Indexação após Migrar Conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) para obter mais informações.

Depois de concluir a assimilação de conteúdo no Cloud Service, você pode visualizar os logs de cada etapa (extração e assimilação) e procurar erros. Consulte [Exibir Logs de um Conjunto de Migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) para saber mais.
