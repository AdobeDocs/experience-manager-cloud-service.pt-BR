---
title: Gerenciamento de principais após a migração
description: Saiba como configurar usuários e grupos no IMS e no AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 4%

---

# Gerenciamento de principais após a migração {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Gerenciamento de principais após a migração"
>abstract="Saiba como configurar usuários e grupos no IMS e no AEM"

Este documento descreve as etapas de alto nível que os clientes devem seguir para configurar seus usuários e grupos no IMS e no AEM para trabalhar com o ambiente AEM as a Cloud Service.

Para obter informações sobre a migração de grupos e o Relatório de migração de entidade de segurança disponível com cada assimilação, consulte [Migração de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Para obter um guia sobre como usar grupos em massa e arquivos de usuário no Admin Console, consulte [Upload em massa de Principais para IMS após usar CTT](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md).

## Gerenciamento de principais {#managing-principals}

Para o AEM as a Cloud Service, os usuários e grupos devem ser gerenciados principalmente usando o Admin Console.  Ao considerar uma migração, algumas dessas tarefas podem ser realizadas antes que a migração de conteúdo ocorra.  Essencialmente, desses principais grupos de tarefas

* Criar usuários e grupos no IMS
* Atribuir usuários a grupos no IMS
* Atribuir grupos IMS a grupos AEM (se necessário)

Os dois primeiros podem ser realizados antes ou depois da migração do conteúdo.  São etapas que afetam usuários e grupos somente no IMS, possivelmente incluindo a integração com um IDP externo, como o Ative Diretory ou o LDAP.  Essas etapas são descritas em [Gerenciamento de Principais no IMS com a Admin Console](/help/journey-migration/managing-principals.md).

Depois que o conteúdo for migrado para o ambiente do AEM as a Cloud Service, a terceira etapa poderá ser realizada.

### Migrando grupos

Durante a fase de assimilação da migração, os grupos são migrados se forem necessários para atender às políticas de ACLs ou CUG no conteúdo migrado.  Consulte [Migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obter mais detalhes.

Os grupos migrados (aqueles não criados pela Coleção do Assets ou pela criação de Pasta privada — consulte Coleções e pastas privadas abaixo) são configurados como grupos IMS.  Isso significa que qualquer grupo com o mesmo nome criado no IMS (por meio do Admin Console, por exemplo) será vinculado ao grupo no AEM, e os usuários que forem membros do grupo IMS também se tornarão membros do grupo no AEM.  Para que esse link ocorra, o grupo também deve ser criado primeiro no IMS.  Use o Admin Console para criar grupos, individualmente ou em massa, na instância do AEM, conforme descrito em [Gerenciando Principais no IMS com o Admin Console](/help/journey-migration/managing-principals.md).

Use a interface de segurança do AEM para atribuir grupos IMS a grupos AEM locais. Para fazer isso, vá para a página Ferramentas no AEM, clique em Segurança e escolha Grupos.

### Usuários do IMS

Como os usuários não são migrados, eles devem ser criados no IMS para serem usados no AEM.  Há várias maneiras de fazer isso, mas é importante que os usuários criados sejam atribuídos aos grupos IMS corretos para que eles tenham o mesmo acesso ao conteúdo que tinham no sistema AEM anterior.  Uma das ferramentas que podem ser usadas para isso é a funcionalidade de upload em massa na Admin Console. Use o carregador em massa para fazer upload de usuários junto com grupos dos quais eles devem ser membros.  Antes de fazer isso, os grupos devem ser criados no IMS, conforme descrito acima.

Para saber a quais grupos cada usuário deve pertencer, use o Relatório de Usuário (consulte [Migração de Grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Este relatório lista os grupos dos quais cada usuário deve ser membro e esta lista normalmente será incluída no arquivo de entrada do Usuário em massa para uso com a funcionalidade de upload em massa do Admin Console.

### Coleções e pastas privadas

A criação de uma coleção ou pasta privada do Assets também cria automaticamente alguns grupos para gerenciar o acesso a esse conteúdo do Assets.  Esses grupos são migrados se forem mencionados no conteúdo migrado, mas não estão configurados para vincular diretamente aos grupos IMS. No AEM, eles permanecem como &quot;grupos locais&quot; e não podem ser gerenciados por meio do IMS.

Como esses grupos não estão no IMS, a ferramenta de upload em massa não pode ser usada para criar usuários como seus membros diretos.  Os usuários do IMS que também estão no AEM podem ser adicionados a esses grupos individualmente, mas fazer isso em massa requer uma etapa extra.  Esta é uma maneira de fazer isso:

* Crie um novo grupo ou grupos no Admin Console/IMS para acessar coleções/pastas privadas e configure-os para o AEM.
* Faça logon como membro dos grupos para que eles sejam criados na AEM.
* Para as coleções ou pastas privadas migradas, use a interface do usuário do Assets para adicionar o novo grupo como editor/proprietário/visualizador.
* Adicionar usuários (ou fazer upload em massa) ao(s) novo(s) grupo(s) no Admin Console.
* Quando o usuário fizer logon pela primeira vez, o usuário do IMS será criado no AEM e ele deverá ter acesso ao(s) novo(s) grupo(s) e, portanto, à coleção original ou aos grupos de pastas privadas.

Observação: para atribuição de usuários em massa, as etapas acima devem ser usadas para criar os usuários no IMS; os usuários que já existem no IMS não podem ser criados novamente por meio de carregamento em massa, embora o editor de itens em massa possa ser usado para fazer esses tipos de alterações (Consulte [Carregamento de usuário em massa do Admin Console](https://helpx.adobe.com/br/enterprise/using/bulk-upload-users.html) em **Editar detalhes do usuário**).
