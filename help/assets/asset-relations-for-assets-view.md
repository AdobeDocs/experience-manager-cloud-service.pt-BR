---
title: Relações do ativo
description: Saiba como relacionar ativos digitais que compartilham alguns atributos comuns. Além disso, crie relacionamentos derivados da origem entre ativos digitais usando relações de ativos.
role: User
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 77dab2731f8d442bf999bf1614ef060944794574
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 9%

---

# Relações do ativo {#related-assets}

O [!DNL Adobe Experience Manager Assets] permite relacionar ativos manualmente com base nas necessidades da sua organização usando o recurso de ativos relacionados. Por exemplo, você pode relacionar um arquivo de licença a um ativo ou uma imagem/vídeo em um tópico semelhante. Você pode relacionar ativos que compartilham determinados atributos comuns. Você também pode usar o recurso para criar relacionamentos de origem/derivados entre ativos. Por exemplo, se você tiver um arquivo PDF gerado a partir de um arquivo INDD, poderá relacionar o arquivo PDF ao seu arquivo INDD de origem.

Usando esse recurso, você tem a flexibilidade de compartilhar um arquivo PDF ou JPG de baixa resolução com fornecedores ou agências e disponibilizar o arquivo INDD de alta resolução somente mediante solicitação.

>[!NOTE]
>
>Somente os usuários com permissões de edição em ativos podem relacionar e não relacionar os ativos.

## Etapas para relacionar ativos {#steps-to-relate-assets}

1. Na interface [!DNL Experience Manager], abra a página **[!UICONTROL Propriedades]** de um ativo que você deseja relacionar.

   ![abra a página Propriedades de um ativo para relacionar o ativo](assets/asset-properties-relate-assets.png)

1. Para relacionar outro ativo ao ativo selecionado, clique em **[!UICONTROL Relações do ativo]** ![relacionar ativos](assets/do-not-localize/link-relate.png).
1. Siga uma das seguintes opções:

   * Para relacionar o arquivo de origem do ativo, selecione **[!UICONTROL Adicionar Source]** na lista. Você pode associar somente um ativo como uma origem.
   * Para relacionar um arquivo derivado, selecione **[!UICONTROL Adicionar derivado]** na lista. Você pode associar vários ativos nesta categoria.
   * Para criar uma relação bidirecional entre os ativos, selecione **[!UICONTROL Adicionar outro]** na lista. Você pode associar vários ativos nesta categoria.

1. Na tela **[!UICONTROL Selecionar Assets]**, navegue até o local do ativo que deseja relacionar e selecione-o. Você pode selecionar um único ativo por vez ou vários ativos mantendo a tecla Shift pressionada ao clicar, o que pode incluir qualquer um dos [formatos de arquivo compatíveis no Modo de Exibição do Assets](/help/assets/supported-file-formats-assets-view.md).

   ![adicionar ativo relacionado](assets/add-related-asset.png)

1. Clique em **[!UICONTROL Selecionar]**. Dependendo da sua escolha de relação na etapa 3, o ativo relacionado é listado em uma categoria apropriada na seção **[!UICONTROL Relações do ativo]**. Por exemplo, se o ativo relacionado for o arquivo de origem do ativo atual, ele será listado em **[!UICONTROL Source]**.

   ![Exemplo de relação do Assets](assets/asset-relations-example.png)

1. Clique em **[!UICONTROL Desrelacionar]** ![desrelacionar ativos](assets/do-not-localize/link-unrelate-icon.png) disponíveis para todos os ativos relacionados em cada seção ([!UICONTROL Source], [!UICONTROL Derivados] e [!UICONTROL Outros]) para desrelacionar um ativo.

## Traduzir ativos relacionados {#translating-related-assets}

Criar relacionamentos de origem/derivados entre ativos usando o recurso de ativos relacionados também é útil em fluxos de trabalho de tradução. Quando você executa um fluxo de trabalho de tradução em um ativo derivado, o [!DNL Experience Manager Assets] busca automaticamente qualquer ativo ao qual o arquivo de origem faça referência e o inclui para tradução. Dessa forma, o ativo referenciado pelo ativo de origem é traduzido junto com os ativos de origem e derivados. Se o arquivo de origem estiver relacionado a outro ativo, [!DNL Experience Manager Assets] buscará o ativo referenciado e o incluirá para tradução.

Consulte [Traduzir ativos no AEM](/help/assets/translate-assets.md).

## Próximas etapas {#next-steps}

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Exibir versões de um ativo](/help/assets/manage-organize-assets-view.md#view-versions)
>* [Traduzir ativos no AEM](/help/assets/translate-assets.md)
>* [Formatos de Arquivo com Suporte na Exibição do Assets](/help/assets/supported-file-formats-assets-view.md).
