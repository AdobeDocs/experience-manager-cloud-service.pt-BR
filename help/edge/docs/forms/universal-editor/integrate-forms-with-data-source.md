---
title: Como criar o Modelo de dados de formulário (FDM) para um formulário no Universal Editor?
description: Saiba como criar formulários com base em um modelo de dados de formulário (FDM). Gere e edite dados de amostra para objetos de modelo de dados no FDM.
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
source-git-commit: e2259e542df5a12748705af901d073e4486292c4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 2%

---


# Integrar formulários com o Modelo de dados de formulário no Editor universal

A integração de formulários com um Modelo de dados de formulário (FDM) no Universal Editor permite usar diversas fontes de dados de back-end para criar um Modelo de dados de formulário (FDM). Você pode usar o Modelo de dados de formulário (FDM) como um esquema em vários workflows de formulário. Configure as fontes de dados e crie um Modelo de dados de formulário (FDM) com base nos objetos de modelo de dados e serviços disponíveis nas fontes de dados.

## Consideração

* No momento, não há suporte para o serviço de preenchimento prévio de formulários no Editor Universal.

## Pré-requisitos

Antes de configurar seu formulário com o Modelo de dados de formulário no Universal Editor, verifique se você concluiu as seguintes etapas:

* [Configurar Data Source](/help/forms/configure-data-sources.md): configure a fonte de dados para conectar seu formulário aos dados de back-end.
* [Criar Modelo de Dados de Formulário (FDM)](/help/forms/create-form-data-models.md): crie um modelo de dados usando objetos de dados e serviços da fonte de dados configurada.
* [Configurar Serviços e Objetos de Modelo de Dados](/help/forms/work-with-form-data-model.md): mapeie os serviços e objetos de modelo de dados para garantir um fluxo de dados suave entre o formulário e a fonte de dados.

## Criação de Forms com modelo de dados de formulário no Editor universal

No Editor universal, é possível criar:
* [Formulário baseado em esquema](#schema-based-form): um formulário baseado em esquema usa uma fonte de dados configurada durante a criação do formulário na guia **Dados**, associando dados automaticamente a campos de formulário.
* [Formulário não baseado em esquema](#non-schema-based-form): um formulário não baseado em esquema requer a adição manual de uma fonte de dados e a associação de cada campo da árvore de conteúdo.

![Tipos de Formulário no Editor Universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

Esses métodos oferecem a flexibilidade de conectar modelos de dados a formulários com base nas suas necessidades.

### Formulário baseado em esquema

Ao criar um formulário baseado em esquema, ele é configurado automaticamente com uma fonte de dados e os campos do formulário já estão vinculados aos dados por meio de associações de dados. Para criar um formulário baseado em esquema usando o assistente de Criação de formulários, execute as seguintes etapas:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].
2. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
3. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto. Na guia **Source**, selecione um modelo:

   ![Modelo do Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

   Quando você seleciona um modelo baseado em Edge Delivery Services, o botão **[!UICONTROL Criar]** é habilitado. Você pode ir para as guias **[!UICONTROL Data Source]** ou **[!UICONTROL Envio]** para selecionar uma fonte de dados ou uma ação de envio.

4. Na guia **Dados**, você pode selecionar um dos seguintes modelos de dados:

   * **Modelo de dados de formulário (FDM)**: integre objetos de modelo de dados e serviços de fontes de dados ao seu formulário. Escolha Modelo de dados de formulário (FDM) se o formulário exigir leitura e gravação de dados de várias fontes.

   * **Esquema JSON**: integre seu formulário a um sistema de back-end associando um esquema JSON que define a estrutura de dados. Ela permite adicionar conteúdo dinâmico usando os elementos do esquema.

     Por exemplo, selecione o Modelo de dados de formulário criado chamado Modelo de dados de formulário Pet.

     ![Selecionar modelo de dados do formulário](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     Por padrão, todos os campos do esquema JSON associado ou do Modelo de dados de formulário (FDM) são automaticamente selecionados e convertidos em componentes de formulário correspondentes, simplificando o processo de criação. O assistente também permite escolher seletivamente quais campos incluir no formulário usando caixas de seleção.

5. Clique em **[!UICONTROL Criar]** e o assistente **Criar formulário** será exibido.
6. Especifique o **Nome** e o **Título**.
7. Especifique a **URL do GitHub**. Por exemplo, se o repositório GitHub for nomeado como `edsforms`, ele estiver localizado na conta `wkndforms`, a URL será:
   `https://github.com/wkndforms/edsforms`
8. Clique em **[!UICONTROL Criar]**.

   ![Criar formulário baseado em esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   Assim que você clicar em **[!UICONTROL Criar]**, o formulário será aberto no editor universal para criação.

   ![crie o formulário](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   O formulário é criado usando os elementos de dados da fonte de dados associada, com os campos de formulário com vinculação de dados pré-configurada.

   ![Associação Automática de Dados](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Agora você pode adicionar e [configurar a ação de envio](/help/edge/docs/forms/universal-editor/submit-action.md) para o seu formulário.

### Formulário não baseado em esquema

Ao criar um formulário não baseado em esquema, nenhuma fonte de dados é configurada. É possível editar as propriedades do formulário posteriormente para adicionar uma fonte de dados e configurar manualmente as associações de dados para seus campos de formulário. Execute as seguintes etapas para editar as propriedades do formulário e adicionar uma fonte de dados:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].
1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o formulário ao qual deseja adicionar a fonte de dados e clique em **[!UICONTROL Propriedades]**.
   ![Abrir propriedades do formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   As propriedades do formulário são abertas.
1. Clique para abrir a guia **Modelo de formulário** e no menu suspenso **Selecionar de**. Você pode selecionar uma das seguintes opções:

   * **Modelo de dados de formulário (FDM)**: crie o formulário usando um modelo de dados de formulário.
   * **Conector**: crie o formulário usando a fonte de dados do Adobe Marketo.
   * **Esquema**: crie o formulário usando um esquema JSON carregado para o AEM Forms.
   * **Nenhum**: criar o formulário do zero sem usar nenhum modelo de formulário.

     Por exemplo, selecione o Modelo de dados de formulário (FDM)

     ![Guia Selecionar modelo de formulário](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. Selecione o modelo de dados de formulário (FDM) criado na lista suspensa. Por exemplo, selecione o Modelo de dados de formulário criado chamado Modelo de dados de formulário Pet na lista suspensa.

   ![Selecionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   Quando você seleciona o Modelo de dados de formulário (FDM), a caixa de diálogo de aviso é exibida. Clique em **OK** para fechar a caixa de diálogo.

   ![Assistente de Modelo de Formulário](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. Clique em **[!UICONTROL Salvar e fechar]**.
1. Abra o formulário para edição. O formulário é aberto no Editor universal para criação.

   ![Criação de formulário não baseada em esquema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   Os elementos de formulário presentes no Form Data Model (FDM) associado são exibidos na guia **[!UICONTROL Datasource]** do **[!UICONTROL Navegador de Conteúdo]** no **Painel de Propriedades**.

   ![Source de dados de formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. Selecione os elementos de dados na guia **[!UICONTROL Datasource]** e clique em **[!UICONTROL Adicionar]**.

   ![Adicionar elementos de dados](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   Você também pode arrastar e soltar esses elementos para criar o Formulário adaptável. Ao clicar em **[!UICONTROL Adicionar]**, os elementos selecionados da guia **[!UICONTROL Fonte de Dados]** são adicionados ao formulário e uma marca de verificação é exibida na frente dos elementos adicionados.

   ![Formulário de compilação](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   Você também pode adicionar manualmente uma associação de dados a um elemento de formulário especificando-a nas propriedades **Bind Reference** do elemento de formulário.
Por exemplo, vamos adicionar uma referência de associação de dados à caixa de texto **Nome do animal de estimação** que já está presente no formulário:

   ![Adicionar manualmente a ligação de dados para um campo de formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   Agora você pode adicionar e [configurar a ação de envio](/help/edge/docs/forms/universal-editor/submit-action.md) para o seu formulário.

## Consulte também:

{{universal-editor-see-also}}
