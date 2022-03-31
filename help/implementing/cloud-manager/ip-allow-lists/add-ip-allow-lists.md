---
title: Adicionar Listas de permissões IP
description: Saiba como adicionar sua própria lista de permissões IP usando o Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---


# Adicionar uma lista de permissões de IP {#add-ip-allow-list}

Saiba como adicionar sua própria lista de permissões IP usando o Cloud Manager.

Um usuário na **Proprietário da empresa** ou **Gerenciador de implantação** pode seguir essas etapas para adicionar uma lista de permissões IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Ambientes** da tela **Visão geral** página.

1. Navegar para **LISTAS DE PERMISSÕES de IP** da página **Ambientes** tela.

   ![Opção de listas de permissões IP no painel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clique em **Adicionar Lista de permissões IP** para abrir o **Adicionar Lista de permissões IP** caixa de diálogo.

   ![A caixa de diálogo Adicionar Lista de permissões IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Insira um nome que gostaria de usar para fazer referência à lista de permissões no **Nome da Lista de permissões IP** campo.

   * Isso é apenas informativo e deve ser descritivo para ajudar a identificar a lista.

1. Insira um bloco IP ou IP CIDR no **Endereço IP/CIDR** campo.

   * Vários blocos podem ser separados por vírgula ou por guia.

1. Clique em **Salvar** para confirmar o envio.

Ao salvar, a lista de permissões IP recém-criada aparecerá como uma linha na tabela no **LISTAS DE PERMISSÕES de IP** página.
