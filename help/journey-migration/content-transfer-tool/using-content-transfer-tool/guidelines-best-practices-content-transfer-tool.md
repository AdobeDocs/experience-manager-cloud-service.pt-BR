---
title: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
description: Saiba mais sobre as diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo.
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 943685ed9c33ba42c4dd1cb941b2eca1cce8bfe8
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 14%

---


# Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo {#guidelines}

## Diretrizes e práticas recomendadas {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/group-migration.md#important-considerations" text="Important Considerations when Migrating Groups" 

-->

A ferramenta Transferência de conteúdo integra o processo de transferência de conteúdo ao Cloud Acceleration Manager. É necessário usar essa versão (2.0 ou posterior, mas a versão 3.0 agora é recomendada) para obter todos os benefícios que ela oferece:

* Sistema de autoatendimento para extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes em paralelo
* Experiência do usuário aprimorada por meio de melhores estados de carregamento, medidas de proteção e tratamento de erros
* Os logs de ingestão são persistentes e sempre estão disponíveis para solução de problemas

Para começar a usar a versão mais recente, desinstale as versões anteriores da ferramenta Transferência de conteúdo. Com a versão 2.0 e posterior, você cria conjuntos de migração e executa novamente a extração e a assimilação nos conjuntos.
As versões anteriores à 2.0.0 não são compatíveis e recomenda-se usar a versão mais recente.

As diretrizes e práticas recomendadas a seguir se aplicam à nova versão da ferramenta Transferência de conteúdo:

* Execute a [Limpeza de Revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=pt-BR) e as [verificações de consistência do repositório de dados](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=pt-BR) no repositório **origem** para que você possa identificar possíveis problemas e reduzir o tamanho do repositório.

* Na fase de assimilação, a Adobe recomenda que você execute a assimilação usando o modo *wipe* habilitado, no qual o repositório existente (Autor ou Publicação) no ambiente de destino do Adobe Experience Manager (AEM) Cloud Service é excluído. Em seguida, atualize com os dados do conjunto de migração. Esse modo é mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a ferramenta de transferência de conteúdo, verifique se há espaço em disco suficiente no subdiretório `crx-quickstart` da instância de origem do AEM. Isso ocorre porque a ferramenta de transferência de conteúdo cria uma cópia local do repositório que depois é carregada no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
  `data store size + node store size * 1.5`

* *tamanho do armazenamento de dados*: a ferramenta de transferência de conteúdo usa 64 GB, mesmo que o armazenamento de dados real seja maior.
* *tamanho do armazenamento do nó*: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmentos de 20 GB, o espaço livre em disco necessário seria de 94 GB.

* Um conjunto de migração deve ser mantido em toda a atividade de transferência de conteúdo para oferecer suporte a atualizações complementares de conteúdo. No máximo 10 conjuntos de migração por projeto no Cloud Acceleration Manager podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo. Se mais de dez conjuntos de migração forem necessários, crie um segundo projeto no Cloud Acceleration Manager. No entanto, isso requer gerenciamento de projetos adicional e governança fora do produto para evitar a substituição do conteúdo no público-alvo por vários usuários.

* Evite alterar o diretório de instalação da ferramenta CTT. Por padrão, a instalação ocorre no caminho crx-quickstart/cloud-migration. Essa localização específica é usada internamente por outras bibliotecas da. A modificação desse caminho pode resultar em problemas de extração.

## Considerações importantes antes de usar a ferramenta Transferência de conteúdo {#important-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta de transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e Java™ 8. Se você estiver em uma versão inferior do AEM, atualize seu repositório de conteúdo para o AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java™ deve ser configurado no ambiente AEM para que o comando `java` possa ser executado pelo usuário que inicia o AEM.

* A Ferramenta de transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Armazenamento de dados de arquivo, Armazenamento de dados S3, Armazenamento de dados S3 compartilhado e Armazenamento de dados do Azure Blob Store.

* Se você estiver usando um *Ambiente de sandbox*, verifique se ele está atualizado e atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para iniciar uma assimilação, você deve pertencer ao grupo local **administradores** do AEM na instância do Cloud Service para a qual você está transferindo conteúdo. Usuários sem privilégios não podem iniciar assimilações sem fornecer manualmente o token de migração.

* Se a opção **Limpar conteúdo existente na instância da nuvem antes da assimilação** estiver habilitada, ela excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Também é verdadeiro para um usuário administrador adicionado ao grupo **administradores**. O usuário deve ser lido no grupo **administradores** para recuperar o token de acesso para a ferramenta Transferência de conteúdo.

* A chave de extração é válida por 14 dias a partir do momento em que foi criada ou renovada. Ele pode ser renovado a qualquer momento. Se a chave de extração tiver expirado, não será possível executar uma extração.

* A ferramenta Transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado ao assimilar conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração é assimilado na instância de destino escolhida. Um usuário pode assimilar um conjunto de migração em uma instância de Autor ou instância de Publicação, ou em ambas. O Adobe recomenda que, ao mover o conteúdo para uma instância de Produção, a CTT seja instalada na instância do Autor de origem para mover o conteúdo para a instância do Autor de destino. E, da mesma forma, instale a CTT na instância de publicação de origem para mover o conteúdo para a instância de publicação de destino. Consulte [Executando a Ferramenta de Transferência de Conteúdo em uma instância de Publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR#running-tool) para obter mais detalhes.

* Os grupos transferidos pela Ferramenta de transferência de conteúdo são apenas os grupos que são exigidos pelo conteúdo para atender às permissões. O processo _Extração_ copia a `/home/groups` inteira para o conjunto de migração. Para obter mais informações, consulte [Migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md). O processo _Assimilação_ copia todos os grupos referenciados nas ACLs de conteúdo migradas. Consulte [Migrando Grupos de Usuários Fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações adicionais sobre grupos usados em uma política de Grupo Fechado de Usuários (CUG).

* Durante a fase de extração, a ferramenta de transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* A *Fase de assimilação* do Autor reduz toda a implantação do Autor. Isso significa que o AEM do autor não estará disponível durante todo o processo de assimilação. Além disso, certifique-se de que nenhum pipeline do Cloud Manager seja executado enquanto você estiver executando a fase *Assimilação*.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados do índice, e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se estiver usando índices personalizados, certifique-se de configurar os índices personalizados com o nó `tika` antes de executar a Ferramenta de transferência de conteúdo. Consulte [Preparando a Nova Definição de Índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=pt-BR#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações complementares, a estrutura de conteúdo do conteúdo existente não deve mudar do momento em que a extração inicial é realizada até quando a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

* Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, desative a limpeza de versões devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão habilitada e estiver executando atualizações complementares em um conjunto de migração, você deve executar a assimilação como `wipe=true`.

* A Ferramenta de transferência de conteúdo (CTT) não oferece suporte a assimilações de mesclagem. Para consolidar o conteúdo de vários sistemas em uma única instância do Cloud Service, somente as versões de um sistema de origem podem ser migradas. Esse processo requer o uso de migrações com o parâmetro wipe=false, que pode resultar em tempos de assimilação estendidos devido à natureza incremental da operação. Se possível, consolide o conteúdo em um único sistema de origem antes de iniciar a migração para eliminar a necessidade de mesclar o conteúdo.

* Um conjunto de migração expira após um período prolongado de inatividade, após o qual seus dados não estarão mais disponíveis. Revise a [Expiração do Conjunto de Migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=pt-BR#migration-set-expiry) para obter mais detalhes.

## O que vem a seguir {#whats-next}

Depois de conhecer as diretrizes, as práticas recomendadas e as considerações importantes sobre o uso da ferramenta Transferência de conteúdo, você estará pronto para instalar e usar a ferramenta, começando com a criação de um conjunto de migração. Consulte [Introdução à ferramenta de transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).
