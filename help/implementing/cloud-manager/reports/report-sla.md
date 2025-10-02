---
title: Relatórios de SLA
description: Saiba como ver o desempenho do seu ambiente de produção do AEM em relação ao Service level agreement contratado.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 11%

---


# Relatórios do SLA {#sla-reporting}

Saiba como ver o desempenho do seu ambiente de produção do AEM em relação ao SLA (Service level agreement) contratado.

## Exibir um relatório do SLA {#introduction}

Os dados de relatório do SLA acompanham as métricas de desempenho de dois níveis de produção: Nível de criação e Nível de publicação.

O gráfico de linhas de um ano selecionado inclui pontos de dados para cada mês de janeiro a dezembro. As métricas a seguir são rastreadas.

| Métrica rastreada | Cor da linha | Descrição |
| --- | --- | --- |
| Camada do autor real | Verde claro | O tempo de atividade medido na camada de autor de produção depois de deduzidos os incidentes causados pela Adobe ou pelos fornecedores da Adobe. |
| Contrato da camada do autor | Azul escuro | A SLA definida em seu contrato com a Adobe para a camada Autor. |
| Publicar camada real | Laranja | O tempo de atividade medido no nível de publicação de produção, considerando incidentes causados pela Adobe ou pelos fornecedores da Adobe. |
| Publicar camada de contrato | Vermelho | O SLA definido em seu contrato com a Adobe para a camada de publicação. |

**Para exibir um relatório do SLA:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Na página **Visão geral do programa**, no menu do lado esquerdo, clique em **Relatórios**.

1. Clique em **Relatórios do SLA**.

   ![Gráfico de linhas de relatório do SLA](/help/implementing/cloud-manager/reports/assets/cm-sla-report2.png)

1. Clique no ano desejado para ver um gráfico de linhas de dados do SLA.

1. (Opcional) Siga qualquer um destes procedimentos:

   * Passe o cursor sobre um ponto de dados no gráfico de linhas para mostrar os valores específicos desse ponto.
   * Abaixo do ano do gráfico de linhas, clique no ícone **Baixar** para salvar um arquivo de imagem PNG do gráfico de linhas.
   * Clique em um nome de métrica para ver apenas os dados dessa métrica. Ou pressione `Shift` no teclado ao selecionar ou desmarcar um ou mais nomes de métrica.

## Análise de eventos {#event-analysis}

A seção **Análise de Eventos** no gráfico mostra o conjunto de incidentes que ocorreram para o programa durante o ano selecionado.

Cada um dos incidentes tem um intervalo de tempo, uma causa e um conjunto de comentários.

![Exemplo de análise de eventos](/help/implementing/cloud-manager/reports/assets/sla-reporting-c.png)

## Atualizar intervalo de relatórios do SLA {#refresh}

Os relatórios do SLA fornecem o insight para o desempenho de seu ambiente de produção do AEM e são atualizados, mas não instantâneos. A geração de relatórios do SLA acontece mensalmente e é gerada para novos programas marcados como `Production previous month`. Não é instantâneo. Devido a esse atraso, lembre-se do seguinte ao revisar seu relatório do SLA:

* O SLA relatado é aquele que existia no início do mês, mesmo se o SLA mudou durante esse mês.
* Se não havia SLA no início do mês porque o programa não existia, a SLA existente na data em que o programa foi criado se aplica.

## Visualizar ambientes {#preview}

O ambiente de visualização é uma ferramenta para que os autores de conteúdo verifiquem a experiência final do conteúdo antes da publicação. Devido a essa funcionalidade, os ambientes de visualização não foram projetados com alta disponibilidade e não têm um SLA associado.

