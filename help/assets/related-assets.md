---
title: Ativos relacionados
description: Saiba como relacionar ativos que compartilham determinados atributos comuns. Você também pode usar o recurso para criar relações de origem/derivadas entre ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Ativos relacionados {#related-assets}

Os ativos Adobe Experience Manager (AEM) permitem relacionar manualmente os ativos com base nas necessidades de sua organização usando o recurso Ativos relacionados. Por exemplo, você pode relacionar um arquivo de licença com um ativo ou uma imagem/vídeo em um tópico semelhante. Você pode relacionar ativos que compartilham determinados atributos comuns. Você também pode usar o recurso para criar relações de origem/derivadas entre ativos. Por exemplo, se você tiver um arquivo PDF gerado a partir de um arquivo INDD, poderá relacionar o arquivo PDF ao arquivo INDD de origem.

Dessa forma, você tem a flexibilidade de compartilhar um arquivo de baixa resolução (por exemplo, PDF/JPG) para fornecedores/agências e disponibilizar o arquivo de alta resolução (por exemplo, INDD) somente mediante solicitação.

## Relate assets {#relating-assets}

1. Na interface Ativos, abra a página de propriedades de um ativo que você deseja relacionar. Como alternativa, selecione o ativo na exibição de lista. Você também pode selecionar o ativo de uma coleção.
1. Para relacionar outro ativo com o ativo selecionado, clique/toque no ícone **[!UICONTROL Relacionar]** na barra de ferramentas.
1. Faça uma das seguintes opções:

   * Para relacionar o arquivo de origem do ativo, selecione **[!UICONTROL Origem]** na lista.
   * Para relacionar um arquivo derivado, selecione **[!UICONTROL Derivado]** na lista.
   * Para criar uma relação bidirecional entre os ativos, selecione **[!UICONTROL Outros]** na lista.

1. Na tela **[!UICONTROL Selecionar ativo]** , navegue até o local do ativo que deseja relacionar e selecione-o.

1. Clique/toque no ícone **[!UICONTROL Confirmar]** .
1. Clique/toque em **[!UICONTROL OK]** para fechar a caixa de diálogo. Dependendo da sua escolha de relacionamento na etapa 3, o ativo relacionado é listado sob uma categoria apropriada na seção **[!UICONTROL Relacionado]** . Por exemplo, se o ativo relacionado for o arquivo de origem do ativo atual, ele será listado em **[!UICONTROL Origem]**.
1. Para desrelacionar um ativo, clique/toque no ícone **[!UICONTROL Desrelacionar]** na barra de ferramentas.
1. Selecione o(s) ativo(s) que deseja desrelacionar na caixa de diálogo **[!UICONTROL Remover relações]** e clique/toque em **[!UICONTROL Desrelacionar]**.
1. Clique/toque em **[!UICONTROL OK]** para fechar a caixa de diálogo. Os ativos para os quais você removeu relações são excluídos da lista de ativos relacionados na seção **[!UICONTROL Relacionados]** .

## Traduzir ativos relacionados {#translating-related-assets}

Criar relacionamentos de origem/derivados entre ativos usando o recurso Ativos relacionados também é útil em fluxos de trabalho de tradução. Quando você executa um fluxo de trabalho de conversão em um ativo derivado, o AEM Assets obtém automaticamente qualquer ativo que o arquivo de origem referencia e o inclui para conversão. Dessa forma, o ativo referenciado pelo ativo de origem é convertido junto com os ativos de origem e derivados. Por exemplo, considere um cenário em que sua cópia em inglês inclua um ativo derivado e seu arquivo de origem, como mostrado.

Se o arquivo de origem estiver relacionado a outro ativo, o AEM Assets busca o ativo referenciado e o inclui para conversão.

1. Traduza os ativos na pasta de origem para um idioma de destino seguindo as etapas em [Criar um novo projeto](/help/assets/translate-assets.md#create-a-new-translation-project)de tradução. Por exemplo, neste caso, traduza seus ativos para francês.
1. Na página Projetos, abra a pasta de tradução.
1. Clique/toque no bloco do projeto para abrir a página de detalhes.
1. Clique/toque nas elipses abaixo do cartão de trabalho de tradução para exibir o status da tradução.
1. Selecione o ativo e clique/toque em **[!UICONTROL Revelar nos ativos]** na barra de ferramentas para exibir o status de conversão do ativo.
1. Para verificar se os ativos relacionados à origem foram convertidos, clique/toque no ativo de origem.
1. Selecione o ativo relacionado à origem e clique/toque em **[!UICONTROL Revelar nos Ativos]**. O ativo relacionado convertido é exibido.
