---
title: Fragmentos de experiência
description: Use os Fragmentos de experiência no Adobe Experience Manager as a Cloud Service para tornar suas experiências reutilizáveis e flexíveis.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
solution: Experience Manager Sites
feature: Authoring, Experience Fragments
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 91%

---

# Fragmentos de experiência {#experience-fragments}

No Adobe Experience Manager as a Cloud Service, um fragmento de experiência:

* é um grupo de um ou mais componentes
* inclui conteúdo e layout
* pode ser referenciado nas páginas
* pode conter qualquer componente

Um fragmento de experiência:

* Faz parte de uma experiência (página).
* Pode ser usado em várias páginas (com base em modelos editáveis).
* É baseado em um modelo (somente editável) para definir a estrutura e os componentes.
* Esse modelo é usado para criar a *página raiz* do Fragmento de experiência.
* É composto de um ou mais componentes, com layout, em um sistema de parágrafos.
* Pode conter outros fragmentos de experiência.
* Podem ser combinados com outros componentes (incluindo outros Fragmentos de experiência) para formar uma página completa (experiência).
* Uma ou mais variações podem ser criadas, com base na página raiz.
* Essas variações podem compartilhar conteúdo e/ou componentes.
* Pode ser dividida em blocos de construção que poderão ser usados em várias variações do fragmento.

Use os Fragmentos de experiência:

* Se um autor quiser reutilizar partes (um fragmento de uma experiência) de uma página.
Sem Fragmentos de experiência, o autor precisaria copiar e colar esse fragmento. Criar e manter essa experiências de copiar/colar é um processo demorado e pode causar erros feitos pelo usuário.
Os fragmentos de experiência eliminam a necessidade de copiar/colar.
* Para dar suporte ao caso de uso de CMS sem periféricos.
Os autores desejam usar o AEM somente para criação, não para entrega ao cliente. Um sistema/ponto de contato de terceiros consumiria essa experiência e depois a entregaria ao usuário.
* Com o [Gerenciamento de vários sites (MSM)](/help/sites-cloud/administering/msm/overview.md); o como um Fragmento de experiência faz parte de uma página. Isso se aplica aos fragmentos individuais e às pastas em que eles residem.

>[!NOTE]
>
>**[Fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md)** e **fragmentos de experiência** são recursos diferentes no AEM:
>
>* Os **fragmentos de conteúdo** são conteúdos editoriais com definição e estrutura, mas sem design visual e/ou layout adicional. Eles podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte [Noções sobre os fragmentos de conteúdo e fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

>[!NOTE]
>
>O acesso de gravação para fragmentos de experiência exige que a conta de usuário seja registrada no grupo:
>
>* `experience-fragments-editors`
>
>Entre em contato com o administrador do sistema se tiver algum problema.

## Quando usar fragmentos de experiência?   {#when-should-you-use-experience-fragments}

Fragmentos de experiência devem ser usados:

* Sempre que quiser reutilizar as experiências.
   * Experiências reutilizadas com conteúdo igual ou semelhante.
* Ao usar o AEM como uma plataforma de entrega de conteúdo para terceiros.
   * Qualquer solução que deseje usar AEM como a plataforma de entrega de conteúdo.
   * Incorporação de conteúdo em pontos de contato de terceiros.
* Se você tiver uma experiência com diferentes variações ou representações.
   * Variações específicas de canal ou contexto.
   * Experiências que fazem sentido agrupar; por exemplo, uma campanha com diferentes experiências entre canais.
* Quando você usar o Comércio omnichannel.
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
  >Você pode usar o [editor de modelos](/help/sites-cloud/authoring/page-editor/templates.md) para criar seu próprio modelo.

O projeto WKND estrutura alguns Fragmentos de experiência de acordo com `Contributors`. A estrutura usada também ilustra a maneira como outros recursos, como o Gerenciamento de vários sites (incluindo cópias de idiomas), podem ser usados.

Consulte:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Pastas para Fragmentos de experiência](/help/sites-cloud/authoring/assets/xf-folders.png)

## Criação e configuração de uma pasta para os Fragmentos de experiência {#creating-and-configuring-a-folder-for-your-experience-fragments}

Para criar e configurar uma pasta para os Fragmentos de experiência, recomenda-se:

1. [Criar uma pasta](/help/sites-cloud/authoring/sites-console/managing-pages.md#creating-a-new-folder).

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

   É obrigatório ter um **título**. Se **Nome** for deixado em branco, ele será derivado do **Título**.

   ![Propriedades de Fragmentos de experiência](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >As tags do modelo do fragmento de experiência não serão unidas com tags nesta página raiz do fragmento de experiência.
   >
   >Elas são completamente separadas.

1. Clique em **Criar**.

   Uma mensagem será exibida. Selecione:

   * **Concluído** para retornar ao console
   * **Abrir** para abrir o editor de fragmento

## Edição de seu fragmento de experiência {#editing-your-experience-fragment}

O Editor de fragmento de experiência oferece recursos semelhantes ao editor de páginas normal.

>[!NOTE]
>
>Consulte [Editar conteúdo da página](/help/sites-cloud/authoring/page-editor/edit-content.md) para obter mais informações sobre como usar o editor de páginas.

O exemplo de procedimento a seguir ilustra como criar um teaser de um produto:

1. Arraste e solte o componente desejado do [Navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

1. Dependendo do componente:
   * Adicione qualquer conteúdo e/ou ativo, conforme necessário.
   * Configure as propriedades conforme necessário.

1. Adicione mais componentes conforme necessário.

Por exemplo: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Fragmento de experiência na página](/help/sites-cloud/authoring/assets/xf-05.png)

## Criação de uma variação de Fragmento de experiência {#creating-an-experience-fragment-variation}

É possível criar variações do Fragmento de experiência, dependendo das suas necessidades:

1. Abra o fragmento para [edição](#editing-your-experience-fragment).
1. Abra a guia **Variações**.

   ![Criação de uma variação de Fragmento de experiência](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Criar** permite criar:

   * **Variação**
   * **Variação como Live Copy**.

     >[!NOTE]
     >
     >Criar uma variação inicial como Live Copy herdará o título usando a Source da Live Copy como a variação principal.

1. Defina as propriedades necessárias:

   * **Modelo**
   * **Título**
   * **Nome**: se deixado em branco, ele será derivado do Título
   * **Descrição**
   * **Tags de variação**

   Por exemplo:

   ![Propriedades de variação](/help/sites-cloud/authoring/assets/xf-07.png)


1. Confirme com **Concluído**, a nova variação será mostrada no painel.

## Usar seu fragmento de experiência {#using-your-experience-fragment}

Agora você poderá usar seu fragmento de experiência ao criar suas páginas:

1. Abra qualquer página para edição.

   >[!NOTE]
   >
   >A página deve ser baseada em um modelo editável.

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

Para criar um Bloco de Construção:

1. No editor de Fragmento de experiência, selecione os componentes que deseja reutilizar:

   ![Selecionar componente para Bloco de Construção](/help/sites-cloud/authoring/assets/xf-09.png)

1. Na barra de ferramentas dos componentes, selecione **Converter em bloco de construção**:

   ![Botão Bloco de construção](/help/sites-cloud/authoring/assets/xf-10.png)

1. Insira o nome do **Bloco de construção** e confirme com **Converter**:

   ![Nomear bloco de construção](/help/sites-cloud/authoring/assets/xf-11.png)

1. O **Bloco de construção** será mostrado na guia esquerda (**Local**) e pode ser selecionado para mais ações:

   ![Bloco de construção no painel](/help/sites-cloud/authoring/assets/xf-12.png)

#### Gerenciar um bloco de construção {#managing-a-building-block}

O bloco de construção está visível na guia **Blocos de construção**. Para cada bloco, as seguintes ações estarão disponíveis:

* **Acesse o mestre**: abra a variação da página raiz em uma nova guia
* **Renomeie**
* **Excluir**

![Gerenciar blocos de construção](/help/sites-cloud/authoring/assets/xf-13.png)

#### Usar um bloco de construção {#using-a-building-block}

Arraste o bloco de construção para o sistema de parágrafo de qualquer fragmento, como com qualquer componente.

Ao editar um Fragmento de experiência disponível, os Blocos de construção são exibidos na guia à esquerda. Você pode filtrar de acordo com:

* **Local** - blocos de construção no Fragmento de experiência atual
* **Todos** - blocos de construção de todos os fragmentos

![Seleção de blocos de construção](/help/sites-cloud/authoring/assets/xf-14.png)

## Personalização no seu fragmento de experiência {#personalization-experience-fragment}

A personalização no Fragmento de experiência permite que você, como profissional de marketing, defina públicos-alvo para o Fragmento de experiência apenas uma vez e, em seguida, reutilize o fragmento em qualquer página. Isto:

* elimina a necessidade de especificar as variações necessárias para cada público-alvo sempre que o fragmento for usado
* mantém o estilo nas ofertas

Você pode criar um Fragmento de experiência com vários componentes agrupados dentro desse único fragmento. Você também pode criar variações do fragmento para cada segmento de público-alvo específico e reutilizar esses Fragmentos de experiência nos canais necessários.

A personalização é alcançada definindo as propriedades de **Personalização** no Fragmento de experiência ou na variação, ou na pasta que contém os fragmentos; isso significa que a herança pode substituir as propriedades de personalização.

A configuração dessas propriedades também habilita o modo **Direcionamento** no editor de Fragmento de experiência.

### Definição de personalização para seu Fragmento de experiência {#defining-personalization-experience-fragment}

Para personalizar o fragmento:

1. Navegue até o local desejado no console **Fragmentos de experiência**.

1. Selecione uma pasta ou o fragmento e clique em **Propriedades** na barra de ferramentas.

   >[!NOTE]
   >
   >As propriedades de personalização definidas em uma pasta são herdadas por todas as pastas filhas abaixo na subárvore e os Fragmentos de experiência (e variações) dentro dessa subárvore. Elas podem ser substituídas quebrando a herança.

1. Abra a guia **Personalização** para definir e salvar suas configurações. Por exemplo, em uma pasta:

   ![Fragmento de experiência - Propriedades de personalização](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >Quando um fragmento é incorporado em uma página do Sites e a **Personalização** estiver configurada, então somente a versão da página com a personalização será usada na hora da renderização.
   >
   >Para que o direcionamento executado nos componentes de um fragmento funcione na renderização da página, as seguintes condições devem ser atendidas:
   >
   >O **Caminho do ContextHub** selecionado na guia **Personalização** deve ser:
   >
   >* o mesmo caminho que o configurado para a página em que o fragmento é renderizado
   >
   >  Ou:
   >
   >* um caminho que contenha um subconjunto dos armazenamentos definidos no ContextHub configurado para a página
   >
   >O **Caminho dos Segmentos** selecionado na guia **Personalization** deve ser:
   >
   >* o mesmo caminho que o configurado para a página em que o fragmento é renderizado
   >
   >  Ou
   >
   >* um caminho que contenha um subconjunto dos segmentos configurados para a página

### Definição de direcionamento para seu Fragmento de experiência {#defining-targeting-experience-fragment}

Após configurar as propriedades de personalização, o modo Direcionamento estará disponível quando o fragmento for aberto para edição.

![Editor de fragmento de experiência - Modo de direcionamento](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

Esse modo opera da mesma maneira que para edição de página. Consulte [Modo de direcionamento para o Editor de páginas](/help/sites-cloud/authoring/personalization/targeted-content.md) para obter mais detalhes.

## Detalhes do Fragmento de experiência {#details-of-your-experience-fragment}

Os detalhes do fragmento podem ser vistos:

1. Navegue até o local dos Fragmentos de experiência (não navegue além das variações dentro do fragmento).
Os detalhes são mostrados em todas as exibições do console **Fragmentos de experiência**, com a de **Exibição em lista**, incluindo detalhes de uma [exportação para o Target](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![Detalhes do fragmento de experiência](/help/sites-cloud/authoring/assets/xf-15.png)

1. Ao abrir as **Propriedades** do fragmento de experiência:

   ![Botão Propriedades](/help/sites-cloud/authoring/assets/xf-16.png)

   As propriedades estão disponíveis em várias guias:

   >[!CAUTION]
   >
   >Essas guias são exibidas quando você abre **Propriedades** no console Fragmentos de experiência.
   >
   >Se você clicar em **Abrir propriedades** ao editar um Fragmento de experiência, as [Propriedades da página](/help/sites-cloud/authoring/sites-console/page-properties.md) apropriadas serão exibidas.

   ![Propriedades do fragmento de experiência](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Básico**
      * **Título** - obrigatório
      * **Descrição**
      * **Tags**
      * **Número total de variantes** - somente informações
      * **Número de variantes da Web** - somente informações
      * **Número de variantes que não são da Web** - somente informações
      * **Número de páginas usando esse fragmento** - somente informações
   * **Cloud Services**
      * **Configuração na nuvem**
      * **Configurações do Cloud Service**
      * **ID da página do Facebook**
      * **Quadro do Pinterest**
   * **Referências**
      * Uma lista de referências
   * **Personalização**
      * **Caminho do ContextHub**
      * **Caminho de segmentos**
      * **Marca**

## A representação HTML simples {#the-plain-html-rendition}

Usando o seletor `.plain.` no URL, você poderá acessar a representação HTML simples a partir do navegador.

>[!NOTE]
>
>Embora isso esteja diretamente disponível no navegador, [o objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos da Web de terceiros, implementações móveis personalizadas) acessem o conteúdo do fragmento de experiência diretamente, usando apenas o URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Publicação de fragmentos de experiência {#publishing-experience-fragments}

Publicar seu fragmento de experiência é basicamente o mesmo que [publicar uma página](/help/sites-cloud/authoring/sites-console/publishing-pages.md) (mas diretamente do console ou do editor de fragmentos de experiência).

Como alternativa, também é possível [publicar para visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) (novamente diretamento do console ou do editor de fragmentos de experiência).

>[!CAUTION]
>
>Por padrão, publicando a pasta raiz dos Fragmentos de experiência (localizados diretamente em `/content/experience-fragments`):
>
>* publica somente a própria pasta do contêiner
>* não publica nenhum filho
>* cancela a publicação de qualquer filho já publicado
>
>Para publicação de todos os Fragmentos de experiência na pasta, cada um deve ser publicado separadamente.

## Exportar fragmentos de experiência {#exporting-experience-fragments}

Por padrão, os fragmentos de experiência são entregues no formato HTML. Isso pode ser usado por canais do AEM e de terceiros.

Para exportar para o Adobe Target, também é possível usar o JSON. Consulte:

* [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportar fragmentos de experiência para o Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
