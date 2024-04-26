---
title: Relatórios de SLA
description: Saiba como visualizar o desempenho do seu ambiente de produção do AEM em relação ao acordo de nível de serviço (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: a0f80a363cb47be9e3d8f7fa96ea3068eb077d42
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 52%

---


# Relatórios de SLA {#sla-reporting}

Saiba como visualizar o desempenho do seu ambiente de produção do AEM em relação ao acordo de nível de serviço (SLA).

## Introdução {#introduction}

Os dados de relatórios de SLA estão disponíveis para cada programa de produção por meio da guia **Relatórios**. Siga estas etapas para acessar.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)** selecione o programa.

1. Usando o painel de navegação lateral, navegue até o **Relatórios** na guia **Visão geral** página.

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

## Intervalo de atualização {#refresh}

Os relatórios de SLA fornecem informações sobre o desempenho do ambiente de produção de AEM e estão atualizados, mas não são instantâneos. A geração de relatórios de SLA acontece mensalmente e é gerada para novos programas marcados como Produção no mês anterior. Não é instantâneo. Devido a esse atraso, lembre-se do seguinte ao revisar seu relatório de SLA:

* O SLA relatado será aquele que existia no início do mês, mesmo se o SLA tiver mudado durante esse mês.
* Se não houver SLA no início do mês porque o programa não existia, será aplicado o SLA existente na data em que o programa foi criado.

## Visualizar ambientes {#preview}

O ambiente de visualização é uma ferramenta para que os autores de conteúdo verifiquem a experiência final do conteúdo antes da publicação. Por causa disso, os ambientes de visualização não foram projetados com alta disponibilidade e não têm um SLA associado.
