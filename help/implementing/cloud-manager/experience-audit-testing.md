---
title: Teste de auditoria de experiência
description: Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 1a7a9ee78d09a9360922a63dfa315ef9d106209e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# Teste de auditoria de experiência {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Teste de auditoria de experiência"
>abstract="Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO."

Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO.

## Visão geral {#overview}

A Auditoria de experiência é um recurso disponível nos pipelines de produção de sites do Cloud Manager que valida o processo de implantação e ajuda a garantir que as alterações sejam implantadas:

1. Atenda aos padrões básicos de desempenho, acessibilidade, práticas recomendadas, SEO (Search Engine Otimization) e PWA (Progressive Web App).

1. Não introduza regressões.

A Auditoria de experiência no Cloud Manager garante que a experiência do usuário final no site seja dos mais altos padrões.

Os resultados da auditoria são informativos e permitem que o gerente de implantação veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.

A Auditoria de experiência é disponibilizada pelo Google Lighthouse, uma ferramenta de código aberto da Google, e é ativada em todos os pipelines de produção do Cloud Manager.

## Noções básicas dos resultados da auditoria de experiência {#understanding-experience-audit-results}

A Auditoria de experiência fornece resultados de teste agregados e detalhados em nível de página por meio da [página de execução do pipeline de produção.](/help/implementing/cloud-manager/deploy-code.md)

* Métricas agregadas medem as pontuações médias nas páginas que foram auditadas para desempenho, acessibilidade, práticas recomendadas, SEO (Otimização do mecanismo de pesquisa).
* As pontuações de nível de página individual também estão disponíveis por meio do detalhamento.
* Detalhes das pontuações estão disponíveis para visualizar os resultados dos testes individuais, juntamente com orientações sobre como corrigir quaisquer problemas identificados.
* Um histórico dos resultados do teste é mantido no Cloud Manager para determinar se as alterações que estão sendo introduzidas no pipeline incluem qualquer regressão da execução anterior.

### Pontuações agregadas {#aggregate-scores}

A pontuação de nível agregado obtém a pontuação média das páginas incluídas na execução. A alteração no nível de agregação representa a pontuação média das páginas na execução atual em comparação à média das pontuações da execução anterior, mesmo se a coleção de páginas configuradas para serem incluídas tiver sido alterada entre as execuções.

Há uma pontuação de nível agregado para cada tipo de teste, como desempenho, acessibilidade, SEO e práticas recomendadas.

A métrica de alteração pode ter um dos valores a seguir.

* **Valor positivo** - As páginas foram aprimoradas no teste selecionado desde a última execução do pipeline de produção.

* **Valor negativo** - a(s) página(s) regressou(ão) ao teste selecionado desde a última execução do pipeline de produção.

* **Sem alteração** - As páginas tiveram a mesma pontuação desde a última execução do pipeline de produção.

* **N/D** - Não havia pontuação anterior disponível para comparação.

![Resultados da auditoria de experiência](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Pontuações no nível da página {#page-level-scores}

Ao detalhar qualquer um dos testes, a pontuação de nível de página mais detalhada está disponível. Você pode ver como as páginas individuais foram pontuadas para o teste específico junto com a alteração da execução do teste anterior.

Clicar nos detalhes de qualquer página individual fornece informações sobre os elementos da página que foram avaliados, bem como orientação para corrigir problemas se forem detectadas oportunidades de melhoria.

![Pontuações no nível da página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
