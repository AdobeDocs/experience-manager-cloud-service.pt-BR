---
title: Como traduzir ativos em AEM?
description: Saiba como automatizar fluxos de trabalho para traduzir ativos em AEM, incluindo binários, metadados e tags em vários idiomas.
contentOwner: AG
feature: Asset Management,Translation
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2642'
ht-degree: 24%

---

# Traduzir ativos em AEM {#multilingual-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/multilingual-assets.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Ativos multilíngues significa ativos com binários, metadados e tags em vários idiomas. Geralmente, os binários, metadados e tags de ativos existem em um idioma, que é traduzido para outros idiomas para uso em projetos multilíngues. Os ativos Adobe Experience Manager permitem automatizar fluxos de trabalho para traduzir ativos (incluindo binários, metadados e tags) para gerar ativos em outros idiomas para usar em projetos multilíngues.

Para automatizar AEM tradução de ativos, você integra os provedores de serviços de tradução ao Experience Manager e cria projetos para traduzir ativos em vários idiomas. O Experience Manager suporta fluxos de trabalho de tradução humana e de máquina.

Tradução de ativos humanos em AEM: Os ativos traduzidos são retornados e importados para o Experience Manager. Quando seu provedor de tradução é integrado ao Experience Manager, os ativos são automaticamente enviados entre o Experience Manager e o provedor de tradução.

Tradução de ativos da máquina no AEM: O serviço de tradução automática traduz imediatamente os metadados e as tags para os ativos.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparar para traduzir ativos {#prepare-to-translate-assets}

Ativos multilíngues significa ativos com binários, metadados e tags em vários idiomas. Geralmente, os binários, metadados e tags de ativos existem em um idioma, que é traduzido para outros idiomas para uso em projetos multilíngues.

No Adobe Experience Manager Assets, os ativos multilíngues são incluídos nas pastas, onde cada pasta contém os ativos em um idioma diferente.

Cada pasta de idioma é chamada de cópia de idioma. A pasta raiz de uma cópia de idioma, conhecida como raiz de idioma, identifica o idioma do conteúdo na cópia de idioma. Por exemplo, `/content/dam/it` é a raiz do idioma italiano para a cópia em língua italiana. As cópias de idioma devem usar um [raiz de idioma configurada corretamente](#create-a-language-root) para que o idioma correto seja direcionado quando as traduções de ativos de origem forem executadas.

A cópia de idioma para a qual você adicionou ativos originalmente é o idioma principal. O idioma principal é a fonte traduzida para outros idiomas. Uma exemplo de hierarquia de pasta inclui várias raízes de idioma:

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

Execute as seguintes etapas para preparar a tradução de ativos:

1. Crie a raiz do idioma do idioma principal. Por exemplo, a raiz de idioma da cópia em inglês na hierarquia de pasta de amostra é `/content/dam/en`. Verifique se a raiz do idioma está configurada corretamente de acordo com as informações em [Criar uma raiz de idioma](#create-a-language-root).

1. Adicione ativos ao idioma principal.
1. Crie a raiz de idioma de cada idioma de destino para o qual você precisa de uma cópia de idioma.

### Criar uma raiz de idioma {#create-a-language-root}

Para criar a raiz de idioma, crie uma pasta e use um código de idioma ISO como o valor da propriedade Name. Depois de criar a raiz do idioma, você pode criar uma cópia de idioma em qualquer nível na raiz do idioma.

Por exemplo, a página raiz da cópia de idioma italiano da hierarquia de amostra tem `it` como a propriedade Name . A propriedade Name é usada como o nome do nó do ativo no repositório e, portanto, determina o caminho dos ativos. (*&lt;server>:&lt;port>/assets.html/content/dam/it/*)

1. No console Assets, clique/toque em **[!UICONTROL Criar]** e escolha **[!UICONTROL Pasta]** no menu.
1. No campo Nome, digite o código do país no formato de `<language-code>`.
1. Clique ou toque em **[!UICONTROL Criar]**. A raiz do idioma é criada no console Assets.

### Exibir raízes do idioma {#view-language-roots}

A interface otimizada para toque fornece um painel Referências que mostra uma lista de raízes de idioma que foram criadas em [!DNL Assets].

1. No console Assets, selecione o idioma principal para o qual deseja criar cópias de idioma.
1. Clique ou toque no ícone de Navegação global e escolha **[!UICONTROL Referências]** para abrir o painel Referência.
1. No painel Referências , clique ou toque em **[!UICONTROL Cópias de idioma]**. O painel Cópias de idioma mostra as cópias de idioma dos ativos.

### Criar um novo projeto de tradução {#create-a-new-translation-project}

Se você usar essa opção, os ativos a serem traduzidos serão copiados para a raiz do idioma no qual deseja traduzir. Dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos . Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou executado automaticamente assim que o projeto de tradução for criado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma cópia de Idioma.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]**, em **[!UICONTROL Cópias]**.
1. Clicar/tocar **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista **[!UICONTROL Idiomas de destino]**, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. No **[!UICONTROL Projeto]** lista, selecione **[!UICONTROL Criar um novo projeto de tradução]**.
1. No campo **[!UICONTROL Título do projeto]**, informe um título para o projeto.
1. Clicar/tocar em **[!UICONTROL Criar]**. Os ativos da pasta de origem são copiados para as pastas de destino das localidades selecionadas na etapa 4.
1. Para navegar até a pasta, selecione a cópia de idioma e clique em **[!UICONTROL Receita em ativos]**.
1. Navegue até o console Projetos . A pasta de tradução é copiada para o console Projetos .
1. Abra a pasta para exibir o projeto de tradução.
1. Clique/toque no projeto para abrir a página de detalhes.
1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior do **[!UICONTROL Tarefa de tradução]** mosaico. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Na interface do usuário do Assets, abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

>[!NOTE]
>
>Esse recurso está disponível para ativos e pastas. Quando um ativo é selecionado em vez de uma pasta, toda a hierarquia de pastas até a raiz do idioma é copiada para criar uma cópia de idioma para o ativo.

### Adicionar a um projeto de tradução existente {#add-to-existing-translation-project}

Se você usar essa opção, o fluxo de trabalho de tradução será executado para ativos que você adicionar à pasta de origem após executar um fluxo de trabalho de tradução anterior. Somente os ativos recém-adicionados são copiados para a pasta de destino que contém ativos traduzidos anteriormente. Nenhum novo projeto de tradução é criado neste caso.

1. Na interface do usuário do Assets, navegue até a pasta de origem que contém ativos não traduzidos.
1. Selecione um ativo que deseja traduzir e abra o **[!UICONTROL painel Referência]**. A seção **[!UICONTROL Cópias de idioma]** exibe o número de cópias de tradução atualmente disponíveis.
1. Clique/toque em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]**. Uma lista de cópias de tradução disponíveis é exibida.
1. Clicar/tocar **[!UICONTROL Criar e traduzir]** na parte inferior.
1. Na lista **[!UICONTROL Idiomas de destino]**, selecione os idiomas para os quais deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]**, selecione **[!UICONTROL Adicionar ao projeto de tradução existente]** para executar o fluxo de trabalho de tradução na pasta.
   >[!NOTE]
   >
   >Se você escolher a variável **[!UICONTROL Adicionar ao projeto de tradução existente]** , seu projeto de tradução será adicionado a um projeto pré-existente somente se as configurações do projeto corresponderem exatamente às configurações do projeto pré-existente. Caso contrário, um novo projeto será criado.
1. No **[!UICONTROL Projeto de tradução existente]** selecione um projeto para adicionar o ativo para tradução.
1. Clique/toque em **[!UICONTROL Criar]**. Os ativos que serão traduzidos são adicionados à pasta de destino. A pasta atualizada está listada na seção **[!UICONTROL Cópias de idioma]**.
1. Navegue até o console Projetos e abra o projeto de tradução existente que você adicionou.
1. Clique/toque em projeto de tradução para exibir a página de detalhes do projeto.
1. Clique/toque nas reticências na parte inferior da **Tarefa de tradução** bloco para exibir os ativos no fluxo de trabalho de tradução. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

   >[!NOTE]
   >
   >* Se você excluir a entrada para tags ou metadados, nenhuma tag ou metadados é traduzido para qualquer um dos ativos.
   >* Se você usar Tradução automática, os binários de ativos não serão traduzidos.
   >* Se o ativo adicionado ao trabalho de tradução incluir subativos, selecione os subativos e remova-os para que a tradução continue sem falhas.


1. Para iniciar a tradução dos ativos, clique/toque na seta na **[!UICONTROL Tarefa de tradução]** bloco e selecione **[!UICONTROL Iniciar]** na lista. Uma mensagem notifica o início do trabalho de tradução.
1. Para exibir o status do trabalho de tradução, clique/toque nas reticências na parte inferior do **[!UICONTROL Tarefa de tradução]** mosaico. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Após a conclusão da tradução, o status é alterado para Pronto para revisar. Navegue até a interface do usuário do Assets e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

### Atualizar cópias de idioma {#update-language-copies}

Execute esse fluxo de trabalho para traduzir qualquer conjunto adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos traduzidos são adicionados à pasta de destino que já contém os ativos traduzidos anteriormente. Dependendo da escolha de opções, um projeto de tradução é criado ou um projeto de tradução existente é atualizado para os novos ativos. O fluxo de trabalho Atualizar cópias de idioma inclui as seguintes opções:

* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project-1}

Se você usar essa opção, o conjunto de ativos será adicionado a um projeto de tradução existente para atualizar a cópia de idioma para o local escolhido.

1. Na interface do usuário do Assets, selecione a pasta de origem na qual você adicionou uma pasta de ativos.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Cópias de idioma]**, que seleciona todas as cópias de idioma. Desmarque as outras cópias, exceto a cópia de idioma (cópias) correspondente às localidades para as quais você deseja traduzir.
1. Clicar/tocar **[!UICONTROL Atualizar cópias de idioma]** na parte inferior.
1. No **[!UICONTROL Projeto]** listar, escolha **[!UICONTROL Adicionar ao projeto de tradução existente]**.
1. No **[!UICONTROL Projeto de tradução existente]** selecione um projeto para adicionar o ativo para tradução.
1. Clique/toque em **[!UICONTROL Iniciar]**.
1. Veja as etapas 9 a 14 de [Adicionar ao projeto de tradução existente](#add-to-existing-translation-project) completar o resto do procedimento.

### Criar cópias temporárias de idioma {#creating-temporary-language-copies}

Quando você executa um fluxo de trabalho de tradução para atualizar uma cópia de idioma com as versões editadas dos ativos originais, a cópia de idioma existente é preservada até que você aprove o(s) ativo(s) traduzido(s). [!DNL Assets] armazena o(s) ativo(s) recém-traduzido(s) em um local temporário e atualiza a cópia de idioma existente após você aprovar explicitamente o(s) ativo(s). Se você rejeitar o(s) ativo(s), a cópia de idioma permanecerá inalterada.

1. Clique/toque na pasta raiz de origem, em **[!UICONTROL Cópias de idioma]** para as quais você já criou uma cópia de idioma e clique/toque em **[!UICONTROL Revelar no Assets]** para abrir a pasta no [!DNL Assets].
1. Na interface do usuário do Assets, selecione um ativo já traduzido e clique/toque no **[!UICONTROL Editar]** ícone na barra de ferramentas para abrir o ativo no modo de edição.
1. Edite o ativo e salve as alterações.
1. Execute as etapas 2 a 14 do [Adicionar ao projeto de tradução existente](#add-to-existing-translation-project) procedimento para atualizar a cópia de idioma.
1. Clique/toque nas reticências na parte inferior da **[!UICONTROL Tarefa de tradução]** mosaico. Na lista de ativos na **[!UICONTROL Tarefa de tradução]** , você pode exibir claramente o local temporário onde a versão traduzida do ativo é armazenada.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Título]**.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Aceitar tradução]** e em **[!UICONTROL Aceitar]** na caixa de diálogo para substituir o ativo traduzido na pasta de destino pela versão traduzida do ativo editado.

   >[!NOTE]
   >
   >Para permitir que o fluxo de trabalho de tradução atualize o(s) ativo(s) de destino, aceite o ativo e os metadados.

   Clicar/tocar **[!UICONTROL Rejeitar tradução]** para reter a versão traduzida originalmente do ativo na raiz da localidade de destino e rejeitar a versão editada.

1. Navegue até o console Assets e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## Criar projetos de tradução {#creating-translation-projects}

Para criar uma cópia de idioma, acione um dos seguintes fluxos de trabalho de cópia de idioma disponíveis no painel Referências na interface do usuário do Assets:

**Criar e traduzir**

Nesse fluxo de trabalho, os ativos a serem traduzidos são copiados para a raiz do idioma no qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos . Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução for criado.

**Atualizar cópias de idioma**

Execute esse fluxo de trabalho para traduzir um grupo adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos traduzidos são adicionados à pasta de destino que já contém os ativos traduzidos anteriormente.

>[!NOTE]
>
>Os binários de ativos são traduzidos somente se o provedor de serviços de tradução suportar a tradução de binários.

>[!NOTE]
>
>Se você iniciar um fluxo de trabalho de tradução para ativos complexos, como arquivos PDF e Adobe InDesign, seus subativos ou representações (se houver) não serão enviados para tradução.

### Criar e traduzir workflow {#create-and-translate-workflow}

Você usa o workflow criar e traduzir para gerar cópias de idioma para um idioma específico pela primeira vez. O fluxo de trabalho fornece as seguintes opções:

* Criar somente estrutura
* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar somente estrutura {#create-structure-only}

Use a opção **Somente criar estrutura** para criar uma hierarquia de pasta de destino na raiz do idioma de destino para corresponder à hierarquia da pasta de origem na raiz do idioma de origem. Nesse caso, os ativos de origem são copiados na pasta de destino. No entanto, nenhum projeto de tradução é gerado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma estrutura na raiz do idioma de destino.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em **[!UICONTROL Cópias de idioma]**, em **[!UICONTROL Cópias]**.
1. Clicar/tocar **[!UICONTROL Criar e traduzir]** na parte inferior.
1. No **[!UICONTROL Idiomas de destino]** selecione o idioma para o qual deseja criar uma estrutura de pastas.
1. Na lista **[!UICONTROL Projeto]**, escolha **[!UICONTROL Somente criar estrutura]**.
1. Clique/toque em **[!UICONTROL Criar]**. A nova estrutura para o idioma de destino está listada em **[!UICONTROL Cópias de idioma]**.
1. Clique/toque na estrutura da lista e, em seguida, clique/toque em **[!UICONTROL Receita em ativos]** para navegar até a estrutura de pastas no idioma de destino.

## Aplicar serviços de nuvem de tradução a pastas {#applying-translation-cloud-services-to-folders}

O Adobe Experience Manager permite que você utilize os serviços de tradução em nuvem do provedor de tradução de sua escolha para garantir que seus ativos sejam traduzidos de acordo com suas necessidades.

Você pode aplicar o serviço da nuvem de tradução diretamente à sua pasta de ativos para que eles possam ser utilizados durante os fluxos de trabalho de tradução.

### Aplicar os serviços de tradução {#applying-the-translation-services}

A aplicação de serviços da nuvem de tradução diretamente à sua pasta de ativos elimina a necessidade de configurar os serviços de tradução ao criar ou atualizar fluxos de trabalho de tradução.

1. Na interface do usuário do Assets, selecione a pasta na qual deseja aplicar os serviços de tradução.
1. Na barra de ferramentas, clique/toque no ícone **[!UICONTROL Propriedades]** para exibir a página **[!UICONTROL Propriedades da pasta]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navegue até a guia **[!UICONTROL Serviços da nuvem]**.
1. Na lista Configurações do Cloud Service, escolha o provedor de tradução desejado. Por exemplo, se você deseja aproveitar os serviços de tradução do Microsoft, escolha **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Escolha o conector para o provedor de tradução.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Na barra de ferramentas, clique/toque em **[!UICONTROL Salvar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. O serviço de tradução é aplicado à pasta.

### Aplicar conector de tradução personalizado {#applying-custom-translation-connector}

Se quiser aplicar um conector personalizado para os serviços de tradução que deseja usar nos fluxos de trabalho de tradução. Para aplicar um conector personalizado, primeiro instale o conector do [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md) Em seguida, configure o conector do console Serviços da nuvem. Após configurar o conector, ele estará disponível na lista de conectores na guia Serviços da nuvem descrita em [Aplicar serviços de tradução](#applying-the-translation-services). Depois de aplicar o conector personalizado e executar os fluxos de trabalho de tradução, o bloco **[!UICONTROL Resumo da tradução]** do projeto de tradução exibe os detalhes do conector nos cabeçalhos **[!UICONTROL Provedor]** e **[!UICONTROL Método]**.

1. Instale o conector de [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)
1. Clique/toque no logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas > Implantação > Cloud Services]**.
1. Localize o conector instalado em **[!UICONTROL Serviços de terceiros]** na página **[!UICONTROL Serviços da nuvem]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Clique/toque no **[!UICONTROL Configurar agora]** para abrir o **[!UICONTROL Criar configuração]** caixa de diálogo.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique um título e nome para o conector e clique/toque em **[!UICONTROL Criar]**. O conector personalizado está disponível na lista de conectores na guia **[!UICONTROL Serviços da nuvem]** descrita na etapa 5 de [Aplicar serviços de tradução](#applying-the-translation-services).
1. Execute qualquer fluxo de trabalho de tradução descrito em Criar projetos de tradução depois de aplicar o conector personalizado. Verifique os detalhes do conector no bloco **[!UICONTROL Resumo da tradução]** do projeto de tradução no console **[!UICONTROL Projetos]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)

**Consulte também**

* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
