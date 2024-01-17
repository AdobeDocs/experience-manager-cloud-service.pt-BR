---
title: Relatórios de SLA
description: Saiba como visualizar o desempenho do seu ambiente de produção do AEM em relação ao acordo de nível de serviço (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 88%

---


# Relatórios de SLA {#sla-reporting}

Saiba como visualizar o desempenho do seu ambiente de produção do AEM em relação ao acordo de nível de serviço (SLA).

## Introdução {#introduction}

Os dados de relatórios de SLA estão disponíveis para cada programa de produção por meio da guia **Relatórios**. Siga estas etapas para acessar.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** selecione o programa.

1. Navegue até a guia **Relatórios** na página **Visão geral**.

1. Clique no ano desejado para ver os dados de SLA mostrados na forma de um gráfico.

![Exemplo de gráfico de SLA](assets/sla-reporting-1.png)

Passe o cursor sobre um ponto de dados para ver os valores específicos desse ponto.

![Exibição de dados detalhados](assets/sla-reporting-b.png)

## Métricas de SLA {#sla-metrics}

O gráfico do ano selecionado inclui vários conjuntos de dados.

* **Contrato de Nível de Publicação** - Esse é o SLA definido em seu contrato com a Adobe para o nível de publicação.

* **Nível de Publicação Real** - Esse é o tempo de atividade medido no nível de publicação de produção depois de deduzidos os incidentes causados pela Adobe ou pelos fornecedores da Adobe.

* **Contrato de Nível de Autor** - Esse é o SLA definido em seu contrato com a Adobe para a camada de autor.

* **Nível de Autoria Real** - Esse é o tempo de atividade medido no nível de autoria de produção depois de deduzidos os incidentes causados pela Adobe ou pelos fornecedores da Adobe.

## Análise de eventos {#event-analysis}

A seção **Análise de eventos** no gráfico mostra o conjunto de incidentes que ocorreram para o programa durante o ano selecionado.

Cada um dos incidentes tem um intervalo de tempo, uma causa e um conjunto de comentários.

![Exemplo de análise de eventos](assets/sla-reporting-c.png)
