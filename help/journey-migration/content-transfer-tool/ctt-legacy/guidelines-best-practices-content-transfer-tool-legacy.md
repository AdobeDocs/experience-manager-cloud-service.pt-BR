---
title: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo (herdado)
description: Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: eadcf71aa96298383b05e61251dfeb5f345df6b9
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 15%

---

# Diretrizes e práticas recomendadas para usar a ferramenta Transferência de conteúdo (herdado) {#guidelines}

## Diretrizes e práticas recomendadas {#best-practices}

Siga a seção abaixo para entender as diretrizes e práticas recomendadas de uso da ferramenta Transferência de conteúdo:

* Executar [Limpeza de revisão](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e [verificações de consistência do armazenamento de dados](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=pt-BR) no **origem** repositório para identificar possíveis problemas e reduzir o tamanho do repositório.

* Se a configuração da rede de entrega de conteúdo (CDN) do autor da nuvem do AEM estiver configurada para ter um incluo na lista de permissões de IPs, verifique se os IPs do ambiente de origem também são adicionados ao grupo de inclui na lista de permissões. Isso garante que o ambiente de origem e o ambiente da nuvem de AEM possam se comunicar entre si.

* Execute a assimilação usando o *varrer* modo ativado em que o repositório existente (autor ou publicação) no ambiente do AEM Cloud Service de destino será excluído e depois atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a ferramenta Transferência de conteúdo, verifique se há espaço em disco suficiente no subdiretório `crx-quickstart` da instância de origem do AEM. Isso ocorre porque a ferramenta Transferência de conteúdo cria uma cópia local do repositório que depois é carregada no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
   `data store size + node store size * 1.5`

   * *tamanho do armazenamento de dados*: a ferramenta Transferência de conteúdo usa 64 GB, mesmo que o armazenamento de dados real seja maior.
   * *tamanho do armazenamento do nó*: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmentos de 20 GB, o espaço livre em disco necessário seria de 94 GB.

* Um conjunto de migração deve ser mantido em toda a atividade de transferência de conteúdo para oferecer suporte a atualizações complementares de conteúdo. Como é possível criar e manter no máximo dez conjuntos de migração por vez durante a atividade de transferência de conteúdo, recomenda-se dividir o repositório de conteúdo adequadamente. Isso garante que você não fique sem conjuntos de migração.

## Considerações importantes antes de usar a ferramenta Transferência de conteúdo {#important-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar a ferramenta Transferência de conteúdo:

* O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é AEM 6.3 + e Java™ 8. Se você estiver em uma versão mais baixa do AEM, precisará atualizar seu repositório de conteúdo para AEM 6.5 para usar a ferramenta Transferência de conteúdo.

* O Java™ deve ser configurado no ambiente AEM, para que a variável `java` comando pode ser executado pelo usuário que inicia o AEM.

* Desinstale versões anteriores da ferramenta Transferência de conteúdo ao instalar a versão 1.3.0, pois houve uma grande mudança de arquitetura na ferramenta. Com a versão 1.3.0, você também deve criar conjuntos de migração e executar novamente a extração e a assimilação nos novos conjuntos de migração.

* A Ferramenta de transferência de conteúdo pode ser usada com os seguintes tipos de armazenamento de dados: Armazenamento de dados de arquivo, Armazenamento de dados S3, Armazenamento de dados S3 compartilhado e Armazenamento de dados do Azure Blob Store.

* Se você estiver usando um *Ambiente de sandbox*, certifique-se de que seu ambiente esteja atualizado e atualizado para a versão mais recente. Se você estiver usando um *Ambiente de produção*, ele será atualizado automaticamente.

* Para usar a ferramenta Transferência de conteúdo, você precisa ser um usuário administrador na instância de origem e pertencer ao AEM local **administradores** grupo na instância do Cloud Service para a qual você está transferindo conteúdo. Usuários sem privilégios não podem recuperar o token de acesso para usar a ferramenta Transferência de conteúdo.

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver ativada, excluirá todo o repositório existente e criará um repositório para assimilar conteúdo. Esse workflow significa que redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Esse resultado é verdadeiro mesmo para um usuário administrador que é adicionado ao **do administrador** grupo. O usuário deve ser lido no campo **do administrador** para recuperar o token de acesso da ferramenta Transferência de conteúdo.

* A ferramenta Transferência de conteúdo não suporta a mesclagem de conteúdo de várias fontes na instância do Cloud Service de destino se o conteúdo das duas fontes for movido para os mesmos caminhos no destino. Para mover o conteúdo de várias fontes para uma única ocorrência de Cloud Service de destino, é necessário garantir que não haja sobreposição dos caminhos de conteúdo das fontes.

* O token de acesso pode expirar periodicamente após um período específico ou após a atualização do ambiente Cloud Service. Se o token de acesso tiver expirado, não será possível se conectar à instância do Cloud Service. Nesse caso, você precisa recuperar o novo token de acesso. O ícone de status associado a um conjunto de migração existente muda para uma nuvem vermelha e exibe uma mensagem quando você passa o mouse sobre ela.

* A ferramenta Transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado ao assimilar conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração é assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou Instância de publicação, ou em ambas. Ao mover o conteúdo para uma instância de Produção, instale a CTT na instância do Autor de origem para mover o conteúdo para a instância do Autor de destino. E, da mesma forma, instale a CTT na instância de publicação de origem para mover o conteúdo para a instância de publicação de destino. Consulte [Execução da ferramenta Transferência de conteúdo em uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) para obter mais detalhes.

* Os usuários e grupos transferidos pela ferramenta Transferência de conteúdo são apenas aqueles exigidos pelo conteúdo para atender às permissões. A variável *Extração* o processo copia todo o `/home` no conjunto de migração e no *Assimilação* O processo copia todos os usuários e grupos referenciados nas ACLs de conteúdo migradas. Para mapear automaticamente os usuários e grupos existentes para suas IDs de IMS, consulte [Utilização da ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* Durante a fase de extração, a ferramenta Transferência de conteúdo é executada em uma instância de origem do AEM ativa.

* Após concluir o *Extração* fase do processo de transferência de conteúdo e antes de iniciar a *Fase de assimilação* para assimilar conteúdo no seu as a Cloud Service AEM *Estágio* ou *Produção* registrará um tíquete de suporte. Notifique o Adobe da sua intenção de executar o *Assimilação* para que o Adobe possa garantir que não ocorram interrupções durante o *Assimilação* processo. Registre o tíquete de suporte uma semana antes do planejado *Assimilação* data. Depois que você enviar o tíquete de suporte, a equipe de suporte fornecerá orientação sobre as próximas etapas. Registre um tíquete de suporte com os seguintes detalhes:

   * A data exata e o horário estimado (com seu fuso horário) em que você planeja iniciar o *Assimilação* fase.
   * Tipo de ambiente (Preparo ou Produção) no qual você planeja assimilar dados.
   * ID do programa.

* A variável *Fase de assimilação* para o autor reduz a implantação do autor inteiro. Esse processo significa que o AEM do autor não está disponível durante todo o processo de ingestão. Certifique-se também de que nenhum pipeline do Cloud Manager seja executado enquanto você estiver executando o *Assimilação* fase.

* Ao usar `Amazon S3` ou `Azure` como o armazenamento de dados no sistema AEM de origem, o armazenamento de dados deve ser configurado para que os blobs armazenados não possam ser excluídos (coleta de lixo). Isso garante a integridade dos dados do índice, e a falha na configuração dessa maneira pode resultar em extrações com falha devido à falta de integridade desses dados de índice.

* Se estiver usando índices personalizados, certifique-se de configurar os índices personalizados com `tika` antes de executar a ferramenta Transferência de conteúdo. Consulte [Preparação da nova definição de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obter mais detalhes.

* Se você pretende fazer atualizações complementares, verifique se a estrutura de conteúdo do conteúdo existente não é alterada desde o momento em que a extração inicial é realizada até quando a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

* Se você pretende incluir versões como parte de um conjunto de migração e estiver executando atualizações com `wipe=false`, é necessário desativar a limpeza de versão devido a uma limitação atual na Ferramenta de transferência de conteúdo. Se preferir manter a limpeza de versão ativada e estiver executando atualizações complementares em um conjunto de migração, você deverá executar a assimilação como `wipe=true`.

## O que vem a seguir {#whats-next}

Depois de conhecer as diretrizes, as práticas recomendadas e as considerações importantes sobre o uso da ferramenta Transferência de conteúdo, você estará pronto para instalar e usar a ferramenta, começando com a criação de um conjunto de migração. Consulte [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR) para saber mais.
