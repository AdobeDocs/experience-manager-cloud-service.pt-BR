---
title: Verificação de status do registro DNS
description: Saiba como determinar se as configurações de DNS estão sendo resolvidas corretamente usando o Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---

# Verificação de status do registro DNS {#check-dns-record-status}

No Cloud Manager, você pode determinar se o nome de domínio está sendo resolvido corretamente para o seu site as a Cloud Service AEM.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** da tela **Visão geral** página.

1. Clique em **Configurações de domínio** no painel de navegação esquerdo.

1. Clique no botão **Status** ícone para o nome do domínio.

O Cloud Manager realiza uma pesquisa de DNS para o nome de domínio e exibe uma das seguintes mensagens de status.

* **Status de DNS não detectado** - O status de DNS não será detectado até que o nome de domínio personalizado tenha sido verificado e implantado com êxito.

   * Esse status também é observado quando o nome do Domínio personalizado está em processo de exclusão.

* **O DNS resolve incorretamente** - Isso indica que a configuração dos registros DNS não foi resolvida ou está incorreta.

   * Consulte o documento [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.
   * Quando estiver pronto, você deverá selecionar a variável **Resolver novamente** ícone ao lado do status.

* **Resolução DNS em Andamento** - A resolução está em curso.

   * Normalmente, esse status é visualizado depois que você seleciona a variável **Resolver novamente** ícone ao lado do status.

* **O DNS resolve corretamente** - Suas configurações de DNS estão configuradas corretamente.

   * Seu site está servindo visitantes.

O Cloud Manager acionará automaticamente uma pesquisa de DNS quando o nome de domínio personalizado for verificado e implantado com êxito pela primeira vez. Para tentativas subsequentes, é necessário selecionar ativamente a variável **Resolver novamente** ícone ao lado do status.
