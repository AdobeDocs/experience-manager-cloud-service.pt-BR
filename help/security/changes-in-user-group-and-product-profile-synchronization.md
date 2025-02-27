---
title: Alterações na sincronização de grupos de usuários e perfis de produtos
description: Saiba mais sobre as alterações na sincronização do grupo de usuários e do perfil de produto que chegam ao AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Alterações na sincronização de grupos de usuários e perfis de produtos {#changes-in-user-group-and-product-profile-synchronization}

Sempre que um usuário faz logon no AEM as a Cloud Service ou um token de acesso é usado, os grupos de usuários, perfis de produtos e serviços de perfil de produtos do Adobe Admin Console são sincronizados no repositório do AEM como grupos.

A partir da Versão de manutenção do AEM 19149, o comportamento de sincronização do grupo é alterado para reduzir a desordem da interface e otimizar o desempenho. Especificamente, a associação do grupo de usuários das duas categorias de grupos AEM a seguir não será mais sincronizada:

1. Grupos AEM com Sufixo `GROUP_NAME_SUFFIX`. Esses grupos não aparecem na Adobe Developer Console, mas aparecem na tela Gerenciamento de grupos AEM, como mostrado abaixo. No caso improvável de o aplicativo AEM fazer referência a esses grupos, faça referência a grupos de usuários do Adobe Admin Console sem esse sufixo.

   ![Grupos removidos 1](/help/security/assets/removed-groups-1.png)

1. Grupos de AEM associados a perfis de produto do Adobe Admin Console não relacionados ao ambiente específico. Isso pode incluir perfis de produto que são:

   * relacionado a outros produtos Adobe
   * relacionados com outros programas de AEM
   * relacionados com outros ambientes AEM no mesmo programa AEM
   * relacionado ao Cloud Manager (por exemplo, `Business Owner - Cloud Service`)

   Por exemplo, na imagem abaixo, há muitas linhas com o padrão `AEM Administrators-<suffix>` ou `AEM Users-<suffix>` onde o sufixo não está relacionado ao ambiente atual.

   ![Grupos removidos 2](/help/security/assets/removed-groups-2.png)

Você pode verificar qual sufixo está relacionado ao ambiente atual selecionando Gerenciar **Acesso - Perfis de Autor** (ou **Perfis do Publish**) no menu de ação do ambiente no Cloud Manager.

![Verificar sufixos](/help/security/assets/suffix-check.png)

Isso navegará para a Adobe Admin Console, conforme representado na captura de tela abaixo. Observe que `<suffix>` pode ser um conjunto aleatório de caracteres ou, melhor, a camada e as IDs de programa e ambiente (por exemplo, `author - Program 12345 - Environment 45678`).

![Sufixos no Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

No caso improvável de seu aplicativo AEM fazer referência a um grupo que não aparecerá mais no AEM, certifique-se de usar i) um Perfil de produto da instância correta do AEM ou ii) um grupo de usuários do Adobe Admin Console.

As associações de grupo do usuário são sincronizadas quando fazem logon no ambiente e são removidas de grupos não relacionados ao ambiente atual. Os próprios grupos permanecem e incluem usuários que não fizeram logon desde que o recurso foi habilitado.
