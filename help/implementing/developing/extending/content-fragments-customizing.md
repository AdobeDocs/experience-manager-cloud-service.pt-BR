---
title: Personalização e extensão de fragmentos de conteúdo
description: Um fragmento de conteúdo estende um ativo padrão.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 3%

---

# Personalização e extensão de fragmentos de conteúdo{#customizing-and-extending-content-fragments}

No Adobe Experience Manager as a Cloud Service, um fragmento de conteúdo estende um ativo padrão; consulte:

* [Criação e gerenciamento de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments.md) e [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md) para obter mais informações sobre fragmentos de conteúdo.

* [Gerenciamento de ativos](/help/assets/manage-digital-assets.md) para obter mais informações sobre ativos padrão.

## Arquitetura {#architecture}

A base [partes componentes](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de um fragmento de conteúdo são:

* A *Fragmento do conteúdo*,
* constituído por um ou mais *Elementos de conteúdo*,
* e que podem ter um ou mais *Variações de conteúdo*.

Os fragmentos de conteúdo individuais são baseados em modelos de fragmento de conteúdo:

* Os modelos de fragmento de conteúdo definem a estrutura de um fragmento de conteúdo quando ele é criado.
* Um fragmento faz referência ao modelo; portanto, as alterações no modelo podem/afetarão qualquer fragmento dependente.
* Os modelos são compostos de tipos de dados.
* As funções para adicionar novas variações etc. precisam atualizar o fragmento de acordo.

  >[!NOTE]
  >
  >Para exibir/renderizar um fragmento de conteúdo, sua conta deve ter `read` para o modelo.

  >[!CAUTION]
  >
  >Qualquer alteração em um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes; isso pode levar a propriedades órfãs nesses fragmentos.

### Integração do Sites com o Assets {#integration-of-sites-with-assets}

O Gerenciamento de fragmentos de conteúdo (CFM) faz parte do AEM Assets como:

* Fragmentos de conteúdo são ativos.
* Eles usam a funcionalidade existente do Assets.
* Eles são totalmente integrados ao Assets (consoles de administração etc.).

Os fragmentos de conteúdo são considerados um recurso do Sites, pois:

* Elas são usadas ao criar suas páginas.

#### Mapeamento de fragmentos de conteúdo para ativos {#mapping-content-fragments-to-assets}

![fragmento de conteúdo para ativos](assets/content-fragment-to-assets.png)

Os fragmentos de conteúdo, com base em um modelo de fragmento de conteúdo, são mapeados para um único ativo:

* Todo o conteúdo é armazenado no `jcr:content/data` nó do ativo:

   * Os dados do elemento são armazenados no subnó principal:
     `jcr:content/data/master`

   * As variações são armazenadas em um subnó que carrega o nome da variação: por exemplo, `jcr:content/data/myvariation`

   * Os dados de cada elemento são armazenados no respectivo subnó como uma propriedade com o nome do elemento: por exemplo, o conteúdo do elemento `text` é armazenado como propriedade `text` em `jcr:content/data/master`

* Os metadados e o conteúdo associado são armazenados abaixo `jcr:content/metadata`
Exceto o título e a descrição, que não são considerados metadados tradicionais e armazenados em `jcr:content`

#### Localização do ativo {#asset-location}

Assim como com os ativos padrão, um fragmento de conteúdo é mantido em:

`/content/dam`

#### Permissões de ativos {#asset-permissions}

Para obter mais detalhes, consulte [Fragmento do conteúdo - excluir considerações](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### Integração de recursos {#feature-integration}

Para integrar ao Assets principal:

* O recurso de Gerenciamento de fragmento de conteúdo (CFM) tem como base o núcleo de Ativos.

* O CFM fornece suas próprias implementações para itens nas exibições de cartão/coluna/lista; elas se conectam às implementações de renderização de conteúdo existentes do Assets.

* Vários componentes do Assets foram estendidos para atender a fragmentos de conteúdo.

### Uso de fragmentos de conteúdo em páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>A variável [O componente Fragmento de conteúdo faz parte dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR). Consulte [Desenvolvimento dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) para obter mais detalhes.

Os fragmentos de conteúdo podem ser referenciados a partir de páginas AEM, como qualquer outro tipo de ativo. O AEM fornece a **[Componente principal do Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)** - a [componente que permite incluir fragmentos de conteúdo nas páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Também é possível estender isso **[Fragmento do conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** componente principal.

* O componente usa o `fragmentPath` para fazer referência ao fragmento de conteúdo real. A variável `fragmentPath` A propriedade é tratada da mesma forma que as propriedades semelhantes de outros tipos de ativos; por exemplo, quando o fragmento de conteúdo é movido para outro local.

* O componente permite selecionar a variação a ser exibida.

* Além disso, um intervalo de parágrafos pode ser selecionado para restringir a saída; por exemplo, isso pode ser usado para saída de várias colunas.

* O componente permite conteúdo intermediário:

   * Aqui, o componente permite colocar outros ativos (imagens etc.) entre os parágrafos do fragmento referenciado.

   * Para conteúdo intermediário, é necessário:

      * esteja ciente da possibilidade de referências instáveis; o conteúdo intermediário (adicionado ao criar uma página) não tem relação fixa com o parágrafo ao lado do qual está posicionado, inserindo um novo parágrafo (no editor de fragmento de conteúdo) antes que a posição do conteúdo intermediário possa perder a posição relativa

      * considere os parâmetros adicionais (como variação e filtros de parágrafo) para configurar o que é renderizado na página

>[!NOTE]
>
>**Modelo de fragmentos do conteúdo:**
>
>Quando um fragmento de conteúdo é usado em uma página, o modelo de fragmento de conteúdo no qual ele se baseia é referenciado.
>
>Isso significa que, se o modelo não tiver sido publicado no momento da publicação da página, ele será sinalizado e o modelo será adicionado aos recursos a serem publicados com a página.

### Integração com outras estruturas {#integration-with-other-frameworks}

Os fragmentos de conteúdo podem ser integrados a:

* **Traduções**

  Os fragmentos de conteúdo são totalmente integrados ao [Fluxo de trabalho de tradução do AEM](/help/sites-cloud/administering/translation/overview.md). Em um nível arquitetônico, isso significa:

   * As traduções individuais de um fragmento de conteúdo são fragmentos separados; por exemplo:

      * eles estão localizados em raízes de idioma diferentes, mas compartilham exatamente o mesmo caminho relativo abaixo da raiz de idioma relevante:

        `/content/dam/<path>/en/<to>/<fragment>`

        vs.

        `/content/dam/<path>/de/<to>/<fragment>`

   * Além dos caminhos com base em regras, não há mais conexão entre as diferentes versões de idioma de um fragmento de conteúdo; elas são tratadas como dois fragmentos separados, embora a interface forneça os meios para navegar entre as variantes de idioma.

  >[!NOTE]
  >
  >O fluxo de trabalho de tradução do AEM funciona com `/content`:
  >
  >* Como os modelos de fragmento de conteúdo residem no `/conf`, elas não estão incluídas em tais traduções. É possível internacionalizar as strings da interface do usuário.

* **Esquemas de metadados**

   * Fragmentos de conteúdo (re)usam o [esquemas de metadados](/help/assets/metadata-schemas.md), que pode ser definido com ativos padrão.

   * O CFM fornece seu próprio esquema específico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     isso pode ser estendido, se necessário.

   * O respectivo formulário de esquema é integrado ao editor de fragmentos.

## A API de gerenciamento de fragmentos de conteúdo — lado do servidor {#the-content-fragment-management-api-server-side}

Você pode usar a API do lado do servidor para acessar os fragmentos de conteúdo; consulte:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>É altamente recomendável usar a API do lado do servidor em vez de acessar diretamente a estrutura de conteúdo.

### Interfaces principais {#key-interfaces}

As três interfaces a seguir podem servir como pontos de entrada:

* **Fragmento do conteúdo** ([FragmentoConteúdo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Essa interface permite trabalhar com um fragmento de conteúdo de forma abstrata.

  A interface fornece os meios para:

   * Gerenciar dados básicos (por exemplo, obter nome; obter/definir título/descrição)
   * Acessar metadados
   * Acessar elementos:

      * Listar elementos
      * Obter elementos por nome
      * Criar novos elementos (consulte [Avisos](#caveats))

      * Acessar dados do elemento (consulte `ContentElement`)

   * Variações de lista definidas para o fragmento
   * Criar novas variações globalmente
   * Gerenciar conteúdo associado:

      * Listar coleções
      * Adicionar coleções
      * Remover coleções

   * Acessar o modelo do fragmento

  As interfaces que representam os elementos principais de um fragmento são:

   * **Elemento do conteúdo** ([ElementoConteúdo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Acessar variações de um elemento:

         * Variações de lista
         * Obter variações por nome
         * Criar novas variações (consulte [Avisos](#caveats))
         * Remover variações (consulte [Avisos](#caveats))
         * Acessar dados de variação (consulte `ContentVariation`)

      * Atalho para resolver variações (aplicar alguma lógica de fallback adicional específica de implementação se a variação especificada não estiver disponível para um elemento)

   * **Variação de conteúdo** ([VariaçãoDeConteúdo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Sincronização simples, com base nas informações da última modificação

  Todas as três interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) estender o `Versionable` , que adiciona recursos de controle de versão, necessários para fragmentos de conteúdo:

   * Criar nova versão do elemento
   * Listar versões do elemento
   * Obter o conteúdo de uma versão específica do elemento com versão

### Adaptação - Uso de adaptTo() {#adapting-using-adaptto}

Os seguintes podem ser adaptados:

* `ContentFragment` pode ser adaptada a:

   * `Resource` - o recurso Sling subjacente; atualizando o subjacente `Resource` exige diretamente a reconstrução do `ContentFragment` objeto.

   * `Asset` - o DAM `Asset` abstração que representa o fragmento de conteúdo; atualizando o `Asset` exige diretamente a reconstrução do `ContentFragment` objeto.

* `ContentElement` pode ser adaptada a:

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para acessar as informações estruturais do elemento.

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` pode ser adaptada a:

   * `ContentFragment`

### Avisos {#caveats}

É de notar que:

* A API inteira foi projetada para **não** manter as alterações automaticamente (a menos que indicado de outra forma no JavaDoc da API). Portanto, sempre é necessário confirmar o resolvedor de recursos da respectiva solicitação (ou o resolvedor que você está usando na verdade).

* Tarefas que podem exigir esforço adicional:

   * É altamente recomendável criar novas variações de `ContentFragment`. Isso garante que todos os elementos compartilhem essa variação e que as estruturas de dados globais apropriadas sejam atualizadas conforme necessário para refletir a variação recém-criada na estrutura de conteúdo.

   * Remoção de variações existentes por meio de um elemento, usando `ContentElement.removeVariation()`, não atualizará as estruturas de dados globais atribuídas à variação. Para garantir que essas estruturas de dados sejam mantidas em sincronia, use `ContentFragment.removeVariation()` em vez disso, o que remove uma variação globalmente.

## A API de gerenciamento de fragmentos de conteúdo - Lado do cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>A API do lado do cliente é interna.

### Informações adicionais {#additional-information}

Consulte o link a seguir:

* `filter.xml`

  A variável `filter.xml` para o gerenciamento de fragmentos de conteúdo é configurado de modo que não se sobreponha ao pacote de conteúdo principal do Assets.

## Editar sessões {#edit-sessions}

>[!CAUTION]
>
>Considere estas informações de referência. Você não deve alterar nada aqui (pois está marcado como um *área privada* no repositório), mas pode ajudar em alguns casos a entender como as coisas funcionam por baixo dos panos.

A edição de um fragmento de conteúdo, que pode abranger várias visualizações (= páginas de HTML), é atômica. Como esses recursos atômicos de edição de várias visualizações não são um conceito típico de AEM, os fragmentos de conteúdo usam o que é chamado de *editando sessão*.

Uma sessão de edição é iniciada quando o usuário abre um fragmento de conteúdo no editor. A sessão de edição é concluída quando o usuário deixa o editor selecionando **Salvar** ou **Cancelar**.

Tecnicamente, todas as edições são feitas em *live* conteúdo, assim como em todas as outras edições de AEM. Quando a sessão de edição for iniciada, uma versão do status atual e não editado será criada. Se um usuário cancelar uma edição, essa versão será restaurada. Se o usuário clicar em **Salvar**, nada específico é feito, pois toda a edição foi executada em *live* conteúdo, portanto, todas as alterações já são persistentes. Além disso, ao clicar em **Salvar** acionará algum processamento em segundo plano (como a criação de informações de pesquisa de texto completo e/ou o manuseio de ativos de mídia mista).

Existem algumas medidas de segurança para casos de borda; por exemplo, se o usuário tentar sair do editor sem salvar ou cancelar a sessão de edição. Além disso, um salvamento automático periódico está disponível para evitar perda de dados.
Observe que dois usuários podem editar o mesmo fragmento de conteúdo simultaneamente e, portanto, podem substituir as alterações um do outro. Para evitar que isso aconteça, o fragmento de conteúdo precisa ser bloqueado aplicando a regra do DAM *Check-out* ação no fragmento.

## Exemplos {#examples}

### Exemplo: acesso a um fragmento de conteúdo existente {#example-accessing-an-existing-content-fragment}

Para isso, você pode adaptar o recurso que representa a API a:

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

Para criar um novo fragmento de conteúdo de forma programática, é necessário usar um
`FragmentTemplate` adaptado de um recurso de modelo.

Por exemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemplo: Especificação do intervalo de salvamento automático {#example-specifying-the-auto-save-interval}

A variável [intervalo de salvamento automático](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) (medido em segundos) pode ser definido usando o gerenciador de configurações (ConfMgr):

* Nó: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`
* Tipo: `Long`

* Padrão: `600` (10 minutos); está definido em `/libs/settings/dam/cfm/jcr:content`

Se você quiser definir um intervalo de salvamento automático de 5 minutos, será necessário definir a propriedade no nó; por exemplo:

* Nó: `/conf/global/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes para criação de página {#components-for-page-authoring}

Para obter mais informações, consulte

* [Componentes principais - Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR) (recomendado)
