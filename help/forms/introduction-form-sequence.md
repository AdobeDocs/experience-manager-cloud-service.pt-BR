---
title: Como criar uma sequência de formulário de várias etapas?
description: Com [!DNL Experience Manager Forms], é possível definir uma sequência de painéis de formulário para que os usuários naveguem e preencham um Formulário adaptável. Saiba mais usando a abordagem de caso de uso como exemplo para criar uma sequência de formulário em várias etapas.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Introdução à sequência de formulários em várias etapas {#introduction-to-multi-step-form-sequence}

O Adaptive Forms permite que os autores de formulários criem uma experiência de captura de dados em várias etapas com grande facilidade. Ele é fornecido com suporte integrado para criar vários painéis e associar cada painel a diferentes padrões de navegação. Os Autores do formulário podem agrupar campos de formulário em seções lógicas e representar um grupo como um painel. A navegação geral entre painéis é controlada com o layout do painel. Os autores podem optar por organizar painéis em diferentes layouts, por exemplo, colocando sequencialmente usando o layout do Assistente ou de maneira ad hoc usando o layout de Tabelas. Para obter informações sobre layouts de painel, consulte [Recursos de layout do Adaptive Forms](layout-capabilities-adaptive-forms.md).

Em uma experiência típica de preenchimento de formulário, há mais etapas envolvidas do que apenas capturar dados. Um envio de formulário completo pode incluir outras etapas, como a assinatura digital do formulário, a verificação das informações preenchidas no formulário, o processamento de pagamentos e assim por diante. Difere de caso para caso.

Se o seu caso de uso determinar um conjunto de etapas para a captura de dados ou houver regulamentos que precisam de determinadas etapas a serem seguidas, [!DNL Experience Manager Forms] O fornece uma maneira de aplicar essa estrutura comum em todos os formulários. A implementação premeditada da estrutura do formulário define a sequência de etapas para um formulário. ![Exemplo de uma sequência de formulário em várias etapas](assets/formpipeline.png)

Exemplo de uma sequência de formulário em várias etapas

Use um caso de uso em que você deve criar uma sequência para preencher, verificar, assinar e confirmar as etapas de um formulário. As etapas para criar essa sequência são as seguintes:

1. Defina um modelo de formulário e adicione o painel necessário a ele. Deve haver um painel para cada etapa na sequência. No entanto, é possível incluir subpainéis dentro de um painel.

   Neste exemplo, podemos adicionar os seguintes painéis:

   * **[!UICONTROL Preenchimento]**: Ele contém campos de formulários para capturar dados. Aqui, você pode incluir subpainéis aninhados para criar seções para diferentes tipos de informações, como pessoais, familiares, financeiras e assim por diante.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL Assinatura eletrônica]**: Ele contém a variável **[!UICONTROL Sign]** componente que pode ser usado em um formulário adaptável baseado em XFA. Ele fornece os seguintes serviços de assinatura:

      * Serviços de eSign da Adobe Document Cloud
      * Assinatura
   * **[!UICONTROL Confirmação]**: Ele contém a variável **[!UICONTROL Resumo]** componente que exibe uma mensagem confirmando o envio do formulário depois que um usuário assina o formulário e atinge a etapa Confirmação (Resumo) na sequência. Os autores podem configurar o texto da variável [!UICONTROL Resumo] , mostrar uma mensagem de agradecimento, mostrar um link para o PDF gerado e assim por diante.



1. Selecione o layout do painel raiz como **[!UICONTROL Assistente]**.
1. Complete as etapas restantes para criar o template de formulário. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

Depois de definir a sequência de formulário no modelo de formulário, é possível usá-lo para criar formulários que terão a estrutura básica definida como a sequência em vigor, embora seja sempre possível personalizar o formulário para atender às suas necessidades.
