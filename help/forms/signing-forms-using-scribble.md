---
title: Como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas?
description: Saiba como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---

# Assinatura eletrônica de um formulário usando assinaturas escritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Este artigo |


Você pode usar o componente **Assinatura Escrita** e o componente **Etapa de Assinatura** para desenhar (Rabiscar) uma assinatura em um Formulário Adaptável. O componente Etapa de assinatura exibe uma versão PDF do Formulário adaptável. Você precisa de uma opção Documento de registro ativada ou de um modelo de formulário baseado no Adaptive Forms para usar o componente Etapa de assinatura.

![Caixa de diálogo Assinar assinatura](assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **A:** Clique no ícone **Pincel de Tinta** para desenhar sua assinatura na tela.
* **B:** Clique no ícone **Limpar** para limpar a assinatura na tela.
* **C:** Clique no ícone **Geolocalização** para adicionar a geolocalização junto com a assinatura.
* **D:** Clique no ícone **Teclado** para digitar seu nome na tela.

Depois de selecionar o ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) na janela Assinatura escritas, você não poderá editar a assinatura. No caso, se você quiser editar a assinatura, desconsidere a assinatura atual e assine novamente usando a opção Pincel/Teclado acima.

Você pode selecionar o ícone **Configurar** ![configurar](assets/configure.png) para definir a proporção da tela Assinatura Escrita.
* Quando a proporção da tela Assinatura Escrita for menor que 1, as informações de localização geográfica serão adicionadas na parte inferior da tela Assinatura Escrita.


* Quando a proporção da tela Assinatura Escrita for maior que 1, as informações de geolocalização serão adicionadas ao lado direito da tela Assinatura Escrita.


![rabisco de assinatura-fundo](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>As assinaturas são sempre salvas em formato PNG.
>

## Configurar um formulário adaptável para usar a assinatura à mão {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crie uma opção Documento de registro ativada ou Formulário adaptável baseado em modelo de formulário. Para obter informações passo a passo, consulte [Criando um Formulário Adaptável](creating-adaptive-form.md).
1. Arraste e solte o componente **Assinatura Escrita** do navegador de componentes para o Formulário Adaptável.
1. Selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre as propriedades do navegador e exibe as propriedades do componente Assinatura Escrita. Configure as propriedades do componente Assinatura Escrita.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o Formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

1. No Navegador de conteúdo, selecione **Contêiner de formulário** e selecione o ícone **Configurar** ![configurar](assets/configure.png). Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável. Navegue até **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Habilitar Adobe Sign**. Selecione o ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.

1. Selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do Elemento**: especifique o nome do componente.

   * **Título:** especifique o título exclusivo do componente.
   * **Mensagem de modelo:** especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços da Adobe Sign demoram algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** selecione a opção **Assinatura assinável**.

   * **Classe CSS**: especifique a classe CSS da biblioteca do cliente, se houver. A Adobe recomenda usar [temas](themes.md) e [estilos embutidos](inline-style-adaptive-forms.md) em vez da Classe CSS.

   Selecione o ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) para salvar as alterações. A Assinatura foi configurada com sucesso.

   Agora, quando você preenche um formulário, uma versão de PDF do formulário adaptável é exibida e as opções para assinar o documento de PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um Formulário Adaptável usando a Assinatura Escrita](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a assinatura escritas {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e acessar a página Etapa de assinatura, a tela de assinatura é exibida.

   ![Tela de assinatura da página do EchoSign](assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Assinar]**. A caixa de diálogo assinar é exibida. Assine o formulário e clique no ícone Concluído ![aem_forms_save](assets/aem_forms_save.png) para salvar a assinatura.

   ![Caixa de diálogo Assinar assinatura](assets/scribblewidget.png)

1. Clique em Concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.

## Consulte também {#see-also}

{{see-also}}