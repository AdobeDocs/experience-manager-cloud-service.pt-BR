---
title: Usar o painel de realização de valor para analisar tendências de uso de formulários e documentos
description: Saiba como usar o painel de insights de uso do Forms para monitorar e entender o desempenho de seus formulários e fragmentos de formulário.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components, Core Components
hide: true
hidefromtoc: true
source-git-commit: ef6c113721ca6f84374ecd01df790a0b37d00192
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---


# Usar o painel de realização de valor para analisar tendências de uso de formulários e documentos

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para aem-forms-ea@adobe.com. <span>

![Painel de realização de valor](/help/edge/docs/forms/universal-editor/assets/forms-insights-banner.svg)


Monitorando regularmente as métricas apresentadas no painel &quot;Insights de uso do Forms&quot;, você pode obter insights valiosos sobre o desempenho de formulários, documentos e fragmentos de formulário. Use esses dados para tomar decisões informadas sobre o design do formulário, o gerenciamento de fragmentos e a estratégia geral do formulário.

Este artigo fornece instruções de uso detalhadas e interpretação de métricas para o Painel de avaliação. Para obter uma visão geral conceitual e os benefícios do painel, consulte [entendendo seu painel de realização de valor](/help/forms/aem-forms-value-realization-dashboard.md).


## Acesso ao painel de insights de uso

Para acessar o painel de Insights de uso do Forms:

1. Navegue até **Forms** > **Forms e Documentos**
1. Clique em **Painel de Insights**. O painel é aberto em uma nova janela.

   ![Painel de realização de valor](/help/forms/assets/forms-usage-insights.png)

## Visão geral

O painel consiste em duas seções principais:

- **Atividade de formulários e documentos ao longo do tempo:** esta seção fornece informações sobre o uso e a evolução de seus formulários durante um período selecionado.
- **Uso de fragmentos:** esta seção permite monitorar a adoção e a reutilização de fragmentos de formulário.

## Atividade de formulários e documentos ao longo do tempo

Esta seção contém quatro gráficos, cada um rastreando um aspecto diferente da atividade do formulário. Todos os gráficos compartilham a mesma estrutura:

- **Tipo de Gráfico:** Gráfico de Linhas e Gráfico de Barras
- **Eixo X:** Data (mostrando atividade diária)
- **Eixo Y:** Contagem (representando o número de ocorrências da atividade rastreada)
- **Período:** Ajustável por meio de um menu suspenso (opções: &quot;Últimos 30 dias&quot;, &quot;Últimos 12 meses&quot;)




### Envios de formulários

- **Propósito:** este gráfico exibe o número de vezes que os formulários foram enviados com êxito durante o período selecionado.

  ![Gráfico de Envios do Forms](/help/forms/assets/forms-submissions-vr-dashboard-form-insights.png)
- **Informações a serem extraídas:**
   - **Análise de tendência:** observe a tendência geral dos envios de formulários. O número está aumentando, diminuindo ou permanecendo relativamente constante?
   - **Períodos de Pico:** Identifique dias ou períodos com taxas de envio excepcionalmente altas. Investigue os possíveis motivos para esses picos (por exemplo, campanhas de marketing, eventos específicos).
   - **Períodos de Baixa Atividade:** Identifique períodos com baixas taxas de envio e investigue as possíveis causas (por exemplo, tempo de inatividade do formulário, problemas de usabilidade).
   - **Análise Comparativa**: compare as taxas de envio em diferentes períodos de tempo (por exemplo, os últimos 30 dias com os 30 dias anteriores) para avaliar as alterações de desempenho.

### Representações do documento

- **Propósito:** este gráfico rastreia o número de documentos gerados como resultado de envios de formulários. Isso é relevante se seus formulários acionarem a criação de documentos (por exemplo, contratos, relatórios).

  ![Gráfico de representações de documentos](/help/forms/assets/document-rendetions-vr-dashboard-form-insights.png)


- **Informações a serem extraídas:**
   - **Correlação com os envios de formulários:** compare a tendência das representações de documentos com a tendência dos envios de formulários. Idealmente, eles devem estar intimamente correlacionados. Discrepâncias podem indicar problemas com o processo de geração de documentos.
   - **Volume de Geração de Documentos:** Avalie o volume geral de documentos que estão sendo gerados para entender a carga de trabalho em seu sistema de geração de documentos.

### Formulários criados


- **Propósito:** este gráfico exibe o número de novos formulários criados dentro do período selecionado.

  ![Gráfico criado pelo Forms](/help/forms/assets/forms-created-vr-dashboard-form-insights.png)

- **Informações a serem extraídas:**
   - **Taxa de Criação de Formulários:** Rastreie a taxa de criação de novos formulários. Isso fornece insights sobre a demanda por novos formulários na organização.
   - **Picos na Criação:** Identifique períodos com atividade de criação de formulário excepcionalmente alta. Isso pode indicar projetos ou iniciativas específicos que exigem novos formulários.

### Forms publicado

- **Propósito:** este gráfico rastreia o número de formulários publicados (disponibilizados para uso) no período selecionado.

  ![Gráfico publicado pelo Forms](/help/forms/assets/forms-publish-vr-dashboard-form-insights.png)


- **Informações a serem extraídas:**
   - **Taxa de Implantação de Formulário:** Monitore a taxa na qual novos formulários estão sendo implantados para usuários.
   - **Atraso entre a Criação e a Publicação:** analise a diferença de tempo entre o gráfico &quot;Forms Criado&quot; e o gráfico &quot;Forms Publicado&quot;. Um atraso significativo pode indicar gargalos no processo de aprovação ou implantação do formulário.

## Uso do fragmento

Esta seção fornece insights sobre o uso de fragmentos de formulário, que são componentes reutilizáveis que podem ser incorporados a vários formulários.

![Gráfico publicado pelo Forms](/help/forms/assets/fragment-usage-vr-dashboard-form-insights.png)

### Número de fragmentos de formulário em uso

- **Tipo de Gráfico:** Exibição Numérica (mostrando um único valor)
- **Propósito:** exibe o número total de fragmentos de formulário exclusivos que estão sendo usados atualmente em formulários ativos.
- **Informações a serem extraídas:**
   - **Adoção de fragmentos:** Avalie a adoção geral de fragmentos de formulário na organização. Um número maior indica maior uso de componentes reutilizáveis.

### Reutilização de fragmento de formulário

- **Tipo de Gráfico:** Exibição Numérica (mostrando um único valor)
- **Propósito:** exibe o número total de vezes que fragmentos de formulário foram reutilizados em diferentes formulários. Essa métrica indica com que eficiência os fragmentos estão sendo aproveitados para evitar duplicação e manter a consistência.
- **Informações a serem extraídas:**
   - **Taxa de Reutilização de Fragmento:** Monitore a taxa na qual os fragmentos existentes estão sendo reutilizados em novos formulários. Um número maior indica melhor aproveitamento de componentes reutilizáveis e maior eficiência.

## Exemplos de cenários

- **Cenário:** você percebe uma queda repentina em &quot;Envios de formulário&quot;.
   - **Ação:** investigue as possíveis causas, como tempo de inatividade do formulário, problemas de usabilidade ou um declínio no tráfego para a página de aterrissagem do formulário.
- **Cenário:** o valor de &quot;Reutilização de Fragmento de Formulário&quot; está baixo.
   - **Ação:** promova os benefícios de usar fragmentos de formulário para a sua equipe, verifique se os fragmentos estão bem organizados e fáceis de localizar e forneça treinamento sobre como criar e reutilizar fragmentos de maneira eficaz.
- **Cenário:** há um atraso significativo entre &quot;Forms Criado&quot; e &quot;Forms Publicado&quot;.
   - **Ação:** revise a aprovação do formulário e o processo de implantação para identificar e eliminar gargalos.



## Consulte também:

- [Noções básicas sobre o seu painel de realização de valor](/help/forms/aem-forms-value-realization-dashboard.md)