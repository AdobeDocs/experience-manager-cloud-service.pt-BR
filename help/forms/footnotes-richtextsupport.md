---
title: Como adicionar uma nota de rodapé a um formulário adaptável?
description: Use o editor de rich text (RTE) para notas de rodapé em um formulário adaptável.
feature: Adaptive Forms, Foundation Components
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Componente de nota de rodapé {#footnotecomponent}

>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

**[!UICONTROL Nota de Rodapé]** é o bit extra de informações ou anotações que aparecem no final da página. A [!UICONTROL Nota de Rodapé] compreende as notas indicadas no texto com números em sobrescrito.

As notas de rodapé são numeradas sequencialmente na ordem em que aparecem na página. Cada nota de rodapé tem um número exclusivo como sobrescrito, que corresponde ao número inserido na parte inferior da página. Ao lado do número, é exibida a informação complementar como uma descrição de nota de rodapé.

![Descrição da Nota de Rodapé](/help/forms/assets/footnote_description.png)


## Uso da Nota de Rodapé {#usesoffootnotes}

* Ajuda a fornecer citações.
* Fornece informações adicionais que podem interromper o fluxo normal das informações principais.
* Fornece informações entre parênteses ou permissões de copyright.

No Adaptive Forms, a [!UICONTROL nota de rodapé] é usada para exibir as informações sobre como preencher ou usar o formulário. Para obter informações sobre como criar um Forms adaptável, consulte [Criando um Formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota de rodapé no Adaptive Forms {#using-footnote-adaptiveforms}

Para adicionar uma nota de rodapé no Adaptive Forms, execute as seguintes etapas:

1. Abra um Formulário adaptável no modo **Editar**.
1. No navegador de componentes, arraste e solte o componente **[!UICONTROL Texto]** no Formulário adaptável.
1. Selecione o componente **[!UICONTROL Texto]** que você adicionou e selecione ![cmppr](assets/configure-icon.svg) para editar suas propriedades.

   ![Nota de Rodapé no Forms Adaptável](/help/forms/assets/footnote_rte.png)

1. Selecione o texto ao qual deseja adicionar uma descrição de nota de rodapé e clique no botão ![estrela](/help/forms/assets/asterisk.svg) para estilizar o componente **[!UICONTROL Nota de Rodapé]**.

1. Clique em ![verificar](/help/forms/assets/save_icon.svg) para salvar as alterações e os estilos.

   >[!NOTE]
   >
   >* As notas de rodapé são numeradas automaticamente e aparecem da maneira que são criadas no Formulário adaptável.
   >* Se houver notas de rodapé duplicadas, a numeração será a mesma para todas as notas de rodapé duplicadas.

1. No navegador de componentes, arraste e solte o componente **[!UICONTROL Espaço Reservado para Nota de Rodapé]** no Formulário Adaptável.

   >[!NOTE]
   >
   >* Na instância de publicação, as notas de rodapé são exibidas na posição em que o componente **[!UICONTROL Espaço Reservado para Nota de Rodapé]** é colocado no Formulário adaptável.
   >* Quando você navega entre painéis diferentes, somente as notas de rodapé visíveis aparecem no **[!UICONTROL Espaço Reservado para Nota de Rodapé]** que está presente no painel navegado.

1. Salve as propriedades.

No tempo de execução, number aparece no texto como sobrescrito e sua descrição correspondente aparece no componente **[!UICONTROL Nota de Rodapé]** na posição onde o [!UICONTROL Espaço Reservado para Nota de Rodapé] é colocado no Formulário Adaptável. Você pode navegar diretamente para a descrição da nota de rodapé clicando no número correspondente na [!UICONTROL Nota de Rodapé].


## Consulte também {#see-also}

{{see-also}}