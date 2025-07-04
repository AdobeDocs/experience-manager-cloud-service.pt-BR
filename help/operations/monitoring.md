---
title: Monitoramento de infraestrutura e serviços no AEM as a Cloud Service
description: Monitoramento de infraestrutura e serviços no AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 5%

---

# Monitoramento de infraestrutura e serviços no AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

O Adobe Experience Manager as a Cloud Service oferece observabilidade e monitoramento de: infraestrutura, serviços e experiência do usuário. Como várias soluções são usadas e há várias camadas de monitoramento, esta página está organizada em três seções:

* [Disponibilidade externa](#external-availability)
* [Monitoramento do módulo interno](#module-monitoring)
* [Observabilidade do cliente](#customer-observability)

A AEM as a Cloud Service usa centenas de monitores nativos em nuvem para relatar continuamente o estado de cada ambiente (24 horas por dia, 7 dias por semana) por 365 dias por ano. As definições do monitor não são estáticas, mas são continuamente revisadas para melhorar a capacidade de detecção antecipada. Além disso, o Adobe tem procedimentos on-call configurados para responder a alertas.

Se você precisar de informações sobre outros tipos de monitoramento, como logon ou monitoramento pelo Cloud Manager, consulte [Recursos Adicionais](#resources).

## Disponibilidade externa {#external-availability}

A disponibilidade externa é composta por duas partes: Service Edge e Monitoramento personalizado.

### Edge de serviço {#service-edge}

Todos os seus ambientes do AEM as a Cloud Service são monitorados em relação à disponibilidade. No entanto, o Monitoramento do Service Edge é configurado apenas para ambientes de produção e as métricas são usadas para calcular o SLA do cliente. Leva em consideração o tempo de execução do ambiente e o AEM as a Cloud Service CDN. O Service Edge Monitoring emprega cinco locais distintos próximos à região escolhida e verifica periodicamente a disponibilidade. A indisponibilidade de um site aciona um alerta e envolve equipes e processos de suporte de chamada do Adobe.

### Monitoramento personalizado {#custom-monitoring}

Com o Monitoramento personalizado, os clientes podem, opcionalmente, fornecer até cinco URLs de propriedade da Web distintas antes da [ativação](/help/journey-migration/go-live.md). Esses URLs devem ser válidos e retornar um código de resposta HTTP 200. Esses monitores oferecem suporte a clientes que [trazem seu próprio CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) na frente do CDN de Adobe e qualquer roteamento de tráfego externo empregado na frente do AEM as a Cloud Service que não está sob o controle do Adobe. Alertas resultantes de verificações de Monitoramento personalizado envolvem equipes e processos de suporte do Adobe.

>[!NOTE]
>
> Essa funcionalidade só é oferecida para ambientes de produção e clientes com o [Suporte na nuvem avançado](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html?lang=pt-BR#support-add-ons). Em caso de dúvidas, entre em contato com a equipe de conta do Adobe.

## Monitoramento do módulo interno {#module-monitoring}

Embora a disponibilidade externa se concentre no monitoramento do usuário final, o monitoramento interno do módulo observa se os subsistemas de arquitetura estão operando nominalmente sem degradação de recursos ou desempenho. Se houver um problema, os alertas são acionados para que os reparos possam ser feitos automaticamente ou por meio do envolvimento da equipe de operações, com o objetivo de evitar comprometimento da disponibilidade. Há várias categorias de monitores. Veja abaixo alguns exemplos de verificações:

* A porcentagem de iowait do CPU não excede um determinado limite.
* As reimplantações de instância não excedem uma determinada frequência.
* O uso do disco está abaixo de um determinado limite.
* O tamanho do repositório do autor está dentro de determinados limites.
* As operações de backup foram concluídas com êxito.
* A integridade e o desempenho do banco de dados são monitorados.
* Os serviços da nuvem do AEM estão se comportando conforme esperado, incluindo a ausência de filas de replicação bloqueadas, dados consistentes e consultas de alto desempenho.

Verificações adicionais são adicionadas aos ambientes provisionados para o Forms. As definições de verificação não são estáticas e estão sujeitas a alterações e atualizações.

## Observabilidade do cliente {#customer-observability}

Os clientes podem usar o conjunto [New Relic Application Performance Monitoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=pt-BR) que fornece dados de desempenho em tempo real coletados e mapeados para análise e solução de problemas. Usando o conjunto de monitoramento, os clientes podem observar diretamente várias métricas, como: métricas de desempenho JVM, tempo de transação para Java™, chamadas externas em segundo plano e chamadas de banco de dados.

## Recursos adicionais {#resources}

* [Monitoramento do Desempenho de Aplicativos do New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=pt-BR)
* [Logs para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=pt-BR)
* [Monitoramento de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=pt-BR)
