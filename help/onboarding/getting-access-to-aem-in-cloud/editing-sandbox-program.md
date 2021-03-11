---
title: 'Edição de um programa de sandbox '
description: 'Edição de um programa de sandbox '
translation-type: tm+mt
source-git-commit: 751f611ecccc39ef4650a1c7a9941655a6b2aedd
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Editar um programa de sandbox {#create-sandbox-program}

Os usuários com a permissão necessária agora podem editar um programa de Produção, permitindo que façam o seguinte de maneira automatizada:

* Adicionar a solução Sites a um programa existente com Ativos (ou vice-versa).
* Remova Sites (ou Ativos) de um programa existente com Sites e Ativos.
* Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

   >[!NOTE]
   >Um usuário na função Proprietário comercial deve estar conectado para editar o programa com êxito.

Siga as etapas abaixo para editar um programa de sandbox:

1. Navegue até a página **Editar programa** na página *Visão geral* do Cloud Manager.

1. A página **Editar programa** exibe duas guias (Geral e Soluções) para os programas Produção e Sandbox.
   ![](assets/edit-program.png)


## Considerações ao editar um programa {#considerations-editing}

Algumas considerações devem ser revisadas durante a edição de um programa:

* Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o uso não terá permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

* Clicar no botão **Save**, se as soluções selecionadas forem alteradas, as atualizações de solução para ambientes entrarão em vigor após a próxima implantação.