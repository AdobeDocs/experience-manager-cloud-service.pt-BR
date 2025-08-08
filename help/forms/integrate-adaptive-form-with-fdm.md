---
title: Como integrar o Modelo de dados de formulário (FDM) de um formulário com o Formulário adaptável?
description: Saiba como criar formulários com base em um modelo de dados de formulário (FDM). Gere e edite dados de amostra para objetos de modelo de dados no FDM.
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Integrar formulários com o Modelo de dados de formulário

A integração de formulários com um Modelo de dados de formulário (FDM) permite usar diversas fontes de dados de back-end para criar um Modelo de dados de formulário (FDM). Você pode usar o Modelo de dados de formulário (FDM) como um esquema em vários workflows de formulário. Configure as fontes de dados e crie um Modelo de dados de formulário (FDM) com base nos objetos de modelo de dados e serviços disponíveis nas fontes de dados.

## Vantagens de integrar o Forms ao Form Data Model (FDM)

* **Conectividade de Back-end Contínua**: conecte formulários a vários sistemas de back-end (por exemplo, bancos de dados, APIs REST, serviços SOAP, CRMs) sem código personalizado. Isso permite a troca de dados em tempo real e reduz o esforço de integração.
* **Esquema de dados centralizado** O modelo de dados de formulário serve como um esquema de dados unificado que simplifica o mapeamento e o gerenciamento de objetos de dados e serviços usados em vários formulários e fluxos de trabalho.

* **Preenchimento e Envio de Formulário aprimorados**: configure facilmente ações de preenchimento e envio usando os serviços de Dados de Formulário, garantindo uma recuperação e um armazenamento de dados precisos e atualizados.

* **Suporte para Fluxos de Trabalho Dinâmicos**: o Modelo de Dados de Formulário pode ser integrado a fluxos de trabalho para automatizar processos comerciais com base em dados enviados ou recuperados, melhorando a eficiência geral.

## Pré-requisitos

Antes de configurar seu formulário com o Modelo de dados de formulário, verifique se você concluiu as seguintes etapas:

* [Configurar Data Source](/help/forms/configure-data-sources.md): configure a fonte de dados para conectar seu formulário aos dados de back-end.
* [Criar Modelo de Dados de Formulário (FDM)](/help/forms/create-form-data-models.md): crie um modelo de dados usando objetos de dados e serviços da fonte de dados configurada.
* [Configurar Serviços e Objetos de Modelo de Dados](/help/forms/work-with-form-data-model.md): mapeie os serviços e objetos de modelo de dados para garantir um fluxo de dados suave entre o formulário e a fonte de dados.

>[!BEGINTABS]

>[!TAB Componente de base]

Execute as seguintes etapas para configurar o Modelo de dados de formulário com o Formulário adaptável baseado no Componente de base como:

1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar Usando o Modelo de Dados de Formulário]**.

   ![enviar usando o Modelo de Dados de Formulário](/help/forms/assets/submit-uisng-fdm-fc.png)

1. Selecione o **[!UICONTROL Modelo de Dados criado para enviar a configuração]**.
Para enviar anexos ao banco de dados, selecione **Enviar anexos de formulário**. O Documento de Registro (DoR) é salvo no banco de dados selecionando **Enviar Documento de Registro**.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

>[!TAB Componente principal]

Execute as seguintes etapas para configurar o Modelo de dados de formulário com o Formulário adaptável com base no Componente principal como:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[Enviar Usando o Modelo de Dados de Formulário]**.
   ![enviar usando o Modelo de Dados de Formulário](/help/forms/assets/submit-uisng-fdm-cc.png)

1. Selecione o **[!UICONTROL Modelo de Dados criado para enviar a configuração]**.
Para enviar anexos ao banco de dados, selecione **Enviar anexos de formulário**. O Documento de Registro (DoR) é salvo no banco de dados selecionando **Enviar Documento de Registro**.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

>[!TAB Editor Universal]

Execute as seguintes etapas para configurar o Modelo de dados de formulário com o Formulário adaptável criado em Universal como:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.

   A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

1. Clique na guia **Envio** e selecione **[!UICONTROL Enviar usando o Modelo de Dados de Formulário]**.

   ![OneDrive GIF](/help/forms/assets/submit-uisng-fdm-ue.png)
Se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais. Você também pode salvar o Documento de registro (DoR) no Armazenamento de blobs do Azure.

1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar&amp;Fechar]**

Para obter instruções detalhadas sobre como integrar formulários criados no Universal Editor, consulte o artigo [Integrar o Forms ao Modelo de Dados de Formulário no Universal Editor](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

>[!ENDTABS]

## Artigos relacionados

{{af-submit-action}}
