---
title: Como integrar o Modelo de dados de formulário (FDM) a um formulário no Universal Editor?
description: Saiba como criar formulários para serviços de entrega de borda com base em um modelo de dados de formulário (FDM). Gere e edite dados de amostra para objetos de modelo de dados no FDM.
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 7d3ea5bdc6545b9610f595660fcfb2ef70c837de
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---


# Integrar o Forms ao Modelo de dados de formulário (FDM)

Conecte seus formulários às fontes de dados de back-end usando o FDM para habilitar a associação de dados, a validação e os workflows de envio.

## Pré-requisitos

Conclua estas etapas antes de integrar o FDM aos seus formulários:

1. **[Configurar Data Source](/help/forms/configure-data-sources.md)**: configurar conexões de back-end
2. **[Criar modelo de dados de formulário](/help/forms/create-form-data-models.md)**: definir estrutura de dados e serviços
3. **[Configurar Objetos de Modelo de Dados](/help/forms/work-with-form-data-model.md)**: Mapear relações de dados

## Considerações

Se você não vir o ícone de **Fontes de Dados** na interface do Universal Editor ou a propriedade **Associar Referência** no painel de propriedades direito, habilite a extensão de **Fonte de Dados** no **Extension Manager**.

![Captura de tela da interface do Universal Editor Extension Manager mostrando as extensões disponíveis, incluindo a extensão de Fontes de Dados que pode ser habilitada para integração de formulários](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar e desabilitar extensões no Universal Editor.

## Escolher o tipo de formulário

O Universal Editor oferece suporte a duas abordagens de criação de formulários:

| Aspecto | Formulário baseado em esquema | Formulário não baseado em esquema |
|--------|-------------------|----------------------|
| **Complexidade da Instalação** | Simples (vínculo automático) | Manual (vinculação campo por campo) |
| **Caso de uso** | Novos formulários com estrutura de dados definida | Formulários existentes ou requisitos flexíveis |
| **Source de dados** | Obrigatório durante a criação | Pode ser adicionado mais tarde |
| **Associação** | Associação de campo automática | Vinculação manual por campo |

![Tipos de Formulário no Editor Universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Formulário baseado em esquema

Os formulários baseados em esquema configuram fontes de dados automaticamente e vinculam campos de formulário aos dados. Essa abordagem é ideal para novos formulários com estruturas de dados bem definidas.

### Criar formulário baseado em esquema

1. **Acessar o Forms Console**
   - Faça logon na sua instância de Autor do [!DNL Experience Manager Forms]
   - Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**

2. **Iniciar Criação de Formulário**
   - Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**
   - Escolha um modelo do Edge Delivery Services
   - Clique em **[!UICONTROL Criar]** quando habilitado

   ![Modelo do Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

3. **Configurar Modelo de Dados**
   - Vá para a guia **Dados**
   - Selecione o **Modelo de Dados de Formulário (FDM)** para várias fontes de dados ou o **Esquema JSON** para um único sistema de back-end
   - Escolha o FDM criado (por exemplo, Modelo de dados do formulário Pet)

   ![Selecionar modelo de dados do formulário](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Concluir configuração do formulário**
   - Inserir **Nome** e **Título**
   - Especifique a **URL do GitHub** (por exemplo, `https://github.com/wkndforms/edsforms`)
   - Clique em **[!UICONTROL Criar]**

   ![Criar formulário baseado em esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verificar Formulário Baseado em Esquema

O formulário é aberto no Universal Editor com vinculação de dados pré-configurada:

![Captura de tela do Editor Universal mostrando um formulário baseado em esquema com campos de formulário pré-preenchidos e o Navegador de Conteúdo exibindo elementos de fonte de dados disponíveis](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Associação Automática de Dados](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Formulário não baseado em esquema

Formulários que não sejam de esquema exigem configuração manual da fonte de dados e associação de campo. Essa abordagem oferece flexibilidade para formulários existentes ou requisitos complexos.

### Criar formulário não baseado em esquema

1. **Acessar Propriedades do Formulário**
   - Faça logon na sua instância de Autor do [!DNL Experience Manager Forms]
   - Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**
   - Selecione seu formulário e clique em **[!UICONTROL Propriedades]**

   ![Abrir propriedades do formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Configurar Modelo de Formulário**
   - Abra a guia **Modelo de formulário**
   - Selecione o **Modelo de Dados de Formulário (FDM)** na lista suspensa **Selecionar de**
   - Escolha seu FDM na lista

   ![Guia Selecionar modelo de formulário](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Selecionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Confirmar configuração**
   - Clique em **OK** na caixa de diálogo de aviso
   - Clique em **[!UICONTROL Salvar e fechar]**

   ![Assistente de Modelo de Formulário](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Adicionar elementos de dados

1. **Abrir formulário para edição**
   - O formulário é aberto no Universal Editor

   ![Criação de formulário não baseada em esquema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Acessar Elementos de Source de Dados**
   - Vá para a guia **[!UICONTROL Fonte de Dados]** no **[!UICONTROL Navegador de Conteúdo]**
   - Exibir elementos de dados disponíveis no FDM

   ![Source de dados de formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Adicionar elementos ao formulário**
   - Selecione os elementos de dados e clique em **[!UICONTROL Adicionar]**
   - Ou arraste e solte elementos para criar seu formulário

   ![Adicionar elementos de dados](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Captura de tela mostrando o Editor Universal com um formulário não de esquema sendo criado ao arrastar e soltar elementos de dados da guia Data Source na estrutura do formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Adicionar vinculação de dados manual

Para campos de formulário existentes, adicione a associação de dados por meio da propriedade **Referência de Associação**:

1. **Abrir Propriedades do Campo**
   - Selecionar o campo de formulário para vinculação
   - Abrir o painel de propriedades

2. **Configurar Referência de Ligação**
   - Vá para a propriedade **Referência de Ligação**
   - Clique no ícone **Procurar**

   ![Adicionar manualmente a ligação de dados para um campo de formulário](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Selecionar Elemento de Dados**
   - Escolha na árvore da fonte de dados no assistente **Selecionar uma Referência de Associação**
   - Selecione o elemento de dados desejado e clique em **Selecionar**

   ![selecionar referência de associação de dados](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![selecionar elemento de dados](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verificar Associação**
   - O campo de formulário agora se associa ao elemento de dados
   - A associação aparece na propriedade **Referência de Associação**

   ![Associação Automática de Dados](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verificar integração

Após concluir a integração:

1. **Testar associação de dados**: verificar se os campos do formulário exibem dados corretos
2. **Validar envios**: certifique-se de que os dados sejam salvos nas fontes configuradas
3. **Verificar tratamento de erros**: teste com cenários de dados inválidos

## Próximas etapas

Configure [enviar ações](/help/edge/docs/forms/universal-editor/submit-action.md) para concluir o fluxo de trabalho do formulário.
