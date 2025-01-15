---
title: Alterações na sincronização de grupos de usuários e perfis de produtos
description: Saiba mais sobre as alterações na sincronização do grupo de usuários e do perfil de produto que chegam ao AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: cddfcddc0ca3652270bdb735e580386ac9ff1fc7
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Alterações na sincronização de grupos de usuários e perfis de produtos {#changes-in-user-group-and-product-profile-synchronization}

Sempre que um usuário faz logon no AEM as a Cloud Service ou um token de acesso é usado, os grupos de usuários, perfis de produtos e serviços de perfil de produtos do Adobe Admin Console são sincronizados no repositório do AEM como grupos.

Com versões do AEM superiores a 18751 (uma versão de manutenção começará a ser implementada em ambientes de produção em 27 de janeiro), a fim de reduzir a desordem da interface do usuário e otimizar o desempenho, haverá algumas alterações no comportamento de sincronização, resultando no surgimento de menos grupos no AEM. Duas categorias de grupos AEM serão removidas:

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

