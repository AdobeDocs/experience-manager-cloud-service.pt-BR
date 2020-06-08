---
title: Fazer check-in e check-out de arquivos em ativos
description: Saiba como fazer check-out dos ativos para edição e check-in deles novamente após a conclusão das alterações.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 4%

---


# Arquivos de check-in e check-out em Ativos {#check-in-and-check-out-files-in-assets}

Os ativos Adobe Experience Manager (AEM) permitem que você faça check-out dos ativos para edição e check-in deles novamente após concluir as alterações. Depois de fazer check-out de um ativo, somente você pode editar, anotar, publicar, mover ou excluir o ativo. Fazer check-out de um ativo bloqueia o ativo. Outros usuários não podem executar nenhuma dessas operações no ativo até que você faça check-in do ativo novamente nos ativos AEM. No entanto, eles ainda podem alterar os metadados do ativo bloqueado.

Para poder fazer check-out/check-in de ativos, você precisa ter acesso de gravação neles.

Esse recurso ajuda a impedir que outros usuários substituam as alterações feitas por um autor, onde vários usuários colaboram na edição de workflows entre equipes.

## Fazendo check-out de ativos {#checking-out-assets}

1. Na interface do usuário Ativos, selecione o ativo que deseja fazer check-out. Você também pode selecionar vários ativos para fazer check-out.

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. Na barra de ferramentas, clique/toque no ícone **[!UICONTROL Checkout]** .

   ![chlimage_1-469](assets/chlimage_1-469.png)

   Observe que o ícone **[!UICONTROL Check-out]** alterna para o ícone **[!UICONTROL Checkout]** com o cadeado aberto.

   ![chlimage_1-470](assets/chlimage_1-470.png)

   Para verificar se outros usuários podem editar o ativo que você fez check-out, faça logon como um usuário diferente. Um ícone de cadeado é exibido na miniatura do ativo que você deu baixa.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Selecione o ativo. Observe que a barra de ferramentas não exibe nenhuma opção que permita editar, anotar, publicar ou excluir o ativo.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   No entanto, você pode clicar/tocar no ícone Propriedades **[!UICONTROL da]** Visualização para editar os metadados do ativo bloqueado.

1. Clique/toque no ícone Editar para abrir o ativo no modo de edição.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite o ativo e salve as alterações. Por exemplo, recorte a imagem e salve-a.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Você também pode optar por anotar ou publicar o ativo.

1. Selecione o ativo editado na interface do usuário do Assets e clique/toque no ícone **[!UICONTROL Check-in]**, da barra de ferramentas.

   ![chlimage_1-475](assets/chlimage_1-475.png)

   O ativo modificado é feito check-in nos ativos AEM e está disponível para outros usuários para edição.

## Entrada forçada {#forced-check-in}

Os administradores podem fazer check-in de ativos cujo check-out foi feito por outros usuários.

1. Faça logon nos ativos AEM como administrador.
1. Na interface do usuário do Assets, selecione um ou mais ativos cujo check-out foi feito por outros usuários.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Na barra de ferramentas, clique/toque no ícone **[!UICONTROL Liberar bloqueio]** . O ativo é devolvido e está disponível para edição para outros usuários.

   ![chlimage_1-477](assets/chlimage_1-477.png)