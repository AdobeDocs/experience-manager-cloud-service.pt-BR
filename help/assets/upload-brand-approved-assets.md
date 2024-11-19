---
title: Carregar os ativos aprovados pela sua marca para  [!DNL Content Hub]
description: Saiba como fazer upload dos ativos aprovados pela sua marca para o Content Hub
role: User
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Fazer upload de ativos aprovados pela marca para o Centro de conteúdo. {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="Fazer upload de ativos aprovados pela marca para o Centro de conteúdo."
>abstract="Adicione ativos aprovados ao Centro de conteúdo a partir do sistema de arquivos local ou importe-os de fontes de dados do OneDrive ou do Dropbox. Todos os ativos são exibidos no nível superior do Centro de conteúdo, independentemente da estrutura de pastas, para aprimorar os recursos de pesquisa."

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

[Os usuários do Content Hub com direitos para adicionar ativos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) podem adicionar ativos ao Content Hub a partir do sistema de arquivos local ou importar ativos de fontes de dados do OneDrive ou do Dropbox. Todos os ativos são exibidos no nível superior do Content Hub, independentemente da estrutura de pastas disponível no sistema de arquivos local ou nas fontes de dados do OneDrive e do Dropbox para aprimorar os recursos de pesquisa.

Os ativos marcados como `Approved` no Assets as a Cloud Service ficam disponíveis automaticamente no Content Hub. Para obter mais informações, consulte [Aprovar ativos para o Content Hub](/help/assets/approve-assets-content-hub.md).

Para aprimorar ainda mais a pesquisa de ativos, o Content Hub permite:

* Defina os principais detalhes relevantes para o upload do seu ativo, como nome da campanha, palavras-chave, canais e assim por diante.

* Gere automaticamente mais propriedades para cada ativo após o upload bem-sucedido, como tamanho do arquivo, formato, resolução e algumas outras propriedades.

* Use a inteligência artificial fornecida pelo [Adobe Sensei](https://www.adobe.com/br/sensei.html) para aplicar automaticamente marcas relevantes a todos os ativos carregados. Essas tags, devidamente chamadas de Tags inteligentes, aumentam a velocidade do conteúdo de seus projetos, ajudando você a encontrar ativos relevantes rapidamente.

Carregue apenas os ativos aprovados pela sua marca [para a Content Hub](/help/assets/approve-assets.md).

![Carregar ativos aprovados pela marca](assets/upload-brand-approved-assets.png)

## Pré-requisitos {#prerequisites-add-assets}

[Usuários do Content Hub com direitos para adicionar ativos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) podem carregar ativos para o Content Hub.

## Adicionar ativos ao Content Hub a partir do sistema de arquivos local {#add-assets-local-file-system}

Para adicionar ativos ao Content Hub, execute as seguintes etapas:

1. Clique em **[!UICONTROL Adicionar Assets]** para exibir a caixa de diálogo **[!UICONTROL Adicionar ativos aprovados]** que permite criar um carregamento.

1. Na seção **[!UICONTROL Arraste arquivos ou pastas aqui]**, disponível no painel direito, você pode arrastar os ativos do sistema de arquivos local ou clicar em **[!UICONTROL Procurar]** para selecionar manualmente os arquivos ou pastas disponíveis no sistema de arquivos local. Essa lista de arquivos que fazem parte do upload está disponível como uma lista.


   Também é possível visualizar as imagens selecionadas usando as miniaturas e clicar no ícone X para remover qualquer imagem específica da lista. O ícone X é exibido somente quando você passa o mouse sobre o nome ou o tamanho da imagem. Você também pode clicar em **[!UICONTROL Remover tudo]** para excluir todos os itens da lista de carregamento.

   Para concluir o processo de carregamento e habilitar o **[!UICONTROL botão Carregar]**, agrupe seus ativos com um nome de Campanha.

   ![Carregar ativos para o Content Hub](assets/upload-assets-content-hub.png)

1. Defina o nome do upload usando o campo **[!UICONTROL Nome da campanha]**. Você pode usar um nome existente ou criar um novo. À medida que você digita o nome, a Content Hub fornece mais opções. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Como prática recomendada, o Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.

1. Da mesma forma, defina valores para os campos **[!UICONTROL Palavras-chave]**, **[!UICONTROL Canais]**, **[!UICONTROL Cronograma]** e **[!UICONTROL Região]**. Marcar e agrupar ativos por palavras-chave, canais e localização permite que todos que usam o conteúdo aprovado da empresa encontrem esses ativos e os mantenham organizados.

1. Clique em **[!UICONTROL Carregar]** para carregar ativos para a Content Hub. A caixa de confirmação [!UICONTROL Detalhes da revisão] é exibida. Clique em [!UICONTROL Continuar].

1. O Assets inicia o upload. Clique em [!UICONTROL Novo carregamento] para reiniciar o procedimento de carregamento. Clique em [!UICONTROL Concluído] para concluir o carregamento.

Os administradores também podem configurar os campos obrigatórios e opcionais exibidos durante o upload de ativos, como nome da campanha, palavras-chave, canais e assim por diante. Para obter mais informações, consulte [Configurar a interface do usuário do Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## Adicionar ativos ao Content Hub a partir de fontes de dados do OneDrive ou do Dropbox {#add-assets-onedrive-dropbox}

Para adicionar ativos ao Content Hub a partir de fontes de dados do OneDrive ou Dropbox:

1. Clique em **[!UICONTROL Adicionar Assets]** para exibir a caixa de diálogo **[!UICONTROL Adicionar ativos aprovados]**, que permite importar ativos do OneDrive ou do Dropbox.

1. Clique em **[!UICONTROL OneDrive]** ou **[!UICONTROL Dropbox]** para iniciar o processo de importação. O Content Hub solicita que você faça logon em sua conta do OneDrive ou do Dropbox e, em seguida, exibe sua estrutura de pastas do OneDrive ou do Dropbox no painel esquerdo.

1. Clique no ícone + adjacente ao arquivo ou ao nome da pasta para exibir o item na lista de Itens selecionados. Depois de selecionar todos os arquivos que precisam ser adicionados ao portal do Content Hub, repita as etapas de 3 a 6 de [Adicionar ativos ao Content Hub a partir do sistema de arquivos local](#add-assets-local-file-system) para concluir o processo de carregamento.

   ![Carregar ativos para o Content Hub a partir do OneDrive ou Dropbox](assets/add-assets-onedrive-dropbox.png)

Os administradores também podem configurar os campos obrigatórios e opcionais exibidos durante o upload de ativos, como nome da campanha, palavras-chave, canais e assim por diante. Para obter mais informações, consulte [Configurar a interface do usuário do Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

## Gerenciar ativos carregados usando o Content Hub {#manage-assets-uploaded-using-content-hub}

[Os usuários do Content Hub com direitos para adicionar ativos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) podem [adicionar ativos ao Content Hub](/help/assets/upload-brand-approved-assets.md) a partir do sistema de arquivos local ou importar ativos de fontes de dados do OneDrive ou do Dropbox. Todos os ativos são exibidos no nível superior do Content Hub, independentemente da estrutura de pastas disponível no sistema de arquivos local ou nas fontes de dados do OneDrive e do Dropbox para aprimorar os recursos de pesquisa.

A exibição de ativos carregados usando o Content Hub depende de se você [habilitou a opção de Aprovação automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Se a opção **[!UICONTROL Aprovação automática]** estiver habilitada, os ativos carregados usando o Content Hub estarão automaticamente disponíveis.

* Se a opção **[!UICONTROL Aprovação automática]** estiver desabilitada, os ativos carregados usando o Content Hub não serão exibidos automaticamente. Os ativos estão disponíveis na pasta `hydrated-assets` do seu ambiente as a Cloud Service do Assets. Navegue até a pasta e [edite em massa](#bulk-approve-assets-content-hub) o status desses ativos para `Approved` para que eles sejam exibidos no Content Hub.

![processo de aprovação do Content Hub](/help/assets/assets/content-hub-approval.png)
