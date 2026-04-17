---
title: Usar o Supervisor de conteúdo para acessar conteúdo do AEM nos aplicativos Adobe
description: O Content Advisor oferece uma experiência unificada de detecção de conteúdo em todos os aplicativos da Adobe e traz detecção inteligente e sensível ao contexto diretamente para a experiência de criação.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Aplicável ao AEM Assets)."
feature: Collaboration
role: User
exl-id: fa737a57-d346-4e6d-a9cd-99bcb6b344fe
source-git-commit: 2ae4533890cbf01183df8b5283109fff0b9eae60
workflow-type: tm+mt
source-wordcount: '1945'
ht-degree: 0%

---

# Usar o Supervisor de conteúdo para acessar conteúdo do AEM em aplicativos Adobe{#content-advisor-aem-assets-adobe-applications}

O Content Advisor oferece uma experiência unificada de detecção de conteúdo em todos os aplicativos Adobe. Integrado nativamente a aplicativos como Adobe Workfront, AJO B2C (em breve), AEM Sites e outros, o Content Advisor reúne o conteúdo (ativos e fragmentos de conteúdo) em uma única interface inteligente. Ele permite que você descubra, navegue e reutilize facilmente o conteúdo mais relevante, diretamente do seu fluxo de trabalho, para que possa se mover mais rápido sem quebrar o contexto.

>[!IMPORTANT]
> 
> O preenchimento de Fragmento de conteúdo não está disponível no momento e será compatível em breve com os aplicativos apropriados do Adobe.

O Content Advisor traz detecção inteligente e sensível ao contexto diretamente para a experiência de criação, ajudando você a encontrar rapidamente conteúdo relevante e aprovado com base em sua intenção. Com recursos como sugestões inteligentes, representações do Dynamic Media e metadados de ativos detalhados, ele permite avaliar e reutilizar o conteúdo com eficiência sem sair da interface do aplicativo, acelerando a criação de conteúdo e mantendo a consistência da marca.

![Imagem de banner do Supervisor de Conteúdo](assets/content-advisor-banner-image-updated.png)

O Adobe Experience Manager (AEM) Assets também se integra nativamente ao Adobe Express, permitindo que você descubra, acesse e use ativos do AEM Assets diretamente na interface do Express usando o Supervisor de conteúdo. Para obter mais informações, consulte [Usar o Supervisor de Conteúdo para acessar o AEM Assets no Adobe Express](/help/assets/native-integration-adobe-express.md).


## Pré-requisitos {#prerequisites}

* Acesso a um ambiente do AEM Assets as a Cloud Service.

* Acesso a um ambiente do AEM Sites com fragmentos de conteúdo criados (necessário somente para trabalhar com fragmentos de conteúdo). Isso não é necessário para acessar ativos binários ou o AEM Assets.

## Detecção inteligente de ativos com o Content Advisor {#intelligent-asset-discovery-content-advisor}

O Supervisor de conteúdo ajuda a detectar conteúdo relevante usando recomendações inteligentes com reconhecimento de contexto baseadas no conteúdo ou no resumo da campanha do aplicativo Adobe do host. Ela também permite selecionar representações do Dynamic Media prontas para canal otimizadas para o seu caso de uso.

>[!IMPORTANT]
> 
>Certifique-se de selecionar um repositório **autor** na lista suspensa **Repositório**. Um repositório de **entrega** não exibe recursos do Supervisor de Conteúdo.
>
> Além disso, o repositório **delivery** não tem conteúdo organizado em pastas e coleções. O conteúdo é exibido no nível raiz em uma estrutura simples.

O Supervisor de Conteúdo fornece os seguintes recursos principais:

* [Pesquisa com IA para detecção mais inteligente de ativos](#content-advisor-ai-search)

* [Sugestões inteligentes com base no contexto e na intenção](#smart-suggestions-content-advisor)

* [Resumos de campanha para descobrir ativos relevantes](#campaign-briefs-content-advisor)

* [Representações de ativos do Dynamic Media disponíveis para uso](#dynamic-media-renditions-content-advisor)

* [Integração perfeita com fragmentos de conteúdo](#content-fragments-integration-content-advisor)

* [Acessar metadados de ativos consistentes com a visualização do Assets](#asset-metadata-content-advisor)

* [Filtros de acesso consistentes com a visualização do Assets](#filters-content-advisor)

* [Acessar e reutilizar pesquisas recentes e salvas](#saved-searches-content-advisor)

* [Pesquisar ativos entre e dentro de coleções](#search-collections-content-advisor)

### Pesquisa com IA para detecção mais inteligente de ativos {#content-advisor-ai-search}

O Supervisor de conteúdo usa um recurso de pesquisa avançada que entende o significado e a intenção por trás da consulta de um usuário, em vez de depender de correspondências exatas de palavras-chave. Ele usa a Inteligência artificial (IA) e o aprendizado de máquina para fornecer resultados mais precisos e com reconhecimento de contexto.

Ao contrário da pesquisa tradicional baseada em palavras-chave, que procura termos exatos, o Pesquisa com IA interpreta as relações entre palavras, conceitos e intenção do usuário. Isso garante que os usuários encontrem o que procuram, mesmo que a consulta seja redigida de forma diferente, contenha erros de digitação ou esteja em outro idioma.

![Pesquisa com IA para ativos no Supervisor de Conteúdo](assets/content-advisor-ai-search.png)

Alguns, se seus principais benefícios incluírem:

* Suporte multilíngue: pesquise em vários idiomas sem exigir traduções exatas. Os usuários podem encontrar conteúdo relevante independentemente do idioma de consulta.

* Lida com erros ortográficos: interpreta erros de digitação e de ortografia, garantindo resultados precisos mesmo com informações imperfeitas.

* Entende sinônimos: fornece resultados para termos e frases relacionados, de modo que os usuários não precisam adivinhar a palavra-chave correta.

* Pesquisa sensível ao contexto: reconhece a intenção por trás de uma consulta, não apenas as palavras exatas.

>[!IMPORTANT]
> 
>* A versão mínima necessária do AEM para acessar Pesquisas com IA no Supervisor de Conteúdo é `21994`
>* Em breve, haverá suporte para Pesquisa com IA nos Fragmentos de conteúdo.


### Sugestões inteligentes com base no contexto e na intenção {#smart-suggestions-content-advisor}

O Supervisor de Conteúdo exibe sugestões inteligentes com base no contexto do aplicativo Adobe do host. Isso ajuda você a descobrir e usar rapidamente os ativos que se alinham às suas necessidades de conteúdo sem a demorada pesquisa manual.

![Conteúdo sugerido do Supervisor de Conteúdo](assets/content-advisor-smart-suggestions.png)

>[!IMPORTANT]
> 
>* Você deve assinar um GenAI Rider para acessar esse recurso no Supervisor de conteúdo. Para assinar o GenAI Rider, entre em contato com seu representante da Adobe.
>* A versão mínima necessária do AEM para acessar este recurso é `21994`.
>* O Supervisor de Conteúdo exibe sugestões inteligentes com base no contexto e na intenção do conteúdo disponível no aplicativo Adobe do host. Ele não exibe resultados com base em imagens. Consulte [Suporte ao recurso do Supervisor de Conteúdo em aplicativos do Adobe](#content-advisor-feature-support-adobe-applications) para obter a lista de aplicativos do Adobe com suporte para esse recurso.


### Resumos de campanha para descobrir ativos relevantes {#campaign-briefs-content-advisor}

O Supervisor de conteúdo permite fazer upload de um documento de resumo da campanha para descobrir ativos relevantes sem inserir manualmente palavras-chave de pesquisa. O Supervisor de Conteúdo analisa as informações no resumo da campanha para entender a intenção da campanha e recomenda ativos relevantes disponíveis no AEM Assets.

![Incluir ativos do complemento Assets](assets/content-advisor-upload-briefs.png)

>[!IMPORTANT]
>
>* O Supervisor de conteúdo analisa as informações disponíveis como texto no resumo da campanha para recomendar ativos relevantes. Não analisa as informações disponíveis como imagens no resumo da campanha.
>* Os tipos de arquivos compatíveis que você pode fazer upload como resumo da campanha incluem documentos PDF, DOCX e TXT.
>* Você deve assinar um GenAI Rider para acessar esse recurso no Supervisor de conteúdo. Para assinar o GenAI Rider, entre em contato com seu representante da Adobe.
>* A versão mínima necessária do AEM para acessar este recurso é `21994`.
>* Upload do resumo da campanha em breve oferecerá suporte aos fragmentos de conteúdo.

### Representações de ativos do Dynamic Media disponíveis para uso {#dynamic-media-renditions-content-advisor}

As representações do Dynamic Media fornecem versões otimizadas de canal de ativos prontas para uso, incluindo [predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md), [Recortes inteligentes](/help/assets/dynamic-media/image-profiles.md), tipos de formato e perfis de cores. Essas representações ajudam a garantir que o ativo selecionado atenda aos requisitos de canal e design sem exigir edição manual ou duplicação de ativos.

Você também pode aplicar modificadores do Dynamic Media para visualizar ajustes em tempo real antes de selecionar a representação do aplicativo do Adobe host, permitindo uma seleção mais rápida da representação mais apropriada e, ao mesmo tempo, mantendo a consistência e a qualidade do ativo.

Clique no ícone ![Informações](assets/info-icon.svg) no cartão de ativos e selecione a guia **[!UICONTROL Dynamic Media]** para exibir as representações disponíveis para um ativo. Você pode optar por exibir representações do [Dynamic Media Scene7](/help/assets/dynamic-media/dynamic-media.md) ou do [Dynamic Media com OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). Ao selecionar **[!UICONTROL OpenAPI]** para um ativo, as representações disponíveis serão exibidas somente se o ativo for aprovado e estiver disponível para Dynamic Media com OpenAPI.

Você deve ter uma licença válida do AEM Dynamic Media para exibir a guia Dynamic Media.

![Exibir representações do Dynamic Media](assets/content-advisor-dm-renditions.png)

Clique no ícone de ![visualização](assets/do-not-localize/preview-icon.svg) para visualizar a representação ou clique no nome da representação e clique em **[!UICONTROL Selecionar]** para disponibilizar a representação no aplicativo host.

![Visualizar representações do Dynamic Media](assets/content-advisor-dm-preview.png)

Clique em **[!UICONTROL Adicionar modificadores]**, especifique um modificador na caixa de texto e pressione Enter para aplicar a transformação a todas as representações de ativos em tempo real. Da mesma forma, é possível adicionar vários modificadores às representações e pré-visualizar essas transformações. Clique no nome da representação e clique em **[!UICONTROL Selecionar]** para torná-la disponível em seu aplicativo host. A representação após a aplicação desses modificadores não é salva. Consulte a lista de modificadores com suporte para [Dynamic Media Scene7](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference) e [Dynamic Media com OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat).

### Descoberta de fragmentos de conteúdo {#content-fragments-discovery-content-advisor}

O Supervisor de conteúdo oferece detecção de fragmentos de conteúdo, permitindo que você navegue e incorpore fragmentos facilmente em aplicativos Adobe compatíveis. Pesquise em uma lista de fragmentos de conteúdo e selecione o conteúdo mais relevante sem sair do fluxo de trabalho atual.

Cada fragmento de conteúdo é representado como um cartão com uma visualização em miniatura ao vivo gerada a partir do conteúdo, ajudando você a identificar rapidamente o fragmento correto. O cartão também exibe os principais detalhes, como o título e o status (Rascunho, Modificado ou Publicado). Para obter insights mais profundos, clique no ícone ![Informações](assets/info-icon.svg) para exibir propriedades detalhadas, referências a outros fragmentos de conteúdo e variações disponíveis, garantindo uma seleção de conteúdo informada e a reutilização.

![Fragmentos de conteúdo no Supervisor de conteúdo](assets/content-advisor-content-fragments.png)

>[!IMPORTANT]
> 
>* Pesquisas com IA, Sugestões inteligentes, Fazer upload de resumos de campanha e Visualizar recursos ainda não são compatíveis com os Fragmentos de conteúdo no Supervisor de conteúdo.

### Acessar metadados de ativos consistentes com a visualização do Assets {#asset-metadata-content-advisor}

O Supervisor de conteúdo fornece acesso às propriedades de ativos definidas no AEM Assets, incluindo metadados disponíveis na visualização do Assets. O Supervisor de Conteúdo usa a mesma configuração de metadados que no Assets View, replicando a lista de guias de metadados e conteúdo na página exibir detalhes do ativo do Assets. Isso permite revisar os principais detalhes do ativo, como título, descrição, formato, tamanho e outros metadados, antes de selecionar um ativo. O acesso às propriedades do ativo ajuda a garantir que você escolha o ativo correto e aprovado para o seu conteúdo.

![Metadados de exibição do Assets no Supervisor de Conteúdo](assets/content-advisor-metadata.png)

Clique no ícone ![Informações](assets/info-icon.svg) no cartão de ativos e selecione a guia **[!UICONTROL Básico]** para exibir os metadados do ativo. Também é possível exibir outras guias de metadados de ativos, como Produto, Campanha e Tags, consistentes com os metadados de ativos existentes na exibição do Assets.

O Supervisor de Conteúdo exibe propriedades (metadados) para arquivos em uma visualização somente leitura. As propriedades não são exibidas para coleções e pastas.

### Filtros de acesso consistentes com a visualização do Assets {#filters-content-advisor}

O Supervisor de conteúdo oferece os mesmos recursos de filtragem do aplicativo Adobe host que estão disponíveis na visualização do Assets, permitindo que você refine ativos usando filtros predefinidos. Os mesmos recursos de filtragem disponíveis na visualização Assets também se aplicam aos filtros específicos aos tipos de conteúdo, como arquivos, pastas e coleções. Isso garante uma experiência consistente de detecção de ativos e ajuda a localizar com eficiência ativos relevantes no aplicativo Adobe do host.

Se você não tiver filtros configurados na visualização do Assets por meio do esquema de filtro, o Supervisor de Conteúdo exibirá filtros prontos para uso, incluindo Tipo de arquivo, Formato de arquivo, Status do ativo, Tamanho do arquivo, Largura da imagem, Altura da imagem, Data de modificação e Data de criação.

O esquema de filtro personalizado é compatível com o Assets (arquivos), mas ainda não é compatível com Pastas e Coleções.

### Acessar e reutilizar pesquisas recentes e salvas {#saved-searches-content-advisor}

Pesquisas salvas criadas na visualização do Assets também estão disponíveis, permitindo que você reutilize critérios de pesquisa predefinidos. Pesquisas salvas funcionam de forma consistente entre a visualização do Assets e o Supervisor de conteúdo nos navegadores. Isso ajuda a localizar ativos com eficiência usando padrões de pesquisa consistentes no AEM Assets e em outros aplicativos da Adobe.

Para salvar a pesquisa usada com frequência usando o Supervisor de Conteúdo:

1. Especifique um termo de pesquisa (opcional), clique no ícone de filtros e selecione as opções com base nos seus requisitos para criar uma consulta de pesquisa.

1. Clique em **Gerenciar pesquisas salvas** > **Criar nova Pesquisa Salva**.

1. Especifique o nome da pesquisa e clique em ![ícone de informações](assets/do-not-localize/checkmark-icon.svg) para salvá-la. A pesquisa é exibida na lista de itens.

   ![Consultor de Conteúdo de Pesquisas Salvas](assets/content-advisor-saved-searches.png)

Para aplicar qualquer um dos itens de pesquisa salvos, selecione o item de pesquisa na lista suspensa **[!UICONTROL Pesquisas salvas]**. O Supervisor de Conteúdo exibe os resultados com base na consulta de pesquisa.

O Supervisor de conteúdo salva as pesquisas recentes e permite salvar as pesquisas usadas com frequência para acesso rápido posteriormente. A lista de pesquisas recentes não é consistente entre a visualização do Assets e o Supervisor de conteúdo. O mesmo usuário pode ter um conjunto diferente de pesquisas recentes na visualização do Assets e no Supervisor de conteúdo. Se você estiver usando o modo Incógnito para acessar o Supervisor de Conteúdo, a lista de pesquisas recentes não estará disponível. Além disso, as pesquisas recentes não são compartilhadas em navegadores diferentes para o mesmo usuário e são específicas do ambiente do AEM.



O recurso Pesquisa salva padrão, disponível na visualização Assets, ainda não está disponível no Supervisor de conteúdo.

### Pesquisar ativos entre e dentro de coleções {#search-collections-content-advisor}

O Supervisor de conteúdo permite pesquisar ativos ou coleções em todas as coleções ou limitar a pesquisa a uma coleção específica. Isso ajuda a localizar e usar ativos de coleções com curadoria rapidamente, preservando o contexto organizacional pretendido.

## Suporte a recursos do Supervisor de conteúdo em aplicativos Adobe {#content-advisor-feature-support-adobe-applications}

A tabela a seguir ilustra o suporte ao recurso Supervisor de Conteúdo nos aplicativos Adobe.

>[!IMPORTANT]
> 
> À medida que o Supervisor de conteúdo se expande para aplicativos Adobe adicionais, esta tabela será atualizada para refletir o suporte mais recente.

| Aplicativo | Suporte para upload breve para pesquisa no Assets | Suporte para o painel de conteúdo sugerido durante a pesquisa no Assets | Suporte para o painel Dynamic Media durante a pesquisa no Assets | Suporte para pesquisar fragmentos de conteúdo |
|--------------------------------------|----------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------|------------------------------------------|
| [AEM Sites - Criação de Documentos](https://www.aem.live/docs/authoring-guide#document-authoring) | ✓ | ✓ | ✓ | − |
| [AEM Sites - Editor universal](https://www.aem.live/docs/authoring-guide#universal-editor-in-aem-sites) | ✓ | ✓ | ✓ | − |
| AEM Sites - [GoogleDrive](https://www.aem.live/docs/authoring-guide#google-drive)/[Criação no Sharepoint](https://www.aem.live/docs/authoring-guide#microsoft-sharepoint) | ✓ | − | ✓ | − |
| AEM Sites (Editor de fragmento de conteúdo) | ✓ | ✓ | ✓ | − |
| Fluxo de trabalho do Adobe Workfront | ✓ | ✓ | − | ✓ |
| Planejamento do Adobe Workfront | ✓ | ✓ | − | ✓ |
