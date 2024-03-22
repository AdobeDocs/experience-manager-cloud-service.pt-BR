---
title: Integração nativa do AEM Assets com o Adobe Express
description: A integração nativa do AEM Assets com o Adobe Express permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 8bbf9a2ba8f708a5a03d11bc0388d39b32d4c7b3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Integração nativa com o Adobe Express {#native-integration-adobe-express}

A AEM Assets integra-se nativamente com o Adobe Express, o que permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express. Você pode colocar o conteúdo gerenciado no AEM Assets na tela Express e depois salvar o conteúdo novo ou editado em um repositório do AEM Assets. A integração oferece os seguintes benefícios principais:

* Maior reutilização de conteúdo ao editar e salvar novos ativos no AEM.

* Redução do tempo e esforço gerais para criar novos ativos ou novas versões de ativos existentes.

## Pré-requisitos {#prerequisites}

Qualificações para acessar o Adobe Express e pelo menos um ambiente no AEM Assets. O ambiente pode ser qualquer um dos repositórios no Assets as a Cloud Service ou Assets Essentials.


## Usar AEM Assets no editor de Adobe Express {#use-aem-assets-in-express}

Execute as seguintes etapas para começar a usar o AEM Assets no editor de Adobe Express:

1. Abra o aplicativo web Adobe Express.

1. Abra uma nova tela em branco carregando um novo modelo ou projeto ou criando um ativo.

1. Clique em **[!UICONTROL Assets]** disponível no painel de navegação esquerdo. Adobe Express exibe a lista de repositórios que você está autorizado a acessar, juntamente com a lista de ativos e pastas disponíveis no nível raiz.

1. Navegue ou pesquise ativos no repositório para arrastar e soltar na tela. Você pode filtrar ativos usando vários filtros disponíveis, como tipo de arquivo, tipo MIME e dimensões.

   ![Incluir ativos do complemento Assets](assets/adobe-express-native-integration.png)


## Salvar projetos do Adobe Express no AEM Assets {#save-express-projects-in-assets}

Depois de incorporar as modificações apropriadas na tela Express, você pode salvá-la no repositório do AEM Assets.

1. Clique em **[!UICONTROL Compartilhar]** para abrir o **[!UICONTROL Compartilhar]** diálogo.

   ![Salvar ativos no AEM](assets/adobe-express-share.png)

1. Selecionar **[!UICONTROL AEM Assets]** do **[!UICONTROL Armazenamento]** seção disponível no painel direito. Adobe Express exibe a caixa de diálogo de upload.
1. Especifique um nome e um formato para o ativo. Você pode salvar o conteúdo da tela de desenho nos tipos de formato PNG ou JPEG.

1. Clique no ícone de pasta adjacente ao **[!UICONTROL Localização]** navegue até o local onde precisa salvar o ativo e clique em **[!UICONTROL Selecionar]**. O nome da pasta é exibido no campo **[!UICONTROL Localização]** campo.

   ![Salvar ativos no AEM](assets/adobe-express-upload.png)

1. Opcional: é possível adicionar metadados de campanha para upload usando o **[!UICONTROL Nome do projeto ou da campanha]** campo. Você pode usar um nome existente ou criar um novo. Você pode definir vários nomes de Projeto ou Campanha para o upload. Enquanto estiver digitando um nome, clique em qualquer outro lugar na caixa de diálogo ou pressione a tecla `,` (Vírgula) para registrar o nome.

   Como prática recomendada, o Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.
1. Da mesma forma, defina valores para a variável **[!UICONTROL Palavras-chave]** e **[!UICONTROL Canais]** campos.

1. Clique em **[!UICONTROL Carregar]** para fazer upload do ativo para o AEM Assets.




## Limitações {#limitations}

Há um erro conhecido enfrentado por alguns usuários com acesso a mais de um repositório do Assets ao salvar um documento com ativos de vários repositórios.
