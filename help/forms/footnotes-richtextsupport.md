---
title: Suporte a notas de rodapé
description: Suporte RTE para notas de rodapé.
source-git-commit: 3d713304512065819ed16bbc9604f2cf9d1cf43f
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente de nota de rodapé {#footnotecomponent}

**[!UICONTROL Nota de rodapé]** é o bit extra de informações ou notas que aparecem no final da página. [!UICONTROL Nota de rodapé] O compreende as notas indicadas no texto com números em sobrescrito.

As notas de rodapé são numeradas sequencialmente na ordem em que aparecem na página. Cada nota de rodapé tem um número exclusivo como sobrescrito, que corresponde ao número inserido na parte inferior da página. Ao lado do número, é exibida a informação complementar como uma descrição de nota de rodapé.

![Descrição da nota de rodapé](/help/forms/assets/footnote_description.png)


## Uso da Nota de Rodapé {#usesoffootnotes}

* Ajuda a fornecer citações.
* Fornece informações adicionais que podem interromper o fluxo normal das informações principais.
* Fornece informações entre parênteses ou permissões de copyright.

No Forms Adaptável, [!UICONTROL nota de rodapé] é usado para exibir as informações sobre como preencher ou usar o formulário. Para obter informações sobre como criar uma Forms adaptável, consulte [Criação de um formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota de rodapé no Adaptive Forms {#using-footnote-adaptiveforms}

Para adicionar uma nota de rodapé no Adaptive Forms, execute as seguintes etapas:
1. Abra um formulário adaptável no **Editar** modo.
1. No navegador de componentes, arraste e solte a **[!UICONTROL Texto]** no Formulário adaptável.
1. Selecione o **[!UICONTROL Texto]** componente adicionado e toque em ![cmppr](assets/configure-icon.svg) para editar suas propriedades.

   ![Nota de rodapé no Adaptive Forms](/help/forms/assets/footnote_rte.png)

1. Selecione o texto ao qual deseja adicionar uma descrição de nota de rodapé e clique em  ![estrela](/help/forms/assets/asterisk.svg) botão para estilizar o **[!UICONTROL Nota de rodapé]** componente.

1. Clique em ![check](/help/forms/assets/save_icon.svg) para salvar as alterações e os estilos.

   >[!NOTE]
   >
   >* As notas de rodapé são numeradas automaticamente e aparecem da maneira que são criadas no Formulário adaptável.
   >* Se houver notas de rodapé duplicadas, a numeração será a mesma para todas as notas de rodapé duplicadas.


1. No navegador de componentes, arraste e solte a **[!UICONTROL Espaço reservado para nota de rodapé]** no Formulário adaptável.
   >[!NOTE]
   >
   >* Na instância de publicação, as notas de rodapé são exibidas na posição em que **[!UICONTROL Espaço reservado para nota de rodapé]** componente é colocado no Formulário adaptável.
   >* Ao navegar entre painéis diferentes, somente as notas de rodapé visíveis aparecerão no **[!UICONTROL Espaço reservado para nota de rodapé]** presentes no painel navegado.


1. Salve as propriedades.

No tempo de execução, o número aparece no texto como um sobrescrito e sua descrição correspondente aparece no **[!UICONTROL Nota de rodapé]** componente na posição em que [!UICONTROL Espaço reservado para nota de rodapé] é colocado no Formulário adaptável. Você pode navegar diretamente para a descrição da nota de rodapé clicando no número correspondente na [!UICONTROL Nota de rodapé].