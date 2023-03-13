---
title: Considerações importantes sobre a ferramenta Mapeamento de usuários (herdado)
description: Considerações importantes sobre a ferramenta Mapeamento de usuários (herdado)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: 69dfe7f98628ab67cc3a994c32b1530550ec6a01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Considerações importantes sobre a ferramenta Mapeamento de usuários {#important-considerations}


## Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos serão registrados:

1. Se um usuário não tiver um endereço de email no `profile/email` do seu *jcr* o usuário ou grupo em questão será migrado, mas não mapeado.  Esse será o caso mesmo se o endereço de email for usado como um nome de usuário para fazer logon.

1. Se um determinado email não for encontrado no sistema Adobe Identity Management System (IMS) para a ID da organização usada (ou se a ID do IMS não puder ser recuperada por outro motivo), o usuário ou grupo em questão será migrado, mas não mapeado.

1. Se o usuário estiver desativado no momento, será tratado da mesma forma que se não estivesse desativado. Ele será mapeado e migrado normalmente e permanecerá desativado na instância da nuvem.

1. Se existir um usuário na instância do AEM Cloud Service de destino com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de AEM de origem, o usuário ou grupo em questão não será migrado.

1. Se um usuário for migrado sem antes ser mapeado por meio do Mapeamento de usuários, ele não poderá fazer logon usando a ID IMS no sistema de nuvem de destino.  Eles podem conseguir fazer logon usando o método tradicional do AEM, mas lembre-se de que isso normalmente não é o que se deseja ou se espera.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver definido, os usuários já transferidos na instância do Cloud Service serão excluídos junto com todo o repositório existente e um novo repositório será criado para assimilar conteúdo no. Isso também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado à **administradores** grupo. O usuário administrador precisará ser adicionado novamente à **administradores** grupo para recuperar o token de acesso para CTT.

* É recomendável remover qualquer usuário existente da instância do Cloud Service AEM de destino antes de executar o CTT com o Mapeamento de usuário. Isso evita qualquer conflito entre a migração de usuários da instância do AEM de origem para a instância do AEM de destino. Conflitos ocorrerão durante a assimilação se o mesmo usuário existir na instância de AEM de origem e na instância AEM de destino.

* Quando atualizações complementares de conteúdo são executadas, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos, mesmo que os usuários e grupos tenham sido alterados enquanto isso. Isso ocorre porque usuários e grupos são migrados junto com o conteúdo ao qual estão associados.

* Se a instância de destino do AEM Cloud Service tiver um usuário com um nome de usuário diferente, mas com o mesmo endereço de email de um dos usuários na instância de origem do AEM e o Mapeamento de usuário estiver ativado, uma mensagem de erro será gravada nos logs, e o usuário do AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.

* Se dois usuários na instância de origem do AEM tiverem o mesmo endereço de email e o Mapeamento de usuário estiver ativado, uma mensagem de erro será gravada nos logs e um dos usuários AEM de origem não será transferido, pois somente um usuário com determinado endereço de email é permitido no sistema de destino.

### O que vem a seguir {#whats-next}

Depois de conhecer as considerações importantes e os casos excepcionais, você estará pronto para usar a ferramenta. Consulte [Usar a ferramenta de Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) para obter mais detalhes.
