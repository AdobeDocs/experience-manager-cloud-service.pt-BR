---
title: Como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas?
description: Saiba como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 55%

---

# Assinatura eletrônica de um formulário usando assinaturas escritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Este artigo |


Você pode usar o componente **Assinatura Escrita** para desenhar (Rabiscar) assinatura em um Formulário Adaptável. <!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![Caixa de diálogo Assinar assinatura](assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **A:** Clique no ícone **Pincel de Tinta** para desenhar sua assinatura na tela.
* **B:** clique no ícone de **Limpar** para limpar a assinatura na tela.
* **C:** clique no ícone de **Geolocalização** para adicionar a geolocalização junto com a assinatura.
* **D:** clique no ícone de **Teclado** para digitar o seu nome na tela.

Depois de selecionar o ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) na janela Assinatura escritas, você não poderá editar a assinatura. Caso você queira editar a assinatura, desconsidere a assinatura atual e assine novamente com a opção de pincel/teclado acima.

Você pode selecionar o ícone **Configurar** ![configurar](assets/configure.png) para definir a proporção da tela Assinatura Escrita.

* Quando a proporção da tela Assinatura Escrita for menor que 1, as informações de localização geográfica serão adicionadas na parte inferior da tela Assinatura Escrita.
* Quando a proporção da tela Assinatura Escrita for maior que 1, as informações de geolocalização serão adicionadas ao lado direito da tela Assinatura Escrita.


![rabisco de assinatura-fundo](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>As assinaturas são sempre salvas no formato PNG.

## Configurar um formulário adaptável para usar a assinatura à mão {#configure-an-adaptive-form-to-use-scribble-signature}

1. Abra um Formulário adaptável em um modo de edição.
1. Arraste e solte o componente **Assinatura Escrita** do navegador de componentes para o Formulário Adaptável.
1. Selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre as propriedades do navegador e exibe as propriedades do componente Assinatura Escrita. [Configure as propriedades da assinatura de Rabisco](#properties-of-scribble-signature-component) conforme discutido na próxima seção.

   ![Assinatura Escrita](/help/forms/assets/scribblesig.png)

1. Selecione o ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) para salvar as alterações. A Assinatura foi configurada com sucesso.

## Configurar propriedades do componente de assinatura de assinatura de assinatura

Você pode personalizar facilmente o componente Assinatura Escrita para visitantes com a Caixa de diálogo de configuração.

### Guia Básico

![Guia Básico](/help/forms/assets/scribblesig-basic.png)

* **Nome**: é possível identificar um componente de formulário facilmente com seu nome exclusivo no formulário e no editor de regras, mas o nome não pode conter espaços ou caracteres especiais.

* **Título**: o título permite identificar facilmente um componente em um formulário; por padrão, ele aparece na parte superior do componente. Se um título não for adicionado, o nome do componente será exibido em vez do texto do título.

* **Permitir rich text para título**: esse recurso permite formatar títulos de texto simples, incorporando recursos como negrito, itálico, texto sublinhado, várias fontes, tamanhos de fonte, cores e uma opção adicional para aprimorar a apresentação visual e a personalização. Ele oferece maior flexibilidade e controle criativo para que os títulos se destaquem em documentos, sites ou aplicativos.\
  Ao marcar a caixa de seleção **Permitir rich text para título**, as opções de formatação se tornam visíveis para estilizar o título do componente. Para acessar todas as opções de formatação disponíveis, clique no ![Ícone de tela cheia](/help/forms/assets/fullscreen-icon.png).

  ![Suporte a rich text](/help/forms/assets/richtext-support-title.png)

* **Ocultar título**: selecione essa opção para ocultar o título do componente.
* **Campo Obrigatório** - Selecione a opção para tornar o campo obrigatório.
* **Mensagem do Campo Obrigatório** - A **Mensagem do Campo Obrigatório** é uma mensagem personalizável exibida aos usuários quando eles tentam enviar um formulário sem preencher um campo obrigatório.
* **Referência de Associação de Modelo de Dados** - Uma referência de associação é uma referência a um elemento de dados armazenado em uma fonte de dados externa e usado em um formulário. A referência de vínculo permite vincular dinamicamente os dados a campos de formulário, de modo que o formulário possa exibir os dados mais atualizados da fonte de dados. Por exemplo, uma referência de vínculo pode ser usada para exibir o nome e o endereço de um cliente em um formulário, com base na ID do cliente inserida no formulário. A referência de vínculo também pode ser usada para atualizar a fonte de dados com os dados inseridos no formulário. Dessa forma, o AEM Forms permite criar formulários que interagem com fontes de dados externas, fornecendo uma experiência do usuário perfeita para coletar e gerenciar dados.
* **Ocultar Objeto** - Selecione a opção para ocultar o componente do formulário. O componente permanece acessível para outros fins, como usá-lo para cálculos no Editor de regras. Isso é útil quando você precisa armazenar informações que não precisam ser vistas ou alteradas diretamente pelo usuário.
* **Desabilitar Objeto** - Selecione a opção para desabilitar o componente. O componente desativado não está ativo nem editável pelo usuário final. O usuário pode ver o valor do campo, mas não pode modificá-lo. O componente permanece acessível para outros fins, como usá-lo para cálculos no Editor de regras.
* **Taxa de Proporção** - A taxa de proporção em um componente de Assinatura Escrita define a relação proporcional entre sua largura e altura.
* **Layout do campo** - A opção **Layout do campo** determina como os elementos do formulário, incluindo os rótulos (legendas) e as mensagens de erro, são posicionados em relação ao componente. A **Legenda e Erro como Parte Superior do Widget** posiciona a legenda do campo (rótulo) e as mensagens de erro acima do componente. **Herdar da Configuração do Formulário Adaptável** usa as configurações de layout de campo padrão especificadas na configuração do Formulário Adaptável.
* **Classe CSS** - A **classe CSS** permite aplicar estilos personalizados a um componente, atribuindo uma ou mais classes CSS definidas na folha de estilos. Ele permite a personalização consistente de estilo e layout no Formulário adaptável.

### Conteúdo de Ajuda

![Guia Conteúdo de ajuda](/help/forms/assets/scribblesig-help.png)

* **Descrição curta**: uma descrição curta é uma breve explicação em texto que fornece informações adicionais ou esclarecimentos sobre a finalidade de um campo de formulário específico. Ela ajuda o usuário a entender qual tipo de dados deve ser inserido no campo e pode fornecer diretrizes ou exemplos para ajudar a garantir que as informações inseridas sejam válidas e atendam aos critérios desejados. Por padrão, as descrições curtas permanecem ocultas. Habilite a opção **Sempre mostrar descrição curta** para exibi-la abaixo do componente.

* **Sempre mostrar descrição curta**: habilite essa opção para exibir a descrição curta abaixo do componente.

* **Descrição longa** - Refere-se às informações ou orientações adicionais fornecidas ao usuário para ajudá-lo a preencher um campo de formulário corretamente. Ele é exibido quando o usuário clica no ícone de ajuda (i) colocado ao lado do componente. Ele fornece informações mais detalhadas do que o rótulo de um campo de formulário ou texto de espaço reservado e foi projetado para ajudar o usuário a entender os requisitos ou restrições do campo. Ele também pode oferecer sugestões ou exemplos para tornar o preenchimento do formulário mais fácil e preciso.

### Guia Acessibilidade {#accessibility}

![Guia Acessibilidade](/help/forms/assets/scribblesig-acc.png)

Na guia **Acessibilidade**, é possível definir os valores dos rótulos de [acessibilidade ARIA](https://www.w3.org/WAI/standards-guidelines/aria/) do componente. Várias opções estão disponíveis para usar o texto para leitor de tela:

* **Precedência de Screen Reader** - A Precedência de Screen Reader refere-se a um texto adicional especificamente destinado a ser lido por tecnologias assistivas, como leitores de tela, usados por indivíduos com deficiência visual. Esse texto fornece uma descrição de áudio da finalidade do campo de formulário e pode incluir informações sobre o título do campo, a descrição, o nome e quaisquer mensagens relevantes (texto personalizado). O texto do leitor de tela ajuda a garantir que o formulário seja acessível a todos os usuários, incluindo aqueles com deficiências visuais, e fornece a eles uma compreensão completa do campo de formulário e de seus requisitos.

   * **Texto personalizado**: selecione essa opção para usar o texto personalizado para rótulos de acessibilidade ARIA. Selecionar essa opção exibe a caixa de diálogo Texto personalizado. Você pode adicionar informações relevantes na caixa de diálogo Texto personalizado.
   * **Descrição curta**: selecione esta opção para usar a descrição para rótulos de acessibilidade ARIA.
   * **Título**: selecione essa opção para usar o título para rótulos de acessibilidade ARIA.
   * **Nome**: selecione essa opção para usar o nome para rótulos de acessibilidade ARIA.
   * **Nenhum**: selecione essa opção se não quiser adicionar rótulos de acessibilidade ARIA.

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## Consulte também {#see-also}

{{see-also}}