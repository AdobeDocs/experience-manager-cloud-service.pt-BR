---
title: Como gerenciar tags na visualização do Assets?
description: Saiba como gerenciar tags na visualização do Assets. As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência.
exl-id: 7c5e1212-054f-46ca-9982-30e40b0482e1
source-git-commit: cadf0e383608a39200d716cc698ad1979f24fd1d
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 70%

---

# Gerenciar tags na visualização do Assets {#view-assets-and-details}


>[!CONTEXTUALHELP]
>id="assets_taxonomy_management"
>title="Gerenciar tags"
>abstract="As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência. Administradores(as) podem usar a estrutura hierárquica de marcação, o que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte à pesquisa, a reutilização de tags, a melhora da capacidade de descoberta e assim por diante."

As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e fluxos de trabalho.

Listas planas de vocabulários controlados podem se tornar incontroláveis com o tempo. Administradores(as) podem usar a estrutura hierárquica de marcação, o que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte à pesquisa, a reutilização de tags, a melhora da capacidade de descoberta e assim por diante.

Você pode criar um namespace no nível raiz e criar uma estrutura hierárquica de subtags no namespace. Por exemplo, você pode criar um namespace `Activities` no nível raiz e ter as tags `Cycling`, `Hiking` e `Running` no namespace. É possível incluir as subtags `Clothing` e `Shoes` em `Running`.

![Gerenciamento de marcação](assets/tags-hierarchy.png)

A marcação oferece muitos benefícios, como:

* A marcação permite que autores organizem facilmente ativos diferentes por meio de uma taxonomia comum. Autores podem pesquisar e organizar ativos rapidamente por tags comuns.

* As tags hierárquicas são extremamente flexíveis e são uma excelente maneira de organizar termos de maneira lógica. Por meio de namespaces, tags e subtags, sistemas taxonômicos inteiros podem ser representados.

* As tags podem evoluir com o tempo, à medida que um vocabulário organizacional muda.

* As tags gerenciadas na visualização de admin permanecem em sincronia com as tags gerenciadas na visualização do Assets, o que garante a governança e a integridade dos metadados.

Para poder aplicar tags nos ativos, primeiro crie um namespace e depois insira tags adicionais nele. Também é possível criar tags e adicioná-las a um namespace existente. Todas as tags criadas no nível raiz são automaticamente adicionadas ao namespace Tags padrão. Em seguida, é possível adicionar o campo Tags ao formulário de metadados para que ele seja exibido na página de detalhes do ativo. Depois de definir essas configurações, você pode começar a aplicar tags nos ativos.

>[!NOTE]
>
>Você precisa adicionar o campo Tags ao formulário de metadados somente se não estiver usando o formulário de metadados padrão.

![Gerenciamento de marcação](assets/tagging-taxonomy-management.png)

Recursos adicionais além dos mencionados neste artigo, incluindo mesclagem, renomeação, localização e publicação de tags, estão disponíveis na visualização de Admin.

## Criar um namespace {#create-a-namespace}

Um namespace é um container para tags que só pode existir no nível raiz. Você pode começar a configurar a estrutura hierárquica de tags definindo primeiro um nome lógico para o namespace. Se você não adicionar uma tag a um dos namespaces existentes, a tag será movida automaticamente para as Tags padrão.

Execute as seguintes etapas para criar um namespace:

1. Acesse `Taxonomy Management` em `Settings` para exibir a lista de namespaces existentes. Você também pode ver a data da última modificação, o usuário que modificou o namespace ou as tags inseridas nele, bem como o número de vezes que a tag foi usada em um ativo.
1. Clique em `Create Namespace`.
1. Adicione `Title`, `Name` e `Description` no namespace. A entrada especificada no campo `Title` é exibida na parte superior da hierarquia. Por exemplo, na imagem a seguir, **Atividades** refere-se ao título do namespace.

   ![Gerenciamento de marcação](assets/tags-hierarchy.png)

1. Clique em `Save`.

## Adicionar tags a um namespace {#add-tags-to-namespace}

Execute as seguintes etapas para adicionar tags a um namespace:

1. Ir para **[!UICONTROL Gerenciamento de taxonomia]**.
1. Selecione o namespace e clique em `Create` para criar a tag no nível superior, logo abaixo do namespace. Se precisar criar uma subtag em uma tag existente em um namespace, selecione a tag e clique em `Create`.
   ![Hierarquia de tags](assets/hierarchy-of-tags.png)

   Neste exemplo, a imagem à esquerda representa a tag diretamente abaixo do namespace `automobile-four-wheeler` exibido no campo `Path`. A imagem à direita é um exemplo de subtags adicionadas em uma tag, pois há outros nomes de tag (`jeep` e `jeep-meridian`) exibidos no campo `Path` além do namespace.
1. Especifique o título, o nome e a descrição da tag e clique em `Save`.


   >[!NOTE]
   >
   >* Os campos `Title` e `Name` são obrigatórios, enquanto o campo `Description` é opcional.
   >* Por padrão, a ferramenta copia o texto digitado no campo Título, remove os espaços em branco ou caracteres especiais (. &amp; / \ : * ? [ ] | &quot; %), e o armazena como o nome.
   >* Você pode atualizar o campo `Title` posteriormente, mas o campo `Name` é somente leitura.

## Adicionar tags às tags padrão {#add-tags-to-standard-tags}

Tags não estruturadas ou que não possuem hierarquia são armazenadas no namespace `Standard Tags`. Além disso, quando quiser adicionar mais termos descritivos sem afetar a taxonomia controlada, você poderá armazenar esse valor em `Standard Tags`. Você pode mover esses valores em namespaces estruturados ao longo do tempo. Além disso, você pode usar o namespace `Standard Tags` como uma entrada de formato livre para palavras-chave.

Para criar uma tag padrão, clique em `Create Tag` no nível raiz. Especifique o título, o nome e a descrição e clique em `Save`.

![Adicionar tags às tags padrão](assets/adding-tags-to-standard-tags.png)

>[!NOTE]
>
>Se você excluir o namespace `Standard Tags` usando o Assets as a Cloud Service, as tags criadas no nível raiz não serão exibidas na lista de tags disponíveis.

## Mover tags {#move-tags}

Caso você armazene as tags na hierarquia errada ou a taxonomia mude ao longo do tempo, é possível mover as tags selecionadas para manter a integridade dos dados. As seguintes condições devem ser consideradas ao movimentar as tags:

* As tags só podem ser movidas entre namespaces existentes ou em uma hierarquia de tags existente.
* As tags não podem ser movidas para a raiz para se tornarem um namespace.
* Mover uma tag principal também move todas as tags secundárias armazenadas na hierarquia.

Execute as seguintes etapas para mover tags de um local para outro:

1. Selecione a tag ou toda a hierarquia de tags no namespace apropriado e clique em `Move`.
1. Na caixa de diálogo Mover, selecione a nova tag de destino ou o namespace usando a seção `Select Tag`.
1. Clique em `Save`. A tag é exibida em seu novo local.

## Editar tags {#edit-tags}

Para editar o título da tag, selecione-a e clique em `Edit`. Especifique o novo título e clique em `Save`.

>[!NOTE]
>
>* O `Name` de uma tag não pode ser atualizado. O caminho raiz de uma tag também se baseia no nome da tag. O caminho permanece o mesmo se você atualizar o campo `Title`.
>* Operações adicionais como mesclar, localizar e publicar estão disponíveis no Assets as a Cloud Service.

## Excluir tags {#delete-tags}

É possível excluir vários namespaces ou tags simultaneamente. A operação de exclusão não pode ser desfeita.

Execute as seguintes etapas para excluir tags:

1. Selecione o namespace ou a tag e clique em `Delete`.
1. Clique em `Confirm`.

>[!NOTE]
>
>* A exclusão da tag principal ou do namespace também exclui as subtags armazenadas na hierarquia. Se precisar excluir ou atualizar o namespace principal, é recomendável [mover as tags](#moving-tags) para o novo destino antes de excluir a hierarquia principal.
>* A exclusão de uma tag também exclui todas as suas referências dos ativos.
>* Não é possível excluir tags padrão existentes no nível raiz.

## Adicionar o componente de Tags ao formulário de Metadados {#add-tags-to-metadata-form}

O componente de tags é adicionado ao formulário de metadados `default` automaticamente. Você pode criar um [formulário de metadados](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/metadata.html?lang=br#metadata-forms) do zero ou utilizar um modelo. Se você não estiver usando um modelo de formulário de metadados existente, poderá modificar o formulário de metadados e adicionar o componente de tags. O mapeamento da propriedade de metadados é preenchido automaticamente e não pode ser modificado neste momento. [!DNL Assets as a Cloud Service] os usuários podem atualizar o mapeamento para armazenar valores de tag usando namespaces personalizados e expor apenas subconjuntos de hierarquias usando caminhos raiz.

Assista a este vídeo rápido para ver como adicionar o componente de tags ao formulário de metadados:

>[!VIDEO](https://video.tv.adobe.com/v/3420452)


### Adicionar tags aos ativos {#add-tags-to-assets}

1. Acesse a página Detalhes do ativo e navegue até a seção `Tags` do formulário de metadados.
1. Selecione o ícone do seletor de tags, ao lado do campo Tags, ou comece a digitar um nome de tag para ver os resultados sugeridos.

   ![Marcação de ativos](assets/adding-tags-to-assets.png)

1. Selecione uma ou mais tags. A subtag é selecionada automaticamente junto com a tag principal ou o namespace.
As tags modificadas no Assets Essentials também são aplicadas no Assets as a Cloud Service.

## Adicionar tags ao incluo na lista de bloqueios {#blocklist-essentials}

[!DNL Assets view] O permite configurar uma inclui na lista de bloqueios que inclui palavras que não devem ser adicionadas como Tags inteligentes a ativos quando eles forem carregados no repositório. Esse recurso ajuda a manter a conformidade da marca e reduz o esforço para moderar as Tags inteligentes.
<!--
### Block smart tags for single asset {#block-smart-tags-for-single-asset}
![block smart tags](assets/block-smart-tags.png)
-->

### Bloquear tags inteligentes para todos os ativos {#block-smart-tags-for-all-assets}

[!DNL Assets view] O permite que um administrador bloqueie tags inteligentes para ativos existentes e recém-adicionados. Para bloquear tags, execute as seguintes etapas:

1. Navegue até **[!UICONTROL Tags bloqueadas]** em **[!UICONTROL Configurações]**.
1. Clique em **[!UICONTROL Adicionar tag bloqueada]**.
1. Digite as tags na caixa de texto que você precisa bloquear e clique em **[!UICONTROL Enter]**.
1. Quando terminar de adicionar tags, clique em **[!UICONTROL Adicionar]**. As tags inseridas são listadas na lista de tags bloqueadas.

   >[!NOTE]
   >
   >É possível adicionar no máximo 25 tags à lista de uma só vez. Repita as etapas para adicionar mais tags à inclui na lista de bloqueios.

Também é possível bloquear tags inteligentes para um único ativo. Navegue até os detalhes de um ativo. Em **[!UICONTROL Tags]** remova as tags inteligentes indesejadas e clique em **[!UICONTROL Salvar]**. Incluir na lista de bloqueios As tags são listadas na pesquisa para o ativo selecionado.

### Ações executadas na inclui na lista de bloqueios {#blocklist-actions}

* **Remover tags:** Também é possível remover as tags do incluo na lista de bloqueios. Para fazer isso, selecione uma ou mais tags que deseja remover. Clique em **[!UICONTROL Remover]**. É possível remover no máximo 25 tags da lista de uma só vez.
* **Selecionar tudo:** Marque a caixa de seleção ao lado de **Nome da tag** incluir na lista de bloqueios para selecionar todas as tags no arquivo de pesquisa.
* **Classificação:** Você pode classificar a inclui na lista de bloqueios em ordem crescente ou decrescente. Para fazer isso, clique na seta adjacente a **Nome da tag**.

  ![tags de bloqueio](assets/blocklist.gif)

  >[!NOTE]
  >
  >Não use caracteres especiais ao adicionar uma tag no incluo na lista de bloqueios. Caracteres como a-z, A-Z, 0-9 e - podem ser usados.

### Exportar inclui na lista de bloqueios{#export-blocklist}

A visualização de ativos permite exportar as tags bloqueadas listadas para o formato CSV. Para exportar a inclui na lista de bloqueios, execute as etapas abaixo:

1. Clique em **[!UICONTROL Exportar como CSV]**.
1. Escolha o local apropriado para salvar o arquivo CSV. Também é possível renomear o arquivo de acordo com o requisito.
1. Clique em **[!UICONTROL Salvar]**. A lista exportada em formato CSV é baixada no local selecionado.

### Importar inclui na lista de bloqueios{#import-blocklist}

A visualização de ativos fornece a capacidade de importar tags bloqueadas de uma fonte de dados (CSV). Para importar a inclui na lista de bloqueios, execute as etapas abaixo:

1. Clique em **[!UICONTROL Importar como CSV]**.
1. Escolha o arquivo CSV do seu dispositivo. Clique em **[!UICONTROL selecionar um arquivo]** para navegar até o arquivo do seu dispositivo. Como alternativa, você pode arrastar e soltar o arquivo CSV do seu dispositivo.
1. Clique em **[!UICONTROL Carregar]**. As tags do arquivo CSV estão listadas na lista de tags bloqueadas.

   ![Importar lista de tags bloqueadas](assets/import-blocked-tags.png)

Caso deseje baixar um modelo de tags bloqueadas, siga as etapas abaixo:

1. Clique em **[!UICONTROL Baixar modelo]**.
1. Escolha o local apropriado para salvar o arquivo CSV. Também é possível renomear o arquivo de acordo com o requisito.
1. Clique em **[!UICONTROL Salvar]**. Os modelos de tags de bloco no formato CSV são baixados no local selecionado.
