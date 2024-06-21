---
title: Uma visão geral do trabalho com fragmentos de conteúdo
description: Saiba como os fragmentos de conteúdo no AEM as a Cloud Service permitem criar e usar conteúdo; ideal para entrega headless e criação de página.
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 39%

---

# Uma visão geral do trabalho com fragmentos de conteúdo {#overview-working-with-content-fragments}

Com o Adobe Experience Manager (AEM) as a Cloud Service, os fragmentos de conteúdo permitem projetar, criar, preparar e [publicar conteúdo independente de página](/help/sites-cloud/authoring/fragments/content-fragments.md). Eles permitem preparar conteúdo pronto para uso em vários locais e em vários canais, ideal para entrega headless e criação de página.

>[!IMPORTANT]
>
>Os fragmentos de conteúdo podem ser acessados de dois consoles: **Fragmentos de conteúdo** e **Assets**.
>
>Também há dois editores disponíveis para Fragmentos de conteúdo. (Ambos os editores podem ser acessados nos dois consoles.)
>
>Esta seção trata da **Fragmentos de conteúdo** e o *novo* Editor de fragmento de conteúdo. Eles foram desenvolvidos para entrega de conteúdo headless (embora possam ser usados para todos os cenários)
>
>Para obter mais informações, consulte:
>
>* utilização do **Assets** console do para [gerenciar fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)
>* utilização do [*original* Editor de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-variations.md),
>* usar [Fragmentos de conteúdo para criação de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).


Os fragmentos de conteúdo contêm conteúdo estruturado:

* Cada fragmento é baseado em um [Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * O Modelo de fragmento de conteúdo define a estrutura do fragmento resultante.
* Cada fragmento consiste em:
   * **[Principal](#main-and-variations)** - uma parte integral do fragmento que contém o conteúdo principal; sempre existe, não pode ser excluído
   * **[Variações](#main-and-variations)** - uma ou mais permutações do conteúdo, criadas pelo autor
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
* permite a entrega em massa; adicionando vários [Componentes principais do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) na página que está sendo usada para entrega da API

O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo de entrega, como:

* Canal físico; por exemplo, desktop, móvel.
* Forma de entrega em um canal físico; por exemplo, “página de detalhes do produto”, “página de categoria do produto” para desktop ou “web para publicação de conteúdo para dispositivos móveis”, “aplicativo para publicação de conteúdo para dispositvos móveis” para celular.

No entanto, você (provavelmente) não deseja usar o *exato* o mesmo conteúdo para todos os canais - é necessário otimizar o conteúdo de acordo com o canal específico.

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
>* Os **fragmentos de conteúdo** são conteúdos editoriais com definição e estrutura, mas sem design visual e/ou layout adicional. Eles podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte [Compreensão de fragmentos de conteúdo e fragmentos de experiência no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

Esta e as seguintes páginas abordam as tarefas de criação, configuração, manutenção e uso dos fragmentos de conteúdo:

* [Ativar a funcionalidade de fragmento de conteúdo para sua instância](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) - ativar, criar e definir modelos
* [Criar os fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (usando o Console de fragmentos de conteúdo)

Após a criação dos fragmentos, é possível:

* [Usar o console de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md) - para acessar, publicar (para visualização ou produção) e fazer referência aos fragmentos
* [Usar o editor de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md) - editar, publicar (para visualização ou produção) e fazer referência aos fragmentos
* [Analisar](/help/sites-cloud/administering/content-fragments/analysis.md)  a estrutura do fragmento de conteúdo, usando o editor
* [Acesse os fragmentos com o GraphQL, para entrega headless em seus aplicativos](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
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
>* A variável [OpenAPIs de fragmento de conteúdo e modelo de fragmento de conteúdo](/help/headless/content-fragment-openapis.md) também estão disponíveis.


## Principais e variações {#main-and-variations}

As variações são um recurso importante dos fragmentos de conteúdo do AEM. Eles permitem criar e editar cópias do **Principal** conteúdo para uso em canais e cenários específicos, tornando a entrega de conteúdo headless e a criação de página ainda mais flexíveis.

* **Principal**

   * **Principal** não é uma variação em si, mas a base de todas as variações.
   * Uma parte integral do fragmento

      * Cada fragmento de conteúdo tem uma instância de **Principal**.
      * **Principal** não pode ser excluído.

   * **Principal** é acessível no editor de fragmentos, em **[Variações](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >No editor disponível no **Assets** console, **Principal** é rotulado como **Principal**.

* **Variações**

   * Representações de texto de fragmento específicas para fins editoriais; podem estar relacionadas a canais, mas não é obrigatório. Também podem ser para modificações locais ad hoc.
   * São criadas como cópias de **Principal**, mas podem ser editadas conforme necessário; geralmente há sobreposição de conteúdo entre as próprias variações.
   * Podem ser definidas durante a criação do fragmento; no painel esquerdo.
   * São armazenadas no fragmento para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [comparado e sincronizado](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) com **Principal**.
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

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos do [Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * Criado e editado no [Editor de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md).

* Acessível para entrega de conteúdo usando o [API GraphQL do AEM](/help/headless/graphql-api/content-fragments.md).

* Disponível na [editor de páginas usando o componente Fragmento de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente de referência):

   * A variável [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) O está disponível para autores de página. Ele permite referenciar e entregar o fragmento de conteúdo necessário nos formatos HTML ou JSON.

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* Não possuem layout ou design (a formatação de texto é possível para campos de texto).
* São independentes do mecanismo de entrega (como a página ou canal).
* Contêm uma ou mais [partes constituintes](#constituent-parts-of-a-content-fragment).
* Podem [conter ou estar conectados a imagens](#fragments-with-visual-assets).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para dar aos autores mais controle do conteúdo, as imagens podem ser adicionadas e/ou integradas a um Fragmento de conteúdo.

Os ativos podem ser usados com um Fragmento de conteúdo de várias maneiras; cada uma com suas próprias vantagens:

* as a **Referência de conteúdo**
* no prazo de **Texto multilinha** campo

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do Fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Você usa um [Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) para criar o fragmento de Conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de uma variedade de tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, geralmente multilinha, que são delimitados como entidades individuais.

   * Ativam o controle de conteúdo durante a criação da página.

* **Metadados de fragmento**

   * Usa os [esquemas de metadados de ativos](/help/assets/metadata-schemas.md).
   * Tags podem ser criadas quando você:

      * Cria o fragmento
      * Ou posteriormente, quando você [exibir ou editar as propriedades](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) quando estiver no editor de fragmento

  >[!CAUTION]
  >
  >Os perfis de processamento de metadados não se aplicam aos fragmentos de conteúdo.

  >[!CAUTION]
  >
  >Um modelo de fragmento de conteúdo pode definir campos de dados chamados **Título** e **Descrição**. Se esses dois campos existirem, eles serão campos definidos pelo usuário e poderão ser atualizados na área de conteúdo do editor.
  >
  >O fragmento de conteúdo e suas variações também têm campos de metadados (propriedade) chamados **Título** e **Descrição**. Esses dois campos de metadados são parte integral de qualquer Fragmento de conteúdo e variação e são definidos inicialmente quando o fragmento é criado. Eles podem ser atualizados na área propriedades/metadados do editor.

* **[Principal](#main-and-variations)**
* **[Variações](#main-and-variations)**

### Exigido por fragmentos {#required-by-fragments}

Para criar fragmentos de conteúdo, você precisa:

* **Modelo de conteúdo**

   * É [ativado usando o Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md).
   * É [criado usando Ferramentas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * Obrigatório para [criar um fragmento](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições do modelo de fragmento de conteúdo exigem um título e um elemento de dados; todo o resto é opcional.
   * O modelo pode definir o conteúdo padrão, se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento, embora possam abrir o editor de modelo no editor de fragmento.
   * As alterações feitas em um modelo após a criação dos fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

Para usar os Fragmentos de conteúdo para a entrega de conteúdo headless, também é necessário:

* a [consulta do GraphQL](/help/headless/graphql-api/content-fragments.md) para solicitar o conteúdo necessário
* esse conteúdo pode ser usado para desenvolver seu próprio SPA para AEM; para obter mais informações, consulte os seguintes documentos:

   * [Tutorial WKND do SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Introdução à utilização do React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Introdução à utilização do Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Para usar os Fragmentos de conteúdo para a criação de páginas, também é necessário:

* A **Componente Fragmento de Conteúdo**

   * Fundamental para entregar o fragmento no formato HTML e/ou JSON.
   * Obrigatório para [fazer referência ao fragmento em uma página](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsável pela disposição e entrega de um fragmento; por exemplo, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associa automaticamente o componente necessário.
   * Consulte a [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR).

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que será usado e onde.

### Amostra do WKND {#wknd-sample}

A variável [Site da WKND e WKND compartilhado](/help/implementing/developing/introduction/develop-wknd-tutorial.md) são fornecidas amostras para ajudá-lo a aprender sobre o AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

O projeto WKND inclui:

* Modelos de fragmentos de conteúdo disponíveis em:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:

   * `.../assets.html/content/dam/wknd/en`
