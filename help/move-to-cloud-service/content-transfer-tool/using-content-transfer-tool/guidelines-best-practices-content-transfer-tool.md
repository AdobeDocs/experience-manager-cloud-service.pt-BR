---
title: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
description: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
source-git-commit: b421cc5e6078112adecb856d723a1bae628d8ec7
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 25%

---


# Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo {#guidelines}

## Diretrizes e práticas recomendadas {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Diretrizes e práticas recomendadas"
>abstract="Analise as diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo, incluindo tarefas de limpeza de revisão, considerações de espaço em disco e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Considerações importantes sobre o uso da ferramenta Transferência de conteúdo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerações importantes sobre o uso da ferramenta Mapeamento de usuários"

Siga a seção abaixo para entender as diretrizes e práticas recomendadas de uso da ferramenta Transferência de conteúdo:

* É aconselhável executar a [Limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e as [verificações de consistência do armazenamento de dados](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) no repositório de **origem** para identificar possíveis problemas e reduzir o tamanho do repositório.

* Se a Rede de entrega de conteúdo (CDN) do Autor da AEM Cloud estiver configurada para ter uma lista de permissões de IPs, será necessário garantir que os IPs do ambiente de origem também sejam adicionados à lista de permissões para que o ambiente de origem e o ambiente da AEM Cloud possam se comunicar.

* Na fase de assimilação, é recomendável executar a assimilação usando o modo de *limpeza* ativado, no qual o repositório existente (autor ou publicação) no ambiente de serviço do AEM Cloud Service será completamente excluído e depois atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a ferramenta Transferência de conteúdo, verifique se há espaço em disco suficiente no subdiretório `crx-quickstart` da instância de origem do AEM. Isso ocorre porque a ferramenta Transferência de conteúdo cria uma cópia local do repositório que depois é carregada no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
   `data store size + node store size * 1.5`

   * *tamanho do armazenamento de dados*: a ferramenta Transferência de conteúdo usa 64 GB, mesmo que o armazenamento de dados real seja maior.
   * *tamanho do armazenamento do nó*: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmentos de 20 GB, o espaço livre em disco necessário seria de 94 GB.

* Um conjunto de migração precisa ser mantido durante toda a atividade de transferência de conteúdo para oferecer suporte a atualizações complementares de conteúdo. Como é possível criar e manter no máximo dez conjuntos de migração por vez durante a atividade de transferência de conteúdo, é recomendável dividir o repositório de conteúdo adequadamente para garantir que você não fique sem conjuntos de migração.

## Considerações importantes antes de usar a ferramenta Transferência de conteúdo {#important-considerations}

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

* Após concluir a fase *Extração* do processo de transferência de conteúdo e antes de iniciar a *Fase de assimilação* para assimilar conteúdo em suas instâncias AEM as a Cloud Service *Stage* ou *Production*, você precisará registrar um tíquete de suporte para notificar o Adobe de sua intenção de executar *Assimilação&lt;a9 para que o Adobe possa garantir que nenhuma interrupção ocorra durante o processo* Assimilação *.* Você precisará registrar o tíquete de suporte uma semana antes da data planejada de *Assimilação*. Depois de enviar o tíquete de suporte, a equipe de suporte fornecerá orientação sobre as próximas etapas. Você pode registrar um tíquete de suporte com os seguintes detalhes:

   * Data exata e hora estimada (com seu fuso horário) quando você planeja iniciar a fase *Assimilação*.
   * Tipo de ambiente (Preparo ou Produção) no qual você planeja assimilar dados.
   * ID do programa.

* A *Fase de assimilação* do autor diminui a implantação do autor inteiro. Isso significa que o AEM do autor não estará disponível durante todo o processo de ingestão. Certifique-se também de que nenhum pipeline do Cloud Manager seja executado enquanto você está executando a fase *Assimilação*.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema de AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados de índice e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se você estiver usando índices personalizados, certifique-se de configurar os índices personalizados com o nó `tika` antes de executar a ferramenta Transferência de conteúdo. Consulte [Preparando a Nova Definição de Índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações adicionais, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

* Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações adicionais com `wipe=false`, você deve desativar a limpeza de versão devido a uma limitação atual na ferramenta Transferência de conteúdo. Se você preferir manter a limpeza de versão ativada e estiver executando os upups em um conjunto de migração, você deve executar a assimilação como `wipe=true`.

## O que vem a seguir {#whats-next}

Depois de conhecer as diretrizes, as práticas recomendadas e as considerações importantes para o uso da ferramenta Transferência de conteúdo, você estará pronto para instalar e usar a ferramenta, começando pela criação de um conjunto de migração. Consulte [Introdução à transferência de conteúdo para](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para saber mais.
