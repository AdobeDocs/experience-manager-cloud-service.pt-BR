---
title: 'Edição de um programa de sandbox '
description: 'Edição de um programa de sandbox '
translation-type: tm+mt
source-git-commit: 78bc94f7e3dab37b7f83f480ef5438165e1897bc
workflow-type: tm+mt
source-wordcount: '221'
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

1. Navegue até a página **Editar Programa**.

1. A página **Editar programa** exibe duas guias (Geral e Soluções) para os programas Produção e Sandbox.
   ![](assets/edit-program.png)

   >[!NOTE]
   >Embora os Sites e os Ativos sejam exibidos, um deles pode ser desativado com base no que foi comprado e não usado. Especificamente, se a organização não tiver direitos não utilizados para uma solução específica, essa solução será exibida, mas desabilitada.

## Considerações ao editar um programa {#considerations-editing}

Algumas considerações devem ser revisadas durante a edição de um programa:

* Pelo menos uma solução deve ser selecionada para um Programa, ou seja, o uso não terá permissão para desmarcar todas as soluções durante o fluxo de trabalho Editar programa.

* Clicar no botão **Save**, se as soluções selecionadas forem alteradas, as atualizações de solução para ambientes entrarão em vigor após a próxima implantação.