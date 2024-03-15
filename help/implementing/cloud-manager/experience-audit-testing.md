---
title: Teste de auditoria de experiência
description: Saiba como a Auditoria de experiência valida seu processo de implantação e ajuda a garantir que as alterações implantadas atendam aos padrões básicos de desempenho, acessibilidade, práticas recomendadas e SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 56%

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

A Auditoria de experiência é disponibilizada pelo Google Lighthouse, uma ferramenta de código aberto da Google.

>[!INFO]
>
>A partir de 31 de agosto de 2023, a Auditoria de experiência fará a transição para mostrar resultados específicos da plataforma móvel. As métricas de desempenho móvel normalmente se registram abaixo do desktop, portanto, você deve antecipar uma mudança no desempenho relatado após essa alteração.

## Disponibilidade {#availability}

A Auditoria de experiência está disponível para o Cloud Manager:

* Pipelines de produção de sites, por padrão.
* Pipelines de desenvolvimento front-end, opcionalmente.

Consulte a [seção Configuração](#configuration) para obter mais informações sobre como configurar a auditoria para os ambientes opcionais.

## Configuração {#configuration}

A Auditoria de experiência está disponível por padrão para pipelines de produção. Ele pode ser ativado opcionalmente para pipelines de desenvolvimento de front-end. Em todos os casos, é necessário definir quais caminhos de conteúdo são avaliados durante a execução do pipeline.

Você configura quais páginas são incluídas na Auditoria de experiência quando configura o pipeline.

1. Dependendo do tipo de pipeline que você deseja configurar, siga as instruções para:

   * Adicionar um novo [pipeline de produção,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) se desejar definir os caminhos que serão avaliados pela auditoria.
   * Adicionar um novo [pipeline de não produção,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) se quiser ativar a auditoria em um pipeline de front-end ou de pilha completa de desenvolvimento.
   * Ou você pode [editar um pipeline existente,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) e atualize as opções existentes.

1. Se você estiver adicionando ou editando um pipeline de não produção para o qual deseja usar a Auditoria de experiência, é necessário selecionar o **Auditoria de experiência** caixa de seleção na **Código-fonte** guia.

   ![Ativar a Auditoria de experiência](assets/experience-audit-enable.jpg)

   * Isso só é necessário para pipelines de não produção.
   * A variável **Auditoria de experiência** é exibida quando a caixa de seleção é marcada.

1. Para pipelines de produção e não produção, você define os caminhos que devem ser incluídos na Auditoria de experiência no **Auditoria de experiência** guia.

   * Os caminhos da página devem começar com `/` e são relativos ao seu site.
   * Por exemplo, se o site for `wknd.site` e gostaria de incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html`.

   ![Definição de um caminho para a Auditoria de experiência](assets/experience-audit-add-page.png)

1. Toque ou clique **Adicionar página** e o caminho é preenchido automaticamente com o endereço do ambiente e adicionado à tabela de caminhos.

   ![Caminho salvo na tabela](assets/experience-audit-page-added.png)

1. Continue a adicionar caminhos, conforme necessário, repetindo as duas etapas anteriores.

   * É possível adicionar no máximo 25 caminhos.
   * Se você não definir nenhum caminho, a página inicial do site será incluída na Auditoria de experiência por padrão.

1. Clique em **Salvar** para salvar o pipeline.

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

* **Sem alterações** - As páginas tiveram a mesma pontuação da última execução do pipeline de produção.

* **N/D** - Não havia pontuação anterior disponível para comparação.

![Resultados da auditoria de experiência](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Pontuações em nível de página {#page-level-scores}

Ao examinar qualquer um dos testes, uma pontuação em nível de página mais detalhada está disponível. Você pode ver as pontuações de páginas individuais para um teste específico, juntamente com a alteração em relação à execução anterior do teste.

Clicar nos detalhes de qualquer página individual fornece informações sobre os elementos da página que foram avaliados, bem como orientação para corrigir problemas se forem detectadas oportunidades de melhoria.

![Pontuações em nível de página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
