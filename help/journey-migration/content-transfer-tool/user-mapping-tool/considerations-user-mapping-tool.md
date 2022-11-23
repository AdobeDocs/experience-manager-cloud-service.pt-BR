---
title: Considerações importantes para a ferramenta Mapeamento de usuários
description: Considerações importantes para a ferramenta Mapeamento de usuários
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 18047b129a9a347cbf6edcdc07dc6570fca26d3b
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Considerações importantes para a ferramenta Mapeamento de usuários {#important-considerations}


## Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos serão registrados:

1. Se um usuário não tiver endereço de email na `profile/email` do seu *jcr* nó em que o usuário ou grupo em questão será migrado, mas não mapeado.  Esse será o caso mesmo se o endereço de email for usado como nome de usuário para fazer logon.

1. Se um determinado email não for encontrado no sistema Adobe Identity Management System (IMS) para a ID da organização usada (ou se a ID IMS não puder ser recuperada por outro motivo), o usuário ou grupo em questão será migrado, mas não mapeado.

1. Se o usuário estiver desabilitado no momento, ele será tratado como se não estivesse desabilitado. Ele será mapeado e migrado normalmente e permanecerá desativado na instância da nuvem.

1. Se um usuário existir na instância de destino do AEM Cloud Service com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de origem do AEM, o usuário ou grupo em questão não será migrado.

1. Se um usuário for migrado sem ser mapeado primeiro por meio do Mapeamento de usuário, no sistema da nuvem de destino, ele não poderá fazer logon usando sua ID IMS.  Eles podem fazer logon usando o método AEM tradicional, mas lembrem-se de que isso não é normalmente o que é desejado ou esperado.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Limpar o conteúdo existente na instância do Cloud antes da assimilação** for definido, os usuários já transferidos na instância do Cloud Service serão excluídos junto com todo o repositório existente e um novo repositório será criado para assimilar conteúdo. Isso também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado ao **administradores** grupo. O usuário administrador precisará ser adicionado novamente ao **administradores** para recuperar o token de acesso para CTT.

* Recomenda-se remover qualquer usuário existente da instância do Cloud Service de destino AEM antes de executar a CTT com o Mapeamento de usuários. Isso é para evitar qualquer conflito entre a migração de usuários da instância de AEM de origem para a instância de AEM de destino. Os conflitos ocorrerão durante a assimilação se o mesmo usuário existir na instância de AEM de origem e na instância de AEM de destino.

* Quando os upups de conteúdo são executados, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos, mesmo se os usuários e grupos tiverem sido alterados enquanto isso. Isso ocorre porque os usuários e grupos são migrados junto com o conteúdo ao qual estão associados.

* Se a instância do AEM Cloud Service de destino tiver um usuário com um nome de usuário diferente, mas o mesmo endereço de email de um dos usuários na instância de AEM de origem e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e o usuário do AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.

* Se dois usuários na instância de AEM de origem tiverem o mesmo endereço de email e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e um dos usuários de AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.

### O que vem a seguir {#whats-next}

Depois de ter aprendido as considerações importantes e os casos excepcionais, você estará pronto para usar a ferramenta. Consulte [Usar a ferramenta Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) para obter mais detalhes.
