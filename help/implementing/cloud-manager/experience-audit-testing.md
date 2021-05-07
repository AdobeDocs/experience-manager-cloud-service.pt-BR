---
title: Teste de auditoria de experiência - Cloud Services
description: Teste de auditoria de experiência - Cloud Services
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Teste de auditoria de experiência {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Teste de auditoria de experiência"
>abstract="A Auditoria de experiência é um recurso disponível em pipelines de produção de sites do Cloud Manager, desenvolvido pelo Google Lighthouse, uma ferramenta de código aberto do Google. Esse recurso é ativado em todos os pipelines de produção do Cloud Manager."

A Auditoria de experiência é um recurso disponível em pipelines de produção de sites do Cloud Manager, desenvolvido pelo Google Lighthouse, uma ferramenta de código aberto do Google. Esse recurso é ativado em todos os pipelines de produção do Cloud Manager.

Ele valida o processo de implantação e ajuda a garantir que as alterações sejam implantadas:

1. Atenda aos padrões básicos de desempenho, acessibilidade, práticas recomendadas, SEO (Search Engine Otimization) e PWA (Progressive Web App).

1. Não inclua regressões nessas dimensões.

A Auditoria de experiência no Cloud Manager garante que a experiência digital dos usuários finais no site possa ser mantida nos mais altos padrões. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.

## Como entender os resultados da auditoria de experiência {#understanding-experience-audit-results}

A Auditoria de experiência fornece resultados de teste agregados e detalhados em nível de página por meio da página de execução do pipeline de produção .

* Métricas de nível agregado medem a pontuação média nas páginas que foram auditadas para desempenho, acessibilidade, práticas recomendadas, SEO (Otimização do mecanismo de pesquisa).
   >[!NOTE]
   >A pontuação do Progressive Web App (PWA) não está incluída na pontuação do resumo e será exibida somente na tela de detalhes do relatório no nível da página.
* As pontuações de nível de página individual também estão disponíveis por meio do detalhamento.
* Os detalhes das pontuações estão disponíveis para ver quais são os resultados dos testes individuais, juntamente com orientações sobre como corrigir quaisquer problemas identificados durante a auditoria da experiência.
* Um histórico dos resultados do teste é mantido no Cloud Manager para que os clientes possam ver se as alterações que estão sendo introduzidas na execução do pipeline incluem qualquer regressão da execução anterior.

### Pontuações agregadas {#aggregate-scores}

Há uma pontuação de nível agregado para cada tipo de teste, como desempenho, acessibilidade, SEO e práticas recomendadas.
>[!NOTE]
>A pontuação do Progressive Web App (PWA) não está incluída na pontuação do resumo e será exibida somente na tela de detalhes do relatório no nível da página.

A pontuação de nível agregado obtém a pontuação média das páginas incluídas na execução. A alteração no nível de agregação representa a pontuação média das páginas na execução atual em comparação à média das pontuações da execução anterior, mesmo se a coleção de páginas configuradas para serem incluídas tiver sido alterada entre as execuções.

O valor da métrica Change pode ser um dos seguintes:

* **Valor positivo**  - as páginas foram aprimoradas no teste selecionado desde a última execução do pipeline de produção

* **Valor negativo**  - as páginas foram regressadas no teste selecionado desde a última execução do pipeline de produção

* **Sem alterações**  - as páginas tiveram a mesma pontuação desde a última execução do pipeline de produção

* **N/A**  - não havia pontuação anterior disponível para comparação a

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Pontuações no nível da página {#page-level-scores}

Ao detalhar qualquer um dos testes, é possível visualizar uma pontuação mais detalhada no nível da página. O usuário poderá ver a pontuação de páginas individuais para o teste específico junto com a alteração da hora anterior em que o teste foi executado.

Clicar nos detalhes de qualquer página individual fornecerá informações sobre os elementos da página que foram avaliados e orientação para corrigir problemas se forem detectadas oportunidades de melhoria. Os detalhes dos testes e as orientações associadas são fornecidos pelo Google Lighthouse.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
