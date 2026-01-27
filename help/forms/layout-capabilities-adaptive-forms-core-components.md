---
title: Quais são os recursos de layout do Adaptive Forms com base nos componentes principais?
description: O layout e as aparências do Adaptive Forms em vários dispositivos são regidos pelas configurações de layout. Entenda os vários layouts e como aplicá-los.
feature: Adaptive Forms, Core Components
keywords: Layout do formulário adaptável com base nos componentes principais, Layouts diferentes para formulários, AEM de layouts dinâmicos de formulário, Layouts de formulário do AEM Cloud Service, Tipos de layout de formulário nos Componentes principais do AEM, Layouts de formulário adaptável
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 1%

---

# Recursos de layout do Forms adaptável com base nos componentes principais


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html) |
| AEM as a Cloud Service (Componentes de base) | [Clique aqui](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service (Componentes principais) | Este artigo |

O Forms adaptável fornece componentes de primeira classe para layout e design de formulários com eficiência. O layout controla como os componentes são exibidos em um formulário. O Forms adaptável é compatível com vários layouts: painel, assistente, acordeão, guias em guias superiores/horizontais e guias em guias esquerdas/verticais.

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## Aplicabilidade e casos de uso

### Seguros

## A AEM Forms oferece suporte a formulários de solicitação de seguro em várias etapas?

Sim. O AEM Forms oferece suporte a formulários adaptáveis guiados em várias etapas com lógica condicional, permitindo que as seguradoras coletem informações sobre solicitações progressivamente com base no tipo e no contexto da solicitação.

## Os clientes podem fazer upload de documentos de solicitação com segurança usando o AEM Forms?

Sim. O AEM Forms oferece suporte ao upload seguro de documentos como parte dos envios de formulários, com controles de acesso e tratamento seguro de dados alinhados aos requisitos de segurança da empresa.


## Tipos de layout adaptáveis do Forms

O formulário adaptável baseado em Componentes principais é compatível com os seguintes tipos de layouts:

* **Layout do painel**
* **Layout do assistente**
* **Layout vertical**
* **Layout horizontal**
* **Layout da opção**

>[!BEGINTABS]

>[!TAB Layout do painel]

O layout do painel é útil para organizar campos relacionados de uma maneira que facilite a navegação e a localização do conteúdo correspondente. O layout do painel organiza os componentes do formulário em seções ou painéis distintos em um Formulário adaptável.

![Layout do painel](/help/forms/assets/panel-layout.png)

Layout do painel

Você pode usar o [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para adicionar o layout do painel em um formulário. Para obter instruções detalhadas sobre como configurar várias propriedades do componente do painel, consulte o artigo [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

>[!TAB Layout do Assistente]

O layout do assistente ajuda a simplificar um formulário complexo, dividindo-o em etapas distintas. Cada etapa representa uma parte diferente do processo, e os usuários navegam pelas etapas sequencialmente, geralmente com os botões **Próximo** e **Anterior**. Você pode usar o layout do assistente para criar um formulário que envolve várias seções ou etapas.

![Layout do Assistente](/help/forms/assets/wizard-layout-compare.gif)

Layout do assistente

Você pode usar o [componente de assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para adicionar o layout de assistente em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente do assistente, consulte o artigo [componente do assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

>[!TAB Layout de Guias Verticais]

O layout de guias verticais também é conhecido como guias no layout esquerdo. O layout de guias verticais organiza painéis ou seções no lado esquerdo de um formulário. É um layout comum para formulários em que os painéis/seções são empilhados verticalmente para facilitar a leitura e a navegação.

![Layout vertical](/help/forms/assets/vertical-tab.gif)

Layout de guias verticais

Você pode usar o [componente de guias verticais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) para adicionar o layout de guias verticais em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente de guias verticais, consulte o artigo [componente de guias verticais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs).


>[!TAB Layout de Guias Horizontais]

O layout de guias horizontais também é conhecido como Guias no layout superior. O layout de guias horizontais organiza os painéis ou as seções lado a lado em uma linha. Este layout apresenta as seções do formulário de maneira linear na largura do formulário ou painel.


![Layout horizontal](/help/forms/assets/horizontal-layout.gif)

Layout de Guias Horizontais

Você pode usar o [componente de guias horizontais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) para adicionar o layout de guias horizontais em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente de guias horizontais, consulte o artigo [componente de guias horizontais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs).


>[!TAB Layout da opção]

O layout do Accordion exibe o conteúdo em seções ou painéis que podem ser recolhidos em um Formulário adaptável. Quando uma seção é expandida, ela exibe o conteúdo em, enquanto outras seções permanecem recolhidas. Esse layout é ideal para exibir grandes quantidades de informações em um formato compacto.

![Layout da opção](/help/forms/assets/accordion-layout-compare.gif)

Layout do acordeão

Você pode usar o [componente Acordeão](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para adicionar o layout acordeão em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente Acordeão, consulte o artigo [componente Acordeão](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

>[!ENDTABS]

Para saber como inserir um layout e adicionar componentes de formulário a ele, consulte a seção intitulada [Como inserir um layout e adicionar componentes de formulário a ele?](#how-to-insert-a-layout-and-add-form-components-to-it)

### Como escolher o layout de formulário adaptável correto?

É importante selecionar o layout de formulário adaptável correto para otimizar a experiência do usuário e a funcionalidade do formulário. A tabela ajuda você a entender as diferentes opções de layout disponíveis e orienta você a selecionar o layout mais adequado com base nas suas necessidades e casos de uso específicos:

| Destaque | Layout do painel | Layout do assistente | Guias no Layout de Guias Superior/Vertical | Guias no Layout de Guias à Esquerda/Horizontal | Layout do acordeão |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **Finalidade** | Agrupa conteúdo relacionado em seções distintas | Orienta os usuários por meio de um processo ou formulário de várias etapas | Permite alternar entre seções/exibições na mesma página | Semelhante às abas superiores, mas organizado verticalmente à esquerda | Organiza o conteúdo em seções que podem ser recolhidas |
| **Estrutura** | Seções distintas | Etapas/páginas sequenciais | Guias horizontais na parte superior | Guias verticais à esquerda | Painéis/seções flexíveis |
| **Navegação** | Clique nos cabeçalhos do painel para navegar | - Avançar: botão &quot;Avançar&quot;<br>- Voltar: botão &quot;Voltar&quot;<br>- Etapas de ignorar opcionais | Clique nas guias para trocar de seção | Clique nas guias para trocar de seção | Clique em cabeçalhos para expandir/recolher seções |
| **Experiência do usuário** | Organiza grandes quantidades de conteúdo de maneira gerenciável | Orientação passo a passo, reduzindo a sobrecarga | Alternância clara e acessível entre exibições | Uso eficiente do espaço vertical, guias sempre visíveis | Exibição compacta com seções expandidas/recolhidas |
| **Caso de uso** | Formulários complexos com seções categorizadas | Processos de configuração, formulários complexos | Organizar configurações ou categorias de conteúdo | Painéis, visualizações de dados complexas | Perguntas frequentes, menus de configurações e seções detalhadas de conteúdo |


## Como inserir um layout e adicionar componentes de formulário a ele?

O diagrama abaixo exibe as etapas para inserir um layout em um formulário e adicionar componentes de formulário a ele:

![Fluxo de trabalho para adicionar um layout e componentes de formulário](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

Considere o **Formulário de solicitação de TI** mostrado na seção [Tipos de layout adaptáveis do Forms](#adaptive-forms-layout-types). O formulário reúne informações de funcionários com problemas técnicos relacionados à rede ou ao laptop. Ele inclui três painéis:

* **Detalhes do Funcionário**: o painel coleta informações sobre o funcionário e contém três caixas de texto rotuladas Nome, ID de Email e Departamento.

* **Detalhes do problema**: o painel captura detalhes sobre o problema. Ela inclui uma caixa de seleção para a categoria de problema com três opções: Rede, Computador ou Outro. Ele também apresenta duas caixas de texto rotuladas Especifique e Comentários.

* **Anexos**: o painel permite que os usuários carreguem documentos de suporte relacionados ao problema.

Vamos explorar o processo passo a passo para inserir um layout e adicionar componentes a ele. Neste exemplo, um layout de guias horizontais é inserido em um formulário.

### &#x200B;1. Inserir um componente de layout em um formulário

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. No canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Abra um formulário adaptável existente em um modo de edição se ele já tiver sido criado.

   ![Abrir um Formulário Adaptável](/help/forms/assets/insert-layout.png)

   Como alternativa, você também pode [criar um novo Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md).

1. Localize a seção no construtor de formulários que permite adicionar um layout.

   ![Construtor de formulários](/help/forms/assets/form-editor.png)
1. Clique no ícone **Adicionar**. O ícone é um sinal de mais (+) que significa a opção de adicionar novos componentes.

   ![Inserir layout](/help/forms/assets/insert-layout-add-icon.png)

   Clicar no ícone **Adicionar** exibe uma caixa de diálogo **Inserir novo componente** que exibe vários componentes para inserção.

   >[!NOTE]
   >
   > Como alternativa, você também pode [arrastar e soltar o componente de layout](#extra-bytes).

1. Navegue pelos componentes disponíveis na caixa de diálogo e selecione o layout desejado na lista. No nosso caso, selecionamos o componente de Guias horizontais para inserir o layout de guias horizontais.

   ![Selecionar guias horizontais](/help/forms/assets/select-horizontal-tab.png)

   Ao adicionar o componente de guias horizontais ao formulário, ele consiste inicialmente em dois painéis vazios, chamados Item1 e Item2, por padrão. É necessário adicionar manualmente os componentes do formulário a esses painéis.

   ![Guias horizontais](/help/forms/assets/insert-tabs-on-top.png)

1. Abra as propriedades do componente de guias horizontais e especifique o nome do componente.
Por exemplo, nesse caso, adicionamos o nome do componente de guias horizontais como Formulário de solicitação de TI.

   ![Adicionar nome para guias horizontais](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. Clique em **Concluído**.

   ![Guias horizontais](/help/forms/assets/tabs-on-top-rename-component.png)

Depois que o componente de layout for adicionado ao formulário, modifique o número de painéis de acordo com os requisitos.

### &#x200B;2. Adicionar painéis ao layout

Adicionar novo painel ao componente de guias horizontais:

1. Abra as propriedades do componente de guias horizontais e clique na guia **Itens**.

   ![Guia Item para guias Horizontais](/help/forms/assets/tabs-on-top-items-tab.png)

1. Clique no ícone **Adicionar** para adicionar um novo painel.

   ![Adicionar novo painel](/help/forms/assets/tabs-on-top-add-panel.png)

   Ao clicar no ícone **Adicionar**, a caixa de diálogo **Inserir novo componente** é exibida.

1. Selecione o componente Painel.

   ![Adicionar novo painel](/help/forms/assets/tabs-on-top-new-panel.png)

   Quando você seleciona o componente Painel, o novo painel é adicionado no layout horizontal.

   ![Adicionar novo painel](/help/forms/assets/tabs-on-top-add-new-panel.png)

   Forneça um nome para o novo painel; caso contrário, não será possível salvar as propriedades do componente de guias horizontais.

1. Especifique os nomes dos painéis, conforme mostrado na figura abaixo:

   ![Nomes do painel](/help/forms/assets/tabs-on-tops-panel-name.png)

1. Clique em **Concluído**.

   Depois de clicar em **Concluído**, os três painéis aparecerão lado a lado em uma linha. Os nomes dos painéis são exibidos como cabeçalhos para cada painel e você pode adicionar componentes de formulário a cada painel.

   ![Nomes do painel](/help/forms/assets/tabs-on-top-initial-view.png)

   É possível configurar as propriedades do componente do painel. Por exemplo, o Formulário de solicitação de TI não inclui títulos de painel, estas são as etapas para configurar as propriedades do componente do painel.

1. Abra as propriedades do primeiro painel.

   Propriedades do ![Painel 1](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. Marque a caixa de seleção **Ocultar título** na guia **Básico**.

   ![Ocultar título](/help/forms/assets/tabs-on-top-hide-panel.png)

1. Clique em **Concluído**.

Da mesma forma, também é possível ocultar títulos dos outros dois painéis. Depois de concluído, você pode continuar com a adição de componentes de formulário a cada painel.

### &#x200B;3. Adicionar componentes de formulário ao painel

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. Localize a seção no painel que permite adicionar componentes.
1. Clique no ícone **Adicionar**. O ícone é um sinal de mais (+) que significa a opção de adicionar novos componentes.
   ![Inserir layout](/help/forms/assets/tabs-on-top-add-component.png)

   Clicar no ícone **Adicionar** exibe uma caixa de diálogo **Inserir novo componente** que exibe vários componentes para inserção.

   ![Caixa de Diálogo Inserir Novo Componente](/help/forms/assets/insert-new-component.png)

1. Navegue pelos componentes disponíveis na caixa de diálogo exibida e selecione o componente desejado. Em nosso caso, selecione o componente Caixa de texto.
1. Abra as propriedades do componente adicionado e especifique seu nome. Deixe editar as propriedades do componente Caixa de texto adicionado e especifique seu nome.
   ![Inserir layout](/help/forms/assets/tabs-on-top-textbox-component.png)
1. Da mesma forma, adicione mais dois componentes Caixa de texto e o nome adicionou os componentes como ID de email e Departamento.\
   ![Primeiro Painel](/help/forms/assets/tabs-on-tops-first-panel.png)

   Agora que os componentes no primeiro painel foram adicionados, você pode continuar com a adição dos componentes ao segundo painel.

1. Para alternar o painel, clique em **Selecionar Painel** na barra de ferramentas.

   ![Painel de Opções](/help/forms/assets/tabs-on-top-select-panel.png)

   Ao clicar em **Selecionar painel**, a lista de painéis adicionados no componente Guias horizontais é exibida.

   ![Painel de Opções](/help/forms/assets/tabs-on-tops-panel2.png)

1. Selecione **2 Painel** na lista do painel e a exibição será alterada do primeiro para o segundo painel.

   ![Segundo Painel](/help/forms/assets/tabs-on-top-panel2-component.png)

1. Repita as etapas descritas da Etapa 2 para a Etapa 4 para adicionar os componentes desejados no painel 2, como mostrado na figura abaixo:

   ![Componentes do segundo painel](/help/forms/assets/panel-2-components.png)

1. Alterne para o **3 Painel** seguindo as etapas descritas nas Etapas 6 e 7.

1. Repita as etapas descritas da Etapa 2 para a Etapa 4 para adicionar o componente desejado no painel 3:

   ![Componentes do terceiro painel](/help/forms/assets/panel-3-component.png)

1. Clique em **[!UICONTROL Visualizar]** no canto superior direito do seu ambiente de criação.
   ![Layout horizontal](/help/forms/assets/horizontal-layout.gif)

Você também pode [arrastar e soltar os componentes](#extra-bytes) para adicionar os componentes de formulário a cada painel.


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



Você também pode excluir o componente de formulário do painel usando o ícone ![Excluir](/help/forms/assets/Smock_Delete_18_N.svg).

![Excluindo um componente](/help/forms/assets/delete-component.png)

Você também pode adicionar as validações necessárias para os componentes, conforme necessário.

## Como substituir um layout existente por um novo layout?

É possível substituir um layout de um formulário por um novo layout, o que envolve modificar como os componentes são organizados e exibidos em um formulário.

Execute as seguintes etapas para substituir o layout existente de um formulário:

1. Clique no ícone Substituir na barra de ferramentas do componente de layout e a caixa de diálogo **[!UICONTROL Substituir componente]** será exibida.

   ![Substituir layout](/help/forms/assets/replace-layout.png)

1. Selecione o layout desejado na caixa de diálogo **[!UICONTROL Substituir Componente]**.

   ![Caixa de diálogo Substituir Componente](/help/forms/assets/replace-component.png)

   Após selecionar o layout, a disposição dos componentes dentro do layout muda de acordo. Por exemplo, selecione o componente de guias verticais na caixa de diálogo **[!UICONTROL Substituir componente]**; a organização do painel muda para guias à esquerda:

   ![Layout vertical](/help/forms/assets/vertical-tab.gif)

## Bytes extras

Para arrastar e soltar componentes no construtor de formulários, execute as seguintes etapas:

1. Localize a seção que permite adicionar componentes.
1. Navegue até o painel esquerdo em seu ambiente de criação e clique em **Componentes**.

   ![Painel do componente](/help/forms/assets/add-new-component.png)

   Ao clicar na opção **Componentes**, a lista dos componentes disponíveis é exibida.

   ![Painel do componente](/help/forms/assets/add-new-component2.png)

1. Navegue pelos componentes disponíveis e selecione o componente desejado.

1. Arraste o componente clicando e segurando o componente selecionado, em seguida, arraste-o sobre a área do painel para colocá-lo.

1. Solte o componente no painel soltando o mouse.

## Próximas etapas

Depois de conhecer os vários recursos de layout de um Formulário adaptável com base nos Componentes principais, você pode seguir para as próximas etapas:

* [Crie seu primeiro formulário adaptável com base nos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)
* [Criar e usar temas do formulário adaptável](/help/forms/using-themes-in-core-components.md)



## Consulte também

{{see-also}}
