---
title: Adicionar Listas de permissões de IP
description: Saiba como adicionar suas próprias Listas de permissões de IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 9%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria Lista de permissões IP usando o Cloud Manager.

Um usuário na função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para adicionar uma Lista de permissões de IP.

{{add-cm-allowlist-frontend-pipeline}}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, usando o painel lateral no lado esquerdo (talvez seja necessário clicar no ícone de hambúrguer no canto superior esquerdo para ver o painel), clique em **Listas de permissões de IP**.

   ![Opção de Listas de permissões IP no painel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Próximo ao canto superior direito da página Listas de permissões IP, clique em **Adicionar Lista de permissões IP**.

   ![A caixa de diálogo Adicionar lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Na caixa de diálogo **Adicionar Lista de permissões IP**, no campo **Nome da Lista de permissões IP**, digite um nome que você deseja usar para fazer referência à Lista de permissões IP. Esse nome é apenas informativo. Verifique se ela é descritiva o suficiente para ajudar a identificar a lista.

1. No campo **Endereço IP / CIDR**, insira um bloco IP ou CIDR para IP. Separe vários blocos com uma vírgula ou uma tabulação.

1. Clique em **Salvar**.

Depois de salvar, a Lista de permissões IP recém-criada aparece como uma linha na tabela na página **Listas de permissões IP**.

## Adicionar a Lista de permissões de IP do Cloud Manager {#add-cm-allowlist}

O pipeline de front-end requer que a seguinte Lista de permissões de IP do Cloud Manager seja adicionada com antecedência.

**Lista de permissões IP Cloud Manager**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

Para evitar a interrupção da execução do pipeline de front-end, verifique se esta Lista de permissões de IP do Cloud Manager foi adicionada e aplicada ao serviço de Autor do ambiente *antes* de habilitar o pipeline.

**Para adicionar a Lista de permissões IP do Cloud Manager:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, usando o painel lateral no lado esquerdo (talvez seja necessário clicar no ícone de hambúrguer no canto superior esquerdo para ver o painel), clique em **Listas de permissões de IP**.

1. Próximo ao canto superior direito da página Listas de permissões IP, clique em **Adicionar Lista de permissões IP**.

1. Na caixa de diálogo **Adicionar Lista de permissões IP**, no campo **Nome da Lista de permissões IP**, digite *`Cloud Manager`*.

1. Copie o bloco de endereços de Lista de permissões IP da Cloud Manager acima. Cada endereço já está separado por vírgula.

1. Na caixa de diálogo **Adicionar Lista de permissões de IP**, cole o bloco no campo **Endereço IP/CIDR**.

1. Coloque o cursor logo após a primeira vírgula na lista de endereços e pressione **Enter**.

1. Clique em **Salvar**.

Agora, [aplique a Lista de permissões IP do Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) aos ambientes do programa.



