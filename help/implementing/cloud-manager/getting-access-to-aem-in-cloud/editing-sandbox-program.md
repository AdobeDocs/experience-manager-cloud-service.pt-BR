---
title: 'Edição de um programa de sandbox '
description: Edição de um programa de sandbox
exl-id: e4545f7e-5329-40ad-81bb-a383c68f5d66
source-git-commit: e7f8e7daa88c5bf8bb13c2a635fb84724f8bd7bb
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Edição de um programa de sandbox {#create-sandbox-program}

Os usuários com a permissão necessária agora podem editar um programa de Produção, permitindo que façam o seguinte de maneira automatizada:

* Adicionar a solução Sites a um programa existente com Ativos (ou vice-versa).
* Remova Sites (ou Ativos) de um programa existente com Sites e Ativos.
* Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

   >[!NOTE]
   >Um usuário na função Proprietário comercial deve estar conectado para editar o programa com êxito.

Siga as etapas abaixo para editar um programa de sandbox:

1. Clique na opção **Editar programa** na página *Visão geral* do Cloud Manager

   ![](assets/edit-program-overview.png)

1. A página **Editar Programa** exibe duas guias **Geral** e **Soluções e Suplementos**.

   Navegue até a guia **General** para editar a descrição do programa.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-sandboxa.png)

   A guia **Soluções e complementos** exibe duas opções, como **Sites** e **Ativos** para programas de Produção e Sandbox. Além disso, você pode selecionar a opção complementar **Commerce**, que está disponível em **Sites**, conforme mostrado na figura abaixo.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o usuário não tem permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

1. Clique em **Atualizar** para concluir o fluxo de trabalho de edição do programa.


## Considerações ao editar um programa {#considerations-editing}

Algumas considerações devem ser revisadas durante a edição de um programa:

* Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o usuário não tem permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

* Clicar no botão **Save**, se as soluções selecionadas forem alteradas, as atualizações de solução para ambientes entrarão em vigor após a próxima implantação.
