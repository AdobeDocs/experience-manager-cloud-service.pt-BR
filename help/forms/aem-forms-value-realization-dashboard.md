---
title: Painel de realização de valor do AEM Forms
description: Monitore facilmente os envios de formulários em suas instâncias do AEM Forms com nosso painel de rastreamento intuitivo.
feature: Adaptive Forms, Foundation Components, Core Components
role: Admin, Developer, Leader, User
hide: true
hidefromtoc: true
source-git-commit: 613adeee805069155881b1a26b247c3dec3eb593
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 22%

---


# Painel de avaliação de valor: Aproveitar ao máximo o seu Forms {#value-realization-dashboard}

Bem-vindo ao seu balcão único para entender o valor que seus formulários estão trazendo! Esse painel fornece insights valiosos para otimizar seus formulários, simplificar fluxos de trabalho e, por fim, atingir suas metas mais rapidamente.

## O que há no painel? {#content-of-dashboard}

Esse painel é a sua janela para o mundo de uso do formulário. Veja a seguir um detalhamento das principais seções:

### Atividade do formulário ao longo do tempo:

* **Envio de formulários**: veja as tendências na frequência com que seus formulários estão sendo preenchidos.
* **Representações do documento**: controle o número de documentos renderizados ao longo do tempo.
* **Forms criado e publicado**: monitore a taxa na qual novos formulários estão sendo criados e implantados.
* **Tempos de criação e publicação do formulário**: Analise os tempos médios de criação e publicação de formulários para identificar áreas para aprimoramento.

### Uso do fragmento:

* **Número de fragmentos de formulário em uso**: veja quantas seções de formulário reutilizáveis estão atualmente incorporadas em formulários ativos.
* **Número de reutilização de fragmentos de formulário**: meça a frequência com que esses fragmentos são usados em diferentes formulários.


## Como Isso Beneficia Você? {#benefits-to-you}

Esse painel permite que você tome decisões orientadas por dados sobre seus formulários. Veja como:

* **Identificar Forms populares**: altas taxas de envio indicam formulários valiosos. Analise esses itens para obter práticas recomendadas que possam ser replicadas em outros.
* **Otimizar a criação de formulários**: reduza os tempos de criação identificando gargalos. Explore modelos pré-criados ou workflows otimizados.
* **Aumentar reutilização do fragmento**: Incentive a colaboração e a capacidade de descoberta de fragmentos reutilizáveis. Bibliotecas de fragmentos bem organizadas podem melhorar significativamente a eficiência.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Rastreador de envios de formulários"
>abstract="Este gráfico representa a contagem de envios de formulários adaptáveis durante períodos específicos. O aumento dos envios pode indicar que o formulário está se tornando mais popular ou que é necessário coletar mais dados dos usuários. **Nota:** O gráfico fornece dados específicos para a instância atual, permitindo analisar tendências rapidamente e tomar decisões informadas. Para encontrar dados de envios de outras instâncias, basta acessar o painel de cada respectiva instância."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Rastreador de representações do documento"
>abstract="Este gráfico representa a contagem de representações de documentos durante períodos específicos. **Nota:** O gráfico fornece dados específicos para a instância atual, permitindo analisar tendências rapidamente e tomar decisões informadas. Para encontrar dados de envios de outras instâncias, basta acessar o painel de cada respectiva instância."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Novo rastreador de formulários"
>abstract="O gráfico fornece informações sobre o número de formulários recém-criados durante períodos específicos. **Nota:** O gráfico fornece dados específicos para a instância atual do autor do AEM Forms. Para exibir dados de outras instâncias, acesse o painel de cada respectiva instância."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Rastreador de formulários publicados"
>abstract="O gráfico fornece informações sobre o número de formulários publicados com êxito durante períodos específicos. **Nota:** O gráfico fornece dados específicos para a instância de publicação atual do AEM Forms. Para exibir dados de conversão de outras instâncias, acesse o painel de cada respectiva instância."


## Transformando insights em ação {#turning-insights-into-actions}

Vamos traduzir esses resultados em etapas acionáveis!

* **Poucos envios?** Investigue a clareza e a facilidade de uso do formulário. É muito longo ou tem perguntas confusas? Considere revisar para obter uma melhor experiência do usuário.
* **Altos tempos de criação?** Analise o processo de criação. Há etapas ou recursos desnecessários que não estão sendo usados com eficiência? Utilize recursos que economizam tempo, como modelos.
* **Fragmentos subutilizados?** Garantir que os fragmentos sejam bem organizados, pesquisáveis e fáceis de entender. Considere promover o uso de fragmentos em sua equipe.

Ao analisar essas tendências, você pode criar formulários melhores, economizar tempo na criação e aproveitar componentes reutilizáveis. Isso se traduz em um fluxo de trabalho mais suave, usuários mais satisfeitos e, em última análise, um maior retorno sobre seu investimento.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Duração média para geração de formulário"
>abstract="O gráfico ilustra o tempo médio necessário para criar um formulário. Cada barra no gráfico representa um formulário específico, e a altura da barra indica a duração média de sua criação durante esse intervalo de tempo."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Duração média da criação de formulário"
>abstract="O gráfico exibe o tempo médio necessário para criar e publicar um formulário, medido a partir do dia inicial em que o formulário foi aberto para edição. **Nota:** O gráfico fornece dados específicos para a instância atual do autor do AEM Forms. Para exibir dados de outras instâncias, acesse o painel de cada respectiva instância."


>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Rastreador de fragmentos do Forms"
>abstract="Este gráfico ajuda a visualizar quantos fragmentos de formulário você está usando em seus formulários. **Nota:** O gráfico fornece dados específicos para a instância de publicação atual do AEM Forms. Para exibir dados de conversão de outras instâncias, acesse o painel de cada respectiva instância."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Rastreador de tempo médio do fragmento de formulário"
>abstract="O gráfico exibe o tempo médio necessário para criar um fragmento de formulário, medido a partir do dia inicial em que o fragmento de formulário foi aberto para edição. **Nota:** O gráfico fornece dados específicos para a instância de publicação atual do AEM Forms. Para exibir dados de conversão de outras instâncias, acesse o painel de cada respectiva instância."


## Dicas adicionais {#additional-tips}

* **Estabeleça metas:** Determine o que você deseja alcançar com seus formulários. É maior coleta de dados, geração mais rápida de leads ou melhor satisfação do cliente? Conhecer suas metas orientará sua análise do painel.
* **Revisão regular:** Agende check-ins regulares com o painel para rastrear o progresso e identificar novas áreas a serem aprimoradas.
* **Experimento e refinamento:** Não tenha medo de experimentar com diferentes designs de formulário e uso de fragmento. O painel ajudará você a medir a eficácia das alterações.

Lembre-se, este painel é seu aliado! Ao utilizá-lo com eficiência, você pode transformar seus formulários de ferramentas simples de coleta de dados em ativos estratégicos que impulsionam o sucesso para você e sua empresa.
