---
title: Hibernar e cancelar hibernação em ambientes de sandbox
description: Saiba como os ambientes de um programa de sandbox entram automaticamente em um modo de hibernação e como você pode removê-los.
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 42%

---


# Hibernar e cancelar hibernação em ambientes de sandbox {#hibernating-introduction}

Os ambientes de um programa de sandbox entram em um modo de hibernação se nenhuma atividade for detectada por oito horas. A hibernação é exclusiva dos ambientes de programas de sandbox. Os ambientes de programas de produção não podem ser hibernados.

## Hibernação {#hibernation-introduction}

A hibernação pode ocorrer automática ou manualmente.

* **Automático** - Os ambientes dos programas de sandbox hibernam automaticamente após oito horas de inatividade. A inatividade é definida como a ausência de solicitações para os serviços de criação, visualização e publicação.
* **Manual** - Como usuário, você pode hibernar manualmente um ambiente de programa de sandbox. Não há necessidade de fazer isso, pois a hibernação ocorre automaticamente, conforme descrito anteriormente.

Pode levar alguns minutos para que os ambientes dos programas de sandbox entrem no modo de hibernação. Os dados são preservados durante a hibernação.

### Hibernar um ambiente de programa de sandbox manualmente {#using-manual-hibernation}

Você pode hibernar manualmente seu programa de sandbox no Console do desenvolvedor. O acesso à Developer Console para um programa de sandbox está disponível para qualquer usuário do Cloud Manager.

**Para hibernar um ambiente de programa de sandbox manualmente:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, clique em um *programa de sandbox* que você deseja hibernar para exibir seus detalhes.

1. No cartão **Ambientes**, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Developer Console**.

   * Consulte [Acesso ao Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obter detalhes adicionais sobre o Developer Console.

   ![Opção de menu do Console do desenvolvedor](/help/implementing/cloud-manager/assets/developer-console-menu-option.png)

1. Na página **Developer Console**, clique em **Hibernar**.

<!-- UPDATE THESE SCREENSHOTS WHEN NEW AEM DEVELOPER CONSOLE UI IS RELEASED. AS OF OCTOBER 14, 2024, NEW UI IS STILL IN PRIVATE BETA -->

![Botão Hibernar](assets/hibernate-1.png)

1. Clique em **Hibernar** para confirmar a etapa.

   ![Confirmar hibernação](assets/hibernate-2.png)

Quando a hibernação for bem-sucedida, você verá a notificação de conclusão do processo de hibernação para o seu ambiente na tela **Developer Console**.

![Confirmação de hibernação](assets/hibernate-4.png)

Na Developer Console, clique no link **Ambientes** na navegação estrutural acima da lista suspensa **Pod** para exibir os ambientes disponíveis para hibernação.

![Lista de ambientes que devem ser hibernados](assets/hibernate-1b.png)

## Cancelar a hibernação de um programa de sandbox da Developer Console manualmente {#de-hibernation-introduction}

Você pode hibernar manualmente seu programa de sandbox na Developer Console.

>[!IMPORTANT]
>
>Um usuário com função de **Desenvolvedor** pode cancelar a hibernação de um ambiente de programa de sandbox.

**Para cancelar a hibernação de um programa de sandbox da Developer Console manualmente:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, clique no programa que deseja cancelar a hibernação para exibir seus detalhes.

1. No cartão **Ambientes**, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Developer Console**.

   * Consulte [Acesso ao Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obter detalhes adicionais sobre o Developer Console.

1. Clique em **Cancelar hibernação**.

   ![Botão Cancelar hibernação](assets/de-hibernation-img1.png)

1. Clique em **Cancelar hibernação** para confirmar a etapa.

   ![Confirmar cancelamento de hibernação](assets/de-hibernation-img2.png)

1. Você recebe uma notificação de que o processo de cancelamento da hibernação foi iniciado, bem como atualizações sobre o progresso.

   ![Notificação do progresso da hibernação](assets/de-hibernation-img3.png)

1. Quando o processo for concluído, o ambiente do programa de sandbox ficará ativo novamente.

   ![Cancelamento da hibernação concluído](assets/de-hibernation-img4.png)

Na Developer Console, clique no link **Ambientes** na navegação estrutural acima da lista suspensa **Pod** para acessar os ambientes disponíveis para desibernação.

![Lista de pods hibernados](assets/de-hibernate-1b.png)

### Permissões para cancelar hibernação {#permissions-de-hibernate}

Qualquer usuário com um perfil de produto que dê acesso ao AEM as a Cloud Service deve poder acessar o **Console do desenvolvedor**, permitindo cancelar a hibernação do ambiente.

## Acessar um ambiente hibernado {#accessing-hibernated-environment}

Quando um usuário faz uma solicitação do navegador para o serviço de autoria, visualização ou publicação de um ambiente hibernado, encontra uma página de aterrissagem. Esta página explica o status hibernado do ambiente e fornece um link para o Developer Console para cancelar a hibernação.

![Página de aterrissagem de um serviço hibernado](assets/de-hibernation-img5.png)

## Implantações e atualizações do AEM {#deployments-updates}

Ambientes hibernados ainda permitem a realização de implantações e atualizações manuais do AEM.

* Um usuário pode usar um pipeline para implantar código personalizado em ambientes hibernados. O ambiente permanece hibernado e o novo código aparece no ambiente após o cancelamento da hibernação.

* As atualizações do AEM podem ser aplicadas a ambientes hibernados e podem ser acionadas manualmente pelo Cloud Manager. O ambiente permanece hibernado e a nova versão aparece no ambiente após o cancelamento da hibernação.

## Hibernação e exclusão {#hibernation-deletion}

* Os ambientes em um programa de sandbox são hibernados automaticamente após oito horas de inatividade.
   * A inatividade é definida como a ausência de solicitações para os serviços de criação, visualização e publicação.
   * Uma vez hibernados, eles podem ter [hibernado manualmente](#de-hibernation-introduction).
* Os programas de sandbox são excluídos após seis meses em modo de hibernação contínua, depois disso, podem ser recriados.

>[!NOTE]
>
>Somente ambientes sandbox são excluídos automaticamente após seis meses de hibernação contínua. O programa sandbox com seu repositório e código é mantido.
