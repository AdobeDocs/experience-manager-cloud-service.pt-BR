---
title: Layout responsivo
description: O AEM permite que você tenha um layout responsivo para suas páginas
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 78%

---

# Layout responsivo {#responsive-layout}

O AEM permite que você tenha um layout responsivo para suas páginas usando o **Contêiner de layout** componente.

Isso fornece um sistema de parágrafo que permite posicionar componentes em uma grade responsiva. Essa grade pode reorganizar o layout de acordo com o tamanho e o formato do dispositivo/janela. O componente é usado em conjunto com o [**Layout** modo](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector), que permite criar e editar o layout responsivo dependendo do dispositivo.

O container de layout:

* Fornece a opção de encaixe horizontal na grade, juntamente com a capacidade de posicionar componentes lado a lado na grade e definir quando devem ser recolhidos/refluídos.
* Usa pontos de interrupção predefinidos (por exemplo, para telefone, tablet etc.) para permitir que você defina o comportamento necessário do conteúdo de acordo com o dispositivo/orientação.
   * Por exemplo, você pode personalizar o tamanho do componente ou se ele pode ser visualizado em dispositivos específicos.
* Pode ser aninhado para permitir o controle de coluna.

Usuários podem ver como o conteúdo é renderizado em dispositivos específicos usando o emulador.

O AEM permite um layout responsivo para suas páginas usando uma combinação de mecanismos:

* Componente [**Contêiner de layout**](#adding-a-layout-container-and-its-content-edit-mode)

  Este componente está disponível no [navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) e fornece um sistema de parágrafo de grade para que você possa adicionar e posicionar componentes em uma grade responsiva. Ele também pode ser definido como o sistema de parágrafos padrão na sua página.

* [**Modo de layout**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)

  Depois que o container de layout é posicionado na página, você pode usar o modo **Layout** para posicionar conteúdo na grade responsiva.

* [**Emulador**](#selecting-a-device-to-emulate)
Isso permite criar e editar sites responsivos que reorganizam o layout de acordo com o tamanho do dispositivo ou da janela, redimensionando componentes interativamente. Usuários podem ver como o conteúdo é renderizado usando o emulador.

Com esses mecanismos de grade responsivos, você pode:

* Usar pontos de interrupção para definir layouts de conteúdo diferentes com base na largura do dispositivo (de acordo com o tipo e a orientação do dispositivo).
* Usar os mesmos pontos de interrupção e layouts de conteúdo para certificar-se de que o conteúdo responde ao tamanho da janela do navegador no desktop.
* Usar o alinhamento com a grade para permitir colocar componentes na grade, redimensionar como necessário e definir quando devem ser recolhidos/refluir para ficarem lado a lado ou acima/abaixo.
* Ocultar componentes de layouts específicos de dispositivos.
* Executar o controle da coluna.

Dependendo do projeto, o Contêiner de layout pode ser usado como o sistema de parágrafo padrão para suas páginas ou como um componente disponível para ser adicionado à sua página por meio do navegador de componentes (ou ambos).

>[!TIP]
>
>Adobe fornece [Documentação do GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) do layout responsivo como uma referência que pode ser fornecida para desenvolvedores de front-end permitindo que usem a grade AEM fora do AEM, por exemplo, ao criar modelos de HTML estáticos para um futuro site de AEM.

>[!NOTE]
>
>O uso dos mecanismos acima é habilitado pela configuração no modelo. Consulte o documento [Configuração de layout responsivo](/help/sites-cloud/administering/responsive-layout.md) para obter mais informações.

## Definições de layout, emulação de dispositivo e pontos de interrupção {#layout-definitions-device-emulation-and-breakpoints}

Ao criar o conteúdo do seu site, você quer garantir que o conteúdo seja exibido apropriadamente no dispositivo usado para exibi-lo.

O AEM permite definir layouts dependendo da largura do dispositivo:

* O emulador permite simular esses layouts em vários dispositivos. Além do tipo de dispositivo, a orientação, selecionada pela opção **Girar dispositivo**, pode afetar o ponto de interrupção selecionado à medida que a largura muda.
* Os pontos de interrupção são pontos que separam as definições de layout.
   * Eles definem efetivamente a largura máxima (em pixels) de qualquer dispositivo com um layout específico.
   * Normalmente, os pontos de interrupção são válidos para alguns dispositivos, dependendo da largura das telas.
   * O alcance do ponto de interrupção se estende da esquerda até o próximo ponto de interrupção.
   * Não é possível selecionar um ponto de interrupção específico, pois o ponto de interrupção apropriado é selecionado quando você seleciona um dispositivo e uma orientação.

Um dispositivo de **desktop** que não possui uma largura específica utiliza o ponto de interrupção padrão (isto é, todos os itens acima do último ponto de interrupção configurado).

>[!NOTE]
>
>Seria possível definir pontos de interrupção para cada dispositivo individual, mas isso aumentaria consideravelmente o trabalho necessário para a definição e a manutenção do layout.

Ao usar o emulador, você seleciona um dispositivo específico para simular e definir o layout, enquanto o ponto de interrupção relacionado também é destacado. Todas as alterações de layout que você fizer serão aplicadas nos outros dispositivos aos quais o ponto de interrupção se aplica. Isto é, qualquer dispositivo posicionado à esquerda do marcador do ponto de interrupção ativo, mas antes do próximo marcador do ponto de interrupção.

Por exemplo, ao selecionar o dispositivo **iPhone 6 Plus** (definido com uma largura de 540 pixels) para emulação e layout, o ponto de interrupção **Celular** (definido como 768 pixels) também é ativado. Todas as alterações de layout feitas para o **iPhone 6** são aplicáveis a outros dispositivos no ponto de interrupção **Celulares**, como o **iPhone 5** (definido como 320 pixels).

![Emuladores](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Selecionar um dispositivo para emular {#selecting-a-device-to-emulate}

1. Abra a página que deseja editar. Por exemplo:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Selecione o ícone **Emulador** na barra de ferramentas superior:

   ![Tecla Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. A barra de ferramentas do emulador se abre.

   ![Barra de ferramentas do emulador](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   A barra de ferramentas do emulador exibe opções adicionais de layout:

   * **Girar dispositivo** - Permite girar um dispositivo de orientação vertical (retrato) para a orientação horizontal (paisagem) e vice-versa.

   ![Botão Girar paisagem do dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Botão Girar retrato do dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Selecionar dispositivo** - defina um dispositivo específico para emular de uma lista (consulte a próxima etapa para obter detalhes)

   ![Botão Selecionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Para selecionar um dispositivo específico para emular, você pode:

   * Usar o ícone Selecionar dispositivo e escolher um na lista suspensa.
   * Selecione o indicador do dispositivo na barra de ferramentas do emulador.

   ![Lista suspensa Selecionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. Depois que um dispositivo específico é selecionado, você pode: 

   * Visualizar o marcador ativo do dispositivo selecionado, como **iPad.**
   * Visualizar o marcador ativo do [ponto de interrupção apropriado](#layout-definitions-device-emulation-and-breakpoints) como **Tablet.**
   * A linha pontilhada azul representa a *dobra* referente ao dispositivo selecionado (aqui, um **iPhone 6 Plus** em paisagem).

   ![A dobra](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * A dobra também pode ser considerada a quebra de linha da página (não deve ser confundida com os [pontos de interrupção](#layout-definitions-device-emulation-and-breakpoints)) do conteúdo. Isso é exibido para maior comodidade, para mostrar qual parte do conteúdo o usuário vê no dispositivo antes de rolar a tela.
   * A linha para a dobra não será mostrada se a altura do dispositivo que está sendo emulado for maior que o tamanho da tela.
   * A dobra é mostrada para a conveniência do autor e não é mostrada na página publicada.

## Adicionar um contêiner de layout e seu conteúdo (Modo de edição) {#adding-a-layout-container-and-its-content-edit-mode}

Um **Contêiner de layout** é um sistema de parágrafos que:

* Contém outros componentes.
* Define o layout.
* Responde às alterações.

>[!NOTE]
>
>Se ainda não estiver disponível, a variável **Contêiner de layout** deve ser explicitamente [ativado para um sistema/página de parágrafo.](/help/sites-cloud/administering/responsive-layout.md)

1. O **Contêiner de layout** está disponível como um componente padrão no [Navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser). Aqui, você pode arrastá-lo até o local desejado na página, onde poderá ver o **Arraste componentes aqui** espaço reservado.
1. Em seguida, você pode adicionar componentes ao container de layout. Esses componentes conterão o conteúdo real:

   ![Contêiner de layout](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selecionar e executar ações em um contêiner de layout (modo Editar) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Assim como em outros componentes, você pode selecionar e atuar em (recortar, copiar ou excluir) um Contêiner de layout (quando estiver no **Editar** modo):

>[!CAUTION]
>
>Visto que um container de layout é um sistema de parágrafo, a exclusão do componente excluirá a grade de layout e todos os componentes (e seu conteúdo) inclusos no container.

1. Se você passar o mouse sobre ou selecionar o espaço reservado da grade, o menu de ação será exibido.

   ![Adicionar ao contêiner de layout](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   É preciso selecionar a opção **Pai**.

   ![Botão Pai](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Se o componente de layout estiver aninhado, selecionar a opção **Principal** apresentará uma lista suspensa, que permite selecionar o container de layout aninhado ou seus componentes principais.

   Ao passar o mouse sobre os nomes dos containers no menu suspenso, seus contornos são exibidos na página.

   * O menor container aninhado do layout será contornado em azul.
   * Cada container sucessivo é contornado com um tom mais claro de azul.

   ![Containers aninhados](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. A grade inteira é realçada com seu conteúdo. A barra de ferramentas da ação será exibida, na qual é possível selecionar uma ação, como **Excluir.**

## Definição de layouts (modo Layout) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Você pode definir um layout separado para cada [ponto de interrupção](#layout-definitions-device-emulation-and-breakpoints) (como determinado pelo tipo e pela orientação do dispositivo emulado).

Para configurar o layout de uma grade responsiva implementada com o Contêiner de layout, use o modo **Layout**.

O modo **Layout** pode ser iniciado de duas maneiras.

* Ao usar o [modo de menu na barra de ferramentas](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) e escolher o modo **Layout**
   * Selecione o modo **Layout** da mesma maneira que você alternaria para o modo de **Edição** ou o modo de **Segmentação**.
   * O modo **Layout** permanece persistente e você não sai do modo **Layout** até que você selecione outro modo por meio do seletor de modo.
* Quando [editar um componente individual.](/help/sites-cloud/authoring/page-editor/edit-content.md#editing-component-layout)
   * Ao usar a opção **Layout** no menu de ação rápida do componente, é possível alternar para o modo **Layout**.
   * O modo **Layout** persiste ao editar o componente e reverte para o modo **Editar** assim que o foco muda para outro componente.

Quando estiver no modo de layout, você poderá executar várias ações em uma grade:

* Redimensione os componentes de conteúdo usando os pontos azuis. O redimensionamento sempre se ajustará à grade. Ao redimensionar, a grade de plano de fundo é mostrada para auxiliar o alinhamento:

  ![Redimensionar componentes](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

  >[!NOTE]
  >
  >As proporções e as taxas são mantidas quando os componentes como **Imagens** são redimensionados.

* Selecione um componente de conteúdo, a barra de ferramentas permite:
   * **Pai** - Permite selecionar o componente do contêiner de layout inteiro para executar uma ação em tudo.
   * **Flutuar para a nova linha** - o componente será movido para uma nova linha, dependendo do espaço disponível na grade.
   * **Ocultar componente** - o componente ficará invisível (ele pode ser restaurado na barra de ferramentas do container de layout).

  ![Ocultar componente](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* Entrada **Layout** você pode selecionar o modo **Arraste os componentes para cá** para selecionar o componente inteiro. A barra de ferramentas é exibida para esse modo.

  A barra de ferramentas tem opções diferentes dependendo do estado do componente de layout e dos componentes que pertencem a ele. Por exemplo:

   * **Pai** - seleciona o componente do pai.

     ![Botão Pai](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Mostrar componentes ocultos** - revela todos os componentes ou componentes individuais. O número indica quantos componentes ocultos há atualmente. O contador mostra quantos componentes estão ocultos.

     ![Botão Mostrar componentes ocultos](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Reverter layout do ponto de interrupção**: reverte para o layout padrão. Nenhum layout personalizado é imposto.

     ![Botão Reverter layout do ponto de interrupção](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Flutuar para uma nova linha** - move o componente uma posição acima, se o espaço permitir.

     ![Botão Flutuar para uma nova linha](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Ocultar componente** - oculta o componente atual.

     ![Botão Ocultar componente](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

  >[!NOTE]
  >
  >No exemplo acima, as ações flutuar e ocultar estão disponíveis porque este Contêiner de layout está aninhado em um Contêiner de layout pai.

   * **Revelar componentes** Selecione os componentes principais para mostrar a barra de ferramentas de ação com a opção **Mostrar componentes ocultos**. Neste exemplo, dois componentes estão ocultos.

     ![Mostrar componentes](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)

  Selecionar a opção **Mostrar componentes ocultos** exibirá em azul os componentes que estão ocultos no momento em suas posições originais.

  ![Botão Restaurar tudo](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

  Selecionar **Restaurar tudo** revelará todos os componentes ocultos.
