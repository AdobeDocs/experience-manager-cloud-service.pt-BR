---
title: Gerenciando entidades após a migração
description: Saiba como configurar usuários e grupos no IMS e no AEM
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Gerenciando entidades após a migração {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Gerenciando entidades após a migração"
>abstract="Saiba como configurar usuários e grupos no IMS e no AEM"

Este documento descreve as etapas de alto nível que os clientes devem seguir para configurar seus usuários e grupos no IMS e no AEM para trabalhar com o ambiente AEM as a Cloud Service.

## Gerenciando Principais {#managing-principals}

Para o AEM as a Cloud Service, os usuários e grupos devem ser gerenciados principalmente usando o Admin Console.  Ao considerar uma migração, algumas dessas tarefas podem ser realizadas antes que a migração de conteúdo ocorra.  Essencialmente, desses principais grupos de tarefas

* Criar usuários e grupos no IMS
* Atribuir usuários a grupos no IMS
* Atribuir grupos IMS a grupos AEM (se necessário)

os dois primeiros podem ser realizados antes ou depois da migração do conteúdo.  São etapas que afetam usuários e grupos somente no IMS, possivelmente incluindo a integração com um IDP externo, como o Ative Diretory ou o LDAP.  Essas etapas são descritas em [Gerenciamento de Principais no IMS com o Admin Console](/help/journey-migration/managing-principals.md).

Depois que o conteúdo for migrado para o ambiente do AEM as a Cloud Service, a terceira etapa poderá ser realizada.

### Migrando grupos

Durante a fase de assimilação da migração, os grupos são migrados se forem necessários para atender às políticas de ACLs ou CUG no conteúdo migrado.  Consulte [Migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obter mais detalhes.

Os grupos migrados (aqueles não criados pela criação da Coleção do Assets — consulte Coleções abaixo) são configurados como grupos IMS.  Isso significa que qualquer grupo com o mesmo nome criado no IMS (via Admin Console, por exemplo) estará vinculado ao grupo no AEM, e os usuários que são membros do grupo IMS se tornarão membros do grupo no AEM também.  Para que esse link ocorra, o grupo também deve ser criado primeiro no IMS.  Use o Admin Console para criar grupos, individualmente ou em massa, na instância do AEM, conforme descrito em [Gerenciando Principais no IMS com o Admin Console](/help/journey-migration/managing-principals.md).

Use a interface de segurança do AEM para atribuir grupos IMS para grupos AEM locais.  Consulte [Criando e configurando grupos](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group).  Embora este documento seja para o AEM 6.5, ele também se aplica à adição de grupos a outros grupos no AEM as a Cloud Service.

### Usuários do IMS

Como os usuários não são migrados, eles devem ser criados no IMS para serem usados no AEM.  Há várias maneiras de fazer isso, mas é importante que os usuários criados sejam atribuídos aos grupos IMS corretos para que os usuários tenham o mesmo acesso ao conteúdo que tinham no sistema AEM anterior.  Uma das ferramentas que podem ser usadas para isso é a funcionalidade de upload em massa no Admin Console; use o carregador em massa para fazer upload de usuários juntamente com os grupos dos quais eles devem ser membros.  Antes de fazer isso, os grupos devem ser criados no IMS, conforme descrito acima.

Para saber a quais grupos cada usuário deve pertencer, use o Relatório de Usuário (consulte [Migração de Grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Este relatório lista os grupos dos quais cada usuário deve ser membro e esta lista pode ser incluída no arquivo de entrada da funcionalidade de upload em massa de Admin Console.

### Coleções

A criação de uma coleção do Assets também cria automaticamente alguns grupos para gerenciar o acesso a essa coleção.  Esses grupos são migrados se forem mencionados em coleções migradas, mas não estiverem configurados para vincular diretamente a grupos IMS; no AEM, eles permanecem como &quot;grupos locais&quot; e não podem ser gerenciados por meio do IMS.

Como esses grupos não estão no IMS, a ferramenta de upload em massa não pode ser usada para criar usuários como seus membros diretos.  Os usuários de IMS que também estão no AEM podem ser adicionados a esses grupos individualmente, mas fazer isso em massa requer uma etapa extra.  Esta é uma maneira de fazer isso:
* Crie um novo grupo ou grupos no Admin Console/IMS para acessar coleções e configure-os para AEM.
* Faça logon como membro do(s) grupo(s) para que ele(s) seja(m) criado(s) no AEM.
* Para as coleções migradas, use a interface do Assets Collections para adicionar o novo grupo como editor/proprietário/visualizador.
* Adicione (ou carregue em massa) usuários ao(s) novo(s) grupo(s) no Admin Console.
* Quando o usuário fizer logon pela primeira vez, o usuário do IMS será criado no AEM e ele deverá ter acesso ao(s) novo(s) grupo(s) e, portanto, aos grupos de coleta originais.

Observação: para atribuição de usuários em massa, as etapas acima devem ser usadas para criar os usuários no IMS; os usuários que já existem no IMS não podem ser criados novamente por meio de upload em massa.


