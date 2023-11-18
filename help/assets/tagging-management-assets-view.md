---
title: Como gerenciar tags na visualização do Assets?
description: Saiba como gerenciar tags na visualização do Assets. As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência.
exl-id: 7c5e1212-054f-46ca-9982-30e40b0482e1
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 96%

---

# Gerenciar tags na visualização do Assets {#view-assets-and-details}


>[!CONTEXTUALHELP]
>id="assets_taxonomy_management"
>title="Gerenciar tags"
>abstract="As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência. Os administradores podem usar a estrutura hierárquica de marcação, que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante."

As tags ajudam a categorizar ativos que podem ser procurados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e fluxos de trabalho.

Listas planas de vocabulários controlados podem se tornar incontroláveis com o tempo. Os administradores podem usar a estrutura hierárquica de marcação, que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante.

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

## Criar um namespace {#creating-a-namespace}

Um namespace é um container para tags que só pode existir no nível raiz. Você pode começar a configurar a estrutura hierárquica de tags definindo primeiro um nome lógico para o namespace. Se você não adicionar uma tag a um dos namespaces existentes, a tag será movida automaticamente para as Tags padrão.

Execute as seguintes etapas para criar um namespace:

1. Acesse `Taxonomy Management` em `Settings` para exibir a lista de namespaces existentes. Você também pode ver a data da última modificação, o usuário que modificou o namespace ou as tags inseridas nele, bem como o número de vezes que a tag foi usada em um ativo.
1. Clique em `Create Namespace`.
1. Adicione `Title`, `Name` e `Description` no namespace. A entrada especificada no campo `Title` é exibida na parte superior da hierarquia. Por exemplo, na imagem a seguir, **Atividades** refere-se ao título do namespace.

   ![Gerenciamento de marcação](assets/tags-hierarchy.png)

   <!--
    >[!NOTE]
    >
    >You can use `Name` as a primary key if you are using any other metadata management tool is the source of truth for taxonomy values, you can use the name as a primary key.
    >
    -->

1. Clique em `Save`.

## Adição de tags a um namespace {#adding-tags-to-namespace}

Execute as seguintes etapas para adicionar tags a um namespace:

1. Acesse `Taxonomy Management`.
1. Selecione o namespace e clique em `Create` para criar a tag no nível superior, logo abaixo do namespace. Se precisar criar uma subtag em uma tag existente em um namespace, selecione a tag e clique em `Create`.
   ![Hierarquia de tags](assets/hierarchy-of-tags.png)

   Neste exemplo, a imagem à esquerda representa a tag diretamente abaixo do namespace `automobile-four-wheeler` exibido no campo `Path`. A imagem à direita é um exemplo de subtags adicionadas em uma tag, pois há outros nomes de tag (`jeep` e `jeep-meridian`) exibidos no campo `Path` além do namespace.
1. Especifique o título, o nome e a descrição da tag e clique em `Save`.


   >[!NOTE]
   >
   >* Os campos `Title` e `Name` são obrigatórios, enquanto o campo `Description` é opcional.
   >* Por padrão, a ferramenta copia o texto digitado no campo Título, remove os espaços em branco ou caracteres especiais (. &amp; / \ : * ? [ ] | &quot; %), e o armazena como o nome.
   >* Você pode atualizar o campo `Title` posteriormente, mas o campo `Name` é somente leitura.

## Adicionar tags às Tags padrão {#adding-tags-to-standard-tags}

Tags não estruturadas ou que não possuem hierarquia são armazenadas no namespace `Standard Tags`. Além disso, quando quiser adicionar mais termos descritivos sem afetar a taxonomia controlada, você poderá armazenar esse valor em `Standard Tags`. Você pode mover esses valores em namespaces estruturados ao longo do tempo. Além disso, você pode usar o namespace `Standard Tags` como uma entrada de formato livre para palavras-chave.

Para criar uma tag padrão, clique em `Create Tag` no nível raiz. Especifique o título, o nome e a descrição e clique em `Save`.

![Adicionar tags às tags padrão](assets/adding-tags-to-standard-tags.png)

>[!NOTE]
>
>Se você excluir o namespace `Standard Tags` usando a visualização de Admin, as tags criadas no nível raiz não serão exibidas na lista de tags disponíveis.

## Mover tags {#moving-tags}

Caso você armazene as tags na hierarquia errada ou a taxonomia mude ao longo do tempo, é possível mover as tags selecionadas para manter a integridade dos dados. As seguintes condições devem ser consideradas ao movimentar as tags:

* As tags só podem ser movidas entre namespaces existentes ou em uma hierarquia de tags existente.
* As tags não podem ser movidas para a raiz para se tornarem um namespace.
* Mover uma tag principal também move todas as tags secundárias armazenadas na hierarquia.

Execute as seguintes etapas para mover tags de um local para outro:

1. Selecione a tag ou toda a hierarquia de tags no namespace apropriado e clique em `Move`.
1. Na caixa de diálogo Mover, selecione a nova tag de destino ou o namespace usando a seção `Select Tag`.
1. Clique em `Save`. A tag é exibida em seu novo local.

## Edição de tags {#editing-tags}

Para editar o título da tag, selecione-a e clique em `Edit`. Especifique o novo título e clique em `Save`.

>[!NOTE]
>
>* O `Name` de uma tag não pode ser atualizado. O caminho raiz de uma tag também se baseia no nome da tag. O caminho permanece o mesmo se você atualizar o campo `Title`.
>* Operações adicionais como mesclar, localizar e publicar estão disponíveis na visualização de Admin.

## Exclusão de tags {#deleting-tags}

É possível excluir vários namespaces ou tags simultaneamente. A operação de exclusão não pode ser desfeita.

Execute as seguintes etapas para excluir tags:

1. Selecione o namespace ou a tag e clique em `Delete`.
1. Clique em `Confirm`.

>[!NOTE]
>
>* A exclusão da tag principal ou do namespace também exclui as subtags armazenadas na hierarquia. Se precisar excluir ou atualizar o namespace principal, é recomendável [mover as tags](#moving-tags) para o novo destino antes de excluir a hierarquia principal.
>* A exclusão de uma tag também exclui todas as suas referências dos ativos.
>* Não é possível excluir tags padrão existentes no nível raiz.

## Adicionar o componente de tags ao formulário de metadados {#adding-tags-to-metadata-form}

O componente de tags é adicionado ao formulário de metadados `default` automaticamente. Você pode criar um [formulário de metadados](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/metadata.html?lang=br#metadata-forms) do zero ou utilizar um modelo. Se você não estiver usando um modelo de formulário de metadados existente, poderá modificar o formulário de metadados e adicionar o componente de tags. O mapeamento da propriedade de metadados é preenchido automaticamente e não pode ser modificado neste momento. Usuários na visualização de Admin podem atualizar o mapeamento para armazenar valores de tag usando namespaces personalizados e expor apenas subconjuntos de hierarquias usando caminhos raiz.

Assista a este vídeo rápido para ver como adicionar o componente de tags ao formulário de metadados:

>[!VIDEO](https://video.tv.adobe.com/v/3420452)


### Adicionar tags a ativos {#adding-tags-to-assets}

1. Acesse a página Detalhes do ativo e navegue até a seção `Tags` do formulário de metadados.
1. Selecione o ícone do seletor de tags, ao lado do campo Tags, ou comece a digitar um nome de tag para ver os resultados sugeridos.

   ![Marcação de ativos](assets/adding-tags-to-assets.png)

1. Selecione uma ou mais tags. A subtag é selecionada automaticamente junto com a tag principal ou o namespace.
As tags modificadas na visualização do Assets também são aplicadas na visualização de Admin.

## Limitações {#limitations}

No momento, os seguintes recursos avançados de taxonomia não estão disponíveis na visualização do Assets e só podem ser acessados por meio da visualização de Admin:

* **Localização:** qualquer localização deve ocorrer na visualização de Admin.
* **Caminho raiz:** os caminhos raiz não podem ser configurados. Todos os namespaces armazenados no gerenciamento de taxonomia são expostos na propriedade Tags da visualização do Assets.
* **Tags padrão:** as tags padrão aplicadas na visualização de Admin estão visíveis na visualização do Assets. Não é possível adicionar novas tags padrão na visualização do Assets por meio da página Detalhes do ativo. Os valores existentes armazenados nas tags padrão são aplicados na página Detalhes do ativo.
* **Namespaces personalizados:** as tags não podem ser mapeadas para namespaces personalizados.
* **Exibição de referências:** admins podem ver o uso da tag na visualização do Assets. Todos os ativos que estão usando ativamente uma tag são informados. No entanto, admins não podem ver ativos individuais usando a tag das referências.

<!--
*   Overview
*   Benefits
*   Prerequisites and Permissions
*   Configuration
*   Managing Tags
    *   Creating a Namespace
    *   Adding Tags to a Namespace
    *   Adding Tags to Standard Tags
    *   Moving Tags
    *   Editing Tags
    *   Deleting Tags
*   Applying Tags
    *   Adding Tags to the Metadata form
    *   Adding Tags to Assets
*   Limitations
-->
