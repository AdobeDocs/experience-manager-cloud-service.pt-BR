---
title: Serviço de notificação do Screens no Screens as a Cloud Service
description: Esta página descreve como configurar o Serviço de notificação no Screens as a Cloud Service.
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---

# Serviço de notificação do Screens {#notification-service}

## Introdução {#introduction}

### Visão geral

O Serviço de notificações da AEM Screens permite que os administradores recebam um relatório com uma lista de todos os players do AEM Screens que não executaram ping por um período configurável em um email.

### Como configurar

Na AEM Screens Cloud, os clientes podem solicitar um relatório sobre o status de inatividade do dispositivo criando um tíquete de suporte com as seguintes informações:

* Nome do Cliente
* IMS OrgID
* Frequência de agendamento: especifique uma hora ou frequência em horas (por exemplo, 1) em que esse monitor deve enviar emails.
* Tempo limite de ping: especifica o intervalo em minutos após o qual um dispositivo deve ser considerado inacessível.
* ID(s) de email : ID(s) de email para onde o relatório será enviado

>[!NOTE]
>Os emails terão o reprodutor relatado somente se o dispositivo que não tiver executado ping para o tempo limite de ping fornecido no momento da geração do email.

### Exemplo de caso de uso

Se você definir a hora do relatório como 5 am e o tempo limite de ping como 1 hora, se o dispositivo Screens não executar ping entre 4:00 e 5:00 am, você receberá uma notificação por email confirmando a inatividade do dispositivo.
