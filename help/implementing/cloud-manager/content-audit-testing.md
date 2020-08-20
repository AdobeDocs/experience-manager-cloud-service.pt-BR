---
title: Teste de auditoria de conteúdo - Cloud Services
description: Teste de auditoria de conteúdo - Cloud Services
translation-type: tm+mt
source-git-commit: 4c4e0724185695279801c55db1b6874f351805a4
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Teste de auditoria de conteúdo {#content-audit-testing}

A auditoria de conteúdo é um recurso disponível nos pipelines de produção do Cloud Manager Sites, uma ferramenta de código aberto do Google. Esse recurso é ativado em todos os pipelines de produção do Cloud Manager.

Ele valida o processo de implantação e ajuda a garantir que as alterações implantadas:

1. Atenda aos padrões básicos de desempenho, acessibilidade, práticas recomendadas, SEO (Search Engine Otimization) e PWA (Progressive Web App).

1. Não inclua regressões nessas dimensões.

A auditoria de conteúdo no Cloud Manager garante que a experiência digital dos usuários finais no site seja mantida com os mais altos padrões. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.

## Como entender os resultados da auditoria de conteúdo {#understanding-content-audit-results}

A Auditoria de conteúdo fornece resultados de testes em nível de página e agregação por meio da página de execução do pipeline de produção.

* As métricas de nível de agregação medem a pontuação média nas páginas que foram auditadas.
* As pontuações de nível de página individuais também estão disponíveis por meio da busca detalhada.
* Detalhes das pontuações estão disponíveis para ver quais são os resultados dos testes individuais, juntamente com orientações sobre como corrigir quaisquer problemas identificados durante a auditoria de conteúdo.
* Um histórico dos resultados do teste é persistente no Cloud Manager para que os clientes possam ver se as alterações que estão sendo introduzidas na execução do pipeline incluem quaisquer regressões da execução anterior.

### Pontuações de agregação {#aggregate-scores}

Há uma pontuação de nível de agregação para cada tipo de teste (desempenho, acessibilidade, SEO, práticas recomendadas e PWA).

A pontuação do nível de agregação obtém a pontuação média das páginas que estão incluídas na execução. A alteração no nível da agregação representa a pontuação média das páginas na execução atual em comparação com a média das pontuações da execução anterior, mesmo se a coleção de páginas configuradas a serem incluídas tiver sido alterada entre as execuções.

O valor da métrica Alterar pode ser um dos seguintes:

* **Valor** positivo - as páginas melhoraram no teste selecionado desde a última execução do pipeline de produção

* **Valor** negativo - as páginas regrediram no teste selecionado desde a última execução do pipeline de produção

* **Sem alteração** - as páginas tiveram a mesma pontuação desde a última execução do pipeline de produção

* **N/D** - não havia pontuação anterior disponível para comparação

   ![](/help/implementing/developing/introduction/assets/content-audit-test1.png)

### Pontuações no nível da página {#page-level-scores}

Ao analisar qualquer um dos testes, é possível visualizar uma pontuação mais detalhada no nível da página. O usuário poderá ver a pontuação das páginas individuais do teste específico junto com a alteração da hora anterior em que o teste foi executado.

Clicar nos detalhes de qualquer página individual fornecerá informações sobre os elementos da página que foram avaliados e orientações para corrigir problemas se as oportunidades de aprimoramento forem detectadas. Os detalhes dos testes e as orientações associadas são fornecidos pelo Google Lighthouse.

![](/help/implementing/developing/introduction/assets/page-level-scores.png)

