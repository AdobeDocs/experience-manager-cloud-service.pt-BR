---
title: Verificando o Status do Registro DNS
description: Verificando o Status do Registro DNS
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Verificando o Status do Registro DNS {#check-dns-record-status}

Você pode determinar se o nome de domínio está sendo resolvido corretamente para o site AEM as a Cloud Service clicando no ícone Status do registro DNS da tabela na página Ambientes das configurações do domínio .

O Cloud Manager acionará automaticamente uma pesquisa de DNS quando o Nome de domínio personalizado for verificado e implantado pela primeira vez com êxito. Para tentativas subsequentes, você deve selecionar ativamente o ícone **resolver novamente** ao lado do status.

O Cloud Manager realiza uma pesquisa de DNS para o nome de domínio e exibe uma das seguintes mensagens de status:

* **O status de DNS não**
detectado. O status de DNS não será detectado até que o nome de domínio personalizado tenha sido verificado e implantado com êxito. Esse status também é observado quando o nome do Domínio personalizado está em processo de exclusão.

* **Resoluções de DNS**
IncorretamenteIsso indica que a configuração de registros de DNS ainda não foi resolvida/apontada ou está incorreta. Um representante da Adobe será notificado automaticamente.

   >[!NOTE]
   >Você deve configurar um `CNAME` ou `A-record` seguindo as instruções correspondentes. Consulte Definição de configurações de DNS para saber mais. Quando estiver pronto, você deve selecionar o ícone **resolver novamente** ao lado do status.

* **Resolução de DNS em**
AndamentoSolução em andamento. Normalmente, esse status é visto depois que você seleciona o ícone &quot;resolver novamente&quot; ao lado do status .

* **Soluções de DNS**
CorretamenteSuas configurações de DNS estão configuradas corretamente. Seu site está servindo visitantes.
