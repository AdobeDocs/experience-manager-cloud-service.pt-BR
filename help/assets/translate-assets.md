---
title: Criar e gerenciar ativos digitais em vários idiomas e executar fluxos de trabalho de tradução
description: Saiba como automatizar os fluxos de trabalho para converter ativos, incluindo binários, metadados e tags em vários idiomas.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Ativos multilíngues {#multilingual-assets}

Ativos multilíngues são ativos com binários, metadados e tags em vários idiomas. Geralmente, binários, metadados e tags para ativos existem em um idioma, que são traduzidos para outros idiomas para uso em projetos multilíngues. Os ativos Adobe Experience Manager (AEM) permitem que você automatize os fluxos de trabalho de tradução em ativos (incluindo binários, metadados e tags) para gerar ativos em outros idiomas para uso em projetos multilíngues.

Para automatizar os fluxos de trabalho de tradução, você integra os provedores de serviços de tradução ao AEM e cria projetos para traduzir ativos em vários idiomas. O AEM suporta fluxos de trabalho de tradução automática e humana.

Tradução humana: Os ativos convertidos são devolvidos e importados para o AEM. Quando seu provedor de tradução está integrado ao AEM, os ativos são automaticamente enviados entre o AEM e o provedor de tradução.

Tradução automática: O serviço de tradução automática traduz imediatamente os metadados e as tags dos ativos.

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

Ativos multilíngues são ativos com binários, metadados e tags em vários idiomas. Geralmente, binários, metadados e tags para ativos existem em um idioma, que são traduzidos para outros idiomas para uso em projetos multilíngues.

Nos ativos Adobe Experience Manager (AEM), ativos multilíngues são incluídos em pastas, onde cada pasta contém os ativos em um idioma diferente.

Cada pasta de idioma é chamada de cópia de idioma. A pasta raiz de uma cópia de idioma, conhecida como raiz de idioma, identifica o idioma do conteúdo na cópia de idioma. Por exemplo, `/content/dam/it` é a raiz do idioma italiano para a cópia em italiano. As cópias de idioma devem usar uma raiz [de idioma configurada](#create-a-language-root) corretamente para que o idioma correto seja direcionado quando as traduções dos ativos de origem forem executadas.

A cópia de idioma para a qual você adicionou ativos originalmente é o idioma mestre. O mestre de idioma é a fonte traduzida para outros idiomas. Uma hierarquia de pastas de amostra inclui várias raízes de idioma:

```
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
1. Crie a raiz de cada idioma de destino para o qual você precisa de uma cópia de idioma.

### Criar uma raiz de idioma {#create-a-language-root}

Para criar a raiz do idioma, crie uma pasta e use um código de idioma ISO como o valor da propriedade Name. Depois de criar a raiz do idioma, é possível criar uma cópia do idioma em qualquer nível na raiz do idioma.

Por exemplo, a página raiz da cópia em idioma italiano da hierarquia de amostra tem `it` a propriedade Name. A propriedade Name é usada como o nome do nó do ativo no repositório e, portanto, determina o caminho dos ativos. (*&lt;servidor>:&lt;porta>/assets.html/content/dam/it/*)

1. No console Ativos, clique/toque em **[!UICONTROL Criar]** e escolha **[!UICONTROL Pasta]** no menu.
1. No campo Nome, digite o código do país no formato de `<language-code>`.
1. Clique ou toque em **[!UICONTROL Criar]**. A raiz do idioma é criada no console Ativos.

### Exibir raízes de idioma {#view-language-roots}

A interface otimizada para toque fornece um painel Referências que mostra uma lista de raízes de idioma que foram criadas nos ativos AEM.

1. No console Ativos, selecione o idioma mestre para o qual deseja criar cópias de idioma.
1. Clique ou toque no ícone GlobalNav e escolha **[!UICONTROL Referências]** para abrir o painel Referência.
1. No painel Referências, clique ou toque em Cópias **[!UICONTROL de idioma]**. O painel Cópias de idioma mostra as cópias de idioma dos ativos.

### Criar um novo projeto de tradução {#create-a-new-translation-project}

Se você usar essa opção, os ativos a serem traduzidos serão copiados para a raiz do idioma para o qual você deseja traduzir. Dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou executado automaticamente assim que o projeto de tradução for criado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma cópia de Idioma.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista Idiomas **[!UICONTROL de]** destino, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]** , selecione **[!UICONTROL Criar um novo projeto]** de tradução.
1. No campo Título **[!UICONTROL do]** projeto, informe um título para o projeto.
1. Clique/toque em **[!UICONTROL Criar]**. Os ativos da pasta de origem são copiados para as pastas de destino das localidades selecionadas na etapa 4.
1. Para navegar até a pasta, selecione a cópia de idioma e clique em **[!UICONTROL Revelar em Ativos]**.
1. Navegue até o console Projetos. A pasta de tradução é copiada para o console Projetos.
1. Abra a pasta para exibir o projeto de tradução.
1. Clique/toque no projeto para abrir a página de detalhes.
1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Na interface do usuário Ativos, abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

>[!NOTE]
>
>Este recurso está disponível para ativos e pastas. Quando um ativo é selecionado em vez de uma pasta, toda a hierarquia de pastas até a raiz do idioma é copiada para criar uma cópia do idioma para o ativo.

### Add to an existing translation project {#add-to-existing-translation-project}

Se você usar essa opção, o fluxo de trabalho de tradução será executado para os ativos adicionados à pasta de origem após executar um fluxo de trabalho de tradução anterior. Somente os ativos recém-adicionados são copiados para a pasta de destino que contém ativos convertidos anteriormente. Nenhum novo projeto de tradução é criado neste caso.

1. Na interface do usuário Ativos, navegue até a pasta de origem que contém ativos não convertidos.
1. Selecione um ativo que deseja traduzir e abra o painel **** Referência. A seção Cópias **[!UICONTROL de]** idioma exibe o número de cópias de tradução atualmente disponíveis.
1. Clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**. Uma lista de cópias de tradução disponíveis é exibida.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista Idiomas **[!UICONTROL de]** destino, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]** , selecione **[!UICONTROL Adicionar ao projeto]** de tradução existente para executar o fluxo de trabalho de tradução na pasta.
   >[!NOTE]
   >
   >Se você escolher a opção **[!UICONTROL Adicionar ao projeto]** de tradução existente, seu projeto de tradução será adicionado a um projeto pré-existente somente se as configurações do projeto corresponderem exatamente às configurações do projeto pré-existente. Caso contrário, um novo projeto será criado.
1. Na lista Projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.
1. Click/tap **[!UICONTROL Create]**. Os ativos a serem convertidos são adicionados à pasta de destino. A pasta atualizada está listada na seção Cópias de **[!UICONTROL idioma]** .
1. Navegue até o console Projetos e abra o projeto de tradução existente ao qual você adicionou.
1. Clique/toque na exibição do projeto de tradução na página de detalhes do projeto.
1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

   >[!NOTE]
   >
   >* Se você excluir a entrada para tags ou metadados, nenhuma tag ou metadados será traduzida para qualquer um dos ativos.
   >* Se você usar Tradução automática, os binários de ativos não serão traduzidos.
   >* Se o ativo adicionado ao trabalho de tradução incluir subativos, selecione os subativos e remova-os para que a tradução continue sem falhas.


1. Para iniciar a tradução dos ativos, clique/toque na seta no bloco Trabalho **[!UICONTROL de]** tradução e selecione **[!UICONTROL Iniciar]** na lista. Uma mensagem notifica o início do trabalho de tradução.
1. Para exibir o status do trabalho de tradução, clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Após a conclusão da tradução, o status é alterado para Pronto para Revisão. Navegue até a interface do usuário Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

### Atualizar cópias de idioma {#update-language-copies}

Execute esse fluxo de trabalho para traduzir qualquer conjunto adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta de destino que já contém ativos convertidos anteriormente. Dependendo da escolha das opções, um projeto de tradução é criado ou um projeto de tradução existente é atualizado para os novos ativos. O fluxo de trabalho de cópias de idioma de atualização inclui as seguintes opções:

* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project-1}

Se você usar essa opção, o conjunto de ativos será adicionado a um projeto de tradução existente para atualizar a cópia de idioma para a localidade escolhida.

1. Na interface do usuário Ativos, selecione a pasta de origem na qual você adicionou uma pasta de ativos.
1. Abra o painel **** Referências e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.
1. Marque a caixa de seleção antes de Cópias **[!UICONTROL de]** idioma, que seleciona todas as cópias de idioma. Cancele a seleção de outras cópias, exceto a cópia de idioma (cópias) correspondente às localidades para as quais você deseja traduzir.
1. Clique/toque em **[!UICONTROL Atualizar cópias]** de idioma na parte inferior.
1. Na lista **[!UICONTROL Projeto]** , escolha **[!UICONTROL Adicionar ao projeto]** de tradução existente.
1. Na lista Projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.
1. Clique/toque em **[!UICONTROL Iniciar]**.
1. Consulte as etapas 9 a 14 de [Adicionar ao projeto](#add-to-existing-translation-project) de tradução existente para concluir o restante do procedimento.

### Criar cópias de idioma temporárias {#creating-temporary-language-copies}

Quando você executa um fluxo de trabalho de tradução para atualizar uma cópia de idioma com versões editadas dos ativos originais, a cópia de idioma existente é preservada até que você aprove os ativos convertidos. O AEM Assets armazena os ativos recém-traduzidos em um local temporário e atualiza a cópia de idioma existente depois que você aprova explicitamente os ativos. Se você rejeitar o(s) ativo(s), a cópia de idioma permanecerá inalterada.

1. Clique/toque na pasta raiz de origem em Cópias **[!UICONTROL de]** idioma para as quais você já criou uma cópia de idioma e clique/toque em **[!UICONTROL Revelar nos ativos]** para abrir a pasta nos ativos AEM.
1. Na interface do usuário do Assets, selecione um ativo que já tenha sido convertido e clique/toque no ícone **[!UICONTROL Editar]** na barra de ferramentas para abrir o ativo no modo de edição.
1. Edite o ativo e salve as alterações.
1. Execute as etapas 2 a 14 do procedimento [Adicionar ao projeto](#add-to-existing-translation-project) de tradução existente para atualizar a cópia de idioma.
1. Clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. Na lista de ativos na página Trabalho **[!UICONTROL de]** tradução, é possível exibir claramente o local temporário onde a versão traduzida do ativo é armazenada.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Título]**.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Aceitar tradução]** e, em seguida, clique/toque em **[!UICONTROL Aceitar]** na caixa de diálogo para substituir o ativo convertido na pasta de destino pela versão traduzida do ativo editado.

   >[!NOTE]
   >
   >Para permitir que o fluxo de trabalho de tradução atualize o(s) ativo(s) de destino, aceite o ativo e os metadados.

   Clique/toque em **[!UICONTROL Rejeitar tradução]** para manter a versão traduzida originalmente do ativo na raiz da localidade de destino e rejeitar a versão editada.

1. Navegue até o console Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

Para obter dicas sobre como traduzir metadados para ativos com eficiência, consulte [5 etapas para traduzir metadados](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)com eficiência.

## Criar projetos de tradução {#creating-translation-projects}

Para criar uma cópia de idioma, dispare um dos seguintes fluxos de trabalho de cópia de idioma disponíveis no painel Referências na interface do usuário do Assets:

**Criar e traduzir**

Neste fluxo de trabalho, os ativos a serem traduzidos são copiados para a raiz do idioma para o qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução for criado.

**Atualizar cópias de idioma**

Você executa esse fluxo de trabalho para traduzir um grupo adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta de destino que já contém ativos convertidos anteriormente.

>[!NOTE]
>
>Os binários de ativos são traduzidos somente se o provedor de serviços de tradução suportar a tradução de binários.

>[!NOTE]
>
>Se você iniciar um fluxo de trabalho de tradução para ativos complexos, como arquivos PDF e arquivos do Adobe InDesign, seus subativos ou representações (se houver) não serão submetidos para conversão.

### Criar e traduzir fluxo de trabalho {#create-and-translate-workflow}

Use o fluxo de trabalho de criação e tradução para gerar cópias de idioma para um idioma específico pela primeira vez. O fluxo de trabalho fornece as seguintes opções:

* Criar somente estrutura
* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar somente estrutura {#create-structure-only}

Use a opção **Criar estrutura somente** para criar uma hierarquia de pasta de destino na raiz do idioma de destino para corresponder à hierarquia da pasta de origem na raiz do idioma de origem. Nesse caso, os ativos de origem são copiados para a pasta de destino. No entanto, nenhum projeto de tradução é gerado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma estrutura na raiz do idioma de destino.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista Idiomas **[!UICONTROL de]** destino, selecione o idioma para o qual deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]** , escolha Somente **** Criar estrutura.
1. Click/tap **[!UICONTROL Create]**. A nova estrutura para o idioma de destino é listada em Cópias **[!UICONTROL de idiomas]**.
1. Clique/toque na estrutura da lista e, em seguida, clique/toque em **[!UICONTROL Revelar nos ativos]** para navegar até a estrutura de pastas dentro do idioma de destino.

## Aplicar serviços de tradução em nuvem a pastas {#applying-translation-cloud-services-to-folders}

O Adobe Experience Manager (AEM) permite que você utilize serviços de tradução baseados em nuvem do provedor de tradução de sua escolha para garantir que seus ativos sejam traduzidos com base em suas necessidades.

Você pode aplicar o serviço de nuvem de tradução diretamente à sua pasta de ativos para que eles possam ser utilizados durante os fluxos de trabalho de tradução.

### Aplicar os serviços de tradução {#applying-the-translation-services}

A aplicação de serviços de tradução em nuvem diretamente à sua pasta de ativos elimina a necessidade de configurar os serviços de tradução ao criar ou atualizar fluxos de trabalho de tradução.

1. Na interface do usuário do Assets, selecione a pasta na qual deseja aplicar os serviços de tradução.
1. Na barra de ferramentas, clique/toque no ícone **[!UICONTROL Propriedades]** para exibir a página Propriedades **[!UICONTROL da]** pasta.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navegue até a guia Serviços **[!UICONTROL em]** nuvem.
1. Na lista Configurações de serviços em nuvem, escolha o provedor de tradução desejado. Por exemplo, se você deseja utilizar os serviços de tradução da Microsoft, escolha **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Escolha o conector para o provedor de tradução.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Na barra de ferramentas, clique/toque em **[!UICONTROL Salvar]** e clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. O serviço de tradução é aplicado à pasta.

### Aplicar conector de tradução personalizado {#applying-custom-translation-connector}

Se quiser aplicar um conector personalizado para os serviços de tradução que deseja usar nos fluxos de trabalho de tradução. Para aplicar um conector personalizado, instale primeiro o conector do Gerenciador de pacotes. Em seguida, configure o conector do console Serviços em nuvem. Após configurar o conector, ele estará disponível na lista de conectores na guia Serviços em nuvem descrita em [Aplicando os serviços](#applying-the-translation-services)de tradução. Depois de aplicar o conector personalizado e executar fluxos de trabalho de tradução, o bloco Resumo **[!UICONTROL da]** tradução do projeto de tradução exibe os detalhes do conector sob os cabeçalhos **[!UICONTROL Provedor]** e **[!UICONTROL Método]**.

1. Instale o conector do Package Manager.
1. Clique/toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Implantação > Serviços]** em nuvem.
1. Localize o conector instalado em Serviços **[!UICONTROL de]** terceiros na página Serviços **[!UICONTROL da]** Cloud.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Clique/toque no link **[!UICONTROL Configurar agora]** para abrir a caixa de diálogo **[!UICONTROL Criar configuração]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique um título e um nome para o conector e clique/toque em **[!UICONTROL Criar]**. O conector personalizado está disponível na lista de conectores na guia Serviços **[!UICONTROL em]** nuvem descrita na etapa 5 de [Aplicação dos serviços](#applying-the-translation-services)de tradução.
1. Execute qualquer fluxo de trabalho de tradução descrito na criação de projetos de tradução depois de aplicar o conector personalizado. Verifique os detalhes do conector no bloco Resumo **[!UICONTROL da]** tradução do projeto de tradução no console **[!UICONTROL Projetos]** .

   ![chlimage_1-220](assets/chlimage_1-220.png)
