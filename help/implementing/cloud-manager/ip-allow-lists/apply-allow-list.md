---
title: Listas de permissões de IP Aplicar e não oferta
description: Aprenda a aplicar e cancelar a aplicação de listas de permissões de IP em ambientes do Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 328ae6d1866a7089fb291d4872d27dc5fa1d4caa
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 6%

---


# Listas de permissão de IP Aplicar e não aplicativos {#apply-allow-list}

Ao aplicar listas de permissões de IP, todos os intervalos IP incluídos na definição do lista estão associados a um serviço de autor ou publicar em um ambiente. Cancelar a aplicação de uma lista é o processo inverso.

{{add-cm-allowlist-frontend-pipeline}}

## Aplicar listas de permissões de IP {#applying}

Uma usuário no **Empresas Owner** ou **no Gerenciador** de implantação função pode seguir essas etapas para aplicar uma Lista de permissões de IP.

**Para aplicar listas de permissão de IP:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selecione a organização apropriada.
1. **[No console Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Na página **Visão geral**, navegue até a tela **Ambientes**.
1. **Na tela Ambientes**, navegue até os detalhes ambiente específicos página.
1. Navegue até a **tabela De lista** de permissões de IP.
1. Use os campos de entrada na parte superior da tabela para selecionar a Lista de permissões de IP e o serviço Autor, Publish ou Visualização ao qual você a aplica.
A lista de permissões de IP já deve existir no Cloud Manager para aplicá-la. Consulte [Adicionar listas de permissão](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de IP.
1. Clique ![em Adicionar ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Aplicar** e confirme seu envio.

## Cancelar aplicação de listas de permissões de IP {#un-applying}

Uma usuário no Proprietário **do Empresas ou** no **Gerenciador** de implantação função pode seguir essas etapas para desaplicar uma Lista de permissões de IP.

**Para desaplicar listas de permissão de IP:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selecione a organização apropriada.
1. **[No console Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. **Na página Visão geral**, navegue até a página de **Ambientes**.
1. Navegue até os detalhes ambiente específicos página.
1. Na guia Geral, role até a **tabela Permitir lista** de permissões de IP.
1. Identifique a linha da Lista de permissões de IP que você deseja cancelar.
1. No lado direito da linha identificada, clique ![em Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Clique **em Cancelar aplicativo**.
1. **Na caixa de diálogo Permitir** lista de permissões de IP não aplicativo, clique **em Cancelar aplicativo**.
