---
title: Teste de auditoria de experiência
description: Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 90%

---


# Teste de auditoria de experiência {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Teste de auditoria de experiência"
>abstract="Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO."

Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO.

## Visão geral {#overview}

A Auditoria de experiência é um recurso disponível nos pipelines de produção de Sites do Cloud Manager que valida o processo de implantação e ajuda a garantir que as alterações sejam implantadas:

1. Atenda aos padrões básicos de desempenho, acessibilidade, práticas recomendadas, SEO (otimização do mecanismo de pesquisa) e PWA (Aplicativo Web Progressivo).

1. Não introduza regressões.

A Auditoria de experiência no Cloud Manager garante que a experiência do usuário no site seja do mais alto padrão.

Os resultados da auditoria são informativos e permitem que o gerente de implantação veja as pontuações e as alterações entre as pontuações atual e anterior. Essa informação é valiosa para determinar se foi introduzida uma regressão com a implantação atual.

A auditoria de experiência é disponibilizada pelo Google Lighthouse, uma ferramenta de código aberto do Google, e é habilitada em todos os pipelines de produção do Cloud Manager.

>[!INFO]
>
>A partir de 31 de agosto de 2023, a Auditoria de experiência fará a transição para mostrar resultados específicos da plataforma móvel. Observe que as métricas de desempenho móvel normalmente se registram abaixo do desktop, portanto, você deve antecipar uma mudança no desempenho relatado após essa alteração.

>[!TIP]
>
>Você define quais páginas são incluídas na auditoria de experiência ao [configurar seu pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).

## Noções básicas sobre os resultados da auditoria de experiência {#understanding-experience-audit-results}

A auditoria de experiência fornece resultados de teste agregados e detalhados em nível de página por meio da [página de execução do pipeline de produção](/help/implementing/cloud-manager/deploy-code.md).

* Métricas agregadas medem as pontuações médias nas páginas que foram auditadas quanto a desempenho, acessibilidade, práticas recomendadas, SEO (otimização do mecanismo de pesquisa).
* As pontuações em nível de página individual também estão disponíveis por meio de detalhamento.
* Detalhes das pontuações estão disponíveis para visualizar os resultados dos testes individuais, juntamente com orientações sobre como corrigir os problemas identificados.
* Um histórico dos resultados de teste é mantido no Cloud Manager para determinar se as alterações introduzidas pelo pipeline incluem qualquer regressão em relação à execução anterior.

### Pontuações agregadas {#aggregate-scores}

A pontuação em nível agregado considera a pontuação média das páginas incluídas na execução. A alteração em nível agregado representa a pontuação média das páginas na execução atual em comparação à média das pontuações da execução anterior, mesmo se a coleção de páginas configuradas para serem incluídas tiver sido alterada entre as execuções.

Há uma pontuação em nível agregado para cada tipo de teste, como desempenho, acessibilidade, SEO e práticas recomendadas.

A métrica de alteração pode ter um dos valores a seguir.

* **Valor positivo** - As páginas foram aprimoradas no teste selecionado desde a última execução do pipeline de produção.

* **Valor negativo** - as páginas regressaram no teste selecionado desde a última execução do pipeline de produção.

* **Sem alteração** - As páginas tiveram a mesma pontuação da última execução do pipeline de produção.

* **N/D** - Não havia pontuação anterior disponível para comparação.

![Resultados da auditoria de experiência](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Pontuações em nível de página {#page-level-scores}

Ao examinar qualquer um dos testes, uma pontuação em nível de página mais detalhada está disponível. Você pode ver as pontuações de páginas individuais para um teste específico, juntamente com a alteração em relação à execução anterior do teste.

Clicar nos detalhes de qualquer página individual fornece informações sobre os elementos da página que foram avaliados, bem como orientação para corrigir problemas se forem detectadas oportunidades de melhoria.

![Pontuações em nível de página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
