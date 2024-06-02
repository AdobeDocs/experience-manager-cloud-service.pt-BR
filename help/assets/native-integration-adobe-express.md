---
title: Integração nativa do AEM Assets com o Adobe Express
description: A integração nativa do AEM Assets com o Adobe Express permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 69d890eaae30468db89b9aff975a2a421f53fcff
workflow-type: tm+mt
source-wordcount: '597'
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

2. Abra uma nova tela em branco carregando um novo modelo ou projeto ou criando um ativo.

3. Clique em **[!UICONTROL Assets]** disponível no painel de navegação esquerdo. Adobe Express exibe a lista de repositórios que você está autorizado a acessar, juntamente com a lista de ativos e pastas disponíveis no nível raiz.

4. Navegue ou pesquise ativos no repositório para arrastar e soltar na tela. Você pode filtrar ativos usando vários filtros disponíveis, como tipo de arquivo, tipo MIME e dimensões.

   >[!NOTE]
   >
   >O filtro por dimensão não se aplica a vídeos.

   ![Incluir ativos do complemento Assets](assets/adobe-express-native-integration.png)


## Salvar projetos do Adobe Express no AEM Assets {#save-express-projects-in-assets}

Depois de incorporar as modificações apropriadas na tela Express, você pode salvá-la no repositório do AEM Assets.

1. Clique em **[!UICONTROL Compartilhar]** para abrir o **[!UICONTROL Compartilhar]** diálogo.

   ![Salvar ativos no AEM](assets/adobe-express-share.png)

2. Na seção Armazenamento do painel direito, selecione, **AEM Assets**. Adobe Express exibe a caixa de diálogo de upload.
3. Especifique um nome e um formato para o ativo. Você pode salvar o conteúdo da tela nos formatos PNG, JPEG, PDF, MP4, MP4+PNG ou MP4+JPEG. O formato se ajusta automaticamente com base no(s) ativo(s).

   >[!NOTE]
   >
   >Selecionar &quot;Página atual&quot; salva o arquivo na pasta de destino. Selecionar &quot;Todas as páginas&quot; cria uma nova pasta no seu destino para todos os arquivos que não são de PDF e os salva lá, enquanto os arquivos de PDF são salvos como um único arquivo na pasta de destino.

4. Clique na área de texto em **Pasta de destino** para selecionar um local e salvar o(s) ativo(s).

   ![Salvar ativos no AEM](/help/assets/assets/page-selection-and-destination-folder.png)

5. Opcional: é possível adicionar metadados de campanha para upload usando o **Nome do projeto ou da campanha** campo. Você pode usar um nome existente ou criar um novo. Você pode definir vários nomes de Projeto ou Campanha para o upload. Para registrar o nome, basta digitar o nome e pressionar Enter.
Como prática recomendada, o Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.

6. Da mesma forma, defina valores para a variável **[!UICONTROL Palavras-chave]** e **[!UICONTROL Canais]** campos.

7. Clique em **[!UICONTROL Carregar]** para fazer upload do ativo para o AEM Assets.




## Limitações {#limitations}

1. Para importar e exportar, o tipo de arquivo de vídeo compatível é MP4.

2. Para importação de vídeo MP4:

   a) O tamanho máximo de arquivo aceito é de 200 MB. Se esse limite for excedido, uma mensagem de alerta será exibida.
b) A resolução máxima suportada é de 3840 X 3840 pixels.
c) Vídeos com planos de fundo transparentes (canal alfa) não são compatíveis.

3. Para exportação de vídeo MP4:

   a) O tamanho máximo de arquivo aceito é de 200 MB. Se esse limite for excedido, uma mensagem de alerta será exibida com uma sugestão alternativa, como mostrado na imagem abaixo
   ![alerta com solução alternativa](/help/assets/assets/alert-with-workaround.png).
