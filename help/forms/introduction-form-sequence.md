---
title: Como criar uma sequência de formulário em várias etapas?
description: Com o [!DNL Experience Manager Forms], é possível definir uma sequência de painéis de formulário para os usuários navegarem e preencherem um formulário adaptável. Aprenda mais utilizando uma abordagem de caso de uso como exemplo para criar uma sequência de formulário em várias etapas.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: ht
source-wordcount: '486'
ht-degree: 100%

---

# Introdução à sequência de formulários em várias etapas {#introduction-to-multi-step-form-sequence}

Os formulários adaptáveis permitem que os autores de formulários criem uma experiência de captura de dados em várias etapas com grande facilidade. Eles possuem suporte integrado para criar vários painéis e associar cada painel a diferentes padrões de navegação. Os autores do formulário podem agrupar campos de formulário em seções lógicas e representar um grupo como um painel. A navegação geral entre painéis é controlada com o layout do painel. Os autores podem optar por organizar painéis em diferentes layouts, por exemplo, posicionando sequencialmente com o layout do assistente ou de maneira ad hoc por meio do layout com guias. Para obter informações sobre layouts de painel, consulte [Recursos de layout dos formulários adaptáveis](layout-capabilities-adaptive-forms.md).

Em uma experiência típica de preenchimento de formulário, há mais etapas envolvidas do que apenas capturar dados. Um envio de formulário completo pode incluir outras etapas, como a assinatura digital do formulário, a verificação das informações preenchidas no formulário, o processamento de pagamentos e assim por diante. Há diferenças de caso para caso.

Se o seu caso de uso determinar um conjunto de etapas para a captura de dados ou se houver regulamentos que precisam de determinadas etapas a serem seguidas, o [!DNL Experience Manager Forms] fornece uma maneira de aplicar essa estrutura comum em todos os formulários. A implementação premeditada da estrutura do formulário define a sequência de etapas de um formulário. ![Exemplo de uma sequência de formulário em várias etapas](assets/formpipeline.png)

Exemplo de uma sequência de formulário em várias etapas

Tomemos como exemplo um caso de uso em que você deve criar uma sequência de formulário com as seguintes etapas: preencher, verificar, assinar e confirmar. As etapas para criar essa sequência são as seguintes:

1. Definir um modelo de formulário e adicionar a ele o painel requerido. Deve haver um painel para cada etapa na sequência. No entanto, é possível incluir painéis secundários dentro de um painel.

   Nesse exemplo, podemos adicionar os seguintes painéis:

   * **[!UICONTROL Preenchimento]**: contém campos de formulários para capturar dados. Aqui, você pode incluir painéis secundários aninhados para criar seções para diferentes tipos de informações: pessoais, familiares, financeiras e assim por diante.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL Assinatura eletrônica]**: contém o componente **[!UICONTROL Assinar]** que pode ser usado em um formulário adaptável baseado em XFA. Ele fornece os seguintes serviços de assinatura:

      * Serviços de assinatura eletrônica da Adobe Document Cloud
      * Assinatura escrita
   * **[!UICONTROL Confirmação]**: contém o componente **[!UICONTROL Resumo]** que exibe uma mensagem confirmando o envio do formulário depois que um usuário o assina e atinge a etapa de Confirmação (Resumo) da sequência. Os autores podem configurar o texto do componente [!UICONTROL Resumo]: mostrar uma mensagem de agradecimento, mostrar um link para o PDF gerado e assim por diante.



1. Selecione o layout do painel raiz como **[!UICONTROL Assistente]**.
1. Conclua as etapas restantes para criar o modelo de formulário. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

Depois de definir a sequência de formulário no modelo de formulário, é possível usá-lo para criar formulários que terão a estrutura básica definida como a sequência em vigor, embora seja sempre possível personalizar o formulário para atender às suas necessidades.
