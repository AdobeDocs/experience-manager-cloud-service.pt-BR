---
title: Alterações na sincronização de grupos de usuários e perfis de produtos
description: Saiba mais sobre as alterações na sincronização do grupo de usuários e do perfil de produto que chegam ao AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: c3e3905d3896d79149a386241d798f78631184b3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Alterações na sincronização de grupos de usuários e perfis de produtos {#changes-in-user-group-and-product-profile-synchronization}

Sempre que um usuário faz logon no AEM as a Cloud Service ou um token de acesso é usado, os grupos de usuários, perfis de produtos e serviços de perfil de produtos do Adobe Admin Console são sincronizados no repositório do AEM como grupos.

Em 28 de janeiro, para reduzir a desordem da interface do usuário e otimizar o desempenho, haverá algumas alterações no comportamento de sincronização, resultando no surgimento de menos grupos no AEM. Duas categorias de grupos AEM serão removidas:

1. Grupos AEM com Sufixo `GROUP_NAME_SUFFIX`. Esses grupos não aparecem na Adobe Developer Console, mas aparecem na tela Gerenciamento de grupos AEM, como mostrado abaixo. No caso improvável de seu aplicativo AEM fazer referência a esses grupos, use grupos de usuários do Adobe Admin Console.

   ![Grupos removidos 1](/help/security/assets/removed-groups-1.png)

1. Grupos de AEM associados a perfis de produto do Adobe Admin Console não relacionados à camada do AEM ou à combinação de ambiente específica (por exemplo, `author` ou `e4535`). Isso pode incluir perfis de produto que são:

   * relacionado a outros produtos Adobe
   * relacionados com outros programas de AEM
   * relacionados com outros ambientes AEM no mesmo programa AEM
   * relacionado a uma camada diferente (por exemplo, `author` vs `publish`) no mesmo ambiente AEM
   * relacionado ao Cloud Manager (por exemplo, `Business Owner - Cloud Service`)

   Por exemplo, na imagem abaixo, há muitas linhas com o padrão `AEM Administrators-<suffix>` ou `AEM Users-<suffix>` onde o sufixo não está relacionado ao ambiente atual.

   ![Grupos removidos 2](/help/security/assets/removed-groups-2.png)

Você pode verificar qual sufixo está relacionado ao ambiente atual selecionando Gerenciar **Acesso - Perfis de Autor** (ou **Perfis do Publish**) no menu de ação do ambiente no Cloud Manager.

![Verificar sufixos](/help/security/assets/suffix-check.png)

Isso navegará para a Adobe Admin Console, conforme representado na captura de tela abaixo. Observe que `<suffix>` pode ser um conjunto aleatório de caracteres ou, melhor, a camada e as IDs de programa e ambiente (por exemplo, `author - Program 12345 - Environment 45678`).

![Sufixos no Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

No caso improvável de seu aplicativo AEM fazer referência a esses grupos, use grupos de usuários do Adobe Admin Console.

>[!NOTE]
>
>Em particular, cuidado com essas possíveis armadilhas:
>
>1. Seu aplicativo AEM depende de um grupo AEM que foi sincronizado de um perfil de produto do Cloud Manager
>1. O nível de publicação do aplicativo AEM depende de um grupo AEM que foi sincronizado de um perfil de produto no nível do autor. Isso também é verdadeiro para o cenário inverso (o nível do autor depende do nível de publicação).