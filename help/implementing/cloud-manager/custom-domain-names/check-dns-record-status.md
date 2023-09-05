---
title: Verificação de status do registro DNS
description: Saiba como determinar se as configurações de DNS são resolvidas corretamente usando o Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '250'
ht-degree: 100%

---

# Verificação de status do registro DNS {#check-dns-record-status}

No Cloud Manager, você pode determinar se o nome de domínio é resolvido corretamente para o seu site do AEM as a Cloud Service.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no painel de navegação esquerdo.

1. Clique no ícone de **Status** do nome do domínio.

O Cloud Manager realiza uma consulta de DNS quanto ao nome do domínio e exibe uma das mensagens de status a seguir.

* **Status de DNS não detectado** - O status de DNS não será detectado até que o nome de domínio personalizado tenha sido verificado e implantado com êxito.

   * Esse status também é observado quando o nome do domínio personalizado está em processo de exclusão.

* **O DNS resolve incorretamente** - Indica que a configuração dos registros DNS não foi resolvida ou está incorreta.

   * Consulte [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.
   * Quando estiver pronto, você deverá selecionar o ícone **Resolver novamente** ao lado do status.

* **Resolução DNS em andamento** - A resolução está em andamento.

   * Normalmente, esse status é exibido depois de selecionar o ícone **Resolver novamente** ao lado do status.

* **O DNS resolve corretamente** - Suas configurações de DNS estão configuradas corretamente.

   * Seu site está atendendo visitantes.

O Cloud Manager acionará automaticamente uma consulta de DNS depois de o nome de domínio personalizado ter sido verificado e implantado com sucesso pela primeira vez. Para tentativas subsequentes, é necessário selecionar ativamente o ícone **Resolver novamente** ao lado do status.
