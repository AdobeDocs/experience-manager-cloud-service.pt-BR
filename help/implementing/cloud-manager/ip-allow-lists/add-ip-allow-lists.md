---
title: Adicionar Listas de permissões de IP
description: Saiba como adicionar suas próprias Listas de permissões de IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 593b8c704c5b016bb55ae6a25420b577044b4126
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 11%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria Lista de permissões IP usando o Cloud Manager.

Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para adicionar uma Lista de permissões de IP.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**Para adicionar uma Lista de permissões IP:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, usando o menu do lado esquerdo (talvez seja necessário clicar em ![Mostrar ícone do menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) no canto superior esquerdo para ver o menu), clique em ![Ícone da lista de tarefas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permissões IP**.

   ![Opção de Listas de permissões IP no menu do lado esquerdo](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Próximo ao canto superior direito da página Listas de permissões IP, clique em **Adicionar Lista de permissões IP**.

   ![A caixa de diálogo Adicionar lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Na caixa de diálogo **Adicionar Lista de permissões IP**, no campo **Nome da Lista de permissões IP**, digite um nome que você deseja usar para fazer referência à Lista de permissões IP. Esse nome é apenas informativo. Verifique se ela é descritiva o suficiente para ajudar a identificar a lista.

1. No campo **Endereço IP / CIDR**, insira um bloco IP ou CIDR para IP. Separe vários blocos com uma vírgula ou uma tabulação.

1. Clique em **Salvar**.

Depois de salvar, a Lista de permissões IP recém-criada aparece como uma linha na tabela na página **Listas de permissões IP**.

