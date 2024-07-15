---
title: Considerações importantes sobre a ferramenta Mapeamento de usuários (herdado)
description: Considerações importantes sobre a ferramenta Mapeamento de usuários (herdado)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Considerações importantes sobre a ferramenta Mapeamento de usuários (herdado) {#important-considerations}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta da ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Mapeamento de Usuário e Migração de Entidade de Segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos são registrados:

1. Se um usuário não tiver um endereço de email no campo `profile/email` de seu nó *jcr*, o usuário ou grupo em questão será migrado, mas não será mapeado. Essa regra ocorre mesmo se o endereço de email for usado como um nome de usuário para fazer logon.

1. Se um email não for encontrado no sistema Adobe Identity Management System (IMS) para a ID de organização usada (ou se a ID do IMS não puder ser recuperada), o usuário ou grupo será migrado, mas não será mapeado.

1. Se o usuário estiver desativado, será tratado da mesma forma que se não estivesse desativado. Ele é mapeado e migrado normalmente e permanece desativado na instância da nuvem.

1. Se existir um usuário na instância do AEM Cloud Service de destino com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de AEM de origem, esse usuário ou grupo não será migrado.

1. Se um usuário for migrado sem ser mapeado primeiro por meio do Mapeamento de usuários, ele não poderá fazer logon usando a ID IMS no sistema de nuvem de destino. Talvez seja possível fazer logon usando o método tradicional do AEM, mas esse fluxo de trabalho normalmente não é o desejado ou esperado.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes de assimilar** estiver definida, os usuários já transferidos na instância do Cloud Service serão excluídos. O repositório existente inteiro também é excluído e um novo repositório é criado no qual o conteúdo é assimilado. Esta ação também redefine todas as configurações, incluindo permissões na instância Cloud Service de destino, e é verdadeira para um usuário administrador adicionado ao grupo **administradores**. O usuário administrador deve ser lido no grupo **administradores** para recuperar o token de acesso para CTT.

* O Adobe recomenda remover qualquer usuário existente da instância do AEM do Cloud Service de destino antes de executar o CTT com o Mapeamento de usuário. Essa ação é necessária para evitar qualquer conflito entre a migração de usuários da instância do AEM de origem para a instância do AEM de destino. Conflitos podem ocorrer durante a assimilação se o mesmo usuário existir na instância de AEM de origem e na instância AEM de destino.

* Quando atualizações complementares de conteúdo são executadas, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos. Essa regra é verdadeira mesmo se os usuários e grupos tiverem sido alterados enquanto isso. Isso ocorre porque usuários e grupos são migrados junto com o conteúdo ao qual estão associados.

* Se o AEM Cloud Service tiver um usuário com um nome de usuário diferente, mas com o mesmo endereço de email de um usuário na instância AEM de origem, e o Mapeamento de usuário estiver ativado, uma mensagem de erro será registrada. Além disso, o usuário AEM de origem não é transferido, pois somente um usuário com determinado endereço de email é permitido no sistema de destino.

* Se dois usuários na instância de origem do AEM tiverem o mesmo endereço de email e o Mapeamento de usuário estiver ativado, uma mensagem de erro será registrada. Além disso, um dos usuários do AEM de origem é transferido porque somente um usuário com determinado endereço de email é permitido no sistema de destino.

### O que vem a seguir {#whats-next}

Depois de conhecer as considerações importantes e os casos excepcionais, você estará pronto para usar a ferramenta. Consulte [Usar a ferramenta de Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) para obter mais detalhes.
