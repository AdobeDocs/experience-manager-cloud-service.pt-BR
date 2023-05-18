---
title: Monitoramento de infraestrutura e serviços no AEM as a Cloud Service
description: Monitoramento de infraestrutura e serviços no AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 34fed4e64b49ab32e7025c9654d930e3fa362a52
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Monitoramento de infraestrutura e serviços no AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

O Adobe Experience Manager as a Cloud Service fornece observabilidade e monitoramento de: infraestrutura, serviços e experiência do usuário. Como várias soluções são usadas e há várias camadas de monitoramento, esta página é organizada em três seções:

* [Disponibilidade externa](#external-availability)
* [Monitoramento de módulo interno](#module-monitoring)
* [Observabilidade do cliente](#customer-observability)

AEM as a Cloud Service usa centenas de monitores nativos em nuvem para informar continuamente o estado de cada ambiente (24 horas por dia, 7 dias por semana) por 365 dias por ano. As definições do monitor não são estáticas, elas são continuamente revisadas para melhorar a capacidade de detecção precoce. Além disso, o Adobe tem procedimentos de chamada configurados para responder a alertas.

Se você precisar de informações sobre outros tipos de monitoramento, como logon ou monitoramento pelo Cloud Manager, consulte a seção [Recursos adicionais](#resources) seção.

## Disponibilidade externa {#external-availability}

A disponibilidade externa é composta por duas partes: Edge de serviço e monitoramento personalizado.

### Edge de serviço {#service-edge}

Todos os seus ambientes AEM as a Cloud Service são monitorados quanto à disponibilidade. No entanto, o Service Edge Monitoring é configurado apenas para ambientes de produção e as métricas são usadas para calcular o SLA do cliente. Leva em consideração o tempo de execução do ambiente e o CDN AEM as a Cloud Service. O Service Edge Monitoring emprega cinco locais distintos próximos à região escolhida e verifica periodicamente a disponibilidade. A indisponibilidade de um site acionará um alerta e envolverá equipes e processos de suporte em chamadas do Adobe.

### Monitoramento personalizado {#custom-monitoring}

Com o monitoramento personalizado, os clientes têm a opção de fornecer até cinco URLs de propriedade da Web distintos antes de [ao vivo](/help/journey-migration/go-live.md). Esses URLs devem ser válidos e retornar um código de resposta HTTP 200. Esses monitores suportam clientes que [traga sua própria CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) na frente da Adobe CDN e de qualquer roteamento de tráfego externo usado em frente de AEM as a Cloud Service que não esteja sob controle de Adobe. Os alertas resultantes de verificações de monitoramento personalizado envolverão equipes e processos de suporte Adobe.

>[!NOTE]
>
> Essa funcionalidade é oferecida apenas para clientes com suporte avançado à nuvem. Em caso de dúvidas, envie um caso de suporte para o Admin Console.

## Monitoramento de módulo interno {#module-monitoring}

Embora a disponibilidade externa esteja focada no monitoramento do usuário final, o monitoramento do módulo interno observa se os sub-sistemas arquitetônicos estão funcionando nominalmente sem degradação de recursos ou desempenho. Em caso de problema, os alertas são acionados para que as reparações possam ser feitas automaticamente ou por meio do envolvimento da equipe de operações, com o objetivo de evitar a disponibilidade comprometida. Há várias categorias de monitores, apresentados abaixo são alguns exemplos de verificações:

* A porcentagem de capacidade da CPU não excede um determinado limite.
* As reimplantações de instância não excedem uma certa frequência.
* O uso de disco está abaixo de um determinado limite.
* O tamanho do repositório do autor está dentro de determinados limites.
* As operações de backup são concluídas com êxito.
* A integridade e o desempenho do banco de dados são monitorados.
* Os serviços da AEM Cloud estão se comportando como esperado, incluindo nenhuma fila de replicação bloqueada, dados consistentes e consultas de desempenho.

Verificações adicionais são adicionadas a ambientes provisionados para o Forms. Lembre-se de que as definições de verificação não são estáticas e estão sujeitas a alterações e atualizações.

## Observabilidade do cliente {#customer-observability}

Os clientes podem usar o [Monitoramento de desempenho do aplicativo New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) que fornece dados de desempenho em tempo real coletados e gráficos para análise e solução de problemas. Ao usar o conjunto de monitoramento, os clientes podem observar diretamente várias métricas, como: Métricas de desempenho da JVM, tempo de transação para Java, chamadas externas em segundo plano e chamadas de banco de dados.

## Recursos adicionais {#resources}

* [Monitoramento de desempenho do aplicativo New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [Registro para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Monitoramento de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
