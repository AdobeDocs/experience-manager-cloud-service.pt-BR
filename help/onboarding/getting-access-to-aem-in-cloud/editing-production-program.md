---
title: 'Editando um programa de produção '
description: Editando um programa de produção
exl-id: 745c10af-f0a0-49e9-bb79-3fd058fad16c
translation-type: tm+mt
source-git-commit: 9de1b85f8909709c08cb7358414c18c813aac684
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Editar um programa de produção {#create-production-program}

Os usuários com as permissões necessárias agora podem editar um programa de Produção, permitindo que façam o seguinte de maneira automatizada:

* Adicionar a solução Sites a um programa existente com Ativos (ou vice-versa).
* Remova Sites (ou Ativos) de um programa existente com Sites e Ativos.
* Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

   >[!NOTE]
   >Um usuário na função Proprietário comercial deve estar conectado para editar o programa com êxito.

Siga as etapas abaixo para editar um programa de Produção:

1. Clique na opção **Editar programa** na página *Visão geral* do Cloud Manager

   ![](assets/edit-program-overview.png)

1. A página **Editar Programa** exibe duas guias **Geral** e **Soluções e Suplementos**.

   Navegue até a guia **General** para editar a descrição do programa.

   ![](assets/edit-program-general.png)

   A guia **Soluções e complementos** exibe duas opções, como **Sites** e **Ativos** para programas de Produção e Sandbox. Além disso, você pode selecionar a opção complementar **Commerce**, que está disponível em **Sites**, conforme mostrado na figura abaixo.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o usuário não tem permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

1. Clique em **Save** para concluir o fluxo de trabalho do programa de edição.


## Considerações ao editar um programa {#considerations-editing}

Algumas considerações devem ser revisadas durante a edição de um programa:

* Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o usuário não tem permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

* Clicar no botão **Save**, se as soluções selecionadas forem alteradas, as atualizações de solução para ambientes entrarão em vigor após a próxima implantação.
