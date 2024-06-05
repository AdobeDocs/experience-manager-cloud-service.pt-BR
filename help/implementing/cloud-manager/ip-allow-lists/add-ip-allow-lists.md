---
title: Adicionar listas de permissões de IP
description: Saiba como adicionar sua própria lista de permissões de IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 71%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria lista de permissões de IP usando o Cloud Manager.

Um usuário com função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para adicionar uma lista de permissões de IP.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)** selecione o programa.

1. No **Visão geral** , navegue até o **LISTAS DE PERMISSÕES IP** usando a guia de navegação lateral.

   ![Opção de listas de permissões de IP no painel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clique em **Adicionar Lista de permissões de IP**.

   ![A caixa de diálogo Adicionar lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. No **Adicionar Lista de permissões de IP** incluir na lista de permissões , digite o nome que deseja usar para fazer referência ao arquivo de pesquisa na caixa de diálogo **Nome da Lista de permissões de IP** campo.

   * Esse nome é apenas informativo e deve fornecer uma descrição que ajude a identificar a lista.

1. Insira um bloco IP ou CIDR para IP no campo **Endereço IP/CIDR**.

   * Vários blocos podem ser separados por vírgula ou por tabulação.

1. Clique em **Salvar**.

Após salvar, a lista de permissões de IP recém-criada aparecerá como uma linha na tabela da página **Listas de permissões de IP**.
