---
title: Experimentação contextual no AEM as a Cloud Service
description: Saiba como usar o painel de experimentação para adicionar recursos de experimentação ao site.
feature: Administering
role: Admin
source-git-commit: c948abf5391e61f01912f769b17e1ac0bd81a745
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 0%

---

# Experimentação contextual no AEM as a Cloud Service {#contextual-experimentation}

A experimentação é a prática de testar o design, a funcionalidade e o código do site para melhorar o desempenho e tornar seu site mais eficaz e simplificado. Isso é feito alterando o conteúdo ou a funcionalidade, comparando os resultados com uma versão anterior e escolhendo as melhorias que têm efeitos mensuráveis.

Quando feito corretamente, é um padrão avançado para melhorar as conversões, o envolvimento e a experiência do visitante. Em geral, há alguns problemas a serem evitados ao tentar adotar a prática:

* **Muito pouco**: a maioria das empresas não está experimentando o suficiente e, quando o fazem, fazem experimentos com muito pouco tráfego para obter resultados significativos.
* **Muito lento**: muitas estruturas de experimentação tornam o site tão lento que novas conversões em potencial não podem compensar o tráfego perdido e rejeições devido à renderização lenta.
* **Muito complexo**: se levar muito tempo para configurar um novo experimento, menos experimentos serão executados.

Para sites executados no Adobe Experience Manager, os desenvolvedores têm a opção de adicionar um novo recurso de experimentação a seus sites. Três coisas tornam essa abordagem diferente de outras estruturas de experimentação:

* É fácil configurar testes com as ferramentas que seus autores já conhecem e nenhum logon separado é necessário.
* Ele é profundamente integrado ao sistema de entrega do AEM, não atrasa o site e é resiliente a alterações no código e no conteúdo.
* Ele permite testar alterações simples de conteúdo, bem como experimentos que abrangem design, funcionalidade e código.

## Trilho de experimentação {#experimentation-rail}

O painel de experimentação é a principal maneira de configurar experimentos. Ele pode ser usado com o seu projeto em um contexto do [Edge Delivery Services](/help/edge/overview.md) ou no [Editor Universal](/help/implementing/universal-editor/introduction.md). Dessa forma, você precisará de uma conta Github, um repositório de conteúdo como o SharePoint ou o Google Drive, e também do plug-in [AEM Sidekick](https://www.aem.live/docs/sidekick). Se você quiser usar o editor universal, também precisará acessar um [ambiente do AEM as a Cloud Service](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Consulte também a [página Introdução - Tutorial do desenvolvedor do Universal Editor](https://www.aem.live/developer/tutorial).

>[!WARNING]
>O mecanismo de experimentação é necessário para usar o recurso de experimentação. Verifique se o mecanismo está instalado e atualizado corretamente antes de implementar as etapas abaixo. Consulte a [página de instalação](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation) a seguir para obter mais detalhes.

### Configuração de experimentação usando o AEM Sidekick no Edge Delivery Services

Para acessar os recursos do painel de experimentação em seu Projeto do Edge Delivery Services, você precisará do plug-in [AEM Sidekick](https://www.aem.live/docs/sidekick). Para configurar o sidekick, siga estas etapas:

1. Adicione a [extensão do AEM sidekick](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar) e fixe-a no navegador.
1. Abra a página do projeto no modo de visualização.
1. Na barra do AEM Sidekick, clique no ícone de configurações ![Configurações](/help/sites-cloud/administering/assets/settings-1.png) e selecione **Adicionar este projeto**.
1. Clique na guia Experimentação para abrir o painel de experimentação.

### Configuração de experimentação no editor universal

Antes de configurar experimentos, lembre-se de que você precisará usar os sites do AEM como uma fonte de conteúdo para poder criar no Universal Editor. Se necessário, você pode converter seu projeto existente em sites do AEM como uma fonte de conteúdo seguindo o tutorial apresentado na página [Configurar o AEM Sites como um Source de Conteúdo](https://www.aem.live/developer/ue-tutorial). Quando estiver pronto para configurar experimentos no Universal Editor, siga estas etapas:

1. Abra o projeto no Universal Editor e verifique a Extensão de Ícone **A/B**. Caso o ícone não esteja visível, confirme se você ativou o recurso no gerenciador de extensões. Se não estiver ativado, ative-o ou solicite acesso.
   <!--1. Open your GitHub repository and check if the `plugins/experimention` folder exists. If not, you will need to set up the experimentation engine and MFE first (see the note above).-->
1. Aponte sua configuração do `fstab.yaml` para a configuração do projeto e vincule-a à instância do autor do AEM. Consulte também [Conectar seu código ao seu conteúdo](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)
1. Abra a instância do AEM e, se o projeto estiver pronto, abra-o diretamente no Universal Editor.
1. Abra o projeto e a página de índice na qual deseja executar experimentos e clique em **Editar** na barra superior.
1. Clique no ícone A/B para abrir a extensão de experimentação.

>[!NOTE]
>Se tiver problemas para configurar a experimentação para seu projeto, entre em contato com `aem-contextual-experimentation@adobe.com`.

>[!NOTE]
>Para obter mais detalhes sobre como instalar e configurar o mecanismo de experimentação, consulte a seção de documentação do seguinte [repositório](https://github.com/adobe/aem-experimentation/tree/v2-ui).

## Variantes de experimentos e fluxo de trabalho geral {#experiment-variants-workflow}

Antes de seguir o restante do guia para configurar seu primeiro experimento, há alguns termos usados com frequência que você deve conhecer:

* **Controle**: a experiência anterior à execução do experimento. Todos os experimentos tentam testar e demonstrar uma melhoria em relação à experiência de controle.
* **Challenger**: uma experiência diferente da experiência de controle e que é &quot;testada&quot; tanto contra ela quanto ao lado dela.
* **Variantes**: controle e desafiante são variantes de um experimento.
* **Significância estatística**: avaliando se seu desafiante é realmente melhor que o controle. Calcular significância estatística permite que você descarte a sorte e se concentre nos resultados que têm um efeito real.

De modo geral, ao configurar um experimento, você usará uma página pré-existente como página de controle. Ao usar o painel de experimentação, você criará uma página desafiante que é inicialmente uma cópia da página de controle. Na página desafiante, você pode testar coisas diferentes, como variantes de conteúdo, diferentes layouts de página, call-to-action (CTA) e assim por diante. Você também pode usar variantes geradas por IA, usando a funcionalidade **Gerar variação** no painel de experimentação.

Para cada experimento, o tráfego é inicialmente dividido 50/50 entre o controle e o desafiante, mas você pode configurar como o tráfego é dividido conforme necessário. Após ativar o experimento, você receberá dados por meio do serviço de Telemetria Operacional.

O [serviço de Telemetria Operacional](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) coleta dados, por exemplo, o número de visitantes na página de controle em comparação com a página de desafiante. Em seguida, você usa esses dados para selecionar as melhorias necessárias para o site. Desde que você fique dentro da linguagem de design estabelecida em seu site e use a funcionalidade existente, será possível configurar uma variante de experimento e enviá-la para produção em questão de minutos.

>[!NOTE]
>Lembre-se que o plug-in não usa nenhum dado do usuário final, nem persiste nenhum, que possa levar à sua identificação. Não é necessário aceitação nem consentimento do usuário final ao usar a configuração padrão que usa o serviço de [Telemetria Operacional no AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

<!--### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. -->

### Criação de experimentos no Universal Editor

Para usar os recursos de experimentação no Universal Editor, primeiro você deve configurar o painel de experimentação conforme detalhado nos capítulos apresentados acima e garantir que use os sites do AEM como fonte de conteúdo. Depois que tudo estiver configurado, siga estas etapas.

### Comece a editar seu projeto no Editor universal

Abra a instância do AEM e, se o projeto estiver pronto, abra-o diretamente no Universal Editor. Se você não tiver um projeto pronto e os sites do AEM configurados como uma fonte de conteúdo, crie um novo projeto padronizado a partir do modelo fornecido. Você pode vincular seu repositório ou nosso repositório de exemplo para direcioná-lo [https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation). Consulte também a página [Configurar AEM Sites como um Source de Conteúdo](https://www.aem.live/developer/ue-tutorial). Após a configuração do projeto, abra-o e a página de índice onde deseja executar experimentos e clique em **Editar** na barra superior.

### Inicie a extensão A/B

Clique no ícone **A/B** para abrir a extensão de experimentação. Na primeira vez que usar, a interface estará vazia. Clique em **Criar novo** para iniciar um novo experimento.

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### Configurar os detalhes do experimento

Alguns dos valores do experimento são predefinidos, como a seguir:

**Tipo de experimento**: teste A/B (somente o tipo suportado por enquanto)
**Otimizando Para**: Conversão (somente tipo suportado por enquanto)

Você também pode renomear o experimento para algo mais descritivo, por exemplo, `homepage-head-experiment`.

![Detalhes-experimento](/help/sites-cloud/administering/assets/exp-values.png)

### Adicionar e editar variantes

Entenda os conceitos de desafiante e variante como apresentados acima antes de continuar. Clique em **Adicionar novo** para criar uma variante desafiante:

* Você será direcionado para a página do desafiante na mesma guia; inicialmente, é apenas uma cópia do seu controle.
* Edite a página diretamente no contexto ou clique em **Gerar variação** para usar a assistência de IA.
* Depois de fazer as alterações, volte para a extensão para continuar.

![Variante de controle](/help/sites-cloud/administering/assets/control-variant.png)

### Definir outras propriedades e Salvar como rascunho

No painel de experimentação, é possível definir uma data de início e término (ambos opcionais). Se nenhuma data de início for fornecida, o teste será iniciado assim que for publicado. Se nenhuma data final for fornecida, o teste será executado indefinidamente. Você também pode ajustar a divisão do tráfego. Recomendamos começar com uma divisão par de 50/50.

Quando terminar, clique em **Salvar**. Isso salvará seu experimento como um Rascunho. Observe que o experimento ainda não está ativo. Você pode retornar à visão geral clicando em **Voltar para o experimento** ou pode ficar na interface de Edição para ativar o experimento.

![Rascunho](/help/sites-cloud/administering/assets/draft-save.png)

### Ativar o experimento

Quando estiver pronto, clique em **Ativar** para iniciar o experimento e publicar a página do experimento. O teste começará a coletar dados de Telemetria operacional (RUM) (consulte mais detalhes nos capítulos abaixo).

![Ativar](/help/sites-cloud/administering/assets/activate.png)

### Monitorar e promover

Depois que o experimento atingir significância estatística, clique em **Promover** para tornar a variante desejada seu novo controle. Lembre-se de que você pode promover a variante de experimento em qualquer ponto após a ativação, mesmo que ela não atinja significância estatística.

### Usar a experimentação com o AEM Sidekick no Edge Delivery Services

Se você tiver o AEM sidekick instalado, poderá usar o painel de experimentação diretamente com seu projeto no Edge Delivery Service sem usar o Universal Editor. A funcionalidade é essencialmente a mesma do teste A/B descrito acima, basta ter em mente que você precisa estar no modo **Visualização** para editar e configurar o teste. Depois de concluir a configuração do teste, clique em **Ativar** para ativar o controle e a variante desafiante e começar a coletar dados de telemetria.

<!-- ### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the “Experiment ID”. Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let’s assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

<!--- The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md). -->

<!--- ### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like. -->

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## Outras considerações {#other-considerations}

Abaixo estão vários aspectos que você deve considerar ao usar a experimentação de contexto.

### Conversão {#conversion}

Os experimentos são configurados para endereçar a conversão (rastreia elementos clicáveis na página). Atualmente, oferecemos suporte a experimentos em nível de página com um experimento por página.

<!--### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.-->

## Desenvolvedor e recursos técnicos {#dev-resources}

A Adobe Experience Manager usa a [Telemetria Operacional](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) para coletar dados de operações estritamente necessários para descobrir e corrigir problemas funcionais e de desempenho em sites viabilizados pela Adobe Experience Manager. Os dados de Telemetria Operacional podem ser usados para diagnosticar problemas de desempenho. A Telemetria operacional preserva a privacidade dos visitantes por meio de amostragem (apenas uma pequena parte de todas as exibições de página serão monitoradas).

### Privacidade {#privacy-experimentation}

O [serviço de Telemetria Operacional no AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) foi criado para preservar a privacidade do visitante e minimizar a coleta de dados. Como visitante, isso significa que a Adobe não tentará coletar informações pessoais sobre você ou informações que possam ser rastreadas até você. Como operador de site, analise os itens de dados coletados abaixo para entender se eles exigem consentimento.
A Telemetria Operacional do AEM não usa nenhum estado ou ID do lado do cliente, como cookies ou `localStorage`, `sessionStorage` ou similar, para coletar métricas de uso. Os dados são enviados de forma transparente por meio de uma chamada `Navigator.sendBeacon`, não por pixels ou técnicas semelhantes. Não há &quot;impressão digital&quot; de dispositivos ou indivíduos por meio de seu endereço IP, sequência de agente do usuário ou quaisquer outros dados para fins de captura de dados de amostra.

Não é permitido adicionar dados pessoais à coleção de dados de Telemetria operacional, nem os dados de Telemetria operacional podem ser usados para casos de uso que vão além do estritamente necessário.
