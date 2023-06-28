---
title: Como gerenciar tags na visualização de Ativos?
description: Saiba como gerenciar tags na visualização de Ativos. As tags ajudam a categorizar ativos que podem ser navegados e pesquisados com mais eficiência.
source-git-commit: bdbe47a8f06d2ec1cd75103905677fcd3955632d
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Gerenciar tags na exibição do Assets {#view-assets-and-details}


>[!CONTEXTUALHELP]
>id="assets_taxonomy_management"
>title="Gerenciar tags"
>abstract="As tags ajudam a categorizar ativos que podem ser navegados e pesquisados com mais eficiência. Os administradores têm a capacidade de usar a estrutura hierárquica de marcação, que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante."

As tags ajudam a categorizar ativos que podem ser navegados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e workflows.

Listas planas de vocabulários controlados podem se tornar incontroláveis com o tempo. Os administradores têm a capacidade de usar a estrutura hierárquica de marcação, que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante.

Você pode criar um namespace no nível raiz e criar uma estrutura hierárquica de subtags no namespace. Por exemplo, você pode criar um `Activities` namespace no nível raiz e têm `Cycling`, `Hiking`, e `Running` no namespace. É possível ter mais subtags `Clothing` e `Shoes` no prazo de `Running`.

![Gerenciamento de tags](assets/tags-hierarchy.png)

A marcação oferece muitos benefícios, como:

* A marcação permite que os autores organizem facilmente ativos diferentes por meio de uma taxonomia comum. Os autores podem pesquisar e organizar ativos rapidamente por tags comuns.

* As tags hierárquicas são extremamente flexíveis e são uma excelente maneira de organizar termos de maneira lógica. Por meio de namespaces, tags e subtags, sistemas taxonômicos inteiros podem ser representados.

* As tags podem evoluir com o tempo, à medida que um vocabulário organizacional muda.

* As tags gerenciadas na exibição do administrador permanecem em sincronia com as tags gerenciadas na exibição do Assets, o que garante a governança e a integridade dos metadados.

Para poder aplicar tags a ativos, primeiro crie um namespace e depois crie e adicione tags a ele. Também é possível criar tags e adicioná-las a um namespace existente. Todas as tags criadas no nível raiz são automaticamente adicionadas ao namespace Tags padrão. Em seguida, é possível adicionar o campo Tags ao formulário de metadados para que ele seja exibido na página de detalhes do ativo. Depois de definir essas configurações, você pode começar a aplicar tags aos ativos.

>[!NOTE]
>
>Você precisa adicionar o campo Tags ao formulário de metadados somente se não estiver usando o formulário de metadados padrão.

![Gerenciamento de tags](assets/tagging-taxonomy-management.png)

Recursos adicionais além do que é mencionado neste artigo, incluindo mesclagem, renomeação, localização e publicação de tags, estão disponíveis na exibição de Administrador.

## Criação de um namespace {#creating-a-namespace}

Um namespace é um container para tags que só podem existir no nível raiz. Você pode começar a configurar a estrutura hierárquica de tags definindo primeiro um nome lógico para o Namespace. Se você não adicionar uma tag a nenhum dos Namespaces existentes, a tag será movida automaticamente para Tags padrão.

Execute as seguintes etapas para criar um Namespace:

1. Ir para `Taxonomy Management` em `Settings` para exibir a lista de Namespaces existentes. Você também pode visualizar a data da última modificação, o usuário que modificou o namespace ou as tags sob ele e o número de vezes que a tag é usada em um ativo.
1. Clique em `Create Namespace`.
1. Adicionar `Title`, `Name`, e `Description` para o Namespace. A entrada especificada na variável `Title` é exibido na parte superior da hierarquia. Por exemplo, na imagem a seguir, **Atividades** refere-se ao título do namespace.

   ![Gerenciamento de tags](assets/tags-hierarchy.png)

   <!--
    >[!NOTE]
    >
    >You can use `Name` as a primary key if you are using any other metadata management tool is the source of truth for taxonomy values, you can use the name as a primary key.
    >
    -->

1. Clique em `Save`.

## Adicionar tags a um namespace {#adding-tags-to-namespace}

Execute as seguintes etapas para adicionar tags a um namespace:

1. Ir para `Taxonomy Management`.
1. Selecione o namespace e clique em `Create` para criar a tag no nível superior no Namespace. Se precisar criar uma subtag em uma tag existente em um Namespace, selecione a tag e clique em `Create`.
   ![Hierarquia de tags](assets/hierarchy-of-tags.png)

   Neste exemplo, a imagem à esquerda representa a tag diretamente no Namespace `automobile-four-wheeler` exibido no `Path` campo. A imagem à direita é um exemplo de subtags adicionadas em uma tag, pois há mais nomes de tags, `jeep` e `jeep-meridian`, exibido no `Path` além do Namespace.
1. Especifique o título, nome e descrição da tag e clique em `Save`.


   >[!NOTE]
   >
   >* A variável `Title` e `Name` os campos são obrigatórios enquanto a variável `Description` é opcional.
   >* Por padrão, a ferramenta copia o texto digitado no campo Título, remove os espaços em branco ou caracteres especiais ( ). &amp; / \ : * ? [ ] | &quot; %), e armazena-o como o Nome.
   >* Você pode atualizar o `Title` posteriormente, mas a variável `Name` O campo é somente leitura.

## Adição de tags a tags padrão {#adding-tags-to-standard-tags}

Tags não estruturadas ou as tags que não têm hierarquia são armazenadas em `Standard Tags` namespace. Além disso, quando quiser adicionar termos descritivos adicionais sem afetar a taxonomia controlada, você poderá armazenar esse valor em `Standard Tags`. Você pode mover esses valores em namespaces estruturados ao longo do tempo. Além disso, você pode usar a variável `Standard Tags` namespace como uma entrada de formato livre para palavras-chave.

Para criar uma tag padrão, clique em `Create Tag` no nível raiz. Especifique o título, nome e descrição e clique em `Save`.

![Adição de tags a tags padrão](assets/adding-tags-to-standard-tags.png)

>[!NOTE]
>
>Se você excluir `Standard Tags` usando a visualização do Administrador, as tags criadas no nível raiz não são exibidas na lista de tags disponíveis.

## Mover tags {#moving-tags}

Caso armazene as tags na hierarquia errada ou suas alterações de taxonomia ao longo do tempo, você poderá mover as tags selecionadas para manter a integridade dos dados. As seguintes condições devem ser consideradas durante a movimentação das tags:

* As tags só podem ser movidas abaixo de namespaces existentes ou em uma hierarquia de tags existente.
* As tags não podem ser movidas para a raiz para se tornarem um namespace.
* Mover uma tag principal também move todas as tags secundárias armazenadas na hierarquia.

Execute as seguintes etapas para mover tags de um local para outro:

1. Selecione a tag ou toda a hierarquia de tags no namespace apropriado e clique em `Move`.
1. Na caixa de diálogo Mover, selecione a nova tag de destino ou Namespace usando o `Select Tag` seção.
1. Clique em `Save`. A tag é exibida em seu novo local.

## Edição de tags {#editing-tags}

Para editar o título da tag, selecione a tag e clique em `Edit`. Especifique o novo título e clique em `Save`.

>[!NOTE]
>
>* A variável `Name` de uma tag não pode ser atualizada. O caminho raiz de uma tag também se baseia no nome da tag. O caminho permanece o mesmo mesmo se você atualizar o `Title` campo.
>* Operações adicionais como mesclar, localizar e publicar estão disponíveis na exibição de Administração.

## Exclusão de tags {#deleting-tags}

É possível excluir vários namespaces ou tags simultaneamente. A operação de exclusão não pode ser desfeita.

Execute as seguintes etapas para excluir tags:

1. Selecione o namespace ou a tag e clique em `Delete`.
1. Clique em `Confirm`.

>[!NOTE]
>
>* A exclusão da tag principal ou Namespace também exclui as subtags armazenadas na hierarquia. Se precisar excluir ou atualizar o Namespace pai, é recomendável [mover suas tags](#moving-tags) ao novo destino antes de excluir a hierarquia pai.
>* A exclusão de uma tag também exclui todas as suas referências dos ativos.
>* Não é possível excluir Tags padrão existentes no nível raiz.

## Adicionar o componente de Tags ao formulário de Metadados {#adding-tags-to-metadata-form}

O componente de tags é adicionado à variável `default` formulário de metadados automaticamente. Você pode criar um [Formulário de metadados](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/metadata.html?lang=en#metadata-forms) usando um modelo ou do zero. Se você não estiver usando um modelo de formulário de Metadados existente, poderá modificar seu formulário de Metadados e adicionar o componente de Tags. O mapeamento da propriedade de metadados é preenchido automaticamente e não pode ser modificado neste momento. Os usuários na visualização Administração podem atualizar o mapeamento para armazenar valores de tag usando namespaces personalizados e expor apenas subconjuntos de hierarquias usando caminhos raiz.

Assista a este vídeo rápido para ver como adicionar o componente Tags ao seu formulário de metadados:

>[!VIDEO](https://video.tv.adobe.com/v/3420452)


### Adição de tags a ativos {#adding-tags-to-assets}

1. Acesse a página Detalhes do ativo e navegue até a `Tags` seção do formulário de Metadados.
1. Selecione o ícone do seletor de tags, ao lado do campo Tags, ou comece a digitar um nome de tag para ver os resultados sugeridos.

   ![Marcação de ativos](assets/adding-tags-to-assets.png)

1. Selecione uma ou mais tags. A subtag é selecionada automaticamente junto com a tag principal ou o namespace.
As tags modificadas na exibição Ativos também são aplicadas na exibição Administração.

## Limitações {#limitations}

No momento, os seguintes recursos avançados de taxonomia não estão disponíveis na exibição do Assets e só podem ser acessados por meio da exibição do Administrador:

* **Localização:** Qualquer localização deve ocorrer na exibição de Administração.
* **Caminho raiz:** Os caminhos raiz não podem ser configurados. Todos os namespaces armazenados no Gerenciamento de taxonomia são expostos na propriedade Tags na exibição Ativos.
* **Tags padrão:** As tags Padrão aplicadas na exibição de Administrador estão visíveis na exibição de Ativos. Não é possível adicionar novas tags padrão na exibição Ativos da página Detalhes do ativo. Os valores existentes armazenados nas Tags padrão são aplicados na página Detalhes do ativo.
* **Namespaces personalizados:** As marcas não podem ser mapeadas para namespaces personalizados.
* **Exibindo referências:** Os administradores podem ver o uso da tag na visualização de Ativos. Refere-se a todos os ativos que estão usando ativamente uma tag. No entanto, os administradores não podem ver ativos individuais usando a tag em referências.

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