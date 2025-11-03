---
title: Aprimorar a descoberta de conteúdo com metadados gerados por IA
description: Saiba como aprimorar a descoberta de conteúdo com metadados gerados por IA
source-git-commit: e5b4d7692c9c57ba3e9c76940f28d72ad14d9fc0
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Aprimorar a descoberta de conteúdo com metadados gerados por IA {#ai-smart-tags}

Em vez de depender da entrada manual, a IA atribui tags descritivas automaticamente a ativos digitais. Essas tags geradas por IA melhoram a qualidade dos metadados, tornando os ativos mais fáceis de pesquisar, categorizar e recomendar. Essa abordagem não só aumenta a eficiência eliminando a marcação manual, mas também garante a consistência e a escalabilidade em grandes volumes de conteúdo digital. Por exemplo, se o ativo for uma imagem, a IA pode identificar objetos, cenas, emoções ou até mesmo logotipos de marca nele e gerar tags relevantes, como &quot;pôr do sol&quot;, &quot;praia&quot;, &quot;férias&quot; ou &quot;sorrir&quot;. O conteúdo gerado por IA pode aprimorar a pesquisa de ativos aproveitando técnicas de pesquisa semântica e léxica. Veja mais [Pesquisar Assets](search-assets-view.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![Metadados gerados pela IA](/help/assets/assets/enhanced-smart-tags.png)

## Como ativar metadados gerados por IA? {#enable-ai-generated-metadata}

Para ativar os metadados gerados por IA:

* A versão mínima necessária do AEM é `20626`.

* Você deve assinar um contrato GenAI Rider. Para obter mais informações, entre em contato com o representante da Adobe.

## Uso de metadados gerados por IA {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Para usar o recurso aprimorado de tags inteligentes, execute as seguintes etapas:

1. Na interface [!DNL Experience Manager], vá para a pasta desejada e clique em **[!UICONTROL Adicionar Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> Os formatos de arquivo de imagem compatíveis são `png`, `jpg`, `jpeg`,`psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` e `bmp`.

1. Espere até que o ativo recém-carregado seja processado. Depois de concluído, acesse os detalhes do ativo.

1. Vá para a guia **[!UICONTROL Gerado por IA]**. Se a versão [!DNL Experience Manager] for incompatível ou não for atualizada, essa guia não estará visível.  Os seguintes campos estão lá:

   * **[!UICONTROL Título gerado]:** o título fornece um título claro e conciso que captura a ideia principal de um ativo carregado, facilitando sua compreensão rápida. Ao adicionar um ativo, se você fornecer um título (em `dc:title`), ele será exibido na exibição de navegação dos ativos. Se deixado em branco, um título gerado pela IA será atribuído automaticamente.
   * **[!UICONTROL Descrição gerada]:** A descrição fornece um resumo breve, mas informativo, sobre o que o ativo trata, ajudando os usuários e o módulo de pesquisa a compreender rapidamente sua relevância.
   * **[!UICONTROL Palavras-chave geradas]:** são termos direcionados que representam os principais temas de um ativo, auxiliando na marcação e filtragem de conteúdo.

1. [Opcional] Você pode adicionar outras marcas ou criar as suas próprias se achar que estão faltando marcas relevantes. Para fazer isso, escreva suas marcas no campo **[!UICONTROL Palavras-chave geradas]** e clique em **[!UICONTROL Salvar]**.

Para obter informações sobre como desabilitar metadados gerados por IA, consulte [Desabilitar metadados gerados por IA](/help/assets/smart-tags.md#disable-ai-generated-metadata).
