---
title: Experimentação contextual no AEM as a Cloud Service
description: Saiba como usar o plug-in de experimentação para adicionar recursos de experimentação ao seu site.
feature: Administering
role: Admin
source-git-commit: 66ee08babae1f6640158260af051f8ad5f9bde85
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 0%

---

# Experimentação contextual no AEM as a Cloud Service {#contextual-experimentation}

>[!NOTE]
>Atualmente, o recurso de experimentação contextual está disponível somente por meio do programa beta. Entre em contato com o suporte da Adobe ou com seu gerente de conta para obter acesso ao programa beta.

A experimentação é a prática de testar o design, a funcionalidade e o código do site para melhorar o desempenho e tornar seu site mais eficaz e simplificado. Isso é feito alterando o conteúdo ou a funcionalidade, comparando os resultados com uma versão anterior e escolhendo as melhorias que têm efeitos mensuráveis.

Quando feito corretamente, é um padrão avançado para melhorar as conversões, o envolvimento e a experiência do visitante. Em geral, há alguns problemas a serem evitados ao tentar adotar a prática:

* **Muito pouco**: a maioria das empresas não está experimentando o suficiente e, quando o fazem, fazem experimentos com muito pouco tráfego para obter resultados significativos.
* **Muito lento**: muitas estruturas de experimentação tornam o site tão lento que as novas conversões em potencial não conseguem compensar o tráfego perdido e as rejeições devido à renderização lenta.
* **Muito complexo**: se levar muito tempo para configurar um novo experimento, menos experimentos serão executados.

Para sites executados no Adobe Experience Manager, há o **plug-in de experimentação** &quot;pronto para uso&quot; que permite aos desenvolvedores adicionar um recurso de experimentação a seus sites. Três coisas tornam essa abordagem diferente de outras estruturas de experimentação:

* É fácil configurar testes com as ferramentas que seus autores já conhecem e nenhum logon separado é necessário.
* Ele é profundamente integrado ao sistema de entrega do AEM, não atrasa o site e é resiliente a alterações no código e no conteúdo.
* Ele permite testar alterações simples de conteúdo, bem como experimentos que abrangem design, funcionalidade e código.

## Antes de começar {#before-start}

O plug-in de experimentação é usado no contexto do [Edge Delivery Services](/help/edge/overview.md), portanto, você precisará de uma conta do Github, um repositório de conteúdo como o SharePoint ou o Google Drive, e também do [AEM Sidekick](https://www.aem.live/docs/sidekick). Consulte também a [página Introdução - Tutorial do desenvolvedor do editor universal](https://www.aem.live/developer/tutorial) e [Introdução - Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial).

Após tudo configurado, **assista a este vídeo** intitulado [Experimentação instantânea](https://business.adobe.com/products/experience-manager/sites/testing-optimization.html) para obter uma breve demonstração sobre como funciona o plug-in de experimentação.

## Termos usados com frequência {#frequently-used-terms}

Antes de seguir o restante do guia para configurar seu primeiro experimento, há alguns termos usados com frequência que você deve conhecer:

* **Controle**: a experiência anterior à execução do experimento. Todos os experimentos tentam testar e demonstrar uma melhoria em relação à experiência de controle.
* **Challenger**: uma experiência diferente da experiência de controle e que é &quot;testada&quot; contra ela ou ao lado dela.
* **Variantes**: controle e desafiante são variantes de um experimento.
* **Significância estatística**: avaliando se seu desafiante é realmente melhor que o controle. Calcular significância estatística permite que você descarte a sorte e se concentre nos resultados que têm um efeito real.

## Variantes de experimentos e fluxo de trabalho geral {#experiment-variants-workflow}

De modo geral, ao configurar um experimento, você usará uma página pré-existente como página de controle. Em seguida, você criará uma página desafiante que substituirá a página de controle para alguns de seus visitantes. Na página desafiante, você pode testar coisas diferentes, como variantes de conteúdo, diferentes layouts de página, call-to-action (CTA) e assim por diante. Você pode configurar essas variantes de experimento adicionando parâmetros de metadados na página de controle (veja abaixo).

O [serviço de Telemetria Operacional](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) reúne dados, por exemplo, o número de visitantes na página de controle em comparação com a página de desafiante. Em seguida, você usa esses dados para selecionar as melhorias necessárias para o site. Desde que você fique dentro da linguagem de design estabelecida em seu site e use a funcionalidade de bloco existente, será possível configurar uma variante de experimento e enviá-la para produção em questão de minutos.

>[!NOTE]
>Lembre-se que o plug-in não usa nenhum dado do usuário final, nem persiste nenhum, que possa levar à sua identificação. Não é necessário o consentimento nem a aceitação do usuário final quando a configuração padrão que usa o serviço de [Telemetria Operacional no AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) é usada.

### Identificador do experimento {#experiment-identifier}

Antes de começar, cada experimento deve ter seu próprio identificador para fins de rastreamento e análise. Um bom ponto de partida é criar um identificador bom e exclusivo para o experimento, que será a &quot;ID do experimento&quot;. Os experimentos geralmente são numerados linearmente ou correlacionados à sua ID de problema em um rastreador de problemas ou sistema de gerenciamento. As IDs de experimento geralmente usam um prefixo para o projeto, por exemplo: `OPT-0134`, `EXP0004` ou `CCX0076`.

### Criar sua página do Challenger {#create-challenger-page}

Por convenção, é recomendável criar uma pasta com uma ID de experimento em minúsculas em seu `/experiments/ folder` (por exemplo /experiment/ccx0076/). Todas as páginas das variantes desafiantes estão localizadas nesta pasta. Você cria essa pasta no repositório local, por exemplo, Sharepoint ou Goggle Drive.

Sua pasta de experimentos deve ser semelhante a:

![experimentos-pasta](/help/sites-cloud/administering/assets/experiments-folder.png)

Depois que a pasta for criada, coloque uma cópia da página de controle nessa pasta e aplique as alterações na página que você deseja testar como parte da variante de experimento (veja o vídeo acima). Como exemplo, vamos supor que temos a seguinte página no site em que queremos executar um experimento:

![página-controle](/help/sites-cloud/administering/assets/control-page.png)

A cópia do desafiante colocada na pasta `experiments/<experiment-id>` pode ter esta aparência:

![página-desafiante](/help/sites-cloud/administering/assets/challenger-page.png)

Pré-visualize e publique a página desafiante usando o sidekick e quando terminar de criar a página desafiante. O URL do desafiante publicado será usado na próxima seção - configuração do experimento.

### Configuração do experimento {#configure-experiment}

Assim que as páginas desafiantes estiverem prontas para serem aceitas, você precisará voltar para a página de controle e adicionar metadados indicando que as páginas agora fazem parte do teste.

Há duas linhas de metadados que precisam ser adicionadas para uma variante de experimento.

* **Experimento**: contendo sua ID de experimento.

* **Variantes de experimento**: contém URLs para todos os desafiantes desta página, separadas por quebras de linha se você tiver mais de um desafiante.

Consulte o exemplo abaixo:

![página-metadados](/help/sites-cloud/administering/assets/metadata-page.png)

Para cada experimento, o tráfego é dividido entre todas as variantes (controle e desafiantes) e é automaticamente definido como uma distribuição par. Dessa forma, se você tem um desafiante, automaticamente haverá uma divisão de 50/50 entre o controle e o desafiante. Se você tem dois desafiantes, você automaticamente verá um terço do tráfego alocado para controlar e cada desafiante e assim por diante.

É possível substituir a divisão de tráfego configurando os metadados. Para obter mais informações sobre como personalizar os metadados usados em seus experimentos, consulte a seguinte [página](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Pré-visualizar e preparar suas variantes de experimento {#preview-stage-experiment}

Assim que estiver pronto para visualizar e preparar seu experimento, clique em Visualizar no lado esquerdo superior. Sempre que estiver visualizando uma página que tenha um experimento em execução, você verá a sobreposição de experimentação no ambiente de visualização `.aem.page`. A sobreposição de experimentação permite alternar entre as variantes de experimento e também fornece dados de tráfego.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

A coleta de dados para medir a eficácia de cada variante é baseada no [serviço de Telemetria Operacional no AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Envie sua variante de experimento para produção {#production-experiment}

Selecione as páginas de experimento e clique em Publicar no botão lateral para ativar o controle e a(s) variante(s) desafiante(s).

### Exemplos de caso de uso {#use-case-examples}

Veja abaixo vários exemplos de casos de uso de variantes de experimento. De modo geral, o fluxo de trabalho básico será semelhante ao descrito acima, com alterações específicas para cada caso de uso (como o número de páginas desafiantes ou alterações nos metadados).

#### Experimento de página inteira {#full-page}

Você usa um experimento de página inteira para testar entre duas variantes da mesma página. Esta é uma variante de página inteira de um teste a/b no qual você tem uma página de controle e uma página desafiante. Você substituirá todo o conteúdo da página de controle &quot;original&quot; na variante desafiante por um tipo diferente de conteúdo. Lembre-se de que, por padrão, o tráfego do cliente é dividido uniformemente (50/50), mas você pode criar divisões personalizadas se desejar.

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

Abaixo estão vários outros aspectos que você deve considerar ao usar a experimentação de contexto.

### Conversão {#conversion}

Os experimentos são configurados para endereçar a conversão (rastreia elementos clicáveis na página). Todos os experimentos devem ser definidos para o seguinte:

* Tipo de experimento
* A qual bloco de experiência o experimento se aplicará
* Quantas variantes o experimento conterá
* Qual é a composição de cada variante

### Verifique se as variantes de experimento não estão indexadas {#experiment-not-indexed}

Ao executar experimentos, geralmente é prática recomendada excluir as variantes do mapa de site e garantir que elas não sejam indexadas por mecanismos de pesquisa. Isso ocorre porque a página variante pode ser vista como conteúdo duplicado e afetar negativamente o SEO.

Você pode fazer isso usando um dos dois métodos a seguir:

* Se centralizar todos os experimentos em uma pasta dedicada, como `/experiments`: verifique se a folha `metadata.xlsx` em massa contém uma linha com `/experiments/**` como caminho e uma coluna de robôs com os valores `noindex`, `nofollow`.
* Se você manter o controle do experimento e as variantes com o conteúdo regular: adicione uma entrada de robôs nos metadados da página para cada variante, com o valor `noindex`, `nofollow`.

## Desenvolvedor e recursos técnicos {#dev-resources}

O Adobe Experience Manager usa [Telemetria Operacional]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md

) para coletar dados de operações estritamente necessários para detectar e corrigir problemas funcionais e de desempenho em sites viabilizados pela Adobe Experience Manager. Os dados de Telemetria Operacional podem ser usados para diagnosticar problemas de desempenho. A Telemetria operacional preserva a privacidade dos visitantes por meio de amostragem (apenas uma pequena parte de todas as exibições de página serão monitoradas).

### Privacidade {#privacy-experimentation}

O [serviço de Telemetria Operacional no AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) foi criado para preservar a privacidade do visitante e minimizar a coleta de dados. Como visitante, isso significa que a Adobe não tentará coletar informações pessoais sobre você ou informações que possam ser rastreadas até você. Como operador de site, analise os itens de dados coletados abaixo para entender se eles exigem consentimento.
A Telemetria Operacional do AEM não usa nenhum estado ou ID do lado do cliente, como cookies ou `localStorage`, `sessionStorage` ou similar, para coletar métricas de uso. Os dados são enviados de forma transparente por meio de uma chamada `Navigator.sendBeacon`, não por pixels ou técnicas semelhantes. Não há &quot;impressão digital&quot; de dispositivos ou indivíduos por meio de seu endereço IP, sequência de agente do usuário ou quaisquer outros dados para fins de captura de dados de amostra.

Não é permitido adicionar dados pessoais à coleção de dados de Telemetria operacional, nem os dados de Telemetria operacional podem ser usados para casos de uso que vão além do estritamente necessário.

### Perguntas frequentes {#faq}

Veja abaixo uma lista das perguntas mais frequentes:

P: Posso ajustar a proporção de divisão entre as variantes do meu experimento, por exemplo, 10% no controle e 90% no desafiante?

Sim, a taxa de divisão pode ser configurada através de [metadados](#configure-experiment).

P: Posso fazer experimentos em texto e imagens?

Sim, a variante pode ser uma página completamente diferente, portanto, você pode até mesmo testar as alterações de layout.
