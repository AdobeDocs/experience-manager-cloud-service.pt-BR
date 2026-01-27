---
title: Como criar um formulário adaptável com base nos Componentes principais usando modelos de formulário XFA?
description: Saiba como criar um formulário adaptável usando  [!DNL Experience Manager Forms] os modelos de formulário XFA ou arquivos XDP.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: f3c9b798-8b20-4674-9b96-a3a0b143d947
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 12%

---

# Criar um formulário adaptável (componentes principais) com base em modelos de formulário XFA

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O AEM as a Cloud Service fornece aos usuários a opção de criar o Forms adaptável com base nos Componentes principais usando modelos de formulário XFA (XML Forms Architecture) ou arquivos `*.XDP` (XML Data Package). Esse recurso permite que os usuários economizem tempo migrando campos do modelo de formulário XFA ou arquivos XDP diretamente para o Adaptive Forms.

Você pode redefinir o modelo de formulário XFA ou os modelos de formulário de arquivos XDP para criar o Forms adaptável com base nos Componentes principais. Para redefinir objetivos, carregue e associe um modelo de formulário XFA ou arquivos XDP a um formulário adaptável. Os elementos do modelo de formulário XFA ou dos arquivos XDP ficam disponíveis para uso no localizador de conteúdo durante a criação do Formulário adaptável. No Localizador de conteúdo, você pode arrastar e soltar os elementos do modelo de formulário no formulário.

## Vantagens de criar formulários com base em modelos de Formulário XFA ou arquivos XDP

Algumas das vantagens de criar formulários com base em modelos de formulário XFA ou arquivos XDP são:

* **Economia de tempo**: você pode reutilizar rapidamente modelos de formulário XFA (arquivos XDP) existentes sem precisar recriar a estrutura do formulário, economizando tempo e esforço durante o processo de criação.
* **Migração sem esforço**: se você já tiver modelos de formulário XFA em uso, essa opção fornecerá um caminho de migração fácil para o Adaptive Forms, permitindo que você aproveite os benefícios dos Componentes principais modernos do AEM sem perder a lógica e os dados de formulário existentes.
* **Experiência do usuário aprimorada**: o Forms adaptável é mais responsivo e personalizável do que os formulários XFA. Ao fazer a transição para o Adaptive Forms, você pode garantir uma experiência mais amigável em diferentes dispositivos e tamanhos de tela.
* **Integração aprimorada**: o Forms adaptável integra-se melhor com outros recursos, como fluxos de trabalho, associação de dados e envios de formulários, permitindo fluxos de trabalho mais suaves e um melhor gerenciamento geral de formulários.

## Pré-requisitos


* Recomenda-se o conhecimento das seguintes áreas:
   * Criação de um formulário adaptável
   * XFA (XML Forms Architecture, arquitetura XML do)

## Como criar um formulário adaptável usando modelos de formulário XFA ou arquivos XDP?

Execute as seguintes etapas para criar um Formulário adaptável usando modelos de formulário XFA ou XDP:

1. Faça logon na instância de autor do [!DNL Experience Manager Forms].
1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Forms e Documentos](/help/forms/assets/create-fdm.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**.

   ![Criar formulário adaptável](/help/forms/assets/create-af.png)

   O assistente de criação de Formulário é aberto.
1. Na guia **Source**, selecione um modelo baseado em Componentes Principais.

   ![Selecionar modelo](/help/forms/assets/select-template.png)

   Quando você seleciona um modelo, um tema e uma ação de envio especificados no modelo são selecionados automaticamente e o botão **[!UICONTROL Criar]** é habilitado.

   ![Selecionar tema](/help/forms/assets/select-form-theme.png)

1. Selecione **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptável é exibida.
1. Especifique o título, o nome e o local.
1. Selecione **[!UICONTROL Criar]**.
   ![Fornecer nome e título](/help/forms/assets/create-form.png)

   Um Formulário adaptável será criado e aberto no editor de Formulários adaptáveis. O editor exibe o conteúdo disponível no modelo.
1. Selecione ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**.

   ![Abrir propriedades](/help/forms/assets/form-properties.png)

   A página Propriedades do formulário será aberta.
1. Vá para a guia **[!UICONTROL Modelo de formulário]** e escolha **Modelos de formulário**.
1. Selecione o arquivo .xdp na lista suspensa.

   ![Selecionar arquivo XDP](/help/forms/assets/select-xdp-file.png)

   Uma caixa de diálogo de aviso é exibida na tela. Clique em **OK** para continuar.

   ![Caixa de Diálogo de Aviso](/help/forms/assets/fdm-warning.png)

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar as propriedades.

   >[!NOTE]
   >
   > Depois de selecionar **Modelos de Formulário** na guia Formulário **Modelo**, ele não pode ser alterado.


Um Formulário adaptável será criado e aberto no editor de Formulários adaptáveis. O editor exibirá o conteúdo disponível no modelo.  Com base no tipo de Formulário adaptável, os elementos de formulário presentes no modelo de formulário XFA associado são exibidos na guia **[!UICONTROL Objetos do modelo de dados]** do **[!UICONTROL Navegador de conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar seu formulário adaptável.

>[!NOTE]
>
> Você pode desativar scripts para campos de formulário XDP usando a barra de ferramentas do painel do campo adicionado. Crie lógicas para os campos adicionados usando o [Editor de Regras Visuais](/help/forms/rule-editor-core-components.md).

