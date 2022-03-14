---
title: Verificação de status do registro DNS
description: Verificação de status do registro DNS
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 5%

---

# Verificação de status do registro DNS {#check-dns-record-status}

Você pode determinar se o nome de domínio está sendo resolvido corretamente para o site AEM as a Cloud Service clicando no ícone Status do registro DNS na tabela na tabela Ambientes da página Configurações de domínio .

O Cloud Manager acionará automaticamente uma pesquisa de DNS quando o Nome de domínio personalizado for verificado e implantado pela primeira vez com êxito. Para tentativas subsequentes, é necessário selecionar ativamente a variável **resolver novamente** ícone ao lado do status.

O Cloud Manager realiza uma pesquisa de DNS para o nome de domínio e exibe uma das seguintes mensagens de status:

* **Status de DNS não detectado**
O status de DNS não será detectado até que o nome de domínio personalizado tenha sido verificado e implantado com êxito. Esse status também é observado quando o nome do Domínio personalizado está em processo de exclusão.

* **O DNS resolve incorretamente**
Isso indica que a configuração de registros DNS ainda não foi resolvida/apontada ou está incorreta.

   >[!NOTE]
   >Você deve configurar um `CNAME` ou `A-record` seguindo as instruções correspondentes. Consulte Definição de configurações de DNS para saber mais. Quando estiver pronto, você deverá selecionar a variável **resolver novamente** ícone ao lado do status.

* **Resolução DNS em Andamento**
A resolução está em curso. Normalmente, esse status é visto depois que você seleciona o ícone &quot;resolver novamente&quot; ao lado do status .

* **O DNS resolve corretamente**
Suas configurações de DNS estão configuradas corretamente. Seu site está servindo visitantes.
