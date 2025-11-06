---
title: Trabalhar com fragmentos de conteúdo (Assets - Fragmentos de conteúdo)
description: Saiba como os Fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service permitem projetar, criar, preparar e usar conteúdo, ideal para a criação de páginas e entrega headless.
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 56%

---

# Trabalho com Fragmentos de conteúdo {#working-with-content-fragments}

Com o Adobe Experience Manager (AEM) as a Cloud Service, os fragmentos de conteúdo permitem projetar, criar, preparar e [publicar conteúdo independente de página](/help/sites-cloud/authoring/fragments/content-fragments.md). Eles permitem preparar conteúdo pronto para uso em vários locais/canais, ideal para entrega headless. Eles também podem ser usados junto com o [Gerenciamento de vários sites para permitir que você reutilize o conteúdo](#reusing-content-fragments-with-msm).

Os fragmentos de conteúdo contêm conteúdo estruturado:

* Eles se baseiam em um [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md), que predefine uma estrutura para o fragmento resultante.
* A estrutura pode variar entre:
   * Básico
      * Por exemplo, um único campo de texto de várias linhas.
      * Ele pode ser usado para preparar conteúdo direto para uso na criação de páginas.
   * Complexo
      * Uma combinação de vários campos de tipos de dados variáveis, incluindo texto, número, booleano, data e hora, entre outros.
      * Ele pode ser usado para preparar conteúdo mais estruturado para a criação de páginas ou para entrega em seu aplicativo.
   * Aninhado
      * Os tipos de dados de referência disponíveis permitem aninhar o conteúdo.
      * Tendem a ser usados para entrega em seu aplicativo.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo Sling (JSON) dos componentes principais do AEM. Esta forma de entrega:

* permite usar o componente para gerenciar quais elementos de um fragmento fornecer
* permite a entrega em massa, adicionando vários componentes principais do fragmento de conteúdo na página que está sendo usada para a entrega da API

>[!NOTE]
>
>Os Fragmentos de conteúdo são um recurso do Sites, mas são armazenados como **Assets**.
>
>Os Fragmentos de conteúdo e os Modelos de fragmento de conteúdo agora são gerenciados principalmente com o console **[Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, embora os Fragmentos de conteúdo ainda possam ser gerenciados no console **Assets** e os Modelos de fragmento de conteúdo no console **Ferramentas**. Esta seção aborda o gerenciamento dos consoles **Assets** e **Ferramentas**.
>
>Há dois editores para a criação de fragmentos de conteúdo; embora a funcionalidade básica seja a mesma, há algumas diferenças. Esta seção abrange o editor original, acessado principalmente do console **Assets**. Consulte a documentação do Sites, [Fragmentos de conteúdo - Criação](/help/sites-cloud/administering/content-fragments/authoring.md), para obter detalhes do novo editor (acessado principalmente do console **Fragmentos de conteúdo**). Ambos os editores têm um botão de alternância na barra de ferramentas superior para fornecer acesso rápido ao outro editor.

Esta e as seguintes páginas abordam as tarefas de criação, configuração, manutenção e uso dos fragmentos de conteúdo:

* [Habilitar a funcionalidade de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md) - habilitando, criando e definindo seus modelos
* [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md) - crie fragmentos de conteúdo; em seguida, edite, publique e faça referência
* [Variações - Criação do conteúdo dos fragmentos](/help/assets/content-fragments/content-fragments-variations.md) — crie o conteúdo do fragmento e variações do Principal
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) — uso da sintaxe de marcação para o fragmento
* [Uso de conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) — adição de conteúdo associado
* [Metadados - Propriedades do fragmento](/help/assets/content-fragments/content-fragments-metadata.md) — visualização e edição das propriedades do fragmento
* Use os [Fragmentos de conteúdo, juntamente com o GraphQL, para que você possa fornecer conteúdo](/help/assets/content-fragments/content-fragments-graphql.md) para uso em seus aplicativos. Para ajudar nisso, você pode visualizar a [saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).
* [Reutilizar fragmentos de conteúdo usando o MSM](#reusing-content-fragments-with-msm)

>[!NOTE]
>
>Essas páginas podem ser lidas com:
>
>* [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* [Personalização e extensão de fragmentos de conteúdo](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Fragmentos de conteúdo configuram componentes para renderização](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Compatibilidade com os Fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API GraphQL do AEM para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
>* As [OpenAPIs de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo](/help/headless/content-fragment-openapis.md)

O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo de entrega, como:

* Canal físico; por exemplo, desktop, móvel.
* Forma de entrega em um canal físico; por exemplo, “página de detalhes do produto”, “página de categoria do produto” para desktop ou “web para publicação de conteúdo para dispositivos móveis”, “aplicativo para publicação de conteúdo para dispositvos móveis” para celular.

No entanto, você (provavelmente) não deseja usar o mesmo conteúdo para todos os canais; é necessário otimizar o conteúdo de acordo com o canal específico.

Com os Fragmentos de conteúdo é possível:

* Considerar como atingir públicos-alvo com eficiência em todos os canais.
* Criar e gerenciar conteúdo editorial neutro para o canal.
* Criar grupos de conteúdo para um intervalo de canais.
* Desenvolver variações de conteúdo para canais específicos.
* Adicionar imagens ao texto inserindo ativos (fragmentos de mídia mista).
* Crie conteúdo aninhado para refletir a complexidade dos seus dados.

Esses fragmentos de conteúdo podem ser reunidos para fornecer experiências em vários canais.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[fragmentos de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md)** são recursos diferentes no AEM:
>
>* Os **fragmentos de conteúdo** são conteúdos editoriais com definição e estrutura, mas sem design visual e/ou layout adicional. Eles podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte também [Entendendo os fragmentos de conteúdo e fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os Serviços de conteúdo do AEM foram criados para generalizar a descrição e a entrega de conteúdo de e para o AEM para além do foco em páginas da Web.

Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos nativos para dispositivos móveis
* outros canais e pontos de contato externos ao AEM

A entrega é feita no formato JSON usando o Exportador JSON.

Os fragmentos de conteúdo do AEM podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter vários tipos de conteúdo, incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Juntamente com os recursos de exportação em JSON dos componentes principais do AEM, esse conteúdo estruturado pode ser usado para fornecer conteúdo do AEM a outros canais além das páginas do AEM.

>[!NOTE]
>
>Consulte [Headless e AEM](/help/headless/introduction.md) para obter uma introdução ao desenvolvimento headless do AEM Sites as a Cloud Service.

>[!NOTE]
>
>O AEM também permite a tradução do conteúdo do fragmento. Consulte [Tradução de ativos](/help/assets/translate-assets.md) para obter mais informações.

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Armazenados como **Ativos**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos no console **Assets**.
   * Criados e editados no Editor de fragmento de conteúdo.

* Usado no [editor de páginas pelo componente Fragmento de Conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente de referência):

   * O componente **Fragmento de conteúdo** está disponível para autores de página. Ele permite referenciar e entregar o fragmento de conteúdo necessário nos formatos HTML ou JSON.

* Acessíveis por meio da [API GraphQL do AEM](/help/headless/graphql-api/content-fragments.md).

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* Não ter layout ou design (alguma formatação de texto é possível no modo Rich Text).
* Contêm uma ou mais [partes constituintes](#constituent-parts-of-a-content-fragment).
* [Contém ou pode ser conectado a imagens](#fragments-with-visual-assets).
* É usado [conteúdo intermediário](#in-between-content-when-page-authoring-with-content-fragments) quando referenciado em uma página.
* Eles são independentes do mecanismo de delivery (ou seja, página, canal).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para conceder mais controle do conteúdo aos autores, as imagens podem ser adicionadas e/ou integradas a um fragmento de conteúdo.

O Assets pode ser usado com um fragmento de conteúdo de várias maneiras; cada uma com suas próprias vantagens:

* **Inserir ativo** em um fragmento (fragmentos de mídia mista)

   * Eles são parte do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Definem a posição do ativo.
   * Consulte [Inserir ativos no fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) no Editor de fragmentos para obter mais informações.

  >[!NOTE]
  >
  >Os ativos visuais inseridos no fragmento de conteúdo propriamente dito são anexados ao parágrafo anterior no fragmento. Quando o fragmento é adicionado a uma página, esses ativos são movidos em relação a esse parágrafo quando o conteúdo intermediário é adicionado.

* **Conteúdo associado**

   * Conectado a um fragmento; mas não a uma parte fixa do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Possui alguma flexibilidade para o posicionamento.
   * Facilmente disponível para uso (como conteúdo intermediário) ao usar o fragmento em uma página.

  Consulte o [Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obter mais informações.

* Ativos disponíveis no **navegador de Ativos** do editor de página

   * Permitem flexibilidade total para a seleção de um ativo.
   * Possui alguma flexibilidade para o posicionamento.
   * Não fornecem o conceito de aprovação para um fragmento específico.

  Consulte [Navegador de ativos](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) para obter mais informações.

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Usa-se um modelo de conteúdo para criar o fragmento de conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de vários tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, geralmente multilinha, que são delimitados como entidades individuais.

   * Nos modos [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), um parágrafo pode ser formatado como um cabeçalho. Nesse caso, ele e o parágrafo a seguir pertencem como uma unidade.

   * Habilitam o controle de conteúdo durante a criação da página.

* **Ativos inseridos em um fragmento (fragmentos de mídia mista)**

   * Ativos (imagens) inseridos no fragmento real e usados como conteúdo interno de um fragmento.
   * Incorporado no sistema de parágrafo do fragmento.
   * Podem ser formatados quando o [fragmento é usado/referenciado em uma página](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Só podem ser adicionados, excluídos ou movidos dentro de um fragmento usando o editor de fragmentos. Essas ações não podem ser realizadas no editor de páginas.
   * Só podem ser adicionados, excluídos ou movidos dentro de um fragmento usando o [formato Rich Text no editor de fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Só podem ser adicionados a elementos de texto multilinha (qualquer tipo de fragmento).
   * São anexados ao texto anterior (parágrafo).

     >[!CAUTION]
     >
     >Os ativos podem ser (inadvertidamente) removidos de um fragmento ao alternar para o formato de Texto sem formatação.

     >[!NOTE]
     >
     >O Assets também pode ser adicionado como conteúdo adicional (intermediário) ao usar um fragmento em uma página; usando o [Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) ou ativos do navegador Assets.

* **Conteúdo associado**

   * Esse é um conteúdo externo a um fragmento, mas com relevância editorial. Normalmente, imagens, vídeos ou outros fragmentos.
   * Os ativos individuais contidos na coleção estão disponíveis para serem usados com o fragmento no editor de páginas, quando ele é adicionado a uma página. Isso significa que elas são opcionais, dependendo dos requisitos do canal específico.
   * Os ativos estão [associados aos fragmentos por meio de coleções](/help/assets/content-fragments/content-fragments-assoc-content.md); as coleções associadas permitem que o autor decida quais ativos usar ao criar a página.

      * As coleções podem ser associadas aos fragmentos como conteúdo padrão ou por autores durante a criação do fragmento.
      * As [coleções de ativos (DAM)](/help/assets/manage-collections.md) são a base para o conteúdo associado de fragmentos.
   * Opcionalmente, também é possível adicionar o próprio fragmento a uma coleção para auxiliar no rastreamento.

* **Metadados de fragmento**

   * Usa os [esquemas de metadados de ativos](/help/assets/metadata-schemas.md).
   * Tags podem ser criadas quando você:

      * Cria o fragmento
      * Ou posteriormente:

         * Ao visualizar/editar as **Propriedades** do fragmento no console
         * Ao editar os **Metadados** no editor de fragmento

  >[!CAUTION]
  >
  >Os perfis de processamento de metadados não se aplicam aos fragmentos de conteúdo.

* **Principal**

   * Uma parte do fragmento

      * Cada fragmento de conteúdo tem uma instância Principal.
      * O Principal não pode ser excluído.

   * O Principal pode ser acessado no editor de fragmentos, em **[Variações](/help/assets/content-fragments/content-fragments-variations.md)**.
   * O Principal não é uma variação em si, mas a base de todas as variações.

* **Variações**

   * Representações de texto de fragmento específicas para um objetivo editorial; podem estar relacionadas a canais, mas não é obrigatório. Também podem ser para modificações locais ad hoc.
   * São criadas como cópias de **Mestre**, mas podem ser editadas conforme necessário. Há sobreposição de conteúdo entre as próprias variações.
   * Podem ser definidas durante a criação do fragmento.
   * São armazenadas no fragmento para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [sincronizadas](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) com o Principal se o conteúdo do Principal tiver sido atualizado.
   * Podem ser [resumidas](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rapidamente o texto em um comprimento predefinido.
   * Disponíveis na guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) do editor de fragmentos.

### Conteúdo intermediário ao criar páginas com fragmentos de conteúdo {#in-between-content-when-page-authoring-with-content-fragments}

Conteúdo intermediário:

* Disponível para uso no Editor de páginas ao trabalhar com Fragmentos de conteúdo.
* [Conteúdo adicional que é adicionado dentro do fluxo de um fragmento](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-in-between-content) depois de ser usado ou referenciado em uma página.
* Disponível para uso no [Editor de páginas ao trabalhar com Fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md).
* O conteúdo intermediário pode ser adicionado a qualquer fragmento onde há apenas um elemento visível.
* O conteúdo associado pode ser usado, assim como os ativos e/ou componentes do navegador apropriado.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Ele não é armazenado no fragmento de conteúdo.

### Exigido por fragmentos {#required-by-fragments}

Para criar fragmentos de conteúdo, é necessário:

* **Modelo de conteúdo**

   * É [habilitado usando o Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * É [criado usando Ferramentas](/help/assets/content-fragments/content-fragments-models.md).
   * Obrigatório para [criar um fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições do modelo de conteúdo exigem um título e um elemento de dados; todo o resto é opcional.
   * O modelo pode definir o conteúdo padrão, se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento.
   * As alterações feitas em um modelo após a criação de fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

Para usar os Fragmentos de conteúdo para a criação de páginas, também é necessário:

* **Componente Fragmento de Conteúdo**

   * Fundamental para entregar o fragmento no formato HTML, JSON ou ambos.
   * Obrigatório para [fazer referência ao fragmento em uma página](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsável pelo layout e entrega de um fragmento (ou seja, os canais).
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associa automaticamente o componente necessário.

## Reutilizar fragmentos de conteúdo com o MSM {#reusing-content-fragments-with-msm}

Quando acessado por meio do console **Assets**, você pode usar o MSM e criar Live Copies para seus fragmentos.

Para obter mais detalhes, consulte:

* [Reutilizar fragmentos de conteúdo usando o MSM](/help/assets/content-fragments/content-fragments-msm.md)
* [Reutilizar ativos usando o MSM para Assets](/help/assets/reuse-assets-using-msm.md).

Eles habilitam a [herança](/help/assets/content-fragments/content-fragments-variations.md#inheritance) para variações e campos individuais dos fragmentos.

>[!CAUTION]
>
>Se você quiser usar o MSM (que cria cópias de Fragmentos de conteúdo), qualquer restrição **única** deverá ser removida de qualquer Tipo de dados usado nos respectivos [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md).

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, considere o que é usado e onde é usado.

### Amostra do WKND {#wknd-sample}

As amostras do [Site WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) são fornecidas para ajudá-lo a aprender sobre o AEM as a Cloud Service.

O projeto WKND inclui:

* Modelos de fragmentos de conteúdo disponíveis em:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
