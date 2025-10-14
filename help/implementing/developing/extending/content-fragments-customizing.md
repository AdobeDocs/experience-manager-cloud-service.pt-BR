---
title: Personalização e extensão de fragmentos de conteúdo
description: Um fragmento de conteúdo estende um ativo padrão. Saiba como personalizá-los.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 1%

---

# Personalização e extensão de fragmentos de conteúdo{#customizing-and-extending-content-fragments}

No Adobe Experience Manager as a Cloud Service, um fragmento de conteúdo estende um ativo padrão; consulte:

* [Criação e gerenciamento de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md) e [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md) para obter mais informações sobre fragmentos de conteúdo.

* [Gerenciando o Assets](/help/assets/manage-digital-assets.md) para obter mais informações sobre ativos padrão.

## Arquitetura {#architecture}

As [partes constituintes](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) básicas de um fragmento de conteúdo são as seguintes:

* Um *fragmento de conteúdo* em si
* Consiste em um ou mais *Elementos de Conteúdo*
* Ele pode ter uma ou mais *Variações de conteúdo*

Os fragmentos de conteúdo individuais são baseados em modelos de fragmento de conteúdo:

* Os modelos de fragmento de conteúdo definem a estrutura de um fragmento de conteúdo quando ele é criado.
* Um fragmento faz referência ao modelo; portanto, as alterações no modelo podem afetar ou afetar qualquer fragmento dependente.
* Os modelos são compostos de tipos de dados.
* As funções para adicionar novas variações, e assim por diante, precisam atualizar o fragmento de acordo.

  >[!NOTE]
  >
  >Para exibir/renderizar um Fragmento de conteúdo, sua conta deve ter `read` permissões para o modelo.

  >[!CAUTION]
  >
  >Qualquer alteração em um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes; isso pode levar a propriedades órfãs nesses fragmentos.

### Integração do Sites com o Assets {#integration-of-sites-with-assets}

O Gerenciamento de fragmentos de conteúdo (CFM) faz parte do Adobe Experience Manager (AEM) Assets como:

* Fragmentos de conteúdo são ativos.
* Eles usam a funcionalidade existente do Assets.
* Eles são totalmente integrados ao Assets (consoles de administração e assim por diante).

Os fragmentos de conteúdo são considerados um recurso do AEM Sites porque:

* Elas são usadas ao criar suas páginas.

#### Mapeamento de fragmentos de conteúdo para o Assets {#mapping-content-fragments-to-assets}

![fragmento de conteúdo para ativos](assets/content-fragment-to-assets.png)

Os fragmentos de conteúdo, com base em um modelo de fragmento de conteúdo, são mapeados para um único ativo:

* Todo o conteúdo é armazenado no nó `jcr:content/data` do ativo:

   * Os dados do elemento são armazenados no subnó principal:

     `jcr:content/data/master`

   * As variações são armazenadas em um subnó que carrega o nome da variação:
por exemplo, `jcr:content/data/myvariation`

   * Os dados de cada elemento são armazenados no respectivo subnó como uma propriedade com o nome do elemento:
por exemplo, o conteúdo do elemento `text` é armazenado como a propriedade `text` em `jcr:content/data/master`

* Os metadados e o conteúdo associado estão armazenados abaixo de `jcr:content/metadata`
Exceto o título e a descrição, que não são considerados metadados tradicionais e armazenados em `jcr:content`

#### Localização do ativo {#asset-location}

Assim como com os ativos padrão, um fragmento de conteúdo é mantido em:

`/content/dam`

#### Permissões de ativos {#asset-permissions}

Consulte [Fragmento do conteúdo - Excluir considerações](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### Integração de recursos {#feature-integration}

Para integrar com o Assets Core:

* O recurso de Gerenciamento de fragmento de conteúdo (CFM) tem como base o núcleo do Assets.

* O CFM fornece suas próprias implementações para itens nas visualizações de cartão/coluna/lista; elas se conectam às implementações de renderização de conteúdo do Assets existentes.

* Vários componentes do Assets foram estendidos para atender a fragmentos de conteúdo.

### Uso de fragmentos de conteúdo em páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>O componente de Fragmento de Conteúdo [faz parte dos Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR). Consulte [Desenvolvendo componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=pt-BR) para obter mais detalhes.

Os fragmentos de conteúdo podem ser referenciados a partir de páginas AEM, como qualquer outro tipo de ativo. O AEM fornece o **[componente principal do Fragmento do Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR)** - um componente [&#x200B; que permite incluir fragmentos de conteúdo em suas páginas](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page). Você também pode estender este **[Componente principal do Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=pt-BR)**.

* O componente usa a propriedade `fragmentPath` para fazer referência ao fragmento de conteúdo real. A propriedade `fragmentPath` é tratada da mesma forma que as propriedades semelhantes de outros tipos de ativos; por exemplo, quando o fragmento de conteúdo é movido para outro local.

* O componente permite selecionar a variação a ser exibida.

* Além disso, um intervalo de parágrafos pode ser selecionado para restringir a saída; por exemplo, isso pode ser usado para saída de várias colunas.

* O componente permite conteúdo intermediário:

   * Aqui, o componente permite colocar outros ativos (imagens e assim por diante) entre os parágrafos do fragmento referenciado.

   * Para conteúdo intermediário:

      * Esteja ciente da possibilidade de referências instáveis. O conteúdo intermediário (adicionado ao criar uma página) não tem relação fixa com o parágrafo posicionado ao lado dele. Inserir um novo parágrafo (no editor de fragmento de conteúdo) antes da posição do conteúdo intermediário pode perder a posição relativa.

      * Considere os parâmetros adicionais (como variação e filtros de parágrafo) para configurar o que é renderizado na página.

>[!NOTE]
>
>**Modelo de fragmento de conteúdo:**
>
>Quando um fragmento de conteúdo é usado em uma página, o modelo de fragmento de conteúdo no qual ele se baseia é referenciado.
>
>Isso significa que, se o modelo não tiver sido publicado no momento da publicação da página, ele será sinalizado e o modelo será adicionado aos recursos a serem publicados com a página.

### Integração com outras estruturas {#integration-with-other-frameworks}

Os fragmentos de conteúdo podem ser integrados a:

* **Traduções**

  Os fragmentos de conteúdo são totalmente integrados ao [fluxo de trabalho de tradução do AEM](/help/sites-cloud/administering/translation/overview.md). Em um nível arquitetônico, isso significa:

   * As traduções individuais de um fragmento de conteúdo são fragmentos separados; por exemplo:

      * eles estão localizados em raízes de idioma diferentes, mas compartilham o caminho relativo abaixo da raiz de idioma relevante:

        `/content/dam/<path>/en/<to>/<fragment>`

        vs.

        `/content/dam/<path>/de/<to>/<fragment>`

   * Além dos caminhos baseados em regras, não há outra conexão entre as diferentes versões de idioma de um fragmento de conteúdo. Eles são manipulados como dois fragmentos separados, embora a interface do usuário forneça os meios de navegar entre as variantes de idioma.

  >[!NOTE]
  >
  >O fluxo de trabalho de tradução do AEM funciona com `/content`:
  >
  >* Como os modelos de fragmento de conteúdo residem em `/conf`, eles não são incluídos nessas traduções. É possível internacionalizar as strings da interface do usuário.

* **Esquemas de metadados**

   * Os fragmentos de conteúdo usam e reutilizam os [esquemas de metadados](/help/assets/metadata-schemas.md) que podem ser definidos com ativos padrão.

   * O CFM fornece seu próprio esquema específico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     isso pode ser estendido, se necessário.

   * O respectivo formulário de esquema é integrado ao editor de fragmentos.

## A API de gerenciamento de fragmentos de conteúdo — lado do servidor {#the-content-fragment-management-api-server-side}

Você pode usar a API do lado do servidor para acessar os fragmentos de conteúdo; consulte:

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>A Adobe recomenda usar a API do lado do servidor em vez de acessar diretamente a estrutura de conteúdo.

### Interfaces principais {#key-interfaces}

As três interfaces a seguir podem servir como pontos de entrada:

* **Fragmento de Conteúdo** ([Fragmento de Conteúdo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Essa interface permite trabalhar com um fragmento de conteúdo de forma abstrata.

  A interface fornece os meios para:

   * Gerenciar dados básicos (por exemplo, obter nome; obter/definir título/descrição)
   * Acessar metadados
   * Acessar elementos:

      * Listar elementos
      * Obter elementos por nome
      * Criar elementos (consulte [Avisos](#caveats))

      * Acessar dados do elemento (consulte `ContentElement`)

   * Variações de lista definidas para o fragmento
   * Criar variações globalmente
   * Gerenciar conteúdo associado:

      * Listar coleções
      * Adicionar coleções
      * Remover coleções

   * Acessar o modelo do fragmento

  As interfaces que representam os elementos principais de um fragmento são:

   * **Elemento de Conteúdo** ([ElementoConteúdo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Acessar variações de um elemento:

         * Variações de lista
         * Obter variações por nome
         * Criar variações (consulte [Avisos](#caveats))
         * Remover variações (consulte [Avisos](#caveats))
         * Acessar dados de variação (consulte `ContentVariation`)

      * Atalho para resolver variações (aplicar alguma lógica de fallback adicional específica de implementação se a variação especificada não estiver disponível para um elemento)

   * **Variação de Conteúdo** ([VariaçãoDeConteúdo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Sincronização simples, com base nas informações da última modificação

  Todas as três interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendem a interface `Versionable`, o que adiciona recursos de controle de versão, necessários para fragmentos de conteúdo:

   * Criar uma versão do elemento
   * Listar versões do elemento
   * Obter o conteúdo de uma versão específica do elemento com versão

### Adaptação - Uso de adaptTo() {#adapting-using-adaptto}

Os seguintes podem ser adaptados:

* `ContentFragment` pode ser adaptado para:

   * `Resource` - o recurso Sling subjacente; a atualização do `Resource` subjacente requer diretamente a recompilação do objeto `ContentFragment`.

   * `Asset` - a abstração `Asset` do DAM que representa o fragmento de conteúdo; a atualização de `Asset` requer diretamente a recompilação do objeto `ContentFragment`.

* `ContentElement` pode ser adaptado para:

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para acessar as informações estruturais do elemento.

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` pode ser adaptado para:

   * `ContentFragment`

### Avisos {#caveats}

É de notar que:

* A API inteira foi projetada para **não** manter as alterações automaticamente (a menos que indicado de outra forma no JavaDoc da API). Portanto, sempre confirme o resolvedor de recursos da respectiva solicitação (ou o resolvedor que você está usando na verdade).

* Tarefas que podem exigir esforço adicional:

   * A Adobe recomenda que você crie variações de `ContentFragment`. Isso garante que todos os elementos compartilhem essa variação e que as estruturas de dados globais apropriadas sejam atualizadas conforme necessário para refletir a nova variação na estrutura de conteúdo.

   * A remoção de variações existentes por meio de um elemento, usando `ContentElement.removeVariation()`, não atualiza as estruturas de dados globais atribuídas à variação. Para garantir que essas estruturas de dados sejam mantidas em sincronia, use `ContentFragment.removeVariation()`, que remove uma variação globalmente.

## A API de gerenciamento de fragmentos de conteúdo - Lado do cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>A API do lado do cliente é interna.

### Informações adicionais {#additional-information}

Consulte o link a seguir:

* `filter.xml`

  O `filter.xml` para gerenciamento de fragmento de conteúdo está configurado de forma que não se sobreponha ao pacote de conteúdo principal do Assets.

## Editar sessões {#edit-sessions}

>[!CAUTION]
>
>Considere essas informações de fundo. Você não deve alterar nada aqui (pois está marcado como uma *área privada* no repositório), mas pode ajudar às vezes a entender como as coisas funcionam por baixo dos panos.

A edição de um fragmento de conteúdo, que pode abranger várias visualizações (= páginas de HTML), é atômica. Como esses recursos atômicos de edição de várias visualizações não são um conceito típico de AEM, os fragmentos de conteúdo usam o que é chamado de *sessão de edição*.

Uma sessão de edição é iniciada quando o usuário abre um fragmento de conteúdo no editor. A sessão de edição é concluída quando o usuário sai do editor selecionando **Salvar** ou **Cancelar**.

Tecnicamente, todas as edições são feitas no conteúdo *live*, como em todas as outras edições do AEM. Quando a sessão de edição for iniciada, uma versão do status atual e não editado será criada. Se um usuário cancelar uma edição, essa versão será restaurada. Se o usuário clicar em **Salvar**, nada específico será feito, pois a edição foi executada no conteúdo *live* e, portanto, todas as alterações já serão persistentes. Além disso, clicar em **Salvar** aciona algum processamento em segundo plano, como a criação de informações de pesquisa de texto completo, a manipulação de ativos de mídia mista ou ambos.

Existem algumas medidas de segurança para casos de borda; por exemplo, se o usuário tentar sair do editor sem salvar ou cancelar a sessão de edição. Além disso, um salvamento automático periódico está disponível para evitar perda de dados.
Dois usuários podem editar o mesmo fragmento de conteúdo simultaneamente e, portanto, substituir as alterações um do outro. Para evitar isso, o fragmento de conteúdo deve ser bloqueado aplicando a ação *Check-out* da administração do DAM no fragmento.

## Exemplos {#examples}

### Exemplo: acesso a um fragmento de conteúdo existente {#example-accessing-an-existing-content-fragment}

Para isso, é possível adaptar o recurso que representa a API a:

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

### Exemplo: Criação de um fragmento de conteúdo {#example-creating-a-new-content-fragment}

Para criar um fragmento de conteúdo de forma programática, use um `FragmentTemplate` adaptado de um recurso de modelo.

Por exemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemplo: Especificação do intervalo de salvamento automático {#example-specifying-the-auto-save-interval}

O [intervalo de salvamento automático](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) (medido em segundos) pode ser definido usando o gerenciador de configurações (ConfMgr):

* Nó: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`
* Tipo: `Long`

* Padrão: `600` (10 minutos); definido em `/libs/settings/dam/cfm/jcr:content`

Se você quiser definir um intervalo de salvamento automático de 5 minutos, defina a propriedade no nó.

Por exemplo:

* Nó: `/conf/global/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes para criação de página {#components-for-page-authoring}

Para obter mais informações, consulte

* [Componentes principais - Componente de Fragmento de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) (recomendado)
