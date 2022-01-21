---
title: Fragmentos de experiência
description: Use os Fragmentos de experiência do Adobe Experience Manager as a Cloud Service para tornar suas experiências reutilizáveis e flexíveis.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: 229e2d8252a9efe1e303e926bde6719387833fa9
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 99%

---

# Fragmentos de experiência {#experience-fragments}

No Adobe Experience Manager as a Cloud Service, um fragmento de experiência:
* é um grupo de um ou mais componentes
* inclui conteúdo e layout
* pode ser referenciado nas páginas
* pode conter qualquer componente

Um fragmento de experiência:

* É parte de uma experiência (página).
* Pode ser usado em várias páginas.
* É baseado em um modelo (somente editável) para definir a estrutura e os componentes.
* É composto por um ou mais componentes, com layout, em um sistema de parágrafos.
* Pode conter outros fragmentos de experiência.
* Pode ser combinado com outros componentes (incluindo outros Fragmentos de experiência) para formar uma página completa (experiência).
* Pode apresentar variações diferentes e pode compartilhar conteúdo e/ou componentes.
* Pode ser dividida em blocos de construção que poderão ser usados em várias variações do fragmento.

Use os Fragmentos de experiência:

* Se um autor quiser reutilizar partes (um fragmento de uma experiência) de uma página.
Sem Fragmentos de experiência, o autor precisaria copiar e colar esse fragmento. Criar e manter essa experiências de copiar/colar é um processo demorado e pode causar erros feitos pelo usuário.
Os fragmentos de experiência eliminam a necessidade de copiar/colar.
* Para dar suporte ao caso de uso de CMS sem periféricos.
Os autores desejam usar o AEM somente para criação, não para entrega ao cliente. Um ponto de contato ou sistema de terceiros consumiria essa experiência e a entregaria para o usuário final.

>[!NOTE]
>
>O acesso de gravação para fragmentos de experiência requer que a conta de usuário seja registrada no grupo:
>
>* `experience-fragments-editors`
>
>Entre em contato com o administrador do sistema se você tiver problemas.

## Quando você deve usar fragmentos de experiência?   {#when-should-you-use-experience-fragments}

Os fragmentos de experiência devem ser usados:

* Sempre que você quiser reutilizar experiências.
   * Experiências que serão reutilizadas com o mesmo conteúdo ou com conteúdo semelhante.
* Ao usar o AEM como uma plataforma de distribuição de conteúdo para terceiros.
   * Qualquer solução que desejar usar o AEM como a plataforma de distribuição de conteúdo.
   * Ao incorporar conteúdo em pontos de contato de terceiros.
* Se você tiver uma Experiência com variações ou execuções diferentes.
   * Canal ou variações específicas ao contexto.
   * Experiências que fazem sentido agrupar; por exemplo, uma campanha com diferentes experiências entre canais.
* Quando você usar o Comércio omnichannel.
   * Ao compartilhar conteúdo comercial em canais de [redes sociais](/help/implementing/developing/extending/experience-fragments.md#social-variations) em escala.
   * Tornar pontos de toque transacionais.

## Organizar os Fragmentos de experiência {#organizing-your-experience-fragments}

Recomenda-se:
* usar pastas para organizar os Fragmentos de experiência,

* [configurar os modelos permitidos nessas pastas](#configure-allowed-templates-folder).

A criação de pastas permite:

* criar uma estrutura significativa para os Fragmentos de experiência; por exemplo, de acordo com a classificação

   >[!NOTE]
   >
   >Não é necessário alinhar a estrutura dos Fragmentos de experiência com a estrutura de página do site.

* [alocar os modelos permitidos no nível da pasta](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >Você pode usar o [editor de modelos](/help/sites-cloud/authoring/features/templates.md) para criar seu próprio modelo.

O projeto WKND estrutura alguns Fragmentos de experiência de acordo com `Contributors`. A estrutura usada também ilustra a maneira como outros recursos, como o Gerenciamento de vários sites (incluindo cópias de idiomas), podem ser usados.

Consulte:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Pastas para Fragmentos de experiência](/help/sites-cloud/authoring/assets/xf-folders.png)

## Criação e configuração de uma pasta para os Fragmentos de experiência {#creating-and-configuring-a-folder-for-your-experience-fragments}

Para criar e configurar uma pasta para os Fragmentos de experiência, recomenda-se:

1. [Criar uma pasta](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [Configurar os modelos de Fragmento de experiência permitidos para essa pasta](#configure-allowed-templates-folder).

>[!NOTE]
>
>Também é possível configurar os [Modelos permitidos para sua instância](#configure-allowed-templates-instance), mas esse método **não** é recomendado, pois os valores podem ser substituídos na atualização.

### Configurar os Modelos permitidos para sua Pasta {#configure-allowed-templates-folder}

>[!NOTE]
>
>Esse é o método recomendado para especificar os **Modelos permitidos**, pois os valores não serão substituídos na atualização.

1. Acesse a pasta **Fragmentos de experiência** necessária.

1. Selecione a pasta e depois as **Propriedades**.

1. Especifique a expressão regular para recuperar os modelos necessários no campo **Modelos permitidos**.

   Por exemplo:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Consulte:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Propriedades dos fragmentos de experiência - Modelos permitidos](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Consulte [Modelos para fragmentos de experiência](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) para obter mais detalhes.

1. Selecione **Salvar e fechar**.

### Configurar os Modelos permitidos para sua Instância {#configure-allowed-templates-instance}

>[!CAUTION]
>
>Não é recomendável alterar os **Modelos permitidos** usando esse método, pois os modelos especificados podem ser substituídos na atualização.
>
>Use esta caixa de diálogo apenas para fins informativos.

1. Acesse o console **Fragmentos de experiência** necessário.

1. Selecione **Opções de configuração**:

   ![Botão Configuração](/help/sites-cloud/authoring/assets/xf-18.png)

1. Especifique os modelos necessários na caixa de diálogo **Configurar fragmentos de experiência**:

   ![Configurar fragmentos de experiência](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Consulte [Modelos para fragmentos de experiência](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) para obter mais detalhes.

1. Selecione **Salvar**.


## Criação de um fragmento de experiência {#creating-an-experience-fragment}

Para criar um fragmento de experiência:

1. Selecione **Fragmentos de experiência** na Navegação global.

   ![Fragmentos de experiência no painel Navegação](/help/sites-cloud/authoring/assets/xf-01.png)

1. Navegue até a pasta desejada e selecione **Criar**:

   ![Criação de uma pasta para Fragmentos de experiência](/help/sites-cloud/authoring/assets/xf-02.png)

1. Selecione **Fragmento de experiência** para abrir o assistente **Criar fragmento de experiência**.

   Selecione o **modelo** obrigatório e, em seguida, clique em **Avançar**:

   ![Seleção de um modelo de Fragmento de experiência](/help/sites-cloud/authoring/assets/xf-03.png)


1. Insira as **Propriedades** do **Fragmento de experiência**.

   É obrigatório ter um **título**. Se o **Nome** for deixado em branco, ele será derivado do **Título**.

   ![Propriedades do fragmento de experiência](/help/sites-cloud/authoring/assets/xf-04.png)

1. Clique em **Criar**.

   Uma mensagem será exibida. Selecionar:

   * **Concluído** para retornar ao console
   * **Abrir** para abrir o editor de fragmento

## Edição de seu fragmento de experiência {#editing-your-experience-fragment}

O Editor de fragmento de experiência oferece recursos semelhantes ao editor de páginas normal.

>[!NOTE]
>
>Consulte [Edição de conteúdo de página](/help/sites-cloud/authoring/fundamentals/editing-content.md) para obter mais informações sobre como usar o Editor de páginas.

O exemplo de procedimento a seguir ilustra como criar um teaser para um produto:

1. Arraste e solte o componente desejado do [Navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. Dependendo do componente:
   * Adicione qualquer conteúdo e/ou ativo, conforme necessário.
   * Configure as propriedades conforme necessário.

1. Adicione mais componentes conforme necessário.

Por exemplo: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Fragmento de experiência na página](/help/sites-cloud/authoring/assets/xf-05.png)

## Criação de uma variação de Fragmento de experiência {#creating-an-experience-fragment-variation}

Você pode criar variações de seu fragmento de experiência, de acordo com suas necessidades:

1. Abra o fragmento para [edição](#editing-your-experience-fragment).
1. Abra a guia **Variações**.

   ![Criação de uma variação de Fragmento de experiência](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Criar** permite criar:

   * **Variação**
   * **Variação como Live Copy**.

1. Defina as propriedades necessárias:

   * **Modelo**
   * **Título**
   * **Nome** - se deixado em branco, ele será derivado do Título
   * **Descrição**
   * **Tags de variação**

   Por exemplo:

   ![Propriedades de variação](/help/sites-cloud/authoring/assets/xf-07.png)

1. Confirme com **Concluído**, a nova variação será mostrada no painel.

## Usar seu fragmento de experiência {#using-your-experience-fragment}

Agora você pode usar o Fragmento de experiência ao criar suas páginas:

1. Abra qualquer página para edição.

1. Crie uma instância do componente Fragmento de experiência, no sistema de parágrafos da página:

1. Adicione o Fragmento de experiência real à ocorrência de componente:

   * Arraste o fragmento necessário do Navegador de Ativos e solte no componente.
   * Selecione **Configurar** na barra de ferramentas do componente e especifique o fragmento a ser usado, confirme com **Concluído**.

   >[!NOTE]
   >
   >Editar, na barra de ferramentas do componente, opera como um atalho para abrir o fragmento no editor de fragmentos.

Por exemplo: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Fragmento de experiência no editor de páginas](/help/sites-cloud/authoring/assets/xf-08.png)

## Blocos de construção {#building-blocks}

Selecione um ou mais componentes para criar um bloco de construção para reciclagem no seu fragmento:

### Criar um bloco de construção {#creating-a-building-block}

Para criar um novo Bloco de construção:

1. No editor Fragmento de experiência, selecione os componentes que deseja reutilizar:

   ![Selecionar componente para Bloco de Construção](/help/sites-cloud/authoring/assets/xf-09.png)

1. Na barra de ferramentas dos componentes, selecione **Converter em bloco de construção**:

   ![Botão Bloco de construção](/help/sites-cloud/authoring/assets/xf-10.png)

1. Insira o nome do **Bloco de construção** e confirme com **Converter**:

   ![Nomear bloco de construção](/help/sites-cloud/authoring/assets/xf-11.png)

1. O **Bloco de construção** será mostrado na guia esquerda (**Local**) e poderá ser selecionado para outras ações:

   ![Bloco de construção no painel](/help/sites-cloud/authoring/assets/xf-12.png)

#### Gerenciar um bloco de construção {#managing-a-building-block}

O bloco de construção está visível na guia **Blocos de construção**. As seguintes ações estão disponíveis para cada bloco:

* **** Acesse o mestre: abra a variação mestre em uma nova guia
* **Renomeie**
* **Excluir**

![Gerenciar blocos de construção](/help/sites-cloud/authoring/assets/xf-13.png)

#### Usar um bloco de construção {#using-a-building-block}

Arraste o bloco de construção para o sistema de parágrafo de qualquer fragmento, como com qualquer componente.

Ao editar um Fragmento de experiência disponível, os Blocos de construção são exibidos na guia à esquerda. Você pode filtrar de acordo com:

* **Local** - blocos de construção no Fragmento de experiência atual
* **Todos** - blocos de construção de todos os fragmentos

![Seleção de blocos de construção](/help/sites-cloud/authoring/assets/xf-14.png)

## Detalhes do Fragmento de experiência {#details-of-your-experience-fragment}

Os detalhes do fragmento podem ser vistos:

1. Navegue até o local dos Fragmentos de experiência (não navegue além das variações dentro do fragmento).
Os detalhes são mostrados em todas as exibições do console **Fragmentos de experiência**, com a **de Exibição em lista**, incluindo detalhes de uma exportação para o Target: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Detalhes do fragmento de experiência](/help/sites-cloud/authoring/assets/xf-15.png)

1. Ao abrir as **Propriedades** do fragmento de experiência:

   ![Botão Propriedades](/help/sites-cloud/authoring/assets/xf-16.png)

   As propriedades estão disponíveis em várias guias:

   >[!CAUTION]
   >
   >Essas guias são exibidas quando você abre **Propriedades** no console Fragmentos de experiência.
   >
   >Se você clicar em **Abrir propriedades** ao editar um Fragmento de experiência, as [Propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md) apropriadas serão exibidas.

   ![Propriedades do fragmento de experiência](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Básico**
      * **Título** - obrigatório
      * **Descrição**
      * **Tags**
      * **Número total de variantes** - somente informações
      * **Número de variantes da Web** - somente informações
      * **Número de variantes que não são da Web** - somente informações
      * **Número de páginas que usam este fragmento** - somente informações
   * **Cloud Services**
      * **Configuração na nuvem**
      * **Configurações do Cloud Service**
      * **ID da Página do Facebook**
      * **Pasta do Pinterest**
   * **Referências**
      * Uma lista de referências
   * **Status da rede social**
      * Detalhes de variações de redes sociais

## A representação HTML simples {#the-plain-html-rendition}

Usando o seletor `.plain.` no URL, você poderá acessar a representação HTML simples do navegador.

>[!NOTE]
>
>Embora isso esteja disponível diretamente no navegador, [o principal objetivo é permitir outros aplicativos (por exemplo, aplicativos Web de terceiros, implementações móveis personalizadas) para acessar o conteúdo do Fragmento de experiência diretamente, usando apenas o URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Exportar fragmentos de experiência   {#exporting-experience-fragments}

Por padrão, os fragmentos de experiência são entregues no formato HTML. Isso pode ser usado pelo AEM e por canais de terceiros.

Para exportar para o Adobe Target, consulte [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

<!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
