---
title: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
description: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: d07a4fd0a335295d399057ea1eef567e757e2d92
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 18%

---

# Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo {#guidelines}

## Diretrizes e práticas recomendadas {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Diretrizes e práticas recomendadas"
>abstract="Analise as diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo, incluindo tarefas de limpeza de revisão, considerações de espaço em disco e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerações importantes sobre o uso da ferramenta Mapeamento de usuários"

Uma nova versão da ferramenta Transferência de conteúdo está disponível e integra o processo de transferência de conteúdo ao Cloud Acceleration Manager. É altamente recomendável mudar para essa nova versão para aproveitar todos os benefícios que ela oferece:

* Maneira de autoatendimento de extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes em paralelo
* Melhoria na experiência do usuário por meio de melhores estados de carregamento, medidas de proteção e tratamento de erros
* Os logs de assimilação são persistentes e sempre estão disponíveis para solução de problemas

Para começar a usar a nova versão, será necessário desinstalar versões mais antigas da ferramenta Transferência de conteúdo. Isso é necessário porque a nova versão traz uma grande mudança arquitetônica. Com a versão 2.0.10, será necessário criar novos conjuntos de migração e executar novamente a extração e a assimilação nos novos conjuntos de migração. Se uma migração já estiver em andamento, você poderá continuar usando a versão anterior da CTT até que a migração seja concluída.
As versões anteriores à 2.0.0 não serão mais suportadas e é recomendável usar a versão mais recente.

As diretrizes e práticas recomendadas a seguir se aplicam à nova versão da ferramenta Transferência de conteúdo:

* É aconselhável executar a [Limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e as [verificações de consistência do armazenamento de dados](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) no repositório de **origem** para identificar possíveis problemas e reduzir o tamanho do repositório.

* Na fase de assimilação, é recomendável executar a assimilação usando o modo de *limpeza* ativado, no qual o repositório existente (autor ou publicação) no ambiente de serviço do AEM Cloud Service será completamente excluído e depois atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a ferramenta Transferência de conteúdo, verifique se há espaço em disco suficiente no subdiretório `crx-quickstart` da instância de origem do AEM. Isso ocorre porque a ferramenta Transferência de conteúdo cria uma cópia local do repositório que depois é carregada no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
   `data store size + node store size * 1.5`

   * *tamanho do armazenamento de dados*: a ferramenta Transferência de conteúdo usa 64 GB, mesmo que o armazenamento de dados real seja maior.
   * *tamanho do armazenamento do nó*: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmentos de 20 GB, o espaço livre em disco necessário seria de 94 GB.

* Um conjunto de migração precisa ser mantido durante toda a atividade de transferência de conteúdo para oferecer suporte a atualizações complementares de conteúdo. No máximo cinco conjuntos de migração por projeto no Cloud Acceleration Manager podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo. Se mais de cinco conjuntos de migração forem necessários, será necessário criar um segundo projeto no Cloud Acceleration Manager. No entanto, isso exigirá gerenciamento de projeto adicional e controle fora do produto para evitar a substituição do conteúdo no público-alvo por vários usuários.

## Considerações importantes antes de usar a ferramenta Transferência de conteúdo {#important-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e o JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java deve ser configurado no ambiente de AEM, para que a variável `java` pode ser executado pelo usuário que inicia o AEM.

* A ferramenta Transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Armazenamento de dados de arquivo, Armazenamento de dados S3, Armazenamento de dados S3 compartilhado e Armazenamento de dados do Azure Blob Store.

* Se estiver usando um *Ambiente de sandbox*, certifique-se de que seu ambiente esteja atualizado e seja atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para iniciar uma assimilação, você precisa pertencer ao AEM local **administradores** na instância do Cloud Service para a qual você está transferindo conteúdo. Os usuários sem privilégios não poderão iniciar ingestões sem fornecer manualmente o token de migração.

* Se a configuração **Limpar o conteúdo existente na instância do Cloud antes da assimilação** estiver ativada, ela excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao **administradores** grupo. O usuário deve ser adicionado novamente ao **administradores** para recuperar o token de acesso da ferramenta Transferência de conteúdo.

* As assimilações não oferecem suporte à mesclagem de conteúdo de várias fontes na instância do Cloud Service de destino se o conteúdo das duas fontes for movido para os mesmos caminhos no destino. Para mover o conteúdo de várias fontes para uma única instância do Cloud Service de destino, você precisa garantir que não haja sobreposição dos caminhos de conteúdo das fontes.

* A chave de extração é válida por 14 dias a partir do momento em que foi criada/renovada. Pode ser renovado a qualquer momento. Se a chave de extração tiver expirado, você não poderá executar uma extração.

* A Ferramenta de transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado enquanto assimila conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração será assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou de Publicação ou em ambos. Recomenda-se que, ao mover o conteúdo para uma instância de Produção, a CTT seja instalada na instância de Autor de origem para mover o conteúdo para a instância de Autor de destino e, de forma semelhante, instale a CTT na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Execução da ferramenta Transferência de conteúdo em uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) para obter mais detalhes.

* Os Usuários e grupos transferidos pela ferramenta Transferência de conteúdo são apenas aqueles que são exigidos pelo conteúdo para atender às permissões. O *Extração* o processo copia todo o `/home` no conjunto de migração e na variável *Assimilação* O processo copia todos os usuários e grupos referenciados nas ACLs do conteúdo migrado. Para mapear automaticamente os usuários existentes para suas IDs IMS, consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* Depois de concluir o *Extração* fase do processo de transferência de conteúdo e antes de iniciar o *Fase de assimilação* para assimilar conteúdo em seu AEM as a Cloud Service *Fase* ou *Produção* , será necessário registrar um tíquete de suporte para notificar o Adobe de sua intenção de executar *Assimilação* para que o Adobe possa garantir que não ocorram interrupções durante a *Assimilação* processo. Você precisará registrar o tíquete de suporte uma semana antes do período planejado *Assimilação* data. Depois de enviar o tíquete de suporte, a equipe de suporte fornecerá orientação sobre as próximas etapas. Você pode registrar um tíquete de suporte com os seguintes detalhes:

   * Data exata e hora estimada (com seu fuso horário) quando você planeja iniciar a *Assimilação* fase.
   * Tipo de ambiente (Preparo ou Produção) no qual você planeja assimilar dados.
   * ID do programa.

* O *Fase de assimilação* para o autor, o dimensiona toda a implantação do autor. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão. Certifique-se também de que nenhum pipeline do Cloud Manager seja executado durante a execução do *Assimilação* fase.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema de AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados de índice e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se estiver usando índices personalizados, certifique-se de configurar os índices personalizados com `tika` antes de executar a ferramenta Transferência de conteúdo. Consulte [Preparando a Nova Definição de Índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações adicionais, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

* Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações adicionais com `wipe=false`, você deve desativar a limpeza de versão devido a uma limitação atual na ferramenta Transferência de conteúdo. Se você preferir manter a limpeza de versão ativada e estiver executando os upups em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.

## O que vem a seguir {#whats-next}

Depois de conhecer as diretrizes, as práticas recomendadas e as considerações importantes para o uso da ferramenta Transferência de conteúdo, você estará pronto para instalar e usar a ferramenta, começando pela criação de um conjunto de migração. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para saber mais.
