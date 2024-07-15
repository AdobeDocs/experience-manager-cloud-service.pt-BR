---
title: Como adicionar texto de espaço reservado a campos de formulário?
description: O texto para espaço reservado tem como objetivo ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um exemplo de valor ou uma breve descrição do formato esperado.
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Texto do espaço reservado em [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

O texto de espaço reservado representa uma palavra ou frase curta. Tem como objetivo auxiliar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um exemplo de valor ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor e é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto do espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

O [!DNL AEM Forms] oferece suporte ao texto de espaço reservado para campos de caixa de senha, seletor de datas, caixa numérica e caixa de texto.\
Os textos de marcadores de posição não são suportados para o widget de data nativo do HTML5. Para especificar um texto de Espaço Reservado:

1. Clique com o botão direito do mouse em um componente que ofereça suporte ao Texto do Espaço Reservado e clique em **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra a guia **Título e texto**.
1. Especifique uma palavra ou uma frase curta na **caixa de texto Espaço Reservado**. Clique em **OK**.

>[!NOTE]
>
>Não há suporte para texto de espaço reservado em [!DNL Microsoft Internet Explorer 9].

