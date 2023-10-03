---
title: Como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas?
description: Saiba como aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# Assinatura eletrônica de um formulário usando assinaturas escritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Este artigo |


Você pode usar o **Rabiscar a assinatura** componente e **Etapa de assinatura** componente para desenhar (Rabiscar) assinatura em um Formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do Formulário adaptável. Você precisa de uma opção Documento de registro ativada ou de um modelo de formulário baseado no Adaptive Forms para usar o componente Etapa de assinatura.

![Caixa de diálogo Scribble sign](assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **R:** Clique em **Pincel de pintura** ícone para desenhar sua assinatura na tela.
* **B:** Clique em **Limpar** ícone para limpar a assinatura na tela.
* **C:** Clique em **Localização geográfica** ícone para adicionar a localização geográfica junto com a assinatura.
* **D:** Clique em **Teclado** ícone para digitar seu nome na tela.

Depois de tocar em Concluído ![aem_forms_save](assets/aem_forms_save.png) ícone na janela Assinatura, não é possível editar a assinatura. No caso, se você quiser editar a assinatura, desconsidere a assinatura atual e assine novamente usando a opção Pincel/Teclado acima.

Você pode tocar no **Configurar** ![ícone de configuração](assets/configure.png) ícone para definir a proporção da tela Assinatura Escrita.
* Quando a proporção da tela Assinatura Escrita for menor que 1, as informações de localização geográfica serão adicionadas na parte inferior da tela Assinatura Escrita.


* Quando a proporção da tela Assinatura Escrita for maior que 1, as informações de geolocalização serão adicionadas ao lado direito da tela Assinatura Escrita.


![rabisco inferior de assinatura](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>As assinaturas são sempre salvas em formato PNG.
>

## Configurar um formulário adaptável para usar a assinatura à mão {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crie uma opção Documento de registro ativada ou Formulário adaptável baseado em modelo de formulário. Para obter informações passo a passo, consulte [Criação de um formulário adaptável](creating-adaptive-form.md).
1. Arraste e solte a variável **Rabiscar a assinatura** componente do navegador de componentes para o Formulário adaptável.
1. Toque no **Configurar** ![configurar](assets/configure.png) ícone. Ele abre as propriedades do navegador e exibe as propriedades do componente Assinatura Escrita. Configure as propriedades do componente Assinatura Escrita.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o Formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

1. No Navegador de conteúdo, toque em **Contêiner de formulário** e toque no **Configurar** ![ícone de configuração](assets/configure.png) ícone. Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável. Navegue até **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Ativar o Adobe Sign** opção. Toque no botão Concluído ![aem_forms_save](assets/aem_forms_save.png) ícone para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.

1. Toque no **Configurar** ![configurar](assets/configure.png) ícone. Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do elemento**: especifique o nome do componente.

   * **Título:** Especifique o título exclusivo do componente.
   * **Mensagem do modelo:** Especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços da Adobe Sign demoram algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** Selecione o **Rabiscar a assinatura** opção.

   * **Classe CSS**: especifique a classe CSS da biblioteca do cliente, se houver. É recomendável usar [temas](themes.md) e [estilos em linha](inline-style-adaptive-forms.md) em vez da classe CSS.

   Toque no botão Concluído ![aem_forms_save](assets/aem_forms_save.png) ícone para salvar as alterações. A Assinatura foi configurada com sucesso.

   Agora, quando você preenche um formulário, uma versão de PDF do formulário adaptável é exibida e as opções para assinar o documento de PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando a assinatura escritas](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a assinatura escritas {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e acessar a página Etapa de assinatura, a tela de assinatura é exibida.

   ![Tela de assinatura para página do EchoSign](assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Sign]**. A caixa de diálogo assinar é exibida. Assine o formulário e clique no link Concluído ![aem_forms_save](assets/aem_forms_save.png) ícone para salvar a assinatura.

   ![Caixa de diálogo Scribble sign](assets/scribblewidget.png)

1. Clique em Concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.
