---
title: Gerenciar listas de permissões de IP
description: Saiba como exibir, editar, excluir e verificar o status de Listas de permissões de IP no Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 19%

---

# Gerenciar listas de permissões de IP {#manage-ip-allow-lists}

Saiba como exibir, editar, excluir e verificar o status de Listas de permissões de IP no Cloud Manager.

## Exibir e atualizar Listas de permissões de IP {#update-ip-allow-lists}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma Lista de permissões de IP.

**Para exibir e atualizar Listas de permissões de IP:**

1. Faça logon no Cloud Manager em[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Na página **Visão geral**, no menu do lado esquerdo, em **Serviços**, clique em ![Ícone da lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permissões IP**.
1. Identifique a linha das Listas de permissões IP que deseja exibir ou atualizar.
1. Clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na extremidade direita da linha.
1. No menu suspenso, clique em **Exibir e atualizar**.
A caixa de diálogo **Exibir e Atualizar Lista de permissões de IP** mostra o nome, os endereços IP (ou intervalos) que definem a regra, juntamente com os ambientes e serviços aos quais a regra é aplicada.
1. Altere o nome ou os endereços IP, conforme desejado.

   A adição ou remoção de um novo intervalo IP em uma Lista de permissões IP automaticamente o aplica/desaplica a todos os ambientes/serviços correspondentes aos quais foram aplicados anteriormente.

   Não é possível atualizar uma Lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.

1. Clique em **Atualizar**.

## Verificar o status das Listas de permissões de IP {#check-allow-list-status}

1. Faça logon no Cloud Manager em[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Na página **Visão geral**, no menu do lado esquerdo, em **Serviços**, clique em ![Ícone da lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permissões IP**.

1. Na coluna **Status** da tabela IP Lista de permissões, passe o ponteiro do mouse sobre uma Lista de permissões IP verde (em uso) para ver um ou mais serviços aplicados a ela.

   Os valores de status mostrados na tabela têm os seguintes significados:

   | Status da Lista de permissões de IP | Descrição |
   | --- | --- |
   | Aplicado | A Lista de permissões IP foi aplicada com sucesso a um ou mais ambientes. |
   | Atualizando | Uma atualização da Lista de permissões de IP está em andamento, o que pode incluir um ou mais aplicativos ou o cancelamento da aplicação da lista. Cada aplicação/cancelamento de aplicação é listado junto com seu próprio status de **Não iniciado**, **Em andamento**, **Concluído** ou **Falha**. |
   | Falhou | Falha em um ou mais processos de aplicação ou cancelamento de aplicação de uma atualização.<br>· Cada aplicação e cancelamento de aplicação é listado junto com seu status.<br>· O status é **Falha** se um aplicativo/cancelamento de aplicativo na atualização falhar. O status permanecerá como **Falha** até que todos os problemas sejam resolvidos.<br>· Clique no ícone **Repetir** ao lado do status para que você possa resolver a falha.<br>· Não é possível atualizar ou excluir uma Lista de permissões IP com status **Falha**. |
   | Excluindo | Uma exclusão de uma Lista de permissões IP está em andamento.<br>· A exclusão envolve o cancelamento da aplicação da lista de todos os serviços.<br>· Cada cancelamento de aplicativo é listado junto com seu próprio status de **Não Iniciado**, **Em Andamento**, **Concluído** ou **Falha**.<br>· Quando a operação de exclusão é concluída, a Lista de permissões de IP não aparece na tabela de Listas de permissões de IP. Além disso, a Lista de permissões IP não é aplicada a nenhum serviço no programa no Cloud Manager. |
   | Falha ao excluir | Um ou mais cancelamentos de aplicação falharam durante uma operação de exclusão.<br>· Cada cancelamento de aplicação é listado junto com o status **Concluído** ou **Falha**.<br>· O status torna-se **Falha ao Excluir** se um cancelamento de aplicação falhar. O status permanece como **Falha ao excluir** até que todas as falhas sejam resolvidas. Na extremidade direita da linha da tabela, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e, no menu suspenso, clique em **Excluir** para resolver qualquer falha.<br>· Não será possível atualizar uma Lista de permissões IP enquanto o status for **Falha**. |

## Excluir uma Lista de permissões IP {#delete-allow-list}

Quando você exclui uma Lista de permissões de IP, ela automaticamente desaplica a lista de todos os serviços e a exclui da tabela de Listas de permissões de IP.

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma Lista de permissões de IP.

**Para excluir uma Lista de permissões IP:**

1. Faça logon no Cloud Manager em[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Na página **Visão geral**, no menu do lado esquerdo, em **Serviços**, clique em ![Ícone da lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permissões IP**.
1. Identifique a linha da Lista de permissões IP que deseja excluir e clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na extremidade direita da linha e em **Excluir**.
1. Na caixa de diálogo **Excluir Lista de permissões IP**, clique em **Excluir**.

## Configurações de CDN pré-existentes {#pre-existing-cdn}

Se você tiver uma configuração de CDN (Content Delivery Network) pré-existente para suas Listas de permissões de IP, há uma mensagem informativa na página **Lista de permissões de IP**. A mensagem incentiva você a adicionar essas configurações por meio da interface, para que elas fiquem visíveis e possam ser definidas no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas de **Certificados SSL** e de **Ambientes** para os ambientes que tenham configurações pré-existentes de CDN para certificados SSL ou nomes de domínio personalizados.
