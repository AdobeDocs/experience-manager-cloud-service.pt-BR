---
title: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
description: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 9212042db782dc413b64d40ebde096c12d754f97
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 19%

---

# Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo {#guidelines}

## Diretrizes e práticas recomendadas {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

Uma nova versão da ferramenta de Transferência de conteúdo está disponível para integrar o processo de transferência de conteúdo ao Cloud Acceleration Manager. É altamente recomendável mudar para essa nova versão para usar todos os benefícios que ela oferece:

* Sistema de autoatendimento para extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes em paralelo
* Aprimoramento da experiência do usuário por meio de melhores estados de carregamento, medidas de proteção e tratamento de erros
* Os logs de assimilação são persistentes e sempre estão disponíveis para solução de problemas

Para começar a usar a nova versão, será necessário desinstalar as versões mais antigas da ferramenta Transferência de conteúdo. Isso é necessário porque a nova versão vem com uma grande mudança arquitetônica. Com a versão 2.x, será necessário criar novos conjuntos de migração e executar novamente a extração e a assimilação nos novos conjuntos de migração.
As versões anteriores à 2.0.0 não serão mais suportadas, e é aconselhável usar a versão mais recente.

As diretrizes e práticas recomendadas a seguir se aplicam à nova versão da ferramenta Transferência de conteúdo:

* É aconselhável executar a [Limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=pt-BR) e as [verificações de consistência do armazenamento de dados](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) no repositório de **origem** para identificar possíveis problemas e reduzir o tamanho do repositório.

* Na fase de assimilação, é recomendável executar a assimilação usando o *varrer* modo ativado em que o repositório existente (autor ou publicação) no ambiente do AEM Cloud Service de destino é completamente excluído e depois atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a ferramenta Transferência de conteúdo, verifique se há espaço em disco suficiente no subdiretório `crx-quickstart` da instância de origem do AEM. Isso ocorre porque a ferramenta Transferência de conteúdo cria uma cópia local do repositório que depois é carregada no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
  `data store size + node store size * 1.5`

   * *tamanho do armazenamento de dados*: a ferramenta Transferência de conteúdo usa 64 GB, mesmo que o armazenamento de dados real seja maior.
   * *tamanho do armazenamento do nó*: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmentos de 20 GB, o espaço livre em disco necessário seria de 94 GB.

* Um conjunto de migração precisa ser mantido durante toda a atividade de transferência de conteúdo para oferecer suporte a atualizações complementares de conteúdo. No máximo cinco conjuntos de migração por projeto no Cloud Acceleration Manager podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo. Se mais de cinco conjuntos de migração forem necessários, será necessário criar um segundo projeto no Cloud Acceleration Manager. No entanto, isso exigirá gerenciamento de projetos adicional e governança fora do produto para evitar a substituição do conteúdo no público-alvo por vários usuários.

* Evite alterar o diretório de instalação da ferramenta CTT. Por padrão, a instalação ocorre no caminho crx-quickstart/cloud-migration. Essa localização específica é utilizada internamente por outras bibliotecas da. A modificação desse caminho pode resultar em problemas de extração.

## Considerações importantes antes de usar a ferramenta Transferência de conteúdo {#important-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e o JAVA 8. Se você estiver em uma versão mais baixa do AEM, precisará atualizar seu repositório de conteúdo para AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java deve ser configurado no ambiente AEM, para que a variável `java` comando pode ser executado pelo usuário que inicia o AEM.

* A Ferramenta de transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Armazenamento de dados de arquivo, Armazenamento de dados S3, Armazenamento de dados S3 compartilhado e Armazenamento de dados do Azure Blob Store.

* Se você estiver usando um *Ambiente de sandbox*, certifique-se de que seu ambiente esteja atualizado e atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para iniciar uma assimilação, você precisa pertencer ao AEM local **administradores** grupo na instância do Cloud Service para a qual você está transferindo conteúdo. Usuários sem privilégios não poderão iniciar assimilações sem fornecer manualmente o token de migração.

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver ativada, excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também ocorre para um usuário administrador adicionado à variável **administradores** grupo. O usuário deve ser adicionado novamente à variável **administradores** grupo para recuperar o token de acesso da ferramenta Transferência de conteúdo.

* As assimilações não são compatíveis com a mesclagem de conteúdo de várias fontes na instância do Cloud Service de destino se o conteúdo das duas fontes for movido para os mesmos caminhos no destino. Para mover o conteúdo de várias fontes para uma única ocorrência de Cloud Service de destino, é necessário garantir que não haja sobreposição dos caminhos de conteúdo das fontes.

* A chave de extração é válida por 14 dias a partir do momento em que foi criada/renovada. Ele pode ser renovado a qualquer momento. Se a chave de extração tiver expirado, você não poderá executar uma extração.

* A ferramenta Transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado ao assimilar conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração é assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou instância de Publicação, ou ambos. É recomendável que, ao mover o conteúdo para uma instância de Produção, a CTT seja instalada na instância do Autor de origem para mover o conteúdo para a instância do Autor de destino e, de forma semelhante, instale a CTT na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Execução da ferramenta Transferência de conteúdo em uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) para obter mais detalhes.

* Os usuários e grupos transferidos pela ferramenta Transferência de conteúdo são apenas aqueles exigidos pelo conteúdo para atender às permissões. A variável _Extração_ o processo copia todo o `/home` no conjunto de migração e faz o Mapeamento de usuários, adicionando um campo criado a partir do endereço de email de cada usuário. Para obter mais informações, consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). A variável _Assimilação_ O processo copia todos os usuários e grupos referenciados nas ACLs de conteúdo migradas. Consulte [Migração de grupos de usuários fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações adicionais sobre grupos usados em uma política de Grupo fechado de usuários (CUG).

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* Após concluir o *Extração* fase do processo de transferência de conteúdo e antes de iniciar a *Fase de assimilação* para assimilar conteúdo no seu as a Cloud Service AEM *Estágio* ou *Produção* instâncias, será necessário registrar um tíquete de suporte para notificar o Adobe de sua intenção de executar o *Assimilação* para que o Adobe possa garantir que não ocorram interrupções durante o *Assimilação* processo. Você precisará registrar o tíquete de suporte 1 semana antes do planejado *Assimilação* data. Após enviar o tíquete de suporte, a equipe de suporte fornecerá orientação sobre as próximas etapas. Você pode registrar um tíquete de suporte com os seguintes detalhes:

   * A data exata e o horário estimado (com seu fuso horário) em que você planeja iniciar o *Assimilação* fase.
   * Tipo de ambiente (Preparo ou Produção) no qual você planeja assimilar dados.
   * ID do programa.

* A variável *Fase de assimilação* para o autor reduz a implantação do autor inteiro. Significa que o AEM do autor não está disponível durante todo o processo de ingestão. Além disso, certifique-se de que nenhum pipeline do Cloud Manager seja executado enquanto você estiver executando o *Assimilação* fase.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados do índice, e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se estiver usando índices personalizados, certifique-se de configurar os índices personalizados com `tika` antes de executar a ferramenta Transferência de conteúdo. Consulte [Preparação da nova definição de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=pt-BR#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações complementares, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é realizada até o momento em que a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

* Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, é necessário desativar a limpeza de versão devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão ativada e estiver executando atualizações complementares em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.

* Um conjunto de migração expirará após um período prolongado de inatividade, após o qual seus dados não estarão mais disponíveis. Revisão [Expiração do conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) para obter mais detalhes.

## O que vem a seguir {#whats-next}

Depois de conhecer as diretrizes, as práticas recomendadas e as considerações importantes sobre o uso da ferramenta Transferência de conteúdo, você estará pronto para instalar e usar a ferramenta, começando com a criação de um conjunto de migração. Consulte [Introdução à ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) para saber mais.
