---
title: Verificando o status do registro DNS
description: Verificando o status do registro DNS
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Verificando o status do registro DNS {#check-dns-record-status}

Você pode determinar se seu nome de domínio está resolvendo corretamente para seu AEM como um site de Cloud Service, clicando no ícone Status do registro DNS na tabela da página Configurações de domínio.

O Cloud Manager acionará automaticamente uma pesquisa DNS quando seu Nome de domínio personalizado for verificado e implantado pela primeira vez com êxito. Para tentativas subsequentes, você deve selecionar ativamente o ícone **resolver novamente** ao lado do status.

O Cloud Manager realiza uma pesquisa DNS para seu nome de domínio e exibe uma das seguintes mensagens de status:

* **O status de DNS não foi**
detectado. O status de DNS não será detectado até que seu nome de domínio personalizado tenha sido verificado e implantado com êxito. Esse status também é observado quando seu nome de Domínio personalizado está em processo de exclusão.

* **Resoluções de DNS**
incorretasIsso indica que a configuração de registros de DNS ainda não foi resolvida/apontou para cima ou está incorreta. Um representante Adobe será notificado automaticamente.

   >[!NOTE]
   >Você deve configurar `CNAME` ou `A-record` seguindo as instruções correspondentes. Consulte Configurando configurações de DNS para saber mais. Quando estiver pronto, você deve selecionar o ícone **resolver novamente** ao lado do status.

* **Resolução DNS em**
andamentoResolução em andamento. Normalmente, esse status é visto depois que você seleciona o ícone &quot;resolver novamente&quot; ao lado do status.

* **Resolve DNS**
corretamenteSuas configurações de DNS estão configuradas corretamente. Seu site está servindo visitantes.
