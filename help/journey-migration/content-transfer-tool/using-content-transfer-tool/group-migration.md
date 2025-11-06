---
title: Migração de grupo
description: Visão geral da migração de grupo no AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 3%

---


# Migração de grupo {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Migração de grupo"
>abstract="A ferramenta de transferência de conteúdo ajuda a copiar grupos do seu sistema existente do Adobe Experience Manager (AEM) para o AEM as a Cloud Service."

>[!NOTE]
>Para ver as versões anteriores da Ferramenta de Mapeamento de Usuários, consulte a [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Os usuários não são migrados"
>abstract="A ferramenta de transferência de conteúdo não migra mais os usuários. Os usuários devem ser gerenciados pelo Admin Console."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentação do Admin Console do AEM"
>additional-url="https://adminconsole.adobe.com/" text="Admin Console do AEM"

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, os grupos devem ser migrados dos sistemas AEM existentes para o AEM as a Cloud Service. Essa tarefa é realizada pela ferramenta Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor. Este processo requer o uso do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece logon único em todos os aplicativos de nuvem da Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=pt-BR#identity-management). Devido a essa alteração, os usuários são criados automaticamente no AEM quando fazem logon pela primeira vez por meio do IMS.  Assim, a CTT não migra os usuários para o sistema de nuvem.  Os usuários do IMS devem ser colocados em grupos do IMS, que podem ser grupos migrados ou novos grupos colocados nos grupos do AEM que receberam permissão para acessar o conteúdo do AEM que está sendo migrado.  Dessa forma, os usuários no sistema de nuvem terão o mesmo acesso que tinham em seu sistema do AEM de origem.

## Detalhes da migração de grupo {#group-migration-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão todos os grupos associados ao conteúdo que está sendo migrado para o sistema de nuvem. A ferramenta Transferência de conteúdo faz isso copiando todos os grupos do sistema AEM de origem durante o processo de extração. A assimilação de CAM seleciona e migra apenas determinados grupos:

* Se um grupo estiver em uma política de ACL ou CUG do conteúdo migrado, esse grupo será migrado, com algumas exceções listadas abaixo.
* Há vários grupos que estão integrados e já estão presentes no sistema de nuvem de destino; eles nunca são migrados.
   * Alguns grupos internos podem incluir grupos de membros _não_ incorporados; todos os grupos de membros (membros diretos ou membros de membros, etc.) referenciados em uma política ACL ou CUG de conteúdo migrado serão migrados, para garantir que os usuários que são membros desses grupos (direta ou indiretamente) mantenham seu acesso ao conteúdo migrado.
* Outros grupos, como aqueles não encontrados em uma política de ACL ou CUG, aqueles que já estão no sistema de destino e aqueles com dados restritos por exclusividade que já estão no sistema de destino, não serão migrados.

Observe que o caminho registrado/relatado para um grupo é somente o primeiro caminho que acionou a migração desse grupo, e esse grupo também pode estar em outros caminhos de conteúdo.

A maioria dos grupos migrados é configurada para ser gerenciada pelo IMS.  Isso significa que um grupo no IMS com o mesmo nome será vinculado ao grupo no AEM e qualquer usuário IMS no grupo IMS se tornará usuário do AEM e membro do grupo no AEM.  Isso permite que esses usuários tenham acesso ao conteúdo de acordo com as políticas de ACLs ou CUGs do grupo.

Observe que os grupos migrados não são mais considerados &quot;grupos locais&quot; do AEM; eles são grupos prontos para IMS no AEM, embora ainda não existam no IMS.  Eles devem ser recriados separadamente no IMS para que possam ser sincronizados entre o AEM e o IMS.  Os grupos podem ser criados no IMS por meio do Admin Console, entre outros métodos, individualmente ou em massa.  Consulte [Gerenciar grupos de usuários](https://helpx.adobe.com/br/enterprise/using/user-groups.html) para obter detalhes sobre como criar grupos individualmente ou em massa na Admin Console.

A exceção para essa configuração IMS é com grupos criados por Coleções Assets e Pastas privadas. Quando uma coleção ou uma pasta privada é criada no AEM, os grupos são criados para acessar esse conteúdo; esses grupos são migrados para o sistema de nuvem, mas não são configurados para serem gerenciados pelo IMS.  Para adicionar usuários do IMS a esses grupos, eles devem ser adicionados na página Propriedades do grupo na interface do usuário do Assets, individual ou coletivamente, como parte de outro grupo IMS.


## Recusar Migração de Grupo {#group-migration-option}

A CTT versão 3.0.20 e posterior inclui uma opção para desativar a migração de grupos.  Isso é configurado no console OSGI da seguinte maneira:

* Abra a Configuração OSGI `(http://<server>/system/console/configMgr)`
* Clique na configuração chamada **Configuração do serviço de extração da ferramenta de transferência de conteúdo**
* Desmarque **Incluir grupos na migração** para desabilitar migrações de grupos
* Clique em **Salvar** para garantir que a configuração seja salva e esteja ativa no servidor

Com essa configuração desativada, os grupos não serão migrados e não haverá nenhum relatório de migração principal nem relatório do usuário (veja abaixo).

## Relatório de migração principal e relatório do usuário {#principal-migration-report}

Quando os grupos são incluídos durante a migração (o padrão), um Relatório de migração principal é salvo, descrevendo o que acontece com cada grupo durante a migração.  Para baixar este relatório após uma assimilação bem-sucedida:

* No CAM, vá para Transferência de conteúdo e selecione Trabalhos de assimilação.
* Clique nas reticências (...) na linha da Assimilação em questão e escolha &quot;Exibir resumo principal&quot;.
* Na caixa de diálogo exibida, selecione &quot;Relatório de migração principal&quot; na lista suspensa em &quot;Baixar um arquivo...&quot; e clique no botão Download.
* Salve o arquivo CSV resultante.

Algumas das informações registradas por grupo são:

* Se migrado, o caminho para a primeira ACL ou CUG que fez com que o grupo fosse migrado.
* Se o grupo foi migrado anteriormente; se a assimilação atual foi uma assimilação não limpa, alguns grupos podem ter sido migrados durante uma assimilação anterior.
* Se o grupo é um grupo integrado; esses grupos não são migrados porque estão sempre no ambiente do AEMaaCS de destino.
* Se o grupo não fizesse parte de uma ACL ou de um CUG no conteúdo migrado, ele não teria sido migrado.
* Se o grupo era local, como um grupo criado por uma coleção da Assets, talvez tenha sido migrado e, nesse caso, a palavra &quot;local&quot; é adicionada ao relatório desse grupo.

Durante a migração, os usuários não são migrados, mas as relações entre usuários e grupos no sistema de origem seriam perdidas, a menos que fossem capturados de alguma forma. O processo de assimilação captura algumas dessas informações no formato de texto em um relatório do usuário, que está no final do relatório de migração principal.

### Relatório do usuário {#user-report}

Na seção Relatório do usuário, os usuários são relatados (um por linha) juntamente com seu endereço de email e uma lista de grupos habilitados para IMS que foram migrados durante essa assimilação.  Os grupos que não foram migrados, que foram migrados durante uma assimilação anterior ou que são grupos locais não são incluídos na lista.   Se um usuário não estiver em nenhum grupo habilitado para IMS migrado e não tiver notas extras indicando que é um caso especial (consulte **Notas** abaixo), ele _não_ aparecerá no relatório. Os grupos relatados junto com cada usuário são aqueles dos quais o usuário é membro, direta ou indiretamente, no sistema de origem; como os grupos no sistema de origem podem ser aninhados enquanto no sistema de destino não estão, essa lista de grupos oferece suporte à nova estrutura de grupos nivelados no IMS.

No caso de uma assimilação sem limpeza e, em seguida, uma assimilação sem limpeza, os grupos em uma lista do usuário da assimilação sem limpeza serão apenas aqueles grupos migrados durante a fase de não limpeza.

#### Notas {#user-report-notes}

Além dos grupos de cada usuário, há um campo no Relatório de usuário em que podem ser fornecidas notas sobre o usuário (e uma descrição detalhada do significado da nota também está no relatório) para fins de informação.  As possíveis observações são:

* **Nota-A** Os usuários referenciados diretamente em uma ACL terão *Nota-A* em sua seção de notas, pois este não é um caso de uso recomendado ou prática recomendada.
* **Nota-B** Os usuários que são membros diretos de um grupo interno terão *Nota-B* em sua seção de notas, pois este também não é um caso de uso recomendado ou uma prática recomendada.
* **Nota-C** Os usuários que são diretos de membros indiretos de um grupo local migrado (como um grupo criado por uma coleção do Assets) terão *Nota-C* em sua seção de notas, pois os grupos locais não estão configurados para serem gerenciados pelo IMS.

Esses casos podem ocorrer simultaneamente e ao mesmo tempo que os casos anteriores.  _Para obter informações adicionais sobre a quais grupos cada Nota se refere para cada usuário, verifique o log de assimilação; ele relata essas informações para cada usuário._

O Relatório de usuários é adicionado ao final do (e, portanto, faz parte do) Relatório de migração principal (consulte [Resumo final e relatório](#final-summary-and-report) abaixo) para fornecer aos clientes uma compreensão mais completa dos grupos e usuários e de suas relações.

## Carregar arquivos em massa {#bulk-upload-files}

Como os grupos são migrados somente para o AEM as a Cloud Service, eles ainda devem ser adicionados ao IMS para funcionarem corretamente com o AEM na nuvem. Além disso, os usuários não são migrados e, portanto, também precisam ser adicionados ao IMS. A ferramenta de migração CTT/CAM não executa essa etapa, mas o processo de assimilação cria dois arquivos de upload em massa, um para grupos e outro para usuários. Esses arquivos podem ser editados e usados, juntamente com a funcionalidade de upload em massa do Admin Console, para criar grupos e usuários do IMS com base nos grupos e usuários do AEM.

Consulte [Grupo em massa e carregamento de usuário para IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md) para obter detalhes sobre como usar arquivos de carregamento em massa para criar usuários e grupos usando o Admin Console.

Consulte também [Gerenciar usuários](https://helpx.adobe.com/ca/enterprise/using/users.html) para obter detalhes adicionais sobre como gerenciar usuários do AEM as a Cloud Service.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes de assimilar** estiver definida, os grupos transferidos anteriormente para a instância do Cloud Service serão excluídos junto com todo o repositório existente; um novo repositório será criado no qual o conteúdo será assimilado. Esse processo também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para qualquer usuário adicionado ao grupo **administradores**. O usuário administrador deve ser adicionado novamente ao grupo **administradores** para recuperar o token de acesso para assimilação de CTT/CAM.
* Quando assimilações que não são de limpeza são executadas (**Limpar conteúdo existente** não está definido), se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os grupos associados a esse conteúdo também não serão transferidos. Essa regra é verdadeira mesmo se os grupos tiverem sido alterados no sistema de origem. Isso ocorre porque os grupos só são migrados junto com o conteúdo ao qual estão associados. Por causa disso, nesse caso, os grupos que são membros de um grupo no sistema de origem não serão migrados, a menos que façam parte de um grupo diferente que está sendo migrado ou na ACL de conteúdo diferente que está sendo migrado. Para migrar esses grupos posteriormente, considere usar pacotes, excluir grupos do público-alvo e migrar novamente o conteúdo relevante ou migrar novamente usando uma assimilação de limpeza.
* Durante uma assimilação sem limpeza, se um grupo existir com qualquer um dos mesmos dados com restrição de exclusividade (rep:principalName, rep:authorizableId, jcr:uuid ou rep:externalId) na instância do AEM de origem e na instância do AEM Cloud Service de destino, o grupo em questão será _não_ migrado e o grupo existente anteriormente no sistema de nuvem permanecerá inalterado. Isso é registrado no Relatório de migração principal.
* Consulte [Migrando Grupos de Usuários Fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações adicionais sobre grupos usados em uma política de Grupo Fechado de Usuários (CUG).

## Resumo final e relatório

Depois que a extração e a assimilação forem concluídas com êxito, um relatório será gerado mostrando os detalhes da migração do grupo. Consulte [Como validar a migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration) para obter detalhes.
