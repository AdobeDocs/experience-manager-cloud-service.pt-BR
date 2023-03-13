---
title: Texto do espaço reservado em [!DNL AEM Forms]
description: O texto para espaço reservado tem como objetivo ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um exemplo de valor ou uma breve descrição do formato esperado.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Texto do espaço reservado em [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

O texto de espaço reservado representa uma palavra ou frase curta. Tem como objetivo auxiliar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um exemplo de valor ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor e é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto do espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

[!DNL AEM Forms] suporte a texto de espaço reservado para campos de caixa Senha, Seletor de data, caixa Numérica e caixa de texto.\
Os textos de marcadores de posição não são suportados para o widget de data nativo do HTML5. Para especificar um texto de Espaço Reservado:

1. Clique com o botão direito do mouse em um componente que suporte Texto para espaço reservado e clique **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra o **Título e texto** guia.
1. Especifique uma palavra ou uma frase curta na variável **Caixa de texto Espaço reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto do espaço reservado não é suportado no [!DNL Microsoft Internet Explorer 9].

