---
title: Integração nativa do AEM Assets com o Adobe Express
description: A integração nativa do AEM Assets com o Adobe Express permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Integração nativa com o Adobe Express {#native-integration-adobe-express}

O AEM Assets se integra nativamente ao Adobe Express, o que permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express. Você pode colocar o conteúdo gerenciado no AEM Assets na tela Express e depois salvar o conteúdo novo ou editado em um repositório do AEM Assets. A integração oferece os seguintes benefícios principais:

* Maior reutilização de conteúdo ao editar e salvar novos ativos no AEM.

* Redução do tempo e esforço gerais para criar novos ativos ou novas versões de ativos existentes.

## Pré-requisitos {#prerequisites}

Qualificações para acessar o Adobe Express e pelo menos um ambiente no AEM Assets. O ambiente pode ser qualquer um dos repositórios no Assets as a Cloud Service ou no Assets Essentials.


## Usar o AEM Assets no editor do Adobe Express {#use-aem-assets-in-express}

Execute as seguintes etapas para começar a usar o AEM Assets no editor do Adobe Express:

1. Abra o aplicativo web do Adobe Express.

2. Abra uma nova tela em branco carregando um novo modelo ou projeto ou criando um ativo.

3. Clique em **[!UICONTROL Assets]** disponível no painel de navegação esquerdo. O Adobe Express exibe a lista de repositórios que você está autorizado a acessar, juntamente com a lista de ativos e pastas disponíveis no nível raiz.

4. Navegue ou pesquise ativos no repositório para arrastar e soltar na tela. Você pode filtrar ativos usando vários filtros disponíveis, como tipo de arquivo, tipo MIME e dimensões.

   >[!NOTE]
   >
   >O filtro por dimensão não se aplica a vídeos.

   ![Incluir ativos do complemento Assets](assets/adobe-express-native-integration.png)


## Salvar projetos do Adobe Express no AEM Assets {#save-express-projects-in-assets}

Depois de incorporar as modificações apropriadas na tela Express, você pode salvá-la no repositório do AEM Assets.

1. Clique em **[!UICONTROL Compartilhar]** para abrir a caixa de diálogo **[!UICONTROL Compartilhar]**.

   ![Salvar ativos no AEM](assets/adobe-express-share.png)

2. Na seção Armazenamento do painel direito, selecione **AEM Assets**. O Adobe Express exibe a caixa de diálogo de upload.
3. Selecione **Página atual** ou **Todas as páginas**. Especifique um nome e um formato para o(s) ativo(s) a ser(em) exportado(s). É possível exportar o conteúdo da tela de desenho nos formatos PNG, JPEG, PDF, MP4, MP4+PNG ou MP4+JPEG. O formato é ajustado automaticamente com base no(s) ativo(s) na(s) página(s) da tela.
Selecionar **Página atual** salva o ativo da página atual na pasta de destino. Se você selecionar **Todas as páginas** e o formato de exportação não for PDF, todas as páginas da tela serão salvas como arquivos separados em uma nova pasta dentro da pasta de destino. Se o formato de exportação for PDF, todas as páginas da tela de desenho serão salvas como um único arquivo PDF na pasta de destino.

4. Clique no ícone de pasta em **Pasta de destino** para selecionar um local e salvar o(s) ativo(s).

   ![Salvar ativos no AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Opcional: Você pode adicionar metadados da campanha para o upload usando o campo **Nome do projeto ou da campanha**. Você pode usar um nome existente ou criar um novo. Você pode definir vários nomes de Projeto ou Campanha para o upload. Para registrar o nome, basta digitar o nome e pressionar Enter.
Como prática recomendada, a Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.

6. Da mesma forma, defina valores para os campos **[!UICONTROL Palavras-chave]** e **[!UICONTROL Canais]**.

7. Clique em **[!UICONTROL Carregar]** para carregar o(s) ativo(s) para o AEM Assets.

## Limitações {#limitations}

1. Para importar e exportar, o tipo de arquivo de vídeo compatível é MP4.

2. Para importação de vídeo MP4:

   1. O tamanho máximo de arquivo aceito é 200 MB. Se esse limite for excedido, uma mensagem de alerta será exibida.
   2. A resolução máxima suportada é de 3840 X 3840 pixels.
   3. Vídeos com planos de fundo transparentes (canal alfa) não são compatíveis.

3. Para exportação de vídeo MP4:

   1. O tamanho máximo de arquivo aceito é 200 MB. Se esse limite for excedido, um alerta sugere cortar o vídeo para 200 MB ou menos, ou carregá-lo manualmente na pasta de destino do AEM Assets após baixá-lo.



