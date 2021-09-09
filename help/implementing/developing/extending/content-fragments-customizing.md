---
title: Personalização e extensão de fragmentos de conteúdo
description: Um fragmento de conteúdo estende um ativo padrão.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: c43b55243a73285b78447e32beb16b25608f6d3c
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 2%

---

# Personalização e extensão de fragmentos de conteúdo{#customizing-and-extending-content-fragments}

No Adobe Experience Manager as a Cloud Service, um fragmento de conteúdo estende um ativo padrão; consulte:

* [Criação e gerenciamento de ](/help/assets/content-fragments/content-fragments.md) fragmentos de conteúdo e criação de  [página com ](/help/sites-cloud/authoring/fundamentals/content-fragments.md) fragmentos de conteúdo para obter mais informações sobre fragmentos de conteúdo.

* [Gerenciamento de ](/help/assets/manage-digital-assets.md) ativos para obter mais informações sobre ativos padrão.

## Arquitetura {#architecture}

As [partes constituintes básicas](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de um fragmento de conteúdo são:

* Um *Fragmento de conteúdo*,
* consistindo em um ou mais *Elementos de conteúdo*,
* e que podem ter uma ou mais *Variações de conteúdo*.

Os Fragmentos de conteúdo individuais são baseados nos Modelos de fragmento de conteúdo:

* Os modelos de fragmento de conteúdo definem a estrutura de um fragmento de conteúdo quando ele é criado.
* Um fragmento faz referência ao modelo; portanto, as alterações no modelo podem/afetarão qualquer fragmento dependente.
* Os modelos são incorporados aos tipos de dados.
* As funções para adicionar novas variações, etc., precisam atualizar o fragmento adequadamente.

   >[!NOTE]
   >
   >Para que você exiba/renderize um Fragmento de conteúdo, sua conta deve ter `read` permissões para o modelo.

   >[!CAUTION]
   >
   >Quaisquer alterações em um modelo de fragmento de conteúdo existente podem afetar fragmentos dependentes; isso pode levar a propriedades órfãs nesses fragmentos.

### Integração de sites com ativos {#integration-of-sites-with-assets}

O Gerenciamento de fragmentos de conteúdo (CFM) faz parte do AEM Assets como:

* Fragmentos de conteúdo são ativos.
* Eles usam a funcionalidade Ativos existente.
* Eles são totalmente integrados aos Ativos (consoles de administrador etc.).

Fragmentos de conteúdo são considerados um recurso de Sites como:

* Elas são usadas ao criar suas páginas.

#### Mapeamento de fragmentos de conteúdo para ativos {#mapping-content-fragments-to-assets}

![fragmento de conteúdo para ativos](assets/content-fragment-to-assets.png)

Fragmentos de conteúdo, com base em um modelo de fragmento de conteúdo, são mapeados para um único ativo:

* Todo o conteúdo é armazenado no nó `jcr:content/data` do ativo:

   * Os dados do elemento são armazenados no subnó principal :
      `jcr:content/data/master`

   * As variações são armazenadas em um subnó que leva o nome da variação:
por exemplo `jcr:content/data/myvariation`

   * Os dados de cada elemento são armazenados no respectivo subnó como uma propriedade com o nome do elemento:
Por exemplo, o conteúdo do elemento `text` é armazenado como propriedade `text` em `jcr:content/data/master`

* Os metadados e o conteúdo associado são armazenados abaixo de `jcr:content/metadata`
Exceto o título e a descrição, que não são considerados metadados tradicionais e armazenados em 
`jcr:content`

#### Localização do ativo {#asset-location}

Como ocorre com os ativos padrão, um fragmento de conteúdo é mantido em:

`/content/dam`

#### Permissões de ativos {#asset-permissions}

Para obter mais detalhes, consulte [Fragmento de conteúdo - Excluir considerações](/help/assets/content-fragments/content-fragments-delete.md).

#### Integração de recursos {#feature-integration}

Para integrar com o núcleo dos ativos:

* O recurso de Gerenciamento de fragmento de conteúdo (CFM) baseia-se no núcleo de Ativos.

* O CFM fornece suas próprias implementações para itens nas visualizações de cartão/coluna/lista; essas são as implementações de renderização de conteúdo do Assets existentes.

* Vários componentes de Ativos foram estendidos para atender a fragmentos de conteúdo.

### Uso de fragmentos de conteúdo em páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>O componente [Fragmento de conteúdo é parte dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html). Consulte [Desenvolvimento de componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) para obter mais detalhes.

Os fragmentos de conteúdo podem ser referenciados AEM páginas, como qualquer outro tipo de ativo. AEM fornece o **[Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)** - um componente [que permite incluir fragmentos de conteúdo em suas páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Você também pode estender esse componente principal **[Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)**.

* O componente usa a propriedade `fragmentPath` para fazer referência ao fragmento de conteúdo real. A propriedade `fragmentPath` é tratada da mesma maneira que as propriedades semelhantes de outros tipos de ativos; por exemplo, quando o fragmento de conteúdo é movido para outro local.

* O componente permite selecionar a variação a ser exibida.

* Além disso, um intervalo de parágrafos pode ser selecionado para restringir a saída; por exemplo, isso pode ser usado para saída de várias colunas.

* O componente permite conteúdo intermediário:

   * Aqui, o componente permite colocar outros ativos (imagens, etc.) entre os parágrafos do fragmento referenciado.

   * Para conteúdo intermediário, é necessário:

      * Estar ciente da possibilidade de referências instáveis; o conteúdo intermediário (adicionado ao criar uma página) não tem relacionamento fixo com o parágrafo ao lado do qual está posicionado, inserindo um novo parágrafo (no editor de fragmentos de conteúdo) antes que a posição do conteúdo intermediário possa perder a posição relativa

      * considere os parâmetros adicionais (como filtros de variação e parágrafo) para configurar o que é renderizado na página

>[!NOTE]
>
>**Modelo de fragmentos de conteúdo:**
>
>Quando um fragmento de conteúdo é usado em uma página, o modelo do fragmento de conteúdo no qual ele é baseado é referenciado.
>
>Isso significa que, se o modelo não tiver sido publicado no momento em que você publicar a página, ela será sinalizada e o modelo será adicionado aos recursos a serem publicados com a página.

### Integração com outros quadros {#integration-with-other-frameworks}

Os fragmentos de conteúdo podem ser integrados com:

* **Traduções**

   Os Fragmentos de conteúdo são totalmente integrados ao [AEM fluxo de trabalho de tradução](/help/sites-cloud/administering/translation/overview.md). A nível arquitetônico, isso significa:

   * As traduções individuais de um fragmento de conteúdo são, na verdade, fragmentos separados; por exemplo:

      * Estejam localizados sob raízes linguísticas diferentes; mas compartilham exatamente o mesmo caminho relativo abaixo da raiz de idioma relevante:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Além dos caminhos baseados em regras, não há mais conexão entre as diferentes versões linguísticas de um fragmento de conteúdo; eles são tratados como dois fragmentos separados, embora a interface do usuário forneça os meios de navegar entre as variantes de idioma.
   >[!NOTE]
   >
   >O fluxo de trabalho de tradução AEM funciona com `/content`:
   >
   >* Como os modelos de fragmento de conteúdo residem em `/conf`, eles não são incluídos nessas traduções. Você pode internacionalizar as cadeias de caracteres da interface do usuário.


* **Esquemas de metadados**

   * Fragmentos de conteúdo (re)use os [esquemas de metadados](/help/assets/metadata-schemas.md), que podem ser definidos com ativos padrão.

   * O CFM fornece seu próprio schema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      isso pode ser estendido se necessário.

   * O respectivo formulário de esquema é integrado ao editor de fragmentos.

## A API de gerenciamento de fragmentos de conteúdo - do lado do servidor {#the-content-fragment-management-api-server-side}

Você pode usar a API do lado do servidor para acessar os fragmentos de conteúdo; consulte:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>É altamente recomendável usar a API do lado do servidor em vez de acessar diretamente a estrutura de conteúdo.

### Principais interfaces {#key-interfaces}

As três interfaces a seguir podem servir como pontos de entrada:

* **Fragmento de conteúdo**  ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Essa interface permite que você trabalhe com um fragmento de conteúdo de forma abstrata.

   A interface fornece os meios para:

   * Gerenciar dados básicos (por exemplo, obter nome; get/set title/description)
   * Acessar metadados
   * Elementos de acesso:

      * Elementos de lista
      * Obter elementos por nome
      * Criar novos elementos (consulte [Avisos](#caveats))

      * Acessar dados do elemento (consulte `ContentElement`)
   * Listar variações definidas para o fragmento
   * Criar novas variações globalmente
   * Gerenciar conteúdo associado:

      * Listar coleções
      * Adicionar coleções
      * Remover coleções
   * Acessar o modelo do fragmento

   As interfaces que representam os elementos principais de um fragmento são:

   * **Elemento de conteúdo**  ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Variações de acesso de um elemento:

         * Listar variações
         * Obter variações por nome
         * Criar novas variações (consulte [Avisos](#caveats))
         * Remover variações (consulte [Avisos](#caveats))
         * Acesse os dados de variação (consulte `ContentVariation`)
      * Atalho para resolver variações (aplicando alguma lógica de fallback adicional específica da implementação se a variação especificada não estiver disponível para um elemento)
   * **Variação de conteúdo**  ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obter dados básicos (nome, título, descrição)
      * Obter/definir conteúdo
      * Sincronização simples, com base nas informações da última modificação

   Todas as três interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendem a interface `Versionable`, que adiciona recursos de controle de versão, necessários para fragmentos de conteúdo:

   * Criar nova versão do elemento
   * Versões de lista do elemento
   * Obter o conteúdo de uma versão específica do elemento com versão







### Adaptação - Uso de adaptTo() {#adapting-using-adaptto}

Podem ser adaptadas as seguintes condições:

* `ContentFragment` pode ser adaptado para:

   * `Resource` - o recurso Sling subjacente; a atualização do subjacente  `Resource` diretamente requer a reconstrução do  `ContentFragment` objeto.

   * `Asset` - a  `Asset` abstração do DAM que representa o fragmento de conteúdo; para atualizar o  `Asset` diretamente, é necessário reconstruir o  `ContentFragment` objeto.

* `ContentElement` pode ser adaptado para:

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para aceder às informações estruturais do elemento.

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` pode ser adaptado para:

   * `ContentFragment`

### Avisos {#caveats}

Note-se que:

* A API inteira foi projetada para **not** persistir alterações automaticamente (a menos que observado de outra forma no JavaDoc da API). Portanto, sempre será necessário confirmar o resolvedor de recursos da respectiva solicitação (ou o resolvedor que você está realmente usando).

* Tarefas que podem exigir esforço adicional:

   * É altamente recomendável criar novas variações a partir de `ContentFragment`. Isso garante que todos os elementos compartilhem essa variação e que as estruturas de dados globais apropriadas sejam atualizadas, conforme necessário, para refletir a variação recém-criada na estrutura do conteúdo.

   * Remover variações existentes por meio de um elemento, usando `ContentElement.removeVariation()`, não atualizará as estruturas de dados globais atribuídas à variação. Para garantir que essas estruturas de dados sejam mantidas em sincronia, use `ContentFragment.removeVariation()`, o que remove uma variação globalmente.

## A API de gerenciamento de fragmento de conteúdo - Lado do cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>A API do lado do cliente é interna.

### Informações adicionais {#additional-information}

Consulte o link a seguir:

* `filter.xml`

   O `filter.xml` para gerenciamento de fragmentos de conteúdo é configurado de forma que não se sobreponha ao pacote de conteúdo principal do Assets.

## Editar sessões {#edit-sessions}

>[!CAUTION]
>
>Considere esta informação de base. Você não deve alterar nada aqui (pois está marcado como uma *área privada* no repositório), mas pode ajudar em alguns casos a entender como as coisas funcionam sob o capô.

A edição de um fragmento de conteúdo, que pode abranger várias exibições (= páginas HTML), é atômica. Como esses recursos atômicos de edição de várias exibições não são um conceito típico de AEM, os fragmentos de conteúdo usam o que é chamado de *sessão de edição*.

Uma sessão de edição é iniciada quando o usuário abre um fragmento de conteúdo no editor. A sessão de edição é concluída quando o usuário deixa o editor selecionando **Salvar** ou **Cancelar**.

Tecnicamente, todas as edições são feitas no conteúdo *live*, assim como com todas as outras edições AEM. Quando a sessão de edição é iniciada, uma versão do status atual e não editado é criada. Se um usuário cancelar uma edição, essa versão será restaurada. Se o usuário clicar em **Salvar**, nada específico será feito, pois toda a edição foi executada no conteúdo *live*, portanto, todas as alterações já são persistentes. Além disso, clicar em **Salvar** acionará algum processamento em segundo plano (como criar informações de pesquisa de texto completo e/ou manipular ativos de mídia mista).

Existem algumas medidas de segurança para os casos de borda; por exemplo, se o usuário tentar sair do editor sem salvar ou cancelar a sessão de edição. Além disso, um salvamento automático periódico está disponível para evitar perda de dados.
Observe que dois usuários podem editar o mesmo fragmento de conteúdo simultaneamente e, portanto, podem substituir as alterações um do outro. Para evitar isso, o fragmento de conteúdo precisa ser bloqueado aplicando a ação *Checkout* da administração do DAM no fragmento.

## Exemplos {#examples}

### Exemplo: Acesso a um fragmento de conteúdo existente {#example-accessing-an-existing-content-fragment}

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

### Exemplo: Criação de um novo fragmento de conteúdo {#example-creating-a-new-content-fragment}

Para criar um novo fragmento de conteúdo programaticamente, você precisa usar um
`FragmentTemplate` adaptado de um recurso de modelo.

Por exemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exemplo: Especificação do intervalo de salvamento automático {#example-specifying-the-auto-save-interval}

O [intervalo de salvamento automático](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions) (medido em segundos) pode ser definido usando o gerenciador de configuração (ConfMgr):

* Nó: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`
* Tipo: `Long`

* Padrão: `600` (10 minutos); isso é definido em `/libs/settings/dam/cfm/jcr:content`

Para definir um intervalo de salvamento automático de 5 minutos, é necessário definir a propriedade no nó ; por exemplo:

* Nó: `/conf/global/settings/dam/cfm/jcr:content`
* Nome da Propriedade: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes da autoria de página {#components-for-page-authoring}

Para obter mais informações, consulte

* [Componentes principais - Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)  (recomendado)
