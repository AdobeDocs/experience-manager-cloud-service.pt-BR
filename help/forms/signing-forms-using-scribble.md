---
title: Aplicar assinaturas eletrônicas a um formulário usando assinaturas do scribble
seo-title: Apply electronic signatures to a form using scribble signatures
description: Assinar formulários usando o scribble
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 73953a3d71f3328def3bd4c1f03516b4839695ea
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Aplicar assinaturas eletrônicas a um formulário usando assinaturas do scribble{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Você pode usar o **Assinatura do Scribble** componente e **Etapa de assinatura** componente para desenhar (Scribble) assinatura em um formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do formulário adaptável. Você precisa ter uma opção Documento de registro ativada ou um modelo de formulário baseado em Adaptive Forms para usar o componente Etapa de assinatura.

Ambos os componentes fornecem uma janela, conforme exibido abaixo, para assinar um formulário. Você também pode clicar no ícone de geolocalização ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) para adicionar geolocalização à assinatura.

![Caixa de diálogo de sinal de rabisco](assets/scribble-signature.png)

## Configurar um formulário adaptável para usar a assinatura do Scribble {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crie uma opção Documento de registro ativada ou o modelo de formulário baseado em Formulário adaptável. Para obter informações passo a passo, consulte [Criação de um formulário adaptável](creating-adaptive-form.md).
1. Arraste e solte a **Assinatura do Scribble** do navegador de componentes ao Formulário adaptável.
1. Toque no **Configurar** ![configure](assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades do componente Assinatura do rabisco. Configure as propriedades do componente Assinatura do Scribble.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o Formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contenha o componente Etapa de assinatura.

1. No navegador Conteúdo, toque em **Contêiner de formulário** e toque no **Configurar** ![](assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades do contêiner do Formulário adaptável. Navegar para **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Ativar o Adobe Sign** opção. Toque em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um Formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.

1. Toque no **Configurar** ![configure](assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do elemento**: Especifique o nome do componente.

   * **Título:** Especifique o título exclusivo do componente.
   * **Mensagem do modelo:** Especifique a mensagem a ser exibida enquanto o PDF de assinatura está sendo carregado. Os serviços da Adobe Sign levam algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** Selecione o **Assinatura do Scribble** opção.

   * **Classe CSS**: Especifique a classe CSS da biblioteca do cliente, se houver. Recomenda-se a utilização de [temas](themes.md) e [estilos em linha](inline-style-adaptive-forms.md) em vez de Classe CSS.

   Toque em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações. A Assinatura é configurada com êxito.

   Agora, quando você preenche um formulário, uma versão PDF do formulário adaptável é exibida e opções para assinar o documento PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando a assinatura do Scribble](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a assinatura do Scribble {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e acessar a página Etapa de assinatura, a tela de assinatura é exibida.

   ![Tela de assinatura para a página do EchoSign](assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Sign]**. A caixa de diálogo de sinal de rabisco é exibida. Assine o formulário e clique em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar a assinatura.

   ![Caixa de diálogo de sinal de rabisco](assets/scribblewidget.jpg)

1. Clique em concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.

