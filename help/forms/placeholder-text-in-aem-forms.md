---
title: Texto de espaço reservado em [!DNL AEM Forms]
description: O texto de espaço reservado destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um valor de amostra ou uma breve descrição do formato esperado.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Texto de espaço reservado em [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

O texto do espaço reservado representa uma palavra ou frase curta. Destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um valor de amostra ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor, ele é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto de espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

[!DNL AEM Forms] suporte ao texto de espaço reservado para os campos Caixa de senha, Seletor de data, Caixa numérica e caixa de texto.\
Os textos de espaço reservado não são suportados para o widget de data HTML5 nativo. Para especificar um texto de Espaço reservado:

1. Clique com o botão direito do mouse em um componente compatível com o Texto de espaço reservado e clique em **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra o **Título e texto** guia .
1. Especifique uma palavra ou uma frase curta no **Caixa de texto Espaço reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto de espaço reservado não é suportado em [!DNL Microsoft Internet Explorer 9].

