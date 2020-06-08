---
title: Crie e gerencie ativos digitais em vários idiomas e execute workflows de tradução
description: Learn how to automate workflows for translating assets, including binaries, metadata, and tags into multiple languages.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '2615'
ht-degree: 23%

---


# Ativos multilíngues {#multilingual-assets}

Multilingual assets means assets with binaries, metadata, and tags in multiple languages. Generally, binaries, metadata, and tags for assets exist in one language, which are then translated to other languages for use in multilingual projects. Adobe Experience Manager (AEM) Assets lets you automate translation workflows on assets (including binaries, metadata, and tags) to generate assets in other languages for use in multilingual projects.

To automate translation workflows, you integrate translation service providers with AEM and create projects for translating assets into multiple languages. AEM supports human and machine translation workflows.

Human translation: The translated assets are returned and imported into AEM. When your translation provider is integrated with AEM, assets are automatically sent between AEM and the translation provider.

Machine translation: The machine translation service immediately translates the metadata and tags for assets.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only 1 master article.

https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/translation-projects.html
https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://docs.adobe.com/content/help/en/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting AEM with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparar ativos para tradução {#prepare-assets-for-translation}

Multilingual assets means assets with binaries, metadata, and tags in multiple languages. Generally, binaries, metadata, and tags for assets exist in one language, which are then translated to other languages for use in multilingual projects.

In Adobe Experience Manager (AEM) Assets, multilingual assets are included in folders, where each folder contains the assets in a different language.

Cada pasta de idioma é chamada de cópia de idioma. The root folder of a language copy, known as the language root, identifies the language of the content in the language copy. For example, `/content/dam/it` is the Italian language root for the Italian language copy. Language copies must use a [correctly-configured language root](#create-a-language-root) so that the correct language is targeted when translations of source assets are performed.

The language copy for which you originally add assets is the language master. O mestre de idioma é a fonte que é traduzida para outros idiomas. Uma hierarquia de pastas de amostra inclui várias raízes de idioma:

```shell
/content
&nbsp; &nbsp; /- dam
&nbsp; &nbsp; &nbsp; |- en
&nbsp; &nbsp; &nbsp; |- fr
&nbsp; &nbsp; &nbsp; |- de
&nbsp; &nbsp; &nbsp; |- es
&nbsp; &nbsp; &nbsp; |- it
&nbsp; &nbsp; &nbsp; |- ja
&nbsp; &nbsp; &nbsp; |- zh
```

Execute as seguintes etapas para preparar seus ativos para tradução:

1. Crie a raiz do idioma do seu mestre de idiomas. Por exemplo, a raiz do idioma da cópia em inglês na hierarquia da pasta de amostra é */content/dam/en*. Verifique se a raiz do idioma está configurada corretamente de acordo com as informações em [Criar uma raiz](#create-a-language-root)de idioma.

1. Adicione ativos ao seu mestre de idiomas.
1. Crie a raiz do idioma de cada idioma do público alvo para o qual você precisa de uma cópia do idioma.

### Criar uma raiz de idioma {#create-a-language-root}

Para criar a raiz do idioma, crie uma pasta e use um código de idioma ISO como o valor da propriedade Name. Depois de criar a raiz do idioma, é possível criar uma cópia do idioma em qualquer nível na raiz do idioma.

Por exemplo, a página raiz da cópia em idioma italiano da hierarquia de amostra tem `it` a propriedade Name. A propriedade Name é usada como o nome do nó do ativo no repositório e, portanto, determina o caminho dos ativos. (*&lt;servidor>:&lt;porta>/assets.html/content/dam/it/*)

1. No console Assets, clique/toque em **[!UICONTROL Criar]** e escolha **[!UICONTROL Pasta]** no menu.
1. No campo Nome, digite o código do país no formato de `<language-code>`.
1. Clique ou toque em **[!UICONTROL Criar]**. A raiz do idioma é criada no console Ativos.

### raízes da língua Visualização {#view-language-roots}

A interface otimizada para toque fornece um painel Referências que mostra uma lista de raízes de idioma que foram criadas nos ativos AEM.

1. No console Ativos, selecione o idioma mestre para o qual deseja criar cópias de idioma.
1. Clique ou toque no ícone GlobalNav e escolha **[!UICONTROL Referências]** para abrir o painel Referência.
1. No painel Referências, clique ou toque em Cópias **[!UICONTROL de idioma]**. O painel Cópias de idioma mostra as cópias de idioma dos ativos.

### Criar um novo projeto de tradução {#create-a-new-translation-project}

Se você usar essa opção, os ativos a serem traduzidos serão copiados para a raiz do idioma para o qual você deseja traduzir. Dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou executado automaticamente assim que o projeto de tradução for criado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma cópia de Idioma.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]**, em **[!UICONTROL Cópias]**.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista **[!UICONTROL Idiomas de destino]**, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]** , selecione **[!UICONTROL Criar um novo projeto]** de tradução.
1. No campo **[!UICONTROL Título do projeto]**, informe um título para o projeto.
1. Click/tap on **[!UICONTROL Create]**. Os ativos da pasta de origem são copiados para as pastas de públicos alvos para as localidades selecionadas na etapa 4.
1. Para navegar até a pasta, selecione a cópia de idioma e clique em **[!UICONTROL Revelar em Ativos]**.
1. Navegue até o console Projetos. A pasta de tradução é copiada para o console Projetos.
1. Abra a pasta para visualização do projeto de tradução.
1. Clique/toque no projeto para abrir a página de detalhes.
1. Para visualização do status do trabalho de tradução, clique nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Na interface do usuário Ativos, abra a página Propriedades de cada um dos ativos traduzidos para visualização dos metadados traduzidos.

>[!NOTE]
>
>Este recurso está disponível para ativos e pastas. Quando um ativo é selecionado em vez de uma pasta, toda a hierarquia de pastas até a raiz do idioma é copiada para criar uma cópia do idioma para o ativo.

### Add to an existing translation project {#add-to-existing-translation-project}

Se você usar essa opção, o fluxo de trabalho de tradução será executado para os ativos adicionados à pasta de origem após executar um fluxo de trabalho de tradução anterior. Somente os ativos recém-adicionados são copiados para a pasta do público alvo que contém ativos convertidos anteriormente. Nenhum novo projeto de tradução é criado neste caso.

1. Na interface do usuário Ativos, navegue até a pasta de origem que contém ativos não convertidos.
1. Selecione um ativo que deseja traduzir e abra o **[!UICONTROL painel Referência]**. A seção **[!UICONTROL Cópias de idioma]** exibe o número de cópias de tradução atualmente disponíveis.
1. Clique/toque em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]**. Uma lista de cópias de tradução disponíveis é exibida.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista **[!UICONTROL Idiomas de destino]**, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]**, selecione **[!UICONTROL Adicionar ao projeto de tradução existente]** para executar o fluxo de trabalho de tradução na pasta.
   >[!NOTE]
   >
   >Se você escolher a opção **[!UICONTROL Adicionar ao projeto]** de tradução existente, seu projeto de tradução será adicionado a um projeto pré-existente somente se as configurações do projeto corresponderem exatamente às configurações do projeto pré-existente. Caso contrário, um novo projeto será criado.
1. Na lista do projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.
1. Clique/toque em **[!UICONTROL Criar]**. Os ativos que serão traduzidos são adicionados à pasta de destino. A pasta atualizada está listada na seção **[!UICONTROL Cópias de idioma]**.
1. Navegue até o console Projetos e abra o projeto de tradução existente ao qual você adicionou.
1. Clique/toque na visualização do projeto de tradução na página de detalhes do projeto.
1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

   >[!NOTE]
   >
   >* Se você excluir a entrada para tags ou metadados, nenhuma tag ou metadados será traduzida para qualquer um dos ativos.
   >* Se você usar Tradução automática, os binários de ativos não serão traduzidos.
   >* Se o ativo adicionado ao trabalho de tradução incluir subativos, selecione os subativos e remova-os para que a tradução continue sem falhas.


1. Para start da tradução dos ativos, clique/toque na seta no bloco Trabalho **[!UICONTROL de]** tradução e selecione **[!UICONTROL Start]** na lista. Uma mensagem notifica o início do trabalho de tradução.
1. Para visualização do status do trabalho de tradução, clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Após a conclusão da tradução, o status é alterado para Pronto para Revisão. Navegue até a interface do usuário Ativos e abra a página Propriedades de cada um dos ativos traduzidos para visualização dos metadados traduzidos.

### Atualizar cópias de idioma {#update-language-copies}

Execute esse fluxo de trabalho para traduzir qualquer conjunto adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta do público alvo que já contém os ativos convertidos anteriormente. Dependendo da escolha das opções, um projeto de tradução é criado ou um projeto de tradução existente é atualizado para os novos ativos. O fluxo de trabalho de cópias de idioma de atualização inclui as seguintes opções:

* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project-1}

Se você usar essa opção, o conjunto de ativos será adicionado a um projeto de tradução existente para atualizar a cópia de idioma para a localidade escolhida.

1. Na interface do usuário Ativos, selecione a pasta de origem na qual você adicionou uma pasta de ativos.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Cópias de idioma]**, que seleciona todas as cópias de idioma. Desmarque as outras cópias, exceto a cópia de idioma (cópias) correspondente às localidades para as quais você deseja traduzir.
1. Clique/toque em **[!UICONTROL Atualizar cópias]** de idioma na parte inferior.
1. Na lista **[!UICONTROL Projeto]** , escolha **[!UICONTROL Adicionar ao projeto]** de tradução existente.
1. Na lista do projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.
1. Clique/toque em **[!UICONTROL Iniciar]**.
1. Consulte as etapas 9 a 14 de [Adicionar ao projeto](#add-to-existing-translation-project) de tradução existente para concluir o restante do procedimento.

### Criar cópias de idioma temporárias {#creating-temporary-language-copies}

Quando você executa um fluxo de trabalho de tradução para atualizar uma cópia de idioma com versões editadas dos ativos originais, a cópia de idioma existente é preservada até que você aprove os ativos convertidos. O AEM Assets armazena os ativos recém-traduzidos em um local temporário e atualiza a cópia de idioma existente depois que você aprova explicitamente os ativos. Se você rejeitar o(s) ativo(s), a cópia de idioma permanecerá inalterada.

1. Clique/toque na pasta raiz de origem, em **[!UICONTROL Cópias de idioma]** para as quais você já criou uma cópia de idioma e clique/toque em **[!UICONTROL Revelar no Assets]** para abrir a pasta no AEM Assets.
1. Na interface do usuário do Assets, selecione um ativo que já tenha sido convertido e clique/toque no ícone **[!UICONTROL Editar]** na barra de ferramentas para abrir o ativo no modo de edição.
1. Edite o ativo e salve as alterações.
1. Execute as etapas 2 a 14 do procedimento [Adicionar ao projeto](#add-to-existing-translation-project) de tradução existente para atualizar a cópia de idioma.
1. Clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. Na lista de ativos na página Trabalho **[!UICONTROL de]** tradução, é possível visualização claramente o local temporário onde a versão traduzida do ativo é armazenada.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Título]**.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Aceitar tradução]** e em **[!UICONTROL Aceitar]** na caixa de diálogo para substituir o ativo traduzido na pasta de destino pela versão traduzida do ativo editado.

   >[!NOTE]
   >
   >Para permitir que o fluxo de trabalho de tradução atualize o(s) ativo(s) de destino, aceite o ativo e os metadados.

   Clique/toque em **[!UICONTROL Rejeitar tradução]** para manter a versão traduzida originalmente do ativo na raiz da localidade do público alvo e rejeitar a versão editada.

1. Navegue até o console Ativos e abra a página Propriedades de cada um dos ativos traduzidos para visualização dos metadados traduzidos.

Para obter dicas sobre como traduzir metadados para ativos com eficiência, consulte [5 etapas para traduzir metadados](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)com eficiência.

## Criar projetos de tradução {#creating-translation-projects}

Para criar uma cópia de idioma, dispare um dos seguintes workflows de cópia de idioma disponíveis no painel Referências na interface do usuário do Assets:

**Criar e traduzir**

Neste fluxo de trabalho, os ativos a serem traduzidos são copiados para a raiz do idioma para o qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução for criado.

**Atualizar cópias de idioma**

Você executa esse fluxo de trabalho para traduzir um grupo adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta do público alvo que já contém os ativos convertidos anteriormente.

>[!NOTE]
>
>Os binários de ativos são traduzidos somente se o provedor de serviço de tradução suportar a tradução de binários.

>[!NOTE]
>
>Se você iniciar um fluxo de trabalho de tradução para ativos complexos, como arquivos PDF e arquivos do Adobe InDesign, seus subativos ou representações (se houver) não serão submetidos para conversão.

### Criar e traduzir fluxo de trabalho {#create-and-translate-workflow}

Use o fluxo de trabalho de criação e tradução para gerar cópias de idioma para um idioma específico pela primeira vez. O fluxo de trabalho fornece as seguintes opções:

* Criar somente estrutura
* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar somente estrutura {#create-structure-only}

Use a opção **Somente criar estrutura** para criar uma hierarquia de pasta de destino na raiz do idioma de destino para corresponder à hierarquia da pasta de origem na raiz do idioma de origem. Nesse caso, os ativos de origem são copiados na pasta de destino. No entanto, nenhum projeto de tradução é gerado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma estrutura na raiz do idioma do público alvo.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]**, em **[!UICONTROL Cópias]**.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. From the **[!UICONTROL Target Languages]** list, select the language for which you want to create a folder structure.
1. Na lista **[!UICONTROL Projeto]**, escolha **[!UICONTROL Somente criar estrutura]**.
1. Clique/toque em **[!UICONTROL Criar]**. A nova estrutura para o idioma do público alvo é listada em Cópias **[!UICONTROL de idiomas]**.
1. Clique/toque na estrutura da lista e, em seguida, clique/toque em **[!UICONTROL Revelar nos ativos]** para navegar até a estrutura da pasta no idioma do público alvo.

## Aplicar serviços de tradução em nuvem a pastas {#applying-translation-cloud-services-to-folders}

O Adobe Experience Manager (AEM) permite que você utilize serviços de tradução baseados em nuvem do provedor de tradução de sua escolha para garantir que seus ativos sejam traduzidos com base em suas necessidades.

Você pode aplicar o serviço de nuvem de tradução diretamente à sua pasta de ativos para que eles possam ser utilizados durante os workflows de tradução.

### Aplicar os serviços de tradução {#applying-the-translation-services}

A aplicação de serviços de tradução em nuvem diretamente à sua pasta de ativos elimina a necessidade de configurar os serviços de tradução ao criar ou atualizar workflows de tradução.

1. Na interface do usuário do Assets, selecione a pasta na qual deseja aplicar os serviços de tradução.
1. Na barra de ferramentas, clique/toque no ícone **[!UICONTROL Propriedades]** para exibir a página **[!UICONTROL Propriedades da pasta]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navegue até a guia **[!UICONTROL Serviços da nuvem]**.
1. Na lista Configurações do serviço em nuvem, escolha o provedor de tradução desejado. Por exemplo, se você deseja utilizar os serviços de tradução da Microsoft, escolha **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Escolha o conector para o provedor de tradução.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Na barra de ferramentas, clique/toque em **[!UICONTROL Salvar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. O serviço de tradução é aplicado à pasta.

### Aplicar conector de tradução personalizado {#applying-custom-translation-connector}

Se quiser aplicar um conector personalizado para os serviços de tradução que deseja usar nos fluxos de trabalho de tradução. Para aplicar um conector personalizado, primeiro instale o conector do Gerenciador de pacotes. Em seguida, configure o conector do console Serviços da nuvem. Após configurar o conector, ele estará disponível na lista de conectores na guia Serviços da nuvem descrita em [Aplicar serviços de tradução](#applying-the-translation-services). Depois de aplicar o conector personalizado e executar os fluxos de trabalho de tradução, o bloco **[!UICONTROL Resumo da tradução]** do projeto de tradução exibe os detalhes do conector nos cabeçalhos **[!UICONTROL Provedor]** e **[!UICONTROL Método]**.

1. Instale o conector do Gerenciador de pacotes.
1. Clique/toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Implantação > Serviços]** em nuvem.
1. Localize o conector instalado em **[!UICONTROL Serviços de terceiros]** na página **[!UICONTROL Serviços da nuvem]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Clique/toque no link **[!UICONTROL Configurar agora]** para abrir a caixa de diálogo **[!UICONTROL Criar configuração]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique um título e nome para o conector e clique/toque em **[!UICONTROL Criar]**. O conector personalizado está disponível na lista de conectores na guia **[!UICONTROL Serviços da nuvem]** descrita na etapa 5 de [Aplicar serviços de tradução](#applying-the-translation-services).
1. Execute qualquer fluxo de trabalho de tradução descrito em Criar projetos de tradução depois de aplicar o conector personalizado. Verifique os detalhes do conector no bloco **[!UICONTROL Resumo da tradução]** do projeto de tradução no console **[!UICONTROL Projetos]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
