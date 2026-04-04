---
title: Personalização de temas do formulário adaptável usando o Editor de temas
description: Saiba como usar o Editor de temas para criar e personalizar temas visuais para Forms adaptável baseada em Componentes principais no Adobe Experience Manager.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 4a541c11-38e9-4dbc-8464-38be6b1ee94d
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---

# Personalização de temas do formulário {#customizing-form-themes}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

O Editor de temas no Adobe Experience Manager (AEM) Forms é uma interface visual que permite criar e personalizar temas para o seu Forms adaptável sem escrever código manualmente. Um tema define a aparência dos componentes e painéis do formulário, incluindo cores do plano de fundo, estilos de fonte, bordas, dimensões e espaçamento. Ao aplicar um tema, os estilos especificados refletem nos componentes correspondentes e você pode reutilizar o mesmo tema em vários Forms adaptáveis.

O Editor de temas elimina a necessidade de uma persona de desenvolvedor dedicada para o estilo de formulário básico. Com apenas um conhecimento prático de CSS, você pode estilizar formulários usando a barra lateral visual ou gravar substituições de CSS avançadas diretamente no editor.

## Pré-requisitos {#prerequisites}

* Permissões no nível do autor no Adobe Experience Manager Forms.
* Compreensão básica dos princípios de estilo CSS. Para obter uma referência CSS completa, consulte a [Referência CSS do MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

## Navegar até o Diretório de Temas {#navigate-to-themes}

1. Faça logon na instância de autor do AEM.
1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.

   O diretório Temas exibe todos os temas disponíveis, incluindo quaisquer temas padrão fornecidos pelo AEM Canvas, juntamente com temas personalizados criados por você ou por sua organização.

### Criar um novo tema {#create-a-new-theme}

1. No diretório Themes, selecione a pasta onde deseja armazenar o novo tema.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Tema]**.

   ![Criar novo Tema](/help/forms/assets/custom-theme-create.png)

1. Na caixa de diálogo **[!UICONTROL Criar Tema]**, especifique os seguintes detalhes:
   * **[!UICONTROL Título]**: um título descritivo para o tema.
   * **[!UICONTROL Nome]**: o nome do nó para o tema.
   * **[!UICONTROL Formulário adaptável para visualizar o tema]**: para um tema de Componente principal, selecione um Formulário adaptável baseado em Componente principal. **[!UICONTROL Usar formulário adaptável padrão]** usa um Formulário adaptável de base, não Componentes principais. O formulário selecionado aparece na tela Editor de temas para visualização em tempo real enquanto você edita.
   * **[!UICONTROL Descrição]** *(Opcional)*: uma breve descrição do tema.
   * **[!UICONTROL Contêiner de Configuração]** *(Opcional)*: o contêiner de configuração que contém os detalhes de configuração da Fonte Adobe.
   * **[!UICONTROL Marcas]** *(Opcional)*: Marcas anexadas ao tema para identificação e pesquisa.
1. Clique em **[!UICONTROL Criar]**.

   ![configurando tema personalizado](/help/forms/assets/custom-theme-name.png)

   O tema é criado. Agora você pode clicar em **[!UICONTROL Editar]** para abri-lo no Editor de Tema.

### Editar um tema existente {#edit-an-existing-theme}

1. No diretório **Themes**, selecione o tema que deseja modificar.
1. Clique em **[!UICONTROL Editar]** na barra de ações para abrir o tema no Editor de Temas.

   ![Editando um tema](/help/forms/assets/custom-theme-edit.png)

### Carregar um tema {#upload-a-theme}

Você pode importar um pacote de tema (por exemplo, um exportado de outro ambiente) para o diretório Themes:

1. No diretório **Themes**, clique em **[!UICONTROL Criar]** > **[!UICONTROL Carregamento de Arquivo]**.
1. Navegue para selecionar o pacote de temas (arquivo ZIP) no computador e clique em **[!UICONTROL Carregar]**.

   ![Carregar tema - Criar menu com a opção Carregar Arquivo](/help/forms/assets/custom-theme-upload.png)

O tema carregado aparece no diretório Themes e pode ser editado como qualquer outro tema.

### Baixar um tema {#download-a-theme}

É possível exportar um tema como um pacote (arquivo ZIP) para reutilizar em outro ambiente AEM Forms ou para fazer backup dele:

1. No diretório **Themes**, selecione um ou mais temas (use as caixas de seleção nos cartões de tema).
1. Clique em **[!UICONTROL Baixar]** na barra de ações. Uma caixa de diálogo pode ser exibida com detalhes dos temas selecionados.
1. Confirme ou clique em **[!UICONTROL Baixar]** na caixa de diálogo. O pacote de tema é baixado como um arquivo ZIP no computador.

   ![Baixar tema - selecione o tema e clique em Baixar](/help/forms/assets/custom-theme-download.png)

Você pode carregar esse ZIP posteriormente usando [Carregar um tema](#upload-a-theme) no mesmo ambiente ou em outro.

## Entender a interface do Editor de temas {#understand-the-theme-editor}

Ao abrir um tema no Editor de temas, você verá duas áreas principais:

![Editor de temas](/help/forms/assets/custom-theme-editor.png)

* **Tela de desenho** (lado direito): Exibe uma visualização do Formulário adaptável vinculado ao tema. Todas as alterações de estilo refletem aqui instantaneamente, para que você possa ver o impacto de suas edições em tempo real.
* **Barra lateral** (lado esquerdo): contém o painel **Seletores** que lista todos os componentes de formulário estilizáveis em uma estrutura de árvore, como Página, Formulário, Campo, Botão, Painel, Imagem, hCaptcha e reCaptcha.

### Barra de ferramentas da tela de desenho {#canvas-toolbar}

![Barra de ferramentas da tela do Editor de Temas com Opções Alternar Painel Lateral, Desfazer, Refazer, Emulador, Editar/Visualizar e Tema](/help/forms/assets/custom-theme-toolbar-utilities.png)

Da esquerda para a direita, a barra de ferramentas fornece:
* **A: Alternar Painel Lateral**: Mostrar ou ocultar a barra lateral Seletores. Use isso para maximizar a área de visualização do formulário quando quiser focalizar na tela de desenho ou mostrar a barra lateral novamente quando precisar selecionar ou estilizar componentes.
* **B: Opções de Tema** (lista suspensa): abre um menu com quatro opções. Clique nele quando precisar alterar o formulário de visualização, exibir CSS, gerenciar estilos salvos ou obter ajuda no editor. Ao abrir a lista suspensa Opções de tema, você verá:

  ![A lista suspensa Opções de Tema mostrando Configurar, Exibir Tema CSS, Gerenciar Estilos e Ajuda](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL Configurar]**: alterne o formulário mostrado na tela para um Formulário adaptável diferente. Use isso para verificar como o tema é exibido em outro formulário sem sair do editor.
     ![Configurar o formulário adaptável para visualização de tema](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL Exibir tema CSS]**: abra uma caixa de diálogo com o CSS compilado completo para o tema. Para ver o CSS somente para o componente selecionado no momento, use a **[!UICONTROL Exibir CSS]** na barra lateral (útil para depurar ou copiar regras).
     ![Exibir CSS Final](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL Gerenciar Estilos]**: abra a caixa de diálogo para salvar, nomear e reutilizar estilos de texto e imagem. Os estilos salvos podem ser aplicados a outros componentes; os estilos usados recentemente também podem aparecer para reutilização rápida.
   * **[!UICONTROL Ajuda]**: iniciar o tour guiado por imagem do Editor de Tema.
* **C: Desfazer / Refazer**: reverter ou reaplicar suas últimas alterações de estilo. Útil se você tentar um estilo e quiser voltar sem perder outras edições.
* **D: Emulador**: Selecione um dispositivo ou ponto de interrupção (por exemplo, Desktop, Tablet ou Mobile) para visualizar o formulário nesse tamanho de tela. A visualização do formulário é redimensionada para corresponder ao ponto de interrupção selecionado. Todos os estilos definidos enquanto um ponto de interrupção está selecionado aplicam-se somente a esse ponto de interrupção, para que você possa definir estilos responsivos. Para obter detalhes, consulte [Estilo para telas de diferentes tamanhos](#styling-for-different-screen-sizes).
* **E: Editar/Visualizar**: alternar entre dois modos. **Editar** é o padrão: você pode clicar em componentes na tela para selecioná-los e alterar seu estilo na barra lateral. **Visualizar** mostra o formulário como um usuário final o veria sem bordas de seleção, rótulos de componentes ou a barra lateral de estilos, para que você possa verificar como o formulário com tema é exibido e se comporta antes de publicar.

<!--
**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).
-->

### Estilo de um componente

Você pode selecionar um componente para estilizar de duas maneiras:
* **Na Tela**: clique diretamente em um componente no formulário (por exemplo, um campo de texto, botão ou lista suspensa). O elemento selecionado é realçado com uma borda, e um rótulo de componente (por exemplo, &quot;Widget de entrada de texto&quot;) é exibido acima dele. As opções de estilo desse componente aparecem na barra lateral.

  ![Editar tema da tela](/help/forms/assets/custom-theme-field-level.png)

* **No painel Seletores**: use a estrutura de árvore na barra lateral esquerda para detalhar componentes específicos. Por exemplo, expanda **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Entrada de texto]** para direcionar especificamente o widget de caixa de texto.

  ![Editar tema no painel Seletor](/help/forms/assets/custom-theme-selector.png)

#### Aplicar estilos a um componente {#apply-styles-to-a-component}

Depois que um componente é selecionado, a barra lateral exibe as propriedades de estilo disponíveis organizadas nas seguintes categorias:

* **[!UICONTROL Dimensões e Posição]**: controle o alinhamento, o tamanho, o preenchimento, a margem, a largura, a altura e o índice Z.
* **[!UICONTROL Texto]**: Configurar família de fontes, peso, cor, tamanho, altura da linha, alinhamento, espaçamento entre letras, decoração de texto e transformação. Para obter uma lista completa de propriedades de texto CSS com suporte, consulte a [documentação sobre texto CSS do MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text).
* **[!UICONTROL Plano de fundo]**: definir uma cor, imagem ou gradiente de plano de fundo. Consulte a [documentação de Planos de Fundo CSS do MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders).
* **[!UICONTROL Borda]**: defina a largura, o estilo, o raio e a cor da borda.
* **[!UICONTROL Efeitos]**: adicionar opacidade, modos de mesclagem e sombras.

Para aplicar um estilo:

1. Selecione o componente na tela de desenho ou no painel Seletores.
1. Defina as propriedades visuais desejadas na barra lateral. Por exemplo, escolha uma **[!UICONTROL Cor de Fundo]** e ajuste a **[!UICONTROL Cor da Fonte]**.
1. Clique no ícone de marca de seleção **[!UICONTROL OK]** para confirmar a alteração da propriedade.

   ![Aplicando estilo](/help/forms/assets/custom-theme-applying-style.png)

<!--
#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.
-->

### Estilo no nível do formulário {#form-level-styling}

O estilo no nível do formulário aplica um estilo amplamente a todos os componentes do mesmo tipo. Por exemplo, se você selecionar **[!UICONTROL Campo]** no painel **Seletores** e definir uma cor de plano de fundo para azul, cada campo no formulário (caixas de texto, caixas numéricas, seletores de data e menus suspensos) herdará esse plano de fundo azul.

**Exemplo:** Para definir uma cor de plano de fundo uniforme em todos os campos do formulário:

1. No painel **Seletores**, selecione **[!UICONTROL Campo]**.
1. Na barra lateral, defina a **[!UICONTROL Cor do Plano de Fundo]** como azul.
1. Clique em **[!UICONTROL OK]**.

   ![Estilo de Nível de Formulário](/help/forms/assets/custom-theme-form-level-styling.png)

Todos os componentes de campo no formulário agora exibem um plano de fundo azul.

### Estilo de nível de componente {#component-level-styling}

O estilo de nível de componente é direcionado a um tipo de componente específico, substituindo qualquer estilo de nível de formulário mais amplo. Por exemplo, se você quiser que apenas o widget Caixa de texto tenha uma cor de fundo diferente, enquanto todos os outros campos permanecem azuis, você pode direcionar o widget Caixa de texto especificamente.

**Exemplo:** Para definir um plano de fundo verde e uma fonte roxa somente no widget caixa de texto:

1. No painel Seletores, expanda **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Entrada de texto]**.
1. Defina a **[!UICONTROL Cor da Fonte]** como violeta.
   ![Estilo de nível de campo](/help/forms/assets/custom-theme-field-level-styling1.png)
1. Defina a **[!UICONTROL Cor do Plano de Fundo]** para verde.
   ![Estilo de nível de campo](/help/forms/assets/custom-theme-field-level-styling2.png)
1. Clique em **[!UICONTROL OK]**.

O widget Caixa de texto agora exibe um plano de fundo verde com texto roxo, enquanto todos os outros campos permanecem azuis no estilo de nível de formulário.

>[!NOTE]
>
> **O estilo no nível do componente sempre tem prioridade sobre o estilo no nível do formulário.** Quando um estilo é definido em ambos os níveis, o seletor de nível de componente mais específico substitui o seletor de nível de formulário mais amplo. Isto segue as [regras de especificidade de CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) padrão. Por exemplo, se você definir um plano de fundo azul em todos os Campos (nível de formulário) e um plano de fundo verde no widget caixa de texto (nível de componente), a caixa de texto exibirá um plano de fundo verde.

## Estilo para telas de tamanhos diferentes {#styling-for-different-screen-sizes}

Você pode definir estilos diferentes para tamanhos de dispositivos diferentes para que seu tema seja responsivo. A barra de ferramentas do Editor de temas mostra **opções de dispositivo** (por exemplo, iPhone 5, iPad, Desktop, Tablet, Tela menor) para visualizar e estilizar o formulário nesse tamanho de tela.

1. Na barra de ferramentas da tela, use o **emulador de dispositivo**: clique em um dos rótulos de dispositivo (por exemplo, **[!UICONTROL Área de Trabalho]**, **[!UICONTROL Tablet]**, **[!UICONTROL iPad]**, **[!UICONTROL Tela Menor]**). Uma régua acima do formulário mostra a largura em pixels do dispositivo selecionado.
1. Com esse dispositivo selecionado, use a barra lateral para definir ou ajustar estilos. Os estilos se aplicam somente à exibição de dispositivo selecionada.
1. Alterne para outro dispositivo e defina estilos para ele conforme necessário.
1. Clique em **[!UICONTROL OK]** e salve o tema quando terminar.

   ![Emulador de dispositivo no Editor de Tema - régua e opções de dispositivo (Área de Trabalho, Tablet, iPad, Tela Menor)](/help/forms/assets/custom-theme-emulator.png)

Portanto, o mesmo tema pode ter diferentes tamanhos de espaçamento ou estilos relacionados a layout por dispositivo, correspondendo ao [comportamento do Editor de temas do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=pt-BR) para estilo responsivo.

## Usar substituições CSS avançadas {#use-advanced-css-overrides}

Para estilos que não estão disponíveis na barra lateral visual, você pode escrever CSS personalizado diretamente no editor.

1. Selecione o componente.
1. Na barra lateral, expanda a seção **[!UICONTROL Avançado]**.
1. Escreva suas regras CSS personalizadas na área **[!UICONTROL Substituição de CSS]**. Essas regras substituem quaisquer propriedades definidas pelos controles visuais se houver um conflito.

Para obter uma referência completa da propriedade CSS, consulte a [Referência de CSS do MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

### Adicionar pseudoelementos CSS {#add-css-pseudo-elements}

A seção **[!UICONTROL Avançado]** também oferece suporte a pseudoelementos CSS, como `::before` e `::after`. Eles permitem inserir conteúdo ou estilo decorativo ao redor de um componente sem modificar a estrutura do formulário. Por exemplo, para adicionar um indicador visual antes de um componente Caixa de texto:

1. Selecione o componente (por exemplo, `CMP Textbox`).
1. Expanda a seção **[!UICONTROL Avançado]**.
1. Nos campos de pseudoelemento `::before`, adicione propriedades CSS, como:

   ```css
   color: #B10DC9;
   ```

   ![Antes de CSS](/help/forms/assets/custom-theme-before-css.png)

1. Nos campos de pseudoelemento `::after`, adicione propriedades CSS, como:

   ```css
   color: #006400;
   ```

   ![Após CSS](/help/forms/assets/custom-theme-after-css.png)


Esses pseudoelementos seguem o comportamento CSS padrão. Para obter uma referência completa, consulte [Pseudo-elementos MDN CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements).

## Práticas recomendadas {#best-practices}

* **Use o painel Seletores para um direcionamento preciso**: ao estilizar elementos aninhados, como um rótulo de campo ou uma descrição longa, use o painel Seletores à esquerda em vez de clicar na tela. Isso garante que o seletor de CSS correto seja gerado com a especificidade adequada.
* **Evitar ativos de outros temas**: ao editar um tema, não procure e adicione ativos (como imagens) de outros temas. Se o tema de origem for movido ou excluído, o tema atual será interrompido.
* **Não alterar a largura do layout do painel de contêiner**: especificar uma largura fixa nos painéis de contêiner os torna estáticos e os impede de se adaptarem a tamanhos de tela diferentes.

## Consulte também {#see-also}

{{see-also}}
