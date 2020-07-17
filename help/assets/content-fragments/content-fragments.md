---
title: Trabalho com fragmentos de conteúdo
description: Saiba como os Fragmentos de conteúdo no Adobe Experience Manager (AEM) como Cloud Service permitem que você crie, crie, prepare e use conteúdo independente de página.
translation-type: tm+mt
source-git-commit: a5b0d8789a50974c5b633feb5a84824b5999916c
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 6%

---


# Trabalho com fragmentos de conteúdo{#working-with-content-fragments}

With Adobe Experience Manager (AEM) as a Cloud Service, Content Fragments allow you to design, create, curate and [publish page-independent content](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Eles permitem que você prepare conteúdo pronto para uso em vários locais/em vários canais.

Fragmentos de conteúdo contêm conteúdo estruturado:

* Eles são baseados em um Modelo [de fragmento de](/help/assets/content-fragments/content-fragments-models.md)conteúdo, que predefine uma estrutura para o fragmento resultante.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo Sling (JSON) dos componentes principais do AEM. Esta forma de delivery:

* permite que você use o componente para gerenciar quais elementos de um fragmento fornecer
* permite delivery em massa, adicionando vários componentes do fragmento do conteúdo na página que está sendo usada para o delivery da API

Esta e as seguintes páginas cobrem as tarefas para criar, configurar e manter seus fragmentos de conteúdo:

* [Gerenciamento de fragmentos](/help/assets/content-fragments/content-fragments-managing.md) de conteúdo - crie seus fragmentos de conteúdo; em seguida, edite, publique e faça referência
* [Modelos](/help/assets/content-fragments/content-fragments-models.md) de fragmento de conteúdo - ativar, criar e definir seus modelos
* [Variações - Criação de conteúdo](/help/assets/content-fragments/content-fragments-variations.md) do fragmento - cria o conteúdo do fragmento e as variações do Principal
* [Marcação](/help/assets/content-fragments/content-fragments-markdown.md) - uso da sintaxe de marcação para o fragmento
* [Usar conteúdo](/help/assets/content-fragments/content-fragments-assoc-content.md) associado - adicionar conteúdo associado
* [Metadados - Propriedades](/help/assets/content-fragments/content-fragments-metadata.md) do fragmento - exibir e editar as propriedades do fragmento

>[!NOTE]
>
>Essas páginas devem ser lidas juntamente com a Criação de [páginas com fragmentos](/help/sites-cloud/authoring/fundamentals/content-fragments.md)de conteúdo.

O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo do delivery, como:

* canal físico; por exemplo, desktop, móvel.
* Forma de delivery num canal físico; Por exemplo, &quot;página de detalhes do produto&quot;, &quot;página de categoria do produto&quot; para desktop ou &quot;Web móvel&quot;, &quot;aplicativo móvel&quot; para dispositivos móveis.

No entanto, você (provavelmente) não deseja usar exatamente o mesmo conteúdo para todos os canais - é necessário otimizar o conteúdo de acordo com o canal específico.

Fragmentos de conteúdo permitem:

* Considere como atingir audiências públicos alvos com eficiência em todos os canais.
* Crie e gerencie conteúdo editorial neutro ao canal.
* Crie pools de conteúdo para uma variedade de canais.
* Projete variações de conteúdo para canais específicos.
* Adicione imagens ao texto inserindo ativos (fragmentos de mídia mista).

Esses fragmentos de conteúdo podem ser montados para fornecer experiências em vários canais.

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os serviços de conteúdo do AEM foram criados para generalizar a descrição e o delivery do conteúdo de/para o AEM, além do foco nas páginas da Web.

Eles fornecem o delivery do conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos móveis nativos
* outros canais e pontos de contato externos ao AEM

O Delivery é feito no formato JSON usando o Exportador JSON.

Fragmentos de conteúdo do AEM podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter diversos tipos de conteúdo; incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Junto com os recursos de exportação JSON dos componentes principais do AEM, esse conteúdo estruturado pode ser usado para fornecer conteúdo do AEM a canais diferentes das páginas do AEM.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**são recursos diferentes no AEM:
>* **Fragmentos** de conteúdo são conteúdos editoriais, que podem ser usados para acessar dados estruturados, incluindo textos, números e datas, entre outros. Eles são conteúdo puro, com definição e estrutura, mas sem design visual e/ou layout adicionais.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.

>
>
Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte também [Compreensão de fragmentos de conteúdo e fragmentos de experiência no AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html).

>[!NOTE]
>
>O AEM também oferece suporte à tradução do conteúdo do fragmento. Consulte Criar projetos de tradução para fragmentos de conteúdo para obter mais informações.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Armazenado como **ativos**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos no console **Ativos** .
   * Autorizado e editado no Editor de fragmentos de conteúdo.

* Usado no editor de [páginas por meio do componente](/help/sites-cloud/authoring/fundamentals/content-fragments.md) Fragmento de conteúdo (componente de referência):

   * O componente Fragmento **do** conteúdo está disponível para autores de páginas. Isso permite que eles façam referência e entreguem o fragmento de conteúdo necessário no formato HTML ou JSON.

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* Estão sem layout ou design (alguma formatação de texto é possível no modo Rich Text).
* Conter uma ou mais partes [constituintes](#constituent-parts-of-a-content-fragment).
* Pode [conter ou estar conectado a imagens](#fragments-with-visual-assets).
* Pode usar conteúdo [intermediário](#in-between-content-when-page-authoring-with-content-fragments) quando referenciado em uma página.

* São independentes do mecanismo do delivery (ou seja, página, canal).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para dar aos autores mais controle de seu conteúdo, as imagens podem ser adicionadas e/ou integradas a um fragmento de conteúdo.

Os ativos podem ser usados com um fragmento de conteúdo de várias maneiras; cada um com as suas próprias vantagens:

* **Inserir ativo** em um fragmento (fragmentos de mídia mista)

   * São parte integrante do fragmento (consulte Partes [constituintes de um fragmento](#constituent-parts-of-a-content-fragment)de conteúdo).
   * Defina a posição do ativo.
   * Consulte [Inserir ativos no fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) no Editor de fragmentos para obter mais informações.

   >[!NOTE]
   >
   >Os ativos visuais inseridos no fragmento de conteúdo propriamente dito são anexados ao parágrafo anterior. Quando o fragmento é adicionado a uma página, esses ativos são movidos em relação a esse parágrafo quando o conteúdo intermediário é adicionado.

* **Conteúdo associado**

   * Estão conectados a um fragmento; mas não uma parte fixa do fragmento (consulte Partes [constituintes de um fragmento](#constituent-parts-of-a-content-fragment)de conteúdo).
   * Permite alguma flexibilidade para posicionamento.
   * São facilmente disponíveis para uso (como conteúdo intermediário) ao usar o fragmento em uma página.
   * Consulte Conteúdo [associado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obter mais informações.

* Ativos disponíveis no **navegador Ativos** do editor de página

   * Permitir flexibilidade total para a seleção de um ativo.
   * Permite alguma flexibilidade para posicionamento.
   * Não fornece o conceito de aprovação para um fragmento específico.
   * Consulte Navegador [de](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) ativos para obter mais informações.

### Componentes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do fragmento de conteúdo são compostos pelas seguintes partes (direta ou indiretamente):

* **Elementos de fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Use um modelo de conteúdo para criar o fragmento de conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de vários tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, muitas vezes com várias linhas, que são delimitados como entidades individuais.

   * Nos modos [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Marcação](/help/assets/content-fragments/content-fragments-variations.md#markdown), um parágrafo pode ser formatado como um cabeçalho, nesse caso ele e o parágrafo a seguir pertencem como uma unidade.

   * Ative o controle de conteúdo durante a criação de páginas.

* **Ativos inseridos em um fragmento (fragmentos de mídia mista)**

   * Ativos (imagens) inseridos no fragmento real e usados como conteúdo interno de um fragmento.
   * São incorporados ao sistema de parágrafo do fragmento.
   * Pode ser formatado quando o [fragmento é usado/referenciado em uma página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Só pode ser adicionado, excluído ou movido dentro de um fragmento usando o editor de fragmentos. Essas ações não podem ser feitas no editor de páginas.
   * Só pode ser adicionado, excluído ou movido dentro de um fragmento usando o formato [Rich Text no editor](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)de fragmentos.
   * Só pode ser adicionado a elementos de texto de várias linhas (qualquer tipo de fragmento).
   * São anexadas ao texto anterior (parágrafo).

   >[!CAUTION]
   >
   >Pode ser (inadvertidamente) removido de um fragmento alternando para o formato Texto simples.

   >[!NOTE]
   >
   >Os ativos também podem ser adicionados como conteúdo [](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) adicional (intermediário) ao usar um fragmento em uma página; usando Conteúdo associado ou ativos do navegador Ativos.

* **Conteúdo associado**

   * Esse é um conteúdo externo a, mas com relevância editorial para, um fragmento. Geralmente, imagens, vídeos ou outros fragmentos.
   * Os ativos individuais dentro da coleção estão disponíveis para serem usados com o fragmento no editor de página, quando ele é adicionado a uma página. Isso significa que eles são opcionais, dependendo dos requisitos do canal específico.
   * Os ativos estão [associados a fragmentos por meio de coleções](/help/assets/content-fragments/content-fragments-assoc-content.md); as coleções associadas permitem que o autor decida quais ativos usar ao criar a página.

      * As coleções podem ser associadas a fragmentos como conteúdo padrão ou por autores durante a criação de fragmentos.
      * [Coleções](/help/assets/manage-collections.md) de ativos (DAM) são a base para o conteúdo associado de fragmentos.
   * Opcionalmente, você também pode adicionar o fragmento em si a uma coleção para ajudar no rastreamento.

* **Metadados de fragmento**

   * Use os schemas [de metadados do](/help/assets/metadata-schemas.md)Assets.
   * As tags podem ser criadas quando você:

      * Criar e criar o fragmento
      * Ou posterior:

         * Ao exibir/editar as **Propriedades** do fragmento no console
         * Ao editar os **Metadados** no editor de fragmentos

   >[!CAUTION]
   >
   >Os perfis de processamento de metadados não se aplicam aos Fragmentos de conteúdo.

* **Mestre**

   * Parte integrante do fragmento

      * Cada fragmento de conteúdo tem uma instância de Principal.
      * Principal não pode ser excluído.
   * Principal pode ser acessado no editor de fragmentos em **[Variações](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Principal não é uma variação enquanto tal, mas a base de todas as variações.


* **Variações**

   * Representações de texto de fragmento específicas para fins editoriais; pode estar relacionado com o canal, mas não é obrigatório, pode também ser feito para modificações locais ad hoc.
   * São criados como cópias de **Principais**, mas podem ser editados conforme necessário; normalmente há sobreposição de conteúdo entre as próprias variações.
   * Pode ser definido durante a criação do fragmento.
   * Armazenado no fragmento, para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [sincronizadas](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) com o Principal se o conteúdo Principal tiver sido atualizado.
   * Pode ser [resumido](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rapidamente o texto em um comprimento predefinido.
   * Disponível na guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) do editor de fragmentos.

### Conteúdo intermediário ao criar páginas com fragmentos de conteúdo {#in-between-content-when-page-authoring-with-content-fragments}

Conteúdo intermediário:

* Está disponível para uso no Editor de páginas ao trabalhar com Fragmentos de conteúdo.
* É conteúdo [adicional adicionado no fluxo de um fragmento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) depois que ele é usado/referenciado em uma página.
* Está disponível para uso no Editor [de páginas ao trabalhar com Fragmentos](/help/sites-cloud/authoring/fundamentals/content-fragments.md)de conteúdo.
* O conteúdo intermediário pode ser adicionado a qualquer fragmento, onde apenas um elemento está visível.
* O conteúdo associado pode ser usado, assim como ativos e/ou componentes do navegador apropriado.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Não é armazenado no fragmento de conteúdo.

### Necessário por fragmentos {#required-by-fragments}

Para criar, editar e usar fragmentos de conteúdo, você também precisa:

* **Modelo de conteúdo**

   * São [ativados e criados usando Ferramentas](/help/assets/content-fragments/content-fragments-models.md).
   * Necessário para [criar um fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tags).
   * As definições dos modelos de conteúdo exigem um título e um elemento de dados; tudo o resto é opcional.
   * O modelo pode definir o conteúdo padrão - se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento.
   * As alterações feitas em um modelo após a criação de fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

* **Componente do fragmento do conteúdo**

   * Instrumental para entregar o fragmento em formato HTML e/ou JSON.
   * Necessário para [fazer referência ao fragmento em uma página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Responsável pelo layout e delivery de um fragmento; ou seja, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associará automaticamente o componente necessário.

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que será usado em qualquer lugar.

### Amostra de WKND {#wknd-sample}

As amostras do site [](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND são fornecidas para ajudá-lo a saber mais sobre o AEM como Cloud Service. Inclui fragmentos de amostra, que podem ser vistos em:

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`
