---
title: Adicionar Listas de permissões de IP
description: Saiba como adicionar suas próprias Listas de permissões de IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 4%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria Lista de permissões IP usando o Cloud Manager.

Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para adicionar uma Lista de permissões de IP.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**Para adicionar uma Lista de permissões IP:**

1. Faça logon no Cloud Manager em [experience.adobe.com](https://experience.adobe.com/experiencemanager/).

1. No menu do lado esquerdo, clique em Cloud Manager e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, usando o menu do lado esquerdo (talvez seja necessário clicar em ![Mostrar ícone do menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) no canto superior esquerdo para ver o menu), clique em ![Ícone da lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permissões IP**.

   ![Opção de Listas de permissões IP no menu do lado esquerdo](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Próximo ao canto superior direito da página Listas de permissões IP, clique em **Adicionar Lista de permissões IP**.

   ![A caixa de diálogo Adicionar lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Na caixa de diálogo **Adicionar Lista de permissões IP**, no campo **Nome da Lista de permissões IP**, digite um nome que você deseja usar para fazer referência à Lista de permissões IP. Esse nome é apenas informativo. Verifique se ela é descritiva o suficiente para ajudar a identificar a lista.

1. No campo **Endereço IP / CIDR**, insira até 50 endereços IP ou blocos CIDR. Você pode adicioná-los de qualquer uma das seguintes maneiras:

   * Digite um endereço de cada vez e pressione `Enter`. Repita o procedimento para cada endereço adicional.
   * Vários de uma vez: Digite endereços separados por vírgulas (,) ou guias e pressione `Enter` para que cada endereço seja reconhecido individualmente.

1. Depois de terminar de inserir o último endereço IP ou bloco CIDR, pressione `Enter` para confirmar a entrada. A entrada é confirmada somente depois que você pressiona `Enter`, e o botão **Salvar** fica ativo.

1. Clique em **Salvar**.

Depois de salvar, a Lista de permissões IP recém-criada aparece como uma linha na tabela na página **Listas de permissões IP**.

