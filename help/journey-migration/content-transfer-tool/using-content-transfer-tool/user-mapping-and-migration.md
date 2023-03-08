---
title: Mapeamento de usuários e migração de entidade de segurança
description: Visão geral do mapeamento de usuários e da migração principal
source-git-commit: aeb8f633b45908a87f15f9feeb3723f90470be92
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 3%

---

# Mapeamento de usuários e migração de entidade de segurança {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mapeamento de usuário"
>abstract="A ferramenta Transferência de conteúdo ajuda a mover usuários e grupos do sistema AEM existente para o AEM as a Cloud Service. Os usuários existentes devem ser mapeados para as IDs IMS para evitar a duplicação na instância do autor do Cloud Service."

>[!NOTE]
>Para versões anteriores da Ferramenta de mapeamento de usuários, consulte a [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service AEM AEM, é necessário mover usuários e grupos do seu sistema existente para o as a Cloud Service. Isso é feito pela ferramenta Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor. Isso exige o uso do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) que fornece logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Devido a essa alteração, os usuários existentes precisam ser mapeados para suas IDs IMS para evitar usuários duplicados na instância do autor do Cloud Service. Como os grupos no AEM tradicional são fundamentalmente diferentes dos grupos no IMS, os grupos não são mapeados, mas os dois conjuntos de grupos devem ser reconciliados após a conclusão da migração.

## Detalhes de mapeamento e migração de usuários {#user-mapping-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão todos os usuários associados ao conteúdo que está sendo migrado. Esse mapeamento é feito automaticamente e a sua realização pode ser controlada por um botão antes de iniciar a extração. A configuração padrão do alternador pode ser substituída pelo usuário ao iniciar a extração.

* Se o sistema de origem for uma instância de autor, por padrão, a opção para fazer o mapeamento será _em_, já que esse é o processo recomendado.
* Se o sistema de origem for uma instância de publicação, por padrão, a opção para fazer o mapeamento será _desligado_, já que os usuários normalmente não são migrados ou usados em instâncias de publicação.

## Considerações importantes ao mapear e migrar usuários {#important-considerations}


### Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos são registrados:

1. Se um usuário não tiver um endereço de email no `profile/email` do seu *jcr* nó o usuário ou grupo em questão pode ser migrado, mas não será mapeado. Esse é o caso mesmo se o endereço de e-mail for usado como um nome de usuário para login.

1. Se o usuário estiver desativado, será tratado da mesma forma que se não estivesse desativado. Ele é mapeado e migrado normalmente e permanece desativado na instância da nuvem.

1. Se existir um usuário na instância do AEM Cloud Service de destino com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de AEM de origem, esse usuário ou grupo não será migrado.

1. Se um usuário for migrado sem ser mapeado primeiro pelo Mapeamento de usuários ou se o endereço de email não corresponder ao endereço usado para fazer logon no IMS, no sistema da nuvem de destino ele não poderá fazer logon usando a ID do IMS. Eles podem conseguir fazer logon usando o método tradicional do AEM, mas lembre-se de que isso normalmente não é o que se deseja ou se espera.


## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver definido, os usuários já transferidos na instância do Cloud Service serão excluídos junto com todo o repositório existente e um novo repositório será criado para assimilar conteúdo no. Isso também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado à **administradores** grupo. O usuário administrador deve ser lido na caixa **administradores** grupo para recuperar o token de acesso para CTT.
* Quando atualizações complementares de conteúdo são executadas, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos, mesmo que os usuários e grupos tenham sido alterados enquanto isso. Isso ocorre porque usuários e grupos são migrados junto com o conteúdo ao qual estão associados.
* Se a instância de destino do AEM Cloud Service tiver um usuário com um nome de usuário diferente, mas com o mesmo endereço de email de um dos usuários na instância de origem do AEM e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e o usuário do AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.
