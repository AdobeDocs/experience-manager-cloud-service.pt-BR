---
title: Serviço de notificação do Screens no Screens as a Cloud Service
description: Esta página descreve como configurar o Serviço de notificação no Screens as a Cloud Service.
index: true
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---


# Serviço de notificação do Screens {#notification-service}

## Introdução {#introduction}

### Visão geral

O Serviço de notificações da AEM Screens permite que os administradores recebam um email se um player do AEM não fizer ping por um período configurável.

### Como configurar

Na AEM Screens Cloud, os clientes podem solicitar alertas sobre o status de inatividade do dispositivo criando um tíquete de suporte com as seguintes informações:

* Nome do Cliente
* IMS OrgID
* Frequência de agendamento: especifique uma hora ou frequência em horas (por exemplo, 1) em que esse monitor deve enviar emails.
* Tempo limite de ping: especifica o intervalo em minutos após o qual um dispositivo deve ser considerado inacessível.
* ID(s) de email : ID(s) de email para onde o relatório será enviado