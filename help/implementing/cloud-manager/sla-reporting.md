---
title: Relatórios de SLA
description: Saiba como visualizar o desempenho de seu ambiente de produção AEM em relação ao Contrato de nível de serviço (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Relatórios de SLA {#sla-reporting}

Saiba como visualizar o desempenho de seu ambiente de produção AEM em relação ao Contrato de nível de serviço (SLA).

## Introdução {#introduction}

Os dados de relatórios de SLA estão disponíveis para cada programa de produção por meio do **Relatórios** guia . Siga estas etapas para acessar o .

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Relatórios** na guia do **Visão geral** página.

1. Clique no ano desejado para ver os dados do SLA em gráfico.

![Exemplo de gráfico de SLA](assets/sla-reporting-1.png)

Passe o cursor sobre um ponto de dados para mostrar os valores específicos desse ponto.

![Exibição de dados detalhados](assets/sla-reporting-b.png)

## Métricas de SLA {#sla-metrics}

O gráfico do ano selecionado inclui vários conjuntos de dados.

* **Publicar Contrato de Camada** - Este é o SLA definido em seu contrato com o Adobe para o nível de publicação.

* **Publicar nível real** - Esse é o tempo de atividade medido dos incidentes de factoring de nível de publicação de produção causados por Adobe ou Adobe vendors.

* **Contrato de camada do autor** - Este é o SLA definido em seu contrato com o Adobe para a camada do autor.

* **Camada do autor real** - Esse é o tempo de funcionamento medido dos incidentes de factoring de camada do autor de produção causados por Adobe ou Adobe vendors.

## Análise de evento {#event-analysis}

O **Análise de evento** A seção do gráfico mostra o conjunto de incidentes que ocorreram para o programa durante o ano selecionado.

Cada um dos incidentes tem um intervalo de tempo, uma causa e um conjunto de comentários.

![Exemplo de análise de evento](assets/sla-reporting-c.png)
