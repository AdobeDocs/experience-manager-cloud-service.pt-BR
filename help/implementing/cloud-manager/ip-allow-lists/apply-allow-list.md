---
title: Aplicar e desaplicar Listas de permissões de IP
description: Saiba como aplicar e desaplicar Listas de permissões de IP a ambientes do Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 12%

---


# Aplicar e desaplicar Listas de permissões de IP {#apply-allow-list}

Ao aplicar Listas de permissões de IP, todos os intervalos de IP incluídos na definição da lista são associados a um serviço de autoria ou publicação em um ambiente. Cancelar a aplicação de uma lista é o processo inverso.

## Aplicar Listas de permissões de IP {#applying}

Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para aplicar uma Lista de permissões de IP.

**Para aplicar Listas de permissões de IP:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página de detalhes do ambiente específico na tela **Ambientes**.
1. Navegue até a tabela **Lista de permissões de IP**.
1. Use os campos de entrada na parte superior da tabela para poder selecionar a Lista de permissões IP e o serviço de autoria ou publicação ao qual deseja aplicá-la.
A Lista de permissões IP já deve existir no Cloud Manager para ser aplicada. Consulte [Adicionar Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Clique em **Aplicar** e confirme o envio.

## Desaplicar Listas de permissões de IP {#un-applying}

Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para desaplicar uma Lista de permissões de IP.

**Para desaplicar Listas de permissões de IP:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página de detalhes do ambiente específico na tela **Ambientes**.1. Navegue até a tabela **Lista de permissões de IP**.
1. Identifique a linha da Lista de permissões IP que deseja desaplicar.
1. No lado direito da linha identificada, clique no botão de reticências e selecione **Desaplicar**.
1. Confirme seu envio.
