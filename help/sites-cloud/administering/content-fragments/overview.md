---
title: Uma visão geral dos conceitos e práticas recomendadas do trabalho com fragmentos de conteúdo
description: Saiba como os fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service permitem criar e usar conteúdo estruturado; ideal para entrega headless e criação de página.
feature: Content Fragments
role: User, Developer
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 2449bc380268ed42b6c8d23ae4a4fecaf1736889
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 30%

---

# Trabalhar com fragmentos de conteúdo - Conceitos e práticas recomendadas {#working-with-content-fragments-concepts-and-best-practices}

Com o Adobe Experience Manager (AEM) as a Cloud Service, os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem preparar conteúdo pronto para uso em vários locais e em vários canais, ideal para [entrega headless](/help/headless/what-is-headless.md) e [criação de página](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!IMPORTANT]
>
>Muitos recursos descritos nesta seção estão *somente* disponíveis no [Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md); portanto, o *online* Adobe Experience Manager (AEM) as a Cloud Service, não é uma instância local.

>[!IMPORTANT]
>
>Os fragmentos de conteúdo podem ser acessados de dois consoles: **Fragmentos de conteúdo** e **Assets**.
>
>Também há dois editores para a criação de fragmentos de conteúdo; embora a funcionalidade básica seja a mesma, há algumas diferenças. Ambos os editores podem ser acessados em ambos os consoles.
>
>Esta seção trata do console de **Fragmentos de conteúdo** e do editor de Fragmento de conteúdo *new*. Eles foram desenvolvidos para entrega de conteúdo headless (embora possam ser usados para todos os cenários)
>
>Para obter mais informações, consulte:
>
>* uso do console **Assets** para [gerenciar fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)
>* uso do [*original* editor de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-variations.md),
>* usando [Fragmentos de conteúdo para a criação de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).


Os fragmentos de conteúdo contêm conteúdo estruturado:

* Cada fragmento é baseado em um [Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).
   * O [Modelo de fragmento de conteúdo define a estrutura](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) do fragmento resultante.
* Cada fragmento consiste em:
   * **[Principal](#main-and-variations)** - uma parte integral do fragmento que contém o conteúdo principal; sempre existe, não pode ser excluído
   * **[Variações](#main-and-variations)** - uma ou mais permutas do conteúdo, criadas pelo autor
* A estrutura pode variar entre:
   * Básico
      * Por exemplo, um único campo de texto de várias linhas.
      * Pode ser usado para preparar conteúdo direto para uso na criação de páginas.
      * Também pode ser usado para entrega headless em seu aplicativo.
   * Complexo
      * Uma combinação de vários campos de tipos de dados variáveis, incluindo texto, número, booleano e data e hora, entre outros.
      * Pode ser usado para preparar conteúdo mais estruturado para a criação de páginas ou para entrega headless em seu aplicativo.
   * Aninhado
      * Os tipos de dados de referência disponíveis permitem aninhar o conteúdo.
      * Tendem a ser usados para entrega headless em seu aplicativo.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo Sling (JSON) dos componentes principais do AEM. Esta forma de entrega:

* permite usar o componente para gerenciar quais elementos de um fragmento fornecer
* permite a entrega em massa; adicionando vários [Componentes principais do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) na página que está sendo usada para a entrega da API

O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo de entrega, como:

* Canal físico; por exemplo, desktop, móvel.
* Forma de entrega em um canal físico; por exemplo, “página de detalhes do produto”, “página de categoria do produto” para desktop ou “web para publicação de conteúdo para dispositivos móveis”, “aplicativo para publicação de conteúdo para dispositvos móveis” para celular.

No entanto, você (provavelmente) não deseja usar o mesmo conteúdo *exato* para todos os canais; é necessário otimizar o conteúdo de acordo com o canal específico.

Com os Fragmentos de conteúdo é possível:

* Considerar como atingir públicos-alvo com eficiência em todos os canais.
* Criar e gerenciar conteúdo editorial neutro para o canal.
* Criar grupos de conteúdo para um intervalo de canais.
* Desenvolver variações de conteúdo para canais específicos.
* Adicionar imagens ao texto inserindo ativos.
* Criar conteúdo aninhado para refletir a complexidade dos seus dados.

Esses Fragmentos de conteúdo podem ser reunidos para fornecer experiências em uma variedade de canais.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[fragmentos de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md)** são recursos diferentes no AEM:
>
>* Os **fragmentos de conteúdo** são conteúdos editoriais com definição e estrutura, mas sem design visual e/ou layout adicional. Eles podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte [Entendendo os fragmentos de conteúdo e fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

Esta e as seguintes páginas abordam as tarefas de criação, configuração, manutenção e uso dos fragmentos de conteúdo:

* [Habilitar a funcionalidade de fragmento de conteúdo para sua instância](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) - habilitando, criando e [definindo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) seus modelos
* [Criar os fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (usando o Console de fragmentos de conteúdo)

Após a criação dos fragmentos, é possível:

* [Use o Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md) - para:
   * acessar, publicar (para visualizar ou produzir) e fazer referência aos fragmentos
* [Use o editor de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md) - para:
   * editar, publicar (para visualização ou produção) e fazer referência aos fragmentos
   * colaborar com outros autores usando Comentários
* [Analisar](/help/sites-cloud/administering/content-fragments/analysis.md) a estrutura do fragmento de conteúdo usando o editor
* [Acesse os fragmentos com o GraphQL para entrega headless em seus aplicativos](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [Integrar e usar os fragmentos de conteúdo no Adobe Journey Optimizer](/help/sites-cloud/administering/content-fragments/content-fragments-with-journey-optimizer.md)
* Criar e gerenciar [Inicializações de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)
* [Ou use os fragmentos para a criação de página](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>Essas páginas podem ser lidas em conjunto com:
>
>* [Personalização e extensão de fragmentos de conteúdo](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Fragmentos de conteúdo configuram componentes para renderização](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Compatibilidade com os Fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API GraphQL do AEM para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
>* [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.


## Principais e variações {#main-and-variations}

As variações são um recurso importante dos fragmentos de conteúdo do AEM. Eles permitem criar e editar cópias do conteúdo **Principal** para uso em canais e cenários específicos, tornando a entrega de conteúdo headless e a criação de página ainda mais flexíveis.

* **Principal**

   * **Principal** não é uma variação propriamente dita, mas é a base de todas as variações.
   * Uma parte integral do fragmento

      * Cada fragmento de conteúdo tem uma instância de **Main**.
      * Não é possível excluir **Principal**.

   * **Principal** está acessível no editor de fragmentos em **[Variações](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >No editor disponível no console **Assets**, **Main** está rotulado como **Master**.

* **Variações**

   * Representações de texto de fragmento específicas para fins editoriais; podem estar relacionadas a canais, mas não é obrigatório. Também podem ser para modificações locais ad hoc.
   * São criadas como cópias de **Principal**, mas podem ser editadas conforme necessário; geralmente há sobreposição de conteúdo entre as próprias variações.
   * Podem ser definidas durante a criação do fragmento; no painel esquerdo.
   * São armazenadas no fragmento para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [comparadas e sincronizadas](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) com **Principal**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os Serviços de conteúdo do AEM foram criados para generalizar a descrição e a entrega de conteúdo de e para o AEM para além do foco em páginas da Web.

Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos nativos para dispositivos móveis
* outros canais e pontos de contato externos ao AEM

A entrega é feita no formato JSON usando o Exportador JSON.

Os fragmentos de conteúdo do AEM podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter vários tipos de conteúdo; incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Juntamente com os recursos de exportação em JSON dos componentes principais do AEM, esse conteúdo estruturado pode ser usado para fornecer conteúdo do AEM a outros canais além das páginas do AEM.

>[!NOTE]
>
>Consulte [Headless e AEM](/help/headless/introduction.md) para obter uma introdução ao desenvolvimento headless do AEM Sites as a Cloud Service.

>[!NOTE]
>
>O AEM também permite a tradução do conteúdo do fragmento. Consulte [Tradução de ativos](/help/assets/translate-assets.md) para obter mais informações.

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Um recurso do **Sites**.

* Armazenados como **Ativos**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos no [console de Fragmentos de conteúdo](#content-fragments-console).
   * Criado e editado no [Editor de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md).

* Acessível para entrega de conteúdo usando a [API GraphQL do AEM](/help/headless/graphql-api/content-fragments.md).

* Disponível no [editor de páginas usando o componente Fragmento de Conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente de referência):

   * O [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) está disponível para autores de página. Ele permite referenciar e entregar o fragmento de conteúdo necessário nos formatos HTML ou JSON.

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* Não possuem layout ou design (a formatação de texto é possível para campos de texto).
* São independentes do mecanismo de entrega (como a página ou canal).
* Contêm uma ou mais [partes constituintes](#constituent-parts-of-a-content-fragment).
* Podem [conter ou estar conectados a imagens](#fragments-with-visual-assets).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para dar aos autores mais controle do conteúdo, as imagens podem ser adicionadas e/ou integradas a um Fragmento de conteúdo.

O Assets pode ser usado com um Fragmento de conteúdo de várias maneiras; cada uma com suas próprias vantagens:

* como uma **Referência de conteúdo**
* em um campo de **Texto multilinha**

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do Fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Você usa um [Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) para criar o fragmento de conteúdo. Os elementos (campos) [especificados no modelo definem a estrutura do fragmento](/help/sites-cloud/administering/content-fragments/content-fragment-models.md). Esses elementos (campos) podem ser de uma variedade de tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, geralmente multilinha, que são delimitados como entidades individuais.

   * Habilitam o controle de conteúdo durante a criação da página.

* **Metadados de fragmento**

   * Usa os [esquemas de metadados de ativos](/help/assets/metadata-schemas.md).
   * Tags podem ser criadas quando você:

      * Cria o fragmento
      * Ou posteriormente, ao [exibir ou editar as propriedades](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) no editor de fragmento

  >[!CAUTION]
  >
  >Os perfis de processamento de metadados não se aplicam aos fragmentos de conteúdo.

  >[!CAUTION]
  >
  >Um modelo de fragmento de conteúdo geralmente pode definir campos de dados chamados **Título** e **Descrição**. Se esses dois campos existirem, eles serão campos definidos pelo usuário e poderão ser atualizados na área de conteúdo do editor.
  >
  >O Fragmento de Conteúdo e suas variações também têm campos de metadados (propriedade) chamados **Título** e **Descrição**. Esses dois campos de metadados são parte integral de qualquer Fragmento de conteúdo e variação e são definidos inicialmente quando o fragmento é criado. Eles podem ser atualizados na área propriedades/metadados do editor.

* **[Principal](#main-and-variations)**
* **[Variações](#main-and-variations)**

### Exigido por fragmentos {#required-by-fragments}

Para criar fragmentos de conteúdo, você precisa:

* **Modelo de conteúdo**

   * É [habilitado usando o Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md).
   * São [criadas usando o Console de Fragmentos de Conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).
   * Obrigatório para [criar um fragmento](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições do modelo de fragmento de conteúdo exigem um título e um elemento de dados; todo o resto é opcional.
   * O modelo pode definir o conteúdo padrão, se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento, embora possam abrir o editor de modelo no editor de fragmento.
   * As alterações feitas em um modelo após a criação dos fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

Para usar os Fragmentos de conteúdo para a entrega de conteúdo headless, também é necessário:

* uma [consulta do GraphQL](/help/headless/graphql-api/content-fragments.md) para solicitar o conteúdo necessário
* esse conteúdo pode ser usado para desenvolver seus próprios SPAs para o AEM; para obter mais informações, revise os seguintes documentos:

   * [Tutorial WKND do SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Introdução à utilização do React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Introdução à utilização do Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Para usar os Fragmentos de conteúdo para a criação de páginas, também é necessário:

* Um **Componente de Fragmento de Conteúdo**

   * Fundamental para entregar o fragmento no formato HTML e/ou JSON.
   * Obrigatório para [fazer referência ao fragmento em uma página](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsável pela disposição e entrega de um fragmento; por exemplo, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associa automaticamente o componente necessário.
   * Consulte o [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR).

## O console de Fragmentos de conteúdo {#content-fragments-console}

O console de Fragmentos de Conteúdo é dedicado ao gerenciamento, pesquisa e criação de [Fragmentos de Conteúdo](/help/sites-cloud/administering/content-fragments/managing.md), [Modelos de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) e [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md). Ele foi otimizado para uso em um contexto headless, mas também é usado ao criar fragmentos de conteúdo e modelos de fragmento de conteúdo para uso na criação de páginas.

O console pode ser acessado diretamente do nível superior da Navegação global.

![Navegação global - Console de fragmentos de conteúdo](assets/cf-managing-global-navigation.png)

Você pode usar o painel à esquerda para selecionar o tipo de recurso para exibir, navegar e gerenciar:

![Console de Fragmentos de conteúdo - navegação](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-navigation.png)

Para obter informações detalhadas, consulte:

* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md)
* [Modelos de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Ativos](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

* Uma seleção de [atalhos de teclado](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) estão disponíveis para uso neste console

>[!CAUTION]
>
>Este console tem *somente* disponível no Adobe Experience Manager (AEM) as a Cloud Service online.

>[!NOTE]
>
>A equipe do projeto pode personalizar o console e o editor, se necessário. Consulte [Personalização do Console e do Editor de Fragmentos de Conteúdo](/help/implementing/developing/extending/content-fragments-console-and-editor.md) para obter mais detalhes.

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que será usado e onde.

### Amostra do WKND {#wknd-sample}

O [Site WKND e as amostras WKND Compartilhadas](/help/implementing/developing/introduction/develop-wknd-tutorial.md) são fornecidos para ajudá-lo a aprender sobre o AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

O projeto WKND inclui:

* Modelos de fragmentos de conteúdo disponíveis em:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:

   * `.../assets.html/content/dam/wknd/en`

## Práticas recomendadas {#best-practices}

Os fragmentos de conteúdo podem ser usados para formar estruturas complexas. O Adobe oferece recomendações para práticas recomendadas ao definir e usar modelos e fragmentos.

### Mantenha a simplicidade {#keep-it-simple}

Ao modelar conteúdo estruturado no AEM, mantenha as estruturas de conteúdo o mais simples possível para garantir um desempenho sólido do sistema e governança simplificada.

### Número de Modelos {#number-of-models}

Crie quantos modelos de conteúdo forem necessários, mas não mais.

Muitos modelos complicam a governança e podem retardar as consultas do GraphQL. Um pequeno conjunto de modelos, máximo de baixas dezenas, é geralmente suficiente. Se você se aproximar das altas dezenas ou mais, reconsidere sua estratégia de modelagem.

### Aninhamento de modelos e fragmentos (muito importante) {#nesting-models-and-fragments}

Evite o aninhamento profundo ou excessivo de fragmentos de conteúdo usando Referências do fragmento de conteúdo, que permitem que os fragmentos façam referência a outros fragmentos, às vezes em vários níveis.

O uso intenso de referências de Fragmento de conteúdo pode afetar significativamente o desempenho do sistema, a capacidade de resposta da interface do usuário e a execução de consultas do GraphQL. Faça com que o aninhamento seja mantido em não mais de dez níveis.

### Número de Campos e Tipos de Dados por Modelo {#number-of-data-fields-and-types-per-model}

Inclua apenas os campos e tipos de dados que um modelo realmente precisa.

Modelos muito complexos levam a fragmentos muito complexos que podem dificultar a criação e reduzir o desempenho do editor.

### Campos de Rich Text {#rich-text-fields}

Use campos Rich Text (o Tipo de Dados **Texto de várias linhas**) levando em consideração.

Limitar o número de campos Rich Text por modelo. Além disso, a quantidade de texto armazenado em cada fragmento e a quantidade de formatação do HTML. Um conteúdo de rich text muito grande pode afetar negativamente o desempenho do sistema.

### Número de variações {#number-of-variations}

Crie quantas variações de fragmento forem necessárias, mas não mais.

As variações adicionam tempo de processamento a um Fragmento de conteúdo, no ambiente de criação e no momento da entrega também. É recomendável manter o número de variações em um mínimo gerenciável.

Uma prática recomendada é não exceder dez variações por Fragmento de conteúdo.

### Teste antes da produção {#test-before-production}

Na dúvida, crie um protótipo das estruturas de conteúdo desejadas antes de implantá-las na produção. A prova de conceito antecipada, juntamente com testes adequados, técnicos e de aceitação do usuário, podem ajudar a evitar problemas posteriormente ao enfrentar prazos na produção.