---
title: Adicionar listas de permissões de IP
description: Saiba como adicionar seu próprio arquivo de inclui na lista de permissões de IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 40%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar seu próprio arquivo de inclui na lista de permissões de IP usando o Cloud Manager.

Um usuário no **Proprietário da empresa** ou **Gerente de implantação** A função pode seguir essas etapas para adicionar um arquivo de inclui na lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.

   ![Opção de listas de permissões de IP no painel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clique em **Adicionar Lista de permissões de IP** para abrir o **Adicionar Lista de permissões de IP** caixa de diálogo.

   ![A caixa de diálogo Adicionar Lista de permissões de IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Insira um nome que gostaria de usar para fazer referência à inclui na lista de permissões na **Nome da Lista de permissões de IP** campo.

   * Esse nome é apenas para informação e deve ser descritivo para ajudar a identificar a lista.

1. Insira um bloco IP ou CIDR para IP no campo **Endereço IP/CIDR**.

   * Vários blocos podem ser separados por vírgula ou por tabulação.

1. Clique em **Salvar** para confirmar o envio.

Depois de salvar, a inclui na lista de permissões de IP recém-criada aparece como uma linha na tabela no **LISTAS DE PERMISSÕES IP** página.
