---
title: Adicionar listas de permissões de IP
description: Saiba como adicionar sua própria lista de permissões IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria lista de permissões IP usando o Cloud Manager.

Um usuário com função de **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para adicionar uma lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.

   ![Opção de listas de permissões de IP no painel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clique em **Adicionar lista de permissões de IP** para abrir a caixa de diálogo **Adicionar lista de permissões de IP**.

   ![A caixa de diálogo Adicionar lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Insira o nome que gostaria de usar para fazer referência à lista de permissões no campo **Nome da lista de permissões de IP**.

   * Isso é apenas para fins de informação e deve ser descritivo para ajudar a identificar a lista.

1. Insira um bloco IP ou CIDR para IP no campo **Endereço IP/CIDR**.

   * Vários blocos podem ser separados por vírgula ou por tabulação.

1. Clique em **Salvar** para confirmar o envio.

Ao salvar, a lista de permissões de IP recém-criada aparecerá como uma linha na tabela localizada na página **Listas de permissões de IP**.
