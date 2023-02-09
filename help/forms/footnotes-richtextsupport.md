---
title: Suporte a notas de rodapé
description: Suporte RTE para notas de rodapé.
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente Nota de Rodapé {#footnotecomponent}

**[!UICONTROL Nota]** é o bit extra de informações ou observações que aparecem no final da página. [!UICONTROL Nota] O inclui as notas indicadas no texto com números em sobrescrito.

As notas de rodapé são numeradas sequencialmente na ordem em que são exibidas na página. Cada nota de rodapé tem um número exclusivo como um sobrescrito que corresponde ao número que é colocado na parte inferior da página. Ao lado do número, as informações suplementares são apresentadas como uma descrição de nota de rodapé.

![Descrição da Nota de Rodapé](/help/forms/assets/footnote_description.png)


## Utilização da nota de rodapé {#usesoffootnotes}

* Ajuda a fornecer citações.
* Fornece informações adicionais que podem interromper o fluxo normal das informações principais.
* Fornece informações entre parênteses ou permissões de direitos autorais.

No Adaptive Forms, [!UICONTROL nota] é usada para exibir as informações sobre como preencher ou usar o formulário. Para obter informações sobre como criar um Forms adaptável, consulte [Criação de um formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota de rodapé no Adaptive Forms {#using-footnote-adaptiveforms}

Para adicionar nota de rodapé no Adaptive Forms, execute as seguintes etapas:
1. Abra um formulário adaptável em **Editar** modo.
1. No navegador de componentes, arraste e solte a **[!UICONTROL Texto]** no formulário adaptável.
1. Selecione o **[!UICONTROL Texto]** componente adicionado e toque em ![cmppr](assets/configure-icon.svg) para editar suas propriedades.

   ![Nota de rodapé no Adaptive Forms](/help/forms/assets/footnote_rte.png)

1. Selecione o texto para o qual deseja adicionar uma descrição de nota de rodapé e clique em  ![star](/help/forms/assets/asterisk.svg) para criar o estilo do botão **[!UICONTROL Nota]** componente.

1. Clique em ![check](/help/forms/assets/save_icon.svg) para salvar as alterações e os estilos.

   >[!NOTE]
   >
   >* As notas de rodapé são numeradas automaticamente e aparecem de uma maneira que são criadas no Formulário adaptável.
   >* Se houver notas de rodapé duplicadas, a numeração será a mesma para todas as notas de rodapé duplicadas.


1. No navegador de componentes, arraste e solte a **[!UICONTROL Espaço Reservado para Nota de Rodapé]** no formulário adaptável.
   >[!NOTE]
   >
   >* Na instância de publicação, as notas de rodapé são exibidas na posição em que **[!UICONTROL Espaço Reservado para Nota de Rodapé]** é colocado no formulário adaptável.
   >* Ao navegar entre diferentes painéis, somente as notas de rodapé visíveis aparecem no **[!UICONTROL Espaço Reservado para Nota de Rodapé]** que estão presentes no painel navegado.


1. Salve as propriedades.

No tempo de execução, o número aparece no texto como um sobrescrito e sua descrição correspondente aparece no **[!UICONTROL Nota]** componente na posição em que [!UICONTROL Espaço Reservado para Nota de Rodapé] é colocado no formulário adaptável. Você pode navegar diretamente para a descrição da nota de rodapé clicando no número correspondente na [!UICONTROL Nota].