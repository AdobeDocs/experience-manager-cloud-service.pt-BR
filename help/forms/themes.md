---
title: Criar e usar temas para estilizar um formulário adaptável
description: É possível usar temas para estilizar e fornecer uma identidade visual para um formulário adaptável. Você pode compartilhar um tema em qualquer número de adaptadores Forms.
exl-id: 99c3d1f7-5756-49d2-98ee-72dd62063110
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 1%

---

# Criação e uso de temas {#creating-and-using-themes}

É possível criar e aplicar temas para estilizar um formulário adaptável<!-- or an interactive communication-->. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes. O tema é gerenciado de maneira independente sem uma referência a um formulário adaptável<!-- or interactive communication -->.

Você pode baixar e instalar [!DNL AEM Forms] pacote de conteúdo de referência de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal para importar temas e modelos de referência para o seu ambiente.

## Criação, download ou upload de um tema {#creating-downloading-or-uploading-a-theme}

Um tema é criado e salvo como uma entidade separada, completa com meta-propriedades como o Adaptive Forms. Permite reutilizar um tema em vários Forms adaptáveis<!-- or  and interactive communications-->. Você também pode mover um tema para uma instância diferente e reutilizá-lo.

### Criação de um tema {#creating-a-theme}

Para criar um tema:

1. Clique em **[!UICONTROL Adobe Experience Manager]**, clique em **[!UICONTROL Forms]** e clique em **[!UICONTROL Temas]**.

1. Na página Temas , clique em **[!UICONTROL Criar]** > **[!UICONTROL Tema]**.
Um assistente para criar um tema é iniciado.

1. Especificar **[!UICONTROL Nome]** do tema.

1. Especifique um formulário para visualizar o tema na **[!UICONTROL Visualização Padrão para este Tema]** campo. Clique em **[!UICONTROL Usar padrão]** para usar o formulário padrão para visualizar o tema.

1. Especifique um **[!UICONTROL Contêiner de configuração]**. Você pode escolher uma **[!UICONTROL Contêiner de configuração]** que contém detalhes de configuração do Adobe Font para sua conta. Você também pode deixar a opção em branco por enquanto e especificar os detalhes posteriormente de [propriedades do tema](#metadata-of-a-theme).

1. Clique em **[!UICONTROL Criar]** e, em seguida, clique em **[!UICONTROL Editar]** para abrir o tema no Editor de Temas ou clique em **[!UICONTROL Concluído]** para retornar à página de temas.

### Diferença de temas no Experience Manager 6.5 Forms e versões anteriores {#difference-in-themes}

Temas criados em uma instância do Cloud Service:

* Ter a versão número 2.

* São armazenadas em `/content/dam/formsanddocuments-themes/<theme-name>/`

* Não forneça a opção da biblioteca do cliente. Não é possível especificar uma categoria e um caminho da biblioteca do cliente.

* Não tenha permissões de gravação e atualização no local /apps (o grupo de usuários do Forms não tem permissão de gravação e atualização no local /apps).

* Antes de fazer upload de um tema criado em [!DNL Experience Manager Forms] 6.5 ou versões anteriores para uma instância do Cloud Service, verifique se o local da biblioteca do cliente está definido como `etc/clientlibs/fd/themes`. Se a biblioteca do cliente não existir no `etc` , atualize manualmente o local para `etc/clientlibs/fd/themes`.  Você pode fazer a alteração no seu [!DNL Experience Manager Forms] Instância 6.5 ou versões anteriores. Após definir a localização da biblioteca do cliente, um administrador pode fazer upload de temas para a instância do Cloud Service ou usar a ferramenta Transferência de conteúdo para migrar os temas das instâncias 6.5 ou da versão anterior para a instância do Cloud Service.

   Além disso, altere o nome da categoria. Se o nome não for alterado, ocorrerá um erro `theme with same category name exists` pode ocorrer. Quando você altera o nome da categoria, isso não afeta o Adaptive Forms que usa o tema.

### Download de um tema {#downloading-a-theme}

Você pode exportar temas como um arquivo zip e usar esses temas em outros projetos ou instâncias do Experience Manager. Para baixar um tema:

1. Clique em **[!UICONTROL Adobe Experience Manager]**, clique em **[!UICONTROL Forms]** e, em seguida, clique em **[!UICONTROL Temas]**.

1. Na página Temas , **[!UICONTROL Selecionar]** um tema e clique em **[!UICONTROL Baixar]**. Uma caixa de diálogo com os detalhes do tema é exibida.

1. Clique em **[!UICONTROL Baixar]**. O tema é baixado como um arquivo zip.

>[!NOTE]
>
>Se você baixar um tema que tem um Formulário adaptativo associado a ele e o Formulário adaptativo associado for baseado em um modelo personalizado, então também baixe o modelo personalizado. Ao fazer upload do tema baixado e do Formulário adaptativo, faça upload do modelo personalizado relacionado também.

### Fazer upload de um tema {#uploading-a-theme}

Um usuário com privilégios de administrador pode fazer upload de um tema criado em [!DNL Experience Manager Forms] 6.5 ou versões anteriores.

Para fazer upload de um tema:

1. Clique em **[!UICONTROL Adobe Experience Manager]**, clique em **[!UICONTROL Forms]** e, em seguida, clique em **[!UICONTROL Temas]**.

1. Na página Temas , clique em **[!UICONTROL Criar]** > **[!UICONTROL Upload de arquivo]**.
1. No prompt Upload de arquivo, procure e selecione um pacote de temas no seu computador e clique em **[!UICONTROL Upload]**.
O tema carregado está disponível na página de temas.

## Metadados de um tema {#metadata-of-a-theme}

Lista de meta-propriedades de um tema (encontrada na página de propriedades de um tema).

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>Nome</strong></th>
   <th><strong>Pode ser editado</strong></th>
   <th><strong>Descrição da propriedade</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>Título</td>
   <td>Sim</td>
   <td>Nome de exibição do tema.</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>Descrição</td>
   <td>Sim</td>
   <td>Descrição sobre o tema.</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>Tipo</td>
   <td>Não</td>
   <td>
    <ul>
     <li>Tipo de ativo.</li>
     <li>Valor é sempre Tema.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>Criado</td>
   <td>Não</td>
   <td>Data de criação do tema</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>Nome do autor</td>
   <td>Sim</td>
   <td>Autor do tema. Calculado no momento da criação do tema.</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>Data da última modificação</td>
   <td>Não</td>
   <td>Data em que o tema foi modificado pela última vez.</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>Status</td>
   <td>Não</td>
   <td>Status do tema (Modificado/Publicado).</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>Data de início da publicação</td>
   <td>Sim</td>
   <td>Tempo para publicar o tema automaticamente.</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>Data de término da publicação</td>
   <td>Sim</td>
   <td>Tempo para desfazer a publicação automática do tema.</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>Tags</td>
   <td>Sim</td>
   <td>Um rótulo anexado ao tema para identificação usado para melhorar a pesquisa.</td>
  </tr>
  <!-- <tr>
   <td>11.</td>
   <td>References</td>
   <td>Links</td>
   <td>
    <ul>
     <li>Contains 'Referred by' section. Lists forms that use the theme.</li>
     <li>Since the theme does not refer to any other asset, there is no 'Refers' section.</li>
    </ul> </td>
  </tr>
   <tr>
   <td>12.</td>
   <td>Clientlib Location</td>
   <td>Yes</td>
   <td>
    <ul>
     <li>The user-defined repository path within '/etc' where the clientlibs corresponding to this theme are stored.</li>
     <li>Default value - '/etc/clientlibs/fd/themes' + relative path of theme asset.</li>
     <li>If the location does not exist, the folder hierarchy is auto-generated.</li>
     <li>When this value is changed, the clientlib node structure is moved to the new location entered.<br /> <em><strong>Note:</strong> If you change default clientlib location, in the CRXDE repository assign <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>to <code>forms-users</code> and <code>crx:replicate</code>, <code>jcr:read </code>to <code>fd-service</code> in the new location. Also attach another ACL by adding <code>deny jcr:addChildNodes</code> for <code>forms-user</code></em></li>
    </ul> </td>
  </tr> 
  <tr>
   <td>13.</td>
   <td>Clientlib Category Name</td>
   <td>Yes</td>
   <td>
    <ul>
     <li>The user-defined clientlib category name for this theme.</li>
     <li>An error is displayed if the name is already in use by some other existing theme.</li>
     <li>Default value - computed using theme location.</li>
     <li>When this value is changed, the category name is updated on the corresponding clientlib node. Updating Clientlib Category Name in the jsp files is not required because clientlib category name is used by reference.</li>
    </ul> </td>
  </tr> -->
 </tbody>
</table>

## Sobre o Editor de Temas {#about-the-theme-editor}

O Editor de Temas é uma interface amigável para usuários empresariais e web designer/desenvolvedor que fornece as funcionalidades necessárias para especificar o estilo de vários Formulários Adaptativos <!-- and interactive communication --> elementos facilmente. Ao criar um tema, ele é armazenado como uma entidade separada, como formulários <!--  , interactive communications, letters, document fragments, and data dictionaries-->.

O Editor de Temas permite personalizar estilos dos componentes estilizados em um tema. Você pode personalizar como um formulário <!-- or interactive communication --> procura em um dispositivo.

O Editor de Temas é dividido em dois painéis:

* **Tela** - Aparece no lado direito. Ele mostra um exemplo de formulário adaptável <!--  or interactive communication --> em que todas as alterações de estilo refletem instantaneamente. Também é possível selecionar objetos diretamente da tela para procurar estilos associados a eles e editar esses estilos. Uma régua de resolução de dispositivo na parte superior governa a Tela. Selecionar um ponto de interrupção de resolução na régua mostra a visualização do formulário de amostra <!--  or interactive communication --> para a respectiva resolução. Tela é discutida em detalhes [below](themes.md#using-canvas).

* **Barra lateral**- Aparece no lado esquerdo. Ela tem os seguintes itens:

   * **Seletor:** Mostra o componente selecionado para estilo e suas propriedades que podem ser estilizadas. O seletor representa todos os componentes de um tipo. Se você selecionar um componente de caixa de texto em um tema para estilo, todas as caixas de texto em seu formulário <!-- or interactive communication --> herde o estilo. Os seletores permitem selecionar um componente genérico ou um componente específico para o estilo. Por exemplo, um componente de campo é um componente genérico e uma caixa de texto é um componente específico.

      **Componente genérico de estilo:**
Um campo pode ser um campo de caixa numérica, como idade, ou um campo de caixa de texto, como endereço.
Ao criar um estilo em um campo, todos os campos, como idade, nome, endereço, são estilizados.

      **Componente específico de estilo**: Um componente específico afeta objetos da categoria específica. Ao criar o estilo do componente de caixa numérica no tema, somente o objeto de caixa numérica no herda o estilo.

      Por exemplo, um campo de caixa de texto, como endereço que é maior e um campo de caixa numérica, como idade, é menor. É possível selecionar um campo de caixa numérica, reduzir seu comprimento e aplicar ao formulário. A largura de todos os campos de caixa numérica é reduzida no formulário.

      Ao personalizar todos os componentes do campo com uma cor de plano de fundo específica, todos os campos, como idade, nome e endereço, herdam a cor de plano de fundo. Ao selecionar uma caixa numérica, como idade, e reduzir sua largura, largura de todas as caixas numéricas, como idade, o número de pessoas em uma família é reduzido. A largura das caixas de texto não é alterada.

   * **Estado:** Permite personalizar estilos de um objeto em um estado específico. Por exemplo, você pode especificar a aparência de um objeto quando ele estiver no padrão, foco, desativado, passar o mouse ou estado de erro.
   * **Categorias de propriedades:** As propriedades de estilo são divididas em várias categorias. Por exemplo, Dimension e posição, texto, plano de fundo, borda e efeitos. Em cada categoria, você fornece informações de estilo. Por exemplo, em Plano de fundo, você pode fornecer Cor do plano de fundo, Imagem e gradiente.

   * **Avançado:** Permite adicionar CSS personalizado a um objeto, que substitui as propriedades que os controles visuais definem se houver uma sobreposição.

   * **Exibir CSS**: Permite que você visualize o CSS do componente selecionado.
   Além disso, na Barra lateral, na parte inferior, uma seta está presente. Ao clicar na seta, você terá mais duas opções: **Simular sucesso** e **Erro Simulado.** Essas opções, juntamente com as opções descritas acima, são discutidas em detalhes [below](themes.md#using-rail).

[ ![Editor de temas](assets/themes.png)](assets/themes-1.png) **A.** Barra lateral **B.** Tela

### Componentes de estilo {#styling-components}

Você pode usar um tema em vários Forms adaptáveis<!-- and interactive communications -->, que importa a formatação do componente especificada no tema. Você pode criar estilo em vários componentes, como títulos, descrição, painéis, campos, ícones e caixas de texto. Use widgets para configurar as propriedades do componente em um tema. O conhecimento anterior de CSS ou LESS não é necessário, mas é desejado, embora a seção Substituições de CSS permita que você grave o código CSS ou forneça seletores personalizados. A seção Substituições de CSS é exibida ao selecionar um componente na barra lateral.

![Componentes estilizáveis na barra lateral](assets/stylable-components.png)

Opções na barra lateral que permitem selecionar e estilizar componentes diferentes.

Clicar no botão Editar em relação a um componente na barra lateral seleciona o componente na Tela e permite estilizar o componente usando opções na barra lateral.

Determinados componentes, como caixa de texto, caixa numérica, botão de opção e caixa de seleção, são categorizados em componentes genéricos, como Campo. Por exemplo, você deseja personalizar o estilo dos botões de opção. Para selecionar botões de opção para estilo, selecione **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Botão de opção]**.

### Layouts de painel de estilo {#styling-panel-layouts-br}

Temas em [!DNL AEM Forms] oferecem suporte ao estilo de elementos no layout de painéis em seus formulários<!-- and  interactive communications -->. O estilo de elementos em layouts prontos e layouts personalizados é compatível.

Os painéis prontos para uso incluem:

* Guias na esquerda
* Guias na parte superior
* Acordeão
* Receptivo
* Assistente
* Layout móvel

   * Títulos do painel no cabeçalho
   * Sem títulos de painel no cabeçalho

Os seletores variam para cada layout.
O estilo de layouts personalizados no Editor de Temas envolve:

* Definir os componentes de um layout que pode ser estilizado e os seletores de CSS para identificar esses componentes exclusivamente.
* Definir as propriedades de CSS que podem ser aplicadas a esses componentes.
* Defina o estilo desses componentes interativamente na interface do usuário.

### Estilos diferentes para tamanhos de tela diferentes {#different-styles-for-different-screen-sizes-br}

Os layouts para desktop e dispositivos móveis podem ter estilos ligeiramente ou totalmente diferentes. Para dispositivos móveis, tablets e telefones compartilham layouts semelhantes, exceto para tamanhos de componentes.

Use pontos de interrupção do Editor de Temas para definir estilos alternativos para tamanhos de tela diferentes. Você pode selecionar um dispositivo ou resolução base em que começa a criar o tema e as variações de estilo para outras resoluções são geradas automaticamente. Você pode modificar explicitamente o estilo de todas as resoluções.

>[!NOTE]
>
>O tema é criado primeiro usando um formulário<!-- or interactive communication-->e, em seguida, aplicadas em formulários diferentes<!-- or interactive communications-->. Os pontos de interrupção usados na criação de temas podem ser diferentes do formulário <!-- or interactive communication --> em que o tema é aplicado. As consultas de mídia CSS são baseadas no formulário <!-- or interactive communication --> usado na criação de temas, e não no formulário <!-- or interactive communication --> em que o tema é aplicado.

### Alterar o contexto das propriedades de estilo na barra lateral ao selecionar objetos {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

Quando você seleciona um componente na Tela, suas propriedades de estilo são listadas na barra lateral. Selecione o tipo de objeto e seu estado e forneça seu estilo.

### Estilos usados recentemente no Editor de Temas {#recently-used-styles-in-theme-editor}

O editor de temas armazena em cache até dez estilos aplicados a um componente. Você pode usar os estilos em cache com outro componente de um tema. Os estilos usados recentemente estão disponíveis logo abaixo do componente selecionado na barra lateral como uma caixa de listagem. Inicialmente, a lista de estilos usados recentemente está vazia.

![Biblioteca de ativos](assets/asset-library.png)

Ao criar um estilo em um componente, os estilos são armazenados em cache e listados na caixa de listagem. Neste exemplo, o rótulo da caixa de texto é estilizado para alterar o tamanho e a cor da fonte. Você pode seguir etapas semelhantes para escolher uma imagem ou alterar cores para criar estilo em um componente. Observe como o estilo é armazenado em cache e listado na caixa de listagem quando o estilo do rótulo do campo é alterado.

![Estilo da fonte armazenado em cache para um componente disponível para outro](assets/font-style-cached1.png)

Neste exemplo, o estilo do rótulo do campo é alterado e, quando a Descrição do painel responsivo é selecionada para estilo, uma entrada de lista é adicionada na biblioteca de ativos. A entrada na biblioteca de ativos pode ser usada para alterar o estilo da Descrição do painel responsivo.

Quando um estilo é adicionado na biblioteca de ativos, ele fica disponível para outros temas e na [modo de estilo](inline-style-adaptive-forms.md) da interface do editor de formulários. Da mesma forma, ao usar o modo de estilo do editor de formulários <!-- or interactive communication editor --> Para criar estilo em um componente, o estilo é armazenado em cache e está disponível em temas.

O botão de mais na biblioteca de ativos permite salvar permanentemente o estilo com um nome que você fornece. O botão de adição salva o estilo mesmo se você não clicar no botão Salvar na barra lateral para aplicar o estilo a um componente. O botão de mais para salvar um estilo para uso posterior não está disponível no modo de estilo.

![Fornecer um nome de estilo personalizado para a biblioteca de ativos](assets/custom-style-name.png)

Quando você fornece um nome personalizado para um estilo, o estilo é vinculado a um tema e não está mais disponível para outros temas. Para excluir um estilo salvo:

1. Na barra de ferramentas do CANVAS, clique em **[!UICONTROL Opções de Tema]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Gerenciar estilos]**.
1. Na caixa de diálogo Gerenciar estilos, selecione um estilo salvo e clique em **[!UICONTROL Excluir]**.

   ![Excluir o estilo salvo](assets/manage-styles.png)

### Visualização ao vivo, salvar e descartar alterações {#live-preview-save-and-discard-changes}

As modificações feitas no estilo são refletidas instantaneamente no formulário <!-- or interactive communication --> carregado na Tela. A visualização ao vivo permite que você defina e veja interativamente o impacto do estilo. Quando você altera o estilo de um componente, a variável **[!UICONTROL Concluído]** estiver ativado na barra lateral. Para manter as alterações, use a **[!UICONTROL Concluído]** botão.

>[!NOTE]
>
>Quando um caractere inválido é inserido em um campo, a cor do limite do campo muda para vermelho e uma mensagem de erro é exibida no canto superior esquerdo da tela. Por exemplo, se você digitar alfabetos em uma caixa de texto que aceite caracteres numéricos como entradas, a cor do limite da caixa de entrada será alterada para vermelho. Não é possível salvar esse tema sem resolver o erro exibido na parte inferior central da tela.

### Tema com outro formulário adaptável {#theme-with-another-adaptive-form}

Ao criar um tema, ele é criado com um formulário enviado com o Editor de Temas. Você fornece estilo para componentes neste formulário. Em vez do formulário enviado com o Editor de Temas, você pode selecionar um formulário <!-- or interactive communication --> de sua escolha para fornecer estilo e visualizar seus resultados.

Para substituir o formulário atual ou <!-- interactive communication --> na Tela do Editor de Temas:

1. No painel EDITOR DE TEMAS , clique em **[!UICONTROL Opções de Tema]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configurar]**.

1. Na guia General , navegue e selecione um formulário <!-- or interactive communication --> para **[!UICONTROL Formulário adaptável]** campo.

### Refazer/Desfazer {#redo-undo}

Você pode desfazer ou refazer as alterações indesejadas que ocorrem acidentalmente. Use os botões refazer/desfazer na Tela.

![Refazer e desfazer ações](assets/redo_undo_new.png)

Os botões Refazer/Desfazer aparecem quando você estimula um componente no Editor de Temas.

## Uso do Editor de Temas {#using-the-theme-editor}

O Editor de Temas permite que você edite um tema que você criou ou carregou. Navegar para **[!UICONTROL Forms &amp; Documents]** > **[!UICONTROL Temas]** e selecione um tema e abra-o. O tema é aberto no Editor de Temas.

Como discutido acima, o Editor de Temas tem dois painéis: Barra lateral e Tela de desenho.
![Editor de temas](assets/theme-editor.png)

Personalização do estilo de estado de sucesso do componente de Widget de caixa de texto no Editor de temas. O componente é selecionado na Tela e seu estado é selecionado na barra lateral. As opções de estilo disponíveis na barra lateral são usadas para personalizar a aparência de um componente.

### Uso da Tela de desenho {#using-canvas}

O tema é criado usando o formulário pronto para uso ou usando um formulário <!-- or interactive communication --> de sua escolha. A Tela mostra a visualização do formulário ou <!-- interactive communication --> usado para criar o tema com personalizações especificadas em tema. A régua acima do formulário é usada para determinar o layout de acordo com o tamanho da exibição do dispositivo.

Na barra de ferramentas da Tela, você vê:

* **[!UICONTROL Alternar painel lateral]** ![painel lateral de alternância](assets/toggle-side-panel.png): Permite mostrar ou ocultar a barra lateral.
* **[!UICONTROL Opções de Tema]** ![theme-options](assets/theme-options.png): Fornece três opções

   * Configurar: Fornece opções para selecionar o formulário de visualização <!-- or interactive communication , base clientlib, -->e configuração do Adobe Fonts.
   * Exibir CSS do Tema: Gera CSS para o tema selecionado.
   * Gerenciar estilos: Fornece opções para gerenciar estilos de texto e imagem
   * Ajuda: Executa um tour guiado por imagem do Editor de Temas.

* **[!UICONTROL Emulador]** ![régua](assets/ruler.png): Emula a aparência do seu tema para tamanhos de exibição diferentes. Um tamanho de exibição é tratado como um ponto de interrupção no emulador. Você pode selecionar um ponto de interrupção e especificar um estilo para ele. Por exemplo, Desktop e Tablet são dois pontos de interrupção. Você pode especificar estilos diferentes para cada ponto de interrupção.

Ao selecionar um componente na Tela, você vê a barra de ferramentas do componente na parte superior dela. A barra de ferramentas do componente permite selecionar componentes ou alternar para componentes genéricos. Por exemplo, você seleciona uma caixa de texto numérico em um painel. Você vê as seguintes opções na barra de ferramentas do componente:

* **[!UICONTROL Widget de caixa numérica]**: Permite que você selecione o componente para personalizar sua aparência na barra lateral.
* **[!UICONTROL Widget de campo]**: Permite selecionar o componente genérico para o estilo. Neste exemplo, todos os componentes de entrada de texto (caixa de texto/caixa numérica/etapa numérica/entrada de data) são selecionados para estilo.

* ![nível de campo](assets/select_parent_icon.svg): Permite selecionar o componente principal para o estilo. Se você selecionar uma caixa numérica e tocar nesse ícone, o componente de campo será selecionado. Se você selecionar o componente de campo e tocar nesse ícone, o painel será selecionado. Se você continuar tocando nesse ícone para seleção, acabará selecionando o layout para o estilo.

>[!NOTE]
>
>As opções disponíveis na barra de ferramentas do componente variam de acordo com o componente selecionado.

### Usar barra lateral {#using-rail}

A barra lateral no editor de temas fornece opções para personalizar estilos para componentes em um tema e usar seletores. Os seletores permitem selecionar um grupo de componentes ou componentes individuais, e você pode procurar seletores na barra lateral. Você pode gravar seletores para componentes personalizados.

Quando você seleciona um componente da Tela ou seletores na barra lateral, a barra lateral mostra todas as opções que permitem personalizar estilos para ela.
Abaixo estão as opções exibidas na barra lateral ao selecionar um componente:

* Estado
* Folha de propriedades
* Simular Erro/Sucesso

#### Estado {#state}

Um estado é um indicador da interação do usuário com um componente. Por exemplo, quando um usuário insere dados incorretos em uma caixa de texto, o estado da caixa de texto muda para um estado de erro. O editor de temas permite que você especifique o estilo para um estado específico.

As opções para personalizar estilos de estado variam para componentes diferentes.

#### Folha de propriedades {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Utilização</strong></td>
  </tr>
  <tr>
   <td><p>Dimensões e Posição</p> </td>
   <td><p>Permite estilizar o alinhamento, o tamanho, o posicionamento e o posicionamento dos componentes no tema. </p> <p>Suas opções são configuração de exibição, preenchimento, margem, largura, altura e Índice Z.</p> <p>Você também pode usar o modo Layout para definir a largura dos componentes usando uma interface de arrastar e soltar fácil. Para obter mais informações, consulte <a href="resize-using-layout-mode.md">Usar o modo Layout para redimensionar componentes</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Permite personalizar os estilos de texto no componente do tema.</p> <p>Por exemplo, você deseja alterar a aparência do texto inserido na caixa de texto.</p> <p>Suas opções são família de fontes, peso, cor, tamanho, altura da linha, alinhamento do texto, espaço da letra, recuo do texto, sublinhado, itálico, transformação do texto, alinhamento vertical, linha de base e direção. </p> </td>
  </tr>
  <tr>
   <td><p>Segundo plano </p> </td>
   <td><p>Permite preencher o plano de fundo do componente com uma imagem ou uma cor. </p> </td>
  </tr>
  <tr>
   <td><p>Borda</p> </td>
   <td><p>Permite escolher a aparência da borda de seu componente. Por exemplo, você deseja que a caixa de texto tenha uma borda vermelha profunda e espessa com uma linha pontilhada. </p> <p>Suas opções são largura, estilo, raio e cor da borda.</p> </td>
  </tr>
  <tr>
   <td><p>Efeitos</p> </td>
   <td><p>Permite adicionar efeitos especiais aos componentes, como opacidade, modo de mesclagem e sombras. </p> </td>
  </tr>
  <tr>
   <td><p>Avançado </p> </td>
   <td><p>Permite adicionar:</p>
    <ul>
     <li>Propriedades de <code>::before</code> e <code>::after</code> pseudoelementos para adicionar conteúdo depois ou antes do conteúdo padrão no seletor, e estilizá-lo.<br /> Consulte <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">Pseudo-elementos CSS</a>.</li>
     <li>Código CSS personalizado em linha para um componente.</li>
    </ul> <p>Quando você adiciona um código CSS personalizado, ele substitui a personalização que você adicionou usando as opções na barra lateral. </p> </td>
  </tr>
 </tbody>
</table>

#### Simular Erro/Sucesso {#simulate-error-success}

As opções Simular erro e sucesso estão disponíveis na parte inferior da barra lateral. Você pode vê-las usando uma seta de mostrar/ocultar visível na parte inferior da barra lateral. Usando o Editor de Temas, você pode criar um estilo em vários estados de um componente.

Por exemplo, você adiciona um campo numérico em seu formulário e especifica seu estilo no editor de temas. Quando um usuário digita um valor alfanumérico no campo, é necessário alterar a cor de fundo da caixa de texto. Você seleciona o campo numérico no tema e usa a opção de estado na barra lateral. Você seleciona o estado Erro na barra lateral e altera a cor do plano de fundo para vermelho. Para visualizar o comportamento, você pode usar a opção Simular erro disponível na barra lateral. As opções Simular erro e sucesso são descritas detalhadamente abaixo:

* **Simular sucesso**: Permite ver a aparência de um componente se você especificar seu estilo para o estado de sucesso. Por exemplo, em um formulário, os clientes definem a senha. Os usuários podem definir a senha de acordo com as diretrizes fornecidas. Quando um usuário digita uma senha seguindo todas as diretrizes fornecidas, a caixa de texto fica verde. Quando a caixa de texto fica verde, ela está em estado de sucesso. Você pode especificar o estilo de um componente em estado de sucesso e simular sua aparência usando a opção Simular sucesso .

* **Erro Simular**: Permite ver a aparência de um componente se você especificar seu estilo para o estado de erro. Por exemplo, em um formulário, os clientes definem a senha. Os usuários podem definir a senha de acordo com as diretrizes fornecidas. Quando um usuário digita uma senha que não siga todas as diretrizes fornecidas, a caixa de texto fica vermelha. Quando a caixa de texto fica vermelha, ela está no estado de erro. Você pode especificar o estilo de um componente em estado de erro e simular sua aparência usando a opção Simular erro .

### Estilo de um componente {#styling-a-component}

Por exemplo, em seu formulário, há dois tipos de caixas de texto: uma que aceita apenas valores numéricos e outra que aceita valores alfanuméricos. É possível personalizar o estilo da caixa de texto que aceita apenas valores numéricos (uma caixa numérica).

Para personalizar o estilo de um componente específico (uma caixa numérica neste exemplo), execute as seguintes etapas:

1. No Editor de Temas, selecione a caixa numérica na Tela.
1. Ao selecionar a caixa numérica, é possível ver a barra de ferramentas do componente com três opções:

   * **[!UICONTROL Widget de caixa numérica]**
   * **[!UICONTROL Widget de campo]**

1. Selecionar **[!UICONTROL Widget de caixa numérica]**.
1. O título da barra lateral muda para o Widget de caixa numérica e mostra opções para personalizar sua aparência.
Use **[!UICONTROL Dimension &amp; Posição]** na barra lateral para personalizar o tamanho do componente. Certifique-se de que o estado seja **[!UICONTROL Padrão]**.

Em vez de selecionar **[!UICONTROL Widget de caixa numérica]**, selecione **[!UICONTROL Widget de campo]** na barra de ferramentas do componente e execute as etapas acima. Ao selecionar dimensões para **[!UICONTROL Widget de campo]** , todas as caixas de texto, exceto a caixa numérica, têm o mesmo tamanho.

### Campos de estilo para um determinado estado {#styling-fields-given-state}

Com a barra de ferramentas do componente, também é possível especificar o estilo dos componentes para seus diferentes estados. Por exemplo, se um componente estiver desativado, ele estará em um estado desativado. Os estados normalmente usados de um componente que pode ser estilizado no editor de temas são: Padrão, Foco, Desativado, Erro, Sucesso e Passar o mouse. Você pode selecionar um componente na Tela e usar a opção Estado na barra lateral para personalizar sua aparência.

Para personalizar o estilo de um componente em um estado específico, execute as seguintes etapas:

1. Selecione um componente na Tela e selecione a opção apropriada na barra de ferramentas do componente.
A barra lateral mostra opções para personalizar o estilo do componente.
1. Selecione um estado na barra lateral. Por exemplo, Estado do erro.
1. Use opções como **[!UICONTROL Borda, Plano de Fundo]** na barra lateral para personalizar a aparência do componente.
1. Use o **[!UICONTROL Erro Simular]** na parte inferior da barra lateral para ver a aparência do estilo na edição.

Quando você personaliza o estilo de um componente após especificar seu estado, a personalização aparece para o componente somente para o estado especificado. Por exemplo, se você personalizar o estilo do componente quando o estado de passar o mouse estiver selecionado. A personalização aparece para o componente quando você move o ponteiro sobre o componente no formulário renderizado <!-- or interactive communication --> ao qual você aplica o tema.

Para simular o comportamento de estados diferentes de erro e sucesso, use o Modo de visualização. Para usar o modo de Visualização, clique em **[!UICONTROL Visualizar]** na barra de ferramentas da página.

### Layouts de estilo para telas menores {#styling-layouts-for-smaller-displays}

Use a régua na Tela de desenho para selecionar pontos de interrupção para dispositivos com exibições menores. Clique no emulador ![régua](assets/emulator-icon.svg) em Tela para exibir a régua e os pontos de interrupção. Os pontos de interrupção permitem visualizar um formulário <!-- or interactive communication --> para tamanhos de exibição pertencentes a diferentes dispositivos, como telefones e tablets. Vários tamanhos de exibição são suportados no Editor de Tema.

Para criar estilos de componentes para diferentes pontos de interrupção:

1. Na Tela, selecione um ponto de interrupção acima da régua.
Um ponto de interrupção representa um dispositivo móvel e seu tamanho de exibição.
1. Use a barra lateral para personalizar o estilo do formulário <!-- or interactive communication --> componentes no tema para o tamanho de exibição selecionado.
1. Certifique-se de que a personalização seja salva.

É possível criar estilo no formulário <!-- or interactive communication --> componentes para vários dispositivos. Formulário <!-- and interactive communication --> os componentes para desktops e dispositivos móveis podem ter estilos totalmente diferentes.

### Uso de Web Fonts em um tema {#using-web-fonts-in-a-theme}

Agora é possível usar fontes disponíveis em um serviço da Web em um Formulário adaptável <!-- or interactive communication -->. Pronto para uso, [Adobe Fonts](https://fonts.adobe.com/), um serviço da Web Adobe está disponível. Para usar o Adobe Fonts, crie um kit, adicione fontes e obtenha a ID do Kit de [Adobe Fonts](https://fonts.adobe.com/).

Para configurar o Adobe Fonts no Experience Manager, execute as seguintes etapas:

1. Na instância do autor, clique em ![Adobe Experience Manager](assets/adobeexperiencemanager.png)**[!UICONTROL Adobe Experience Manager ]**>**[!UICONTROL  Ferramentas ]**![martelo](assets/hammer.png) >**[!UICONTROL  Implantação ]**>**[!UICONTROL  Cloud Services ]**.
1. No **[!UICONTROL Cloud Services]** navegue e abra a página **[!UICONTROL Adobe Fonts]** opção. Abra a pasta de configuração e clique em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um título para a configuração e clique em **[!UICONTROL Criar]**.

   Você é redirecionado para a página de configuração.

1. Na caixa de diálogo Editar componente, forneça sua ID do Kit e clique em **[!UICONTROL OK]**.

Para configurar um tema para usar a configuração do Adobe Fonts, execute as seguintes etapas:

1. Na instância do autor, abra um tema no editor de temas.
1. No editor de temas, navegue até **[!UICONTROL Opções de Tema]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configurar]**.
1. Em **[!UICONTROL Configuração do Adobe Fonts]** , selecione um kit e clique em **[!UICONTROL Salvar]**.

   Agora, é possível ver que as fontes são adicionadas na propriedade família de fontes do tema.

<!-- >
### Listing and selecting fonts in theme editor {#listing-and-selecting-fonts-in-theme-editor}

You can use the theme configuration service to add more fonts to the theme editor. Perform the following steps to add fonts:

1. Log in to Experience Manager Web Console with administrative privileges. URL for the Experience Manager Web Console is `https://'[server]:[port]'/system/console/configMgr`.
1. Open **[!UICONTROL Adaptive Form Theme Configuration Service]**.

   ![theme-config](assets/theme-config.png)

1. Click +, specify the name of the font, and click **Save**. The font is added and available in theme editor. -->

#### Seleção de fontes no editor de temas {#selecting-fonts-in-theme-editor}

Você pode usar o botão + para adicionar uma fonte. Quando você adiciona uma fonte, ela é listada na barra lateral.

![Nova fonte listada no editor de temas](assets/theme-font.png)

Além da opção de configuração de tema, também é possível adicionar a fonte do próprio editor de temas. Digite a fonte que deseja usar no campo família de fontes na barra lateral e pressione a tecla de retorno no teclado.

![Digitação e seleção de fonte no editor de temas](assets/font-selection.png)

Ao selecionar uma fonte, ela é adicionada sob a lista família de fontes. Você pode usar a opção Máscara no editor de temas para desativar ou ativar as fontes listadas.

![Multifontes](assets/multi-fonts.jpg)

É possível ver a alteração da fonte do componente.

O campo Família de fontes oferece suporte a várias fontes. Quando você digita uma fonte, o navegador a procura e a aplica ao componente selecionado. Se o navegador não conseguir localizar uma fonte, ele procurará uma fonte próxima a ela na família. Você pode começar digitando a fonte específica que está procurando. Se você não encontrar a fonte que deseja usar, é possível digitar uma fonte genérica na família e usá-la.

#### Estilos de máscara aplicados no editor de temas {#mask-styles-applied-in-theme-editor}

É possível mascarar estilos aplicados em um tema. Na barra lateral do editor de temas, você pode usar o ![alternar_olho](assets/toggle_eye.png)ícone para desativar um estilo aplicado. Por exemplo, se você alterar dimensões de um componente em um formulário <!-- or interactive communication -->, é possível usar o botão de máscara à esquerda de uma propriedade para desativá-la. Ao salvar um tema, as opções de mascaramento selecionadas são mantidas.

![Opção de máscara disponível na barra lateral do editor de temas](assets/mask-styles.png)

O exemplo abaixo mostra estilos mascarados e não mascarados em um tema.

![Estilos mascarados e não mascarados](assets/mask2.png)

## Aplicação de um tema a um formulário {#applying-a-theme-to-a-form-or-interactive-communication-br}

Para aplicar um tema a um formulário adaptável:

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione-o e clique em **[!UICONTROL Abrir]**.
1. No modo de edição, selecione um componente e clique em ![nível de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e, em seguida, clique em ![cmppr](assets/cmppr.png).

   É possível editar as propriedades do formulário na barra lateral.

1. Na barra lateral, clique em **[!UICONTROL Estilo]**.
1. Selecione seu tema no **[!UICONTROL Tema de formulário adaptável]** e clique em **[!UICONTROL Concluído]** ![botão de seleção](assets/check-button.png).

Você também pode definir um tema para um Formulário adaptável ao criá-lo.

<!-- To apply a theme to an interactive communication:

1. Open your interactive communication in edit mode. To open a interactive communication in edit mode, select a form and click **Open**.
1. In the edit mode, select a component, then click ![field-level](assets/field-level.png) &gt;**Document Container**, and then click ![cmppr](assets/cmppr.png).

   You can edit properties of your form in the sidebar.

1. In the sidebar, under **Basic**, select your theme from the **Theme** drop-down and click **Done** ![check-button](assets/check-button.png) -->

### Alterar o tema de um formulário no tempo de execução {#change-theme-of-a-form-at-runtime}

Um tema estimula diferentes componentes de um formulário. Você pode usar o `themeOverride` para alterar dinamicamente o tema de um formulário. Um URL típico de um formulário é:

`https://<server>:<port>/content/forms/af/test.html`

Você pode usar o parâmetro themeOverride para aplicar um tema no tempo de execução.

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

O `themeOverride` permite fornecer um caminho para um tema. Altera o tema do formulário e atualiza o formulário com estilos atualizados.

## Obter aparência específica usando Temas {#specific-af-appearance}

Com [!DNL AEM Forms], juntamente com o tema de tela predefinido, há muitos outros temas. Se você quiser projetar seu formulário <!-- or interactive communication --> utilizando outros temas, juntamente com mais alterações, copie o tema da pasta Biblioteca de Temas. Cole os temas copiados fora da pasta Biblioteca de Temas e edite o tema copiado de acordo com as alterações desejadas.

Para copiar um tema, execute as seguintes etapas:

1. Na instância de criação, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.
1. Abra a pasta Biblioteca de Temas.
1. Na pasta Biblioteca de Temas, passe o ponteiro do mouse sobre o tema predefinido correspondente e toque em **[!UICONTROL Copiar]**.
1. Cole o tema copiado fora da pasta Biblioteca de Temas.
1. Personalize o tema copiado.

Depois de personalizar o tema, aplique-o ao formulário <!-- or interactive communication -->.

>[!NOTE]
>
>Não modifique os temas disponíveis na pasta Biblioteca de Temas. Esta pasta contém temas do sistema. Qualquer alteração feita nesses temas será substituída pela instalação de uma versão mais recente ou de um hotfix de [!DNL AEM Forms].

## Impacto em outros casos de uso do formulário adaptável {#impact-on-other-adaptive-form-use-cases}

* **Publicar/desfazer a publicação de um formulário:** Ao publicar um formulário, o tema aplicado a também é publicado (se ainda não estiver publicado)
* **Importar/exportar um formulário:** Ao importar ou exportar um formulário, seu tema associado também é automaticamente importado ou exportado.
* **Referências de um formulário:** A seção Referências em referências de formulário contém uma entrada extra para o tema.
* **Hora da última modificação de um formulário:** Atualizado quando o tema associado é alterado.
<!-- * **A/B Testing:** You can apply a different theme to two versions of the form in A/B testing. The information of the two themes is individually stored on the two guide containers. -->

## Sequência de geração de CSS {#css-generation-sequence}

Ao selecionar exibir CSS, o Editor de Temas coleta todas as informações de estilização e cria um CSS. Ele coleta informações na seguinte ordem:

<!-- 1. Styling defined in the theme's base client library. -->
1. Estilo definido pelo usuário, especificado pelas propriedades na barra lateral.
1. O estilo CSS fornecido usando a opção Substituição de CSS.

Por exemplo, a cor de fundo de uma caixa de texto é azul<!-- in the base client library-->. Altere-o para rosa usando as propriedades na barra lateral. Ao gerar CSS, você vê a cor de fundo da caixa de texto como rosa. Depois de alterar a cor do plano de fundo usando as propriedades, outro autor usa a opção de substituição de CSS para alterar a caixa de texto da cor do plano de fundo como branco. Ao gerar CSS, você vê a cor do fundo como branca no CSS gerado.

## Estilos de depuração {#debugging-styles}

Ao especificar estilos para componentes no Editor de Temas, um CSS é gerado. Ao criar um estilo em um componente genérico, vários componentes incluídos nele também têm o estilo. Por exemplo, ao criar um estilo em um campo, a caixa de texto e o rótulo nele também têm o estilo. Ao criar um estilo para a caixa de texto dentro do campo, ela recebe seu próprio CSS. Se você deseja depurar o CSS gerado para o campo e o componente, o Editor de Temas fornece opções que permitem a visualização do CSS.

Você pode ver o CSS gerado usando as seguintes opções:

* **Exibir CSS** na barra lateral: Ao selecionar um componente no Tema, você pode ver a opção EXIBIR CSS na barra lateral. Ele mostra o CSS gerado, incluindo o CSS para `::before` e `::after` pseudo elementos.
* **Exibir CSS do Tema** na barra de ferramentas da tela: Na barra de ferramentas da Tela, clique em ![theme-options](assets/theme-options.png) > **[!UICONTROL Exibir CSS do Tema]**. Você pode ver o CSS do tema inteiro gerado pelas propriedades definidas no Editor de Temas.

## Solução de problemas, recomendações e práticas recomendadas {#troubleshooting-recommendations-and-best-practices}

* **Evitar ativos de outro Tema**

   Ao editar um tema, você pode procurar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o plano de fundo de uma página. Por exemplo, ao selecionar **[!UICONTROL Página]** ![botão editar](assets/edit-button.png)> **[!UICONTROL Histórico]** > **[!UICONTROL Adicionar]** > **[!UICONTROL Imagem]**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

* Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar navegar e adicionar ativos de outros temas.

<!-- * **Using base clientlib, theme editor, and inline styling**

    * **Base clientlib**:

      Base client library contains styling information. To use styling information in client-side libraries in themes.

        1. Navigate to **[!UICONTROL Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Themes]**.
        1. In the Themes page, select a theme and click **[!UICONTROL Properties]**.
        1. In the Properties page that opens, click **[!UICONTROL Advanced]**.
        1. In the Advanced tab, in the Clientlib Location field, browse, and select the client-library you want to use.
        1. Click **[!UICONTROL Save]**.

      The styling you specify in client library is imported in the theme that uses it. For example, you specify styling for text box, numeric box, and switch in the client library. When you import your client library in the theme, styling for text box, numeric box, and switch is imported. You can then style other components using theme editor. -->
    Você também pode criar um tema, criar cópias dele e modificar o estilo fornecido nos temas copiados para casos de uso semelhantes.
    Consulte [Obter aparência específica usando Temas](#specific-af-appearance)
    
    * **Editor de Temas:**
    
    O Editor de Temas permite criar temas para criar um estilo em seu formulário &lt;!>— ou comunicação interativa —>. É possível especificar o estilo dos componentes em um tema, que permite a consistência entre várias formas &lt;!>— ou comunicações interativas —> você desenvolve. É recomendável especificar informações de estilo em um tema e aplicar o tema a um formulário.
    
    * **Estilo em linha:**
    
    É possível estilizar componentes usando o modo Estilo no formulário &lt;!>— ou comunicação interativa —> editor multicanal ao trabalhar com um formulário. Usar o modo de estilo para alterar o estilo do componente de formulário substitui o estilo especificado no tema. Para alterar o estilo de determinados componentes de um formulário específico, consulte [Estilo em linha de componentes] (inline-style-adaptive-forms.md).

<!-- * **Using client-side libraries**

  If you want to create client libraries to import styling information, see [Using Client-Side Libraries](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/clientlibs.html). After you create a client library, you can import it in your theme using the steps mentioned above. -->

* **Alteração da largura do layout do painel do contêiner**

   Não é recomendável alterar a largura do layout do painel do contêiner. Quando você especifica a largura de um painel de contêiner, ele se torna estático e não se adapta a exibições diferentes.

* **Quando usar o editor de formulário ou o editor de temas para trabalhar com o cabeçalho e o rodapé**

   Use o editor de temas se desejar criar um estilo de cabeçalho e rodapé usando opções de estilo, como estilo de fonte, plano de fundo e transparência.
Se desejar fornecer informações como uma imagem de logotipo, nome da empresa no cabeçalho e informações de direitos autorais no rodapé, use as opções do editor de formulário.
