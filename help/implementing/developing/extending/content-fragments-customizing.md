---
title: Personalização e extensão de fragmentos de conteúdo
description: Um fragmento de conteúdo estende um ativo padrão.
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7

---


# Personalização e extensão de fragmentos de conteúdo{#customizing-and-extending-content-fragments}

No Adobe Experience Manager como um serviço em nuvem, um fragmento de conteúdo estende um ativo padrão; consulte:

* [Criação e gerenciamento de fragmentos](/help/assets/content-fragments/content-fragments.md) de conteúdo e criação de [páginas com fragmentos](/help/sites-cloud/authoring/fundamentals/content-fragments.md) de conteúdo para obter mais informações sobre fragmentos de conteúdo.

* [Gerenciamento de ativos](/help/assets/manage-digital-assets.md) e [personalização e extensão do Editor](/help/assets/extend-asset-editor.md) de ativos para obter mais informações sobre ativos padrão.

## Arquitetura {#architecture}

As partes [](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) constituintes básicas de um fragmento de conteúdo são:

* Um fragmento *do conteúdo*,
* consistindo em um ou mais elementos *de conteúdo*,
* e que podem ter uma ou mais Variações *de* conteúdo.

Dependendo do tipo de fragmento, os modelos ou o modelo de Fragmento **** simples também são usados:

>[!CAUTION]
>
>[Modelos](/help/assets/content-fragments/content-fragments-models.md) de fragmento de conteúdo agora são recomendados para a criação de todos os fragmentos.
>
>Os modelos de fragmento de conteúdo são usados para todos os exemplos no WKND.

* Modelos de fragmentos do conteúdo:

   * Usado para definir fragmentos de conteúdo que contêm conteúdo estruturado.
   * Os modelos de fragmento de conteúdo definem a estrutura de um fragmento de conteúdo quando ele é criado.
   * Um fragmento faz referência ao modelo; portanto, as alterações no modelo podem/afetarão quaisquer fragmentos dependentes.
   * Os modelos são construídos de tipos de dados.
   * As funções para adicionar novas variações, etc., precisam atualizar o fragmento de acordo.
   >[!NOTE]
   >
   >Para que você exiba/renderize um Fragmento de conteúdo, sua conta deve ter `read` permissões para o modelo.

   >[!CAUTION]
   >
   >Quaisquer alterações em um modelo de fragmento de conteúdo existente podem afetar fragmentos dependentes; isso pode levar a propriedades órfãs nesses fragmentos.

* Modelo de fragmento de conteúdo - Fragmento **simples**:

   * Usado para definir fragmentos de conteúdo simples.

   * Esse modelo define a estrutura (básica, somente texto) de um fragmento de conteúdo quando ele é criado.

   * O modelo é copiado para o fragmento quando ele é criado.

   * As funções para adicionar novas variações, etc., precisam atualizar o fragmento de acordo.

   * O modelo de fragmento de conteúdo (Fragmento **** simples) opera de maneira diferente da de outros mecanismos de formatação no ecossistema do AEM (por exemplo, modelos de página, etc.). Por conseguinte, deve ser considerada separadamente.

   * Quando baseado no modelo de Fragmento **** simples, o tipo MIME do conteúdo é gerenciado no conteúdo real; isso significa que cada elemento e variação pode ter um tipo MIME diferente.

### Integração de sites com ativos {#integration-of-sites-with-assets}

O Gerenciamento de fragmentos de conteúdo (CFM) faz parte dos ativos AEM como:

* Fragmentos de conteúdo são ativos.
* Eles usam a funcionalidade Ativos existente.
* Eles são totalmente integrados aos Ativos (consoles de administrador etc.).

Fragmentos de conteúdo são considerados um recurso Sites como:

* Elas são usadas ao criar suas páginas.

#### Mapeamento de fragmentos de conteúdo estruturados para ativos {#mapping-structured-content-fragments-to-assets}

![fragmento de conteúdo em ativos estruturados](assets/content-fragment-to-assets-structured.png)

Fragmentos de conteúdo com conteúdo estruturado (isto é, com base em um modelo de fragmento de conteúdo) são mapeados para um único ativo:

* Todo o conteúdo é armazenado no `jcr:content/data` nó do ativo:

   * Os dados do elemento são armazenados sob o subnó mestre:
      `jcr:content/data/master`

   * As variações são armazenadas em um subnó que contém o nome da variação:
por exemplo, `jcr:content/data/myvariation`

   * Os dados de cada elemento são armazenados no respectivo subnó como uma propriedade com o nome do elemento:
Por exemplo, o conteúdo do elemento `text` é armazenado como propriedade `text` em `jcr:content/data/master`

* Os metadados e o conteúdo associado são armazenados abaixo, `jcr:content/metadata`exceto o título e a descrição, que não são considerados metadados tradicionais e armazenados em `jcr:content`

#### Mapeamento de fragmentos de conteúdo simples para ativos {#mapping-simple-content-fragments-to-assets}

![fragmento de conteúdo para ativos simples](assets/content-fragment-to-assets-simple.png)

Fragmentos de conteúdo simples (com base no modelo de Fragmento **simples** ) são mapeados para um composto composto que consiste em um ativo principal e subativos (opcionais):

* Todas as informações de não conteúdo de um fragmento (como título, descrição, metadados, estrutura) são gerenciadas exclusivamente no ativo principal.
* O conteúdo do primeiro elemento de um fragmento é mapeado para a representação original do ativo principal.

   * As variações (se houver) do primeiro elemento são mapeadas para outras representações do ativo principal.

* Elementos adicionais (se existentes) são mapeados para subativos do ativo principal.

   * O conteúdo principal desses elementos adicionais mapeia para a representação original do respectivo subativo.
   * Outras variações (se aplicável) de quaisquer elementos adicionais mapeiam outras representações do respectivo subativo.

#### Local do ativo {#asset-location}

Como ocorre com os ativos padrão, um fragmento de conteúdo é mantido em:

`/content/dam`

#### Permissões de ativos {#asset-permissions}

Para obter mais detalhes, consulte Fragmento [do conteúdo - Excluir considerações](/help/assets/content-fragments/content-fragments-delete.md).

#### Integração de recursos {#feature-integration}

Para integrar com o núcleo Ativos:

* O recurso de Gerenciamento de fragmento de conteúdo (CFM) baseia-se no núcleo Ativos.

* O CFM fornece suas próprias implementações para itens nas visualizações de cartão/coluna/lista; eles são conectados às implementações existentes de renderização de conteúdo dos Ativos.

* Vários componentes do Assets foram estendidos para atender a fragmentos de conteúdo.

### Uso de fragmentos de conteúdo em páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>O componente Fragmento [do conteúdo faz parte dos Componentes](https://docs.adobe.com/content/help/pt/experience-manager-core-components/using/components/content-fragment-component.html)principais. Consulte [Desenvolvimento de componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) principais para obter mais detalhes.

Os fragmentos de conteúdo podem ser referenciados em páginas AEM, assim como qualquer outro tipo de ativo. O AEM fornece o componente **[principal do Fragmento](https://docs.adobe.com/content/help/pt/experience-manager-core-components/using/components/content-fragment-component.html)**de conteúdo - um[componente que permite incluir fragmentos de conteúdo em suas páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Você também pode estender esse componente principal do Fragmento**[](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** de conteúdo.

* O componente usa a `fragmentPath` propriedade para fazer referência ao fragmento de conteúdo real. A `fragmentPath` propriedade é tratada da mesma forma que as propriedades semelhantes de outros tipos de ativos; por exemplo, quando o fragmento de conteúdo é movido para outro local.

* O componente permite selecionar a variação a ser exibida.

* Além disso, um intervalo de parágrafos pode ser selecionado para restringir a saída; por exemplo, isso pode ser usado para saída de várias colunas.

* O componente permite conteúdo intermediário:

   * Aqui, o componente permite que você coloque outros ativos (imagens, etc.) entre os parágrafos do fragmento referenciado.

   * Para conteúdo intermediário, é necessário:

      * Estar ciente da possibilidade de referências instáveis; o conteúdo intermediário (adicionado ao criar uma página) não tem relação fixa com o parágrafo ao lado do qual está posicionado, inserindo um novo parágrafo (no editor de fragmentos de conteúdo) antes que a posição do conteúdo intermediário possa perder a posição relativa

      * considere os parâmetros adicionais (como filtros de variação e parágrafo) para configurar o que é renderizado na página

>[!NOTE]
>
>**Modelo de fragmentos do conteúdo:**
>
>Ao usar um fragmento de conteúdo que tenha sido baseado em um modelo de fragmento de conteúdo em uma página, o modelo é referenciado. Isso significa que, se o modelo não tiver sido publicado no momento em que você publicar a página, ele será sinalizado e o modelo será adicionado aos recursos a serem publicados com a página.
>
>**Modelo de fragmento de conteúdo - Fragmento simples:**
>
>Ao usar um fragmento de conteúdo que tenha sido baseado no modelo de fragmento de conteúdo Fragmento **simples** em uma página, não há referência, pois o modelo foi copiado ao criar o fragmento.

### Integração com outros quadros {#integration-with-other-frameworks}

Os fragmentos de conteúdo podem ser integrados com:

* **Traduções**

   Fragmentos de conteúdo são totalmente integrados ao fluxo de trabalho de tradução do AEM. Em nível arquitetônico, isso significa:

   * As traduções individuais de um fragmento de conteúdo são, na verdade, fragmentos separados; por exemplo:

      * Estejam localizados sob raízes linguísticas diferentes; mas compartilham exatamente o mesmo caminho relativo abaixo da raiz do idioma relevante:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Além dos caminhos baseados em regras, não há mais conexão entre as diferentes versões linguísticas de um fragmento de conteúdo; são manipulados como dois fragmentos separados, embora a interface do usuário forneça os meios de navegação entre as variantes de idioma.
   >[!NOTE]
   >
   >O fluxo de trabalho de tradução do AEM funciona com `/content`:
   >
   >* Como os modelos de fragmento de conteúdo residem em `/conf`, eles não são incluídos nessas traduções. Você pode internacionalizar as strings da interface do usuário.


* **Esquemas de metadados**

   * Os fragmentos de conteúdo (re)usam os schemas [de](/help/assets/metadata-schemas.md)metadados, que podem ser definidos com ativos padrão.

   * O CFM fornece seu próprio schema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      isso pode ser estendido se necessário.

   * O respectivo formulário de schema é integrado ao editor de fragmentos.

## A API de gerenciamento de fragmentos de conteúdo - lado do servidor {#the-content-fragment-management-api-server-side}

Você pode usar a API do lado do servidor para acessar seus fragmentos de conteúdo; consulte:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/package-frame.html)

>[!CAUTION]
>
>É altamente recomendável usar a API do lado do servidor em vez de acessar diretamente a estrutura de conteúdo.

### Interfaces principais {#key-interfaces}

As três interfaces a seguir podem servir como pontos de entrada:

* **Fragmento** do conteúdo ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Essa interface permite que você trabalhe com um fragmento de conteúdo de forma abstrata.

   A interface fornece os meios para:

   * Gerenciar dados básicos (por exemplo, obter nome; get/set título/descrição)
   * Acessar metadados
   * Elementos de acesso:

      * Elementos de Lista
      * Obter elementos por nome
      * Criar novos elementos (consulte [Avisos](#caveats))

      * Dados do elemento de acesso (consulte `ContentElement`)
   * variações de Lista definidas para o fragmento
   * Criar novas variações globalmente
   * Gerenciar conteúdo associado:

      * Coleções de Lista
      * Adicionar coleções
      * Remover coleções
   * Acessar o modelo ou modelo do fragmento
   As interfaces que representam os principais elementos de um fragmento são:

   * **Elemento** de conteúdo ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Variações de acesso de um elemento:

         * variações de Lista
         * Obter variações por nome
         * Criar novas variações (consulte [Avisos](#caveats))
         * Remover variações (consulte [Avisos](#caveats))
         * Dados de variação de acesso (consulte `ContentVariation`)
      * Atalho para resolver variações (aplicando alguma lógica de fallback adicional e específica da implementação se a variação especificada não estiver disponível para um elemento)
   * **Variação** de conteúdo ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Sincronização simples, com base nas últimas informações modificadas
   Todas as três interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation``Versionable` ) estendem a interface, que adiciona recursos de controle de versão, necessários para fragmentos de conteúdo:

   * Criar nova versão do elemento
   * Versões de Lista do elemento
   * Obter o conteúdo de uma versão específica do elemento com versão







### Adaptando - usando adaptTo() {#adapting-using-adaptto}

Podem ser adaptados:

* `ContentFragment` pode ser adaptado para:

   * `Resource` - o recurso Sling subjacente; atualizar o subjacente `Resource` diretamente requer a reconstrução do `ContentFragment` objeto.

   * `Asset` - a `Asset` abstração DAM que representa o fragmento do conteúdo; atualizar o objeto `Asset` diretamente requer a reconstrução do `ContentFragment` objeto.

* `ContentElement` pode ser adaptado para:

   * `ElementTemplate` - para aceder às informações estruturais do elemento.

* `Resource` pode ser adaptado para:

   * `ContentFragment`

### Avisos {#caveats}

Note-se que:

* A API inteira foi projetada para **não** persistir as alterações automaticamente (a menos que seja observado de outra forma no JavaDoc da API). Portanto, você sempre terá que confirmar o resolvedor de recursos da respectiva solicitação (ou o resolvedor que você está usando).

* Tarefas que podem exigir esforço adicional:

   * Crie novas variações de `ContentFragment` para atualizar a estrutura de dados.

   * A remoção de variações existentes por meio de um elemento, usando `ContentElement.removeVariation()`, não atualizará as estruturas de dados globais atribuídas à variação. Para garantir que essas estruturas de dados sejam mantidas sincronizadas, use `ContentFragment.removeVariation()` , que remove uma variação globalmente.

## A API de gerenciamento de fragmentos de conteúdo - lado do cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>A API do cliente é interna.

### Informações adicionais {#additional-information}

Consulte o link a seguir:

* `filter.xml`

   O gerenciamento de fragmentos do conteúdo `filter.xml` para o conteúdo é configurado de modo que não se sobreponha ao pacote de conteúdo principal dos Ativos.

## Editar sessões {#edit-sessions}

>[!CAUTION]
>
>Considere estas informações de fundo. Você não deve mudar nada aqui (pois está marcado como uma área ** privada no repositório), mas isso pode ajudar em alguns casos a entender como as coisas funcionam debaixo do capô.

A edição de um fragmento de conteúdo, que pode abranger várias visualizações (= páginas HTML), é atômica. Como esses recursos atômicos de edição de várias visualizações não são um conceito típico do AEM, os fragmentos de conteúdo usam o que é chamado de sessão *de* edição.

Uma sessão de edição é iniciada quando o usuário abre um fragmento de conteúdo no editor. A sessão de edição é concluída quando o usuário sai do editor selecionando **Salvar** ou **Cancelar**.

Tecnicamente, todas as edições são feitas em conteúdo *ativo* , assim como em todas as outras edições do AEM. Quando a sessão de edição é iniciada, uma versão do status atual não editado é criada. Se um usuário cancelar uma edição, essa versão será restaurada. Se o usuário clicar em **Salvar**, nada específico será feito, pois toda a edição foi executada em conteúdo *ativo* , portanto, todas as alterações já são mantidas. Além disso, clicar em **Salvar** acionará algum processamento em segundo plano (como criar informações de pesquisa de texto completo e/ou manipular ativos de mídia mista).

Existem algumas medidas de segurança para casos de borda; por exemplo, se o usuário tentar sair do editor sem salvar ou cancelar a sessão de edição. Além disso, um salvamento automático periódico está disponível para evitar perda de dados.
Observe que dois usuários podem editar o mesmo fragmento de conteúdo ao mesmo tempo e, portanto, podem substituir as alterações entre si. Para evitar isso, o fragmento de conteúdo precisa ser bloqueado aplicando a ação de *Check-out* da administração do DAM no fragmento.

## Exemplos {#examples}

### Exemplo: Acessar um fragmento de conteúdo existente {#example-accessing-an-existing-content-fragment}

Para conseguir isso, você pode adaptar o recurso que representa a API para:

`com.adobe.cq.dam.cfm.ContentFragment`

Por exemplo:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Exemplo: Criação de um novo fragmento de conteúdo {#example-creating-a-new-content-fragment}

Para criar um novo fragmento de conteúdo programaticamente, é necessário usar um`FragmentTemplate` adaptado de um modelo ou recurso de modelo.

Por exemplo:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemplo: Especificação do intervalo de salvamento automático {#example-specifying-the-auto-save-interval}

O intervalo [de salvamento](/help/assets/content-fragments/content-fragments-managing.md#save-cancel-and-versions) automático (medido em segundos) pode ser definido usando o gerenciador de configuração (ConfMgr):

* Nó: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`
* Tipo: `Long`

* Padrão: `600` (10 minutos); isso é definido em `/libs/settings/dam/cfm/jcr:content`

Se você quiser definir um intervalo de salvamento automático de 5 minutos, é necessário definir a propriedade no nó; por exemplo:

* Nó: `/conf/global/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes da autoria de página {#components-for-page-authoring}

Para obter mais informações, consulte

* [Componentes principais - Componente](https://docs.adobe.com/content/help/pt/experience-manager-core-components/using/components/content-fragment-component.html) de fragmento do conteúdo (recomendado)
